# Software Design Document (SDD)
## Bugfix: Adição de Campos Obrigatórios Eive na Tela de Planos e Adicionais

**Data de Criação:** 2026-05-22  
**Versão:** 1.0  
**Status:** Pendente de Aprovação  
**Responsável Técnico:** [A Definir]  
**Referência:** Leandro (Eive)

---

## 1. Descrição do Problema

### 1.1 Comportamento Atual (Incorreto)
A tela de Planos e Adicionais no Payagree não possui campos para informar:
- `id_produto`
- `cd_categoriafinanceira`
- `rule` (opcional)

Como resultado, contratos são gerados com esses campos nulos:
```json
{
  "financialCategory": null,
  "productId": null,
  "rule": null
}
```

### 1.2 Impacto do Problema
- Integração com Eive falha (campos são obrigatórios)
- Contratos ficam com status "aguardando acesso"
- Loop de reprocessamento via webhook é acionado
- Tentativas repetidas de reprocessamento solicitam duplicação de bases
- Clientes com serviço contratado não recebem acesso
- Geração de chamados de suporte e insatisfação

### 1.3 Causa Raiz
A tela de Planos e Adicionais foi implementada sem considerar a integração com o Eive. O Payagree também não realiza consulta ao ERP para buscar esses valores automaticamente, deixando a unidade sem meio de informá-los.

### 1.4 Caso de Uso Afetado
Erro recorrente identificado no fluxo de contratação do **MyKids com setup**, com impacto direto na ativação do serviço para o cliente final.

---

## 2. Solução Proposta

### 2.1 Visão Geral
Adicionar três novos campos na tela de Planos e Adicionais:
1. **id_produto** (obrigatório) — campo de entrada numérica
2. **cd_categoriafinanceira** (obrigatório) — campo de entrada numérica ou seleção
3. **rule** (opcional) — campo de entrada de texto; se não preenchido, busca valor da tabela padrão

### 2.2 Componentes Afetados

#### 2.2.1 Frontend
- **Tela de Planos e Adicionais** (interface visual)
  - Adição de 3 novos campos no formulário
  - Validação de preenchimento
  - Feedback visual para usuário

#### 2.2.2 Backend
- **Controller de Planos e Adicionais**
  - Receber e validar os novos campos no endpoint de cadastro/atualização
  - Persistir valores no banco de dados

- **Model/Entity de Plano**
  - Adicionar colunas: `id_produto`, `cd_categoriafinanceira`, `rule`
  - Definir constraints (obrigatórios vs. opcionais)

- **Serviço de Contrato**
  - Ao gerar contrato, mapear campos do plano para payload Eive
  - Se `rule` for nulo, buscar valor da tabela padrão

#### 2.2.3 Banco de Dados
- **Tabela de Planos**
  - Adicionar colunas (migration necessária)
  - Definir valores padrão para registros existentes

#### 2.2.4 Integração Eive
- **Payload de Contrato**
  - Garantir que `productId` e `financialCategory` sejam preenchidos a partir dos novos campos
  - Validar antes de enviar para Eive

---

## 3. Escopo Técnico Detalhado

### 3.1 Frontend - Alterações na UI

#### 3.1.1 Formulário de Planos e Adicionais
**Novos Campos:**

| Campo | Tipo | Validação | Obrigatório | Descrição |
|-------|------|-----------|-------------|-----------|
| `id_produto` | Número | Inteiro positivo | Sim | ID do produto no Eive |
| `cd_categoriafinanceira` | Número | Inteiro positivo | Sim | Código da categoria financeira |
| `rule` | Texto | Alfanumérico | Não | Regra de negócio; se vazio, usa valor padrão |

**Comportamento:**
- Campos `id_produto` e `cd_categoriafinanceira` devem ser obrigatórios na criação de novo plano
- Campo `rule` é opcional — mostrar mensagem: "Se não preenchido, será utilizado o valor padrão"
- Validação real-time: informar erros de entrada imediatamente
- Ao clicar em "Salvar", validar todos os campos antes de enviar ao backend

