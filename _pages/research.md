---
permalink: /research/
title: "Research"
toc: true
toc_label: "On This Page"
toc_icon: "list"
toc_sticky: true
---


## Unlocking Protein Dynamics
Static protein structures have transformed our understanding of life — but they are snapshots of molecules that are fundamentally in motion. Proteins' function is critically linked to this motion. Uncovering these motions will unlock new ways to understand disease, design better drugs, and engineer proteins with precise, tunable function.

The DiffUSE Project was co-developed with funders and scientists. The team includes both dedicated staff and institutional researchers to enable fast-paced infrastructure-building and specialized basic research. 

## Four Areas of Focus

<div style="display: flex; flex-wrap: wrap; gap: 1.25rem; margin: 1.5rem 0 2.5rem;">

  <div style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(227,88,33,.25); border-radius: 8px; padding: 1.5rem; background: rgba(227,88,33,.04);">
    <div style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #e35821; margin-bottom: .5rem;">Methods</div>
    <h3 style="margin: 0 0 .75rem; font-size: 1.1rem;"></h3>
    <p style="margin: 0; line-height: 1.7;">Democratize dynamic structural biology methods so that capturing protein motion becomes routine.</p>
  </div>

  <div style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(227,88,33,.25); border-radius: 8px; padding: 1.5rem; background: rgba(227,88,33,.04);">
    <div style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #e35821; margin-bottom: .5rem;">Modeling</div>
    <h3 style="margin: 0 0 .75rem; font-size: 1.1rem;"></h3>
    <p style="margin: 0; line-height: 1.7;">Model and predict conformational ensembles. Build interpretable models that reveal hidden structural states hidden in experimental data.</p>
  </div>

  <div style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(227,88,33,.25); border-radius: 8px; padding: 1.5rem; background: rgba(227,88,33,.04);">
    <div style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #e35821; margin-bottom: .5rem;">Infrastructure</div>
    <h3 style="margin: 0 0 .75rem; font-size: 1.1rem;"></h3>
    <p style="margin: 0; line-height: 1.7;">Make dynamic data as accessible as static structures. Build the databases, standards, and tools so anyone, not just structural biologists, can leverage this data.</p>
  </div>

  <div style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(227,88,33,.25); border-radius: 8px; padding: 1.5rem; background: rgba(227,88,33,.04);">
    <div style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #e35821; margin-bottom: .5rem;">Impact</div>
    <h3 style="margin: 0 0 .75rem; font-size: 1.1rem;"></h3>
    <p style="margin: 0; line-height: 1.7;">Define the biological questions where dynamic structural information is most informative.</p>
  </div>

</div>

## Our First Experimental Deep Dive: Diffuse Scattering

Our first experimental deep dive is expanding the use of diffuse scattering: a largely overlooked signal measured by X-ray crystallography that could unlock our ability to measure protein dynamics. 

![diffuse scattering signals](/assets/images/diffuse_signals.png){:style="max-height:300px; display: block; margin-left: auto; margin-right: auto;"}

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
