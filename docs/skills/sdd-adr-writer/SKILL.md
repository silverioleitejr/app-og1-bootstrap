---
name: sdd-adr-writer
description: Analisa um assunto, problema ou mudança de arquitetura em linguagem natural com critérios técnicos de arquitetura, segurança e privacidade. Registra a decisão no docs/ADR.md (append-only), identificando o próximo número e atualizando o índice.
---

# Skill: SDD ADR Writer

> **Documento:** SKILL.md  
> **Autor:** Silverio Leite Jr · Senior Solution Architect · OG1 TI  
> **E-mail:** silverio.leitejr@og1.com.br · **Telefone:** (11) 96020-6334  
> **Versão:** 1.1  
> **Data:** 2026-11-19  

## 1. Missão

Você é responsável por **analisar e registrar Decisões de Arquitetura (ADRs)** a partir de uma descrição em linguagem natural.

**Princípios:**
- Usar o template `docs/templates/ADR-TEMPLATE.md` como modelo.
- Manter o documento `docs/ADR.md` **append-only**.
- Analisar o assunto com critérios de arquitetura de software, segurança da informação e privacidade.
- Consultar o checklist de referência (`docs/templates/CHECKLIST-ARQUITETURA.md`) como guia, adaptando à stack definida no `SAD.md`.
- Identificar o próximo número sequencial de ADR e atualizar o Índice Rápido.

## 2. Documentos de Referência

1. `docs/GUIDELINE.md`
2. `docs/SAD.md`
3. `docs/templates/ADR-TEMPLATE.md`
4. `docs/ADR.md` (se existir)
5. `docs/templates/CHECKLIST-ARQUITETURA.md` (guia de análise)
6. `docs/DATABASE-PATTERN.md` e `docs/AGENTS.md` (quando relevante)

## 3. Comandos Suportados

### 3.1 Registrar nova decisão
```
Registrar ADR: [descrição em linguagem natural do problema ou mudança]
```
ou
```
Analisar e registrar decisão de arquitetura sobre: [assunto]
```

**Comportamento:**

1. **Leitura**  
   Leia o `docs/ADR.md` atual (ou crie a partir do template se não existir).  
   Identifique o maior número de ADR existente e calcule o próximo (`ADR-NNN`).

2. **Análise técnica**  
   Avalie o assunto considerando:
   - Segurança e proteção de dados
   - Desempenho e escalabilidade
   - Disponibilidade e resiliência
   - Manutenibilidade e observabilidade
   - Aderência à stack e padrões do `SAD.md`
   - Princípios de privacidade (menor privilégio, isolamento, minimização de dados)

   Use o checklist como guia. Não force itens de stacks não utilizadas no projeto.

3. **Esclarecimentos**  
   Se faltar informação crítica para uma decisão fundamentada, liste perguntas objetivas e aguarde resposta antes de registrar.

4. **Registro**  
   Adicione ao final de `docs/ADR.md` uma nova entrada no formato:

   ```markdown
   ### ADR-{NNN}
   - **Data:** {{YYYY-MM-DD}}
   - **Status:** Proposta
   - **Assunto:** {{TITULO}}
   - **Contexto:** {{FORCAS_E_RESTRICOES}}
   - **Alternativas:** {{OPCAO_DESCARTADA}} (descartada: {{MOTIVO}}) · {{OPCAO_ESCOLHIDA}} (escolhida)
   - **Decisão:** {{O_QUE_FOI_DECIDIDO}}
   - **Consequências:** + {{GANHO}} / − {{CUSTO}}
   - **Substitui:** —
   - **Pacotes SDD impactados:** `docs/sdd/{{NN}}-{{SLUG}}/`
   ```

   Se esta decisão substitui outra, preencha **Substitui** com o ID antigo e altere somente a linha **Status** do ADR anterior para `Substituída por ADR-{NNN}`.

5. **Atualização do Índice**  
   Adicione uma linha na tabela “Índice Rápido de Decisões” com o novo ID, data, assunto e status.

6. **Saída**  
   Apresente o ADR registrado e um resumo da análise realizada.

## 4. Regras

- Nunca sobrescreva ou apague o corpo de um ADR anterior.
- Status inicial obrigatório: `Proposta`. Só mude para `Aceita` após aprovação humana.
- Ao substituir, altere apenas a linha **Status** do ADR antigo (`Substituída por ADR-NNN`).
- Referencie sempre o `SAD.md` quando a decisão alterar ou complementar a arquitetura base.
- Se a decisão impactar pacotes SDD existentes, liste-os no campo correspondente.
- Mantenha linguagem técnica clara e justificada.

## 5. Definition of Done

- [ ] Próximo número de ADR identificado corretamente.
- [ ] Nova entrada adicionada ao final do documento (append-only).
- [ ] Índice Rápido atualizado.
- [ ] Análise considerou segurança, resiliência e privacidade.
- [ ] Documento salvo em `docs/ADR.md`.

---

*Skill mantida em `docs/skills/sdd-adr-writer/SKILL.md`  
e publicada em `.agents/skills/sdd-adr-writer/SKILL.md`.*
