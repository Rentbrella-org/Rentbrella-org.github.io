## Nova versão no portal de política

Use este checklist ao adicionar ou atualizar uma versão de firmware (fw-rb-main ou IHM).

### Arquivo da versão

- [ ] Arquivo criado em `_fw_rb_main_versions/` ou `_ihm_versions/` (ex.: `v2.28.0-1.md`)
- [ ] Front matter completo conforme schema (`product`, `version`, `status`, `impact`, flags)
- [ ] Campo **`summary`** preenchido em linguagem clara para a operação (uma frase)
- [ ] Listas `recommended_for` e `not_required_for` preenchidas quando aplicável
- [ ] Resumo técnico (`added`, `fixed`, `changed`, `breaking`, etc.) revisado — não substitui o CHANGELOG
- [ ] Se a versão for `danificada`, o `summary` deve deixar o risco evidente

### Versão anterior

- [ ] Status da versão anterior atualizado (ex.: `recomendada` → `estavel`)
- [ ] Se a versão anterior ficou `descontinuada`, preencher `discontinued_at`
- [ ] Campo `replaces` aponta para a versão imediatamente anterior, se relevante

### Compatibilidade

- [ ] Flag operacional correta (`still_supported`)
- [ ] Regra adicionada ou ajustada em `_data/cross-compat.yml` (se a combinação Main+IHM mudou)
- [ ] Par recomendado em `recommended_pairs` atualizado, se aplicável

### Revisão

- [ ] Conteúdo revisado por engenharia
- [ ] Linguagem clara para operador (gramática e termos consistentes)
- [ ] Build local OK: `bundle exec jekyll build`

### Links úteis

- [Política de ciclo de vida](/releases/policy/)
- [Tabela de compatibilidade](/releases/compatibility/)
- CHANGELOG fw-rb-main: [fw-rb-main](https://github.com/Rentbrella-org/fw-rb-main/blob/main/CHANGELOG.md)
- CHANGELOG IHM: [fw-rb-ihm-dwin](https://github.com/Rentbrella-org/fw-rb-ihm-dwin/blob/main/CHANGELOG.md)
