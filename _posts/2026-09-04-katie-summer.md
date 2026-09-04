---
title: Varying crystallization conditions to study lattice effects on diffuse scattering
layout: single
author: katie-lu
excerpt: My summer research project in the Ando Lab
classes: wide
categories:
  - posts
tags:
  - diffuse scattering
  - crystallography
comments: true
---

This summer, I worked on a diffuse scattering project within the Ando Lab, focusing on the protein SARS-CoV-2 NSP3 macrodomain (Mac1). This protein is a virulence factor in the COVID-19 virus, which disrupts ADP-ribosylation to resist host immune response and has been used before for diffuse scattering experiments. To further explore this protein, we aimed to study what effects different crystallization conditions could have on its diffuse scattering. The plan was to first crystallize and optimize the protein in different conditions, then collect diffuse scattering data, determine crystal structures, and analyze what effects differences in the crystal structures arising from crystallization could have on diffuse scattering.

## High-throughput screening

The first step of this experiment was finding different Mac1 growth conditions, through crystallographic screening. Previously, the protein has been crystallized before in several space groups, including P43 and C2 space groups from a 2022 Fraser Lab paper (PDB ID 7KQO​ and 7KR1 respectively)[^Correy2022]. The aforementioned two constructs, Mac1 P43 purified by Kara Zielinski and Mac1 C2 purified by Alex Wirganowicz, were used for sitting-drop vapor diffusion screening. Four 96-well screens from Hampton Research (Index HT, PEGRx HT, PEG/Ion HT, PEG/pH HT) were primarily used for the crystallization conditions. The proteins were first screened without seeding, and then with microseeding using crystals grown in the previous unseeded trays. The Mac1 P43 trays were highly productive: before seeding, the trays produced 8 potential hits total and after, this number climbed to 54. In contrast, the C2 construct was more elusive than the P43 construct, with the unseeding trays yielding 0 hits total. Because there were no hits, for microseeding, crystals were not used from the screening trays, but rather from an earlier hanging-drop tray following the conditions described in the 2022 paper[^Correy2022]. Subsequently, there appeared to be 1 potential hit. 

## Phase diagrams

Next, the focus of the project shifted to optimization using phase diagrams. Optimizing to produce very large crystals is critical to achieve interpretable diffuse scattering signals. This summer, the Ando Lab obtained a Douglas Instruments Oryx 8 crystallization robot, which makes setting up crystallization plates more efficient. One of the robot’s features is producing phase diagrams, where the protein concentration is plotted against the precipitant concentration (the precipitant in this case referring to the crystallization cocktail) (Figure 1).

![Figure 1](/assets/images/posts/2026-09-04/douglas_instruments_phase_diagram.jpg){: .align-center}

*Figure 1. An example of a crystallization phase diagram with four clearly defined regions. From [Douglas Instruments Automated Phase Diagram](https://www.douglas.co.uk/phasediagram).*

To produce phase diagrams, the robot makes two trays, one unseeded and one microseeded. Phase diagrams are beneficial because they help identify the ideal concentrations of protein and precipitant for crystal growth. The target region in phase diagrams is where there is crystal growth but no spontaneous nucleation, meaning that aggregation should result in larger crystals and not more numerous ones. This region is referred to as the “metastable zone”. To observe this region, one should see a clear drop in the unseeded plot and a drop with crystals in the microseeded plot.[^Stubbs2026] Furthermore, to better visualize the concentrations for growth, phase diagrams were created using microbatch-under-oil with 100% paraffin oil instead of vapor diffusion, since vapor diffusion relies on changing concentrations. 

A total of eleven phase diagrams were created based on conditions from the crystallization screens over the summer. Phase diagrams were represented in two ways: firstly, with microscope images of the unseeded and microseeded phase diagrams (Figure 2), and secondly with a scatter plot to make the boundaries between regions more clear (Figure 3). Generally, the phase diagrams reflected the expected pattern of having more crystals on the microseeded side. However, defining the regions was still not perfectly straightforward as not every drop was obviously categorized as either clear, crystal, or precipitate. For instance, it was hard to tell whether some drops were light granular precipitate or whether they were microcrystals. The Ando Lab is considering upgrading their imaging system, which would allow for this issue to be resolved if a new imager could distinguish between the two.

<table>
  <tr>
    <td><img src="/assets/images/posts/2026-09-04/Index_H11_without_seeds.jpg" alt="Figure2a" width="100%"></td>
    <td><img src="/assets/images/posts/2026-09-04/Index_H11_seeds.jpg" alt="Figure2b" width="100%"></td>
  </tr>
</table>

*Figure 2. Crystallization phase diagram for Mac1 based on the hit condition from Index HT screening tray well H11 (0.1 M Potassium thiocyanate, ​30% w/v PEG monomethyl ether 2000). Microscope images have been cropped and overlaid on dots (blue) representing the concentration of protein and precipitant corresponding to each image. The image on the right shows the same experiment with seeds added to the precipitant solution.*

![Figure 3](/assets/images/posts/2026-09-04/Index_H11_phase_diagram.png){: .align-center}

*Figure 3. Scatter plot representation of Mac1 P43 phase diagram based on the condition from Index HT screening tray well H11.*

## What's next?

Further optimizations after the phase diagrams are currently in process. This includes fine-tuning PEG, salt, and pH concentrations, as well as finding the right seed concentration and scaling up microbatch drops. I plan to continue work on optimizing the crystals and collect their data at the Fall beamtimes at the Cornell High Energy Synchrotron Source. Additionally, I hope to work on solving their crystal structures to analyze what effects their crystallization conditions had on them, to better understand what role these changes can have on lattice dynamics. I’m looking forward to continuing work on this project and getting to experience the whole workflow of crystallography from screening to solving structures, while broadly deepening my understanding of biochemical and biophysical research.

## References

[^Correy2022]: Correy, G. J., Kneller, D. W., Phillips, G., Pant, S., Russi, S., Cohen, A. E., ... & Fraser, J. S. (2022). The mechanisms of catalysis and ligand binding for the SARS-CoV-2 NSP3 macrodomain from neutron and x-ray diffraction at room temperature. Science Advances, 8(21), eabo5083. [doi.org/10.1126/sciadv.abo5083](https://doi.org/10.1126/sciadv.abo5083)
[^Stubbs2026]: Stubbs, J., Tremlett, C. J., Waitman, A., Harmer, N. J., Orville, A. M., Tews, I., ... & Shaw Stewart, P. D. (2026). Automated microbatch-under-oil phase diagrams to rationalize serial crystallography sample preparation. IUCrJ, 13(2). [doi.org/10.1107/S2052252526000448](https://doi.org/10.1107/S2052252526000448)