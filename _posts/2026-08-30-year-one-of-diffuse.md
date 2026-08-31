---
title: A Year (plus) of DiffUSE
layout: single
author: stephaniewankowicz
layout: single
excerpt: Science progress over the first year-ish of the DiffUSE Project
categories:
  - posts
tags:
  - meta
comments: true
---
## A Year (plus-ish) of DiffUSE

The DiffUSE Project began in July 2025 as an experiment in democratizing the methods of dynamic structural biology. The conventional approach to a project like this would be sequential: collect the data, process it, model it, encode it, then interpret it. We instead chose to address the full pipeline at once. By organizing loose teams around data collection and processing, modeling (both molecular dynamics and machine learning), encoding, and interpretation, each team worked immediately within the scope of the problem in front of it. 

Over the past year, we have made significant progress in every area. We demonstrated reproducibility in diffuse scattering, our first experimental data collection area; measurements across two beamlines (pub coming soon!); [collected data on 8 different proteins](https://diffuse.science/logbook/); and [advanced theory to better model this data](https://diffuse.science/posts/goodvibes/). We also built [a robust modeling platforms that integrate structure predictors with experimental data](https://github.com/prism-science/sampleworks) and used it to [stress-test how much memorization exists in structure predictors](https://thestacks.org/publications/sampleworks-release). We also [recovered latent heterogeneity from deposited X-ray crystallography data in over 60k X-ray structures](https://thestacks.org/publications/qfit-at-scale). Finally, we have developed [algorithms](https://www.biorxiv.org/content/10.64898/2026.08.26.747373v1) and [methods](https://thestacks.org/publications/method-bulksolvent) for analyzing solvent signal in protein structures, a crux for correctly modeling experimental structural biology data. 
A year in, the individual parts of the project are now beginning to converge. We are beginning to integrate diffuse scattering data into our modeling software, and consider how to encode different types of heterogeneity in mmCIF files.


### By the Numbers

#### 4 Scholarly Pubs with 8 different contributors

- [sampleworks: A Modular Platform for Experimentally Guided Biomolecular Ensemble Generation](https://thestacks.org/publications/sampleworks-release)
- [Supplying a User-Defined Bulk Solvent Map for Refinement](https://thestacks.org/publications/method-bulksolvent)
- [Recovering Conformational Heterogeneity from the Protein Data Bank at Scale](https://thestacks.org/publications/qfit-at-scale)
- [WaterFlow: Prediction of Ordered Water Molecule Positions on Protein Structures](https://www.biorxiv.org/content/10.64898/2026.08.26.747373v1)

#### [16 Logbooks](https://diffuse.science/logbook/) with 18 different contributors

#### 5 Key Software Methods with 13 different contributors

- [Mdx2: an open-source toolkit for diffuse data processing written in Python](https://github.com/prism-science/mdx2)
- [sampleworks: a Python framework for integrating generative biomolecular structure models with experimental data](https://github.com/prism-science/sampleworks)
- [WaterFlow: a Deep Learning model that predicts the positions of ordered water molecules conditioned on a protein structure](https://github.com/prism-science/WaterFlow)
- [Goodvibes (General Optimization Of Diffuse halos from VIBrational Elastic network Simulations): a software package that produces a full forward model of the phononic contribution to the diffuse signal](https://github.com/prism-science/goodvibes)
- [A Python library and command-line tool for reading, writing, and modifying PDBx/mmCIF protein structure files with support for hierarchical heterogeneity extensions](https://github.com/prism-science/pdbx_hierarchy)

#### [38 Blog Posts written by 14 different authors!](https://diffuse.science/posts/)
