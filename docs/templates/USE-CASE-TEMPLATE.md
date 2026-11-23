# [UC-{{NN}}] {{USE_CASE_TITLE}}

> **Documento:** USE-CASE-{{NN}}-{{SLUG_UPPER}}.md  
> **Autor:** {{AUTHOR_NAME}}  
> **Versão:** 0.1.0-DRAFT  
> **Data:** {{DATE}}  
> **Status:** Draft  
> **Aprovado por:** {{APPROVER_NAME}} · **Data de Aprovação:** {{APPROVAL_DATE}}  

> **Projeto:** {{PROJECT_NAME}}  
> **Pacote SDD:** `docs/sdd/{{NN}}-{{SLUG}}/`  
> **User Story Relacionada:** `US-{{NN}}`  
> **Test Cases Relacionados:** `TC-{{NN}}`  
> **Rastreabilidade PRD:** {{PRD_SECTION_REF}}  
> **Skill Responsável:** `docs/skills/sdd-developer/SKILL.md`  
> **Aprovado por:** {{APPROVER_NAME}} · **Data:** {{APPROVAL_DATE}}

---

## PARTE I — CORE (OBRIGATÓRIO)

### 1. Objetivo e Escopo Técnico
- **Objetivo:** {{OBJECTIVE_ONE_SENTENCE}}
- **Atores e Sistemas Envolvidos:** {{ACTORS_AND_SYSTEMS}}
- **Natureza do Pacote:**
  - [ ] Extensão A — Interface & UX
  - [ ] Extensão B — Back-end / Integração / Assíncrono
  - [ ] Extensão C — Orquestração de IA
- **Fora de Escopo:**
  - {{OUT_OF_SCOPE_ITEM_1}}

### 2. Pré-condições e Referências
- **Pré-condições:** {{PRECONDITION_1}}
- **Referências obrigatórias** (conforme GUIDELINE.md §4):
  - `docs/SAD.md` (seções {{SAD_SECTIONS}})
  - `docs/DATABASE-PATTERN.md`
  - `docs/NAMING-CONVENTION.md`
  - `docs/DESIGN.md` (se Extensão A)

### 3. Contrato de Dados e Persistência
- **Entidades afetadas:** `{{entity_name}}` — operação ({{OPERATION}})
- **Governança:** mutações em transação atômica, auditoria conforme `DATABASE-PATTERN.md`, isolamento conforme `SAD.md`.
- **Input DTO:** conforme validação definida em `SAD.md` ({{SAD_SECTION_VALIDATION}})
- **Output DTO:** {{OUTPUT_STRUCTURE}}

### 4. Fluxo Principal
1. {{STEP_1_TRIGGER}}
2. Camada de entrada valida autenticação e entrada (conforme `SAD.md` §{{SAD_SECTION_AUTH}}), mantendo-se fina.
3. Delega para serviço de domínio.
4. Serviço executa lógica de negócio.
5. Persistência em transação com auditoria.
6. Retorna resposta de sucesso.

### 5. Fluxos Alternativos
- **Validação inválida:** erro estruturado antes de acessar serviços ou dados.
- **Falha de autenticação/autorização:** bloqueio imediato.
- **Recurso não encontrado:** erro de domínio sem vazamento de detalhes internos.
- **Falha de persistência:** rollback completo + log estruturado (sem stack trace ou segredos).

### 6. Regras de Negócio e Guardrails
- **`[RN-{{NN}}-01]`:** {{BUSINESS_RULE_1}}
- **Fronteira de confiança:** conforme definido em `SAD.md` e `AGENTS.md` §9 (remover se não aplicável).
- **Aprovação humana:** conforme `AGENTS.md` §5.

### 7. Critérios de Aceite Técnicos
- [ ] Fluxo principal coberto por testes.
- [ ] Fluxos de exceção cobertos.
- [ ] Comandos de qualidade do `AGENTS.md` verdes.
- [ ] Zero segredos expostos.

---

## PARTE II — EXTENSÕES (marcar N/A se não aplicável)

### EXTENSÃO A — Interface & UX
> **Status:** {{ATIVA | N/A}}

- Rota / componente: conforme estrutura do projeto.
- Diretrizes visuais: exclusivamente tokens e componentes de `docs/DESIGN.md`.
- Estados obrigatórios: Loading, Empty, Success, Error.

### EXTENSÃO B — Back-end / Integrações
> **Status:** {{ATIVA | N/A}}

- Gatilho: {{TYPE_AND_IDENTIFIER}}
- Port / Adapter: conforme `SAD.md`.
- Idempotência e concorrência: {{RULE_OR_NA}}
- Resiliência: timeout, retry e fail-fast conforme `SAD.md`.

### EXTENSÃO C — IA Generativa
> **Status:** {{ATIVA | N/A}}

- Provedor e parâmetros: conforme `SAD.md` ({{SAD_SECTION_AI}}).
- Sanitização de entrada: obrigatória se definida no SAD (remover se não aplicável).
- Revisão humana do output antes de persistir.
- Telemetria de uso registrada.

---

*Template stack-agnóstico. Todas as decisões técnicas devem referenciar seções do SAD.md.*
