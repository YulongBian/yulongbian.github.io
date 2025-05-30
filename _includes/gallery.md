---
layout: page
title: 照片墙
permalink: /gallery/
---

<div class="photo-gallery-container">
  <div id="justified-gallery">
    {% for image in site.static_files %}
      {% if image.path contains 'images/gallery' %}
        <a href="{{ site.baseurl }}{{ image.path }}" 
           data-pswp-width="2000" 
           data-pswp-height="1500" 
           data-cropped="false">
          <img src="{{ site.baseurl }}{{ image.path }}" alt="{{ image.name | remove: '.jpg' | remove: '.png' | remove: '.jpeg' | capitalize }}"/>
        </a>
      {% endif %}
    {% endfor %}
  </div>
</div>

<!-- PhotoSwipe UI 容器 -->
<div class="pswp" tabindex="-1" role="dialog" aria-hidden="true">
  <div class="pswp__bg"></div>
  <div class="pswp__scroll-wrap">
    <div class="pswp__container">
      <div class="pswp__item"></div>
      <div class="pswp__item"></div>
      <div class="pswp__item"></div>
    </div>
    <div class="pswp__ui pswp__ui--hidden">
      <div class="pswp__top-bar">
        <div class="pswp__counter"></div>
        <button class="pswp__button pswp__button--close" title="关闭 (Esc)"></button>
        <button class="pswp__button pswp__button--share" title="分享"></button>
        <button class="pswp__button pswp__button--fs" title="全屏"></button>
        <button class="pswp__button pswp__button--zoom" title="放大/缩小"></button>
        <div class="pswp__preloader">
          <div class="pswp__preloader__icn">
            <div class="pswp__preloader__cut">
              <div class="pswp__preloader__donut"></div>
            </div>
          </div>
        </div>
      </div>
      <div class="pswp__share-modal pswp__share-modal--hidden pswp__single-tap">
        <div class="pswp__share-tooltip"></div>
      </div>
      <button class="pswp__button pswp__button--arrow--left" title="上一张"></button>
      <button class="pswp__button pswp__button--arrow--right" title="下一张"></button>
      <div class="pswp__caption">
        <div class="pswp__caption__center"></div>
      </div>
    </div>
  </div>
</div>

<!-- 引入所需的库 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/justifiedGallery@3.8.1/dist/css/justifiedGallery.min.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/photoswipe@5.3.8/dist/photoswipe.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/photoswipe@5.3.8/dist/default-skin/default-skin.css">

<script src="https://cdn.jsdelivr.net/npm/jquery@3.6.4/dist/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/justifiedGallery@3.8.1/dist/js/jquery.justifiedGallery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/photoswipe@5.3.8/dist/umd/photoswipe.umd.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/photoswipe@5.3.8/dist/umd/photoswipe-lightbox.umd.min.js"></script>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    // 初始化 Justified Gallery
    $("#justified-gallery").justifiedGallery({
      rowHeight: 200,         // 行高
      margins: 5,             // 图片间距
      lastRow: 'justify',     // 最后一行的对齐方式
      border: 0,              // 边框宽度
      randomize: false,       // 是否随机排序
      waitThumbnailsLoad: true // 等待所有缩略图加载完成
    });

    // 初始化 PhotoSwipe
    const lightbox = new PhotoSwipeLightbox({
      gallery: '#justified-gallery',
      children: 'a',
      pswpModule: PhotoSwipe,
      showHideAnimationType: 'zoom'
    });

    // 获取图片实际尺寸
    lightbox.addFilter('itemData', (itemData, index) => {
      const img = new Image();
      img.src = itemData.src;
      
      // 异步获取图片大小
      img.onload = function() {
        itemData.width = img.naturalWidth;
        itemData.height = img.naturalHeight;
      };
      
      return itemData;
    });

    lightbox.init();
  });
</script>