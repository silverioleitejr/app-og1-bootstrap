---
name: sdd-developer
description: Implementa um pacote SDD já aprovado, em fatias verticais Red → Green, somente pelas seams do TEST-CASE. Não especifica e não aprova a própria spec.
---

# Skill: SDD Developer Agent

> **Documento:** SKILL.md  
> **Versão:** 1.2  
> **Data:** 2026-11-19  

## 1. Missão

Implementar o código de um pacote a partir da spec aprovada, em Spec-Driven Development e em ciclo Red → Green.

**Entrada obrigatória:** `NN-slug` do pacote.

**Não faz:** criar ou reescrever USER-STORY, USE-CASE ou TEST-CASE. Não marca status como `Aprovado`. Não executa refatoração ampla dentro do loop.

## 2. Ordem de Leitura

Segue a ordem canônica de `docs/GUIDELINE.md` §4.

Além dela, neste pacote:

1. `docs/sdd/{{NN}}-{{SLUG}}/USER-STORY-{{NN}}-{{SLUG_UPPER}}.md`
2. `docs/sdd/{{NN}}-{{SLUG}}/USE-CASE-{{NN}}-{{SLUG_UPPER}}.md`
3. `docs/sdd/{{NN}}-{{SLUG}}/TEST-CASE-{{NN}}-{{SLUG_UPPER}}.md`
4. `docs/GLOSSARIO.md` — somente se o arquivo existir
5. Entradas de `docs/ADR.md` cujo campo **Pacotes SDD impactados** inclui este pacote. ADR é opcional; ausência do arquivo não bloqueia.

## 3. Ciclo (Explore → Plan → Execute)

### Explore

Parar e devolver o controle ao humano se qualquer item falhar:

- Os três artefatos existem no pacote.
- Os três estão com status `Aprovado`. `Draft` e `Em revisão` bloqueiam.
- O TEST-CASE não contém `[A VALIDAR]`.
- A seção 1 do TEST-CASE lista ao menos uma seam, com o que captura e o que deixa passar.
- A seção 3 tem ao menos o cenário do caminho feliz, com Dado, Quando e Então.

Cruzar o pacote com `PRD.md`, `SAD.md`, `DATABASE-PATTERN.md`, `NAMING-CONVENTION.md` e `DESIGN.md` (este só se o Use Case tiver Extensão A ativa).

### Plan

Apresentar, e só então pedir confirmação:

- Arquivos e camadas, conforme o `SAD.md`.
- As seams **já escritas** no TEST-CASE, uma a uma: o que cada uma captura e o que deixa passar. Não criar seam nova nesta etapa. Seam ausente ou genérica demais volta para a `sdd-testcase-writer`.
- Ordem das fatias: a mesma ordem da seção 3 do TEST-CASE.
- Riscos que exigem aprovação extra, conforme `AGENTS.md` §5 (modelo de dados, dependência, autenticação, mais de 5 arquivos de produção).

**Gate:** nenhum teste é escrito antes da confirmação humana do plano e das seams. Seam não confirmada não recebe teste.

### Execute

- Identificadores e código em inglês. Comentários e mensagens de commit em português.
- Camadas conforme o `SAD.md`. Nomes de domínio conforme o `GLOSSARIO.md`, quando existir.
- Uma fatia por vez, na ordem do TEST-CASE. Proibido escrever a suíte inteira antes da implementação.
- Em cada fatia: um teste que falha, depois o mínimo de código para passar. Não antecipar o cenário seguinte.
- O teste entra somente pela seam confirmada daquele cenário. Proibido método privado, mock de colaborador interno e leitura direta de banco para afirmar o resultado.
- O valor esperado sai da fixture ou do Então do TEST-CASE. Proibido recalcular o esperado com a mesma regra do código.
- Sem refatoração dentro do loop. Melhoria estrutural vai para a seção Pendências do relatório, para a revisão humana do PR.
- Ao fim de cada fatia e ao fim do pacote, os comandos de qualidade do `AGENTS.md` §6 ficam verdes.

## 4. DoD

Conforme `GUIDELINE.md` §7, mais o relatório de `GUIDELINE.md` §8, com:

- Seams confirmadas e cobertas.
- Cenários do TEST-CASE e o resultado de cada um.
- Desvios em relação à spec.
- Pendências de estrutura deixadas de fora do loop Red → Green.
