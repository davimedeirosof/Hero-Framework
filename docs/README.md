# Documentação — Hero Skills & Framework

Estrutura de documentação do repositório. Tudo que é gerado, aprendido ou reutilizável fica aqui.

---

## Estrutura

```
docs/
├── README.md                        ← este arquivo
│
├── agentes/
│   ├── nativos/
│   │   └── agentes-nativos-claude.md   ← 5 agentes built-in do Claude Code
│   └── instalados/
│       └── README.md                   ← índice dos 348 agentes instalados
│
├── skills/
│   └── README.md                       ← índice das 211 skills disponíveis
│
├── projetos/
│   └── README.md                       ← projetos realizados com agentes
│
└── reutilizaveis/
    └── README.md                       ← prompts, padrões e contextos reutilizáveis
```

---

## Como usar

### Incorporar contexto de um projeto anterior
1. Acesse `docs/projetos/nome-do-projeto.md`
2. Copie o conteúdo relevante
3. Cole no início da nova sessão e peça ao Hero para incorporar

### Reutilizar uma skill documentada
1. Acesse `docs/reutilizaveis/`
2. Encontre o padrão desejado
3. Peça ao Hero: _"use o padrão X documentado em reutilizaveis/"_

### Consultar capacidades de um agente
1. Acesse `docs/agentes/`
2. Leia o arquivo do agente desejado
3. Peça ao Hero para delegar a tarefa para aquele agente
