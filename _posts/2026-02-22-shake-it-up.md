---
layout: single
title: 'Shake It Up!'
author: mewall
date: 2026-02-22
classes: wide
categories:
  - post
tags:
  - diffuse scattering
  - molecular dynamics
  - modeling
  - open science
  - meta
gallery:
    - url: /assets/images/posts/2026-02-23/Mac1_NoADPr.png
      image_path: /assets/images/posts/2026-02-23/Mac1_NoADPr.png
      alt: "MD diffuse with CHES"
      title: "MD diffuse with CHES (buffer molecule)"
    - url: /assets/images/posts/2026-02-23/Mac1_WithADPr.png
      image_path: /assets/images/posts/2026-02-23/Mac1_WithADPr.png
      alt: "MD diffuse with ADPr"
      title: "MD diffuse with ADPr"
    - url: /assets/images/posts/2026-02-23/Mac1_DeltaADPr.png
      image_path: /assets/images/posts/2026-02-23/Mac1_DeltaADPrAniso.png
      alt: "Difference ADPr - CHES"
      title: "Difference ADPr - CHES"
excerpt: >
  MD simulations of changes in diffuse scattering depending on ligand binding
comments: true
---

## *MD simulations of changes in diffuse scattering depending on ligand binding*

{% include gallery caption="MD simulations of Mac1 diffuse scattering change depending on ligand binding. *Left*. Mac1 with CHES (buffer molecule). *Center*. Mac1 with ADPr. *Right*. Difference." %}

## What did we find?

In a previous [post]({% post_url 2025-11-15-in_the_cloud %}) I talked about our plan to perform MD simulations of Mac1 crystals under different conditions. We had just started an MD simulation of Mac1 in complex with ADP-ribose (ADPr), and were waiting for it to finish. We weren't sure how different it would be from the [initial simulations]({% post_url 2025-08-05-lets-dance %}) of Mac1 without ADPr, in which a CHES buffer occupies the ADPr binding site.  

Now we know more. Visual comparisons (above images) show that the rich anisotropic diffuse diffuse features in the maps with CHES buffer (left) vs. ADPr (center) in the binding pocket have similar patterns of peaks and troughs that differ in detail. Subtracting them reveals the differences more clearly (right). Quantitative analysis shows that the variations in the difference map are comparable in strength to the intensities in either individual map. This result is encouraging as it indicates that such differences might be observed in experiments.

## It's a trap!

Along the way we encountered a common pitfall in making these kinds of comparisons: due to an indexing ambiguity in the P43 space group, the structures of Mac1 used for simulations with and without ADPr were solved using different definitions of the lattice vectors, with the *h* and *k* axis swapped, and the *l* axis reversed (compare PDB IDs [7TX0](https://www.rcsb.org/structure/7TX0) and [7TX3](https://www.rcsb.org/structure/7TX3)). The diffUSE modeling team worked out how to make the simulated diffuse maps consistent at our recent [all hands meeting]({% post_url 2026-02-02-allhands %}), enabling us to perform a controlled comparison of the simulations.

## What next?

The next step is to compare both of these simulations with data recently collected at CHESS (see [logbook](https://diffuse.science/logbook/beamtime/20251105-chess/)), in one of a series of diffUSE beam times that are expected to yield a large number of datasets. These runs already have revealed that diffuse data are [reproducible between CHESS and ALS beamlines]({% post_url 2026-02-02-allhands %}). Data from Mac1 +/- ADPr are now in the processing pipeline; we're eager to see how Mac1 diffuse scattering changes upon ligand binding, and whether MD simulations can help explain what we see.

---
