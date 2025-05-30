---
layout: page
title: 照片墙
permalink: /gallery/
---

<div class="gallery-container">
  <div class="gallery-grid">
    {% for image in site.static_files %}
      {% if image.path contains 'images/gallery' %}
        <div class="gallery-item">
          <a href="{{ site.baseurl }}{{ image.path }}" data-lightbox="gallery" data-title="{{ image.name | remove: '.jpg' | remove: '.png' | remove: '.jpeg' | capitalize }}">
            <img src="{{ site.baseurl }}{{ image.path }}" alt="{{ image.name }}">
          </a>
        </div>
      {% endif %}
    {% endfor %}
  </div>
</div>

<!-- 添加masonry和lightbox的JS和CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/lightbox2@2.11.3/dist/css/lightbox.min.css">
<script src="https://cdn.jsdelivr.net/npm/masonry-layout@4.2.2/dist/masonry.pkgd.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/imagesloaded@5.0.0/imagesloaded.pkgd.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/lightbox2@2.11.3/dist/js/lightbox.min.js"></script>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    var grid = document.querySelector('.gallery-grid');
    
    // 等待所有图片加载完成后初始化Masonry
    imagesLoaded(grid, function() {
      new Masonry(grid, {
        itemSelector: '.gallery-item',
        columnWidth: '.gallery-item',
        percentPosition: true
      });
    });
    
    // 配置Lightbox
    lightbox.option({
      'resizeDuration': 200,
      'wrapAround': true,
      'fadeDuration': 300
    });
  });
</script>