# Opensquad Core — Arquitetura Interna

Documentação dos componentes internos de `_opensquad/core/`.

---

## Estrutura de diretórios

```
_opensquad/
├── .opensquad-version
├── config/
│   └── playwright.config.json
├── core/
│   ├── architect.agent.yaml
│   ├── runner.pipeline.md
│   ├── skills.engine.md
│   ├── best-practices/          ← 23 arquivos (8 discipline + 14 platform)
│   │   ├── _catalog.yaml
│   │   ├── copywriting.md
│   │   ├── researching.md
│   │   ├── image-design.md
│   │   ├── review.md
│   │   ├── social-networks-publishing.md
│   │   ├── strategist.md
│   │   ├── technical-writing.md
│   │   ├── data-analysis.md
│   │   ├── instagram-feed.md
│   │   ├── instagram-reels.md
│   │   ├── instagram-stories.md
│   │   ├── linkedin-post.md
│   │   ├── linkedin-article.md
│   │   ├── twitter-post.md
│   │   ├── twitter-thread.md
│   │   ├── youtube-script.md
│   │   ├── youtube-shorts.md
│   │   ├── email-newsletter.md
│   │   ├── email-sales.md
│   │   ├── blog-post.md
│   │   ├── blog-seo.md
│   │   └── whatsapp-broadcast.md
│   └── prompts/
│       └── sherlock.prompt.md
└── _investigations/             ← .gitkeep (vazio, preenchido pelo Sherlock)
```

---

## Architect Agent (`architect.agent.yaml`)

Agente que cria squads via linguagem natural. "Strategic systems thinker" que quebra processos complexos em responsabilidades claras por agente.

### Princípios operacionais
- **YAGNI**: nunca criar agentes que não sejam estritamente necessários
- **Single responsibility**: cada agente = exatamente uma responsabilidade clara
- **Quality checkpoints**: pipelines exigem checkpoint em todo ponto de decisão do usuário
- **Path safety**: usar Write tool ao invés de Bash mkdir (evita conflitos Windows/Unix)
- **Atomic generation**: todos os arquivos do squad criados sem estados incompletos

### Fluxo de criação de squad (4 fases)
1. **Discovery** (3-4 perguntas): propósito, audiência/contexto, referências, domínio
2. **Research** (fase 1.5 — Sherlock): análise de perfis de referência
3. **Extraction**: converter pesquisa em artefatos operacionais
4. **Design**: apresentar arquitetura proposta para aprovação do usuário

### Padrão para squads de conteúdo
- Pesquisadores separados (só descoberta, não geração de ângulos)
- Criadores específicos por plataforma (ângulos + conteúdo)
- Agentes revisores obrigatórios
- Checkpoints antes de qualquer geração visual ou publicação

### Padrão de definição de agente (`.agent.md`)
Mínimo 100 linhas com:
- Persona (Role, Identity, Communication Style)
- Mínimo 6 princípios específicos do domínio
- Frameworks operacionais com 5+ passos concretos
- Voice guidance (vocabulário, tom)
- Exemplos de output (15+ linhas, realistas)
- Anti-patterns (Never Do / Always Do)
- Critérios de qualidade e specs de integração

Nomenclatura: aliteração no idioma do usuário (ex: "Tiago Twitter", "Diana Design")

### Modos de execução
| Modo | Descrição |
|------|-----------|
| Alta Performance | Pipelines completos, múltiplas passes de otimização, variantes A/B |
| Econômico | Single-pass simplificado, revisão leve |

### Gates de validação (bloqueantes)
- Agente: mínimo 100 linhas com todas as seções obrigatórias
- Task: mínimo 50 linhas com processo, exemplos e condições de veto
- Step: mínimo 60 linhas com templates e exemplos
- **Content approval gate**: steps de visual/publicação devem ter checkpoint imediatamente antes

---

## Pipeline Runner (`runner.pipeline.md`)

Executa pipelines passo a passo com coordenação de agentes, resolução de skills, versionamento de output e atualização do estado do dashboard.

### Inicialização
1. **Skill Verification**: valida todos os skills não-nativos em `skills/{skill}/SKILL.md`
2. **State Init**: gera run ID (`YYYY-MM-DD-HHmmss`), cria pastas de output, cria `state.json`
3. **Agent Loading**: carrega `.agent.md` completo (frameworks, exemplos, anti-patterns, voice)