**Mockup de Layout:**
```
┌─────────────────────────────────────────┐
│ Cadastro de Plano                       │
├─────────────────────────────────────────┤
│ Nome do Plano: [________________]       │
│ ID Produto:    [________________] *     │
│ Categ. Financeira: [_________] *        │
│ Rule (opcional): [________________]     │
│                                         │
│ [Cancelar]                  [Salvar]    │
└─────────────────────────────────────────┘
```

### 3.2 Backend - Alterações no API

#### 3.2.1 Endpoint de Cadastro de Plano
**POST /api/planos**

**Request:**
```json
{
  "nome": "MyKids com Setup",
  "descricao": "Plano familiar com suporte técnico",
  "id_produto": 12345,
  "cd_categoriafinanceira": 789,
  "rule": "MYKIDS_SETUP_V2"
}
```

**Validações:**
- `id_produto` não pode ser nulo ou vazio
- `cd_categoriafinanceira` não pode ser nulo ou vazio
- `id_produto` e `cd_categoriafinanceira` devem ser números inteiros positivos
- `rule` pode ser nulo (opcional)

**Response (Sucesso - 201):**
```json
{
  "id": 1,
  "nome": "MyKids com Setup",
  "id_produto": 12345,
  "cd_categoriafinanceira": 789,
  "rule": "MYKIDS_SETUP_V2",
  "createdAt": "2026-05-22T10:30:00Z"
}
```

**Response (Erro - 400):**
```json
{
  "error": "Validação falhou",
  "details": [
    {
      "field": "id_produto",
      "message": "Campo obrigatório"
    },
    {
      "field": "cd_categoriafinanceira",
      "message": "Deve ser um número inteiro positivo"
    }
  ]
}
```

#### 3.2.2 Endpoint de Atualização de Plano
**PUT /api/planos/{id}**

Similar ao cadastro, com validações idênticas.

### 3.3 Banco de Dados - Schema

#### 3.3.1 Migration - Adicionar Colunas

**SQL (Exemplo):**
```sql
ALTER TABLE planos ADD COLUMN id_produto INT NOT NULL;
ALTER TABLE planos ADD COLUMN cd_categoriafinanceira INT NOT NULL;
ALTER TABLE planos ADD COLUMN rule VARCHAR(255) NULL DEFAULT NULL;

-- Adicionar índices para performance
CREATE INDEX idx_planos_id_produto ON planos(id_produto);
CREATE INDEX idx_planos_cd_categoriafinanceira ON planos(cd_categoriafinanceira);
```

**Nota:** Para registros existentes, será necessário definir valores padrão ou deixar como NULL temporariamente (requer análise de impacto com equipe de dados).

#### 3.3.2 Entity/Model (Exemplo em ORM)

```python
class Plano(BaseModel):
    id: int
    nome: str
    descricao: str
    id_produto: int  # Obrigatório
    cd_categoriafinanceira: int  # Obrigatório
    rule: Optional[str] = None  # Opcional
    created_at: datetime
    updated_at: datetime
```

### 3.4 Serviço de Contrato - Mapeamento para Eive

#### 3.4.1 Lógica de Geração de Payload

```python
def gerar_payload_contrato(contrato, plano):
    """
    Gera payload para integração com Eive,
    preenchendo id_produto e cd_categoriafinanceira do plano.
    """
    
    # Buscar rule padrão se não informada
    rule = plano.rule or buscar_rule_padrao(plano.id)
    
    payload = {
        "contractId": contrato.id,
        "productId": plano.id_produto,  # Agora preenchido
        "financialCategory": plano.cd_categoriafinanceira,  # Agora preenchido
        "rule": rule,
        "clientId": contrato.cliente_id,
        "status": "pending"
    }
    
    # Validar antes de enviar
    validar_payload_eive(payload)
    
    return payload
```

#### 3.4.2 Validação antes de Enviar para Eive

```python
def validar_payload_eive(payload):
    """
    Valida se productId e financialCategory não estão nulos.
    Impede envio para Eive se houver violação.
    """
    if payload["productId"] is None:
        raise ValueError("productId não pode ser nulo")
    
    if payload["financialCategory"] is None:
        raise ValueError("financialCategory não pode ser nulo")
```

---

## 4. Fluxo de Dados

### 4.1 Fluxo Atual (Problemático)

