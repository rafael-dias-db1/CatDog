# Definição de Arquitetura

> **Como preencher:** registre aqui o padrão arquitetural adotado para este sistema e a justificativa da escolha. Seja direto — o objetivo é que qualquer pessoa do time entenda como o sistema está estruturado e por que.
> **Caminho:** `02-systems/{sistema}/architecture/architecture-definition.md`
> **Divergências dos padrões organizacionais** devem ser registradas como ADR em `architecture/adr/`.

---

## Padrão Arquitetural Adotado

**Padrão:** Monólito em camadas

**Justificativa:** O sistema será uma aplicação web para uma única organização, com escopo bem definido e equipe pequena. Um monólito em camadas atende melhor esse contexto porque simplifica desenvolvimento, implantação e manutenção, sem a complexidade de microserviços. A separação em camadas permite isolar responsabilidades entre interface, regras de negócio e persistência, mantendo o projeto organizado para evolução gradual.

---

## Como o Sistema está Organizado

A aplicação será estruturada em três grandes partes: front-end web, back-end e banco de dados. O front-end concentra a navegação pública, o login e as telas de gestão; o back-end centraliza autenticação, regras de adoção, gestão de pets e administração de usuários; e o banco armazena usuários, pets, adoções e seus status. As regras de negócio ficam no back-end, enquanto o front-end atua como consumidor da API e responsável pela experiência de uso. O acesso dos usuários e ADMs será autenticado por email ou nome de usuário.

---

## Decisões Arquiteturais Importantes

| Decisão | O que foi decidido | Justificativa |
|---|---|---|
| Tipo de aplicação | A solução será apenas web | O produto foi definido para uso em navegador, sem versão mobile nativa |
| Estrutura de sistema | Organização em front-end, back-end e banco de dados | Atende ao escopo com separação clara de responsabilidades e manutenção simples |
| Autenticação | Login por email ou nome de usuário | Facilita o acesso de usuários e dos 3 ADMs ao sistema |
| Escopo de acesso | Usuários e ADMs precisam de login | O sistema precisa controlar quem pode cadastrar pets e administrar o processo |

---

## Diagramas

**C1 — Contexto:** _`architecture/diagrams/c4/c1-context.png` — visão do sistema no ecossistema_
**C2 — Containers:** _`architecture/diagrams/c4/c2-containers.png` — principais blocos e tecnologias_
**C3 — Componentes:** _`architecture/diagrams/c4/c3-components.png` — organização interna_

---

> **Lembrete:** este documento descreve a intenção arquitetural. Quando houver divergência entre o que está aqui e o que está no código, o código deve ser corrigido — ou este documento deve ser atualizado com um ADR justificando a mudança.