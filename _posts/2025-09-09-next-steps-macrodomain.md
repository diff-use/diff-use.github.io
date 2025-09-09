---
title: Next Steps with the Macrodomain Data
layout: single
author: fraserlab
excerpt: What to do next about improving macrodomain data quality and processing
catagories:
  - posts
tags:
  - meta
comments: true
---

In our [last update](https://diffuse.science/posts/wetfeet/), we described the challenges of “getting our feet wet” with the first macrodomain diffuse scattering datasets. Since then, the team has been working to refine both collection strategies and processing approaches. A lot of the progress has come through open exchanges on Slack and logbook notes, which we’re now documenting here for the broader community.

## Choosing a Starting Dataset

From the July 1, 2025 beamtime at ALS 8.3.1 ([log entry here](https://diffuse.science/logbook/beamtime/20250701-als/)), Steve identified several crystals with unusually low mosaicity and high apparent resolution, with **xtal9** standing out as a strong candidate. James Holton merged in additional metadata from his beamline notes, clarifying details like cryostream settings, attenuator positions, and whether backgrounds were measured from air, sleeve, or even the loop neck itself. With that context in place, the group agreed to move forward with xtal9 for parallel processing in **mdx2**.

## The Background Question

One theme that emerged in discussion was *what counts as “background”* in diffuse scattering. James emphasized that centrosymmetric scattering is often difficult to distinguish from air, water, or plastic, and may not be informative. Steve countered that models of diffuse scattering do make predictions for the isotropic component, and by measuring it directly, we can test models on an **absolute scale**—demanding that they account for every observed photon. Different groups have taken different approaches here, and this will remain an active area for debate and experimentation as we broaden access to the methods.

## Tracking Edits and Comments

To help keep track of evolving notes and clarifications, James updated the ALS 7/1 logbook entry with merged metadata, while Steve enabled a [commenting system](https://diffuse.science/logbook/beamtime/20250701-als/) on the logbook site. This should make it easier to trace edits, reference commits on GitHub, and hold technical conversations in context rather than only in Slack. We’re experimenting with how best to use this feature, but it already feels like a useful step toward more transparent documentation.

## Looking Ahead

The next steps are to complete parallel processing of xtal9 with **mdx2** across both teams and to document what works and what doesn’t. We also plan to revisit mounting protocols and humidity control during future beamtime, since unit cell variation between crystals remains a puzzle. 