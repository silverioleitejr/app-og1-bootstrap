---
name: sdd-structure-validator
description: Valida a estrutura de pastas, documentos de fundação, templates, skills e pacotes SDD de um projeto sem alterar nenhum arquivo.
---

# Skill: SDD Structure Validator

> **Documento:** SKILL.md  
> **Autor:** Silverio Leite Jr · Senior Solution Architect · OG1 TI  
> **Versão:** 1.3  
> **Data:** 2026-11-23  

## 1. Missão

Auditar a aderência de um projeto à estrutura SDD e emitir um relatório objetivo de gaps.

**Regra fixa:** somente leitura. Nunca cria, altera, move nem remove arquivos.

## 2. Ordem de Leitura (subconjunto)

1. `docs/GUIDELINE.md` §3, §4 e §10
2. `docs/ESTRUTURA-ARTEFATOS-SDD.md` (se existir)

## 3. Verificações mínimas

### 3.1 Estrutura raiz e segurança
- Diretórios obrigatórios: `docs/`, `docs/templates/`, `docs/sdd/`, `.agents/skills/`, `src/`, `db/`.
- Arquivos raiz: `README.md` e `.gitignore`.
- `.gitignore` deve bloquear `README.ini` (ou `readme.ini`), `.env` e `.env.*`.

### 3.2 Documentos de fundação em `docs/`
- Presença de: `GUIDELINE.md`, `AGENTS.md`, `PRD.md`, `SAD.md`, `DATABASE-PATTERN.md`, `NAMING-CONVENTION.md`, `TO-DO.md` e `GLOSSARIO.md`.
- `DESIGN.md`: obrigatório quando o projeto possuir interface (Extensão A).
- **Proibido:** existência de `DESIGN-SYSTEM.md` (nome oficial é `DESIGN.md`, conforme `GUIDELINE.md` §10).
- **Unicidade / sem duplicatas (Bloqueante):** artefatos críticos de fundação (`GUIDELINE.md`, `AGENTS.md`, `PRD.md`, `SAD.md`, `ADR.md`, `DATABASE-PATTERN.md`, `NAMING-CONVENTION.md`, `DESIGN.md`, `TO-DO.md` e `GLOSSARIO.md`) devem existir **exclusivamente** na raiz de `docs/`. Varrer recursivamente o projeto (incluindo raiz do repositório, subpastas de `docs/` e demais diretórios, excetuando os modelos `*-TEMPLATE.md` em `docs/templates/`) e reportar como `Divergente` (`Bloqueante`) qualquer duplicata ou cópia fora de `docs/`.

### 3.3 Templates em `docs/templates/`
- Obrigatórios (padrão `NOME-TEMPLATE.md`):
  - `PRD-TEMPLATE.md`
  - `USE-CASE-TEMPLATE.md`
  - `USER-STORY-TEMPLATE.md`
  - `TEST-CASE-TEMPLATE.md`
  - `AGENTS-TEMPLATE.md`
- Recomendados (sinalizar como `Aviso` se ausentes): `TO-DO-TEMPLATE.md`, `SAD-TEMPLATE.md`, `ADR-TEMPLATE.md`, `DATABASE-PATTERN-TEMPLATE.md`, `NAMING-CONVENTION-TEMPLATE.md`, `DESIGN-TEMPLATE.md`.

### 3.4 Skills
- **Projeto destino:** `.agents/skills/` presente e populada (cada subpasta de skill contendo `SKILL.md`).
- **Repositório fonte / starter kit** *(quando `docs/skills/` existir)*:
  - Presença das nove skills SDD com `SKILL.md`: `sdd-prd-writer`, `sdd-userstory-writer`, `sdd-usecase-writer`, `sdd-testcase-writer`, `sdd-developer`, `sdd-adr-writer`, `sdd-ascii-mockup`, `sdd-structure-validator` e `sdd-project-init`.
  - `scripts/sync-skills.sh` presente.
  - Paridade entre `docs/skills/` e `.agents/skills/` (mesma presença e, quando possível, mesmo hash).

### 3.5 Pacotes SDD em `docs/sdd/NN-slug/`
- Nome da pasta no padrão `NN-slug` (`NN` com dois dígitos; `slug` em kebab-case minúsculo).
- Arquivos no padrão exato:
  - `USER-STORY-NN-SLUG_UPPER.md`
  - `USE-CASE-NN-SLUG_UPPER.md`
  - `TEST-CASE-NN-SLUG_UPPER.md`
  - `ASCII-MOCKUP-NN-SLUG_UPPER.md` somente se a Extensão A do Use Case estiver ativa.
- **Proibido:** qualquer arquivo com sufixo `-REQUIREMENTS`.

## 4. Formato do relatório

Emitir o relatório sem alterar arquivos, contendo:
- **Alvo validado:** caminho raiz e perfil detectado (`projeto destino` ou `repositório fonte`).
- **Tabela de gaps:**

| Item | Status | Severidade | Detalhe |
|---|---|---|---|
| `<caminho ou regra>` | `OK` / `Ausente` / `Divergente` | `Bloqueante` / `Aviso` | `<observação objetiva>` |

- **Resumo:** total de itens `OK`, `Bloqueantes` e `Avisos`.

---

*Skill mantida em `docs/skills/sdd-structure-validator/SKILL.md`.*
