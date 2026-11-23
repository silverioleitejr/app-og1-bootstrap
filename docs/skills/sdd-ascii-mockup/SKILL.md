---
name: sdd-ascii-mockup
description: Lê um Use Case aprovado e desenha o mockup das páginas em ASCII. Se faltar informação, pergunta ao arquiteto antes de gravar. Não escreve código.
---

# Skill: SDD ASCII Mockup

> **Documento:** SKILL.md  
> **Autor:** Silverio Leite Jr · Senior Solution Architect · OG1 TI  
> **E-mail:** silverio.leitejr@og1.com.br · **Telefone:** (11) 96020-6334  
> **Versão:** 1.0  
> **Data:** 2026-11-19  

## 1. Missão

Traduzir a Extensão A de um Use Case aprovado em mockup de página, em texto ASCII.

**Entrada obrigatória:** `NN-slug` do pacote.

**Saída:** `docs/sdd/{{NN}}-{{SLUG}}/ASCII-MOCKUP-{{NN}}-{{SLUG_UPPER}}.md`  
A pasta do pacote é a pasta do requisito (`docs/sdd/nn-slug`). Não criar outra pasta fora dela. Não gravar imagem.

**Não faz:** código de interface, alteração do Use Case, TEST-CASE, nem marcação do Use Case como `Aprovado`.

## 2. Ordem de Leitura (subconjunto)

1. `docs/GUIDELINE.md` §3 e §9
2. `docs/sdd/{{NN}}-{{SLUG}}/USE-CASE-{{NN}}-{{SLUG_UPPER}}.md`
3. `docs/DESIGN.md` — somente se a Extensão A estiver ativa
4. `docs/sdd/{{NN}}-{{SLUG}}/USER-STORY-{{NN}}-{{SLUG_UPPER}}.md` — se existir, só para o ator e o benefício

## 3. Gate de entrada

Só desenhar se todas as condições forem verdadeiras:

- O arquivo do Use Case existe. Se não existir, avisar o caminho esperado e parar. Não criar o Use Case.
- O status do Use Case é exatamente `Aprovado`. `Draft` e `Em revisão` bloqueiam. Pedir a aprovação ao arquiteto e parar.
- A Extensão A está `ATIVA`. Se estiver `N/A`, informar que não há página neste pacote e parar. Não inventar tela.

## 4. Comandos

```
Criar mockup ASCII do Use Case NN-slug
```

```
Alterar mockup ASCII de NN-slug conforme: [descrição]
```

## 5. Esclarecimentos

Antes de desenhar, conferir se o Use Case (e o `DESIGN.md`, quando existir) já respondem:

1. Quantas páginas ou vistas existem, e o nome de cada uma.
2. Quem é o ator que olha a tela.
3. Qual é a ação principal.
4. Quais campos, listas ou ações aparecem.
5. O que a pessoa vê em Loading, Empty, Success e Error.
6. O que fica fora da tela (já está no fora de escopo do Use Case).

Se qualquer resposta mudar o desenho e não estiver escrita, fazer uma rodada de perguntas numeradas ao arquiteto e esperar. Não preencher com tela genérica. No máximo duas rodadas. O que continuar aberto fica `[A VALIDAR]` no mockup, não vira bloco desenhado.

## 6. Como desenhar

- Um bloco ASCII por página e, na mesma página, um bloco por estado que o Use Case exige (Loading, Empty, Success, Error). Estado não citado não é desenhado.
- Largura máxima de 72 caracteres. Usar `+`, `-`, `|` e espaços. Sem cor, sem imagem, sem nome de framework.
- Rótulos em português, com as mesmas palavras do Use Case e do `DESIGN.md`.
- A ação principal aparece uma vez, no lugar em que o fluxo principal a dispara.
- Cada bloco cita a origem: seção do Use Case ou estado da Extensão A.
- Não desenhar dado de exemplo que o Use Case não tenha. Usar `[A VALIDAR]` no lugar do valor.

Formato de cada bloco:

```markdown
### Página: {{NOME}} — estado {{ESTADO}}
Origem: UC-{{NN}} Extensão A / §4 passo {{N}}

+------------------------------------------------------------------+
| {{TITULO}}                                                       |
+------------------------------------------------------------------+
| {{CAMPO_OU_LISTA}}                                               |
|                                                                  |
| [ {{ACAO_PRINCIPAL}} ]                                           |
+------------------------------------------------------------------+
```

## 7. Gravação

- Status do mockup: `Draft`. O Use Case aprovado autoriza o desenho; não aprova o desenho sozinho.
- Se o arquivo já existir, não sobrescrever em silêncio. Mostrar quais páginas mudam e pedir confirmação.
- Cabeçalho mínimo: pacote, Use Case de origem, data, status `Draft`.

## 8. Definition of Done

- [ ] Use Case existia e estava `Aprovado` antes do primeiro traço.
- [ ] Extensão A estava `ATIVA`.
- [ ] Perguntas feitas quando faltou página, campo ou estado.
- [ ] Arquivo em `docs/sdd/{{NN}}-{{SLUG}}/ASCII-MOCKUP-{{NN}}-{{SLUG_UPPER}}.md`.
- [ ] Cada página exigida tem bloco ASCII e origem citada.
- [ ] Nenhum código de interface foi escrito.

---

*Skill mantida em `docs/skills/sdd-ascii-mockup/SKILL.md`.*
