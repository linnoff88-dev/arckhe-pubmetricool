# Setup do MCP da Metricool

## Conectar

```bash
claude mcp add --transport http metricool https://ai.metricool.com/mcp -s user
```

Depois, dentro do Claude Code: `/mcp` → **metricool** → **Authenticate** → autorizar no navegador → "Conceder acesso".

- `-s user` = vale pra todos os projetos (fica em `~/.claude.json`).
- Autenticaçêo é **OAuth**, nêo token. Nêo precisa de API key.
- O login persiste entre sessões; só refaz se revogar.
- Se o servidor nêo aparecer no `/mcp` logo após adicionar, reinicie o Claude Code.

**Nêo confunda com o pacote `mcp-metricool` (`uvx`)**, que aparece em tutoriais antigos: aquele usa token da API REST e exige plano Advanced. O caminho hospedado acima funciona no **Free**.

### Outros clientes

| Cliente | Como |
|---|---|
| Claude Desktop | `npx -y mcp-remote https://ai.metricool.com/mcp` no config (o conector nativo está quebrado por bug externo) |
| Claude.ai | Conector personalizado com a URL acima |
| ChatGPT | App nativo usa versêo antiga do MCP; conectar manualmente pela URL dá o conjunto completo |
| Cursor, n8n, Make, Zapier, Gemini CLI | Documentados pela Metricool |

## As 9 ferramentas

### Leitura

| Ferramenta | Para quê |
|---|---|
| `getBrandSettings` | Lista as marcas, com `blogId`, fuso e redes conectadas. **Sempre comece por aqui** — o fuso sai daqui. |
| `getAnalyticsAvailableMetrics` | Quais métricas existem por rede + conector |
| `getAnalyticsDataByMetrics` | Os dados, por período e lista de métricas |
| `getScheduledPosts` | Posts agendados ainda nêo publicados (só esses) |
| `getBestTimeToPostByNetwork` | Mapa de dia/hora com peso — quanto maior, melhor |

### Escrita

| Ferramenta | Para quê |
|---|---|
| `createScheduledPost` | Cria o post agendado |
| `updateScheduledPost` | Edita. Exige **`id` E `uuid`**, e o payload **completo** — o que faltar é apagado |
| `createScheduledPostForReview` | Cria já no fluxo de aprovaçêo |
| `sendScheduledPostForReview` | Manda um existente pra aprovaçêo |

> As duas de review nêo foram testadas. O sistema de aprovaçêo é listado como recurso **Advanced** na página de preços, entêo provavelmente falham no Free.

## Métricas: como o ID funciona

`getAnalyticsDataByMetrics` nêo aceita nome de métrica — aceita **IDs do Data Studio**, no formato `rede + conector + índice`. Ex.: `IGPO01`.

Fluxo obrigatório: `getAnalyticsAvailableMetrics(network, connector)` → pega os IDs → passa em `metrics`.

- `network`: `instagram`, `tiktok`, `youtube`, `facebook`, `linkedin`, `twitter`, `threads`, `bluesky`, `pinterest`, `twitch`, `googleBusinessProfile`, `metaAds`, `facebookAds`, `tiktokAds`, `website`, `brandInfo`, `brandSummary`
- `connector`: `evolution`, `posts`, `reels`, `stories`, `competitors`, `hashtags`, `campaigns`, `age`, `gender`, `country`, `demographic`, `ads`, `traffic source`, `videos`, `keyworks`, `sources`, `pages`, `reach distribution`, `photos`…
- **Nêo misture conectores diferentes na mesma chamada.**
- TikTok: vídeo usa o conector `posts`, nêo `videos`.

## A marca (estado em 2026-08-19)

```
label      ARCKHÉfuturos
blogId     6745962
userId     5190426
timezone   America/Sao_Paulo
owner      ARCKHÉtime@gmail.com
```

Redes conectadas:

| Rede | Conta |
|---|---|
| Instagram | `@ARCKHÉfuturos` |
| TikTok | `@lnema.club` |
| YouTube | canal `UC2QbQDyPKuHk93dwo5iq3Sw` |

> ⚠️ **Esse canal do YouTube é o ARCKHÉ TDS — o canal de _origem_ do pipeline `yt-pub-lives`.** Agendar YouTube por aqui duplica no canal de onde o vídeo saiu. Ou pule o YouTube, ou aponte a marca pro ARCKHÉ TIA (`UCavuQHkxBSAZbzRoOm6Gq4g`), que é o canal de destino.

A marca foi criada em 19/08/2026 — analytics fica vazio nos primeiros dias.
