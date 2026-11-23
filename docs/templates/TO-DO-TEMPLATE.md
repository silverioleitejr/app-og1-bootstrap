# TO-DO-TEMPLATE.md

> **Documento:** TO-DO.md  
> **Versão:** 0.1.0  
> **Data:** {{DATE}}  
> **Status:** Em uso  

## Matriz de Rastreabilidade e Status

| Pacote (`NN-slug`) | RF | US | UC | TC | Status Spec | Status Código | Prioridade | Responsável |
|--------------------|----|----|----|----|-------------|---------------|------------|-------------|
| {{NN}}-{{SLUG}} | RF-{{N}} | US-{{NN}} | UC-{{NN}} | TC-{{NN}}.xx | Draft | Pendente | Alta | {{OWNER}} |

## Legenda

- **Status Spec:** `Draft` | `Em revisão` | `Aprovado`
- **Status Código:** `Pendente` | `Em andamento` | `Concluído`
- **Prioridade:** Alta | Média | Baixa

## Registro de Aprovação do Plano Técnico

| Pacote | Data | Aprovado por | Observações |
|--------|------|--------------|-------------|
| {{NN}}-{{SLUG}} | {{DATE}} | {{APPROVER}} | {{NOTES}} |

## Regras de Avanço

- PRD com itens `[A VALIDAR]` pendentes **não pode** gerar novos pacotes nem avançar para priorização.
- Um pacote só pode ir para implementação se USER-STORY, USE-CASE e TEST-CASE estiverem com Status `Aprovado`.
- A aprovação do Plano Técnico deve ser registrada na tabela acima antes do início da implementação.

## Histórico

| Data | Pacote | Ação | Autor |
|------|--------|------|-------|
| {{DATE}} | — | Criação inicial (Etapa 1b) | {{AUTHOR}} |
