# app-og1-bootstrap

## Descrição breve

Projeto **app-og1-bootstrap** – um **bootstrap** para iniciar projetos seguindo a metodologia **Spec‑Driven Development (SDD)**.  Utiliza **Antigravity**, **GitHub**, **Supabase** e o ecossistema **Node.js**/**Python** para provisionar rapidamente a estrutura de diretórios, templates e skills necessários.

## Requisitos

- **Node.js** (>= 18) 
- **npm** ou **pnpm** 
- **Python 3.10+** (para scripts auxiliares) 
- **Supabase CLI** (`supabase`) e conta com token configurado no `.env`
- **Git** (para versionamento) 
- **Antigravity CLI** (`agy`) 

## Instalação / Setup

```bash
# Clone o repositório
git clone https://github.com/silverioleitejr/app-og1-bootstrap.git
cd app-og1-bootstrap

# Instale dependências (se houver)
pm install   # ou pnpm install

# Copie o .env de exemplo e preencha as variáveis
cp docs/templates/.env .env
# edite .env com GIT_TOKEN, SUPABASE_TOKEN, etc.
```

## Uso

Com a skill `sdd-project-init` você pode iniciar um novo projeto SDD:

```bash
agy run sdd-project-init --project_name "Innovation Cards" \
    --project_slug_name "app-innovation-cards" \
    --local_path "c:\\@projetos"
```

Outras skills úteis:
- `sdd-structure-validator` – valida a estrutura do projeto.
- `sdd-developer` – implementa pacotes aprovados.

## Estrutura do repositório

```
app-og1-bootstrap/
│   .gitignore
│   README.md
│   .env               # NÃO versionado
│
├── docs/              # Artefatos de spec e templates
│   ├── GUIDELINE.md
│   ├── AGENTS.md
│   ├── PRD.md
│   ├── SAD.md
│   ├── ...
│   └── templates/      # Templates mestre (MD)
│
├── .agents/           # Skills publicadas (copiadas de docs/skills)
│   └── skills/
│       ├── sdd-project-init/
│       │   └── SKILL.md
│       └── ...
│
├── src/               # Código da aplicação (a ser adicionado)
├── db/                # Migrations, seeds, schemas
└── .git/              # Repositório Git
```

## Contribuição

1. Fork o repositório.
2. Crie uma branch para sua feature (`git checkout -b feat/minha-feature`).
3. Siga o padrão de commit **Conventional Commits**.
4. Execute `npm run lint` e `npm test` antes de abrir o PR.
5. Abra um Pull Request descrevendo as mudanças.

## Licença

Este projeto está licenciado sob a **MIT License** – veja o arquivo `LICENSE` para mais detalhes.
