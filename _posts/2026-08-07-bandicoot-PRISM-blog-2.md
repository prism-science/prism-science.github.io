---
layout: single
title: 'Displaying Conformational Heterogeneity in BANDICOOT'
author: lyubimov-art
date: 2026-08-07
classes: wide
categories:
  - post
tags:
  - coot
  - molecular modeling
  - macos
gallery1:
    - url: /assets/images/posts/2026_08_07/altloc_coloring_bandicoot_3NYD.png
      image_path: /assets/images/posts/2026_08_07/altloc_coloring_bandicoot_3NYD.png
      title: "Model colored by heterogeneity displayed in Bandicoot v0.1.4.12"
excerpt: "In preparation for hierarchical hetereogeneity encoding, BANDICOOT has a new, more intuitive display mode for alternate conformations."
comments: true
---

In order for structural biologists to effectively use the new paradigm of hierarchical conformational heterogeneity to understand and build macromolecular structures, they should be able to view and model it. The new version of BANDICOOT (v0.1.4.12) takes a small step in that direction by introducing a new atom coloring mode: by alternate conformation.

This display mode, selected in a drop-down menu in BANDICOOT's Display Manager, generates a hue offset for each altloc (a residue modeled with conformational hetereogeneity) such that all the alternate conformations are visually distinguishable at a glance. The offsets are configurable, so that each user can create the level of visual distinction most comfortable and intuitive to them. The mode works smoothly: removing all alternate conformations automatically reverts the residue to the coloring of bulk molecule, while each added alternate conformation is automatically hue-shifted from the last one.

This is only the first small step in a larger project to implement hierarchical heterogeneity tools and features in BANDICOOT. When complete, users will be able to not only view altlocs in different colors, but visualize the hierarchy, assign hierarchical positions to each alternate conformation, and, importantly, output mmCIF-formatted files with this information.

{% include gallery id="gallery1" caption="Model colored by heterogeneity displayed in Bandicoot v0.1.4.12" %}

Bandicoot is an open-source project, forked from Coot 0.9.8.95. Source code and binary releases are available for download from the public repository at [https://github.com/fraser-lab/bandicoot](https://github.com/fraser-lab/bandicoot). Currently, Bandicoot runs on only on MacOS (tested on Tahoe but runnable on previous MacOS versions as well). It's a work in progress and thus is a bit rough around the edges. Users are encouraged to report any issues and submit pull requests.
