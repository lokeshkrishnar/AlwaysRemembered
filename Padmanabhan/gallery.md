---
layout: default
title: Photo Gallery
---

# 📸 Memories in Pictures

<div class="gallery">
{% for file in site.static_files %}
  {% if file.path contains '/SaraswathyKalyanaraman/assets/images/' %}
    {% assign ext = file.extname | downcase %}
    {% if ext == '.jpg' or ext == '.jpeg' or ext == '.png' or ext == '.webp' or ext == '.gif' %}
      <div class="gallery-item">
        <a href="{{ site.baseurl }}{{ file.path }}" target="_blank">
          <img src="{{ site.baseurl }}{{ file.path }}" alt="{{ file.name }}">
        </a>
        <p>{{ file.name | replace: '_', ' ' | replace: '.jpeg', '' | replace: '.jpg', '' | replace: '.png', '' | replace: '.webp', '' | replace: '.gif', '' }}</p>
      </div>
    {% endif %}
  {% endif %}
{% endfor %}
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

.gallery-item img {
  width: 100%;
  height: 260px;
  object-fit: contain;   /* keeps full image, no cropping */
  border-radius: 10px;
  background: #fff;
  cursor: pointer;
}

.gallery-item p {
  margin-top: 8px;
  font-size: 14px;
  color: #5a4a42;
}
</style>

## 📸 [Memories in Voice](audio.md)

## 📸 [Memories in Video](videos.md)
.
