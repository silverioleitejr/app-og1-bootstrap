---
name: sdd-usecase-writer
description: Gera, altera e valida o Use Case de um pacote SDD a partir do PRD e da User Story, usando docs/templates/USE-CASE-TEMPLATE.md. Não escreve código nem plano de testes.
---

# Skill: SDD Use Case Writer

> **Documento:** SKILL.md  
> **Autor:** Silverio Leite Jr · Senior Solution Architect · OG1 TI  
> **E-mail:** silverio.leitejr@og1.com.br · **Telefone:** (11) 96020-6334  
> **Versão:** 1.3.0  
> **Data:** 2026-11-19  

## 1. Missão

Transformar um requisito do PRD em um Use Case implementável, no formato de `docs/templates/USE-CASE-TEMPLATE.md`.

**Entrada obrigatória:** `NN-slug` do pacote, ou `RF-NN` mais o slug desejado.

**Saída:** `docs/sdd/{{NN}}-{{SLUG}}/USE-CASE-{{NN}}-{{SLUG_UPPER}}.md`

**Não faz:** código, teste automatizado, USER-STORY, TEST-CASE, ADR ou alteração de `SAD.md`. Não marca o artefato como `Aprovado`.

## 2. Ordem de Leitura (subconjunto)

1. `docs/GUIDELINE.md` §3 e §9 (nome de arquivo, IDs, status). Demais itens: subconjunto da ordem de §4
2. `docs/templates/USE-CASE-TEMPLATE.md`
3. `docs/PRD.md` — somente o `RF-NN` pedido, suas regras e os `CA` ligados a ele
4. `docs/sdd/{{NN}}-{{SLUG}}/USER-STORY-{{NN}}-{{SLUG_UPPER}}.md` — se existir
5. `docs/SAD.md` — só para citar a seção (validação, auth, IA, camadas). Não copiar stack para o Use Case
6. `docs/DATABASE-PATTERN.md` — só se o fluxo persiste ou altera dados
7. `docs/NAMING-CONVENTION.md`
8. `docs/DESIGN.md` — só se a Extensão A for ativada
9. `docs/ADR.md` — só entradas que já citem este pacote ou o `RF-NN`

`SLUG_UPPER` é o slug em maiúsculas, conservando o hífen (`04-eventos` → `04-EVENTOS` no nome do arquivo: `USE-CASE-04-EVENTOS.md`).

## 3. Comandos

```
Criar Use Case para NN-slug a partir de RF-NN
```

```
Alterar Use Case NN-slug conforme: [descrição]
```

```
Revisar e validar Use Case NN-slug
```

## 4. Comportamento — Criar

1. **Achar o requisito.** Localizar `RF-NN` no PRD. Se o PRD não existir, ou o RF não existir, parar e pedir o requisito. Não inventar funcionalidade.
2. **Bloqueio de PRD.** Se o trecho daquele RF ainda tiver `[A VALIDAR]`, listar os itens e parar. Use Case não nasce de requisito aberto.
3. **User Story.** Se `USER-STORY-{{NN}}-{{SLUG_UPPER}}.md` não existir, avisar, acionar a `sdd-userstory-writer` e seguir só com o RF, registrando `US-{{NN}}` como `[A VALIDAR]`. Não criar a User Story nesta skill.
4. **Esclarecer antes de escrever** quando faltar qualquer item que mude o fluxo:
   - ator principal e quem não pode executar
   - o que dispara o fluxo e o que é sucesso observável
   - o que está fora de escopo
   - se há tela (Extensão A), integração ou assíncrono (B), ou chamada de modelo (C)
   - quais entidades são lidas ou gravadas
   - regras que rejeitam a operação
   Uma rodada, perguntas numeradas. No máximo duas rodadas. O que continuar em aberto entra como `[A VALIDAR]`, nunca como fato.
5. **Preencher o template inteiro**, Parte I e Parte II. Seção vazia não se apaga: extensão inativa fica `N/A — não se aplica`.
6. **Status inicial:** `Draft`, versão `0.1.0`. Campos de aprovador ficam em branco. Preencher `AUTHOR_*` com os dados do solicitante.

### Como preencher cada seção

**1. Objetivo e escopo.** Uma frase com o resultado para o ator, não a solução técnica. Marcar só as extensões que o RF exige. Fora de escopo com pelo menos um item explícito, tirado do PRD ou da resposta do humano.

**2. Pré-condições.** Estado que já precisa existir (usuário autenticado, registro presente, ADR aceito). Citar seções do SAD pelo número, sem nome de framework.

**3. Contrato de dados.** Entidade, operação (criar, alterar, consultar, remover) e a forma do resultado. Governança aponta para `DATABASE-PATTERN.md` e para a seção de isolamento do SAD. Se o fluxo não persiste, escrever `N/A — sem persistência` em vez de inventar tabela.

