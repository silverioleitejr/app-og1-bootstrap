# [UC-01] Abrir o workspace e a estrutura inicial

> **Documento:** USE-CASE-01-ABRIR-WORKSPACE.md  
> **Autor:** Silverio Leite Jr  
> **Versão:** 0.1.0  
> **Data:** 2026-11-19  
> **Status:** Draft  
> **Aprovado por:** — · **Data de Aprovação:** —

> **Projeto:** SDD Project Bootstrapper  
> **Pacote SDD:** `docs/sdd/01-abrir-workspace/`  
> **User Story Relacionada:** `US-01` [A VALIDAR] — arquivo ainda não existe; acionar `sdd-userstory-writer`  
> **Test Cases Relacionados:** `TC-01`  
> **Rastreabilidade PRD:** `RF-01` · `RN-01.1` · `RN-01.2` · `CA-01`  
> **Skill Responsável:** `docs/skills/sdd-developer/SKILL.md`

---

## PARTE I — CORE (OBRIGATÓRIO)

### 1. Objetivo e Escopo Técnico

- **Objetivo:** O Arquiteto de Soluções informa a identidade de um projeto e passa a ver o workspace aberto, com a estrutura inicial do método pronta para receber os artefatos, sem comando de terminal.
- **Atores e Sistemas Envolvidos:** Arquiteto de Soluções / Tech Lead. Quem mais pode criar, e quem está impedido, está [A VALIDAR] no PRD §4.
- **Natureza do Pacote:**
  - [x] Extensão A — Interface & UX
  - [ ] Extensão B — Back-end / Integração / Assíncrono
  - [ ] Extensão C — Orquestração de IA
- **Fora de Escopo:**
  - Percorrer as etapas 1 a 8, redigir `PRD.md`, `SAD.md`, `DESIGN.md` ou `AGENTS.md`, escolher skills e publicar no repositório remoto (`RF-02` a `RF-07`).
  - Implementar o produto do projeto que está sendo iniciado.
  - Qualquer passo que peça comando de terminal.

### 2. Pré-condições e Referências

- **Pré-condições:** A pessoa chegou à abertura de um projeto novo. Não existe workspace deste fluxo em andamento. A permissão de quem pode criar está [A VALIDAR].
- **Referências obrigatórias** (conforme GUIDELINE.md §4):
  - `docs/SAD.md` — arquivo ainda não existe. Seções de validação, autenticação e isolamento ficam [A VALIDAR]. Nenhuma escolha de stack entra neste Use Case.
  - `docs/DATABASE-PATTERN.md` — arquivo ainda não existe. Auditoria da criação fica [A VALIDAR].
  - `docs/NAMING-CONVENTION.md` — arquivo ainda não existe no projeto. O nome do pacote segue a convenção do `GUIDELINE.md` §3.
  - `docs/DESIGN.md` — arquivo ainda não existe. Tokens visuais da Extensão A ficam [A VALIDAR].
  - `docs/ADR.md` — sem entrada para `RF-01`. Não há decisão de arquitetura a aplicar.

### 3. Contrato de Dados e Persistência

- **Entidades afetadas:** `workspace` — operação (criar). Um workspace representa um único projeto (`RN-01.1`).
- **Governança:** a criação do workspace e da estrutura inicial ocorre na mesma transação. Se a gravação falhar, nada permanece. Isolamento e colunas de auditoria ficam [A VALIDAR] até existirem `SAD.md` e `DATABASE-PATTERN.md`.
- **Input DTO:** identidade do projeto, conforme validação em `SAD.md` [A VALIDAR]. O PRD não lista os campos dessa identidade.
- **Output DTO:** workspace aberto, vinculado a um projeto, com a estrutura inicial do método visível e pronta para receber artefatos.

### 4. Fluxo Principal

