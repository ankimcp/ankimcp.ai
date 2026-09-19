---
title: "Solução de problemas do AnkiMCP: resolva os erros comuns"
linkTitle: "Solução de problemas"
description: "Resolva os problemas comuns do AnkiMCP: Anki fechado, add-on ou AnkiConnect parado, o app de IA ou o túnel remoto sem conectar e edições de nota que não salvam."
keywords:
  - solução de problemas ankimcp
  - anki mcp não funciona
  - anki mcp não conecta
  - add-on anki mcp não inicia
  - túnel anki mcp não conecta
  - corrigir anki mcp
  - anki mcp pydantic_core download failed
weight: 7
sitemap_priority: 0.7
---

**A maioria dos problemas do AnkiMCP tem uma destas três causas: o Anki está fechado, a conexão ou o add-on não está rodando, ou o seu app de IA precisa ser reiniciado.**

Encontre o seu sintoma abaixo, aplique a solução e tente de novo com o seu assistente de IA. A maioria das soluções leva um ou dois minutos. Alguns passos mudam conforme o jeito que você conecta, então cada seção diz a qual caminho ela se aplica.

## Comece por estas verificações rápidas

Estas duas verificações resolvem a maior parte dos problemas, não importa como você conecta.

1. **Confira se o Anki está aberto.** O AnkiMCP só alcança os seus cards enquanto o app do Anki estiver rodando. Abra o Anki e pergunte de novo para a sua IA.
2. **Reinicie o seu app de IA.** Feche e abra de novo, para ele se reconectar ao AnkiMCP. Os apps se conectam ao AnkiMCP só na hora em que iniciam.

Se a sua IA ainda não alcança os seus cards, continue lendo.

## A sua IA não vê os seus baralhos ou não conecta

**Sintoma:** Você pede para a sua IA listar os seus baralhos e ela não encontra nada, ou nem consegue conectar.

A solução depende de como você conecta. Não sabe qual caminho você usa? Veja [Add-on vs CLI](/docs/concepts/add-on-vs-cli/) (em inglês).

### Se você usa o add-on AnkiMCP

O add-on roda um servidor dentro do Anki. O AnkiConnect não entra nesse caminho.

1. No Anki, abra **Ferramentas (Tools) → AnkiMCP Server Settings...**
2. Confirme que o servidor aparece como rodando. Ele inicia sozinho quando o Anki abre.
3. Se você não encontrar isso, reinicie o Anki e confira de novo.

### Se você usa a CLI ou o pacote do Claude Desktop

Esses caminhos alcançam o Anki pelo add-on **AnkiConnect**.

