# PRD — SDD Project Bootstrapper (MVP)

> **Documento:** PRD.md  
> **Autor / Product Owner:** Silverio Leite Jr  
> **E-mail:** silverio.leitejr@og1.com.br · **Telefone:** (11) 96020-6334  
> **Versão:** 0.1.0-DRAFT  
> **Data:** 2026-11-19  
> **Status:** Draft  

> **Projeto / Produto:** SDD Project Bootstrapper (`sdd-project-bootstrapper`)  
> **Documentos Relacionados:** `docs/SAD.md` · `docs/DESIGN.md` · `docs/GUIDELINE.md` · `docs/ADR.md` (opcional)

---

## 1. Visão Geral do Produto

### 1.1 Resumo Executivo

O SDD Project Bootstrapper é uma aplicação web de produtividade e governança para arquitetos e desenvolvedores que praticam Spec-Driven Development com apoio de agentes de IA. O produto conduz a abertura de um projeto novo em um fluxo guiado de 9 etapas sequenciais, da estrutura inicial até a publicação no repositório remoto, sem exigir que a pessoa execute comandos em terminal.

### 1.2 Proposta de Valor do MVP

Quem inicia um projeto deixa de remontar, à mão, a documentação, o contrato dos agentes e a carga inicial do repositório. A ferramenta oferece templates e skills reutilizáveis, ajuda a redigir os artefatos e publica a estrutura pronta, com histórico consultável.

> **Nota de Governança SDD:** Este documento descreve exclusivamente o escopo funcional, as regras de negócio e a experiência esperada. Decisões de stack, persistência, integrações, segurança técnica e infraestrutura ficam no `docs/SAD.md` e no `docs/ADR.md`.

---

## 2. Problema, Contexto e Hipótese de Negócio

### 2.1 Contexto Atual

Abrir um projeto web aderente à metodologia SDD exige uma sequência repetida de preparação documental, estrutural e de contexto para agentes. Feita à mão, a sequência muda de repositório para repositório e atrasa o início da implementação.

### 2.2 Dores e Problemas Identificados

- **Dor 01:** As 9 etapas estruturais e documentais são repetidas manualmente a cada projeto novo.
- **Dor 02:** `PRD.md`, `SAD.md`, `DESIGN.md` e `AGENTS.md` não seguem o mesmo padrão entre repositórios.
- **Dor 03:** Etapas críticas são esquecidas antes da codificação assistida por agentes, em especial a seleção de skills e as regras de comportamento no `AGENTS.md`.
- **Dor 04:** Criar o repositório remoto e enviar a carga inicial depende de comandos de terminal.
- **Dor 05:** Não há um lugar único para reutilizar templates e skills nem para acompanhar vários projetos ao mesmo tempo.

### 2.3 Hipótese do MVP

Acreditamos que, ao conduzir as 9 etapas do bootstrap, oferecer templates e skills reutilizáveis, auxiliar na redação dos artefatos e publicar a estrutura direto no repositório remoto, reduziremos o tempo de setup de novos projetos em mais de 80% e levaremos 100% dos projetos publicados a nascer com os artefatos obrigatórios do método.

---

## 3. Objetivos e Métricas de Sucesso (KPIs do MVP)

| Objetivo de Negócio | Métrica / Indicador | Meta do MVP | Como Medir (Visão Funcional) |
| --- | --- | --- | --- |
| Acelerar o setup | Tempo desde a criação do workspace até o repositório pronto | < 3 minutos | [A VALIDAR] marco de início e marco de “pronto” na própria jornada |
| Padronizar artefatos SDD | Projetos iniciados com `PRD.md`, `SAD.md`, `DESIGN.md` e `AGENTS.md` | 100% dos projetos publicados | Conferência da carga publicada |
| Eliminar o terminal | Criação do repositório e envio inicial feitos pela interface | 100% via interface web | Nenhuma etapa do fluxo pede comando ao usuário |
| Reutilizar governança | Projetos publicados com skills padrão escolhidas no catálogo | 100% dos projetos | Registro das skills selecionadas na publicação |
| Dar visibilidade | Histórico de publicações e estrutura remota consultáveis na ferramenta | 100% das publicações rastreadas | Cada publicação gera um registro consultável |

