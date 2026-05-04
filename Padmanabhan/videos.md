---
layout: default
title: Video Memories
---

# 🎥 Videos

<div class="video-gallery">

{% for file in site.static_files %}
  {% if file.path contains '/Padmanabhan/assets/videos/' %}
    {% assign ext = file.extname | downcase %}
    {% if ext == '.mp4' or ext == '.webm' or ext == '.mov' %}
      <div class="video-card"
           onclick="openVideoModal('local', '{{ site.baseurl }}{{ file.path }}', '{{ file.name }}')">
        
        <div class="video-wrapper">
          <video preload="metadata" muted>
            <source src="{{ site.baseurl }}{{ file.path }}">
          </video>
          <div class="play-overlay">▶</div>
        </div>

        <p>{{ file.name | replace: '_', ' ' | replace: '.mp4', '' | replace: '.webm', '' | replace: '.mov', '' }}</p>
      </div>
    {% endif %}
  {% endif %}
{% endfor %}


{% assign youtube_videos = site.data.padmanabhan_youtube %}
{% if youtube_videos %}
  {% for video in youtube_videos %}
    
    {% assign video_id = video.url | split: '/' | last %}
    
    <div class="video-card"
         onclick="openVideoModal('youtube', '{{ video.url }}', '{{ video.title }}')">
      
      <div class="video-wrapper">
        <img src="https://img.youtube.com/vi/{{ video_id }}/hqdefault.jpg">
        <div class="play-overlay">▶</div>
      </div>

      <p>{{ video.title }}</p>
    </div>

  {% endfor %}
{% endif %}

</div>

<!-- MODAL -->
<div id="videoModal" class="modal" onclick="closeVideoModal()">
  <span class="modal-close">&times;</span>
  <div id="modalContent"></div>
  <p id="modalCaption" class="modal-caption"></p>
</div>

<style>
.video-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 22px;
}

.video-card {
  background: #f4efe9;
  padding: 12px;
  border-radius: 14px;
  text-align: center;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

.video-wrapper {
  position: relative;
  width: 100%;
  aspect-ratio: 16 / 9;
  border-radius: 12px;
  overflow: hidden;
  background: #000;
}

/* Thumbnail (image or video preview) */
.video-wrapper img,
.video-wrapper video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Play button */
.play-overlay {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 48px;
  color: white;
  background: rgba(0,0,0,0.3);
}

/* Caption */
.video-card p {
  margin-top: 8px;
  font-size: 14px;
  color: #5a4a42;
}

/* MODAL */
.modal {
  display: none;
  position: fixed;
  z-index: 9999;
  padding: 30px;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.9);
  text-align: center;
}

.modal video,
.modal iframe {
  max-width: 95%;
  max-height: 80vh;
  border-radius: 10px;
}

.modal-caption {
  color: #fff;
  margin-top: 12px;
}

.modal-close {
  position: absolute;
  top: 20px;
  right: 30px;
  color: #fff;
  font-size: 36px;
  cursor: pointer;
}
</style>

<script>
function cleanName(name) {
  return name
    .replace(/\.(mp4|webm|mov)$/i, "")
    .replace(/_/g, " ");
}

function openVideoModal(type, src, title) {
  const modal = document.getElementById("videoModal");
  const content = document.getElementById("modalContent");
  const caption = document.getElementById("modalCaption");

  modal.style.display = "block";

  if (type === "youtube") {
    content.innerHTML = `<iframe src="${src}?autoplay=1" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>`;
    caption.innerText = title;
  } else {
    content.innerHTML = `<video controls autoplay><source src="${src}"></video>`;
    caption.innerText = cleanName(title);
  }
}

function closeVideoModal() {
  document.getElementById("videoModal").style.display = "none";
  document.getElementById("modalContent").innerHTML = "";
}
</script>