Posição dos agentes no dashboard: `col = (index % 2) + 1`, `row = floor(index / 2) + 1`

### Modos de execução de steps
| Modo | Como funciona |
|------|---------------|
| Subagent | Dispatch via Task tool, seleciona tier (`fast` ou `powerful`) |
| Inline | Assume persona do agente, anuncia trabalho, apresenta output diretamente |
| Checkpoint | Apresenta escolhas ao usuário, coleta input, salva em `outputFile` |

### Versionamento de output
Path transform em 2 passos:
1. Inserir `{run_id}` após `output/`
2. Detectar versões existentes via Bash, incrementar maior versão, inserir pasta de versão

Exemplo: `output/slides/draft.md` → `output/2026-03-03-143022/slides/v1/draft.md`

### Quality enforcement
- Condições de veto checadas pós-execução
- Máximo 2 tentativas de fix por step antes de escalar para o usuário

### Dashboard updates
Escritas obrigatórias de `state.json`: antes de cada step, durante handoffs (delivering→working), ao completar. Cleanup final após janela de 10s.

---

## Skills Engine (`skills.engine.md`)

Gerencia integrações de skills via sistema de diretórios. Skill instalado = `skills/<nome>/SKILL.md` presente.

### Tipos de skill
| Ícone | Tipo | Descrição |
|-------|------|-----------|
| 🔌 | mcp | Integração com servidor MCP |
| 📜 | script | Scripts customizados |
| 🔀 | hybrid | MCP + script |
| 💡 | prompt | Apenas instruções comportamentais |

### 7 operações do engine
1. **List**: scan do diretório `skills/`, exibe tipo, versão, descrição, categorias, status de env vars
2. **Install**: busca SKILL.md do catálogo GitHub, cria diretório, escreve manifest, configura MCP/env
3. **Create**: requer skill `opensquad-skill-creator` instalada para guiar criação
4. **Remove**: lista numerada, avisa se squads dependem, remove diretório, limpa `.claude/settings.local.json`
5. **Resolve for Pipeline**: valida todos os skills do squad antes da execução; diferencia nativos (`web_search`, `web_fetch`) de instalados
6. **Inject Instructions**: injeta corpo do SKILL.md no contexto do agente em runtime
7. **Discovery**: durante criação de squad (fase 3.5), faz match de skills por categoria com requisitos

---

## Sherlock (`prompts/sherlock.prompt.md`)

Subagente de investigação de perfis de referência. Dispatchado pelo Architect na fase 1.5.

### Workflow
1. Architect recebe URLs de referência no discovery
2. Lança um subagente Sherlock por URL
3. Cada subagente produz 2 arquivos em `squads/{squad}/_investigations/{username}/`:
   - `raw-content.md` — conteúdo extraído sem edição
   - `pattern-analysis.md` — análise estruturada de padrões
4. Architect consolida em `consolidated-analysis.md`
5. Análise enriquece todos os arquivos de dados da fase 3

### Plataformas suportadas
| Plataforma | Modo de extração |
|-----------|-----------------|
| Instagram | Até 10 posts do grid |
| YouTube | 8-10 vídeos recentes, transcrição via yt-dlp + Whisper |
| Twitter/X | 15-20 tweets recentes, prioriza threads sobre replies |
| LinkedIn | 10-15 posts e artigos recentes |

### Modos de investigação
- `single_post` — apenas um post específico
- `profile_1` — um post do perfil
- `profile_5_10` — até 10 posts do perfil

### Requisitos técnicos
- **Sempre:** Playwright MCP (`browser_navigate`, `browser_snapshot`, `browser_click`, `browser_evaluate`)
- **Para vídeo:** yt-dlp + ffmpeg + OpenAI Whisper (sem eles, continua mas sem transcrição)
- Browser profile: `_opensquad/_browser_profile/` (mantém cookies de login)
- Screenshot paths: sempre especificar path completo

### Mapeamento de output para arquivos de squad
| Arquivo investigação | Alimenta |
|---------------------|----------|
| output-examples.md | Exemplos de conteúdo real |
| quality-criteria.md | Critérios baseados em conteúdo de alta performance |
| tone-of-voice.md | Tom extraído de conteúdo real |
| domain-framework.md | Framework baseado em padrões do domínio |

---

## Best Practices — Catálogo (`best-practices/`)

23 guias em 2 categorias. Selecionados pelo Architect ao criar squads para enriquecer agentes.

