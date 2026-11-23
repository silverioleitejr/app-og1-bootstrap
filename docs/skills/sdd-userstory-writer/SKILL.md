---
name: sdd-userstory-writer
description: Gera, altera e valida a USER-STORY de um pacote SDD a partir de um RF do PRD, usando docs/templates/USER-STORY-TEMPLATE.md. Não escreve Use Case, testes nem código.
---

# Skill: SDD User Story Writer

> **Documento:** SKILL.md  
> **Autor:** Silverio Leite Jr · Senior Solution Architect · OG1 TI  
> **E-mail:** silverio.leitejr@og1.com.br · **Telefone:** (11) 96020-6334  
> **Versão:** 1.0.0  
> **Data:** 2026-11-19  

## 1. Missão

Transformar um `RF-NN` do PRD em uma User Story com critérios de aceite rastreáveis (`CAU-NN.x`).

**Entrada obrigatória:** `NN-slug` do pacote e o `RF-NN` de origem (ou apenas `NN-slug` se o TO-DO já mapear o RF).
**Saída:** `docs/sdd/{{NN}}-{{SLUG}}/USER-STORY-{{NN}}-{{SLUG_UPPER}}.md`
**Não faz:** USE-CASE, TEST-CASE, código. Não marca `Aprovado`.

## 2. Ordem de Leitura (subconjunto)

1. `docs/GUIDELINE.md` §3 e §9
2. `docs/templates/USER-STORY-TEMPLATE.md`
3. `docs/TO-DO.md` (mapeamento pacote ↔ RF)
4. `docs/PRD.md` — só o `RF-NN`, suas `RN-NN.x` e o `CA-NN`
5. `docs/GLOSSARIO.md` (se existir)

## 3. Comandos

```
Criar User Story para NN-slug a partir de RF-NN
```
```
Alterar User Story NN-slug conforme: [descrição]
```
```
Revisar e validar User Story NN-slug
```

## 4. Comportamento

1. Localizar o `RF-NN`. Se o PRD ou o RF não existir, parar e pedir. Se o trecho tiver `[A VALIDAR]`, listar e parar.
2. Uma story por pacote. Se o RF pede mais de um comportamento independente, sugerir dividir em outro `NN-slug` (decisão humana, registrada no TO-DO).
3. Escrever Como / Quero / Para em linguagem de negócio, sem solução técnica.
4. Derivar cada `CAU-NN.x` de um `CA-NN` do PRD, citando a origem. Critério verificável e observável; nada que o PRD não sustente.
5. Esclarecer antes de escrever se faltar ator, benefício ou critério (uma rodada, máx. 2). O que ficar aberto vira `[A VALIDAR]`.
6. Status `Draft`, versão `0.1.0`, aprovador em branco. Autoria dos campos `AUTHOR_*` conforme o solicitante.
7. **Alterar:** aplicar só o pedido, subir a versão; se estava `Aprovado`, voltar a `Em revisão` e limpar aprovador e data; sinalizar impacto em USE-CASE e TEST-CASE.
8. **Revisar:** não reescrever. Falha se: `RF` inexistente ou com `[A VALIDAR]`; `CAU` sem `CA` de origem; critério não verificável; solução técnica na história. Encerrar com `Aprovado para revisão humana` ou `Devolver ao autor`.
9. Não sobrescrever arquivo existente em silêncio.

## 5. Definition of Done

- [ ] Arquivo no caminho e nome corretos (`GUIDELINE.md` §3).
- [ ] Como/Quero/Para preenchidos; ao menos 2 `CAU-NN.x` com origem `CA-NN`.
- [ ] Nenhum placeholder `{{...}}` restante.
- [ ] Status `Draft`; nenhum outro artefato foi escrito.

---

*Fonte em `docs/skills/sdd-userstory-writer/SKILL.md`; publicada por `scripts/sync-skills.sh`.*
