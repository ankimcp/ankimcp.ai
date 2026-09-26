---
title: "Como colocar áudio no Anki (manualmente ou com IA)"
linkTitle: "Adicionar áudio aos cards"
description: "Veja como colocar áudio no Anki de dois jeitos: anexe ou grave o som no editor do Anki, ou deixe a IA salvar o arquivo e montar o flashcard para você."
keywords:
  - como colocar audio no anki
  - como adicionar áudio no anki
  - flashcards com áudio anki
  - adicionar áudio aos cards do anki
  - anki pronúncia áudio
  - anki audio flashcards
weight: 7
sitemap_priority: 0.8
---

**Para colocar áudio no Anki, anexe o arquivo de som no editor do Anki — ou grave o som ali mesmo. Com uma IA conectada, você pode simplesmente dizer onde está o arquivo de som, e ela guarda o áudio e coloca no card para você.**

Este guia mostra os dois caminhos de como adicionar áudio no Anki: o jeito padrão do Anki, para um card ou outro, e o jeito com IA, quando você quer que os cards com áudio sejam montados para você.

## O jeito padrão do Anki (sem add-on)

Para um único card, o Anki puro já resolve bem:

1. No Anki, clique em **Adicionar (Add)** (ou abra um card no **Painel (Browse)**).
2. Clique dentro do campo onde o som deve entrar.
3. Clique no **ícone de clipe de papel** na barra de ferramentas do editor e escolha o seu arquivo de áudio — ou clique no **ícone de microfone** para gravar a sua própria voz na hora.
4. Salve o card. O Anki copia o áudio para a sua coleção e mostra um botão de play no card.

<img src="anki-editor-toolbar.png" width="740" alt="Janela Add note do Anki com a barra de ferramentas do editor no topo; o ícone de clipe de papel anexa arquivos de áudio e o ícone de microfone grava áudio na hora." />

Esse é todo o fluxo manual. O jeito com IA abaixo ajuda quando você cria muitos cards com áudio, ou quer que o áudio venha de um link.

## Adicionar áudio com IA

Não importa de onde vem o áudio — um arquivo que você já tem, um link ou uma voz gerada para você —, você aponta o caminho para a sua IA, e o AnkiMCP salva o som na sua coleção do Anki e coloca no card. O resto deste guia mostra esse fluxo, os métodos que funcionam e os limites.

## O que você precisa

- **A sua IA conectada ao Anki.** Faça primeiro o guia [Conectar o Claude ao Anki](/pt-br/docs/how-to/connect-claude/).
- **Anki aberto** no mesmo computador.
- **Um arquivo de áudio** que você quer no card. Pode ser um arquivo no seu computador, uma URL pública, uma voz criada pelo [Text to Speech do Anki Studio](/docs/anki-studio/text-to-speech/) (em inglês) ou um arquivo feito por um servidor MCP de áudio separado (veja abaixo).

**Tempo:** cerca de 5 minutos.

## Como o áudio vai parar no card

O AnkiMCP salva o seu arquivo de áudio na pasta de mídia do Anki. Depois, ele escreve a tag de som do Anki em um campo do card, assim: `[sound:hello.mp3]`. Essa tag diz ao Anki para mostrar um botão de play.

Você pode entregar o áudio para a IA de três jeitos:

1. **Um arquivo no seu computador.** Diga à IA o caminho do arquivo. Este é o método mais rápido.
2. **Uma URL pública.** A IA baixa o arquivo e salva. Não precisa de mais nada.
3. **Áudio gerado.** O [Text to Speech do Anki Studio](/docs/anki-studio/text-to-speech/) (em inglês) cria a voz para você e salva o mp3 na sua biblioteca de mídia. Um servidor MCP de TTS (texto para fala) separado também funciona.

Evite colar dados brutos de áudio. Caminhos de arquivo e URLs são mais rápidos e gastam muito menos tokens.

## Passo 1: prepare o seu áudio

Deixe o arquivo de áudio pronto antes, de uma destas três formas:

