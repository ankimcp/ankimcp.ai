---
title: "Como colocar imagem no Anki (manualmente ou com IA)"
linkTitle: "Adicionar imagens aos cards"
description: "Como colocar imagem no Anki de dois jeitos: cole a foto no editor do Anki ou deixe a IA montar os flashcards com imagem a partir de um link ou arquivo."
keywords:
  - como colocar imagem no anki
  - como adicionar imagem no anki
  - flashcards com imagem anki
  - adicionar imagens aos cards do anki
  - flashcards com foto anki
  - anki image flashcards
weight: 6
sitemap_priority: 0.8
---

**Para colocar uma imagem no Anki, cole a foto em um campo do editor do Anki ou use o botão de anexar do editor. Com uma IA conectada, você pode pular tudo isso: diga à IA onde está a imagem, e ela monta o card para você.**

Este guia mostra os dois caminhos de como adicionar imagem no Anki: o jeito padrão do Anki, para um ou dois cards, e o jeito com IA, quando você quer que os flashcards com imagem sejam montados para você.

## O jeito padrão do Anki (sem add-on)

Para um único card, o Anki puro já resolve bem:

1. No Anki, clique em **Adicionar (Add)** (ou abra um card no **Painel (Browse)**).
2. Clique dentro do campo onde a imagem deve entrar.
3. Cole a imagem (**Ctrl+V** / **Cmd+V**) ou clique no **ícone de clipe de papel** na barra de ferramentas do editor e escolha o arquivo de imagem.
4. Salve o card. O Anki copia a imagem para a sua coleção automaticamente, então ela sincroniza para os seus outros dispositivos.

<img src="anki-editor-image-card.png" width="740" alt="Janela Add note do Anki: o campo Front (Frente) pergunta What is this tree, com a foto de um baobá colada abaixo da pergunta; o campo Back (Verso) diz Baobab, e a barra de ferramentas mostra o ícone de clipe de papel para anexar." />

É isso. O jeito com IA abaixo vale a pena quando você cria cards enquanto lê ou precisa de imagens em vários cards de uma vez.

## Adicionar imagens com IA

No jeito com IA, você não cola figuras nem edita HTML na mão. Você diz à IA onde está a imagem, em palavras simples. Ela baixa a imagem, adiciona no Anki e coloca no card. O resto deste guia mostra como.

## O que você precisa

- **A IA já conectada ao Anki.** Se você ainda não fez isso, veja [Conectar o Claude ao Anki](/pt-br/docs/how-to/connect-claude/).
- **Anki aberto** no seu computador.
- **Uma imagem**, que pode ser um link da web ou um arquivo salvo no seu computador.

## Jeitos de passar uma imagem para a IA

Existem dois jeitos rápidos de adicionar uma imagem. Os dois deixam a própria IA buscar a figura, então você não perde tempo com uploads lentos.

### Por link da web (URL)

Melhor para uma imagem que já está online. Copie o link da imagem e cole na sua mensagem.

Exemplo de pedido:

> Crie um card no meu baralho Geografia. Front: uma foto da Torre Eiffel deste link — https://example.com/eiffel.jpg. Back: "A Torre Eiffel, Paris."

A IA baixa a imagem e monta o card com a figura na frente.

### Por arquivo no seu computador

Melhor para capturas de tela, fotos ou downloads salvos na sua máquina. Diga à IA o caminho completo do arquivo.

Exemplo de pedido:

> Adicione a imagem em /Users/me/Desktop/cell-diagram.png na frente do meu card de Biologia sobre as partes da célula.

No Windows, o caminho fica assim: `C:\Users\me\Desktop\cell-diagram.png`.

{{< callout type="info" >}}
**Como copiar o caminho completo de um arquivo.** No **macOS**: clique com o botão direito no arquivo, segure a tecla **Option** e escolha **Copiar ... como Nome do Caminho (Copy ... as Pathname)**. No **Windows**: clique com o botão direito no arquivo e escolha **Copiar como caminho (Copy as path)** (no Windows 10, segure **Shift** enquanto clica com o botão direito). Depois cole na sua mensagem.
{{< /callout >}}

A IA lê o arquivo, adiciona no Anki e coloca no card.

<img src="chat-add-local-image.png" width="740" alt="Uma conversa em que a pessoa passa ao Claude o caminho de um arquivo local com a foto de um baobá e pede um card no baralho Trees; o Claude confirma que guardou a imagem em collection.media e criou o card com frente e verso." />

### Um jeito lento que você deve evitar

Você pode colar uma imagem direto no chat. Evite isso. A IA precisa primeiro transformar a figura em um bloco enorme de texto, o que é lento e pode falhar com imagens grandes. Em vez disso, salve a imagem no seu computador e use o método por arquivo acima.

## Adicione uma imagem a um card que você já tem

Você também pode colocar uma figura em um card que já existe. Diga à IA qual é o card e onde está a imagem.

Exemplo de pedido:

> Encontre o meu card sobre mitocôndrias e adicione este diagrama na frente: /Users/me/Downloads/mito.png

(No Windows: `C:\Users\me\Downloads\mito.png`.)

A IA encontra o card e o atualiza com a imagem.

Uma coisa para saber: **feche antes a janela Painel (Browse) do Anki.** Se um card estiver aberto no Painel (Browse) enquanto a IA o atualiza, a mudança pode não ser salva — e você não vê nenhum erro. Mude para outra nota ou feche o Painel (Browse), e peça de novo.

## Confira se funcionou

Abra o baralho no Anki e olhe o card. A imagem deve aparecer na frente ou no verso, onde você pediu.

Se você sincroniza com o AnkiWeb, sincronize agora para a figura chegar aos seus outros dispositivos.

## Resolva problemas comuns

**A imagem não apareceu no meu card.**
Provavelmente o card estava aberto na janela Painel (Browse) do Anki durante a atualização. Feche o Painel (Browse) ou mude para outra nota, e peça para a IA tentar de novo.

**A IA diz que não consegue ler o meu arquivo.**
Passe o caminho completo, não só o nome do arquivo. No Mac ele fica assim: `/Users/you/Desktop/image.png`; no Windows, `C:\Users\you\Desktop\image.png`. Só arquivos de imagem, áudio e vídeo são permitidos — outros tipos de arquivo são bloqueados por segurança.

**O link da web não funcionou.**
Confirme que o link aponta direto para o arquivo de imagem (normalmente termina em `.jpg` ou `.png`), e não para uma página da web que mostra a imagem. Clique com o botão direito na imagem e copie o endereço da imagem.

<!-- VERIFY: which image file extensions (PNG, JPG, GIF, WebP, etc.) the file-path import accepts — README says "image MIME types" but does not list extensions -->

**A imagem fica grande demais ou estraga o card.**
Redimensione ou reduza a imagem antes de adicionar, e depois peça para a IA adicionar o arquivo menor.

## Próximos passos

- Chegou agora? Comece pelo [Conectar o Claude ao Anki](/pt-br/docs/how-to/connect-claude/).
- Quer cards melhores em menos tempo? Veja os [prompts de IA para o Anki](/pt-br/docs/how-to/anki-ai-prompts/).

---

*Aviso: "Anki" é uma marca registrada da Ankitects Pty Ltd. O AnkiMCP é um projeto independente, criado pela comunidade, e **não** tem vínculo com a Ankitects, nem é endossado ou patrocinado por ela. MCP é um padrão aberto criado pela Anthropic; o AnkiMCP também não tem vínculo com a Anthropic nem é endossado por ela.*
