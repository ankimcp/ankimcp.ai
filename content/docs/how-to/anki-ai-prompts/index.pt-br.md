---
title: "Como usar prompts de IA para criar flashcards no Anki"
linkTitle: "Prompts de IA para flashcards"
description: "Prompts prontos para criar flashcards no Anki com IA: transforme anotações em cards bem formulados e use os prompts embutidos do AnkiMCP para revisar."
keywords:
  - prompt para flashcards anki
  - prompt para criar flashcards anki
  - prompt anki
  - anki com ia
  - flashcards com ia
  - anki mcp
weight: 5
sitemap_priority: 0.8
---

**Anexe um prompt embutido do AnkiMCP no Claude e peça os cards — o Claude monta flashcards bem formulados seguindo regras comprovadas.**

O AnkiMCP já vem com prompts prontos que ensinam a IA a escrever bons cards e a conduzir revisões. Você anexa um, diz o que quer e o Claude faz o resto. Este guia mostra os dois prompts embutidos, como anexá-los e ainda traz um prompt para criar flashcards no Anki que você pode [copiar e colar em qualquer IA](#prompts-para-copiar-e-colar-que-funcionam-em-qualquer-ia).

## O que você precisa

- **Claude conectado ao Anki.** Termine primeiro o [Conectar o Claude ao Anki](/pt-br/docs/how-to/connect-claude/).
- **Anki aberto**, com pelo menos um baralho de notas.

**Tempo:** cerca de 2 minutos.

## O que são prompts embutidos?

Um prompt é um conjunto de instruções de especialista que você entrega à IA. Ele diz ao Claude *como* fazer a tarefa antes de você pedir. O AnkiMCP inclui dois, então você recebe ajuda consistente e de qualidade sempre.

## Os prompts embutidos

Os dois já vêm dentro do AnkiMCP.

| Prompt | O que ele faz |
|---|---|
| `twenty_rules` | Ensina a IA a escrever cards eficazes usando as "Vinte Regras para Formular Conhecimento", do Dr. Piotr Wozniak. Mantém os cards simples, atômicos e claros. Melhor para transformar anotações ou livros em cards. |
| `anki_review` | Conduz uma sessão de revisão com repetição espaçada: sincroniza, mostra um card por vez, espera a sua resposta e depois pede a nota (De novo / Again, Difícil / Hard, Bom / Good, Fácil / Easy). Melhor para o estudo diário. |

Os prompts podem mudar de uma versão para outra. Para ver a lista mais recente, veja o [repositório do AnkiMCP](https://github.com/ankimcp/anki-mcp-server) (em inglês).

## Passo 1: anexe um prompt

No Claude, os prompts se anexam do mesmo jeito que arquivos.

1. Clique no **botão de anexo (+)** na caixa de mensagem.
2. Abra **Conectores (Connectors)** e escolha **Adicionar de [nome do seu conector] (Add from ...)** — o item do menu mostra o nome que você deu ao seu conector AnkiMCP.
3. Escolha um prompt na lista. No menu, eles aparecem com nomes mais amigáveis: `twenty_rules` aparece como **Twenty rules** e `anki_review` aparece como **Review session**.

As instruções do prompt ficam anexadas à sua conversa. Agora o Claude sabe quais regras seguir.

{{< callout type="info" >}}
**Está usando um app sem menu de anexos?** Copie o texto do prompt direto no chat — os [prompts para copiar e colar abaixo](#prompts-para-copiar-e-colar-que-funcionam-em-qualquer-ia) funcionam em qualquer lugar.
{{< /callout >}}

<img src="claude-prompts-menu.png" width="700" alt="Menu de anexos do Claude com o conector AnkiMCP ativado: o submenu Add from AnkiMCP.ai lista prompts como Review session e Twenty rules." />

## Passo 2: peça o que você quer

Escreva o seu pedido em linguagem simples. O Claude segue o prompt anexado pelo resto da conversa.

Para criar cards, anexe o `twenty_rules` e experimente:

```text
Crie 10 flashcards do Anki a partir destas anotações, uma ideia por card.
Use o meu baralho "Biologia". [cole suas anotações]
```

Para revisar, anexe o `anki_review` e diga:

```text
Vamos revisar meu baralho de Espanhol.
```

O Claude mostra um card, espera a sua resposta, revela a resposta certa e pede que você dê uma nota.

<img src="claude-creating-cards.png" width="740" alt="Claude com o prompt twenty_rules anexado criando um baralho de Farmacologia: a resposta confirma 9 notas cloze gerando 10 cards, com os primeiros cards listados como omissões curtas de um único fato." />

## Confira se funcionou

Abra o Anki e olhe o seu baralho. Com o `twenty_rules`, você deve ver cards novos, curtos e com uma ideia só, em vez de parágrafos longos. Com o `anki_review`, o Claude deve mostrar um card por vez e pedir que você dê uma nota a cada um — e não despejar todas as respostas de uma vez.

## Prompts para copiar e colar que funcionam em qualquer IA

Você não precisa dos prompts embutidos para ter bons cards. Os prompts abaixo funcionam em qualquer chatbot — Claude, ChatGPT, Gemini ou outro. Com o AnkiMCP conectado, a IA consegue adicionar os cards no Anki para você. Sem ele, peça que a IA escreva os cards em texto e depois cole no Anki você mesmo.

**Criar flashcards a partir das suas anotações:**

```text
Transforme as anotações abaixo em flashcards para o Anki. Uma ideia
por card. Deixe cada pergunta curta e específica, e cada resposta
com um único fato. Adicione os cards ao meu baralho "[nome do baralho]".

[cole suas anotações]
```

**Criar cards cloze (preencher a lacuna):**

```text
Transforme o texto abaixo em cards Cloze (Omissão de Palavras) do
Anki. Omita apenas um termo-chave por card e mantenha curta a frase
ao redor. Adicione-os ao meu baralho "[nome do baralho]".

[cole seu texto]
```

**Me testar como um tutor:**

```text
Me teste sobre [tema] como um tutor gentil. Faça uma pergunta de
cada vez e espere a minha resposta. Diga se eu acertei e explique
rapidamente se eu errar. Comece fácil e vá aumentando a dificuldade.
```

**Aprender idiomas — traduzir e criar um card:**

```text
Estou aprendendo [idioma]. Para a palavra ou expressão "[palavra]",
me dê a tradução, uma frase curta de exemplo e uma observação sobre
a pronúncia. Depois crie um card do Anki com o [idioma] no campo
Front (Frente) e o resto no campo Back (Verso), no meu baralho
"[nome do baralho]".
```

## Resolva problemas comuns

**Não aparece nenhum prompt no menu de anexos.**
O servidor AnkiMCP não está conectado. Abra o Claude Desktop, confirme que a extensão do AnkiMCP está instalada e reinicie o Claude. Veja [Conectar o Claude ao Anki](/pt-br/docs/how-to/connect-claude/#claude-desktop).

**O Claude criou os cards, mas ignorou as regras.**
Anexe o prompt `twenty_rules` de novo e peça outra vez. O prompt só guia as conversas em que ele está anexado, então comece um pedido novo com ele ativo.

## Perguntas frequentes

**Posso escrever meu próprio prompt?**
Pode. Você pode digitar qualquer instrução no chat. Os prompts embutidos só poupam você de escrever as regras do zero.

**Qual prompt devo usar para criar cards?**
Use o `twenty_rules`. Ele foi feito para criar flashcards bem formulados. Use o `anki_review` só para estudar cards que já existem.

## Próximos passos

- Chegou agora? Comece pelo [Conectar o Claude ao Anki](/pt-br/docs/how-to/connect-claude/).
- Quer estudar, e não só criar cards? Releia o fluxo do `anki_review` acima.
- Leia a fonte das regras de criação de cards: [Twenty Rules of Formulating Knowledge](https://www.supermemo.com/en/blog/twenty-rules-of-formulating-knowledge) (em inglês).

---

*Aviso: "Anki" é uma marca registrada da Ankitects Pty Ltd. O AnkiMCP é um projeto independente, criado pela comunidade, e **não** tem vínculo com a Ankitects, nem é endossado ou patrocinado por ela. MCP é um padrão aberto criado pela Anthropic; o AnkiMCP também não tem vínculo com a Anthropic nem é endossado por ela.*