- **Salve um arquivo de som no seu computador** e anote o caminho completo dele — algo como `/Users/you/hola.mp3` no Mac, ou `C:\Users\you\hola.mp3` no Windows. Não sabe como copiar um caminho? Veja a dica em [Adicionar imagens aos cards](/pt-br/docs/how-to/add-images-to-cards/#por-arquivo-no-seu-computador).
- **Encontre um link público** para um áudio de pronúncia.
- **Peça ao [Anki Studio](/docs/anki-studio/text-to-speech/) (em inglês) para criar a voz.** Ele transforma o seu texto em um mp3 e salva na sua biblioteca de mídia, pronto para entrar em um card. Uma alternativa é um servidor MCP separado que gera áudio, como o [servidor MCP da ElevenLabs](https://github.com/elevenlabs/elevenlabs-mcp) (em inglês).

<img src="finder-hola-mp3.png" width="700" alt="Finder com o arquivo hola.mp3 selecionado na pasta Downloads; a barra de caminho embaixo mostra o caminho completo anatoly, Downloads, hola.mp3." />

## Passo 2: peça à sua IA para adicionar o áudio

Abra a sua IA e faça um pedido simples. Seja claro sobre o arquivo e sobre o card.

Para um card novo:

> Crie um card no meu baralho "Spanish". Front: o arquivo de áudio em /Users/you/hola.mp3. Back: "Hello".

Para um card que já existe, descreva o card pelo conteúdo dele:

> Adicione o arquivo de áudio em /Users/you/hola.mp3 na frente do meu card sobre "hola".

(No Windows, o caminho fica assim: `C:\Users\you\hola.mp3`.)

Uma coisa para saber antes de atualizar um card que já existe: **feche antes a janela Painel (Browse) do Anki.** Se a nota estiver aberta no Painel (Browse) enquanto a IA a atualiza, a mudança pode não ser salva — e você não vê nenhum erro.

A IA guarda o arquivo na pasta de mídia do Anki e depois escreve a tag `[sound:hola.mp3]` no campo.

<img src="chat-add-audio.png" width="740" alt="Uma conversa em que a pessoa pede um card no baralho Spanish com o arquivo de áudio /Users/anatoly/Downloads/hola.mp3 na frente e Hello no verso; o Claude confirma que guardou o hola.mp3 e adicionou a tag de som ao card." />

## Passo 3: abra o Anki e estude

Abra o seu baralho no Anki e comece uma revisão. O card com áudio mostra um **botão de play**. Clique nele para ouvir o som.

## Confira se funcionou

Encontre o card na janela **Painel (Browse)** do Anki. O campo deve conter uma tag de som como `[sound:hola.mp3]`, e a pré-visualização do card deve mostrar um botão de play. Se você ouvir o áudio, deu certo.

## Tipos de áudio suportados

O AnkiMCP aceita os arquivos de áudio mais comuns. O **MP3** é a escolha mais segura e mais comum, e toca em todas as plataformas do Anki. Se você passar o áudio pela [Media Library](/docs/anki-studio/media-library/) (em inglês) do Studio, ela aceita MP3 e WAV.

Os métodos de caminho de arquivo e de URL só aceitam arquivos de mídia (áudio, imagens, vídeo). Outros tipos de arquivo são bloqueados por segurança.

## Resolva problemas comuns

**A IA diz que adicionou o áudio, mas o card não mudou.**
As atualizações falham em silêncio quando a nota está aberta na janela Painel (Browse) do Anki. Feche a janela Painel (Browse), ou selecione outra nota, e peça para a IA tentar de novo.

**Não ouço nada quando clico no play.**
Confirme que o arquivo é mesmo um arquivo de áudio e que o nome na tag `[sound:...]` é exatamente igual ao do arquivo salvo. No Anki, use **Ferramentas (Tools) → Verificação e Mídia (Check Media)** para encontrar arquivos ausentes.

## Perguntas frequentes

**O AnkiMCP faz texto para fala?**
Faz, pelo [Anki Studio](/docs/anki-studio/text-to-speech/) (em inglês). Peça o áudio para a sua IA: o Studio cria o mp3 e salva na sua biblioteca de mídia. Depois o AnkiMCP guarda o arquivo no Anki e escreve a tag de som. Se você preferir um servidor MCP de TTS separado, ele continua funcionando.

**O Anki aceita flashcards com áudio?**
Aceita. O Anki toca áudio com a tag `[sound:nomedoarquivo.mp3]`. O AnkiMCP escreve essa tag para você, então você não precisa editar campos na mão.

## Próximos passos

- [Text to speech](/docs/anki-studio/text-to-speech/) (em inglês) — deixe o Anki Studio gerar a voz para você.
- [Adicionar imagens aos cards](/pt-br/docs/how-to/add-images-to-cards/) usando as mesmas ferramentas de mídia.
- [Escreva prompts melhores para o Anki](/pt-br/docs/how-to/anki-ai-prompts/) para a IA criar os cards que você quer.

---

*Aviso: "Anki" é uma marca registrada da Ankitects Pty Ltd. O AnkiMCP é um projeto independente, criado pela comunidade, e **não** tem vínculo com a Ankitects, nem é endossado ou patrocinado por ela. MCP é um padrão aberto criado pela Anthropic; o AnkiMCP também não tem vínculo com a Anthropic nem é endossado por ela.*
