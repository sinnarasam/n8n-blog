---
layout: page   # minima 테마의 일반 페이지 레이아웃 사용 (헤더/푸터 포함)
title: AI 블로그
---

<!-- ============================================================
  히어로 섹션 (상단 배너)
  - site.posts | size : Jekyll이 _posts/ 폴더 .md 파일 수를 자동으로 셈
============================================================ -->
<div class="hero-section">
  <h1 class="hero-title">내 AI 블로그</h1>
  <p class="hero-desc">n8n + Solar AI가 자동으로 생성하는 블로그</p>
  <p class="hero-stats">📝 {{ site.posts | size }}개 포스트</p>
</div>

<!-- ============================================================
  카테고리 필터 버튼
  - data-cat 속성값이 아래 자바스크립트 필터와 연결됨
  - "all" → 전체 표시 / 나머지 → 해당 카테고리 카드만 표시
  - n8n 워크플로우에 정의된 5개 카테고리를 그대로 사용
============================================================ -->
<div class="filter-bar">
  <button class="filter-btn active" data-cat="all">전체</button>
  <button class="filter-btn" data-cat="AI">AI</button>
  <button class="filter-btn" data-cat="기술">기술</button>
  <button class="filter-btn" data-cat="비즈니스">비즈니스</button>
  <button class="filter-btn" data-cat="라이프">라이프</button>
  <button class="filter-btn" data-cat="헬스">헬스</button>
</div>

<!-- ============================================================
  포스트 카드 목록 (Liquid 템플릿)

  [링크 생성 방식]
  - site.posts : _posts/ 폴더의 .md 파일을 Jekyll이 자동 수집
                 → posts.yml을 쓰지 않으므로 동기화 누락 문제 없음
                 → 이미 날짜 내림차순(최신 글 먼저) 정렬된 상태
  - post.url   : _config.yml 의 permalink 규칙으로 Jekyll이 생성한 URL
                 예) /posts/2026/06/23/딥페이크의-두-얼굴/
  - relative_url 필터 : GitHub Pages 배포 경로(baseurl)를 자동으로 앞에 붙여줌
                 예) /n8n-blog/posts/2026/06/23/딥페이크의-두-얼굴/

  [카테고리]
  - post.categories : frontmatter 의 categories: [기술] 배열
  - | first         : 배열의 첫 번째 값만 꺼냄 → "기술"
============================================================ -->
<div class="post-grid">
{% for post in site.posts %}
  <a class="post-card"
     href="{{ post.url | relative_url }}"
     data-cat="{{ post.categories | first }}">

    <!-- 카테고리 뱃지: badge-기술, badge-라이프 등 CSS 클래스로 색상 구분 -->
    <span class="cat-badge badge-{{ post.categories | first }}">
      {{ post.categories | first }}
    </span>

    <!-- 포스트 제목 -->
    <h3 class="card-title">{{ post.title }}</h3>

    <!-- 작성일: Jekyll date 필터로 "2026.06.23" 형식 포맷 -->
    <p class="card-date">📅 {{ post.date | date: "%Y.%m.%d" }}</p>

  </a>
{% endfor %}
</div>

<!-- ============================================================
  카테고리 필터 자바스크립트
  - 버튼 클릭 시 data-cat이 일치하는 카드만 표시, 나머지는 숨김
  - "all" 클릭 시 모든 카드 표시
  - IIFE(즉시 실행 함수)로 감싸서 전역 변수 오염 방지
============================================================ -->
<script>
(function () {
  var btns  = document.querySelectorAll('.filter-btn');
  var cards = document.querySelectorAll('.post-card');

  btns.forEach(function (btn) {
    btn.addEventListener('click', function () {

      /* 1) 모든 버튼의 active 스타일 제거 */
      btns.forEach(function (b) { b.classList.remove('active'); });

      /* 2) 클릭한 버튼에 active 스타일 추가 */
      btn.classList.add('active');

      var cat = btn.dataset.cat; /* 버튼의 data-cat 값 읽기 */

      /* 3) 카드 표시 / 숨김 결정 */
      cards.forEach(function (card) {
        var match = (cat === 'all') || (card.dataset.cat === cat);
        card.style.display = match ? 'flex' : 'none';
      });

    });
  });
})();
</script>
