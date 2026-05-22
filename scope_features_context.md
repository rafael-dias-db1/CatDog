# Detalhamento do Escopo Macro do Projeto

> **Como preencher:** descreva a visão geral do produto, liste os módulos na ordem em que serão entregues e detalhe as features de cada um. Para cada feature, escreva pelo menos 3 linhas — o que faz, para quem serve e qual valor entrega.  
> **Caminho:** `02-systems/{sistema}/product/scope-features.md`
> **Próximo passo:** com este documento aprovado, cada feature vira uma spec em `specs/{modulo}/{feature}.md` gerada pelo `makuco-specify`.

---

## Visão Geral do Produto

A Cat Dog - Rafael é uma plataforma web de adoção de animais para uma única organização, criada para centralizar a divulgação dos pets, o registro de interesse, o controle interno da adoção e a finalização presencial do processo. O sistema substitui a adoção espalhada entre redes sociais, WhatsApp e controles manuais, dando mais organização para quem administra a operação e mais clareza para quem deseja adotar. O estado desejado ao final do projeto é ter um fluxo único e rastreável, no qual o pet possa ser cadastrado, acompanhado e finalmente registrado como adotado dentro da plataforma.

---

## Roadmap

| Ordem | Módulo | O que entrega ao negócio |
|---|---|---|
| 1 | Autenticação | Permite acesso seguro de usuários, doadores e ADMs ao sistema |
| 2 | Usuários | Organiza o cadastro e a gestão das contas e perfis da plataforma |
| 3 | Pets para doação | Permite cadastrar, editar e controlar os animais inseridos na plataforma |
| 4 | Pets disponíveis para adoção | Exibe os animais aptos a serem adotados e gera interesse público |
| 5 | Fluxo de adoção | Registra e acompanha o caminho do interesse até a conclusão presencial |
| 6 | Pets adotados | Mantém histórico dos animais já adotados e encerrados no sistema |
| 7 | Administração | Dá aos ADMs controle operacional sobre pets, usuários e adoções |

---

## Módulos e Features

---

### Módulo: Autenticação

Este módulo garante que usuários, doadores e administradores acessem a plataforma com identificação própria. Ele sustenta o controle de acesso do sistema e diferencia o que pode ser feito por cada perfil, sem depender de canais externos para essa validação.

#### Feature: Cadastro de conta

Permite que uma pessoa crie sua conta com dados básicos para começar a usar a plataforma. Serve para usuários comuns e doadores que desejam acompanhar pets, registrar interesse ou cadastrar animais para adoção.

Essa feature entrega o ponto de entrada do sistema e é necessária para ações restritas, como cadastrar um pet para doação. O cadastro precisa refletir os dados mínimos necessários para operação, sem exigir processos complexos.

#### Feature: Login com e-mail e senha

Permite que usuários autenticados entrem na plataforma com sua credencial principal. Serve para todos os perfis que precisam acessar áreas protegidas do sistema.

Essa feature garante acesso seguro às áreas de usuário, doador e ADM. O login é a base para que ações internas, como cadastro de pet e administração, sejam controladas corretamente.

#### Feature: Recuperação de senha

Permite que o usuário recupere o acesso à conta quando esquecer a senha. Serve para reduzir bloqueios de acesso e evitar perda de uso da plataforma por problemas simples de autenticação.

A recuperação deve ser direta e simples, sem criar etapas desnecessárias para o usuário. O valor está em manter o uso contínuo da plataforma sem depender de suporte manual constante.

---

### Módulo: Usuários

Esse módulo organiza o cadastro e a gestão da conta de quem usa a plataforma. Ele suporta a navegação de perfil, o histórico individual e o relacionamento entre a pessoa e as adoções que ela participa.

#### Feature: Edição de perfil

Permite que o usuário atualize suas informações cadastrais, como nome, telefone, cidade e e-mail. Serve para manter os dados corretos durante o uso do sistema e facilitar o contato quando houver interesse em adoção.

Essa feature entrega autonomia ao usuário para manter sua própria conta atualizada. Também ajuda a organização a trabalhar com dados mais confiáveis ao avaliar adoções.

#### Feature: Visualização de histórico pessoal

