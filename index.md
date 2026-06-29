---
layout: splash
author: diffuse
author_profile: false
header:
  overlay_image: assets/images/20250805_Mac1_diffuse_crop.png
  overlay_filter: 0.4
excerpt: "Unlocking Protein Dynamics"

feature_row_science:
  - image_path: assets/images/morph2_static.png
    alt: "diffuse scattering signals"
    title: "Dynamic Structural Biology"
    excerpt: >
      Proteins are dynamic molecules. They move. They breathe. This movement enables their function. The diffUSE Project is building the methods, tools, and infrastructure to make protein motion visible, measurable, and usable — transforming how we discover drugs, design biology, and understand disease.
    url: /research/
    btn_label: "Our Research"
    btn_class: "btn--primary"

feature_row_philosophy:
  - image_path: assets/images/diffuse_group_2026_01.jpg
    alt: "DiffUSE kick-off meeting"
    title: "Reimagining How We Approach Science"
    excerpt: >
     We believe that unlocking protein dynamics requires not just new methods but also new ways we work together as scientists. By building openly, we aim to enable the collection of dynamic data at the scale and diversity needed to uncover the fundamental principles of biology.
    url: /about/
    btn_label: "About the Project"
    btn_class: "btn--primary"

---

<div class="video-hero-overlap">
  <div class="video-wrapper">
    <iframe
      src="https://www.youtube.com/embed/_DILlMou1GM?autoplay=1&mute=1&cc_load_policy=1&loop=1&playlist=_DILlMou1GM&rel=0&modestbranding=1"
      title="Introducing the DiffUSE Project"
      frameborder="0"
      allow="autoplay; encrypted-media"
      allowfullscreen>
    </iframe>
  </div>
</div>

<div class="home-actions">

  <a href="https://github.com/diff-use" target="_blank" rel="noopener">
    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>
    Code
  </a>

  <a href="https://diffuse.science/logbook/" target="_blank" rel="noopener">
    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"/><path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/></svg>
    Logbook
  </a>

  <a href="/posts/">
    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 3a2.828 2.828 0 1 1 4 4L7.5 20.5 2 22l1.5-5.5L17 3z"/></svg>
    Blog Posts
  </a>

  <a href="https://thestacks.org/organizations/radial" target="_blank" rel="noopener">
    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/><line x1="10" y1="9" x2="8" y2="9"/></svg>
    Scholarly Work
  </a>

</div>

{% include feature_row id="feature_row_science" type="left" %}

{% include feature_row id="feature_row_philosophy" type="right" %}

<h2 style="text-align: center;"><a href="/posts/" style="text-decoration: none; color: inherit;">Latest Posts from our Scientists</a></h2>

<div class="grid__wrapper">
  {% for post in site.posts limit:3 %}
    {% include archive-single.html type="list" %}
  {% endfor %}
</div>

![diffUSE Project logo](/assets/images/diffuse_logo_banner.jpg){:style="max-height:300px; display: block; margin-left: auto; margin-right: auto;"}
