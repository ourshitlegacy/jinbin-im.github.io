---
layout: page
permalink: /conferences/
title: conferences
description: conferences by categories in reversed chronological order.
nav: true
nav_order: 3
---

<style>
.year-group {
  margin-bottom: 3rem;
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
  color: #7b27d8;
  margin-bottom: 1.5rem;
}

@media (max-width: 768px) {
  .conf-group {
    flex-direction: column;
  }
  
}
</style>

<!-- 2025년 -->
<div class="year-group">
  
  <!-- ICCEPM 2025 -->
  <div class="conf-group">
    <div class="conf-group-content">
      <div class="conf-group-title">International Conference on Construction Engineering and Project Management (ICCEPM)</div>
      <div class="publications">
        {% bibliography --file conferences --template bib_conference --query @*[year=2025 && booktitle ~= ICCEPM] %}
      </div>
    </div>
  </div>

  <!-- ISARC 2025 -->
  <div class="conf-group">
    <div class="conf-group-content">
      <div class="conf-group-title">International Symposium on Automation and Robotics in Construction (ISARC)</div>
      <div class="publications">
        {% bibliography --file conferences --template bib_conference --query @*[year=2025 && booktitle ~= ISARC] %}
      </div>
    </div>
  </div>
</div>

<!-- 2024년 -->
<div class="year-group">
  
  <!-- ICCEPM 2024 -->
  <div class="conf-group">
    <div class="conf-group-content">
      <div class="conf-group-title">International Conference on Construction Engineering and Project Management (ICCEPM)</div>
      <div class="publications">
        {% bibliography --file conferences --template bib_conference --query @*[year=2024 && booktitle ~= ICCEPM] %}
      </div>
    </div>
  </div>
</div>
