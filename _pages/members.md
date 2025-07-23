---
permalink: /members/
title: "Members"
---

{% for author in site.data.authors %}
{% assign member = author[1] %}
{% if member.member %}
{% if member.current %}

## {{ member.name }}

{% if member.avatar %}
![Photograph of {{member.name}}]({{member.avatar}}){:style="float: left; object-fit: contain; width: 30%; max-height: 12em; margin-left: 1em; margin-right: 1em;"}
{% endif %}

{% if member.bio %}
**{{ member.bio }}**
{% endif %}

{% if member.email %}
Email: [{{ member.email }}](mailto:{{ member.email }})
{% endif %}

{% if member.website %}
[Personal website]({{ member.website }})
{% endif %}

{% if member.twitter %}
[@{{ member.twitter }}](https://twitter.com/{{ member.twitter }})
{% endif %}

{{ member.fullbio }}

{% endif %}
{% endif %}
{% endfor %}
