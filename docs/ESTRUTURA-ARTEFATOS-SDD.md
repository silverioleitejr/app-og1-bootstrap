# Estrutura de Artefatos SDD — Atualizada

> **Documento:** ESTRUTURA-ARTEFATOS-SDD.md  
> **Autor:** Silverio Leite Jr · Senior Solution Architect · OG1 TI  
> **Versão:** 1.2  
> **Data:** 2026-11-19  

> **Propósito:** Visão consolidada da estrutura de artefatos após as atualizações de consistência (Prioridades 1 e 2).

---

## Visão Geral

```text
projeto/
│
├── docs/
│   │
│   ├── GUIDELINE.md                 ← AGNÓSTICO (metodologia + ordem canônica)
│   ├── AGENTS.md                    ← CUSTOMIZADO (contrato operacional)
│   ├── PRD.md                       ← CUSTOMIZADO (escopo funcional)
│   ├── SAD.md                       ← CUSTOMIZADO (arquitetura + stack)
│   ├── ADR.md                       ← CUSTOMIZADO (decisões — append-only)
│   ├── DATABASE-PATTERN.md          ← CUSTOMIZADO (padrões de banco)
│   ├── NAMING-CONVENTION.md         ← CUSTOMIZADO (convenções)
│   ├── DESIGN.md                    ← CUSTOMIZADO (identidade visual)
│   ├── TO-DO.md                     ← CUSTOMIZADO (matriz de rastreabilidade)
│   ├── GLOSSARIO.md                 ← Linguagem da metodologia e do projeto
│   ├── BACKLOG.md                   ← Itens pendentes
│   │
│   ├── templates/                   ← TEMPLATES MESTRES
│   │   ├── PRD-TEMPLATE.md
│   │   ├── USE-CASE-TEMPLATE.md
│   │   ├── USER-STORY-TEMPLATE.md
│   │   ├── TEST-CASE-TEMPLATE.md
│   │   ├── TO-DO-TEMPLATE.md
│   │   ├── SAD-TEMPLATE.md
│   │   ├── ADR-TEMPLATE.md
│   │   ├── AGENTS-TEMPLATE.md
│   │   ├── NAMING-CONVENTION-TEMPLATE.md
│   │   ├── DESIGN-TEMPLATE.md
│   │   └── CHECKLIST-ARQUITETURA.md
│   │
│   ├── skills/                      ← FONTE DA VERDADE DAS SKILLS
│   │   ├── sdd-developer/SKILL.md
│   │   ├── sdd-usecase-writer/SKILL.md
│   │   ├── sdd-prd-writer/SKILL.md
│   │   ├── sdd-userstory-writer/SKILL.md
│   │   ├── sdd-structure-validator/SKILL.md
│   │   ├── sdd-project-init/SKILL.md
│   │   ├── sdd-adr-writer/SKILL.md
│   │   ├── sdd-testcase-writer/SKILL.md
│   │   └── sdd-ascii-mockup/SKILL.md
│   │
│   └── sdd/                         ← SPECS POR FUNCIONALIDADE
│       └── NN-slug/
│           ├── USER-STORY-NN-SLUG_UPPER.md
│           ├── USE-CASE-NN-SLUG_UPPER.md
│           ├── TEST-CASE-NN-SLUG_UPPER.md
│           └── ASCII-MOCKUP-NN-SLUG_UPPER.md
│
├── .agents/
│   └── skills/                      ← SKILLS PUBLICADAS (via sync-skills.sh)
│       └── ...
│
├── scripts/
│   └── sync-skills.sh               ← Publica skills de docs/skills/ para .agents/skills/
│
├── src/                             ← código da aplicação
├── db/                              ← schema, migrations, seeds
└── README.md
```

---

## Ordem de Leitura Canônica

Definida exclusivamente em `docs/GUIDELINE.md` §4:

1. GUIDELINE.md
2. AGENTS.md
3. TO-DO.md
4. PRD.md
5. SAD.md
6. ADR.md (se existir)
7. DATABASE-PATTERN.md
8. NAMING-CONVENTION.md
9. DESIGN.md (se aplicável)
10. docs/sdd/NN-slug/

---

## Separação de Responsabilidades

| Artefato | Tipo | Reuso |
|----------|------|-------|
| GUIDELINE.md | Agnóstico | 100% |
| AGENTS.md | Customizado | Por projeto |
| PRD / SAD / ADR / DATABASE / NAMING / DESIGN / TO-DO | Customizado | Por projeto |
| docs/templates/ | Reutilizável | Copiar e instanciar |
| docs/skills/ | Fonte | Versionada no repositório |
| .agents/skills/ | Publicado | Gerado pelo script de sync |
| docs/sdd/NN-slug/ | Customizado | Por pacote |

---

## Fluxo Resumido

1. **Etapa 0 — Fundação:** SAD, DATABASE-PATTERN, NAMING, DESIGN, AGENTS, TO-DO
2. **Etapa 1 — PRD**
3. **Etapa 1b — Decomposição:** RFs → pacotes NN-slug + matriz no TO-DO
4. **Etapa 2–6:** Priorizar → Especificar → Plano → Implementar → Entregar

---

*Estrutura alinhada com a metodologia SDD após as atualizações de consistência.*
