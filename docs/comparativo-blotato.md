# Metricool vs Blotato

Pesquisa de 2026-08-19, a partir das páginas públicas de preços e da central de ajuda das duas.
**A Blotato nêo foi testada** — o que está aqui é o que elas declaram, nêo mediçêo.

## O eixo

> **Metricool é uma suíte de analytics que também publica.
> Blotato é uma API de publicaçêo feita pra agentes de IA, que também mede.**

A Blotato se descreve como *"Social Media APIs for AI Agents"*. Nêo é slogan: o produto **é** a API — MCP hospedado, REST em `backend.blotato.com/v2`, e nodes oficiais de n8n e Make.

Isso explica quase toda diferença abaixo.

## Comparaçêo

| | Metricool | Blotato |
|---|---|---|
| **Plano grátis** | ✅ real e permanente | ❌ trial de 7 dias |
| **Entrada paga** | €16/mês (Starter) | $29/mês (Starter) |
| **API REST** | só Advanced, **€43/mês** | **incluída no Starter, $29** |
| **MCP** | ✅ até no Free | ✅ hospedado |
| **API no trial** | — | ❌ **fica de fora** |
| **Contas sociais** | 1 por rede × nº de marcas | **20 no total** (Starter), somando tudo |
| **Modelo de conta** | marca = 1 conta de cada rede | conexões soltas, teto único |
| **Publicaçêo** | ilimitada do Starter pra cima | até 900 posts/mês no TikTok |
| **Responder DM / comentário** | ❌ **inexistente** | ✅ 1.000 contatos ativos/mês |
| **Automaçêo de DM** (comente X → recebe link) | ❌ | ✅ |
| **Analytics** | ✅ profundo | básico |
| **Concorrentes** | ✅ 5 (Free) / 100 (Starter) | ❌ |
| **Hashtags** | ✅ | ❌ |
| **Anúncios** (Meta/Google/TikTok Ads) | ✅ | ❌ |
| **Looker Studio / PDF / PPT** | ✅ Advanced | ❌ |
| **Geraçêo de IA** (imagem, vídeo, voz) | assistente de texto | ✅ créditos inclusos, ElevenLabs |
| **Nodes n8n / Make** | via API (Advanced) | **oficiais** |
| **Plataformas** | 13 + Ads | 9 |
| **Maturidade** | consolidada | mais nova |

Planos Blotato: Starter $29 (20 contas, 1.250 créditos IA) · Creator $97 (40 contas, 5.000) · Agency $499 (15.000 contatos ativos).

## Os três pontos que importam pro `yt-pub-livesx`

### 1. Resolve o bloqueio do daemon

O problema descrito em [integracao-yt-pub-livesx.md](integracao-yt-pub-livesx.md): `scheduler.py` é um daemon e nêo tem sessêo OAuth do MCP.

Na Metricool, as saídas eram `claude -p` (gasta cota Claude por post), `mcp-remote` (token em cache, nêo testado, pode morrer calado) ou API REST — **só no Advanced, €43/mês**.

Na Blotato, **REST já vem no plano de $29**. O bloqueio deixa de existir, e mais barato que o Advanced.

### 2. Contas: as duas limitam de formas diferentes — cuidado ao comparar

Nêo é "quem dá mais contas". É **o que cada uma restringe**:

| | Metricool | Blotato |
|---|---|---|
| O que limita | **formato** — 1 conta por rede, por marca | **total** — 20 conexões, qualquer mistura |
| Aperta quando | você tem 2+ contas da mesma rede | você tem muitas conexões no geral |
| Folga quando | você tem 1 conta em muitas redes | você tem muitas contas em poucas redes |

Contra o **Free** da Metricool (1 marca = 1 Instagram no total), a Blotato ganha fácil.

Contra o **Starter** dela, o número inverte: €16 = 5 marcas = até 5 contas *de cada rede* = **~65 conexões**, contra 20 da Blotato por $29. **Em contagem bruta, a Metricool Starter entrega mais, por menos.**

Ou seja: **nêo pague a Blotato por quantidade de contas** — nesse quesito ela perde pro Starter da Metricool. Pague pela **API** (que a Metricool só libera no Advanced, €43) e pelos **DMs** (que a Metricool nêo tem em plano nenhum).

### 3. Tem o que a Metricool nêo tem em plano nenhum

**Responder DM e comentário por API.** As 9 ferramentas do MCP da Metricool nêo tocam Inbox — e isso nêo é limitaçêo de plano, é ausência da superfície. O Inbox da Metricool existe (até no Free) mas só na mêo, pelo app.

## Onde a Metricool continua ganhando

- **Mediçêo séria**: concorrentes, hashtags, demografia, alcance, evoluçêo, histórico ilimitado no pago
- **Anúncios**: Meta, Google e TikTok Ads — a Blotato nêo cobre
- **Relatório pra cliente**: Looker Studio, PDF, PPT, white label
- **Custo zero** pra quem só precisa medir e publicar pouco

## Custo lado a lado

| Cenário | Metricool | Blotato |
|---|---|---|
| Curadoria, ~20 posts/mês, 1 conta | **€0** | $29 |
| Publicaçêo automatizada por API | €43/mês | **$29/mês** |
| Várias contas + responder DM | €43+ (sem DM) | **$29** |
| Analytics profundo + concorrentes + Ads | **€0 a €43** | nêo faz |

## Recomendaçêo

**Nêo escolha uma — elas nêo competem de frente.**

- **Metricool Free** como camada de **mediçêo**: analytics, concorrentes, Ads. Custo zero, já configurado e validado.
- **Blotato Starter ($29)** como **motor de publicaçêo** do `yt-pub-livesx`, via REST, direto do `scheduler.py`.

A soma custa **menos que o Advanced da Metricool sozinho** e entrega mais — inclusive DMs.

Se a escolha tiver que ser única:

- **Só medir, publicar pouco** → Metricool Free
- **Automatizar publicaçêo em volume** → Blotato
- **Relatório pra cliente / gestêo de anúncios** → Metricool Advanced

## Antes de decidir — a validar

- ❓ Confiabilidade real de publicaçêo da Blotato (taxa de falha, comportamento em erro) — nêo testada
- ❓ O que conta como "contato ativo" nos 1.000/mês de DM
- ❓ Se a Blotato aceita **upload de arquivo local** ou também exige URL pública (mudaria o fluxo do [`linnoff88-dev/midia`](https://github.com/linnoff88-dev/midia))
- ❓ Profundidade real do analytics da Blotato
- ⚠️ **A API nêo entra no trial de 7 dias** — testar a API exige pagar um mês

Ordem sensata: assinar 1 mês do Starter, portar um clip pelo REST, comparar com o fluxo Metricool já validado. ~$29 pra decidir com dado em vez de página de preços.
