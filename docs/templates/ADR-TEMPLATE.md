<!--
===============================================================================
INSTRUÇÕES DE USO (NÃO REMOVER ESTE BLOCO)
===============================================================================
1. PROPÓSITO: Um único arquivo `docs/ADR.md` centraliza o histórico cronológico
   das Decisões de Arquitetura do projeto {{PROJECT_NAME}}.
2. REGRA DE REGISTRO (APPEND-ONLY): Nunca apague nem reescreva o corpo de uma
   decisão. Cada nova decisão gera uma entrada sequencial (ADR-001, ADR-002...)
   no final do arquivo e uma linha no Índice Rápido.
3. EXCEÇÃO ÚNICA: ao substituir uma decisão, altere somente a linha **Status**
   do ADR antigo para `Substituída por ADR-NNN`. O restante permanece intacto.
4. STATUS INICIAL: toda entrada nova nasce como `Proposta`. Só passa a `Aceita`
   após aprovação humana. Demais valores: `Substituída por ADR-NNN`, `Depreciada`.
5. RASTREABILIDADE SDD: alinhar ao `docs/SAD.md` e listar os pacotes
   `docs/sdd/NN-slug/` impactados. Se não houver pacote, usar `—`.
===============================================================================
-->

# Registro de Decisões de Arquitetura (ADR) — {{PROJECT_NAME}}

> **Documento:** ADR.md  
> **Autor:** {{AUTHOR_NAME}}  
> **Versão:** 1.1  
> **Data:** {{DATE}}  
> **Status:** Ativo  

> **Projeto:** {{PROJECT_NAME}} (`{{PROJECT_SLUG}}`)  
> **Documento de Arquitetura Base:** `docs/SAD.md`  
> **Metodologia:** Spec-Driven Development (SDD)  
> **Formato:** arquivo único, estilo Nygard + alternativas e substituição  

---

## Índice Rápido de Decisões

| ID | Data | Assunto | Status |
| :--- | :--- | :--- | :--- |
| `ADR-001` | 2026-11-19 | Persistir eventos com outbox | Proposta |

---

## Entradas de Decisão

<!--
EXEMPLO PREENCHIDO (não copiar como decisão real do projeto).
Mostra a densidade esperada de cada campo.
-->

### ADR-001
- **Data:** 2026-11-19
- **Status:** Proposta
- **Assunto:** Persistir eventos com outbox
- **Contexto:** Publicar o evento e gravar o estado no mesmo fluxo perde a mensagem quando o processo falha no meio.
- **Alternativas:** fila direta (descartada: perda em falha) · outbox (escolhida)
- **Decisão:** Gravar o evento na mesma transação do estado e publicar a partir da tabela outbox.
- **Consequências:** + não perde evento em falha parcial / − acrescenta latência e um publicador
- **Substitui:** —
- **Pacotes SDD impactados:** `docs/sdd/04-eventos/`

---

<!--
COPIE O BLOCO ABAIXO PARA REGISTRAR UMA NOVA DECISÃO.
Status inicial: Proposta. Substitui: — ou ADR-NNN.

### ADR-NNN
- **Data:** {{YYYY-MM-DD}}
- **Status:** Proposta
- **Assunto:** {{TITULO}}
- **Contexto:** {{FORCAS_E_RESTRICOES}}
- **Alternativas:** {{OPCAO_DESCARTADA}} (descartada: {{MOTIVO}}) · {{OPCAO_ESCOLHIDA}} (escolhida)
- **Decisão:** {{O_QUE_FOI_DECIDIDO}}
- **Consequências:** + {{GANHO}} / − {{CUSTO}}
- **Substitui:** —
- **Pacotes SDD impactados:** `docs/sdd/{{NN}}-{{SLUG}}/`

---
-->

---

*Arquivo único. Append-only, exceto a linha de Status quando um ADR for substituído.*
