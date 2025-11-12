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
/* 컨퍼런스 헤더 스타일 - 클릭 가능 */
.conference-header {
  margin-top: 1rem;
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

/* 컨퍼런스별 고유 색상 */
.conference-header[data-conference*="ICCEPM 2024"] {
  border-left-color: #858f99;
}

.conference-header[data-conference*="ICCEPM 2025"] {
  border-left-color: #164b9d;
}

.conference-header[data-conference*="ISARC 2025"] {
  border-left-color: #8d2214;
}

.conference-header[data-conference*="i3CE 2026"],
.conference-header[data-conference*="I3CE 2026"] {
  border-left-color: #152d97;
}

.conference-header[data-conference*="IAQVEC 2026"] {
  border-left-color: #b58c65;
}

.conference-header:hover {
  background: #f0f1f3;
  box-shadow: 0 2px 4px rgba(0,0,0,0.08);
}

/* h3를 그리드 레이아웃으로 변경 - 고정 너비 */
.conference-header h3 {
  margin: 0 0 0.5rem 0;
  font-size: 1.3rem;
  color: #222;
  font-weight: 600;
  display: grid;
  grid-template-columns: 200px 200px 1fr auto;  /* 학회명(200px) | month(200px) | address(나머지) | 화살표 */
  align-items: center;
  gap: 1rem;
}

/* 학회명 - 고정 너비 200px, 왼쪽 정렬 */
.conference-name {
  font-size: 1.3rem;
  font-weight: 600;
  color: #222;
  width: 200px;
}

/* Month - 고정 너비 200px, 왼쪽 정렬 */
.conference-month {
  font-size: 0.75rem;
  font-weight: 400;
  color: #888;
  width: 150px;
}

/* Address - 나머지 공간 사용, 왼쪽 정렬 */
.conference-address {
  font-size: 0.75rem;
  font-weight: 400;
  color: #888;
}

/* 화살표 */
.conference-header h3::after {
  content: '▼';
  font-size: 0.8rem;
  color: #7b27d8;
  transition: transform 0.3s;
  justify-self: end;
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
      const monthValue = row.getAttribute('data-month') || '';  // 변수명 명확하게
      
      if (!yearGroups[year]) {
        yearGroups[year] = {};
      }
      
      if (!yearGroups[year][conference]) {
        yearGroups[year][conference] = {
          rows: [],
          booktitle: booktitle,
          address: address,
          month: monthValue  // monthValue를 저장
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
        header.className = 'conference-header collapsed';
        header.setAttribute('data-conference', conference);
        
        const title = document.createElement('h3');
        
        // 1. 컨퍼런스 이름 (고정 너비 200px, 왼쪽 정렬)
        const confName = document.createElement('span');
        confName.className = 'conference-name';
        confName.textContent = conference;
        title.appendChild(confName);
        
        // 2. Month (고정 너비 200px, 왼쪽 정렬)
        const monthSpan = document.createElement('span');  // 변수명 변경
        monthSpan.className = 'conference-month';
        monthSpan.textContent = group.month || '';  // group.month 값 사용
        title.appendChild(monthSpan);
        
        // 3. Address (나머지 공간, 왼쪽 정렬)
        const addressSpan = document.createElement('span');  // 변수명 변경
        addressSpan.className = 'conference-address';
        addressSpan.textContent = group.address || '';
        title.appendChild(addressSpan);
        
        header.appendChild(title);
        
        // Full title (booktitle)
        if (group.booktitle) {
          const fullTitle = document.createElement('div');
          fullTitle.className = 'conference-full-title';
          fullTitle.textContent = group.booktitle;
          header.appendChild(fullTitle);
        }
        
        publications.appendChild(header);
        
        // 논문 리스트를 감싸는 컨테이너 생성
        const papersContainer = document.createElement('div');
        papersContainer.className = 'conference-papers hidden';
        
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
