# Restrições e Decisões Técnicas

> **Como preencher:** registre aqui o que não deve ser usado neste projeto e por quê. Restrições sem justificativa são ignoradas — registre o motivo com clareza.
> **Caminho:** `02-systems/{sistema}/architecture/tech-restrictions.md`
> **Importante:** restrições que exigem mais contexto ou que divergem dos padrões organizacionais devem virar um ADR em `architecture/adr/`.

---

## Tecnologias Proibidas

> Liste tecnologias, bibliotecas, frameworks ou abordagens que não devem ser usados neste projeto, independentemente do contexto.

| O que não usar | Motivo | Alternativa recomendada |
|---|---|---|
| Docker | Não será usado a princípio no projeto | Hospedagem serverless e execução direta do ambiente definido |
| Pagamentos | O produto não terá fluxo financeiro | Não se aplica |
| Automação de etapas por mensagens, email ou notificações | O processo de adoção não será conduzido por comunicação automática dentro do sistema | Fluxo interno simplificado e controle manual do ADM |
| Gestão de múltiplas organizações | O sistema é destinado a uma única organização | Estrutura única da organização dona do produto |

---

## Restrições de Ambiente

> Limitações impostas pelo ambiente do cliente, infraestrutura existente ou políticas da organização.

| Restrição | Descrição | Impacto no projeto |
|---|---|---|
| Apenas uma organização | O sistema atenderá somente a organização dona do projeto | Simplifica regras de acesso, cadastro e administração |
| Três ADMs | O acesso administrativo será restrito a três usuários internos | Exige controle explícito de permissões e auditoria interna mínima |
| Navegação pública com login para ações específicas | Qualquer pessoa pode visualizar, mas só usuários autenticados executam ações restritas | Exige separar áreas públicas e protegidas |
| Hospedagem serverless | A aplicação será hospedada em Azure Functions | Influencia a forma de deploy, exposição dos serviços e operação da solução |

---

## Restrições de Segurança e Compliance

> Requisitos obrigatórios de segurança, privacidade ou regulação que condicionam as decisões técnicas.

| Requisito | Descrição | Como é atendido |
|---|---|---|
| Controle de acesso autenticado | Usuários e ADMs precisam fazer login por email ou nome de usuário | Autenticação obrigatória para ações restritas |
| Critérios de aprovação de adotantes | O ADM precisa validar se o usuário atende critérios definidos pela organização, como ter casa e não possuir histórico de maus-tratos | A decisão de aprovação é feita internamente pelo ADM antes da adoção avançar |
| LGPD | O sistema lida com dados pessoais de usuários interessados e doadores | Dados devem ser tratados com finalidade restrita ao processo de adoção |

---

## Decisões Tomadas e Não Reverter

> Escolhas técnicas já feitas e consolidadas que não devem ser questionadas sem um ADR. Diferente de proibições — são decisões que já custaram tempo e que reverter teria custo alto.

| Decisão | Contexto | Por que não reverter |
|---|---|---|
| Uso de GitHub | Definido pela equipe para versionamento e pipelines | Já é o fluxo de colaboração escolhido para o projeto |
| Uso de GitHub Actions | Definido como pipeline de automação | Já sustenta a automação de build e entrega |
| Uso de migrations | Escolha para controlar evolução do banco | Evita divergência de schema e facilita manutenção |
| Hospedagem em Azure Functions | Definido como ambiente serverless | Reverter alteraria toda a estratégia de deploy e operação |

---
