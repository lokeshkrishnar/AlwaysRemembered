
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
        <img src="{{ site.baseurl }}{{ file.path }}" alt="{{ file.name }}">
        <p>{{ file.name }}</p>
      </div>
    {% endif %}
  {% endif %}
{% endfor %}
</div>

<style>
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 16px;
}

.gallery-item img {
  width: 100%;
  height: auto;
  border-radius: 12px;
}

.gallery-item p {
  text-align: center;
  font-size: 14px;
}
</style>

## 📸 [Memories in Voice](audio.md)

## 📸 [Memories in Video](videos.md)