---

## 4. Usuários, Personas e Perfis de Acesso

### Persona 1: Arquiteto de Soluções / Tech Lead *(Principal)*

- **Perfil e Contexto:** Define visão de produto, diretrizes de arquitetura, padrão visual e regras de governança antes de delegar a implementação aos agentes.
- **Objetivo no Produto:** Abrir projetos com rigor metodológico, templates padronizados e rastreio entre vários trabalhos ao mesmo tempo.
- **Principal Frustração Atual:** Repetir a preparação e ainda assim encontrar repositórios incompletos.

### Persona 2: Desenvolvedor Full-Stack AI-First *(Secundária)*

- **Perfil e Contexto:** Usa agentes de desenvolvimento no dia a dia e recebe repositórios já iniciados.
- **Objetivo no Produto:** Encontrar `PRD.md`, `SAD.md`, `DESIGN.md`, `AGENTS.md` e as skills de comportamento prontas para uso.
- **Principal Frustração Atual:** Retrabalho e desvio de escopo quando o repositório nasce sem contrato nem contexto.

Quem pode criar workspace, quem pode publicar e quem apenas consulta ficam [A VALIDAR].

---

## 5. Escopo Funcional do MVP (Requisitos Funcionais)

### 5.1 Mapa de Macro-Fluxo do Usuário (Jornada Principal)

1. **Entrada / Acesso:** A pessoa cria ou abre um workspace de projeto.
2. **Ação Principal:** Percorre as 9 etapas em ordem, da estrutura inicial à revisão dos artefatos, à escolha de skills e ao contrato `AGENTS.md`.
3. **Processamento / Transformação:** A ferramenta monta a carga do projeto a partir dos templates e das escolhas feitas.
4. **Resultado / Entrega de Valor:** O repositório remoto é criado e a carga inicial é publicada pela interface, com registro no histórico.

A lista fechada do que é cada uma das etapas 0 a 8 não foi informada. O nome e o critério de conclusão de cada etapa ficam [A VALIDAR]. O que a demanda já fixa, e que o fluxo precisa conter, está nos requisitos abaixo.

### 5.2 Detalhamento das Funcionalidades

#### `[RF-01]` Abrir o workspace e a estrutura inicial

- **Descrição Funcional:** A pessoa informa a identidade do projeto e recebe a estrutura inicial de pastas do método, pronta para receber os artefatos. Não há comando de terminal.
- **Atores Envolvidos:** Arquiteto de Soluções / Tech Lead.
- **Regras de Negócio Aplicáveis:**
  - `RN-01.1`: Um workspace representa um único projeto.
  - `RN-01.2`: A estrutura inicial segue o padrão do método. A pessoa não começa de uma pasta vazia sem esse padrão.

#### `[RF-02]` Conduzir as 9 etapas em sequência

- **Descrição Funcional:** O produto apresenta as etapas 0 a 8 em ordem e mostra em qual delas o projeto está. A pessoa vê o que falta antes de seguir.
- **Atores Envolvidos:** Arquiteto de Soluções / Tech Lead.
- **Regras de Negócio Aplicáveis:**
  - `RN-02.1`: A etapa seguinte só libera quando a atual está concluída.
  - `RN-02.2`: Etapa pulada não pode ser dada como concluída. [A VALIDAR] se é permitido voltar e reeditar uma etapa já concluída.

#### `[RF-03]` Elaborar e revisar os artefatos de especificação

- **Descrição Funcional:** Nas etapas correspondentes, a pessoa redige e revisa `PRD.md`, `SAD.md` e `DESIGN.md` a partir de templates reutilizáveis, com auxílio de redação. O artefato só entra na carga publicada depois de revisado por ela.
- **Atores Envolvidos:** Arquiteto de Soluções / Tech Lead.
- **Regras de Negócio Aplicáveis:**
  - `RN-03.1`: Os três artefatos são obrigatórios na publicação do MVP.
  - `RN-03.2`: Texto gerado com auxílio permanece em rascunho até a pessoa confirmar. Nada é publicado sem essa confirmação.

