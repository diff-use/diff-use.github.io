---
permalink: /members/
title: Diffuse Team Members              # layout will auto-render this as page__title
layout: default                  # or "page" – match your other content pages
---

<div class="members-grid">

{% comment %}  Loop over the new YAML you added in _data/members.yml {% endcomment %}
{% for block in site.data.members %}
### {{ block.group }}

<div class="card-column">
{% for person in block.items %}
  <div class="member-card">
    <img src="{{ person.photo }}" alt="{{ person.name }}" class="avatar">
    <div class="info">
      <span class="name">{{ person.name }}</span><br>
      <span class="title">{{ person.title }}</span>
    </div>
  </div>
{% endfor %}
</div>
{% endfor %}

</div>