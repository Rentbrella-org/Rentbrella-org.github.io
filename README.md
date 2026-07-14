# Portal de Política de Releases

Site estático (Jekyll + GitHub Pages) com consulta informativa de **quais versões de firmware existem** e **suas funcionalidades** — para `fw-rb-main` (placa principal) e IHM (tela de interface).

Site em produção: [https://rentbrella-org.github.io](https://rentbrella-org.github.io)

---

## Como funciona

O conteúdo é Markdown com front matter YAML. O Jekyll gera páginas a partir de:

| Pasta / arquivo | Função |
|---|---|
| `index.md` | Home do portal |
| `fw_rb_main/index.md` | Lista de versões da placa principal |
| `ihm/index.md` | Lista de versões da IHM |
| `_fw_rb_main_versions/*.md` | Uma página por versão do Main |
| `_ihm_versions/*.md` | Uma página por versão da IHM |
| `_data/cross-compat.yml` | Regras de compatibilidade Main ↔ IHM |
| `_data/roadmap.yml` | Roadmap de versões nomeadas e conjuntos em teste |
| `releases/policy.md` | Política de ciclo de vida (status, impacto) |
| `releases/compatibility.md` | Tabela de compatibilidade |
| `releases/futuro.md` | Página Futuro (roadmap + testes) |
| `_layouts/` | Templates (`default`, `dashboard`, `version`) |
| `_includes/` | Badges, tabelas e lookups reutilizáveis |
| `_config.yml` | Collections, permalinks e defaults |

Cada arquivo em `_fw_rb_main_versions/` ou `_ihm_versions/` vira uma página em:

- `/fw-rb-main/versions/<nome-do-arquivo>/`
- `/ihm/versions/<nome-do-arquivo>/`

O nome do arquivo (ex.: `v2.25.2.md` ou `Aurora.md`) define o slug da URL; o campo `version` no front matter é o que aparece na UI.

---

## Pré-requisitos

- Ruby 3.x
- Bundler

```bash
ruby -v
gem install bundler
```

---

## Setup local

```bash
git clone https://github.com/Rentbrella-org/Rentbrella-org.github.io.git
cd Rentbrella-org.github.io
bundle config set --local path 'vendor/bundle'
bundle install
```

---

## Rodar localmente (preview)

```bash
bundle exec jekyll serve
```

Abra [http://127.0.0.1:4000](http://127.0.0.1:4000). O servidor recarrega ao salvar arquivos.

Opções úteis:

```bash
# Rebuild completo (útil após mudar _config.yml)
bundle exec jekyll serve --livereload

# Escutar em todas as interfaces (acesso na rede local)
bundle exec jekyll serve --host 0.0.0.0
```

---

## Build

Gera o site estático em `_site/`:

```bash
bundle exec jekyll build
```

Para validar sem servir:

```bash
bundle exec jekyll build --strict_front_matter
```

`_site/` é gerado localmente e está no `.gitignore` — não versionar.

---

## Como atualizar o portal

### 1. Adicionar uma nova versão

1. Crie um arquivo Markdown na collection correta:
   - Main: `_fw_rb_main_versions/vX.Y.Z.md`
   - IHM: `_ihm_versions/vX.Y.Z.md`
2. Preencha o front matter (schema abaixo).
3. Atualize o status da versão anterior (ex.: `recomendada` → `estavel`).
4. Se a combinação Main+IHM mudou, edite `_data/cross-compat.yml`.
5. Abra um PR usando o checklist em `.github/PULL_REQUEST_TEMPLATE/new-release.md`.
6. Confirme o build local: `bundle exec jekyll build`.

### 2. Schema do front matter (versão)

Cada `status` tem um template próprio. Use como referência os arquivos em `_fw_rb_main_versions/` (e o equivalente em `_ihm_versions/`). Não use texto livre abaixo do front matter — só YAML.

Campos comuns a todos:

| Campo | Uso |
|---|---|
| `product` / `product_name` | Identificação do produto |
| `version` | Texto exibido na UI (o slug vem do nome do arquivo) |
| `summary` | Contexto operacional em uma frase (banner) |
| `ihm_compat_min` / `ihm_compat_max` | Só em Main (`null` se não aplicável) |
| `main_compat_min` / `main_compat_max` | Só em IHM (`null` se não aplicável) |
| `status` | `recomendada` \| `estavel` \| `danificada` \| `descontinuada` |
| `released_at` | Data de release |
| `still_supported` | `true` / `false` |
| `added` / `fixed` / `changed` | Changelog (listas; omita as vazias se preferir) |

#### Template — `recomendada`

Referência atual para produção. Inclui impacto, para quem atualizar e o que substitui.

```yaml
---
product: fw_rb_main
product_name: "fw-rb-main — Placa principal"
version: "aurora"
summary: "Versão de referência atual para produção. Consolida correções de sensores e estabilidade."
ihm_compat_min: null
ihm_compat_max: null
status: recomendada
impact: recommended          # none | recommended | group_specific | mandatory
released_at: 2026-07-13
replaces: "v2.25.2-1"
recommended_for:
  - "Novas instalações em produção"
  - "Máquinas com leitura instável de sensores"
not_required_for: []
still_supported: true
added:
  - "..."
fixed:
  - "..."
changed:
  - "..."
---
```

#### Template — `estavel`

Ainda aceitável em produção, mas não é a referência geral. Preencha `recommended_for` / `not_required_for` e o `impact` (muitas vezes `group_specific` ou `none`).

```yaml
---
product: fw_rb_main
product_name: "fw-rb-main — Placa principal"
version: "v2.25.2-1"
summary: "Suporte à IHM DWIN de 7 polegadas e correção de segurança do Modo Evento."
ihm_compat_min: null
ihm_compat_max: null
status: estavel
impact: group_specific       # none | recommended | group_specific | mandatory
released_at: 2025-07-08
replaces: "v2.23.1-1"
recommended_for:
  - "Máquinas com tela Proculus de 7 polegadas"
not_required_for: []
still_supported: true
added:
  - "..."
fixed:
  - "..."
changed:
  - "..."
---
```

#### Template — `danificada`

Problema crítico conhecido. Foque em `known_issues`; `still_supported` deve ser `false`. Não precisa de `impact` / `recommended_for`.

```yaml
---
product: fw_rb_main
product_name: "fw-rb-main — Placa principal"
version: "v2.16.0-1"
summary: "Primeira versão para RB-05 com placa LED — não use em produção: LEDs falham e a máquina pode reiniciar em loop."
ihm_compat_min: null
ihm_compat_max: null
status: danificada
released_at: 2024-02-09
still_supported: false
added:
  - "..."
known_issues:
  - "Em RB-05, os LEDs não acionavam corretamente"
  - "Em RB-05, a máquina podia entrar em loop infinito de reinícios ao ligar"
---
```

#### Template — `descontinuada`

Fora do ciclo operacional. Inclua `discontinued_at` e `still_supported: false` (exceto casos excepcionais ainda no parque).

```yaml
---
product: fw_rb_main
product_name: "fw-rb-main — Placa principal"
version: "v2.18.0-1"
summary: "Modo Evento e consolidação dos fluxos de crachá e acessibilidade."
ihm_compat_min: null
ihm_compat_max: null
status: descontinuada
released_at: 2024-08-28
discontinued_at: 2024-11-14
replaces: "v2.17.1-1"        # opcional
still_supported: false
added:
  - "..."
fixed:
  - "..."
changed:
  - "..."
---
```

### 3. Compatibilidade cruzada

Edite `_data/cross-compat.yml`:

- `rules` — faixas IHM ↔ Main (`ok`, `warning`, `incompatible`)
- `recommended_pairs` — par recomendado atual para novas máquinas

### 4. Roadmap e versões em teste (aba Futuro)

A página `/releases/futuro/` é alimentada por `_data/roadmap.yml` (mesmo padrão da compatibilidade: edite o YAML, sem páginas individuais).

Três seções:

1. **Versões seguintes** — nomes reservados; passe o mouse (ou toque no celular) para ver `summary` e `planned_features`
2. **Testes em andamento** — conjuntos Main + IHM sob validação
3. **Testes finalizados** — testes encerrados (operação pode retirar da rua)

#### Status das versões no roadmap

| Valor | Label na UI | Significado |
|---|---|---|
| `planejada` | Planejada | Nome reservado; ainda sem trabalho ativo |
| `conceito` | Conceito | Escopo e ideias em definição |
| `desenvolvimento` | Em desenvolvimento | Features sendo implementadas |
| `teste` | Em teste | Validação em lab ou campo |

Quando a versão é lançada, **remova-a** de `_data/roadmap.yml` e crie a página em `_fw_rb_main_versions/` (ou `_ihm_versions/`) com status operacional (`recomendada`, `estavel`, etc.).

#### Schema — `versions`

| Campo | Uso |
|---|---|
| `name` | Nome da versão (ex.: `"Brisa"`) |
| `status` | `planejada` \| `conceito` \| `desenvolvimento` \| `teste` |
| `expected_release` | Previsão de lançamento (`YYYY-MM-DD` ou `null`) |
| `date_updated_at` | Quando a previsão foi revisada pela última vez (`YYYY-MM-DD` ou `null`). Na UI, datas com ≤ 14 dias aparecem como “recente” |
| `summary` | Resumo curto (aparece no preview ao hover) |
| `planned_features` | Lista do que está previsto na versão (também no preview) |

Ao mudar a data de lançamento, atualize **sempre** `expected_release` **e** `date_updated_at` juntos.

```yaml
versions:
  - name: "Brisa"
    status: planejada
    expected_release: 2026-09-01
    date_updated_at: 2026-07-14
    summary: "Próxima versão nomeada após Aurora."
    planned_features:
      - "Funcionalidade dos slots"
```

#### Schema — `active_tests` / `finished_tests`

| Campo | Uso |
|---|---|
| `name` | Nome do teste / funcionalidade |
| `main` | Lista de versões Main sob teste (ex.: `["v2.27.5-1", "v2.27.7-1"]`) |
| `ihm` | Lista de versões IHM sob teste |
| `started_at` | Início dos testes |
| `expected_end` | Só em `active_tests` — previsão de fim |
| `finished_at` | Só em `finished_tests` — data de encerramento |
| `target_version` | Opcional — em qual versão nomeada isso deve sair |
| `notes` | Observações para operação / engenharia |

Ao concluir um teste: mova o item de `active_tests` para `finished_tests` e preencha `finished_at`.

```yaml
active_tests:
  - name: "funcionalidade dos slots"
    main:
      - "v2.27.7-1"
    ihm:
      - "v3.2.1-1"
    started_at: 2026-07-01
    expected_end: 2026-07-31
    notes: ""
    target_version: "brisa"

finished_tests:
  - name: "exemplo concluído"
    main:
      - "v2.26.0-1"
      - "v2.26.1-1"
    ihm:
      - "v3.2.1-1"
    started_at: 2026-05-01
    finished_at: 2026-06-15
    notes: "Operação pode remover da rua."
```

### 5. Páginas estáticas

- Política: `releases/policy.md`
- Compatibilidade: `releases/compatibility.md`
- Futuro: `releases/futuro.md`
- Textos dos dashboards: `fw_rb_main/index.md`, `ihm/index.md`

---

## Deploy

O site é publicado via **GitHub Pages** a partir do branch padrão (`main`). Após o merge do PR, o Pages rebuilda automaticamente.

URL: `https://rentbrella-org.github.io`

---

## Estrutura rápida

```
├── _config.yml                 # Collections e defaults
├── _data/
│   ├── cross-compat.yml        # Compat Main ↔ IHM
│   └── roadmap.yml             # Roadmap + testes (aba Futuro)
├── _fw_rb_main_versions/       # Versões do Main
├── _ihm_versions/              # Versões da IHM
├── _includes/                  # Partials (badges, tabelas, roadmap)
├── _layouts/                   # Templates
├── assets/css/style.css
├── fw_rb_main/index.md
├── ihm/index.md
├── releases/
│   ├── policy.md
│   ├── compatibility.md
│   └── futuro.md
├── index.md
├── Gemfile
└── .github/PULL_REQUEST_TEMPLATE/new-release.md
```

---

## Links úteis

- [Política de ciclo de vida](https://rentbrella-org.github.io/releases/policy/)
- [Tabela de compatibilidade](https://rentbrella-org.github.io/releases/compatibility/)
- [Futuro / versões em teste](https://rentbrella-org.github.io/releases/futuro/)
- CHANGELOG [fw-rb-main](https://github.com/Rentbrella-org/fw-rb-main/blob/main/CHANGELOG.md)
- CHANGELOG [fw-rb-ihm-dwin](https://github.com/Rentbrella-org/fw-rb-ihm-dwin/blob/main/CHANGELOG.md)
