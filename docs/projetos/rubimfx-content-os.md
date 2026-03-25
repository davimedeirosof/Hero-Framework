# rubimfx-content-os — Sistema de Produção de Conteúdo Instagram

**Repositório:** `gabrielrbm-prog/opensquad-content-os`
**Criado:** Março 2026
**Stack:** Python 3 + Node.js + Playwright + Google Gemini API

---

## O que é

Sistema completo de produção de carrosséis Instagram para @rubimfx com IA.
Multi-agent framework + 6 estilos visuais + clone facial + publicação automática.
Média de ~15 minutos por carrossel, da pesquisa até a publicação.

**Resultados:** 19 carrosséis publicados em 4 dias, 6 estilos testados.

---

## Nicho @rubimfx

Posicionamento na interseção de **ICT/SMC + Order Flow + Mesa Proprietária (Summit Prop) + Economia Macro**.

**Brecha de mercado (2026):** ICT sistematizado em PT-BR no Instagram é o maior espaço vazio do mercado brasileiro. Apenas @smc_trading_br (47K) opera sistematicamente nesse espaço — @rubimfx tem o diferencial único de ser dono de mesa prop + educador ICT.

**Referência de estilo:** @economesteter (149K) — carrosséis informativos dark mode com alta densidade.

### Funil de conteúdo

| Camada | % | Objetivo |
|--------|---|----------|
| Macro/Economia | 40% | Topo — alcance máximo |
| ICT/SMC Educação | 25% | Retenção — autoridade |
| Análise de Trades | 15% | Engajamento — prova social |
| Summit Prop | 10% | Conversão |
| Order Flow/Mindset | 10% | Diferenciação |

**A ponte crítica:** Conectar eventos macro (FOMC, NFP) a setups técnicos ICT — ninguém faz isso no Brasil.

### Conformidade CVM/ANBIMA
- Permitido: educação sobre conceitos, trades reais com disclaimers
- Proibido: "calls" de compra/venda sem autorização, sem transparência publicitária

---

## Squad rubimfx-content

### Agentes (9 total)

| Agente | Execução | Skills | Função |
|--------|----------|--------|--------|
| Nara Notícia 📰 | subagent | web_search, web_fetch | Pesquisa notícias macro (FOMC, NFP, CPI, Selic) — Tier 1: Bloomberg/Reuters |
| Vitor Visual 👁️ | subagent | web_search, web_fetch | Tendências visuais, monitora 5 contas-referência semanalmente |
| Iago Instagram 💡 | inline | — | 5 ângulos distintos, rascunho do carrossel, variante de capa A/B |
| Diana Design 🖼️ | inline | image-creator | 10 slides HTML 1080x1440px dark mode |
| Léo Legenda ✍️ | inline | — | Legendas: hook ≤125 chars, corpo 150-400 palavras, CTA |
| Renata Revisão ✅ | inline | — | Score 1-10, veredicto APROVADO/AJUSTES/RETRABALHO |
| carousel-designer | — | — | Designer auxiliar |
| image-creator | — | — | Criador de imagens auxiliar |
| image-generator | — | — | Gerador de imagens auxiliar |

### Pipeline (11 steps)

```
1. Foco de Pesquisa
2. Pesquisa de Notícias (Nara)
3. Tendências Visuais (Vitor)
4. Seleção de Notícias          ← checkpoint
5. Geração de Ângulos (Iago)
6. Seleção de Ângulo            ← checkpoint
7. Criação de Carrossel (Diana + Iago)
8. Redação de Caption (Léo)
9. Aprovação de Conteúdo        ← checkpoint Davi
10. Revisão (Renata)
11. Aprovação Final              ← checkpoint Davi
```

---

## 6 Templates Visuais

Todos: **1080x1350px** (4:5 IG), fonte mínima 22px, português com acentos, sem URLs externas.

| # | Template | Características |
|---|----------|----------------|
| 1 | Twitter Dark | 7 tipos de card, tema escuro (padrão) |
| 2 | Esteter Style | Tweet threads numerados com screenshots |
| 3 | Hollyfield News | Hero images full-bleed com barra laranja |
| 4 | **Kaique Epic** ⭐ | Capas cinematográficas, headlines 80-96px, keywords amarelas |
| 5 | BrunoGPT Neon | Covers com neon vibrante |
| 6 | Minimal Clean | Fundo branco, ultraminimal |

