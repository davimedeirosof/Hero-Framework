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

### Concorrentes mapeados

| Tipo | Conta | Seguidores |
|------|-------|-----------|
| Direto | @smc_trading_br | 47K |
| Direto | @escolatrading | — |
| Direto | @zoom_trader_ict | — |
| Referência internacional | @smcandict | 214K |
| Mercado amplo | @antunes | ~2M |
| Mercado amplo | @capaiffer | ~1M |
| Mercado amplo | @atomeducacional | 258K |
| Referência estrutural | @economesteter | 149K |

### Frequência recomendada
- **Reels:** 2-3x/semana
- **Carrosséis:** 2-3x/semana
- **Stories:** diariamente
- **Lives:** 1x/semana (maior engajamento em mesas BR)
- **Eventos macro:** publicação mesmo dia ou D+1
- **Semanas normais:** 3-4 carrosséis semanais
- **Horários:** 7h–9h ou 18h–20h (BRT)

### Identidade visual (regras de campo)
- Paleta base: navy `#0D1117`, branco, dourado `#F59E0B` ou teal `#00D4AA`
- **Regra crítica:** anotar DENTRO do TradingView, não redesenhar no Canva — autenticidade supera design polido

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

## Identidade do Gabriel Rubim (clone facial)

- Pele clara/oliva, olhos castanho-avelã, barba bem aparada
- Tattoo sleeve braço esquerdo, porte atlético, estilo dark minimal
- Books disponíveis: minimalista e impactante
- **NUNCA** usar stock genérico — usar fotos editoriais reais (Firecrawl) ou gerar via Gemini / clonar com `clone_image.py`

## Tom de voz (6 modos)

| Tom | Quando usar | Características |
|-----|-------------|----------------|
| **1 — Analítico Direto** | Análises, teses de mercado (padrão) | Linguagem técnica acessível, afirmações claras com justificativa |
| **2 — Educacional Paciente** | Conteúdo conceitual, tutoriais | Professor com analogias, presume leitor iniciante |
| **3 — Provocativo Contrário** | Desmistificação, teses contrárias | Desafia consenso com argumentação, tensão intelectual |
| **4 — Urgente Noticioso** | Breaking news, bancos centrais | "O que aconteceu + significado + ação", publicar em ≤4h |
| **5 — Inspiracional Practitioner** | Mentalidade, disciplina, risco | Motivação ancorada em experiência real operacional |
| **6 — Storytelling Pessoal** | Trades reais, bastidores | 1ª pessoa, datas/horários específicos, setup→execução→resultado→aprendizado |

**Regras gerais de tom:**
- Português BR + termos financeiros em inglês (FOMC, NFP, order block, etc.)
- Registro informal profissional com contrações naturais
- Emojis: 1-3 por parágrafo em captions; **zero em slides**
- Parágrafos curtos, listas para múltiplos itens, negrito para ênfase
- Minúsculas, frases curtas, CTA final sempre (salva/comenta/manda)
- Viés conservador com fé cristã naturalmente integrada

## Critérios de qualidade (scoring)

Todos os critérios devem passar antes da publicação. Um reprovado = bloqueio.

| Critério | Peso | Mínimo |
|----------|------|--------|
| Precisão Factual | 5x | Fontes primárias: BLS, Fed, BCB, Bloomberg |
| Compliance CVM/ANBIMA | 5x | Abaixo de 4 = reprovação automática |
| Estrutura do Carrossel | 4x | 8-12 slides, 40-80 palavras/slide, hook ≤15 palavras |
| Bridge Macro→Setup | 4x | Opcional mas pontuado |
| Tom e Voz | 3x | Analítico direto PT-BR, termos EN mantidos |
| Consistência Visual | 3x | Dark mode, bold condensada, cores limitadas |
| Caption | 2x | Hook ≤125 chars, 150-300 palavras, 5-15 hashtags |

**Mínimo para publicação:** 80% do score total.

## Seleção de pauta (pontuação)

| Critério | Peso |
|----------|------|
| Impacto em forex/futuros | 5 |
| Importância para audiência | 4 |
| Timing | 4 |
| Potencial de Bridge | 2 |
| Viralização | 2 |

**Mínimo:** 14/25 pontos para entrar em produção.

## 12 Anti-patterns proibidos