Permite que o usuário veja os pets e adoções vinculados à sua conta. Serve para acompanhar o que já foi solicitado, o que está em andamento e o que já foi concluído.

O valor está em dar rastreabilidade para o próprio adotante ou doador dentro do sistema. O histórico ajuda a entender a jornada do usuário sem precisar recorrer a registros externos.

#### Feature: Gerenciamento de conta pelo ADM

Permite que o administrador ative, desative ou ajuste contas de usuários conforme a necessidade da organização. Serve para proteger o sistema e manter apenas usuários aptos participando do fluxo de adoção.

Essa feature é importante porque o projeto possui critérios definidos para participação. O ADM precisa ter controle para manter a base de usuários coerente com as regras da organização.

---

### Módulo: Pets para doação

Esse módulo concentra o cadastro dos animais que serão disponibilizados pela organização ou pelo doador autorizado. Ele é a base para alimentar a vitrine pública e iniciar o processo de adoção de forma controlada.

#### Feature: Cadastro de pet com fotos e descrição

Permite registrar um pet com informações essenciais, fotos e requisitos para adoção. Serve para que o animal seja apresentado de forma clara para quem deseja adotar.

Essa feature entrega visibilidade e padronização para a divulgação dos animais. O cadastro precisa permitir que a organização publique pets com dados suficientes para apoiar a decisão do adotante.

#### Feature: Edição e remoção de pets

Permite corrigir informações e remover pets cadastrados quando houver necessidade. Serve para manter o catálogo atualizado e evitar que dados incorretos permaneçam visíveis.

O valor está em dar controle ao doador e ao ADM sobre o conteúdo publicado. Isso é importante para representar corretamente o estado real de cada animal.

#### Feature: Acompanhamento de status do pet

Permite acompanhar a evolução do pet entre os estados de disponibilidade, processo de adoção e adoção concluída. Serve para informar claramente em que ponto o animal está dentro do fluxo.

Essa feature dá rastreabilidade operacional ao cadastro do pet. Ela evita ambiguidades e ajuda a organização a saber quais animais ainda estão disponíveis e quais já foram adotados.

---

### Módulo: Pets disponíveis para adoção

Esse módulo é a vitrine pública do produto. Ele reúne os animais aptos a serem adotados e permite que o usuário encontre pets de acordo com filtros e critérios simples de busca.

#### Feature: Listagem filtrável de pets

Mostra os pets disponíveis em uma lista pública com filtros como espécie, porte, idade e cidade. Serve para que o usuário encontre mais rapidamente o animal mais compatível com seu contexto.

Essa feature reduz o esforço de busca e melhora a experiência de descoberta. O valor de negócio está em aproximar o adotante do pet certo com mais agilidade.

#### Feature: Tela de detalhes do pet

Exibe informações completas do animal, como fotos, descrição, requisitos e dados relevantes para adoção. Serve para apoiar a decisão do usuário antes de iniciar o interesse.

Essa feature entrega transparência e ajuda a evitar contatos pouco qualificados. Quanto melhor o detalhe apresentado, maior a chance de alinhar expectativas antes do início da adoção.

#### Feature: Ação “Quero Adotar”

Permite que o usuário manifeste interesse em adotar um pet diretamente a partir da vitrine pública. Serve para iniciar o fluxo interno de adoção sem depender de comunicação manual solta.

Essa ação é o ponto de entrada do processo de adoção no sistema. O valor está em transformar interesse em registro rastreável dentro da plataforma.

---

### Módulo: Fluxo de adoção

Esse módulo controla a jornada desde o interesse inicial até a conclusão presencial da adoção. Ele não automatiza conversa ou comunicação externa, mas mantém o estado do processo registrado para a organização.

#### Feature: Registro de interesse

Registra quando um usuário demonstra interesse em um pet disponível. Serve para que o sistema e a organização saibam quem iniciou a adoção e em qual animal.

Essa feature substitui o controle informal de mensagens e anotações manuais. O valor está em criar um ponto de partida claro para o processo.

#### Feature: Acompanhamento do andamento da adoção

Mostra as etapas da adoção em andamento para o usuário, o doador e o ADM, até a conclusão presencial. Serve para dar visibilidade do status sem transformar a plataforma em um canal de chat.