### Padrões visuais (Diana Design)

- **Formato:** 1080x1440px (3:4 carousel)
- **Background:** `#0A0A0F` / `#111118` / `#0D1117` (dark mode obrigatório)
- **Accent (máx 2/slide):** azul `#3B82F6`, verde `#10B981`, vermelho `#EF4444`, dourado `#F59E0B`, roxo `#8B5CF6`
- **Tipografia:** headlines 48-64px, subheads 28-36px, body 22-26px, sans-serif bold
- **Header bar:** 60-80px com "@rubimfx" em todos os slides
- **Densidade:** 40-80 palavras/slide, 1 conceito/slide, padding mínimo 40px
- **Contraste:** texto/bg ≥ 4.5:1

### Fórmula de carrossel (10 slides)

1. Hook (≤10 palavras)
2. Credibilidade / preview 3 pontos
3-4. Problema (erro comum ilustrado)
5-7. Solução (1 ponto por slide)
8. Resumo (pronto para screenshot)
9. CTA suave (engajamento)
10. CTA direto (conversão)

---

## Scripts críticos

| Script | Função |
|--------|--------|
| `render_slides.py` | Converte HTML slides em PNG via Playwright |
| `pipeline.py` | Pipeline completo de automação |
| `generate_image.py` | Geração de imagens via Gemini API |
| `clone_image.py` | Clone facial com 12 presets de cenário |
| `preflight_check.py` | Validação de qualidade (26 testes) |
| `validate_accents.py` | Verifica acentuação portuguesa |
| `validate_fonts_html.py` | Verifica tamanho mínimo de fontes |

---

## Skills do projeto

| Skill | Tipo | Função |
|-------|------|--------|
| apify | mcp | Scraping web via Apify Actors — env: `APIFY_TOKEN` |
| blotato | mcp | Agendamento multi-plataforma — env: `BLOTATO_API_KEY` |
| canva | mcp | Criar/exportar designs OAuth — url: `mcp.canva.com/mcp` |
| image-creator | mcp (Playwright) | HTML/CSS → PNG, presets por plataforma, fonte mín 20px |
| image-fetcher | hybrid (Playwright) | Busca web + screenshots + assets locais |
| instagram-publisher | script (Node.js) | JPEG → imgbb → Graph API → publish; 2-10 imgs, 2200 chars |
| opensquad-agent-creator | prompt | Cria best-practices com semver; mínimo 200 linhas |
| opensquad-skill-creator | prompt | Ciclo draft→test→eval→improve; testes paralelos with/baseline |

### Env vars necessárias (instagram-publisher)
```
INSTAGRAM_ACCESS_TOKEN   (validade 60 dias via Graph API)
INSTAGRAM_USER_ID        (requer conta Business)
IMGBB_API_KEY            (conta gratuita imgbb.com)
```

---

## Squad rubimfx-video

Vídeos curtos (Reels/TikTok, 15-60s) via clone de voz e imagem.

**Pipeline:** Fotos → Nano Banana (clone) → ElevenLabs (áudio) → HeyGen/Hedra (animação) → Vídeo final

### Stack e custos (~R$350/mês — 64% mais barato que avatar direto)

| Ferramenta | Uso | Custo |
|-----------|-----|-------|
| Nano Banana Pro 2 | Clonagem fotográfica | ~R$0,35/foto |
| HeyGen Avatar IV | Animação facial | $24/mês |
| Hedra Character-3 | Animação alternativa | $10-15/mês |
| ElevenLabs | Clone de voz | $22/mês |
| Submagic Pro | Legendas | $23/mês |

### 10 Agentes
Rex Roteirista, Hugo HeyGen, Elia ElevenLabs, Sam Submagic, Bea B-Roll,
Pablo Publisher, Tina Trend, Ana Analytics, Cal Calendar, Rip Repurpose

---

## Instalação

```bash
git clone [repo]
npm install
pip3 install google-genai --break-system-packages
cp .env.example .env
# Adicionar chave Gemini API no .env
# Adicionar 3-5 fotos de referência para clone facial
# Rodar /opensquad no Claude Code para onboarding
```
