---
layout: single
title: 'mmCIF Explorer and the Heterogeneity Proposal'
author: kushner-artem
date: 2026-07-25
classes: wide
categories:
  - posts
tags:
  - meta
  - encoding
  - tools
excerpt: "A playground for the PDBx/mmCIF file exploration, a look at the current proposal for encoding correlated heterogeneity"
comments: true
---

The atomic models in the PDB are, for the most part, static snapshots: one set of coordinates representing what is usually a population of many copies of a molecule. A growing body of work across structural biology and machine learning is trying to look past that snapshot at the distribution underneath it, and to predict[^1], measure[^2] and represent[^3][^4] it. This goes under the loose heading of "heterogeneity" — a molecule modelled not as a single conformation but as an ensemble of them, with populations.

One of the hurdles to this is less scientific than operational: you have to be able to write whatever you are trying to represent down — [PDBx/mmCIF](https://mmcif.wwpdb.org/). That format is old, rich, and has a very particular structure that a large amount of software reads, writes and depends on. So extending it gracefully is nontrivial. Any extension has to satisfy several kinds of constraint — physical (it must be able to say what is true of the sample), ontological (it must sit sensibly inside the existing dictionary), and social (the surrounding ecosystem should be able to adopt without rewriting too much).

The tool we are putting together is a bit of a playground towards this effort: [mmcif-browser](https://mmcif-browser-2.vercel.app/). There are three pages: a browser for the mmCIF dictionary itself, a live file inspector paired with a 3D viewer (inspired by [the compiler explorer](https://godbolt.org/)) -- source on one side, its consequence on the other -- and a written version of the current working proposal that anyone can read and pick apart.

![Screenshot of the mmcif-browser file inspector and 3D viewer](/assets/images/posts/2026-07-25/mmcif-browser-image1.png "Figure 1")
*Figure 1: The mmcif-browser file inspector and 3D viewer.*

1. **The dictionary switcher** — flips the definitions the page reads between plain PDBx/mmCIF v50 and v50 plus the proposed heterogeneity extension, so the new categories light up (or don't).
2. **The examples** — the set of example files to play with (some real PDB depositions, some hand-crafted scenarios in service of the proposal).
3. **The heterogeneity states** — where the file contains clearly defined heterogeneity states (either via the existing altloc/occupancy/bfactor mechanisms or via the newly-proposed ones) I provide some QOL UI elements to toggle through them.
4. **The settings bar** — contains filters and by-category navigation so one may quickly find the part of the cif file that one needs.

## The current proposal, briefly

![Diagram of the proposed heterogeneity categories and how they relate to existing altloc/occupancy fields](/assets/images/posts/2026-07-25/mmcif-browser-image2.png "Figure 2")
*Figure 2: The proposed heterogeneity categories, layered on top of the existing altloc/occupancy/bfactor mechanisms.*

mmCIF already records two things per atom: which alternate a given atom belongs to (`label_alt_id`), and the fraction of copies it is present in (`occupancy`).

Both are one-atom-at-a-time facts. What they cannot express is which alternates are found *together* in the same copy — the correlation between sites, the joint distribution rather than its marginals.

The extension aims to add a few optional categories that name alternate states, say which of them exclude one another, and list the combinations that actually co-occur with their joint occupancy.

If that were added, that would bring us one step closer to being able to *communicate* multiple types of heterogeneity, but it's very much an open problem as to how to actually compute these joint states perfectly, define or recover them from standard refinement and bundle them together into biologically meaningful states.

All of this is very much a work in progress — the proposal most of all.

[^1]: Zhong, E. D., Bepler, T., Berger, B. & Davis, J. H. CryoDRGN: reconstruction of heterogeneous cryo-EM structures using neural networks. *Nat Methods* 18, 176–185 (2021). https://doi.org/10.1038/s41592-020-01049-4
[^2]: Meisburger, S. P., Case, D. A. & Ando, N. Robust total X-ray scattering workflow to study correlated motion of proteins in crystals. *Nat Commun* 14, 1228 (2023). https://doi.org/10.1038/s41467-023-36734-3
[^3]: Riley, B. T., Wankowicz, S. A., de Oliveira, S. H. P., van Zundert, G. C. P., Hogan, D. W., Fraser, J. S., Keedy, D. A. & van den Bedem, H. qFit 3: Protein and ligand multiconformer modeling for X-ray crystallographic and single-particle cryo-EM density maps. *Protein Sci* 30, 270–285 (2021). https://doi.org/10.1002/pro.4001
[^4]: Pearce, N. M. & Gros, P. A method for intuitively extracting macromolecular dynamics from structural disorder. *Nat Commun* 12, 5493 (2021). https://doi.org/10.1038/s41467-021-25814-x
