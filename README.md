ï»¿# pubmetricool

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


PublicaêÂ§êÂ£o em redes sociais (Instagram, TikTok, YouTubeê¢â¬Â¦) via **MCP da Metricool**, a partir da linha de comando / de um agente.

Documenta o que foi **testado de verdade** em 2026-08-19 ê¢â¬â um Reel + TikTok agendados ponta a ponta ê¢â¬â e o desenho da integraêÂ§êÂ£o com o pipeline `yt-pub-livesx`.

## Docs

| Doc | O que responde |
|---|---|
| [`docs/mcp-setup.md`](docs/mcp-setup.md) | Conectar o MCP, as 9 ferramentas disponêÂ­veis, dados da marca |
| [`docs/publicar-video.md`](docs/publicar-video.md) | O fluxo validado: master local ê¢â â host pêÂºblico ê¢â â agendamento |
| [`docs/limites.md`](docs/limites.md) | Limites de contas, de publicaêÂ§êÂ£o, janela de analytics, MCP vs API |
| [`docs/recursos.md`](docs/recursos.md) | O que dêÂ¡ e o que **nêÂ£o** dêÂ¡ pra fazer (responder mensagens, etc.) |
| [`docs/integracao-yt-pub-livesx.md`](docs/integracao-yt-pub-livesx.md) | Proposta de integraêÂ§êÂ£o com o pipeline de clips |
| [`docs/comparativo-blotato.md`](docs/comparativo-blotato.md) | Metricool vs Blotato ê¢â¬â quando cada uma vale |
| [`docs/comparativo-zernio.md`](docs/comparativo-zernio.md) | Zernio ê¢â¬â API + MCP, $6/mêÂªs pro caso INEMA, hospeda mêÂ­dia |

## O fluxo, em 10 linhas

```bash
# 1. master local (NêÆO baixar do YouTube ê¢â¬â ver docs/publicar-video.md)
cp /mnt/hd8t/yt-pub-lives/yt-pub-lives8/lives/<live_id>/clips/<arq>.mp4 ./reel.mp4

# 2. host pêÂºblico (o Metricool sêÂ³ aceita URL direta de arquivo)
gh release upload v1 reel.mp4 --repo inematds/midia --clobber
# ê¢â â https://github.com/inematds/midia/releases/download/v1/reel.mp4

# 3. agendar via MCP (no Claude Code, com o MCP conectado)
#    createScheduledPost ê¢â â blogId 6745962, providers [instagram, tiktok],
#    media [a URL acima], publicationDate {dateTime, timezone}
```

O Metricool baixa o arquivo da URL e re-hospeda no CDN dele. A URL do GitHub sêÂ³ precisa responder no momento do agendamento.

## Estado

- ê¢Åâ¦ **Validado:** conexêÂ£o MCP, agendamento IG Reel + TikTok, GitHub Release como host, ediêÂ§êÂ£o de post agendado
- ê¢Å¡Â ê¯Â¸Â **A validar:** uso do MCP por daemon nêÂ£o-interativo (ver [integraêÂ§êÂ£o](docs/integracao-yt-pub-livesx.md)), fluxo de aprovaêÂ§êÂ£o, se post multi-rede consome 1 ou N da cota mensal
- ê¢ÂÅ **NêÂ£o existe:** responder mensagens/comentêÂ¡rios via MCP (ver [recursos](docs/recursos.md))

## Contexto

Marca **inemafuturos** êÂ· `blogId 6745962` êÂ· plano **Free**.
MêÂ­dia hospedada em [`inematds/midia`](https://github.com/inematds/midia) (release `v1`).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>