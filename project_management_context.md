# Gestão do Projeto e Ciclo de Desenvolvimento

> **Como preencher:** registre aqui como o projeto é gerenciado — onde o trabalho vive, como está organizado e como o time opera no dia a dia. Qualquer pessoa que entre no projeto deve conseguir entender o fluxo de trabalho lendo este documento.
> **Caminho:** `02-systems/{sistema}/management/project-management.md`

---

## Plataforma de Gestão

**Plataforma:** GitHub Projects
**URL / Acesso:** Não informado
**Como solicitar acesso:** Pelo responsável do projeto / PO

---

## Modelo de Organização do Trabalho

> Defina o significado de cada nível da hierarquia de trabalho neste projeto. Sem essa definição, cada pessoa do time interpreta os conceitos de forma diferente.

| Nível | Nome utilizado | O que representa | Exemplo |
|---|---|---|---|
| 1 — mais alto | Epic | Grande bloco de entrega ligado a uma área principal do produto | Cadastro de usuários e pets |
| 2 | Feature | Funcionalidade relevante dentro de um Epic | Cadastro de pets disponíveis |
| 3 | PBI / Story | Entrega pequena, refinada e implementável em um ciclo | Formulário de cadastro de pet |
| 4 — mais baixo | Task | Atividade técnica dentro de um PBI | Criar validação do formulário |

---

## Tamanho e Critérios de um PBI

**Tamanho máximo:** Um PBI deve ser pequeno o suficiente para ser concluído e testado dentro de um ciclo de sprint, preferencialmente por um desenvolvedor sem se tornar uma entrega longa ou dependente de múltiplos fluxos.

**Um bom PBI deve:**
- Ter um critério de aceite claro e verificável
- Poder ser desenvolvido e testado de forma independente
- Ser pequeno o suficiente para caber em um ciclo
- Ter valor de negócio ou técnico identificável

**Um PBI deve ser quebrado quando:**
- Possuir mais de uma responsabilidade principal
- Depender fortemente de outro PBI para poder ser validado
- Ficar grande a ponto de comprometer a entrega dentro da sprint

---

## Modelo de Desenvolvimento

**Metodologia:** Scrum com decisões complementadas por poker planning nas sprints

**Duração do ciclo:** Sprints

**Início do ciclo:** Não informado

---

## Cerimônias e Rituais

> Liste apenas as cerimônias que este time realmente pratica. Remova as que não se aplicam.

| Cerimônia | Frequência | Duração | Objetivo |
|---|---|---|---|
| Planning | A cada sprint | Não informado | Definir prioridade e planejar as entregas do ciclo |
| Poker planning | Durante o planejamento da sprint | Não informado | Estimar e alinhar o esforço dos itens |
| Review | A cada sprint | Não informado | Revisar o que foi entregue |
| Retrospectiva | A cada sprint | Não informado | Ajustar o processo do time |
| Refinamento | Conforme necessidade | Não informado | Preparar itens para próxima sprint |

---

## Fluxo de Status

> Defina os status que um item percorre desde a criação até a entrega. Mapeie exatamente como está configurado na plataforma de gestão.

| Status | Descrição | Quem move para cá |
|---|---|---|
| Backlog | Item criado e ainda não iniciado | PO / time |
| Em refinamento | Item sendo detalhado para entrar em uma sprint | PO / time |
| Pronto para desenvolvimento | Item refinado e apto para execução | Time |
| Em desenvolvimento | Item em execução | Desenvolvedor responsável |
| Em revisão | Pull request aberto e aguardando validação | Desenvolvedor que finalizou |
| Concluído | Item entregue e aceito | PO após validação |

---

## Definição de Pronto (Definition of Done)

> Um item só pode ser marcado como Done quando todos os critérios abaixo forem atendidos. Esta lista é do time — ajuste conforme a realidade do projeto.

- Código revisado por outro desenvolvedor
- Testes automatizados passando
- Funcionalidade validada pelo PO quando aplicável
- Interface e fluxo aderentes ao esperado
- Documentação atualizada quando houver impacto relevante
- Deploy feito no ambiente definido, quando aplicável

---

## Acompanhamento e Monitoramento

**Responsável pelo acompanhamento:** PO

**Métricas acompanhadas:**

| Métrica | O que mede | Onde é acompanhada | Frequência |
|---|---|---|---|
| Velocity | Quantidade de trabalho entregue por sprint | GitHub Projects / planning do time | A cada sprint |
| Itens concluídos | Volume de entregas finalizadas no ciclo | GitHub Projects | A cada sprint |
| Bloqueios | Itens travados por dependência ou dúvida | Reuniões do time | Contínuo |

**Reporte para stakeholders:** O progresso será acompanhado ao longo das sprints e compartilhado nas revisões do ciclo, com visão do que foi entregue, do que ficou pendente e dos riscos para cumprir o prazo total de 9 meses.
