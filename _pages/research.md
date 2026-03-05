---
permalink: /research/
title: "Research"
toc: true
toc_label: "On This Page"
toc_icon: "list"
toc_sticky: true
---


## Unlocking Protein Dynamics
Biology is a study of motion and change — yet we still rely on frozen snapshots to understand it.

Static structures can’t tell us what makes a designed enzyme functional, how dynamics shape drug efficacy and resistance, or how motion itself can be engineered and optimized. These are the questions at the frontier of drug discovery, enzyme design, and disease research. The DiffUSE project is building the methods, tools, and infrastructure to make protein motion visible, measurable, and usable — so this frontier becomes accessible to endless biological questions.

## Four Areas of Focus

<div style="display: flex; flex-wrap: wrap; gap: 1.25rem; margin: 1.5rem 0 2.5rem;">

  <details style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(227,88,33,.25); border-radius: 8px; padding: 1.5rem; background: rgba(227,88,33,.04); cursor: pointer;">
    <summary style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #e35821; list-style: none;">Methods</summary>
    <p style="margin: .75rem 0 0; line-height: 1.7;">We are supporting ambitious technical moonshots to improve how dynamic structural biology data is collected, processed, and extracted, with the goal of democratizing these methods so that capturing protein motion becomes routine.</p>
  </details>

  <details style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(227,88,33,.25); border-radius: 8px; padding: 1.5rem; background: rgba(227,88,33,.04); cursor: pointer;">
    <summary style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #e35821; list-style: none;">Modeling</summary>
    <p style="margin: .75rem 0 0; line-height: 1.7;">We are developing machine learning algorithms to uncover hidden information in experimental data, build more robust ensemble models, and leverage information across multiple experimental sources, enabling improved future ensemble prediction models.</p>
  </details>

  <details style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(227,88,33,.25); border-radius: 8px; padding: 1.5rem; background: rgba(227,88,33,.04); cursor: pointer;">
    <summary style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #e35821; list-style: none;">Infrastructure</summary>
    <p style="margin: .75rem 0 0; line-height: 1.7;">We are establishing standards and infrastructure needed to deposit, validate, search, and prepare dynamic structural data for machine learning at scale. Make dynamic data as accessible as static structures so that anyone, not just structural biologists, can leverage it to answer biological questions.</p>
  </details>

  <details style="flex: 1 1 calc(50% - 0.625rem); min-width: 260px; border: 1px solid rgba(227,88,33,.25); border-radius: 8px; padding: 1.5rem; background: rgba(227,88,33,.04); cursor: pointer;">
    <summary style="font-size: .75rem; font-weight: 700; text-transform: uppercase; letter-spacing: .12em; color: #e35821; list-style: none;">Biological Impact</summary>
    <p style="margin: .75rem 0 0; line-height: 1.7;">We are developing tools to elucidate how conformational ensembles drive function, from binding specificity and catalysis to mutational effects, by building the computational tools and metrics that make ensemble-aware enzyme design a practical reality.</p>
  </details>

</div>

## Our First Experimental Deep Dive: Diffuse Scattering

Our first experimental deep dive is expanding the use of diffuse scattering: a largely overlooked signal measured by X-ray crystallography that could unlock our ability to measure protein dynamics. 

![diffuse scattering signals](/assets/images/diffuse_signals.png){:style="max-height:300px; display: block; margin-left: auto; margin-right: auto;"}

- [The DiffUSE Project Logbook](http://diffuse.science/logbook): Catalog X-ray datasets, collect notes from synchrotron data collection, share reports from data processing, and post preliminary analysis without filters.

- [The DiffUSE Data Management App](https://app.diffuse.science): Under active development, this site will function to document experiment processing with markdown, images, tables, and rich     metadata fields for comprehensive research tracking across datasets and beamlines.

- [Posts from our Scientists](https://diffuse.science/posts/):  Read direct dispatches from our distributed DiffUSE team.


![MD simulated diffuse scattering](/assets/images/20250805_Mac1_diffuse_crop.png){:style="max-height:300px; display: block; margin-left: auto; margin-right: auto;"}

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
