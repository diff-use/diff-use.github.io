---
layout: splash
author: diffuse
author_profile: false
header:
  overlay_image: assets/images/20250805_Mac1_diffuse_crop.png
  overlay_filter: 0.4
excerpt: "Unlocking Protein Dynamics"

feature_row_science:
  - image_path: assets/images/morph2.gif
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
     We believe that unlocking protein dynamics require not just new methods but also new ways we work together as scientists. By building openly, we are enabling the entire community to generate high-quality dynamic data at the scale and diversity needed to uncover the fundamental principles of how biology moves.
    url: /about/
    btn_label: "About the Project"
    btn_class: "btn--primary"

---
{% include feature_row id="feature_row_science" type="left" %}

{% include feature_row id="feature_row_philosophy" type="right" %}

<h2 style="text-align: center;"><a href="/posts/" style="text-decoration: none; color: inherit;">Latest Posts from our Scientists</a></h2>

<div class="grid__wrapper">
  {% for post in site.posts limit:3 %}
    {% include archive-single.html type="list" %}
  {% endfor %}
</div>

![diffUSE Project logo](/assets/images/diffuse_logo_banner.jpg){:style="max-height:300px; display: block; margin-left: auto; margin-right: auto;"}

