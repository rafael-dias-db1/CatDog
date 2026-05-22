# Objetivo do Projeto

---

## Identificação do Sistema

**Nome do sistema:** Cat Dog - Rafael

**Status:** Draft

**Repositório de código:** Não informado

**Última atualização:** 2026-05-22 — Makuco

### Ambientes

| Ambiente | URL |
|---|---|
| Desenvolvimento | Não informado |
| Homologação | Não informado |
| Produção | Não informado |

---

## Problema a Ser Resolvido

**Situação atual:** As adoções dos animais acontecem hoje por meios dispersos e pouco controlados, como redes sociais, conversas no WhatsApp e registros manuais. Isso dificulta acompanhar quem demonstrou interesse, em que etapa cada adoção está e se o animal realmente encontrou um novo lar.

**Causa raiz:** A ausência de uma plataforma única para centralizar a divulgação dos animais, o contato com interessados e o acompanhamento do processo de adoção faz com que a operação dependa de mensagens soltas, planilhas ou anotações manuais.

**Impacto:** Os organizadores da adoção têm dificuldade para gerenciar o fluxo, responder interessados e manter o controle dos casos. Quem quer adotar também enfrenta um processo pouco organizado, com risco de demora, perda de informação e desistências. Os próprios animais ficam mais tempo disponíveis sem uma jornada clara até a adoção.

---

## Objetivo do Projeto

**Onde devemos chegar com o projeto entregue:** Ao final do projeto, a organização deve conseguir registrar, divulgar e acompanhar os animais disponíveis para adoção em um único sistema, reduzindo a dependência de processos manuais e canais dispersos. O projeto será considerado bem-sucedido quando um animal cadastrado no site puder ser adotado e o novo lar ficar registrado no sistema.

- Centralizar as adoções em uma única plataforma.
- Permitir que a organização acompanhe o status de cada animal e de cada adoção.
- Facilitar o contato entre interessados e organizadores.
- Registrar no sistema quando o animal tiver sido adotado e encaminhado para um novo lar.

---

## Visão Geral do Sistema

### Propósito

A plataforma serve para centralizar o processo de adoção de animais de uma única organização. Ela reúne em um só lugar o cadastro dos animais, a divulgação para interessados e o acompanhamento da adoção até o encerramento do processo. O objetivo é dar mais controle para a organização e tornar a jornada de adoção mais simples e rastreável.

### Público-Alvo e Usuários

**Perfil 1 — Organizador da adoção**
Descrição: pessoa da organização responsável por cadastrar animais, divulgar informações e acompanhar as adoções.
O que faz e quando faz: registra os animais, atualiza informações, acompanha interessados e finaliza a adoção quando o novo lar é confirmado.

**Perfil 2 — Interessado em adotar**
Descrição: pessoa que visita a plataforma para conhecer animais disponíveis e iniciar o processo de adoção.
O que faz e quando faz: consulta os animais, verifica informações, demonstra interesse e entra em contato com a organização para seguir com a adoção.

**Perfil 3 — Administrador da organização**
Descrição: pessoa com visão mais ampla da operação, responsável por manter o controle da plataforma e da rotina de adoções.
O que faz e quando faz: gerencia o uso geral do sistema, supervisiona os registros e acompanha os resultados das adoções.

### Contexto de Mercado e Posicionamento

**Contexto de mercado:** O sistema atua no segmento de adoção responsável de animais, atendendo uma necessidade comum de organizações que divulgam animais disponíveis para adoção e precisam controlar esse processo de forma mais organizada.

**Posicionamento:** A proposta é ser uma plataforma simples e centralizada, criada para uma única organização, substituindo a fragmentação entre redes sociais, WhatsApp e controle manual.

**Público-alvo de mercado:** Organizações de proteção animal, abrigos, protetores independentes ou iniciativas semelhantes que precisam divulgar animais e administrar adoções.

### Contexto de Uso pelo Cliente

A organização usa este sistema como canal principal para registrar os animais disponíveis, divulgar suas informações e acompanhar o andamento das adoções. Ele substitui o controle distribuído entre redes sociais, mensagens e registros manuais, concentrando a operação em um único ambiente. O sistema atende o processo de publicação do animal, interesse do adotante, acompanhamento interno e confirmação final da adoção.

---

## Contexto de Negócio

**Sobre o negócio:** Trata-se de uma plataforma voltada para uma única organização que trabalha com adoção de animais e precisa organizar melhor sua operação de divulgação e controle das adoções.

**Domínio e segmento:** Adoção de animais, com foco em gestão interna do processo de adoção e divulgação de animais disponíveis.

**Processo atual (como as pessoas fazem hoje):** O processo acontece de forma descentralizada, com divulgação em redes sociais, troca de mensagens por WhatsApp e controles feitos manualmente, o que dificulta rastrear o status de cada adoção.

**Restrições e regras de negócio relevantes:** O sistema deve atender uma única organização e refletir a operação real de adoção responsável. Cada animal cadastrado precisa ter acompanhamento até a confirmação de adoção. O encerramento do processo ocorre quando o novo lar é registrado no sistema.

---

## Escopo Macro do Projeto

| # | Módulo / Epic | Prioridade |
|---|---|---|
| 1 | Cadastro e gerenciamento de animais | Alta |
| 2 | Divulgação pública de animais disponíveis para adoção | Alta |
| 3 | Acompanhamento do processo de adoção | Alta |
| 4 | Administração e controle operacional da organização | Média |

---

## Escopo Negativo do Projeto

| O que não será feito | Motivo |
|---|---|
| Gestão de múltiplas organizações | O sistema será usado por uma única organização |
| Integração com redes sociais para publicação automática | O problema descrito é a dispersão entre canais, então a plataforma centraliza o fluxo próprio |
| Integração com WhatsApp como canal principal de operação | O objetivo é reduzir a dependência de conversas manuais |
| Marketplace de adoção para várias instituições | O produto não foi definido como uma plataforma multi-tenant |

---

## Pessoas e Interesses (Stakeholders)

| Nome | Empresa / Área | Papel no Projeto |
|---|---|---|
| Rafael | Organização dona do projeto | Responsável pelo produto / patrocinador |
| Organizadores da adoção | Organização | Usuários operacionais que cadastram e acompanham os animais |
| Interessados em adoção | Público externo | Usuários finais que consultam os animais e iniciam o processo |
| Equipe de desenvolvimento | DB1 Group | Implementação e evolução da solução |

---

> **Próximo passo:** com este documento preenchido e revisado, acione o `makuco-specify` referenciando este arquivo para gerar as specs de cada módulo listado no Escopo Macro.