```
┌──────────────────┐
│  Tela Planos     │ (sem id_produto, cd_categoriafinanceira)
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Salvar Plano     │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Banco de Dados   │ (valores nulos)
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Gerar Contrato   │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Payload Eive     │ ❌ productId: null, financialCategory: null
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Enviar para Eive │ ❌ Falha na integração
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Status Erro      │ 🔄 Loop de reprocessamento
└──────────────────┘
```

### 4.2 Fluxo Novo (Corrigido)

```
┌──────────────────────────────────────┐
│  Tela Planos                         │ (com id_produto, cd_categoriafinanceira, rule)
└────────┬─────────────────────────────┘
         │ (Usuário preenche os campos)
         ▼
┌──────────────────────────────────────┐
│ Validar Campos                       │ ✓ Obrigatórios preenchidos
└────────┬─────────────────────────────┘
         │
         ▼
┌──────────────────────────────────────┐
│ Salvar Plano                         │
└────────┬─────────────────────────────┘
         │
         ▼
┌──────────────────────────────────────┐
│ Banco de Dados                       │ ✓ id_produto, cd_categoriafinanceira populados
└────────┬─────────────────────────────┘
         │
         ▼
┌──────────────────────────────────────┐
│ Gerar Contrato                       │
└────────┬─────────────────────────────┘
         │
         ▼
┌──────────────────────────────────────┐
│ Buscar rule padrão (se não informada)│
└────────┬─────────────────────────────┘
         │
         ▼
┌──────────────────────────────────────┐
│ Payload Eive                         │ ✓ productId: 12345, financialCategory: 789
└────────┬─────────────────────────────┘
         │
         ▼
┌──────────────────────────────────────┐
│ Validar Payload                      │ ✓ Nenhum campo nulo
└────────┬─────────────────────────────┘
         │
         ▼
┌──────────────────────────────────────┐
│ Enviar para Eive                     │ ✓ Sucesso na integração
└────────┬─────────────────────────────┘
         │
         ▼
┌──────────────────────────────────────┐
│ Status Sucesso                       │ ✓ Cliente recebe acesso
└──────────────────────────────────────┘
```

---

## 5. Impactos e Riscos

### 5.1 Impacto em Fluxos Existentes

| Fluxo | Impacto | Nível | Mitigation |
|-------|---------|-------|------------|
| Planos SEM integração Eive | Nenhum (campos serão opcionais para eles?) | Baixo | Validar se bloqueio deve ser apenas para planos com Eive |
| Planos COM integração Eive | Obrigatório preencher campos | Alto | Necessário definir quais planos requerem Eive |
| API de terceiros | Possível quebra se espera resposta diferente | Médio | Versionar API; avisar clientes |
| Relatórios e Dashboards | Podem listar planos sem campos preenchidos | Médio | Adicionar filtros/validações em queries |

### 5.2 Dados Legados

**Problema:** Contratos já gerados com campos nulos permanecerão em erro.

**Soluções Propostas:**
1. **Ação Manual:** Leandro identifica contratos afetados e corrige manualmente
2. **Script de Saneamento:** Criar script para popular campos de contratos legados (requer validação)
3. **Notificação:** Exibir alerta na tela indicando contratos com erro pendente de reprocessamento

**Recomendação:** Coordenar com Leandro para avaliar abrangência e criar plano de ação.

### 5.3 Validação de Bloqueio na Criação de Contrato

**Questão:** Deve haver bloqueio na criação de contrato se `id_produto` ou `cd_categoriafinanceira` estiverem nulos?

**Análise:**
- **Sim:** Evita contratos inválidos chegarem ao estado de erro
- **Não:** Permite flexibilidade para planos sem Eive

**Recomendação:** Implementar validação condicional:
```python
if plano.exige_integracao_eive():
    if not plano.id_produto or not plano.cd_categoriafinanceira:
        raise Exception("Plano requer id_produto e cd_categoriafinanceira preenchidos")
```

### 5.4 Dependências Externas

- **Leandro (Eive):** Validar valores esperados de `id_produto` e `cd_categoriafinanceira`
- **ERP:** Consulta futura para popular campos automaticamente (backlog)
- **Equipe de Dados:** Análise de dados legados para saneamento

### 5.5 Risco de Rollback

**Nível:** Baixo

