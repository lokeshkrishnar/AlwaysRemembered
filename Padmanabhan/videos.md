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
      <div class="video-card">
        <div class="video-wrapper">
          <video controls>
            <source src="{{ site.baseurl }}{{ file.path }}">
            Your browser does not support the video tag.
          </video>
        </div>
        <p>{{ file.name | replace: '_', ' ' | replace: '.mp4', '' | replace: '.webm', '' | replace: '.mov', '' }}</p>
      </div>
    {% endif %}
  {% endif %}
{% endfor %}

{% assign youtube_videos = site.data.youtube %}
{% if youtube_videos %}
  {% for video in youtube_videos %}
    <div class="video-card">
      <div class="video-wrapper">
        <iframe
          src="{{ video.url }}"
          title="{{ video.title }}"
          frameborder="0"
          allowfullscreen>
        </iframe>
      </div>
      <p>{{ video.title }}</p>
    </div>
  {% endfor %}
{% endif %}

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

.video-wrapper iframe,
.video-wrapper video {
  width: 100%;
  height: 100%;
  border: 0;
  display: block;
}

.video-card p {
  margin-top: 8px;
  font-size: 14px;
  color: #5a4a42;
}
</style>
## 🎥 A Special Memory

<iframe width="560" height="315" 
src="https://www.youtube.com/embed/YmBDH4jXudA" 
title="Thatha Video"
frameborder="0" 
allowfullscreen>
</iframe>

<iframe width="560" height="315" 
src="https://www.youtube.com/embed/cqCxBk_drCY" 
title="Thatha Video"
frameborder="0" 
allowfullscreen>
</iframe>

<iframe width="560" height="315" 
src="https://www.youtube.com/embed/J7MdsF64tjg" 
title="Thatha Video"
frameborder="0" 
allowfullscreen>
</iframe>
