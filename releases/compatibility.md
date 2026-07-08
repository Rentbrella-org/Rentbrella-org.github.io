---
layout: default
title: Compatibilidade
description: Flags operacionais por versão e matriz cruzada Main ↔ IHM.
permalink: /releases/compatibility/
---

# Tabela de compatibilidade

Use esta página para responder **"pode ir para produção?"** e **"Main X combina com IHM Y?"**

## RBX-01 — Main Board

<div class="table-wrapper">
  <table class="dashboard-table">
    <thead>
      <tr>
        <th>Versão</th>
        <th>Deploy oficial</th>
        <th>Suportada</th>
        <th>Pode instalar</th>
        <th>Somente teste</th>
      </tr>
    </thead>
    <tbody>
      {% assign rbx = site.rbx01_versions | sort: 'released_at' | reverse %}
      {% for v in rbx %}
      <tr>
        <td><a href="{{ v.url | relative_url }}">v{{ v.version }}</a></td>
        <td>{% if v.official_deploy %}✅{% else %}❌{% endif %}</td>
        <td>{% if v.still_supported %}✅{% else %}❌{% endif %}</td>
        <td>{% if v.can_install %}✅{% else %}❌{% endif %}</td>
        <td>{% if v.test_only %}⚠️ Sim{% else %}Não{% endif %}</td>
      </tr>
      {% endfor %}
    </tbody>
  </table>
</div>

## IHM — Display DWIN

<div class="table-wrapper">
  <table class="dashboard-table">
    <thead>
      <tr>
        <th>Versão</th>
        <th>Deploy oficial</th>
        <th>Suportada</th>
        <th>Pode instalar</th>
        <th>Somente teste</th>
      </tr>
    </thead>
    <tbody>
      {% assign ihm = site.ihm_versions | sort: 'released_at' | reverse %}
      {% for v in ihm %}
      <tr>
        <td><a href="{{ v.url | relative_url }}">v{{ v.version }}</a></td>
        <td>{% if v.official_deploy %}✅{% else %}❌{% endif %}</td>
        <td>{% if v.still_supported %}✅{% else %}❌{% endif %}</td>
        <td>{% if v.can_install %}✅{% else %}❌{% endif %}</td>
        <td>{% if v.test_only %}⚠️ Sim{% else %}Não{% endif %}</td>
      </tr>
      {% endfor %}
    </tbody>
  </table>
</div>

## Compatibilidade cruzada Main ↔ IHM

Edite as regras em [`_data/cross-compat.yml`](https://github.com/Rentbrella-org/Rentbrella-org.github.io/blob/main/_data/cross-compat.yml) no GitHub.

{% include cross-compat-table.html %}

<p class="muted">Regras marcadas como placeholder refletem conhecimento preliminar — confirme com engenharia antes de deploy em massa.</p>
