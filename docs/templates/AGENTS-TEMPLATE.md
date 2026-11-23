# AGENTS.md — Contrato Operacional dos Agentes

> **Documento:** AGENTS.md  
> **Autor:** {{AUTHOR_NAME}} · {{AUTHOR_ROLE}}  
> **E-mail:** {{AUTHOR_EMAIL}} · **Telefone:** {{AUTHOR_PHONE}}  
> **Versão:** 0.1.0  
> **Data:** {{DATE}}  

> **Projeto:** {{PROJECT_NAME}}  
> **Metodologia:** Spec-Driven Development (SDD)  
> **Documento base:** `docs/GUIDELINE.md`

Se qualquer `{{...}}` permanecer neste arquivo depois de copiado para `docs/AGENTS.md`, pare e peça o valor. Não use o placeholder como nome do produto, de pessoa ou de comando.

---

## 1. Ordem de Leitura

Siga **exclusivamente** a ordem canônica definida em `docs/GUIDELINE.md` §4.

Não duplique a lista neste arquivo. `docs/GLOSSARIO.md` não entra nessa ordem: é apoio de vocabulário, lido quando a tarefa usar um termo de domínio.

---

## 2. Contexto do Projeto

- **Produto:** {{PROJECT_NAME}}
- **Stack:** somente a que estiver escrita em `docs/SAD.md`. Não inferir stack a partir de exemplos deste arquivo.
- **Idioma:** documentação em português. Código e identificadores em inglês. Commit: assunto em português; o escopo, se houver, usa o identificador em inglês (`feat(workspace): abre o workspace`).
- **Metodologia:** SDD conforme `GUIDELINE.md`.
- **Nomes:**
  - IDs (`RF-NN`, `CA-NN`, `RN-NN.x`, `US-NN`, `CAU-NN.x`, `UC-NN`, `RU-NN.x`, `TC-NN.MM`, `ADR-NNN`) seguem o `GUIDELINE.md` §3.
  - Palavra de domínio segue o `docs/GLOSSARIO.md` §3, quando o arquivo existir.
  - Termo que não está no glossário: perguntar. Não criar sinônimo.

---

## 3. Ciclo de Trabalho

Siga o ciclo Explore → Plan → Execute do `GUIDELINE.md` §5.

Não escrever código de produção se User Story, Use Case ou Test Case do pacote não estiver `Aprovado`. `Draft` e `Em revisão` bloqueiam a implementação.

---

## 4. Regras de Comportamento

### Sempre

- Seguir a spec e citar os IDs do `GUIDELINE.md` §3.
- Atualizar `docs/TO-DO.md` quando o arquivo existir. Na Etapa 0, não inventar a matriz.
- Parar quando uma suposição mudar fluxo, dado, permissão ou contrato. Registrá-la no relatório não autoriza seguir.
- Suposição que não muda comportamento pode constar em Desvios / suposições, e em nenhum outro lugar.

### Nunca

- Introduzir dependências ou alterar stack ou segurança sem aprovação.
- Modificar migrações aplicadas.
- Commitar segredos.
- Desativar testes ou lint.
- Inventar requisito, regra, campo ou termo de domínio.
- Dividir uma mudança só para ficar abaixo do limite de arquivos da seção 5.
- Escolher um documento e ignorar o outro quando houver conflito.

---

## 5. Quando Pedir Aprovação Humana

Pare e peça aprovação explícita antes de continuar, quando ocorrer qualquer item:

- Alteração de modelo de dados ou migração
- Nova dependência ou versão major
- Mudança em autenticação ou autorização
- Alteração que afete mais de 5 arquivos de produção, sem contar spec, teste gerado em massa nem formatação
- Conflito entre spec, `SAD.md`, `DATABASE-PATTERN.md`, `NAMING-CONVENTION.md` ou `ADR.md`

Enquanto a aprovação não chegar, não há implementação parcial do item.

---

## 6. Comandos Padrão

Substitua o bloco abaixo pelos comandos reais do `SAD.md` antes de publicar este arquivo. Enquanto a linha `EXEMPLO` existir, não execute nada deste bloco.

```bash
# EXEMPLO — apagar e colocar os comandos do projeto
# install: <comando>
# qualidade: <lint> && <typecheck>
# teste: <comando>
```

---

## 7. Convenções de Entrega

- **Branch:** `feat/NN-slug` ou `fix/NN-slug`
- **Commit:** Conventional Commits. Assunto em português. Escopo, se usado, é identificador em inglês.
- **PR:** citar os IDs que a mudança toca: `RF-NN`, `RN-NN.x`, `US-NN`, `CAU-NN.x`, `UC-NN`, `RU-NN.x`, `TC-NN.MM`.

---

## 8. Formato do Relatório Final

Conforme `GUIDELINE.md` §8.

---

## 9. Segurança

A regra de segurança vigente é a do `docs/SAD.md`. Este template não adiciona controle que o SAD não tenha.

Não deixar neste arquivo exemplo apresentado como regra. Se o projeto precisar de uma regra extra, escreva a regra real e apague o exemplo.

```text
EXEMPLO — apagar antes de publicar
- Fronteira em que a interface não acessa persistência nem serviço externo diretamente.
- Sanitização de segredo antes de chamada a modelo, se o SAD exigir.
```

---

## 10. Skills

Fonte da verdade: `docs/skills/`. Publicação: `scripts/sync-skills.sh`, que copia para `.agents/skills/`.

Na cópia inicial, a coluna Publicada fica `não`. Mude para `sim` só depois que o sync tiver rodado e o arquivo existir em `.agents/skills/`. Não procure skill publicada que esta tabela marque como `não`.

| Skill | Fonte (`docs/skills/`) | Publicada (`.agents/skills/`) |
|-------|------------------------|-------------------------------|
| sdd-prd-writer | sdd-prd-writer/SKILL.md | não |
| sdd-userstory-writer | sdd-userstory-writer/SKILL.md | não |
| sdd-usecase-writer | sdd-usecase-writer/SKILL.md | não |
| sdd-testcase-writer | sdd-testcase-writer/SKILL.md | não |
| sdd-developer | sdd-developer/SKILL.md | não |
| sdd-adr-writer | sdd-adr-writer/SKILL.md | não |
| sdd-ascii-mockup | sdd-ascii-mockup/SKILL.md | não |
| sdd-structure-validator | sdd-structure-validator/SKILL.md | não |
| sdd-project-init | sdd-project-init/SKILL.md | não |

Remova a linha da skill que o projeto não usar. Não invente skill que não esteja em `docs/skills/`.

---

*Template. Copiar para `docs/AGENTS.md` e customizar. Não é o contrato do projeto enquanto se chamar template.*
