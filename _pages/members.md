---
permalink: /members/
title: "Members"
layout: default          # or "page" – match other pages
---

<!-- HERO STRIP (uses your existing 'heading-xl' utility) -->
<section class="hero">
  <div class="wrapper container-padding">
    <h1 class="heading-xl">Team Members</h1>
  </div>
</section>

<!-- MEMBERS GRID -->
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