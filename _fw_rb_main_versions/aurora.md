---
product: fw_rb_main
product_name: "fw-rb-main — Placa principal"
version: "aurora"
summary: "Versão de referência atual para produção. Consolida correções de sensores e estabilidade."
ihm_compat_min: "v3.2.1-1"
ihm_compat_max: null
status: recomendada
impact: recommended
released_at: 2026-07-13
replaces: "v2.25.2-1"
recommended_for:
  - "Novas instalações em produção"
  - "Máquinas com leitura instável de sensores"
not_required_for: []
still_supported: true
added:
  - "Fluxo para forçar a placa principal a rever o status dos guarda-chuvas"
fixed:
  - "Filtro do sensor de guarda-chuvas ao iniciar a máquina"
  - "Congelamento da placa principal"
changed:
  - "Leitura da memória flash mais estável, para reduzir desconfiguração"
  - "Leitura dos sensores mais estável, para reduzir leituras erradas"
  - "Novos códigos fixos para entrar no Modo Operador"
---