### Disciplinas (8)
| Arquivo | Quando usar |
|---------|-------------|
| `copywriting.md` | Agentes de escrita persuasiva |
| `researching.md` | Agentes de pesquisa e coleta de dados |
| `image-design.md` | Agentes de design visual e HTML/CSS |
| `review.md` | Agentes de revisão e controle de qualidade |
| `social-networks-publishing.md` | Agentes de publicação em redes sociais |
| `strategist.md` | Agentes estratégicos |
| `technical-writing.md` | Agentes de documentação técnica |
| `data-analysis.md` | Agentes de análise de dados |

### Plataformas (14)
Instagram Feed, Instagram Reels, Instagram Stories, LinkedIn Post, LinkedIn Article, Twitter Post, Twitter Thread, YouTube Script, YouTube Shorts, Email Newsletter, Email Sales, Blog Post, Blog SEO, WhatsApp Broadcast

---

## Best Practices — Pontos críticos por disciplina

### Copywriting
- Investir 50% da energia criativa no hook (abertura)
- 3 opções de hook antes de escrever o body (cada um com driver emocional diferente)
- Emoção precede lógica — lead com sentimento, suporte com prova
- Diagnóstico obrigatório: nível de consciência (Schwartz), sofisticação do mercado, Big Idea, driver psicológico dominante
- CTA Ladder: Nível 1 (salva/segue) → ... → Nível 5 (compromisso high-ticket)
- Redução de 15-25% de palavras no processo de revisão

### Researching
- Mínimo 2 fontes independentes para cada finding
- Níveis de confiança: alto (3+ fontes), médio (2), baixo (1 ou contraditório)
- Estrutura obrigatória de brief: Key Findings + Trending Angles + Sources + Recommendations + Gaps
- Nativo (web_search) primeiro; Playwright só quando nativo não acessa
- Parar pesquisa quando fontes adicionais confirmam sem novidades (diminishing returns)

### Image Design
- HTML 100% self-contained: CSS inline, sem CDN, sem JS, sem fontes externas (exceto Google Fonts @import)
- Tamanhos mínimos: Instagram carousel — hero 58px, heading 43px, body 34px, caption 24px
- Contraste WCAG AA: 4.5:1 mínimo texto/fundo
- Máximo 5 cores no design system
- **Proibido:** contadores de slide em imagens de carousel (Instagram provê navegação nativa)
- Grid/Flexbox para layout; nunca `position: absolute` como layout primário

### Review / Quality Control
- Vereditos: APPROVE (média ≥7, sem critério <4) | CONDITIONAL (média ≥7, não-crítico 4-6) | REJECT (média <7 OU qualquer critério <4)
- Critério abaixo de 4 = rejeição automática mesmo com média alta
- Feedback sempre executável: citar parágrafo exato + fornecer a correção, não só o problema
- Separar "Required change:" de "Suggestion (non-blocking):"
- Máximo 3 ciclos de revisão com os mesmos problemas antes de escalar

### Social Networks Publishing
- **NUNCA publicar sem confirmação explícita do usuário** — dry-run ≠ aprovação para publicar
- Dry-run sempre primeiro; verificar credenciais, specs, conectividade de API
- Publicação sequencial por plataforma (nunca em paralelo)
- Constraints Instagram: JPEG only, 2-10 imagens, 2.200 chars legenda
- Verificar rate limits ANTES de tentar publicar

### Instagram Feed (Carrosséis)
- Hierarquia de engajamento: Saves > Shares > Comments > Likes
- Carrosséis têm 1.4x mais alcance que imagens únicas
- 7 formatos: Editorial/Tese, Listicle, Tutorial, Mito vs Realidade, Antes e Depois, Storytelling, Problema→Solução
- Melhor horário: 9-11h ou 19-21h (fuso do público), Ter-Qui
- Cadência: 4-7x/semana mantém favor algorítmico
- Primeiros 30-60 min de engajamento definem distribuição

### Instagram Reels
- Watch time é a métrica dominante: completion rate e replays impulsionam distribuição
- 85% dos usuários assistem sem som — legendas obrigatórias
- Estrutura: Hook (0-2s) → Setup (2-5s) → Delivery (5-60s) → CTA (últimos 3-5s)
- Cortes visuais a cada 3-5 segundos
- Ritmo de script: 130-150 palavras por minuto
- Loop design: final deve conectar de volta ao início visualmente