Essa feature organiza a operação interna e deixa explícito se a adoção está em interesse, em processo ou concluída. Ela respeita o limite de que a conversa e os acordos finais acontecem fora do sistema.

#### Feature: Conclusão presencial da adoção

Permite registrar que o processo foi encerrado quando o adotante e o doador finalizam o acordo pessoalmente. Serve para marcar oficialmente o pet como adotado e encerrar o ciclo dentro da plataforma.

O valor dessa feature é formalizar o resultado final do processo no sistema. Ela garante que o histórico reflita a adoção concluída e que o pet saia da vitrine pública.

---

### Módulo: Pets adotados

Esse módulo armazena a lista de pets que já passaram pelo processo de adoção e foram encaminhados a um novo lar. Ele existe para manter histórico, transparência e rastreabilidade do que já foi concluído.

#### Feature: Lista de pets adotados

Mostra os animais cujo processo de adoção já foi concluído. Serve para consulta pública ou interna, conforme o perfil do usuário, e reforça o histórico da organização.

Essa feature ajuda a distinguir os pets ainda disponíveis daqueles que já cumpriram seu ciclo na plataforma. O valor está em manter memória operacional e evitar duplicidade de interesse.

#### Feature: Visualização do histórico de adoção

Permite consultar as informações do pet e o status final da adoção. Serve para usuários e administradores acompanharem o que já foi concluído no sistema.

Essa feature traz clareza sobre o encerramento do processo e facilita consultas futuras. Ela também apoia a gestão interna da organização ao manter o histórico acessível.

#### Feature: Correção administrativa de registros concluídos

Permite que somente administradores editem ou corrijam informações de pets já adotados, quando necessário. Serve para ajustes de cadastro ou correções operacionais sem abrir o histórico para qualquer usuário.

Essa feature protege a integridade dos registros e mantém o controle da informação com a equipe administrativa. O valor está em garantir que o histórico continue confiável.

---

### Módulo: Administração

Esse módulo concentra as ações de controle da operação da plataforma. Ele existe para que os três ADMs consigam moderar o conteúdo, gerir usuários e acompanhar a jornada dos pets com visão centralizada.

#### Feature: Gerenciamento de usuários

Permite que o ADM ative, desative e avalie contas de usuários conforme os critérios definidos pela organização. Serve para impedir acesso indevido e proteger o fluxo de adoção.

Essa feature é importante porque o processo exige julgamento interno sobre a aptidão do adotante. O valor está em manter a base de usuários coerente com os critérios da organização.

#### Feature: Gerenciamento de pets

Permite que o ADM aprovem, ocultem ou corrijam dados de pets cadastrados. Serve para garantir que apenas animais aptos estejam visíveis para adoção.

Essa feature entrega controle operacional e evita que informações incorretas ou pets não liberados apareçam na vitrine pública. Ela sustenta a qualidade do catálogo de adoção.

#### Feature: Visão geral das adoções

Permite ao ADM consultar adoções em andamento e já concluídas. Serve para acompanhar a operação e entender o que está acontecendo com cada caso.

Essa feature oferece supervisão centralizada sem exigir comunicação automática ou relatórios complexos. O valor está em dar transparência à operação interna da organização.

---

## Fora do Escopo

> Liste o que foi explicitamente excluído. Registrar o que não será feito evita discussões recorrentes e alinhamentos tardios.

| Item excluído | Motivo |
|---|---|
| Notificações push, e-mail, SMS e alertas automáticos | O processo não terá automação de comunicação nesta fase |
| Chat interno entre usuário e doador | O contato ocorre fora do sistema, sem mensageria interna |
| Pagamentos, doações financeiras e checkout | O produto não possui fluxo financeiro |
| Dashboard, BI e relatórios exportáveis | Não fazem parte desta fase do produto |
| Multi-tenant e múltiplas organizações | A plataforma atenderá apenas uma organização |
| Aplicativo mobile nativo | O sistema será apenas web |
| Acompanhamento pós-adoção | O fluxo termina na conclusão presencial |
| Upload de documentos oficiais | Não foi previsto no escopo desta fase |

---
