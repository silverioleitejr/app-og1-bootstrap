<!--
===============================================================================
INSTRUÇÕES PARA O AGENTE / SYSTEM PROMPT (NÃO INCLUIR NO OUTPUT FINAL)
===============================================================================
1. OBJETIVO: Transformar a entrada em linguagem natural do usuário em um
   PRD.md estruturado, focado exclusivamente em produto, negócio e escopo funcional.
2. REGRA DE OURO (AGNOSTICISMO TÉCNICO): É estritamente proibido mencionar
   linguagens de programação, frameworks, bancos de dados, provedores de nuvem,
   APIs específicas, bibliotecas ou padrões de código. Toda decisão técnica
   pertence exclusivamente ao SAD.md e aos ADRs.
3. TRATAMENTO DE LACUNAS: Se a descrição inicial omitir algum dado
   (ex.: métricas, personas ou riscos), infira com bom senso de produto para o
   contexto de MVP e marque o trecho com `[A VALIDAR]` para revisão humana.
4. RASTREABILIDADE: Numere funcionalidades (RF-01, RF-02...) e critérios de
   aceite (CA-01, CA-02...) para vínculo com USER-STORY, USE-CASE e TEST-CASE.
5. BLOQUEIO: Enquanto houver `[A VALIDAR]` pendente, o PRD não avança para a
   Etapa 1b (decomposição em pacotes) nem para priorização.
6. SAÍDA: Gerar apenas o Markdown final do PRD.md, sem este bloco de instrução.
===============================================================================
-->

# PRD — {{PROJECT_NAME}} (MVP)

> **Documento:** PRD.md  
> **Autor / Product Owner:** {{AUTHOR_NAME}}  
> **E-mail:** {{AUTHOR_EMAIL}} · **Telefone:** {{AUTHOR_PHONE}}  
> **Versão:** 0.1.0-DRAFT  
> **Data:** {{DATE}}  
> **Status:** Draft  

> **Projeto / Produto:** {{PROJECT_NAME}} (`{{PROJECT_SLUG}}`)  
> **Documentos Relacionados:** `docs/SAD.md` · `docs/DESIGN.md` · `docs/GUIDELINE.md` · `docs/ADR.md` (opcional)

---

## 1. Visão Geral do Produto

### 1.1 Resumo Executivo
{{PRODUCT_OVERVIEW_DESCRIPTION}}

### 1.2 Proposta de Valor do MVP
{{VALUE_PROPOSITION_STATEMENT}}

> **Nota de Governança SDD:** Este documento descreve exclusivamente o **escopo funcional, regras de negócio e experiência esperada pelo usuário**. Decisões de stack, persistência, integrações, segurança técnica e infraestrutura ficam no `docs/SAD.md` e no `docs/ADR.md`.

---

## 2. Problema, Contexto e Hipótese de Negócio

### 2.1 Contexto Atual
{{CURRENT_CONTEXT_AND_SCENARIO}}

### 2.2 Dores e Problemas Identificados
- **Dor 01:** {{PAIN_POINT_1}}
- **Dor 02:** {{PAIN_POINT_2}}
- **Dor 03:** {{PAIN_POINT_3}}

### 2.3 Hipótese do MVP
Acreditamos que ao entregar **{{CORE_MVP_CAPABILITY}}** para **{{TARGET_AUDIENCE}}**, resolveremos as dores acima e alcançaremos **{{EXPECTED_OUTCOME}}**.

---

## 3. Objetivos e Métricas de Sucesso (KPIs do MVP)

| Objetivo de Negócio | Métrica / Indicador | Meta do MVP | Como Medir (Visão Funcional) |
| --- | --- | --- | --- |
| {{OBJECTIVE_1}} | {{METRIC_1}} | {{TARGET_1}} | {{MEASUREMENT_1}} |
| {{OBJECTIVE_2}} | {{METRIC_2}} | {{TARGET_2}} | {{MEASUREMENT_2}} |
| {{OBJECTIVE_3}} | {{METRIC_3}} | {{TARGET_3}} | {{MEASUREMENT_3}} |

---

## 4. Usuários, Personas e Perfis de Acesso

### Persona 1: {{PERSONA_1_NAME}} *(Principal)*
- **Perfil e Contexto:** {{PERSONA_1_DESCRIPTION}}
- **Objetivo no Produto:** {{PERSONA_1_GOAL}}
- **Principal Frustração Atual:** {{PERSONA_1_FRUSTRATION}}

### Persona 2: {{PERSONA_2_NAME}} *(Secundária — se aplicável)*
- **Perfil e Contexto:** {{PERSONA_2_DESCRIPTION}}
- **Objetivo no Produto:** {{PERSONA_2_GOAL}}
- **Principal Frustração Atual:** {{PERSONA_2_FRUSTRATION}}

---

## 5. Escopo Funcional do MVP (Requisitos Funcionais)

### 5.1 Mapa de Macro-Fluxo do Usuário (Jornada Principal)
1. **Entrada / Acesso:** {{JOURNEY_STEP_1}}
2. **Ação Principal:** {{JOURNEY_STEP_2}}
3. **Processamento / Transformação:** {{JOURNEY_STEP_3}}
4. **Resultado / Entrega de Valor:** {{JOURNEY_STEP_4}}

