# Glossário

> **Documento:** GLOSSARIO.md  
> **Autor:** Silverio Leite Jr · Senior Solution Architect · OG1 TI  
> **E-mail:** silverio.leitejr@og1.com.br · **Telefone:** (11) 96020-6334  
> **Versão:** 1.0  
> **Data:** 2026-11-20  
> **Status:** Ativo  

> **Papel:** Apoio de linguagem. Não entra na ordem canônica de `docs/GUIDELINE.md` §4.  
> **Fonte dos nomes:** `docs/GUIDELINE.md` §3, §9 e §10. Se este arquivo divergir do GUIDELINE, vale o GUIDELINE.

---

## 1. Nome de agentes

Skills em `docs/skills/`. A publicação em `.agents/skills/` é uma cópia. A fonte da verdade é `docs/skills/`.

| Agente | O que faz | Não faz |
|---|---|---|
| `sdd-prd-writer` | Gera `docs/PRD.md` a partir de linguagem natural, no formato do `PRD-TEMPLATE.md`. | Não escolhe stack. Não decompõe pacotes. |
| `sdd-userstory-writer` | Gera a User Story de um pacote a partir de um `RF-NN`. | Não escreve Use Case, teste nem código. |
| `sdd-usecase-writer` | Gera o Use Case de um pacote a partir do PRD e, se existir, da User Story. | Não escreve a User Story, o plano de testes nem código. |
| `sdd-testcase-writer` | Lê o Use Case e gera o plano de testes do pacote. | Não implementa nem executa a suíte. |
| `sdd-developer` | Implementa o pacote aprovado, em fatias Red → Green, pelas seams do plano de testes. | Não aprova spec. Não cria seam nova. |
| `sdd-adr-writer` | Analisa uma mudança de arquitetura e acrescenta uma entrada em `docs/ADR.md`. | Não apaga decisão anterior. |
| `sdd-ascii-mockup` | Desenha as páginas do Use Case aprovado em ASCII, quando a Extensão A está ativa. | Não escreve interface. Não desenha se o Use Case não estiver `Aprovado`. |
| `sdd-structure-validator` | Confere pastas, templates e pacotes. Só leitura. | Não corrige arquivo. |
| `sdd-project-init` | Cria `{LOCAL_PATH}/{project-slug-name}`, o repositório Git com esse slug e o projeto Supabase com o mesmo slug. Lê `TOKEN`, `GIT-USER-NAME` e `GIT-USER-EMAIL` do `.env`. | Não escreve spec. Não imprime nem versiona segredo. Não executa sem confirmação. |

---

## 2. Termos da metodologia SDD

### 2.1 Termos

| Termo | Definição |
|---|---|
| SDD | Spec-Driven Development. A especificação aprovada precede o código. |
| GUIDELINE | Metodologia agnóstica. Copiar sem alterar. |
| AGENTS | Contrato operacional de um projeto. Customizado. |
| Pacote | Uma unidade de entrega em `docs/sdd/NN-slug/`. Um fluxo principal. |
| Spec | Os três artefatos do pacote: User Story, Use Case e Test Case. |
| Etapa 0 | Fundação: `SAD`, `DATABASE-PATTERN`, `NAMING-CONVENTION`, `DESIGN` (se houver UI), `AGENTS`, `TO-DO`. |
| Etapa 1 | Consolidar e aprovar o `PRD.md`. |
| Etapa 1b | Quebrar os `RF` em pacotes e preencher a matriz do `TO-DO.md`. Bloqueada enquanto o PRD tiver `[A VALIDAR]`. |
| `[A VALIDAR]` | Lacuna explícita. Não é fato. Impede decomposição no PRD e impede implementação no Test Case. |
| Status da spec | Somente `Draft`, `Em revisão` ou `Aprovado`. |
| DoD | Definição de pronto do `GUIDELINE.md` §7. |
| Seam | Interface pública pela qual um teste observa comportamento. O que ela captura e o que deixa passar fica no Test Case. |
| Extensão A | O pacote tem interface. Exige `DESIGN.md` e estados Loading, Empty, Success e Error quando fizerem sentido. |
| Extensão B | O pacote chama sistema externo ou rotina assíncrona. |
| Extensão C | O pacote usa modelo generativo. Saída não persiste sem confirmação humana. |
| ADR | Decisão de arquitetura. Arquivo único `docs/ADR.md`, append-only. Opcional. Status inicial `Proposta`. |
| Fundação | Documentos que existem antes da primeira spec. Não incluem o código do produto. |

