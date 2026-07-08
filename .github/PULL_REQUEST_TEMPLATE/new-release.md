## Nova versão no portal de política

Use este checklist ao adicionar ou atualizar uma versão de firmware (RBX-01 ou IHM).

### Arquivo da versão

- [ ] Arquivo criado em `_rbx01_versions/` ou `_ihm_versions/` (ex.: `v2.28.0.md`)
- [ ] Front matter completo conforme schema (product, version, status, impact, flags)
- [ ] Campo **`should_update`** preenchido em linguagem de negócio (texto livre)
- [ ] Campo **`should_update_short`** definido (`Sim`, `Não` ou `Depende`)
- [ ] Listas `recommended_for` e `not_required_for` preenchidas quando aplicável
- [ ] Resumo técnico (`added`, `fixed`, `breaking`, etc.) revisado — não substitui CHANGELOG

### Versão anterior

- [ ] Status da versão anterior atualizado (ex.: `recommended` → `maintenance`)
- [ ] Campo `replaces` aponta para a versão imediatamente anterior, se relevante
- [ ] Dashboard (`rbx-01/index.md` ou `ihm/index.md`) — `recommended_version` atualizado se necessário

### Compatibilidade

- [ ] Flags operacionais corretas (`official_deploy`, `still_supported`, `can_install`, `test_only`)
- [ ] Regra adicionada ou ajustada em `_data/cross-compat.yml` (se combinação Main+IHM mudou)
- [ ] Par recomendado em `recommended_pairs` atualizado, se aplicável

### Revisão

- [ ] Conteúdo revisado por engenharia
- [ ] Landing page (`index.md`) — versão recomendada nos cards, se mudou
- [ ] Build local OK: `bundle exec jekyll build`

### Links úteis

- [Política de ciclo de vida](/releases/policy/)
- [Tabela de compatibilidade](/releases/compatibility/)
- CHANGELOG RBX-01: [fw-rb-main](https://github.com/Rentbrella-org/fw-rb-main/blob/main/CHANGELOG.md)
- CHANGELOG IHM: [fw-rb-ihm-dwin](https://github.com/Rentbrella-org/fw-rb-ihm-dwin/blob/main/CHANGELOG.md)
