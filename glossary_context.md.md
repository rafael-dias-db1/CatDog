# Glossário do Projeto

> **Como preencher:** registre aqui todos os termos do domínio de negócio que qualquer pessoa do time precisa conhecer para trabalhar neste projeto. Ordene alfabeticamente.
> **Caminho:** `02-systems/{sistema}/context/glossary.md`
> **Regra de ouro:** se alguém de fora do negócio não entendesse um termo nas conversas, nos requisitos ou nas telas, ele deve estar aqui.

---

## Termos do Domínio

> Escreva definições completas — o que é o termo, como funciona no contexto do negócio e quem o usa. Evite definições de uma linha.
> **Exemplo:** _Pedido — solicitação de compra com 1 ou mais produtos, realizada por um Cliente. Passa pelos seguintes status: Rascunho → Confirmado → Em separação → Entregue. Um pedido cancelado não pode ser reativado._

| Termo | Tradução EN | Definição | Evitar (sinônimos incorretos) |
|---|---|---|---|
| ADM | Administrator | Usuário com permissão de administração da plataforma. No contexto deste projeto, a operação terá apenas três ADMs, responsáveis por gerenciar os pets aptos para adoção, avaliar usuários interessados e controlar o funcionamento interno do sistema. | admin genérico, moderador |
| Adotante | Adopter | Pessoa que navega na plataforma para conhecer os pets disponíveis, avaliar informações e iniciar o interesse em adotar. Pode ter conta no sistema para manter seus dados e interagir com o fluxo de adoção. | cliente, comprador, interessado |
| Adoções | Adoptions | Processo que representa a intenção e o andamento da adoção de um pet. A adoção começa no app, mas a finalização do acordo acontece presencialmente, fora da plataforma, após validação interna da organização. | venda, pedido, solicitação de compra |
| Doador | Donor | Pessoa que cadastra um pet para que ele seja disponibilizado para adoção. Para inserir um pet na plataforma, precisa estar logada. O doador usa o sistema para registrar o animal e acompanhar o status da publicação. | tutor, proprietário, anunciante |
| Pet acolhido | Adopted pet / Sheltered pet | Pet que já passou pelo processo de adoção e foi encaminhado para um novo lar. No contexto deste projeto, o status indica que o animal já não está mais disponível para adoção. | pet disponível, pet ativo |
| Pet disponível | Available pet | Pet cadastrado e liberado para visualização pública como apto a ser adotado. Esse status indica que o animal está visível na plataforma e pode ser analisado por adotantes e administrado pelos ADMs. | pet em aberto, pet para venda, pet listado |

---

## Status e Ciclos de Vida

> Liste os status de cada entidade principal do sistema e o fluxo entre eles. Essencial para que o time entenda as transições permitidas e as regras de negócio associadas.

### Pet

> O pet começa como cadastro interno e só entra na vitrine pública quando o ADM o libera para adoção.

| Status | Descrição | Transições permitidas |
|---|---|---|
| Em cadastro | O pet foi inserido na plataforma, mas ainda não está disponível para adoção pública. | Pode avançar para Disponível para adoção ou ser removido pelo ADM. |
| Disponível para adoção | O pet está publicado e visível para os usuários interessados em adotar. | Pode avançar para Acolhido quando a adoção for concluída. Pode voltar para Em cadastro se houver necessidade de correção ou suspensão. |
| Acolhido | O pet já foi adotado e está com novo lar registrado. | Não deve avançar para outros status. |

### Usuário

> O usuário pode manter sua conta e, quando aprovado, participar do processo de adoção ou cadastrar pets para adoção.

| Status | Descrição | Transições permitidas |
|---|---|---|
| Ativo | Conta liberada para uso normal na plataforma. | Pode ser suspenso pelo ADM, ou permanecer ativo. |
| Em análise | Conta sendo avaliada pelo ADM com base nos critérios definidos pela organização. | Pode avançar para Ativo ou Suspenso. |
| Suspenso | Conta bloqueada para participação nas ações do sistema. | Pode voltar para Em análise ou Ativo, conforme decisão do ADM. |

### Adoção

> A adoção representa o vínculo entre um adotante e um pet até a finalização presencial do processo.

| Status | Descrição | Transições permitidas |
|---|---|---|
| Iniciada | O interesse de adoção foi registrado no app, mas ainda não foi concluído presencialmente. | Pode avançar para Aguardando validação ou Cancelada. |
| Aguardando validação | O caso está sendo analisado internamente pelo ADM, considerando os critérios definidos pela organização. | Pode avançar para Aprovada, Reprovada ou Cancelada. |
| Aprovada | A organização aprovou o adotante e o processo pode seguir para o encontro presencial e encerramento. | Pode avançar para Concluída. |
| Reprovada | O adotante não atendeu aos critérios definidos para adoção. | Não avança para outros status, exceto por reabertura administrativa se necessário. |
| Concluída | A adoção foi finalizada presencialmente e o pet passou para o novo lar. | Não deve avançar para outros status. |
| Cancelada | O processo foi interrompido antes da conclusão. | Não deve avançar para outros status. |

---

## Relações Entre Termos

> Descreva como os principais conceitos se relacionam — hierarquias, dependências e regras de associação. Uma frase por relação é suficiente.
> **Exemplo:** _"Um Pedido contém 1 ou mais Itens de Pedido. Um Item de Pedido pertence a exatamente 1 Pedido e referencia 1 Produto."_

- Um ADM gerencia a publicação dos pets disponíveis e avalia os usuários interessados em adotar.
- Um Doador precisa estar autenticado para cadastrar um pet para adoção.
- Um Adotante pode iniciar uma adoção a partir de um Pet disponível, e essa adoção só é concluída presencialmente.
- Um Pet só passa para Pet acolhido quando a adoção é finalizada e o novo lar é confirmado.

---

## Siglas e Abreviações

> Apenas siglas do negócio ou da empresa — não registre siglas técnicas universais.

| Sigla | Significado | Contexto de uso |
|---|---|---|
| ADM | Administrador | Usado para identificar os três administradores da plataforma e suas permissões de gestão. |

---

## Histórico de Alterações

> Mudanças de nomenclatura afetam o time inteiro — registre para rastreabilidade.

| Data | Termo | Alteração | Motivo |
|---|---|---|---|
| 2026-05-22 | Pet acolhido | Adicionado | Padronização do status do animal após conclusão da adoção |
| 2026-05-22 | Pet disponível | Adicionado | Padronização do status de animais publicados para adoção |
| 2026-05-22 | Adoções | Adicionado | Padronização do processo de adoção entre app e finalização presencial |
| 2026-05-22 | Doador | Adicionado | Padronização do papel de quem cadastra pets para adoção |
| 2026-05-22 | Adotante | Adicionado | Padronização do papel de quem busca adotar pets |
| 2026-05-22 | ADM | Adicionado | Padronização do papel administrativo com três usuários internos |
