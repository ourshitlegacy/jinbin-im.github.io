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

.year-title {
  font-size: 2rem;
  font-weight: 300;
  color: #ccc;
  text-align: right;
  margin-bottom: 2rem;
}

.conf-group {
  display: flex;
  margin-bottom: 2rem;
  padding: 1.5rem;
  background: #f8f9fa;
  border-left: 4px solid #7b27d8;
  border-radius: 8px;
  gap: 1.5rem;
  align-items: flex-start;
}

.conf-group-logo {
  flex-shrink: 0;
  width: 120px;
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
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
  
  .conf-group-logo {
    width: 100%;
    height: 100px;
  }
}
</style>

<!-- 2025년 -->
<div class="year-group">
  <h2 class="year-title">2025</h2>
  
  <!-- ICCEPM 2025 -->
  <div class="conf-group">
    <div class="conf-group-logo" style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);">
      <span style="color: white; font-size: 1.1rem; font-weight: 700; text-align: center; padding: 10px; line-height: 1.3;">ICCEPM<br>2025</span>
    </div>
    <div class="conf-group-content">
      <div class="conf-group-title">International Conference on Construction Engineering and Project Management 2025</div>
      <div class="publications">
        {% bibliography --file conferences --template bib_conference --query @*[year=2025 && booktitle ~= ICCEPM] %}
      </div>
    </div>
  </div>

  <!-- ISARC 2025 -->
  <div class="conf-group">
    <div class="conf-group-logo" style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);">
      <span style="color: white; font-size: 1.1rem; font-weight: 700; text-align: center; padding: 10px; line-height: 1.3;">ISARC<br>2025</span>
    </div>
    <div class="conf-group-content">
      <div class="conf-group-title">International Symposium on Automation and Robotics in Construction 2025</div>
      <div class="publications">
        {% bibliography --file conferences --template bib_conference --query @*[year=2025 && booktitle ~= ISARC] %}
      </div>
    </div>
  </div>
</div>

<!-- 2024년 -->
<div class="year-group">
  <h2 class="year-title">2024</h2>
  
  <!-- ICCEPM 2024 -->
  <div class="conf-group">
    <div class="conf-group-logo" style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);">
      <span style="color: white; font-size: 1.1rem; font-weight: 700; text-align: center; padding: 10px; line-height: 1.3;">ISARC<br>2024</span>
    </div>
    <div class="conf-group-content">
      <div class="conf-group-title">International Conference on Construction Engineering and Project Management 2024</div>
      <div class="publications">
        {% bibliography --file conferences --template bib_conference --query @*[year=2024 && booktitle ~= ISARC] %}
      </div>
    </div>
  </div>
</div>
