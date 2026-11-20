# pubmetricool

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


PublicaÃ§Ã£o em redes sociais (Instagram, TikTok, YouTubeâ€¦) via **MCP da Metricool**, a partir da linha de comando / de um agente.

Documenta o que foi **testado de verdade** em 2026-08-19 â€” um Reel + TikTok agendados ponta a ponta â€” e o desenho da integraÃ§Ã£o com o pipeline `yt-pub-livesx`.

## Docs

| Doc | O que responde |
|---|---|
| [`docs/mcp-setup.md`](docs/mcp-setup.md) | Conectar o MCP, as 9 ferramentas disponÃ­veis, dados da marca |
| [`docs/publicar-video.md`](docs/publicar-video.md) | O fluxo validado: master local â†’ host pÃºblico â†’ agendamento |
| [`docs/limites.md`](docs/limites.md) | Limites de contas, de publicaÃ§Ã£o, janela de analytics, MCP vs API |
| [`docs/recursos.md`](docs/recursos.md) | O que dÃ¡ e o que **nÃ£o** dÃ¡ pra fazer (responder mensagens, etc.) |
| [`docs/integracao-yt-pub-livesx.md`](docs/integracao-yt-pub-livesx.md) | Proposta de integraÃ§Ã£o com o pipeline de clips |
| [`docs/comparativo-blotato.md`](docs/comparativo-blotato.md) | Metricool vs Blotato â€” quando cada uma vale |
| [`docs/comparativo-zernio.md`](docs/comparativo-zernio.md) | Zernio â€” API + MCP, $6/mÃªs pro caso INEMA, hospeda mÃ­dia |

## O fluxo, em 10 linhas

```bash
# 1. master local (NÃƒO baixar do YouTube â€” ver docs/publicar-video.md)
cp /mnt/hd8t/yt-pub-lives/yt-pub-lives8/lives/<live_id>/clips/<arq>.mp4 ./reel.mp4

# 2. host pÃºblico (o Metricool sÃ³ aceita URL direta de arquivo)
gh release upload v1 reel.mp4 --repo inematds/midia --clobber
# â†’ https://github.com/inematds/midia/releases/download/v1/reel.mp4

# 3. agendar via MCP (no Claude Code, com o MCP conectado)
#    createScheduledPost â†’ blogId 6745962, providers [instagram, tiktok],
#    media [a URL acima], publicationDate {dateTime, timezone}
```

O Metricool baixa o arquivo da URL e re-hospeda no CDN dele. A URL do GitHub sÃ³ precisa responder no momento do agendamento.

## Estado

- âœ… **Validado:** conexÃ£o MCP, agendamento IG Reel + TikTok, GitHub Release como host, ediÃ§Ã£o de post agendado
- âš ï¸ **A validar:** uso do MCP por daemon nÃ£o-interativo (ver [integraÃ§Ã£o](docs/integracao-yt-pub-livesx.md)), fluxo de aprovaÃ§Ã£o, se post multi-rede consome 1 ou N da cota mensal
- âŒ **NÃ£o existe:** responder mensagens/comentÃ¡rios via MCP (ver [recursos](docs/recursos.md))

## Contexto

Marca **inemafuturos** Â· `blogId 6745962` Â· plano **Free**.
MÃ­dia hospedada em [`inematds/midia`](https://github.com/inematds/midia) (release `v1`).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>