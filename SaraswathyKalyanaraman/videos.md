---
layout: default
title: Video Memories
---

# 🎥 Videos

<div class="video-gallery">

{% for file in site.static_files %}
  {% if file.path contains '/SaraswathyKalyanaraman/assets/videos/' %}
    {% assign ext = file.extname | downcase %}
    {% if ext == '.mp4' or ext == '.webm' or ext == '.mov' %}
      <div class="video-card"
           onmouseenter="playLocalPreview(this)"
           onmouseleave="pauseLocalPreview(this)"
           onclick="openVideoModal('local', '{{ site.baseurl }}{{ file.path }}', '{{ file.name }}')">

        <div class="video-wrapper">
          <video muted loop playsinline preload="metadata">
            <source src="{{ site.baseurl }}{{ file.path }}">
          </video>
          <div class="play-overlay">▶</div>
        </div>

        <p>{{ file.name | replace: '_', ' ' | replace: '.mp4', '' | replace: '.webm', '' | replace: '.mov', '' }}</p>
      </div>
    {% endif %}
  {% endif %}
{% endfor %}

{% assign youtube_videos = site.data.saraswathykalyanaraman_youtube %}
{% if youtube_videos %}
  {% for video in youtube_videos %}
    {% assign video_id = video.url | split: '/' | last %}

    <div class="video-card"
         data-youtube-id="{{ video_id }}"
         onmouseenter="playYouTubePreview(this)"
         onmouseleave="stopYouTubePreview(this)"
         onclick="openVideoModal('youtube', '{{ video.url }}', '{{ video.title }}')">

      <div class="video-wrapper youtube-wrapper">
        <img src="https://img.youtube.com/vi/{{ video_id }}/hqdefault.jpg" alt="{{ video.title }}">
        <div class="youtube-preview-holder"></div>
        <div class="play-overlay">▶</div>
      </div>

      <p>{{ video.title }}</p>
    </div>
  {% endfor %}
{% endif %}

</div>

<div id="videoModal" class="modal" onclick="closeVideoModal()">
  <span class="modal-close">&times;</span>
  <div id="modalContent" onclick="event.stopPropagation()"></div>
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

.video-wrapper img,
.video-wrapper video,
.video-wrapper iframe {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border: 0;
  display: block;
}

.youtube-preview-holder {
  position: absolute;
  inset: 0;
  z-index: 2;
}

.play-overlay {
  position: absolute;
  inset: 0;
  z-index: 3;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 48px;
  color: white;
  background: rgba(0,0,0,0.3);
  transition: opacity 0.25s ease;
}

.video-card:hover .play-overlay {
  opacity: 0;
}

.video-card p {
  margin-top: 8px;
  font-size: 14px;
  color: #5a4a42;
}

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
  box-sizing: border-box;
}

.modal video,
.modal iframe {
  width: 95%;
  max-width: 1000px;
  height: 75vh;
  border-radius: 10px;
  border: 0;
}

.modal-caption {
  color: #fff;
  margin-top: 12px;
  font-size: 16px;
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

function playLocalPreview(card) {
  const video = card.querySelector("video");
  if (video) {
    video.currentTime = 0;
    video.play();
  }
}

function pauseLocalPreview(card) {
  const video = card.querySelector("video");
  if (video) {
    video.pause();
    video.currentTime = 0;
  }
}

function playYouTubePreview(card) {
  const videoId = card.dataset.youtubeId;
  const holder = card.querySelector(".youtube-preview-holder");

  if (!holder || holder.innerHTML.trim() !== "") return;

  holder.innerHTML = `
    <iframe
      src="https://www.youtube.com/embed/${videoId}?autoplay=1&mute=1&controls=0&loop=1&playlist=${videoId}&modestbranding=1&rel=0"
      allow="autoplay; encrypted-media"
      allowfullscreen>
    </iframe>
  `;
}

function stopYouTubePreview(card) {
  const holder = card.querySelector(".youtube-preview-holder");
  if (holder) {
    holder.innerHTML = "";
  }
}

function openVideoModal(type, src, title) {
  const modal = document.getElementById("videoModal");
  const content = document.getElementById("modalContent");
  const caption = document.getElementById("modalCaption");

  modal.style.display = "block";

  if (type === "youtube") {
    const separator = src.includes("?") ? "&" : "?";
    content.innerHTML = `
      <iframe
        src="${src}${separator}autoplay=1"
        allow="autoplay; encrypted-media"
        allowfullscreen>
      </iframe>
    `;
    caption.innerText = title;
  } else {
    content.innerHTML = `
      <video controls autoplay>
        <source src="${src}">
      </video>
    `;
    caption.innerText = cleanName(title);
  }
}

function closeVideoModal() {
  document.getElementById("videoModal").style.display = "none";
  document.getElementById("modalContent").innerHTML = "";
}
</script>
