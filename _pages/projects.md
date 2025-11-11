---
layout: page
title: projects
permalink: /projects/
description: A growing collection of your cool projects.
nav: true
nav_order: 4
display_categories: [Built Environment, Construction Management]
horizontal: true
---
<!-- Tag filters -->
<div class="project-tags" style="margin-bottom: 30px;">
  <button class="btn btn-sm btn-primary tag-btn active" data-tag="all">All</button>
  <button class="btn btn-sm btn-outline-primary tag-btn" data-tag="Extended Reality">Extended Reality</button>
  <button class="btn btn-sm btn-outline-primary tag-btn" data-tag="Human Centered Design">Human Centered Design</button>
  <button class="btn btn-sm btn-outline-primary tag-btn" data-tag="Communication">Communication</button>
  <button class="btn btn-sm btn-outline-primary tag-btn" data-tag="Physiology">Physiology</button>
  <button class="btn btn-sm btn-outline-primary tag-btn" data-tag="ML/AI">ML/AI</button>
  <!-- 나머지 태그들... -->
</div>

<!-- pages/projects.md -->
<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}
  <!-- Display projects without categories -->
  {% assign sorted_projects = site.projects | sort: "importance" %}
  
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const tagButtons = document.querySelectorAll('.tag-btn');
  const projectCards = document.querySelectorAll('.project-card');
  
  tagButtons.forEach(button => {
    button.addEventListener('click', function() {
      const selectedTag = this.getAttribute('data-tag');
      
      // Update active button
      tagButtons.forEach(btn => btn.classList.remove('active'));
      this.classList.add('active');
      
      // Filter projects
      projectCards.forEach(card => {
        if (selectedTag === 'all' || card.dataset.tags.includes(selectedTag)) {
          card.style.display = 'block';
        } else {
          card.style.display = 'none';
        }
      });
    });
  });
});
</script>
