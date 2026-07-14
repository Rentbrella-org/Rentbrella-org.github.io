---
layout: default
title: Política de ciclo de vida
description: Status, impacto e regras de ciclo de vida das versões de firmware.
permalink: /releases/policy/
---

# Política de ciclo de vida

Este portal traduz as releases técnicas em **contexto operacional**: o estado de cada versão, o impacto descrito da atualização e a compatibilidade entre placa principal (Main) e tela (IHM). A decisão de atualizar ou não fica com a operação.

## Fluxo de vida de uma versão

```mermaid
flowchart LR
    lancamento[Lançamento] --> recomendada
    recomendada --> estavel[Estável]
    estavel --> descontinuada
    recomendada --> problemaCritico[Problema crítico]
    estavel --> problemaCritico
    problemaCritico --> danificada
```

## Status operacionais

Cada status descreve o **estado atual** da versão. A decisão de instalar, manter ou trocar fica com a operação, com base nesse contexto.

<table class="definitions-table">
  <thead>
    <tr><th>Status</th><th>Estado da versão</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>{% include status-badge.html status='recomendada' %}</td>
      <td>Versão de referência no momento: validada para produção, alinhada ao parque atual e indicada pela engenharia para novas instalações e atualizações de rotina.</td>
    </tr>
    <tr>
      <td>{% include status-badge.html status='estavel' %}</td>
      <td>Versão sem bug conhecido específico dela e ainda aceitável em produção, mas já não é a referência geral — existe uma Recomendada mais recente, ou ela só faz sentido para um modelo, tipo de máquina ou cliente específico.</td>
    </tr>
    <tr>
      <td>{% include status-badge.html status='danificada' %}</td>
      <td>Versão com problema crítico identificado. Máquinas nessa versão estão expostas a falha relevante e a engenharia sinaliza risco operacional.</td>
    </tr>
    <tr>
      <td>{% include status-badge.html status='descontinuada' %}</td>
      <td>Versão fora do ciclo operacional: não recebe mais suporte ativo e não faz parte do conjunto indicado para o parque atual.</td>
    </tr>
  </tbody>
</table>

### Resumo rápido

1. **Recomendada** — referência atual da engenharia (validada, alinhada ao parque, indicada para novas instalações e atualizações).
2. **Estável** — sem problema conhecido específico dela; já há uma referência mais nova, ou só é útil para um modelo, tipo de máquina ou cliente específico.
3. **Danificada** — problema crítico conhecido; risco operacional nessa versão.
4. **Descontinuada** — fora de suporte e fora do conjunto indicado para o parque.

## Status do roadmap (aba Futuro)

Nomes de versões ainda não lançadas ficam em [Futuro]({{ '/releases/futuro/' | relative_url }}). Quando a versão é lançada, ela **sai do roadmap** e passa a aparecer nas páginas de versões (Main / IHM) com um status operacional (`recomendada`, `estavel`, etc.).

```mermaid
flowchart LR
    planejada[Planejada] --> conceito[Conceito]
    conceito --> desenvolvimento[Em desenvolvimento]
    desenvolvimento --> teste[Em teste]
    teste --> lancamento[Lançamento]
    lancamento --> versoes[Pagina de versoes]
```

<table class="definitions-table">
  <thead>
    <tr><th>Status</th><th>O que significa para a operação</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>{% include status-badge.html status='planejada' %}</td>
      <td>Nome reservado no roadmap. Ainda não há escopo nem data firme — não espere essa versão em campo.</td>
    </tr>
    <tr>
      <td>{% include status-badge.html status='conceito' %}</td>
      <td>Engenharia está definindo o que entra na versão (ideias e escopo). Nada para instalar; mudanças de plano são esperadas.</td>
    </tr>
    <tr>
      <td>{% include status-badge.html status='desenvolvimento' %}</td>
      <td>Features sendo implementadas. Pode haver builds internos, mas não é versão de teste em campo nem de produção.</td>
    </tr>
    <tr>
      <td>{% include status-badge.html status='teste' %}</td>
      <td>Conjunto sob validação (lab ou campo). Consulte a seção “Testes em andamento” no Futuro. Só a engenharia libera o uso; ao encerrar o teste, a operação pode ser orientada a retirar essas builds da rua.</td>
    </tr>
  </tbody>
</table>

### Resumo rápido (roadmap)

1. **Planejada** — nome reservado; sem trabalho ativo.
2. **Conceito** — escopo em definição.
3. **Em desenvolvimento** — implementação em andamento.
4. **Em teste** — validação; acompanhe datas e conjuntos na aba Futuro.
5. **Ao lançar** — some do Futuro e entra na lista oficial de versões.

## Níveis de impacto da atualização

<table class="definitions-table">
  <thead>
    <tr><th>Impacto</th><th>Significado</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>{% include impact-badge.html impact='none' %}</td>
      <td>Atualização não traz benefício relevante para a maioria do parque.</td>
    </tr>
    <tr>
      <td>{% include impact-badge.html impact='recommended' %}</td>
      <td>Atualização desejável para novas instalações e máquinas em expansão.</td>
    </tr>
    <tr>
      <td>{% include impact-badge.html impact='group_specific' %}</td>
      <td>Benefício limitado a um grupo de máquinas (hardware, região ou fluxo).</td>
    </tr>
    <tr>
      <td>{% include impact-badge.html impact='mandatory' %}</td>
      <td>Atualização necessária por mudança incompatível com a versão anterior ou por requisito de segurança.</td>
    </tr>
  </tbody>
</table>

## Regras de negócio

- **Status descreve estado, não ordem** — o portal informa o contexto da versão; a operação decide com base nisso e no cenário da máquina.
- **O portal informa, não decide** — o banner e o status descrevem o estado da versão; a operação decide no cenário de cada máquina.
- **Compatibilidade cruzada Main ↔ IHM** — consulte a [tabela de compatibilidade]({{ '/releases/compatibility/' | relative_url }}) antes de combinar versões da placa e da tela.
- **Roadmap ≠ produção** — nomes em [Futuro]({{ '/releases/futuro/' | relative_url }}) não são versões instaláveis; só entram no parque após o lançamento nas páginas de versões.
- **Conteúdo preliminar** — alguns campos podem estar provisórios até validação pela equipe; em caso de dúvida, confirme com a engenharia.
