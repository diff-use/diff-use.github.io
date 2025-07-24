---
permalink: /members/
title: "Team Members"
layout: default           # or "page" – whatever the other pages use
---

<!-- ─────────── HERO STRIP ─────────── -->
<section class="hero">
  <div class="wrapper container-padding">
    <h1 class="heading-xl">Team Members</h1>
    <p class="heading-lg">
      Meet the dedicated researchers and scientists driving the diffUSE project forward
    </p>
  </div>
</section>

<!-- ───────── GRID OF GROUPS & CARDS ───────── -->
<div class="wrapper container-padding members-grid">

{% for block in site.data.members %}
  <h2 class="heading-lg group-heading">{{ block.group }}</h2>

  <div class="card-column">
  {% for person in block.items %}
    <div class="member-card">
      <img src="{{ person.photo }}" alt="{{ person.name }}" class="avatar" />
      <div class="info">
        <span class="name">{{ person.name }}</span><br>
        <span class="title">{{ person.title }}</span>
      </div>
    </div>
  {% endfor %}
  </div>
{% endfor %}

</div>