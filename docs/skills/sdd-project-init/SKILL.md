---
name: sdd-project-init
description: Cria a pasta local com a estrutura SDD inicial a partir do repositório central versionado app-og1-bootstrap, o repositório Git privado e o projeto Supabase usando o project-slug-name. Lê GIT_TOKEN, GIT_USER_NAME e GIT_USER_EMAIL do .env. Não imprime nem versiona segredo.
---

# Skill: SDD Project Init

> **Documento:** SKILL.md  
> **Autor:** Silverio Leite Jr · Senior Solution Architect · OG1 TI  
> **E-mail:** silverio.leitejr@og1.com.br · **Telefone:** (11) 96020-6334  
> **Versão:** 2.0  
> **Data:** 2026-11-23  

## 1. Missão

Inicializar um projeto novo com o mesmo identificador nos três destinos: diretório local (populado a partir do repositório central versionado `https://github.com/silverioleitejr/app-og1-bootstrap`), repositório Git privado e projeto Supabase.

**Não faz:** escrever spec, escolher stack, criar tabela, gravar segredo no repositório, imprimir o token, fazer fallback silencioso para pasta local, nem seguir com dado em branco.

## 2. Ordem de Leitura (subconjunto)

1. `docs/GUIDELINE.md` §2.2 (setup do projeto)
2. `docs/AGENTS.md` §5 e §9 (se existir)
3. `docs/GLOSSARIO.md` §3 (se existir)

## 3. Entradas

Perguntar o que faltar e esperar. Não inventar.

| Campo | Obrigatório | Significado |
|---|---|---|
| `project_name` | Sim | Nome de exibição do projeto |
| `project_slug_name` | Sim | Identificador único. `kebab-case`, minúsculas, sem espaço. É o nome da pasta, do repositório Git e do projeto Supabase |
| `local_path` | Sim | Diretório pai. A pasta do projeto é `{local_path}/{project_slug_name}` |
| `bootstrap_ref` | Não | Tag SemVer (ex.: `v1.0.0`) ou branch do repositório central `app-og1-bootstrap`. Padrão: última tag `v*` publicada; se não houver tags, `main` |

O slug que não estiver em `kebab-case` é recusado. Não converter em silêncio.

## 4. Credenciais

Ler somente do arquivo `.env` do ambiente de onde a skill executa. Nunca do chat. Nunca da pasta do projeto novo.

| Variável | Uso |
|---|---|
| `GIT_TOKEN` | Autenticação no GitHub para ler o repositório central `app-og1-bootstrap`, criar o repositório do novo projeto e enviar o commit inicial |
| `GIT_USER_NAME` | `user.name` do Git, só neste repositório |
| `GIT_USER_EMAIL` | `user.email` do Git, só neste repositório |

Se uma das três não existir ou estiver vazia, parar antes de criar qualquer coisa. Dizer o nome da variável ausente. Não pedir o valor no chat.

Não copiar nenhum `.env` para `{local_path}/{project_slug_name}`. Não escrever o `GIT_TOKEN` em arquivo, remote, commit ou resposta. O remote gravado no `.git/config` é a URL limpa, sem token.

## 5. Confirmação

Antes de mostrar o plano, consultar (somente leitura) a versão resolvida (`bootstrap_ref` e `commit_sha`) no repositório central `https://github.com/silverioleitejr/app-og1-bootstrap`.

Mostrar o plano e esperar um **sim**. No plano, o token aparece apenas como `presente` ou `ausente`.

1. Baixar snapshot da versão `{bootstrap_ref}` (`{commit_sha}`) de `https://github.com/silverioleitejr/app-og1-bootstrap` em diretório temporário.
2. Criar `{local_path}/{project_slug_name}`, a estrutura inicial de diretórios SDD definida no `bootstrap-manifest.json` (ou allowlist padrão) e o `.git` dentro dessa pasta.
3. Criar o repositório Git privado com o nome `{project_slug_name}`, autenticado pelo `GIT_TOKEN`.
4. Gravar `.gitignore` (bloqueando `README.ini`, `readme.ini`, `.env`, `**/.env`, `.env.*` e `**/.env.*`), `README.md` e `README.ini` (apenas local, registrando `source_repo`, `version` e `commit_sha`), e enviar a estrutura inicial (sem `README.ini` nem `.env`) à branch `main`.
5. Criar o projeto Supabase com o nome `{project_slug_name}`.

Sem o **sim**, nenhum comando de criação roda.

Parar, sem criar nada, se:

- `{local_path}/{project_slug_name}` já existe e não está vazio.
- O repositório central `https://github.com/silverioleitejr/app-og1-bootstrap` estiver inacessível ou `bootstrap_ref` não existir (nunca fazer fallback silencioso para pasta local).
- O repositório `{project_slug_name}` já existe na conta autenticada pelo `GIT_TOKEN`.
- O projeto Supabase com esse nome já existe.
- Falta `GIT_TOKEN`, `GIT_USER_NAME` ou `GIT_USER_EMAIL`.

## 6. Execução

Se um passo falhar, não executar o seguinte. Informar o que já foi criado e sempre remover o diretório temporário do bootstrap ao final.

### 6.1 Obtenção da versão centralizada e estrutura inicial

