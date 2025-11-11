---
layout: page
permalink: /conferences/
title: conferences
nav: true
nav_order: 3
---

<style>

.conf-location {
  display: inline-block;
  background: #7b27d8;
  color: white;
  padding: 4px 12px;
  border-radius: 15px;
  font-size: 0.85rem;
  font-weight: 500;
  margin-left: 10px;
}
  
.year-title {
  font-size: 2rem;
  font-weight: 300;
  color: #ccc;
  text-align: right;
  margin-bottom: 2rem;
}

.conf-group {
  display: flex;
  margin-bottom: 1rem;
  padding: 0.5rem;
  background: #f8f9fa;
  border-left: 4px solid #e0e0e0;
  border-radius: 8px;
  gap: 1.5rem;
  align-items: flex-start;
}

.conf-group-content {
  flex: 1;
}

.conf-group-title {
  font-size: 1.2rem;
  font-weight: 600;
  color: #333;
}

@media (max-width: 768px) {
  .conf-group {
    flex-direction: column;
  }
  
}`
</style>

<!-- 2025년 -->
<div class="year-group">
  <h2 class="year-title">2025</h2>
  
  <!-- ICCEPM 2025 -->
  <div class="conf-group">
    <div class="conf-group-content">
      <div class="conf-group-title">International Conference on Construction Engineering and Project Management (ICCEPM)</div>
        {%- assign conf_loc  = entry.location | default: entry.address -%}
      <div class="publications">
        {% bibliography --file conferences --template bib_conference --query @*[conference ~= ICCEPM 2025] %}
      </div>
    </div>
  </div>

  <!-- ISARC 2025 -->
  <div class="conf-group">
    <div class="conf-group-content">
      <div class="conf-group-title">International Symposium on Automation and Robotics in Construction (ISARC)</div>
        {%- assign conf_loc  = entry.location | default: entry.address -%}
      <div class="publications">
        {% bibliography --file conferences --template bib_conference --query @*[conference ~= ISARC 2025] %}
      </div>
    </div>
  </div>
</div>

<!-- 2024년 -->
<div class="year-group">
  <h2 class="year-title">2024</h2>

  <!-- ICCEPM 2024 -->
  <div class="conf-group">
    <div class="conf-group-content">
      <div class="conf-group-title">International Conference on Construction Engineering and Project Management (ICCEPM)</div>
        {%- assign conf_loc  = entry.location | default: entry.address -%}
      <div class="publications">
        {% bibliography --file conferences --template bib_conference --query @*[conference ~= ICCEPM 2024] %}
      </div>
    </div>
  </div>
</div>