**4. Fluxo principal.** Passos numerados, na ordem em que o ator ou o sistema os percebe. A camada de entrada só autentica, valida e responde. Regra de negócio fica no serviço. Persistência, quando houver, é um passo próprio, em transação, com auditoria. O último passo é a resposta de sucesso observável.

**5. Fluxos alternativos.** Os quatro do template só entram se o fluxo puder encontrá-los. Consulta sem gravação não ganha "falha de persistência". Cada alternativo diz o que o ator vê e o que não foi gravado. Sem stack trace, sem detalhe interno, sem código HTTP inventado.

**6. Regras.** Uma regra por linha, ID `RU-{{NN}}.1`, `RU-{{NN}}.2`, na ordem, citando a `RN-NN.x` do PRD que a regra implementa. A regra é uma condição de negócio verificável ("carrinho vazio não confirma"), não um passo repetido. Fronteira de confiança só se o SAD ou o `AGENTS.md` §9 a definirem para este projeto; senão, remover a linha.

**7. Critérios técnicos.** Manter o checklist do template. Não marcar itens como feitos: este artefato ainda não tem teste nem código.

**Extensão A.** Ativa só com interface. Citar a rota ou o componente pelo nome do produto, estados Loading, Empty, Success e Error, e `DESIGN.md`. Sem token inventado.

**Extensão B.** Ativa só com chamada externa ou rotina assíncrona. Gatilho, porta conforme o SAD, idempotência e o que acontece quando o externo falha (timeout, retry, desistência).

**Extensão C.** Ativa só com modelo generativo. Provedor e parâmetros pela seção do SAD. Entrada sanitizada se o SAD exigir. Saída não persiste sem confirmação humana. Telemetria citada, não especificada com nome de SDK.

## 5. Comportamento — Alterar

Ler o Use Case atual. Aplicar só o que foi pedido. Subir a versão (`0.1.0` → `0.1.1`; após aprovação, `1.0.0` → `1.1.0`). Se o status já era `Aprovado`, voltar para `Em revisão` e apagar aprovador e data. Mostrar as seções alteradas antes de gravar se a mudança mudar fluxo, regra ou extensão.

## 6. Comportamento — Revisar e validar

Não reescrever. Devolver um parecer com falhas objetivas:

| Verificação | Falha se |
|---|---|
| Arquivo e cabeçalho | Nome fora de `USE-CASE-NN-SLUG_UPPER.md` ou status ausente |
| Rastro | `RF-NN` citado não existe no PRD, ou o RF ainda tem `[A VALIDAR]` |
| Fluxo | Passo sem resultado observável, ou regra de negócio dentro da camada de entrada |
| Alternativos | Caminho de erro que grava estado parcial |
| Regras | `RU` sem condição verificável, sem `RN` de origem no PRD, ou ID fora de `RU-NN.x` |
| Extensões | Marcada ativa sem conteúdo, ou N/A com conteúdo de implementação |
| Agnosticismo | Nome de framework, biblioteca, banco ou provedor que não seja uma referência a seção do SAD |
| Escopo | Funcionalidade que o PRD lista como fora do MVP |

Encerrar com `Aprovado para revisão humana` ou `Devolver ao autor`, e a lista do que corrigir. Não mudar o status para `Aprovado`.

## 7. Regras

- Um Use Case, um pacote, um fluxo principal. Segundo fluxo principal vira outro `NN-slug`.
- Não copiar placeholder do template (`{{OBJECTIVE_ONE_SENTENCE}}`) para o arquivo final.
- Não promover decisão de arquitetura. Se o RF exigir escolha ainda não registrada, apontar `ADR.md` e parar nessa seção com `[A VALIDAR]`.
- Se o arquivo já existir, não sobrescrever em silêncio. Confirmar ou usar o comando Alterar.

## 8. Definition of Done

- [ ] `RF-NN` de origem identificado e sem `[A VALIDAR]` pendente nesse trecho.
- [ ] Arquivo em `docs/sdd/{{NN}}-{{SLUG}}/USE-CASE-{{NN}}-{{SLUG_UPPER}}.md`.
- [ ] Parte I completa e Parte II com cada extensão `ATIVA` ou `N/A`.
- [ ] Fluxo principal numerado e pelo menos uma regra `RU-{{NN}}.x`, ou `N/A` justificado quando o fluxo não tiver regra própria.
- [ ] Fora de escopo explícito.
- [ ] Status `Draft`. Nenhum código e nenhum TEST-CASE foram escritos.

---

*Skill mantida em `docs/skills/sdd-usecase-writer/SKILL.md`.*