1. **Snapshot temporário:** clonar `https://github.com/silverioleitejr/app-og1-bootstrap` com `git clone --depth 1 --branch {bootstrap_ref}` para um diretório temporário (autenticando apenas via header HTTP com `GIT_TOKEN`) e capturar o `commit_sha` (`git rev-parse HEAD`).
2. **Leitura do manifesto:** se existir `bootstrap-manifest.json` na raiz do snapshot, seguir rigorosamente as listas `directories`, `gitkeep`, `copy_files`, `copy_dirs` e `instantiate_from_templates`. Caso contrário, aplicar a allowlist padrão:
   - `docs/GUIDELINE.md` → `docs/GUIDELINE.md` (100% agnóstico, sem alterar)
   - `docs/templates/*.md` → `docs/templates/` (somente `*.md`; nunca copiar `.env`)
   - `docs/skills/*` → `.agents/skills/` (cópia recursiva)
   - Instanciar `docs/DATABASE-PATTERN.md`, `docs/NAMING-CONVENTION.md`, `docs/DESIGN.md` e `docs/TO-DO.md` a partir dos respectivos `*-TEMPLATE.md` (ou placeholder mínimo se o template não existir).
3. **Estrutura alvo resultante:**

```text
{local_path}/{project_slug_name}/
│
├── docs/
│   ├── GUIDELINE.md                 ← AGNÓSTICO (metodologia SDD — reutilizar 100%)
│   ├── DATABASE-PATTERN.md          ← CUSTOMIZADO (padrões de banco)
│   ├── NAMING-CONVENTION.md         ← CUSTOMIZADO (convenções de código)
│   ├── DESIGN.md                    ← CUSTOMIZADO (identidade visual)
│   ├── TO-DO.md                     ← CUSTOMIZADO (status das entregas)
│   ├── templates/                   ← TEMPLATES MESTRES (*.md)
│   └── sdd/                         ← SPECS POR FUNCIONALIDADE
├── .agents/
│   └── skills/                      ← SKILLS PUBLICADAS (copiadas da versão do bootstrap)
├── src/                             ← código da aplicação
├── db/                              ← schema, migrations, seeds
├── .gitignore
├── README.ini                       ← apenas local (ignorado pelo Git)
└── README.md
```

4. **Nunca copiar do repositório central:** `.git/`, `.env`, `docs/templates/.env`, `docs/PRD.md`, `docs/BACKLOG.md`, `docs/sdd/`, `docs/slides/`.
5. **Limpeza:** apagar o diretório temporário do snapshot imediatamente após a cópia.
6. **Pastas vazias versionáveis:** criar `docs/sdd/.gitkeep`, `src/.gitkeep` e `db/.gitkeep`.
7. **Git local:** inicializar o `.git` dentro de `{local_path}/{project_slug_name}` (nunca em `local_path`) e configurar, apenas neste repositório:
   - `user.name` = valor de `GIT_USER_NAME`
   - `user.email` = valor de `GIT_USER_EMAIL`
   - Não alterar o `git config --global`.

### 6.2 Repositório Git

Com o `GIT_TOKEN` lido do `.env`, criar o repositório privado de nome `{project_slug_name}`, vazio, sem arquivo gerado pelo serviço. A URL pública resultante é `https://github.com/<dono>/{project_slug_name}`, em que `<dono>` é a conta que o token identifica. Visibilidade diferente de privada só se a pessoa pedir.

### 6.3 `.gitignore`, `README.md`, `README.ini` e commit inicial

Criar `.gitignore` na raiz da pasta do projeto contendo, no mínimo:

```gitignore
README.ini
readme.ini
.env
**/.env
.env.*
**/.env.*
```

Criar `README.md` na raiz da pasta do projeto com o título `{project_name}` e o identificador `{project_slug_name}`.

Criar `README.ini` apenas localmente na raiz da pasta do projeto, com este conteúdo e nada mais:

```ini
[project]
name = {project_name}
slug = {project_slug_name}
local_path = {local_path}/{project_slug_name}
github_url = https://github.com/<dono>/{project_slug_name}

[bootstrap]
source_repo = https://github.com/silverioleitejr/app-og1-bootstrap
version = {bootstrap_ref}
commit_sha = {commit_sha}
```

Não incluir token, e-mail de serviço nem connection string. Não enviar `README.ini` nem `.env` para o repositório remoto.

Fazer o commit inicial na branch `main` (mensagem `chore: inicializa estrutura sdd do projeto`) contendo `.gitignore`, `README.md`, `docs/`, `.agents/skills/`, `src/` e `db/` (conferindo antes com `git status` que `README.ini` e nenhum `.env` estão staged). Configurar remote `origin` com a URL limpa e fazer push usando o `GIT_TOKEN` só na autenticação da chamada.

### 6.4 Supabase

Criar o projeto Supabase com o nome `{project_slug_name}`. Não criar tabela. Não gravar chave do Supabase em arquivo do repositório. Credencial do Supabase, se a ferramenta exigir, também sai do `.env` e não do chat. Se a credencial de Supabase não estiver no `.env`, parar neste passo e dizer o nome da variável ausente, sem pedir o valor.

## 7. Encerramento

Informar, sem nenhum segredo:

- caminho `{local_path}/{project_slug_name}`
- versão do bootstrap aplicada (`source_repo`, `bootstrap_ref` e `commit_sha`)
- resumo da estrutura inicial criada (templates e skills copiados)
- URL limpa do GitHub
- hash do commit inicial
- nome do projeto Supabase
- o que não foi feito, se algum passo parou

---

*Skill mantida em `docs/skills/sdd-project-init/SKILL.md`.*
