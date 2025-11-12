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
{% bibliography --file conferences --template bib_conference %}
</div>

<style>
/* 컨퍼런스 헤더 스타일 */
.conference-header {
  margin-top: 2rem;
  margin-bottom: 1rem;
  padding: 1.2rem;
  background: #f8f9fa;
  border-left: 4px solid #7b27d8;
  border-radius: 4px;
}

.conference-header h3 {
  margin: 0 0 0.3rem 0;
  font-size: 1.2rem;
  color: #333;
  font-weight: 600;
}

.conference-full-title {
  font-size: 0.95rem;
  color: #555;
  font-style: italic;
  margin-bottom: 0.3rem;
}

.conference-meta {
  font-size: 0.9rem;
  color: #666;
}

/* 중복 연도 숨김 */
.pub-year {
  display: none !important;
}

/* Abstract는 토글 (기본 숨김) */
.abstract.hidden {
  display: none;
}

.abstract {
  margin-top: 1rem;
  padding: 1rem;
  background: #f8f9fa;
  border-left: 3px solid #7b27d8;
  border-radius: 4px;
  font-size: 0.9rem;
  line-height: 1.6;
  color: #555;
}

/* Periodical 숨김 (컨퍼런스 헤더에 표시) */
.conference-row .periodical {
  display: none !important;
}

/* Conference row 스타일 */
.conference-row {
  margin-bottom: 2rem;
  padding-left: 1rem;
}
</style>

<script>
// Conference별 그룹핑을 클라이언트 사이드에서 처리
document.addEventListener('DOMContentLoaded', function() {
  setTimeout(function() {
    const publications = document.querySelector('.publications');
    if (!publications) return;
    
    const rows = Array.from(publications.querySelectorAll('.conference-row'));
    if (rows.length === 0) return;
    
    // 연도별, 컨퍼런스별 그룹핑
    const yearGroups = {};
    
    rows.forEach(function(row) {
      const year = row.getAttribute('data-year') || 'Unknown';
      const conference = row.getAttribute('data-conference') || 'Other';
      const booktitle = row.getAttribute('data-booktitle') || '';
      const address = row.getAttribute('data-address') || '';
      const month = row.getAttribute('data-month') || '';
      
      if (!yearGroups[year]) {
        yearGroups[year] = {};
      }
      
      if (!yearGroups[year][conference]) {
        yearGroups[year][conference] = {
          rows: [],
          booktitle: booktitle,
          address: address,
          month: month
        };
      }
      
      yearGroups[year][conference].rows.push(row);
    });
    
    // 기존 내용 제거
    publications.innerHTML = '';
    
    // 연도별로 정렬 (최신순)
    const sortedYears = Object.keys(yearGroups).sort().reverse();
    
    sortedYears.forEach(function(year) {
      // 연도 헤더 생성
      const yearHeader = document.createElement('h2');
      yearHeader.className = 'bibliography-year';
      yearHeader.textContent = year;
      publications.appendChild(yearHeader);
      
      // 해당 연도의 컨퍼런스들을 정렬
      const conferences = Object.keys(yearGroups[year]).sort();
      
      conferences.forEach(function(conference) {
        const group = yearGroups[year][conference];
        
        // 컨퍼런스 헤더 생성
        const header = document.createElement('div');
        header.className = 'conference-header';
        
        const title = document.createElement('h3');
        title.textContent = conference;
        header.appendChild(title);
        
        // Full title (booktitle)
        if (group.booktitle) {
          const fullTitle = document.createElement('div');
          fullTitle.className = 'conference-full-title';
          fullTitle.textContent = group.booktitle;
          header.appendChild(fullTitle);
        }
        
        // Meta info (address, month)
        if (group.address || group.month) {
          const meta = document.createElement('div');
          meta.className = 'conference-meta';
          const metaText = [group.address, group.month].filter(Boolean).join(', ');
          meta.textContent = metaText;
          header.appendChild(meta);
        }
        
        publications.appendChild(header);
        
        // 해당 컨퍼런스의 논문들 추가
        group.rows.forEach(function(row) {
          publications.appendChild(row);
        });
      });
    });
  }, 100);
});
</script>