### 5.2 Detalhamento das Funcionalidades

#### `[RF-01]` {{FEATURE_1_TITLE}}
- **Descrição Funcional:** {{FEATURE_1_DESCRIPTION}}
- **Atores Envolvidos:** {{FEATURE_1_ACTORS}}
- **Regras de Negócio Aplicáveis:**
  - `RN-01.1`: {{BUSINESS_RULE_1_1}}
  - `RN-01.2`: {{BUSINESS_RULE_1_2}}

#### `[RF-02]` {{FEATURE_2_TITLE}}
- **Descrição Funcional:** {{FEATURE_2_DESCRIPTION}}
- **Atores Envolvidos:** {{FEATURE_2_ACTORS}}
- **Regras de Negócio Aplicáveis:**
  - `RN-02.1`: {{BUSINESS_RULE_2_1}}
  - `RN-02.2`: {{BUSINESS_RULE_2_2}}

#### `[RF-03]` {{FEATURE_3_TITLE}}
- **Descrição Funcional:** {{FEATURE_3_DESCRIPTION}}
- **Atores Envolvidos:** {{FEATURE_3_ACTORS}}
- **Regras de Negócio Aplicáveis:**
  - `RN-03.1`: {{BUSINESS_RULE_3_1}}
  - `RN-03.2`: {{BUSINESS_RULE_3_2}}

*(Adicionar novos blocos `[RF-NN]` conforme a complexidade do MVP.)*

---

## 6. Fora do Escopo (Não-Objetivos do MVP)

- **Não-Objetivo 01:** {{OUT_OF_SCOPE_1}}
- **Não-Objetivo 02:** {{OUT_OF_SCOPE_2}}
- **Não-Objetivo 03:** {{OUT_OF_SCOPE_3}}
- **Nota:** Infraestrutura, banco de dados, frameworks e integrações de baixo nível ficam fora deste documento (consultar `SAD.md` e `ADR.md`).

---

## 7. Requisitos Não-Funcionais (Visão de Produto e Qualidade)

*(Apenas expectativas perceptíveis pelo usuário ou exigências de negócio. A solução técnica fica no `SAD.md`.)*

| Dimensão | Expectativa de Produto / Negócio |
| --- | --- |
| **Usabilidade** | {{NFR_USABILITY}} |
| **Disponibilidade / Confiabilidade** | {{NFR_RELIABILITY}} |
| **Privacidade e Conformidade** | {{NFR_PRIVACY}} |
| **Desempenho Percebido** | {{NFR_PERFORMANCE}} |
| **Auditabilidade** | {{NFR_AUDIT}} |

---

## 8. Critérios de Aceite Globais do MVP

Base para os pacotes em `docs/sdd/NN-slug/` (`USER-STORY`, `USE-CASE` e `TEST-CASE`):

### `CA-01` — {{ACCEPTANCE_GROUP_1_TITLE}} *(Rastreável a `RF-01`)*
- [ ] {{ACCEPTANCE_CRITERIA_1_1}}
- [ ] {{ACCEPTANCE_CRITERIA_1_2}}

### `CA-02` — {{ACCEPTANCE_GROUP_2_TITLE}} *(Rastreável a `RF-02`)*
- [ ] {{ACCEPTANCE_CRITERIA_2_1}}
- [ ] {{ACCEPTANCE_CRITERIA_2_2}}

### `CA-03` — {{ACCEPTANCE_GROUP_3_TITLE}} *(Rastreável a `RF-03`)*
- [ ] {{ACCEPTANCE_CRITERIA_3_1}}
- [ ] {{ACCEPTANCE_CRITERIA_3_2}}

---

## 9. Premissas, Dependências de Negócio e Riscos

### 9.1 Premissas e Dependências
- **Premissa 01:** {{ASSUMPTION_1}}
- **Dependência 01:** {{DEPENDENCY_1}}

### 9.2 Riscos de Produto e Mitigações

| Risco de Negócio / Produto | Probabilidade | Impacto | Estratégia de Mitigação Funcional |
| --- | --- | --- | --- |
| {{RISK_1}} | Alta / Média / Baixa | Alto / Médio / Baixo | {{MITIGATION_1}} |
| {{RISK_2}} | Alta / Média / Baixa | Alto / Médio / Baixo | {{MITIGATION_2}} |

---

## 10. Visão de Evolução (Roadmap Pós-MVP)

| Fase | Incremento Funcional Previsto | Valor Agregado Esperado |
| --- | --- | --- |
| **v1.1** | {{POST_MVP_V1_1_FEATURE}} | {{POST_MVP_V1_1_VALUE}} |
| **v1.2** | {{POST_MVP_V1_2_FEATURE}} | {{POST_MVP_V1_2_VALUE}} |
| **v2.0** | {{POST_MVP_V2_0_FEATURE}} | {{POST_MVP_V2_0_VALUE}} |

---

*Template de PRD. Instanciar como `docs/PRD.md`. Revisão humana obrigatória antes da decomposição em pacotes.*
