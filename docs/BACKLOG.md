# BACKLOG.md — Itens Pendentes de Desenvolvimento

> **Documento:** BACKLOG.md  
> **Autor:** Silverio Leite Jr · Senior Solution Architect · OG1 TI  
> **Versão:** 1.0  
> **Data:** 2026-11-19  
> **Status:** Ativo  

---

## Skills a Desenvolver

| ID | Skill | Descrição | Prioridade | Status | Observações |
|----|-------|-----------|------------|--------|-------------|
| BL-01 | `sdd-spec-guardian` | Valida consistência entre USER-STORY, USE-CASE e TEST-CASE de um pacote. Verifica rastreabilidade, cobertura de critérios de aceite e ausência de conflitos com PRD/SAD. | Alta | Pendente | Citada anteriormente na estrutura; não implementada. |
| BL-06 | Skill `sdd-adr-writer` | Analisa e registra decisões de arquitetura no ADR.md | Alta | Concluído | Criada |

---

## Outros Itens de Backlog

| ID | Item | Descrição | Prioridade | Status |
|----|------|-----------|------------|--------|
| BL-03 | Script de sincronização de skills | Copiar/publicar de `docs/skills/` para `.agents/skills/` com verificação de hash. | Média | Concluído | Script em `scripts/sync-skills.sh` |
| BL-04 | Regeneração do deck | Atualizar `Metodologia-SDD-Artefatos.pptx` com a ordem canônica e Etapa 0/1b. | Média | Concluído | Slide de skills + ADR opcional incluídos |
| BL-05 | Neutralização completa do USE-CASE-TEMPLATE | Remover acoplamento residual de stack (Zod, Next.js, Gemini etc.). | Alta | Concluído |

---

## Como usar este backlog

- Novos itens devem ser adicionados com ID sequencial `BL-NN`.
- Ao iniciar o desenvolvimento de um item, mover o status para `Em andamento`.
- Ao concluir, mover para `Concluído` e referenciar o commit/PR.

---

*Backlog vivo. Atualizar conforme novos gaps forem identificados.*
