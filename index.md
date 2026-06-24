---
layout: page
title: 내 AI 블로그
---

<!-- ============================================================
  히어로 배너
  - Markdown 블록쿼트(>) 를 CSS 에서 다크 그라디언트 배너로 스타일링
  - site.posts | size : Jekyll 이 _posts/ 파일 수를 자동으로 셈
============================================================ -->
> 🤖 **n8n + Solar AI** 가 자동 생성하는 블로그 &nbsp;&nbsp;|&nbsp;&nbsp; 📝 총 **{{ site.posts | size }}**개 포스트

<!-- ============================================================
  포스트 카드 목록

  [래퍼 div 역할]
  - markdown="1"    : kramdown 이 이 div 안의 내용을 Markdown 으로 파싱함
  - class="post-list": CSS 에서 .post-list h3 / .post-list h3+p 로만
                       카드 스타일 적용 → 포스트 본문의 h3 에는 영향 없음

  [링크 생성 방식]
  - site.posts      : _posts/ 폴더 .md 파일을 Jekyll 이 자동 수집 (최신순 정렬)
  - post.url        : _config.yml permalink 규칙으로 Jekyll 이 만든 정확한 URL
                      예) /posts/2026/06/23/딥페이크의-두-얼굴-혁신과-위험-사이/
  - | relative_url  : GitHub Pages 배포 경로(baseurl)를 자동으로 앞에 붙여줌
                      예) /n8n-blog/posts/2026/06/23/.../

  [카드 Markdown 구조 → 렌더링 결과]
  - ### [제목](링크) → <h3><a href="...">제목</a></h3>  (카드 상단·제목)
  - 📅 날짜 · `카테고리` → <p>...</p>                    (카드 하단·메타)
  - ---              → <hr>                              (카드 간 여백, 선 숨김)
============================================================ -->
<div class="post-list" markdown="1">
{% for post in site.posts %}
### [{{ post.title }}]({{ post.url | relative_url }})
📅 {{ post.date | date: "%Y.%m.%d" }} &nbsp;·&nbsp; `{{ post.categories | first }}`

---
{% endfor %}
</div>
