# Hero-Skills-Framework v2.3

Setup completo e otimizado do Claude Code do Davi Medeiros. 937 commands, 354 agents, 220 skills, 28 hooks, 14 marketplaces, Opensquad multi-agent orchestration, GSD meta-prompting, e muito mais.

## Quick Install

```bash
git clone https://github.com/davimedeirosof/Hero-Skills-Framework.git
cd Hero-Skills-Framework
./install.sh
```

## Changelog

### v2.1
- +9 skills: apify, blotato, canva, image-creator, image-fetcher, image-generator, instagram-publisher, opensquad-agent-creator, opensquad-skill-creator
- +1 agente: skill-hunter (busca e instala novas skills automaticamente)
- Painel dinamico com stats atualizados via GitHub Actions
- CLAUDE.md: persona Hero configurada

### v2.0 (base)
937 commands, 354 agents, 220 skills, 28 hooks

## V1 vs V2.1

| Componente | V1 | V2.1 | Crescimento |
|---|---|---|---|
| Slash Commands | 109 | 937 | 8.6x |
| Agents | 16 | 354 | 22.1x |
| Skills | 0 | 220 | novo |
| Hooks | 22 | 28 | +27% |
| Marketplaces | 5 | 14 | 2.8x |
| Project Rules | 8 | 8 | = |
| Opensquad | - | 30 files | novo |
| Command Namespaces | 15 | 86 | 5.7x |

### Novos namespaces na V2

**Desenvolvimento:**
- `deploy/` — releases, rollbacks, CI/CD, containerization, Kubernetes
- `dev/` — code review, debugging, refactoring, ultra-think, parallel builds
- `docs/` — API docs, architecture, troubleshooting, migration guides
- `performance/` — audit, bundle, caching, CDN, database, monitoring
- `project/` — init, milestones, health checks, PAC (Product as Code)
- `setup/` — environment, linting, formatting, monorepo, database, GraphQL
- `sync/` — GitHub/Linear bidirectional sync, cross-references
- `team/` — standup, sprint planning, retrospectives, workload balancing
- `test/` — comprehensive testing (unit, E2E, visual, load, mutation, property-based)
- `orchestration/` — task orchestration system
- `spec-workflow/` — spec-driven development with parallel tasks

**AI/Reasoning:**
- `boundary/` — knowledge boundary detection, hallucination prevention
- `context/` — prompt optimization for token efficiency
- `memory/` — memory checkpoint, compression, merge, recall, pruning
- `reasoning/` — multi-path reasoning, chain validation, logic vectors
- `semantic/` — semantic tree management
- `wfgy/` — WFGY semantic reasoning formulas

**Marketing (full suite):**
- `mktg-analytics/`, `mktg-audit/`, `mktg-brand/`, `mktg-campaign/`
- `mktg-checklist/`, `mktg-competitor/`, `mktg-content/`, `mktg-crm/`
- `mktg-cro/`, `mktg-growth/`, `mktg-leads/`, `mktg-marketing/`
- `mktg-ops/`, `mktg-pricing/`, `mktg-report/`, `mktg-research/`
- `mktg-sales/`, `mktg-seo/`, `mktg-sequence/`, `mktg-settings/`, `mktg-social/`
- `mktg-training/` (EN, PT-BR, ES, FR, DE, JA, KO, ZH, AR, RU, VI)

**Expert Squads (multi-agent teams):**
- `advisory-board/` — Ray Dalio, Charlie Munger, Naval Ravikant, Peter Thiel...
- `brand-squad/` — David Aaker, Marty Neumeier, Al Ries...
- `c-level-squad/` — CTO, CMO, COO, CIO, CAIO architects
- `claude-code-mastery/` — meta-optimization of Claude Code itself
- `copy-squad/` — Gary Halbert, Eugene Schwartz, David Ogilvy...
- `cybersecurity/` — pentest, recon, incident response, OWASP audit
- `data-squad/` — Sean Ellis, Avinash Kaushik, Peter Fader...
- `design-squad/` — Brad Frost, Dan Mall, UX/UI engineers
- `hormozi-squad/` — Alex Hormozi business frameworks
- `movement/` — movement building, manifestos, identity creation
- `storytelling/` — Joseph Campbell, Nancy Duarte, Blake Snyder...
- `traffic-masters/` — paid media experts, ad account auditing