### 2.2 Padrões de nomenclatura

Estas formas são as oficiais. Outras grafias encontradas nos artefatos estão na nota de desvio.

| Item | Forma oficial | Exemplo |
|---|---|---|
| Pasta do pacote | `docs/sdd/NN-slug/` | `docs/sdd/01-abrir-workspace/` |
| `NN` | Dois dígitos | `01` |
| `slug` | kebab-case, minúsculas | `abrir-workspace` |
| `SLUG_UPPER` | O mesmo slug em maiúsculas, com hífen | `ABRIR-WORKSPACE` |
| Arquivo de spec | `TIPO-NN-SLUG_UPPER.md` | `USE-CASE-01-ABRIR-WORKSPACE.md` |
| Sufixo proibido | `-REQUIREMENTS` | Não usar |
| Requisito funcional | `RF-NN` | `RF-01` |
| User Story | `US-NN` | `US-01` |
| Use Case | `UC-NN` | `UC-01` |
| Caso de teste | `TC-NN.MM` | `TC-01.03` |
| Regra de negócio do PRD | `RN-NN.x` | `RN-01.1` |
| Regra do Use Case | `RU-NN.x`, citando a `RN` de origem | `RU-01.1` |
| Critério de aceite do PRD | `CA-NN` | `CA-01` |
| Critério de aceite da User Story | `CAU-NN.x`, citando o `CA` de origem | `CAU-01.1` |
| Decisão de arquitetura | `ADR-NNN` | `ADR-001` |
| Mockup ASCII | `ASCII-MOCKUP-NN-SLUG_UPPER.md`, no pacote | `ASCII-MOCKUP-01-ABRIR-WORKSPACE.md` |
| Identidade visual | `DESIGN.md` | Nunca `DESIGN-SYSTEM.md` |
| Template | `NOME-TEMPLATE.md` em `docs/templates/` | `AGENTS-TEMPLATE.md` |
| Glossário | `docs/GLOSSARIO.md` | Este arquivo |

**Nota.** Estas formas estão em `GUIDELINE.md` §3. O exemplo de checkout no `TEST-CASE-TEMPLATE.md` usa `TC-{{NN}}.MM` e não deve ser copiado como domínio do projeto.

---

## 3. Termos do projeto

Projeto atual: **SDD Project Bootstrapper** (`sdd-project-bootstrapper`).  
Esta seção é a única que muda quando o glossário for copiado para outro projeto. As seções 1 e 2 permanecem.

| Termo | Definição neste projeto |
|---|---|
| Bootstrapper | Aplicação web que conduz a abertura de um projeto SDD até a publicação no repositório remoto, sem comando de terminal. |
| Workspace | Um projeto em preparação. Um workspace representa um único projeto (`RN-01.1`). |
| Identidade do projeto | O que a pessoa informa para abrir o workspace. Os campos ainda estão [A VALIDAR]. |
| Estrutura inicial | Pastas do método entregues na abertura. Não é uma pasta vazia (`RN-01.2`). |
| Etapas 0 a 8 | Jornada guiada do produto. A lista fechada de nomes e o critério de conclusão de cada etapa estão [A VALIDAR] no PRD. |
| Catálogo de skills | Conjunto reutilizável de skills que o projeto destino leva na publicação. |
| Skills padrão | Mínimo do catálogo sem o qual a publicação é recusada (`RN-04.1`). |
| Contrato dos agentes | O `AGENTS.md` do projeto destino, confirmado antes da publicação. |
| Publicação | Criação do repositório remoto e envio da carga inicial pela interface (`RF-06`). |
| Carga inicial | Artefatos confirmados (`PRD.md`, `SAD.md`, `DESIGN.md`, `AGENTS.md`) mais as skills selecionadas. |
| Persona principal | Arquiteto de Soluções / Tech Lead. |
| Persona secundária | Desenvolvedor Full-Stack AI-First. Quem vê qual projeto está [A VALIDAR]. |

Pacote já aberto neste projeto:

| Pacote | Requisito | Artefato | Status |
|---|---|---|---|
| `01-abrir-workspace` | `RF-01` | `USE-CASE-01-ABRIR-WORKSPACE.md` | `Draft` |

User Story e Test Case desse pacote ainda não existem. O PRD continua `Draft` e ainda tem `[A VALIDAR]`, então a Etapa 1b não está liberada para os demais requisitos.
