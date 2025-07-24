---
permalink: /members/
title: Members          # keeps the navbar label unchanged
layout: default         # or "page" – match your other pages
---

# Team Members           <!-- uses the default H1 font -->

<div class="members-grid">

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