---
layout: page
permalink: /conferences/
title: conferences
nav: true
nav_order: 3
---

<!-- _pages/conferences.md -->
<!-- Bibsearch Feature -->
{% include bib_search.liquid %}
<div class="publications">
{%- for y in page.years %}
  <h2 class="bibliography-year">{{y}}</h2>
{%- capture bib_year %}{{ y | append: '.bib' }}{% endcapture %}
{%- bibliography_group_by conference --file conference --query @[year={{y}}]* %}
{%- for group in bibliography_groups %}
{%- if group.key != '' %}
<!-- 컨퍼런스 헤더 -->
<div class="conference-header">
<h3>{{ group.key }}</h3>
{%- assign first_entry = group.entries | first %}
{%- if first_entry.address or first_entry.month %}
<div class="conference-meta">
{%- if first_entry.address %}{{ first_entry.address }}{% endif %}
{%- if first_entry.address and first_entry.month %}, {% endif %}
{%- if first_entry.month %}{{ first_entry.month }}{% endif %}
</div>
{%- endif %}
</div>
  <!-- 해당 컨퍼런스의 논문들 -->
  {%- for entry in group.entries %}
    {%- capture entry_html %}{% include bib/conference_bib.liquid %}{% endcapture %}
    {{ entry_html }}
  {%- endfor %}
{%- endif %}
{%- endfor %}
{%- endfor %}
</div>
