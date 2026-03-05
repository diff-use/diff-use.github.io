---
permalink: /research/
title: "Research"
toc: true
toc_label: "On This Page"
toc_icon: "list"
toc_sticky: true
---


## Unlocking Protein Dynamics
Static structural biology has long been a key enabler of drug discovery and protein function understanding. But proteins are dynamic, and their functions are critically linked to these dynamics. However, our ability to measure, model, and encode these dynamics has been limited. The diffUSE Project aims to unlock our understanding of protein dynamics at a scale never before possible. 

## Four Pillars of Transformation

<div style="display: flex; flex-wrap: wrap; gap: 1.25rem; margin: 1.5rem 0 2.5rem;">

  <div style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(13,148,136,.25); border-radius: 8px; padding: 1.5rem; background: rgba(13,148,136,.04);">
    <div style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #2dd4bf; margin-bottom: .5rem;">Methods</div>
    <h3 style="margin: 0 0 .75rem; font-size: 1.1rem;"></h3>
    <p style="margin: 0; line-height: 1.7;">Democratize dynamic structural biology methods so that capturing protein motion becomes routine.</p>
  </div>

  <div style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(13,148,136,.25); border-radius: 8px; padding: 1.5rem; background: rgba(13,148,136,.04);">
    <div style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #2dd4bf; margin-bottom: .5rem;">Modeling</div>
    <h3 style="margin: 0 0 .75rem; font-size: 1.1rem;"></h3>
    <p style="margin: 0; line-height: 1.7;">Model and predict conformational ensembles. Build interpretable models that reveal hidden structural states hidden in experimental data.</p>
  </div>

  <div style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(13,148,136,.25); border-radius: 8px; padding: 1.5rem; background: rgba(13,148,136,.04);">
    <div style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #2dd4bf; margin-bottom: .5rem;">Infrastructure</div>
    <h3 style="margin: 0 0 .75rem; font-size: 1.1rem;"></h3>
    <p style="margin: 0; line-height: 1.7;">Make dynamic data as accessible as static structures. Build the databases, standards, and tools so anyone — not just structural biologists — can leverage this data.</p>
  </div>

  <div style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(13,148,136,.25); border-radius: 8px; padding: 1.5rem; background: rgba(13,148,136,.04);">
    <div style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #2dd4bf; margin-bottom: .5rem;">Impact</div>
    <h3 style="margin: 0 0 .75rem; font-size: 1.1rem;"></h3>
    <p style="margin: 0; line-height: 1.7;">Define the biological questions where dynamic structural information is most informative. Ensure every method and tool is grounded in real biological problems.</p>
  </div>

</div>



Our first experimental deep dive is expanding the use of diffuse scattering: a largely overlooked signal measured by X-ray crystallography that could unlock our ability to measure protein dynamics. 

![diffuse scattering signals](/assets/images/diffuse_signals.png){:style="max-height:300px; display: block; margin-left: auto; margin-right: auto;"}

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