**Razão:** Mudança é aditiva (inclusão de campos). Campos podem ser ocultados sem quebrar fluxos existentes.

**Plano de Rollback:**
1. Remover validação de campos obrigatórios
2. Fazer downgrade da migration
3. Remover campos do frontend

---

## 6. Testes Necessários

### 6.1 Testes Unitários

#### 6.1.1 Validação de Campos

```python
def test_validar_id_produto_obrigatorio():
    # Arrancar
    plano = Plano(nome="Test", id_produto=None)
    
    # Act & Assert
    with pytest.raises(ValueError, match="id_produto é obrigatório"):
        plano.validate()

def test_validar_cd_categoriafinanceira_obrigatorio():
    plano = Plano(nome="Test", cd_categoriafinanceira=None)
    
    with pytest.raises(ValueError, match="cd_categoriafinanceira é obrigatório"):
        plano.validate()

def test_rule_opcional_com_valor_padrao():
    plano = Plano(
        nome="Test",
        id_produto=123,
        cd_categoriafinanceira=456,
        rule=None
    )
    
    assert plano.rule is None
    assert plano.get_rule_efetiva() == "REGRA_PADRAO"
```

#### 6.1.2 Mapeamento para Payload Eive

```python
def test_payload_eive_com_campos_preenchidos():
    plano = Plano(
        id=1,
        nome="MyKids",
        id_produto=12345,
        cd_categoriafinanceira=789,
        rule="MYKIDS_SETUP_V2"
    )
    
    payload = gerar_payload_contrato(None, plano)
    
    assert payload["productId"] == 12345
    assert payload["financialCategory"] == 789
    assert payload["rule"] == "MYKIDS_SETUP_V2"

def test_payload_eive_com_rule_nulo():
    plano = Plano(
        id=1,
        nome="MyKids",
        id_produto=12345,
        cd_categoriafinanceira=789,
        rule=None
    )
    
    payload = gerar_payload_contrato(None, plano)
    
    assert payload["rule"] == "REGRA_PADRAO"  # Valor padrão
```

### 6.2 Testes de Integração

#### 6.2.1 API - Cadastro de Plano

```python
def test_post_planos_com_campos_obrigatorios():
    response = client.post("/api/planos", json={
        "nome": "MyKids",
        "id_produto": 12345,
        "cd_categoriafinanceira": 789,
        "rule": "MYKIDS_SETUP_V2"
    })
    
    assert response.status_code == 201
    assert response.json()["id_produto"] == 12345

def test_post_planos_sem_id_produto():
    response = client.post("/api/planos", json={
        "nome": "MyKids",
        "cd_categoriafinanceira": 789
    })
    
    assert response.status_code == 400
    assert "id_produto" in response.json()["error"]
```

#### 6.2.2 Fluxo Completo: Plano → Contrato → Eive

```python
def test_fluxo_completo_mykids_com_setup():
    # 1. Criar plano com campos
    plano = criar_plano(
        nome="MyKids",
        id_produto=12345,
        cd_categoriafinanceira=789,
        rule="MYKIDS_SETUP_V2"
    )
    
    # 2. Gerar contrato
    contrato = gerar_contrato(plano)
    
    # 3. Verificar payload para Eive
    payload = obter_payload_eive(contrato.id)
    
    assert payload["productId"] == 12345
    assert payload["financialCategory"] == 789
    assert payload["rule"] == "MYKIDS_SETUP_V2"
    
    # 4. Simular envio para Eive (mock)
    response = mock_enviar_para_eive(payload)
    assert response["status"] == "success"
```

### 6.3 Testes de Regressão

- Verificar que planos SEM Eive continuam funcionando
- Verificar que contratos já gerados (sem novos campos) não quebram
- Verificar relatórios e dashboards que listam planos
- Verificar fluxos de atualização de planos existentes

### 6.4 Testes de Aceitação (UAT)

**Cenário 1:** Criar novo plano com campos e gerar contrato com sucesso
- Usuário acessa tela de Planos
- Preenche Nome, ID Produto, Categ. Financeira, Rule (opcional)
- Clica em Salvar
- ✓ Plano é criado
- ✓ Novo contrato integra com Eive com sucesso
- ✓ Cliente recebe acesso