**Domain-specific:**
- `media/` — video frame extraction, ElevenLabs transcription
- `rust/` — Rust architecture audits, Tauri MCP integration
- `simulation/` — business scenarios, digital twins, decision trees
- `svelte/` — Svelte 5+ development, Storybook, testing
- `skills/` — skill builder, packager, validator
- `session/` — handoff documents for session continuity
- `webmcp/` — WebMCP tool creation and management

### 354 Agent Personas

Agentes especializados cobrindo todas as areas:
- **Dev:** React, Next.js, Vue, Svelte, Angular, Django, Rails, Spring Boot, Laravel, Flutter, Swift, Kotlin, Rust, Go, C/C++, Elixir
- **Infra:** Kubernetes, Docker, Terraform, AWS/Azure/GCP, CI/CD, SRE
- **Data:** PostgreSQL, database optimization, data engineering, ML/MLOps
- **Security:** penetration testing, security auditing, compliance
- **Business:** product management, project management, UX research
- **Marketing:** SEO, paid media, content, social, email, CRO, analytics
- **China market:** Douyin, Xiaohongshu, WeChat, Baidu, Bilibili, Kuaishou

### 220 Skills

Libraries de skills organizadas por funcao:
- **Learning Network (ln-*):** 50+ skills para documentacao, auditoria, bootstrap, testing, otimizacao
- **Marketing:** copywriting, content strategy, SEO, email marketing, pricing, CRO
- **Opensquad:** multi-agent orchestration framework completo

### Opensquad (novo)

Framework de orquestracao multi-agente com:
- Architect agent para criacao de squads
- Sherlock investigator para analise de perfis sociais
- Pipeline Runner para execucao automatica
- 24 best-practices guides (Instagram, YouTube, Twitter, LinkedIn, etc.)
- Browser persistente para sessoes de redes sociais

### Novos hooks na V2

- `gsd-context-monitor.js` — monitoramento de contexto GSD
- `gsd-statusline.js` — status line dinamica
- `gsd-check-update.js` — verificacao de updates GSD
- `pre-compact-save.js` — salva estado antes de compact
- `post-compact-restore.js` — restaura contexto pos-compact
- `context-health-monitor.js` — monitora saude do contexto

## Estrutura

```
Hero-Skills-Framework/
├── install.sh              # Script de instalacao
├── settings.json           # Config global (hooks, permissions, marketplaces)
├── .mcp.json               # MCP servers config
├── CLAUDE.md               # Persona Hero
├── commands/               # 937 slash commands (86 namespaces)
├── agents/                 # 354 agent personas
├── skills/                 # 220 skill libraries
├── hooks/                  # 28 hook scripts
│   ├── scripts/            # Hook scripts (Node.js)
│   ├── gsd-context-monitor.js
│   ├── gsd-statusline.js
│   └── gsd-check-update.js
├── project-rules/          # 8 rules templates
├── _opensquad/             # Multi-agent orchestration framework
│   ├── core/               # Core engine
│   ├── best-practices/     # 24 content guides
│   └── config/             # Playwright config
└── README.md
```

## Pos-instalacao

Rodar dentro do Claude Code:

```
/plugin install planning-with-files@planning-with-files
/plugin install claude-hud
/claude-hud:setup
/plugin install oh-my-claudecode
/omc-setup
```

## Ferramentas externas

```bash
# Dippy (auto-approve safe bash commands)
brew tap ldayton/dippy && brew install dippy

# Claude Squad (multi-instance manager)
brew install claude-squad

# parry (prompt injection scanner)
cargo binstall parry-ai
```

## Para projetos

Copie as rules para cada projeto:

```bash
mkdir -p seu-projeto/.claude/rules
cp project-rules/* seu-projeto/.claude/rules/
```
