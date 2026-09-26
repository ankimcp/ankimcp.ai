---
title: "Hosted Anki — o Anki rodando na nuvem"
linkTitle: "Hosted Anki"
description: "O Hosted Anki é um Anki completo rodando na nuvem, nos servidores do AnkiMCP: alcance pela sua IA ou pelo navegador, com hibernação e sincronização explicadas."
keywords:
  - hosted anki
  - anki na nuvem
  - anki online sem computador
  - rodar anki na nuvem
  - acesso remoto ao anki
weight: 4
sitemap_priority: 0.8
---

{{< callout type="warning" >}}
**Faça um backup da sua coleção do Anki antes de começar**: exporte os seus baralhos como arquivos `.apkg` ou sincronize tudo com o AnkiWeb primeiro. Perder dados é improvável, mas nenhum serviço na nuvem pode descartar isso, e apagar uma instância é definitivo.
{{< /callout >}}

**O Hosted Anki é o app do Anki de verdade rodando na nuvem, nos servidores do AnkiMCP — o seu Anki, hospedado para você. O seu assistente de IA alcança ele a qualquer hora, de qualquer lugar, sem o seu computador estar ligado.**

{{< zoom-image src="hosted-anki-overview.png" alt="Hosted Anki aberto na visão Anki Instance do painel: o app do Anki de verdade rodando em um acesso remoto dentro do navegador, mostrando a lista de baralhos com os baralhos German e Python e a janela Painel (Browse) com um card de vocabulário de alemão (der Schlüssel — the key), com o botão On da instância e o controle Back to instance no topo." width="740" caption="O Anki de verdade, rodando na nuvem, dentro do seu navegador — clique para ampliar" >}}

## O que é

O seu Hosted Anki é o mesmo Anki que você já conhece — o app completo para desktop, não uma cópia nem uma imitação — rodando nos nossos servidores, com os add-ons do AnkiMCP já instalados. Você alcança ele de dois jeitos:

| Acesso                  | Como                                                             |
| ----------------------- | --------------------------------------------------------------- |
| **O seu assistente de IA** | Pelo MCP, do mesmo jeito que ele conversa com um Anki local   |
| **Acesso remoto**       | Um visualizador VNC no seu navegador — você vê e usa o app do Anki de verdade |

O Hosted Anki faz parte do [**plano Pro ($15/mês)**](/pt-br/pricing/).

## Hibernação e despertar

Para economizar recursos, o seu Hosted Anki **hiberna depois de 1 hora sem atividade**. Atividade significa: usar o painel, interagir com o acesso remoto ou o seu assistente de IA chamar o seu Anki.

Acordar funciona de duas formas:

- **Automaticamente** — a próxima requisição da IA acorda ele. A primeira requisição depois da hibernação leva mais ou menos **30 a 60 segundos** enquanto o Anki inicia; a requisição espera por ele. Se der tempo esgotado, é só tentar de novo daqui a um minuto.
- **Manualmente** — clique em **Start** no painel.

Hibernar é seguro. A sua coleção fica em armazenamento permanente — nada se perde quando o seu Hosted Anki hiberna.

## Anki na nuvem e Anki local juntos

Você pode ter um Hosted Anki **e** rodar um Anki local com o túnel na mesma conta. A regra é simples: **enquanto o seu Anki na nuvem estiver rodando, é sempre ele que recebe as requisições da sua IA** — mesmo que o seu Anki local esteja conectado ao mesmo tempo. O painel mostra um aviso sempre que isso acontece.

Para mandar as requisições para o seu Anki local, **pare o Anki na nuvem** (ou deixe ele hibernar sozinho). O botão de ligar/desligar no painel é a chave:

| Estado do Anki na nuvem        | Quem responde à sua IA                                              |
| ------------------------------ | ------------------------------------------------------------------- |
| Rodando                        | O Anki na nuvem — sempre                                            |
| Hibernando, Anki local conectado | O seu Anki local                                                  |
| Hibernando, sem Anki local     | O Anki na nuvem acorda e responde                                   |
| Parado por você                | O seu Anki local, se estiver conectado; senão, a requisição é recusada |

Repare na diferença entre as duas últimas linhas: um Hosted Anki que **hibernou** sozinho acorda automaticamente na próxima requisição da IA. Um que **você parou** no botão de ligar/desligar fica desligado até você clicar em **Start** — uma requisição da IA não liga ele de volta.

## Sincronização com o AnkiWeb

A plataforma **nunca guarda a sua senha do AnkiWeb**. Para sincronizar o seu Hosted Anki com o AnkiWeb, abra o acesso remoto e entre na sua conta do AnkiWeb dentro do Anki você mesmo — exatamente como faria no seu próprio computador.

O seu login continua valendo depois de reinícios e hibernações. Ele só é apagado quando você apaga o seu Hosted Anki.

## Apagar o seu Hosted Anki

Apagar o seu Hosted Anki é **definitivo**: o aparelho hospedado e todos os dados guardados nele são destruídos. É por isso que o conselho de backup no topo desta página importa.

A sua conta do AnkiWeb não é tocada — tudo o que você sincronizou com o AnkiWeb continua lá.

{{< callout type="info" >}}
O Hosted Anki está em evolução. Se alguma coisa não funcionar como descrito aqui, ou se você tiver ideias para ele, conte para a gente no [fórum da comunidade](https://forum.ankimcp.ai/).
{{< /callout >}}

---

*Aviso: "Anki" é uma marca registrada da Ankitects Pty Ltd. O AnkiMCP é um projeto independente, construído pela comunidade, e **não** é afiliado, endossado ou patrocinado pela Ankitects. O MCP é um padrão aberto criado pela Anthropic; o AnkiMCP também não é afiliado nem endossado pela Anthropic.*
