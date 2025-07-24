---
permalink: /members/
title: Team Members        # shows automatically as the normal page heading
layout: default            # keep whatever your other pages use
---

<div class="members-layout">
  {%- assign first = site.data.members | first -%}
  {%- assign rest  = site.data.members | slice: 1, 10 -%}

  <!-- LEFT column ───────────────────────────────────── -->
  <div class="left-col">
    <h2 class="heading-lg">{{ first.group }}</h2>
    <div class="card-column">
      {%- for person in first.items -%}
      <div class="member-card">
        <img src="{{ person.photo }}" alt="{{ person.name }}" class="avatar">
        <div class="info">
          <span class="name">{{ person.name }}</span><br>
          <span class="title">{{ person.title }}</span>
        </div>
      </div>
      {%- endfor -%}
    </div>
  </div>

  <!-- RIGHT column ──────────────────────────────────── -->
  <div class="right-col">
    {%- for block in rest -%}
    <h2 class="heading-lg">{{ block.group }}</h2>
    <div class="card-column">
      {%- for person in block.items -%}
      <div class="member-card">
        <img src="{{ person.photo }}" alt="{{ person.name }}" class="avatar">
        <div class="info">
          <span class="name">{{ person.name }}</span><br>
          <span class="title">{{ person.title }}</span>
        </div>
      </div>
      {%- endfor -%}
    </div>
    {%- endfor -%}
  </div>
</div>