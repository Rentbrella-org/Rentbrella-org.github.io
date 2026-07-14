---
layout: default
title: Portal de Política de Releases
description: Consulta informativa das versões de firmware e suas funcionalidades.
---

<section class="hero">
  <div class="hero-logo">
    <img src="{{ '/assets/img/logo-purple.png' | relative_url }}" alt="Rentbrella" height="48">
  </div>
  <h1>Portal de Política de Releases</h1>
  <p class="lead">
    Portal informativo com <strong>quais versões de firmware existem</strong> e
    <strong>suas funcionalidades</strong> — para as máquinas de compartilhamento de guarda-chuva.
  </p>
</section>

<div class="product-cards">
  <a href="{{ '/fw-rb-main/' | relative_url }}" class="product-card">
    <h2>fw-rb-main — Placa principal</h2>
    <p>Firmware da placa principal (Main). Controla sensores, motores, LEDs e a comunicação com a tela (IHM).</p>
    {% include recommended-version.html product='fw_rb_main' %}
  </a>
  <a href="{{ '/ihm/' | relative_url }}" class="product-card">
    <h2>IHM — Tela de interface</h2>
    <p>Firmware da tela (IHM). Modelos de 7 polegadas (800×480, atual) e 10 polegadas (1024×768, legado).</p>
    {% include recommended-version.html product='ihm' %}
  </a>
</div>

<div class="quick-links">
  <a href="{{ '/releases/policy/' | relative_url }}">
    <span class="quick-link__icon" aria-hidden="true">
      <svg viewBox="0 0 24 24" role="img"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8l-6-6zm-1 2 5 5h-5V4zM8 13h8v2H8v-2zm0 4h5v2H8v-2z"/></svg>
    </span>
    <span class="quick-link__label">Política de ciclo de vida</span>
    <span class="quick-link__arrow" aria-hidden="true">→</span>
  </a>
  <a href="{{ '/releases/compatibility/' | relative_url }}">
    <span class="quick-link__icon" aria-hidden="true">
      <svg viewBox="0 0 24 24" role="img"><path d="M4 5h16a1 1 0 0 1 1 1v3H3V6a1 1 0 0 1 1-1zm-1 6h18v8a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1v-8zm4 2v2h3v-2H7zm0 4v2h8v-2H7z"/></svg>
    </span>
    <span class="quick-link__label">Tabela de compatibilidade</span>
    <span class="quick-link__arrow" aria-hidden="true">→</span>
  </a>
</div>
