---
name: sdd-testcase-writer
description: Lê um Use Case existente, analisa o fluxo e gera o plano de testes no formato de docs/templates/TEST-CASE-TEMPLATE.md. Não implementa nem executa testes.
---

# Skill: SDD Test Case Writer

> **Documento:** SKILL.md  
> **Autor:** Silverio Leite Jr · Senior Solution Architect · OG1 TI  
> **E-mail:** silverio.leitejr@og1.com.br · **Telefone:** (11) 96020-6334  
> **Versão:** 1.0  
> **Data:** 2026-11-19  

## 1. Missão

Gerar o plano de testes de um pacote SDD a partir do Use Case já escrito.

**Entrada obrigatória:** identificador do Use Case (`NN-slug` ou `UC-NN`).

**Saída:** `docs/sdd/{{NN}}-{{SLUG}}/TEST-CASE-{{NN}}-{{SLUG_UPPER}}.md`  
Não gravar um arquivo único `docs/test-case.md`. Cada pacote tem o seu plano.

Esta skill **não** escreve código de teste e **não** executa a suíte. Isso é da `sdd-developer`, e só depois que este artefato estiver `Aprovado`.

## 2. Ordem de Leitura (subconjunto)

1. `docs/GUIDELINE.md` (convenção de IDs e status)
2. `docs/templates/TEST-CASE-TEMPLATE.md` (modelo obrigatório — seções 1 a 4)
3. `docs/sdd/{{NN}}-{{SLUG}}/USE-CASE-{{NN}}-{{SLUG_UPPER}}.md`
4. `docs/sdd/{{NN}}-{{SLUG}}/USER-STORY-{{NN}}-{{SLUG_UPPER}}.md` (se existir)
5. `docs/PRD.md` (somente o `RF` e os `CA` citados pelo Use Case)
6. `docs/SAD.md` e `docs/ADR.md` (somente para nomear a interface pública real; não inventar rota)

## 3. Comandos

```
Criar plano de testes para o Use Case NN-slug
```

```
Revisar o plano de testes de NN-slug conforme: [descrição]
```

```
Validar cobertura do plano de testes de NN-slug
```

## 4. Comportamento

1. **Localizar o Use Case.** Se o arquivo não existir, avisar e parar. Não criar o Use Case aqui.
2. **Analisar** o fluxo principal, os fluxos alternativos, cada `RU-NN.x` e as extensões A/B/C marcadas como ativas.
3. **Esclarecer** antes de escrever se faltar dado que mude o resultado esperado (valor literal, ator, regra, interface pública). Uma rodada de perguntas objetivas. Não inventar número, status HTTP nem nome de rota.
4. **Preencher o template** mantendo as quatro seções, nesta ordem:
   - **Seams.** Só interfaces públicas citadas no Use Case ou no SAD. Cada seam declara o que captura e o que deixa passar. Detalhe interno (método privado, SQL, mock interno) não é seam.
   - **Fixtures.** Valores literais independentes do cálculo que o teste vai afirmar (zero tautologia). Nome estável (`USER_VALID`, não "o usuário"). Se o Use Case não trouxer o valor, usar `[A VALIDAR]`, não um exemplo de outro domínio.
   - **Cenários**, na ordem de fatia vertical: caminho feliz do fluxo principal primeiro; depois exceções, bordas e segurança que o Use Case realmente descreve. Extensão N/A não gera cenário.
   - **DoR.** Marcar o que ficou coberto e o que ficou `[A VALIDAR]`.
5. **Formato de cada cenário**, igual ao modelo:

```markdown
### `TC-{{NN}}.MM` — [Tipo] Título curto
* **Seam:** `SEAM-0N` | **Rastreabilidade:** `CA-xx`, `RN-{{NN}}-x`
* **Dado** ...;
* **Quando** ...;
* **Então** resultado observável, com literal da fixture quando houver número.
```

6. **Status inicial:** `Draft`. Não marcar `Aprovado`.
7. Se o arquivo já existir, não sobrescrever em silêncio. Mostrar o diff das seções e pedir confirmação.

## 5. Regras

- Um cenário prova um comportamento do Use Case. Sem origem (fluxo, regra ou critério de aceite), o cenário não entra.
- O caminho feliz do fluxo principal é obrigatório. Sem ele o plano não está pronto.
- Resultado esperado descreve o comportamento. Código HTTP só entra se o Use Case ou o SAD já o definir. Caso contrário, `[A VALIDAR]`.
- Proibido acoplar o plano a método privado, SQL direto ou mock de colaborador interno.
- IDs: `TC-{{NN}}.01`, `TC-{{NN}}.02`, … O checkout do template é ilustração de forma, não conteúdo do projeto.

## 6. Definition of Done

- [ ] Use Case de origem lido e citado no cabeçalho.
- [ ] Arquivo gerado em `docs/sdd/{{NN}}-{{SLUG}}/TEST-CASE-{{NN}}-{{SLUG_UPPER}}.md`.
- [ ] Seções 1 a 4 do template presentes.
- [ ] Fluxo principal coberto por ao menos um cenário feliz.
- [ ] Cada cenário tem seam, rastreabilidade, Dado, Quando e Então.
- [ ] Lacunas marcadas com `[A VALIDAR]`, não preenchidas com o exemplo de checkout do template.
- [ ] Status `Draft`. Nenhum código de teste foi escrito.

---

*Skill mantida em `docs/skills/sdd-testcase-writer/SKILL.md`.*
