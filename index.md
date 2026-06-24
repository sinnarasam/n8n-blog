---
layout: page
title: AI 블로그
---

<div class="hero-section">
  <h1 class="hero-title">내 AI 블로그</h1>
  <p class="hero-desc">n8n + Solar AI가 자동으로 생성하는 블로그</p>
  <p class="hero-stats">📝 {{ site.posts | size }}개 포스트</p>
</div>

<div class="filter-bar">
  <button class="filter-btn active" data-cat="all">전체</button>
  <button class="filter-btn" data-cat="AI">AI</button>
  <button class="filter-btn" data-cat="기술">기술</button>
  <button class="filter-btn" data-cat="비즈니스">비즈니스</button>
  <button class="filter-btn" data-cat="라이프">라이프</button>
  <button class="filter-btn" data-cat="헬스">헬스</button>
</div>

<div class="post-grid">
{% assign sorted = site.posts | sort: 'date' | reverse %}
{% for post in sorted %}
  <a class="post-card" href="{{ post.url | relative_url }}" data-cat="{{ post.categories | first }}">
    <span class="cat-badge badge-{{ post.categories | first }}">{{ post.categories | first }}</span>
    <h3 class="card-title">{{ post.title }}</h3>
    <p class="card-date">📅 {{ post.date | date: "%Y.%m.%d" }}</p>
  </a>
{% endfor %}
</div>

<script>
(function () {
  const btns = document.querySelectorAll('.filter-btn');
  const cards = document.querySelectorAll('.post-card');
  btns.forEach(function (btn) {
    btn.addEventListener('click', function () {
      btns.forEach(function (b) { b.classList.remove('active'); });
      btn.classList.add('active');
      var cat = btn.dataset.cat;
      cards.forEach(function (card) {
        card.style.display = (cat === 'all' || card.dataset.cat === cat) ? 'flex' : 'none';
      });
    });
  });
})();
</script>