1. Abra [http://localhost:8765](http://localhost:8765) no seu navegador. Você deve ver o texto simples `AnkiConnect`.
2. Se não vir, instale ou reinstale o AnkiConnect. No Anki, vá em **Ferramentas (Tools) → Extensões (Add-ons) → Obter extensões... (Get Add-ons...)**, digite o código `2055492159`, clique em **OK** e reinicie o Anki.
3. Para a CLI, confirme também que o Node.js 22.12.0 ou mais recente está instalado.
4. Para a CLI, procure erros de digitação no seu arquivo JSON de configuração: sem vírgulas sobrando, sem chaves desemparelhadas.
5. Reinicie o seu app de IA para ele se reconectar.

Para ajuda na configuração, veja [Conectar o Claude](/pt-br/docs/how-to/connect-claude/) ou [Conectar outros clientes MCP](/docs/how-to/connect-mcp-clients/) (em inglês).

## Usando o Claude na web, o ChatGPT ou outra IA remota (túnel)

**Sintoma:** Uma IA remota como o ChatGPT não alcança os seus cards, ou a conexão cai.

Uma IA remota alcança o seu computador por um **túnel**. O túnel só repassa as requisições para o Anki na sua própria máquina, então algumas coisas precisam continuar valendo.

1. **Verifique se o túnel está conectado.** Add-on: abra **Ferramentas (Tools) → AnkiMCP Server Settings...** e confirme que o túnel aparece como conectado. CLI: confira se o terminal com o `--tunnel` ainda está rodando (veja a [documentação do túnel na CLI](https://github.com/ankimcp/anki-mcp-server#tunnel--recommended), em inglês).
2. **Mantenha o computador acordado e o Anki aberto.** Se o computador dormir ou o Anki fechar, o túnel não tem o que repassar.
3. **Entre na sua conta de novo se a sessão expirou.** Reconecte o túnel para renová-la.

Para a configuração completa, veja [Conectar o ChatGPT ao Anki](/pt-br/docs/how-to/connect-chatgpt-to-anki/).

**Avançado:** Se você vir `421 Invalid Host header` (cabeçalho de host inválido) depois de definir um hostname personalizado para o servidor HTTP do add-on, veja [Remote Access Security](/docs/concepts/remote-access-security/) (em inglês) para liberar esse nome.

## As edições de nota dão certo, mas a nota não muda

**Sintoma:** Você pede para a sua IA editar uma nota. Ela responde "pronto", mas a nota não muda. Nenhum erro aparece.

Isso acontece quando a nota está aberta na janela **Painel (Browse)** do Anki. Você não consegue atualizar uma nota enquanto está vendo ou selecionando ela ali. Essa é uma **limitação da janela Painel (Browse) do próprio Anki**, não um bug do AnkiMCP, e ela afeta tanto o add-on quanto o AnkiConnect.

**Solução:** Antes de pedir para a sua IA editar uma nota, desmarque ou feche ela no Anki:

1. Feche a janela **Painel (Browse)** do Anki, **ou** pressione **Escape** para desmarcar a nota, **ou** clique em outra nota.
2. Peça para a sua IA fazer a alteração.
3. Abra o Painel (Browse) de novo para confirmar que a mudança foi salva.

A [documentação do AnkiConnect](https://git.sr.ht/~foosoft/anki-connect#codeupdatenotefieldscode) (em inglês) registra a mesma regra: "You must not be viewing the note that you are updating on your Anki browser, otherwise the fields will not update." — ou seja, você não pode estar vendo, no navegador de cards do Anki, a nota que está atualizando; senão os campos não são alterados. Veja a [issue #82 do AnkiConnect](https://github.com/FooSoft/anki-connect/issues/82) (em inglês) para o relato original. Isso vale para o add-on também, porque o limite vem do próprio Anki.

A gente não consegue corrigir isso automaticamente. Não existe um jeito confiável de detectar uma nota aberta, desmarcá-la por você ou devolver um erro quando a atualização é bloqueada. Por enquanto, desmarcar a nota você mesmo é a solução que funciona.

## Na primeira vez que o add-on inicia, ele baixa alguma coisa

**Sintoma:** Você instala o add-on AnkiMCP, reinicia o Anki e aparece uma janelinha **AnkiMCP Server - Setup** dizendo que está baixando o `pydantic_core`. Ou esse download falha e o servidor não inicia.

{{< callout type="info" >}}
**Isso vale para o add-on AnkiMCP** — a versão que se instala dentro do Anki. Não tem a ver com a CLI. Não sabe qual você usa? Veja [Add-on vs CLI](/docs/concepts/add-on-vs-cli/) (em inglês).
{{< /callout >}}

<!-- TODO(cli-agent): If the CLI has a first-run/install-time equivalent
     (npm install, Node version mismatch, etc.), add it as a sibling entry
     below this one rather than editing this add-on prose. -->

**Isso é esperado, e acontece uma única vez.** Na primeira execução, o add-on baixa um componente, o `pydantic_core` (cerca de 2 MB), do PyPI, o índice padrão de pacotes do Python. Ele não pode vir dentro do add-on: o `pydantic_core` é compilado separadamente para Windows, macOS e Linux, e um add-on do Anki é um arquivo único que precisa funcionar em todos eles. Então o add-on busca a versão que combina com o seu computador e guarda ela. Nas próximas vezes que você abrir o Anki, nada é baixado e nenhuma janela aparece.

De vez em quando você pode ver um segundo download, igualmente rápido, chamado `rpds`. Normalmente o próprio Anki fornece esse, então ele só aparece se a sua versão do Anki não fizer isso.

**Se o download falhar**, o add-on mostra um erro e o servidor não inicia. Resolva o caminho da rede e reinicie o Anki — ele tenta de novo sozinho a cada abertura, então não precisa reinstalar nada.

1. **Confira se você está online** e reinicie o Anki.
2. **Está numa rede de trabalho, escola ou hospital?** Um proxy ou firewall pode estar bloqueando o índice de pacotes. Peça para liberarem `pypi.org` e `files.pythonhosted.org`, ou abra o Anki uma vez numa conexão sem filtro — o Wi-Fi de casa ou o roteador do celular — para o download único terminar. Depois disso, a rede bloqueada não é mais problema.
3. **VPN ou antivírus atrapalhando?** Desligue por um instante, reinicie o Anki e deixe o download terminar.

## Ainda travado?

Se nada disso resolveu, você tem algumas opções:

- Leia o guia [Obter ajuda](/pt-br/docs/getting-help/) para mais suporte.
- Pergunte no [fórum da comunidade](https://forum.ankimcp.ai/).
- Relate o problema nas [issues do GitHub](https://github.com/ankimcp/anki-mcp-server/issues).

---

*Aviso: "Anki" é uma marca registrada da Ankitects Pty Ltd. O AnkiMCP é um projeto independente, construído pela comunidade, e **não** é afiliado, endossado ou patrocinado pela Ankitects. O MCP é um padrão aberto criado pela Anthropic; o AnkiMCP também não é afiliado nem endossado pela Anthropic.*
