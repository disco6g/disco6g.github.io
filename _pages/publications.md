---
layout: page
permalink: /publicaciones/
title: publicaciones
description: Publicaciones ordenadas cronológicamente asociadas a DISCO-6G.
years: [2025]
conference_years: [2025]
nav: true
nav_order: 2
---

<!-- Bibsearch Feature -->
{% include bib_search.liquid %}

<div id="publications-root" class="publications">

  <div class="pub-toolbar" aria-label="Publications controls">
    <button id="pub-expand-all" type="button" class="btn-small" aria-pressed="false">Expand all</button>
    <button id="pub-collapse-all" type="button" class="btn-small">Collapse all</button>
  </div>

  <details class="pub-section" open>
    <summary><span class="h2">Artículos científicos (JCR)</span></summary>

    {% for y in page.years %}
      <details class="pub-year" data-year="{{ y }}"{% if forloop.index <= 2 %} open{% endif %}>
        <summary><span class="year">{{ y }}</span></summary>
        <div class="bibwrap">
          {% bibliography -f disco6g_publications -q @*[year={{y}}]* %}
        </div>
      </details>
    {% endfor %}
  </details>

  <hr>

  <details class="pub-section" open>
    <summary><span class="h2">Congresos</span></summary>

    {% for y in page.conference_years %}
      <details class="pub-year" data-year="{{ y }}"{% if forloop.index <= 2 %} open{% endif %}>
        <summary><span class="year">{{ y }}</span></summary>
        <div class="bibwrap">
          {% bibliography -f disco6g_conferences -q @*[year={{y}}]* %}
        </div>
      </details>
    {% endfor %}
  </details>

  <script>
  document.addEventListener('DOMContentLoaded', function () {
    const root = document.getElementById('publications-root');
    if (!root) return;

    const btnExpand   = root.querySelector('#pub-expand-all');
    const btnCollapse = root.querySelector('#pub-collapse-all');
    if (!btnExpand || !btnCollapse) return;

    const allDetails = () => root.querySelectorAll('details');

    function setAll(open) {
      allDetails().forEach(d => { d.open = !!open; });
      updateState();
    }

    function updateState() {
      const details = allDetails();
      const openCount = Array.from(details).filter(d => d.open).length;
      const allOpen = details.length > 0 && openCount === details.length;

      btnExpand.setAttribute('aria-pressed', allOpen ? 'true' : 'false');
      root.classList.toggle('all-expanded', allOpen);
    }

    btnExpand.addEventListener('click', () => setAll(true));
    btnCollapse.addEventListener('click', () => setAll(false));

    root.addEventListener('toggle', (e) => {
      if (e.target.tagName === 'DETAILS') updateState();
    }, true);

    updateState();
  });
  </script>

</div>
