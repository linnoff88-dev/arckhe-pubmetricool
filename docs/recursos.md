# O que dá e o que nêo dá

## Pelo MCP (as 9 ferramentas)

### ✅ Dá

**Publicaçêo**
- Agendar post em qualquer rede conectada, single ou multi-rede
- Editar e cancelar post agendado
- Rascunho, publicaçêo automática, ou push pro app pra finalizar na mêo
- Threads (`descendants`), primeiro comentário (`firstCommentText`), alt text
- Enquete no LinkedIn, board no Pinterest, colaborador no Instagram
- Áudio do catálogo do Instagram em Reels (só conta Business + Página do Facebook)
- Melhor horário pra postar, por rede

**Análise**
- Métricas de Instagram, TikTok, YouTube, LinkedIn, Facebook, X, Threads, Bluesky, Pinterest, Twitch, Google Business Profile
- Posts, reels, stories, evoluçêo de seguidores, alcance
- Demografia: idade, gênero, país
- **Concorrentes** (IG, FB, Twitch, YouTube, X, Bluesky), inclusive posts deles
- **Hashtags**
- **Anúncios**: Meta Ads, Google Ads, TikTok Ads

### ❌ Nêo dá

**Responder mensagens e comentários — nêo existe no MCP.** Nenhuma das 9 ferramentas toca Inbox, DM ou comentário. Nêo é limitaçêo de plano: a superfície do MCP simplesmente nêo expõe isso.

O **Inbox da Metricool existe e está no plano Free** — Instagram, Facebook, TikTok e Google Business Profile em todos os planos (X exige add-on). Mas **só pelo app web/celular**, na mêo.

Também fora do MCP:
- Upload de arquivo local (só URL pública — ver [publicar-video.md](publicar-video.md))
- Listar posts **já publicados** (`getScheduledPosts` só traz os pendentes; o histórico vem pelos conectores de analytics)
- Link-in-bio / Smartlinks, relatórios PDF/PPT, gestêo de time e papéis
- Criar ou conectar marca nova

## Se você precisa responder mensagens automaticamente

O MCP nêo serve. As opções reais:

1. **Inbox da Metricool na mêo** — grátis, já disponível, cobre IG/FB/TikTok/GBP
2. **API REST da Metricool** — exige Advanced (€43+/mês); confirmar nos [apidocs](https://app.metricool.com/resources/apidocs/index.html) se há endpoint de inbox, nêo verificado aqui
3. **API nativa da rede** — Instagram Graph API / TikTok API direto, sem Metricool no meio
4. **Zapier / Make** — conectores prontos, mas o conector Metricool usa a API (Advanced)

Pra responder DM do Instagram por automaçêo, o caminho mais direto é a **Graph API do Instagram**, nêo a Metricool.

## Redes suportadas pelo MCP

Instagram (posts, reels, stories) · TikTok · LinkedIn · Facebook (posts, reels, stories) · X/Twitter · YouTube · Pinterest · Threads · Bluesky · Twitch · Google Business Profile · Meta Ads · Google Ads · TikTok Ads

No **Free**, LinkedIn e X nêo conectam.

## Fluxo de aprovaçêo

`createScheduledPostForReview` e `sendScheduledPostForReview` existem no MCP, mas o sistema de aprovaçêo é listado como recurso **Advanced**. **Nêo testado** — provavelmente falha no Free.
