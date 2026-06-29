---
permalink: /members/
title: Team Members        # shows automatically as the normal page heading
layout: default            # keep whatever your other pages use
---

<h2>DiffUSE Project Team Members</h2>{:style="text-align:center;margin-top: 20px"}

<div class="members-layout">
  {%- assign first = site.data.members | first -%}
  {%- assign rest  = site.data.members | slice: 1, 10 -%}
  {%- assign halfway = site.data.members | size | divided_by: 2 -%}

  <!-- LEFT column ───────────────────────────────────── -->
  <div class="left-col">
    <div class="card-column">
      {%- for person in site.data.members -%}
      {%- if forloop.index <= halfway -%}
        <div class="member-card">
          <img src="{{ person.photo }}" alt="{{ person.name }}" class="avatar">
          <div class="info">
            <span class="name">{{ person.name }}</span><br>
            <span class="title">{{ person.title }}</span>
            {%- if person.email -%}
            <br><a href="mailto:{{ person.email }}" class="btn btn--small btn--diffuse">Email {{ person.name | split: " " | first }}</a>
            {%- endif -%}
          </div>
        </div>
      {%- endif -%}
      {%- endfor -%}
    </div>
  </div>

  <!-- RIGHT column ──────────────────────────────────── -->
  <div class="right-col">
    <div class="card-column">
      {%- for person in site.data.members -%}
      {%- if forloop.index > halfway -%}
        <div class="member-card">
          <img src="{{ person.photo }}" alt="{{ person.name }}" class="avatar">
          <div class="info">
            <span class="name">{{ person.name }}</span><br>
            <span class="title">{{ person.title }}</span>
            {%- if person.email -%}
            <br><a href="mailto:{{ person.email }}" class="btn btn--small btn--diffuse">Email {{ person.name | split: " " | first }}</a>
            {%- endif -%}
          </div>
        </div>
      {%- endif -%}
      {%- endfor -%}
  </div>
</div>