#### `[RF-04]` Selecionar skills do catálogo

- **Descrição Funcional:** A pessoa consulta um catálogo de skills reutilizáveis e escolhe quais entram no projeto, incluindo um conjunto padrão oferecido pela ferramenta.
- **Atores Envolvidos:** Arquiteto de Soluções / Tech Lead. O desenvolvedor passa a consumir a seleção já publicada.
- **Regras de Negócio Aplicáveis:**
  - `RN-04.1`: Não é possível publicar sem ao menos as skills padrão do catálogo selecionadas.
  - `RN-04.2`: Skill fora do catálogo não entra no MVP. [A VALIDAR] se a pessoa pode trazer uma skill própria.

#### `[RF-05]` Configurar o contrato operacional dos agentes

- **Descrição Funcional:** A pessoa completa o `AGENTS.md` do projeto com as regras de comportamento, a partir de um modelo, antes da publicação.
- **Atores Envolvidos:** Arquiteto de Soluções / Tech Lead.
- **Regras de Negócio Aplicáveis:**
  - `RN-05.1`: Projeto sem `AGENTS.md` confirmado não pode ser publicado.
  - `RN-05.2`: O contrato referencia as skills escolhidas em `RF-04`. Skill selecionada e omitida no contrato impede a conclusão da etapa.

#### `[RF-06]` Publicar no repositório remoto pela interface

- **Descrição Funcional:** A pessoa cria o repositório remoto e envia a carga inicial sem sair da interface e sem digitar comando. Ao terminar, a ferramenta mostra que a publicação ocorreu e guarda o registro.
- **Atores Envolvidos:** Arquiteto de Soluções / Tech Lead.
- **Regras de Negócio Aplicáveis:**
  - `RN-06.1`: A publicação só ocorre com `RF-03`, `RF-04` e `RF-05` concluídos.
  - `RN-06.2`: Falha na publicação não marca o projeto como publicado e informa o que a pessoa pode tentar de novo.
  - `RN-06.3`: [A VALIDAR] se o destino remoto já precisa existir ou se a ferramenta o cria.

#### `[RF-07]` Acompanhar projetos e publicações

- **Descrição Funcional:** A pessoa vê a lista dos seus projetos, a etapa atual de cada um, o histórico de publicações e a estrutura que foi para o remoto.
- **Atores Envolvidos:** Arquiteto de Soluções / Tech Lead e Desenvolvedor Full-Stack AI-First.
- **Regras de Negócio Aplicáveis:**
  - `RN-07.1`: Toda publicação concluída aparece no histórico, com data e projeto.
  - `RN-07.2`: [A VALIDAR] se o desenvolvedor vê todos os projetos do arquiteto ou apenas os que lhe foram indicados.

---

## 6. Fora do Escopo (Não-Objetivos do MVP)

- **Não-Objetivo 01:** Implementar as funcionalidades do projeto que está sendo iniciado. O Bootstrapper prepara o repositório; não escreve o produto do cliente.
- **Não-Objetivo 02:** Executar o ciclo de codificação dos agentes depois da publicação.
- **Não-Objetivo 03:** Substituir o `SAD.md` do projeto destino. A stack daquele projeto continua sendo decisão do artefato de arquitetura dele.
- **Nota:** Infraestrutura, persistência, integrações e segurança técnica deste Bootstrapper ficam fora deste documento (consultar `SAD.md` e `ADR.md`).

---

## 7. Requisitos Não-Funcionais (Visão de Produto e Qualidade)

| Dimensão | Expectativa de Produto / Negócio |
| --- | --- |
| **Usabilidade** | As 9 etapas são visíveis, a etapa atual é óbvia e nenhuma delas pede comando de terminal. |
| **Disponibilidade / Confiabilidade** | Uma falha na publicação não perde o rascunho já confirmado pela pessoa. [A VALIDAR] meta de disponibilidade. |
| **Privacidade e Conformidade** | Credencial de acesso ao repositório remoto não aparece em artefato do projeto nem no histórico consultável. |
| **Desempenho Percebido** | Do workspace criado ao repositório pronto, menos de 3 minutos no caminho feliz. |
| **Auditabilidade** | Cada publicação guarda quem publicou, quando, quais artefatos e quais skills foram incluídos. [A VALIDAR] retenção desse histórico. |