1. O Arquiteto de Soluções pede para abrir um workspace e informa a identidade do projeto.
2. A camada de entrada verifica se a pessoa pode criar [A VALIDAR] e se a identidade foi informada. Não aplica regra de negócio.
3. A entrada delega ao serviço de domínio.
4. O serviço aplica `RN-01.1`: o workspace que será criado representa um único projeto. Aplica `RN-01.2`: a estrutura inicial é a do método, nunca uma pasta vazia.
5. O serviço persiste o workspace e a estrutura inicial na mesma transação, com auditoria [A VALIDAR].
6. A pessoa vê o workspace aberto e a estrutura inicial pronta para os artefatos, sem ter usado terminal.

### 5. Fluxos Alternativos

- **Validação inválida:** a identidade do projeto não foi informada. A entrada devolve erro claro e o serviço não é chamado. Nenhum workspace é criado.
- **Falha de autenticação/autorização:** a pessoa não está apta a criar um workspace [A VALIDAR quem está apto]. O fluxo bloqueia na entrada. Nenhum workspace é criado.
- **Recurso não encontrado:** N/A — este fluxo cria o workspace; não busca um já existente.
- **Identidade já usada:** [A VALIDAR]. O PRD não diz se duas identidades iguais podem coexistir.
- **Falha de persistência:** a transação é desfeita. A pessoa vê que o workspace não foi aberto. Não fica estrutura parcial. O registro do erro não expõe detalhe interno nem segredo.

### 6. Regras de Negócio e Guardrails

- **`[RU-01.1]`** (implementa `RN-01.1`): o workspace criado neste fluxo representa exatamente um projeto. Não nasce workspace sem projeto, nem um workspace com mais de um projeto.
- **`[RU-01.2]`** (implementa `RN-01.2`): a estrutura entregue é a estrutura inicial do método. Estrutura vazia não é resultado de sucesso.
- **Aprovação humana:** não se aplica a este fluxo. A abertura não altera modelo de dados do produto destino nem publica repositório. Mudanças estruturais do Bootstrapper seguem `AGENTS.md` §5.

### 7. Critérios de Aceite Técnicos

- [ ] Fluxo principal coberto por testes.
- [ ] Fluxos de exceção cobertos (identidade ausente, pessoa não apta, falha de persistência).
- [ ] Comandos de qualidade do `AGENTS.md` verdes.
- [ ] Zero segredos expostos.
- [ ] `CA-01` do PRD, na parte de estrutura inicial sem terminal, é verificável por este fluxo. A parte de “não avançar de etapa” pertence ao `RF-02`, não a este Use Case.

---

## PARTE II — EXTENSÕES

### EXTENSÃO A — Interface & UX

> **Status:** ATIVA

- A pessoa abre o workspace por uma vista do produto. O nome da rota fica [A VALIDAR] até o `SAD.md` ou o `DESIGN.md` nomeá-la.
- Diretrizes visuais: exclusivamente o que estiver em `docs/DESIGN.md`. O arquivo ainda não existe [A VALIDAR].
- Estados obrigatórios:
  - **Loading:** a abertura foi pedida e o resultado ainda não voltou.
  - **Empty:** não se aplica à criação. Não há lista vazia neste fluxo.
  - **Success:** workspace aberto e estrutura inicial visível, pronta para artefatos.
  - **Error:** identidade ausente, pessoa não apta, ou falha ao gravar. A vista não mostra um workspace pela metade.

### EXTENSÃO B — Back-end / Integrações

> **Status:** N/A — não se aplica

Este fluxo não chama sistema externo nem rotina assíncrona. Publicar no repositório remoto é `RF-06`.

### EXTENSÃO C — IA Generativa

> **Status:** N/A — não se aplica

A abertura do workspace não usa modelo generativo.

---

*Gerado pela skill `sdd-usecase-writer` a partir de `RF-01`. Status `Draft`. Não implementar enquanto estiver `Draft` ou enquanto os itens `[A VALIDAR]` deste arquivo não forem fechados.*
