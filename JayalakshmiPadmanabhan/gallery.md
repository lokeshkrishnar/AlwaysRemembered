
---
layout: default
title: Photo Gallery
---

# 📸 Memories in Pictures

<div class="gallery">
{% for file in site.static_files %}
  {% if file.path contains '/JayalakshmiPadmanabhan/assets/images/' %}
    {% assign ext = file.extname | downcase %}
    {% if ext == '.jpg' or ext == '.jpeg' or ext == '.png' or ext == '.webp' or ext == '.gif' %}
      <div class="gallery-item">
        <div class="image-wrapper" style="background-image: url('{{ site.baseurl }}{{ file.path }}');">
          <img
            src="{{ site.baseurl }}{{ file.path }}"
            alt="{{ file.name }}"
            onclick="openModal('{{ site.baseurl }}{{ file.path }}', '{{ file.name }}')"
          >
        </div>

        <p>{{ file.name | replace: '_', ' ' | replace: '.jpeg', '' | replace: '.jpg', '' | replace: '.png', '' | replace: '.webp', '' | replace: '.gif', '' }}</p>
      </div>
    {% endif %}
  {% endif %}
{% endfor %}
</div>

<div id="imageModal" class="modal" onclick="closeModal()">
  <span class="modal-close">&times;</span>
  <img id="modalImage" class="modal-content">
  <p id="modalCaption" class="modal-caption"></p>
</div>

<style>
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 22px;
}

.gallery-item {
  background: #f4efe9;
  padding: 12px;
  border-radius: 14px;
  text-align: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

.image-wrapper {
  position: relative;
  width: 100%;
  height: 260px;
  border-radius: 12px;
  overflow: hidden;
  background-size: cover;
  background-position: center;
}

.image-wrapper::before {
  content: "";
  position: absolute;
  inset: 0;
  background-image: inherit;
  background-size: cover;
  background-position: center;
  filter: blur(20px);
  transform: scale(1.15);
  z-index: 1;
}

.image-wrapper img {
  position: relative;
  z-index: 2;
  width: 100%;
  height: 100%;
  object-fit: contain;
  cursor: pointer;
}

.gallery-item p {
  margin-top: 8px;
  font-size: 14px;
  color: #5a4a42;
}

/* Fullscreen modal */
.modal {
  display: none;
  position: fixed;
  z-index: 9999;
  padding: 30px;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.88);
  box-sizing: border-box;
  text-align: center;
}

.modal-content {
  max-width: 95%;
  max-height: 85%;
  object-fit: contain;
  border-radius: 10px;
}

.modal-caption {
  color: #fff;
  font-size: 16px;
  margin-top: 12px;
}

.modal-close {
  position: absolute;
  top: 18px;
  right: 28px;
  color: #fff;
  font-size: 36px;
  font-weight: bold;
  cursor: pointer;
}
</style>

<script>
function cleanCaption(filename) {
  return filename
    .replace(/\.(jpeg|jpg|png|webp|gif)$/i, "")
    .replace(/_/g, " ");
}

function openModal(imageSrc, imageName) {
  document.getElementById("imageModal").style.display = "block";
  document.getElementById("modalImage").src = imageSrc;
  document.getElementById("modalCaption").innerText = cleanCaption(imageName);
}

function closeModal() {
  document.getElementById("imageModal").style.display = "none";
}
</script>

## 📸 [Memories in Voice](audio.md)

## 📸 [Memories in Video](videos.md)