---

## 8. Critérios de Aceite Globais do MVP

Base para os pacotes em `docs/sdd/NN-slug/` (`USER-STORY`, `USE-CASE` e `TEST-CASE`):

### `CA-01` — Workspace e jornada guiada *(Rastreável a `RF-01` e `RF-02`)*

- [ ] Um projeto novo nasce com a estrutura inicial padrão, sem comando de terminal.
- [ ] A pessoa não avança de etapa com a etapa atual incompleta.

### `CA-02` — Artefatos obrigatórios *(Rastreável a `RF-03` e `RF-05`)*

- [ ] `PRD.md`, `SAD.md`, `DESIGN.md` e `AGENTS.md` existem e foram confirmados pela pessoa antes da publicação.
- [ ] Texto auxiliado permanece em rascunho até a confirmação humana.

### `CA-03` — Skills *(Rastreável a `RF-04`)*

- [ ] O catálogo oferece um conjunto padrão e a publicação inclui as skills que a pessoa selecionou.
- [ ] Publicação sem as skills padrão é recusada.

### `CA-04` — Publicação sem terminal *(Rastreável a `RF-06`)*

- [ ] Repositório remoto e carga inicial são concluídos pela interface.
- [ ] Falha de publicação deixa o projeto como não publicado e preserva o que já estava confirmado.

### `CA-05` — Rastreio *(Rastreável a `RF-07`)*

- [ ] A lista de projetos mostra a etapa atual de cada um.
- [ ] Cada publicação concluída aparece no histórico com data, projeto, artefatos e skills.

---

## 9. Premissas, Dependências de Negócio e Riscos

### 9.1 Premissas e Dependências

- **Premissa 01:** O método SDD já está definido (estrutura, nomes de artefatos e papel do `AGENTS.md`). O Bootstrapper aplica esse método; não o redesenha.
- **Dependência 01:** A pessoa tem permissão para criar ou escrever no destino remoto em que a publicação será feita. [A VALIDAR] o tipo de conta exigido.

### 9.2 Riscos de Produto e Mitigações

| Risco de Negócio / Produto | Probabilidade | Impacto | Estratégia de Mitigação Funcional |
| --- | --- | --- | --- |
| As 9 etapas não estão nomeadas e o fluxo guiado nasce incompleto | Alta | Alto | Não priorizar pacotes até a lista 0–8 e o critério de conclusão de cada etapa saírem de [A VALIDAR] |
| A pessoa confirma artefato fraco só para destravar a publicação | Média | Alto | [A VALIDAR] se o MVP exige um conteúdo mínimo por artefato ou apenas a confirmação explícita |
| Publicação parcial gera repositório que parece pronto e não está | Média | Alto | Estado “publicado” só depois da carga completa; falha permanece visível (`RN-06.2`) |

---

## 10. Visão de Evolução (Roadmap Pós-MVP)

| Fase | Incremento Funcional Previsto | Valor Agregado Esperado |
| --- | --- | --- |
| **v1.1** | [A VALIDAR] reedição de projeto já publicado e nova publicação da diferença | Corrigir artefato sem recomeçar o workspace |
| **v1.2** | [A VALIDAR] convite do desenvolvedor ao projeto do arquiteto | A persona secundária entra sem ver projetos alheios |
| **v2.0** | [A VALIDAR] catálogo compartilhado entre times, além do catálogo padrão do produto | Reuso de governança entre várias pessoas |

---

*PRD gerado pela skill `sdd-prd-writer` a partir da demanda de 2026-11-19. Status `Draft`. Um `RF` com `[A VALIDAR]` no próprio texto não entra na Etapa 1b. O PRD não pode ser marcado `Aprovado` enquanto restar qualquer `[A VALIDAR]`.*
