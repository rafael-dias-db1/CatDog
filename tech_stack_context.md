# Stack de Tecnologia

> **Como preencher:** registre todas as tecnologias, ferramentas e sistemas utilizados neste projeto. O objetivo é que qualquer desenvolvedor novo saiba exatamente com o que vai trabalhar antes de configurar o ambiente.
> **Caminho:** `02-systems/{sistema}/architecture/tech-stack.md`

---

## Linguagem e Runtime

| Item | Tecnologia | Versão | Observação |
|---|---|---|---|
| Linguagem principal | Java | 20 | Usada no backend |
| Runtime / Plataforma | Node.js | 20 | Base do front-end |
| Gerenciador de pacotes | npm | 10+ | Gerenciamento de dependências do front-end |

---

## Frameworks e Bibliotecas Principais

| Camada | Framework / Biblioteca | Versão | Finalidade |
|---|---|---|---|
| Backend | Spring Boot | 3.3.4 | Estruturar a API e concentrar as regras de negócio |
| Frontend | Vue | 3 | Construção da interface web |
| ORM / Acesso a dados | JPA / Hibernate | Não informado | Persistência e mapeamento objeto-relacional |
| Testes | JUnit | Não informado | Testes automatizados do backend |

---

## Banco de Dados

| Tipo | Tecnologia | Versão | Uso no sistema |
|---|---|---|---|
| Relacional | MySQL | Não informado | Armazenar usuários, pets, adoções, perfis e status do processo |
| Cache | Não informado | Não utilizado a princípio | Não utilizado na fase atual |
| Busca | Não informado | Não utilizado a princípio | Não utilizado na fase atual |

---

## Infraestrutura e Cloud

| Item | Tecnologia | Observação |
|---|---|---|
| Cloud provider | Azure Functions | Hospedagem serverless da aplicação |
| Containers | Não utilizado a princípio | O projeto não prevê Docker nesta fase |
| Orquestração | Não utilizado a princípio | Não aplicável no cenário atual |
| CI/CD | GitHub Actions | Pipeline automatizado do projeto |
| Monitoramento | Não informado | Ainda não definido |

---

## Sistemas e Componentes Externos

> Registre todos os sistemas de terceiros, APIs externas e componentes compartilhados da organização que este sistema consome ou com os quais se integra.

| Sistema / Componente | Tipo | Finalidade | Como integra |
|---|---|---|---|
| GitHub | Plataforma de código | Hospedagem do repositório e colaboração da equipe | Git |
| Azure Functions | Plataforma serverless | Hospedagem dos fluxos web e recursos da aplicação | Deploy na nuvem Azure |

---

## Ferramentas de Desenvolvimento

| Ferramenta | Finalidade |
|---|---|
| IntelliJ IDEA | IDE principal do backend |
| VS Code | IDE principal do front-end |
| JUnit | Execução de testes automatizados no backend |
| GitHub | Controle de versão e hospedagem do código |
| GitHub Actions | Execução de pipelines e automação do fluxo de entrega |

---