1. Hook genérico sem tensão (deve criar curiosidade em ≤15 palavras)
2. Slides rasos com menos de 40 palavras
3. Bridge ausente — macro sem conexão com setup acionável
4. Promessas de retorno — viola CVM/ANBIMA
5. Estética Canva stock — proibido templates genéricos
6. Hashtag spam (30+) — usar 5-15: 3-5 fixas + 3-8 contextuais
7. Caption sem CTA — sempre terminar com pergunta, salva ou compartilha
8. Inconsistência visual entre slides (troca de background/accent)
9. Fundo claro — backgrounds devem ser dark (`#0D1117` ou `#1A1B2E`)
10. Jargão sem explicação — introduzir termos antes de usar abreviatura
11. Frequência irregular — manter 3-4 posts/semana independente do calendário
12. Copiar outros nichos — só referenciar contas macro (@economesteter, Hedgeye)

## Conceito BRIDGE

Fórmula que conecta notícia a trade acionável:

```
Evento Macro → Impacto no Ativo → Leitura Técnica → Setup Ativado
```

**Exemplo FOMC:** Fed sinaliza 3 cortes → Treasury yields caem, DXY enfraquece → XAU/USD liquidity sweep + order block + BOS → Setup long Gold ativado

**Exemplo COPOM:** Selic +50bps → Diferencial BR-EUA alarga → Pressão vendedora no dólar → WDO sweep e reversão

## 8 Templates HTML disponíveis

| # | Nome | Uso ideal |
|---|------|-----------|
| 01 | Dark Tweet | Cover de impacto máximo — card preto, badge vermelho |
| 02 | News Magazine | Contextualizar artigos jornalísticos reais |
| 03 | Neon Data | Slides com muitos dados de mercado — neon cyan |
| 04 | Minimal Clean | Narrativa textual e análise — muito espaço branco |
| 05 | Breaking News | Notícias urgentes — glow vermelho, breaking bar pulsante |
| 06 | Personal Brand | Últimos slides e CTA — foto full-bleed, pílula dourada |
| 07 | Infographic | Comparações e rankings — tabela + gráfico de barras |
| 08 | Meme Editorial | Reações virais — simulação browser com comentário irônico |

**Fontes obrigatórias:** Anton (headlines, 96px máx), Inter (body, 20px mín). Nenhum texto abaixo de 20px.

**Paletas por estilo:**
- **Kaique Epic:** Amarelo `#FFD600`, Vermelho `#FF3B30`, Azul `#1D9BF0`, Verde `#00BA7C`
- **InvisIA:** Roxo `#7C3AED` sobre preto `#000000`
- **Padrão dark:** navy `#0D1117` ou charcoal `#1A1B2E` + branco + 1 accent (gold `#F59E0B` ou teal `#00D4AA`)

## Estrutura alternada de slides

Alternância obrigatória: **Epic Cover** (foto dark full-bleed) + **Tweet Card** (branco, profile header). Nunca 3 slides consecutivos do mesmo tipo.

## Fontes de dados primárias

- **EUA:** FOMC, NFP, CPI/PPI, PCE, ISM, GDP
- **Brasil:** COPOM/Selic, IPCA, PIB, balança comercial
- **Global:** BCE, BoJ, BoE, geopolítica, OPEC
- **Ativos monitorados:** DXY, XAU/USD, S&P500, Nasdaq, WTI/Brent, EUR/USD, GBP/USD, USD/JPY, USD/BRL, WDO, WIN

## Fluxo de produção típico

1. **Pesquisa** — histórias virais de múltiplas fontes (Nara)
2. **Seleção de design** — tema e estilo visual (checkpoint Davi)
3. **Geração de imagens** — IA via Gemini `gemini-2.5-flash-image` + variantes clonadas
4. **Criação dos slides** — 10 slides HTML com template escolhido (Diana)
5. **Renderização** — conversão screenshot HTML → PNG via Playwright
6. **Validação** — preflight checks automatizados (26 testes)
7. **Publicação** — upload automático via Instagram Graph API

## Tecnologias

| Camada | Tecnologia |
|--------|-----------|
| Orquestração | Opensquad multi-agent |
| Renderização | HTML/CSS → PNG via Playwright |
| Geração de imagens | Google Gemini API (`gemini-2.5-flash-image`) |
| Clone facial | Sistema multi-referência customizado com identity headers |
| Publicação automática | Playwright MCP (Chrome) + Instagram Graph API |
| Runtime | Python 3 + Node.js |

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
