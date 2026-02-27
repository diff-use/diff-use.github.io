---
permalink: /research/
title: "Research"
toc: true
toc_label: "On This Page"
toc_icon: "list"
toc_sticky: true
---


## Unlocking Protein Dynamics
Static structural biology has long been a key enabler of drug discovery and protein function understanding. But proteins are dynamic, and their functions are critically linked to these dynamics. However, our ability to measure, model, and encode these dynamics has been limited. 

The diffUSE Project aims to unlock our understanding of protein dynamics at a scale never before possible.

![diffuse scattering signals](/assets/images/diffuse_signals.png){:style="max-height:300px; display: block; margin-left: auto; margin-right: auto;"}

To unlock the next frontier of advances, we need new methods, more experimental data, and better ways to model and encode protein dynamics. However, we cannot do this on our own. By openly building tools and methods, we engage the entire community to contribute, enabling the scale and diversity of data needed to uncover biological principles. 

Our first avenue is expanding the use of diffuse scattering: a largely overlooked signal measured by X-ray crystallography that could unlock our ability to measure protein dynamics. 

The DiffUSE Project was co-developed with funders and scientists. The team includes both dedicated staff and institutional researchers to enable fast-paced infrastructure-building and specialized basic research. 

## How we are sharing our science

- [The DiffUSE Project Logbook](http://diffuse.science/logbook): Catalog X-ray datasets, collect notes from synchrotron data collection, share reports from data processing, and post preliminary analysis without filters.

- [The DiffUSE Data Management App](https://app.diffuse.science): Under active development, this site will function to document experiment processing with markdown, images, tables, and rich     metadata fields for comprehensive research tracking across datasets and beamlines.

- [Posts from our Scientists](https://diffuse.science/posts/):  Read direct dispatches from our distributed DiffUSE team.


![MD simulated diffuse scattering](/assets/images/20250805_Mac1_diffuse_crop.png){:style="max-height:300px; display: block; margin-left: auto; margin-right: auto;"}

## The DiffUSE Project is working to

{% assign interests = site.research | sort: "index" %}

{% for interest in interests %}
### {{ interest.name }}

{% assign parity = interest.index | modulo:2 %}
{% if parity == 0 %}
{% assign alignment = "right" %}
{% else %}
{% assign alignment = "left" %}
{% endif %}

![{{interest.image_alt}}]({{interest.image}}){:style="float: {{alignment}}; object-fit: contain; width: 35%; max-height: 50em; margin-left: 1em; margin-right: 1em;"}

{{ interest.content }}
{% endfor %}
