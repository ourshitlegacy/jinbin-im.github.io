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
{% bibliography --file conferences --template conference_bib %}
</div>

<style>
/* 컨퍼런스 헤더 스타일 - 클릭 가능 */
.conference-header {
  margin-top: 2rem;
  margin-bottom: 1.5rem;
  padding: 1.2rem;
  background: #f8f9fa;
  border-left: 4px solid #7b27d8;
  border-radius: 4px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.05);
  cursor: pointer;
  transition: all 0.2s;
  user-select: none;
}

.conference-header:hover {
  background: #f0f1f3;
  box-shadow: 0 2px 4px rgba(0,0,0,0.08);
}

.conference-header h3 {
  margin: 0 0 0.5rem 0;
  font-size: 1.3rem;
  color: #222;
  font-weight: 600;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.conference-header h3::after {
  content: '▼';
  font-size: 0.8rem;
  color: #7b27d8;
  transition: transform 0.3s;
}

.conference-header.collapsed h3::after {
  transform: rotate(-90deg);
}

.conference-full-title {
  font-size: 0.95rem;
  color: #666;
  font-style: italic;
  margin-bottom: 0.5rem;
  line-height: 1.4;
}

.conference-meta {
  font-size: 0.9rem;
  color: #888;
  font-weight: 500;
}

/* 논문 리스트 숨김/표시 */
.conference-papers {
  display: block;
  overflow: hidden;
  max-height: 10000px;
  transition: max-height 0.3s ease-out, opacity 0.3s ease-out;
  opacity: 1;
}

.conference-papers.hidden {
  max-height: 0;
  opacity: 0;
  margin: 0;
  padding: 0;
}

/* 중복 연도 숨김 */
.pub-year {
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
        header.className = 'conference-header collapsed';  // 기본 닫힌 상태
        
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
        
        // 논문 리스트를 감싸는 컨테이너 생성
        const papersContainer = document.createElement('div');
        papersContainer.className = 'conference-papers hidden';  // 기본 숨김
        
        // 해당 컨퍼런스의 논문들 추가
        group.rows.forEach(function(row) {
          papersContainer.appendChild(row);
        });
        
        publications.appendChild(papersContainer);
        
        // 헤더 클릭 시 토글
        header.addEventListener('click', function() {
          header.classList.toggle('collapsed');
          papersContainer.classList.toggle('hidden');
        });
      });
    });
  }, 100);
});
</script>