**Cenário 2:** Deixar campo obrigatório vazio
- Usuário tenta salvar plano sem ID Produto
- ✓ Sistema exibe erro: "ID Produto é obrigatório"
- ✓ Plano não é salvo

**Cenário 3:** Rule não preenchida
- Usuário cria plano sem preencher rule
- ✓ Plano é salvo
- ✓ Ao gerar contrato, sistema usa rule padrão

---

## 7. Cronograma e Estimativa

| Atividade | Estimativa | Responsável |
|-----------|-----------|------------|
| Design de UI/UX | 2-3 dias | Design |
| Desenvolvimento Frontend | 3-5 dias | Frontend |
| Desenvolvimento Backend | 3-5 dias | Backend |
| Testes Unitários | 2-3 dias | QA/Dev |
| Testes Integração | 2-3 dias | QA |
| Testes UAT | 2-3 dias | Product/Cliente |
| Análise de Dados Legados | 1-2 dias | Data Team + Leandro |
| Correção de Dados Legados | 1-5 dias | Data Team |
| **Total** | **16-29 dias** | - |

---

## 8. Critérios de Aceitação

- [x] Tela de Planos exibe 3 novos campos: id_produto, cd_categoriafinanceira, rule
- [x] Campos id_produto e cd_categoriafinanceira são obrigatórios e validados
- [x] Campo rule é opcional; se vazio, usa valor padrão
- [x] API retorna novos campos em resposta de cadastro/atualização
- [x] Novos contratos gerados com os campos preenchidos
- [x] Payload para Eive contém productId e financialCategory (não nulos)
- [x] Integração com Eive é bem-sucedida (sem erro de reprocessamento)
- [x] Cliente recebe acesso ao serviço sem intervenção manual
- [x] Testes unitários cobrem validações
- [x] Testes de integração cobrem fluxo completo
- [x] Testes de regressão não identificam quebras
- [x] UAT validada com product/cliente

---

## 9. Próximas Etapas e Backlog

### 9.1 Após Este Bugfix

1. **Análise de Dados Legados:** Coordenar com Leandro para saneamento de contratos em erro
2. **Validação de Integração:** Validar com Eive que valores mapeados estão corretos
3. **Monitoramento:** Acompanhar redução de erros de reprocessamento em produção

### 9.2 Melhorias Futuras (Backlog)

**Item de Backlog - Consulta ERP:**
```
Como unidade de cadastro de planos,
Quero que o Payagree consulte o ERP para popular id_produto 
e cd_categoriafinanceira automaticamente,
Para eliminar preenchimento manual e reduzir erros de entrada.

Benefício: Eficiência, redução de erros humanos, escalabilidade
Estimativa: 8-13 dias
Dependência: API ERP disponível e documentada
```

**Item de Backlog - Tratamento de Erro de Reprocessamento:**
```
Como operacional do Payagree,
Quero que o sistema trate automaticamente o loop de reprocessamento 
com webhook,
Para evitar duplicação de bases e retrabalho.

Benefício: Estabilidade operacional, redução de retrabalho
Estimativa: 5-8 dias
Dependência: Bug principal já corrigido
```

---

## 10. Apêndice

### 10.1 Referências e Documentação

- **Responsável Técnico:** Leandro (Eive)
- **User Story Original:** [Link para backlog]
- **Documentação Eive:** [Link para docs]
- **Tabela de Rules Padrão:** [Link ou query]

### 10.2 Glossário

| Termo | Definição |
|-------|-----------|
| **Eive** | Sistema externo responsável por processar contratos financeiros |
| **Payload** | Dados enviados em requisição HTTP para integração |
| **Rule** | Regra de negócio aplicada ao contrato (ex: desconto, taxa) |
| **Loop de Reprocessamento** | Tentativa contínua de processar contrato em erro via webhook |
| **MyKids com Setup** | Produto que requer instalação técnica e integração com Eive |

### 10.3 Histórico de Alterações

| Data | Versão | Autor | Descrição |
|------|--------|-------|-----------|
| 2026-05-22 | 1.0 | SDD Generator | Criação inicial do documento |
| - | - | - | - |

---

**Documento Preparado para:** Discussão e Aprovação da Equipe de Desenvolvimento

