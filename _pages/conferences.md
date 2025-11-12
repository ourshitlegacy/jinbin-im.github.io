---
layout: page
permalink: /conferences/
title: conferences
nav: true
nav_order: 3
years: [2025, 2024, 2023, 2022, 2021]
---

<!-- _pages/conferences.md -->
<!-- Bibsearch Feature -->
{% include bib_search.liquid %}

<div class="publications">
{%- for y in page.years %}
  <div class="year-section" data-year="{{y}}">
    <h2 class="bibliography-year">{{y}}</h2>
    <div class="year-content">
      {%- bibliography --file conferences --template conference_bib --query @*[year={{y}}]* %}
    </div>
  </div>
{%- endfor %}
</div>

<style>
/* 컨퍼런스 헤더 스타일 */
.conference-header {
  margin-top: 2rem;
  margin-bottom: 1rem;
  padding: 1rem;
  background: #f8f9fa;
  border-left: 4px solid #7b27d8;
  border-radius: 4px;
}

.conference-header h3 {
  margin: 0;
  font-size: 1.2rem;
  color: #333;
  font-weight: 600;
}

.conference-meta {
  margin-top: 0.5rem;
  font-size: 0.9rem;
  color: #666;
}

/* 중복 연도 숨김 */
.pub-year {
  display: none !important;
}

/* 권호 페이지 정보 숨김 */
.periodical em {
  display: block;
}

.periodical strong,
.periodical em + strong,
.periodical em + * {
  display: none !important;
}
</style>

<script>
// Conference별 그룹핑을 클라이언트 사이드에서 처리
document.addEventListener('DOMContentLoaded', function() {
  // 약간의 지연을 두고 실행 (bibliography가 완전히 로드된 후)
  setTimeout(function() {
    const yearSections = document.querySelectorAll('.year-content');
    
    yearSections.forEach(function(section) {
      const rows = Array.from(section.querySelectorAll('.conference-row'));
      if (rows.length === 0) return;
      
      // conference 데이터 속성으로 그룹핑
      const conferenceGroups = {};
      
      rows.forEach(function(row) {
        const conference = row.getAttribute('data-conference') || 'Other';
        if (!conferenceGroups[conference]) {
          conferenceGroups[conference] = {
            rows: [],
            address: row.getAttribute('data-address') || '',
            month: row.getAttribute('data-month') || ''
          };
        }
        conferenceGroups[conference].rows.push(row);
      });
      
      // 기존 내용 제거
      section.innerHTML = '';
      
      // 정렬된 conference 순서대로 다시 추가
      Object.keys(conferenceGroups).sort().forEach(function(conference) {
        const group = conferenceGroups[conference];
        
        // 컨퍼런스 헤더 생성
        const header = document.createElement('div');
        header.className = 'conference-header';
        
        const title = document.createElement('h3');
        title.textContent = conference;
        header.appendChild(title);
        
        if (group.address || group.month) {
          const meta = document.createElement('div');
          meta.className = 'conference-meta';
          const metaText = [group.address, group.month].filter(Boolean).join(', ');
          meta.textContent = metaText;
          header.appendChild(meta);
        }
        
        section.appendChild(header);
        
        // 해당 컨퍼런스의 논문들 추가
        group.rows.forEach(function(row) {
          section.appendChild(row);
        });
      });
    });
  }, 100); // 100ms 지연
});
</script>
