---
title: "To ensembles and beyond!"
layout: single
author: sampleworks_team
excerpt: "Sampleworks is a framework for integrating structural biology observables, structure predictors, and guidance to improve the modeling of conformational ensembles."
categories:
  - posts
tags:
  - meta
  - modeling
comments: true
---

Most structural biology experimental observables, including those from X-ray crystallography and cryo-electron microscopy (cryo-EM), reflect time and ensemble averages over millions of conformations. Thus, only conformational ensemble models accurately represent the experimental measurements [(Lane 2021\)](https://pubmed.ncbi.nlm.nih.gov/36639584/). However, due to limitations in modeling algorithms, most structural modeling approaches tend to model only the ground state, discarding the rich heterogeneity in the raw data that reflects the broader conformational ensemble ([Bozovic et al. 2020](https://pubmed.ncbi.nlm.nih.gov/33020277/), [Kuzmanic et al. 2014](https://pubmed.ncbi.nlm.nih.gov/24504120/)). While new algorithms have pushed the field beyond a singular state, they only capture a fraction of the accessible states and are often limited by resolution ([Wankowicz et al. 2024](https://pubmed.ncbi.nlm.nih.gov/38904665/), [Flowers et al. 2025](https://doi.org/10.7554/eLife.103797.3), [Ploscariu et al. 2021](https://pubmed.ncbi.nlm.nih.gov/34726164/)). 

Generative biomolecular structure predictors like AlphaFold 3 ([Abramson et al., 2024](https://www.nature.com/articles/s41586-024-07487-w)), Boltz-1/2 ([Passaro et al., 2025](https://www.biorxiv.org/content/10.1101/2025.06.14.659707v1), [Wohlwend et al., 2025](https://www.biorxiv.org/content/10.1101/2024.11.19.624167v3)), RoseTTAFold 3 ([Corley et al., 2025](https://www.biorxiv.org/content/10.1101/2025.08.14.670328v2)), and Protenix ([Protenix Team, 2026](https://www.biorxiv.org/content/10.64898/2026.02.05.703733v3)) produce remarkably accurate single-state structures. These structure predictors sample from a distribution of conformations learned from data–but largely from the single-state structures they were trained on, implicitly assuming a single protein sequence maps to just one conformation. We have only begun to understand the extent to which these models learn the actual conformational heterogeneity of each protein, or simply memorize the individual protein structures ([Chakravarty et al., 2024](https://www.nature.com/articles/s41467-024-51801-z); [del Alamo et al., 2022](https://elifesciences.org/articles/75751)). 

“Diffusion”-based generative structure predictors work by predicting a series of updates which map from noise to a final protein structure–creating a “trajectory” that can be steered by modifying the updates to better match some criteria–such as how well the model fits experimental data. This “guidance” approach was recently used ([Maddipatla et al., 2026](https://www.biorxiv.org/content/10.64898/2026.02.27.708490v1)) to steer Protenix to identify previously unmodeled states in existing PDB entries. CryoBoltz ([Raghu et al. 2025](http://arxiv.org/abs/2506.04490)) similarly guides Boltz-1 to better model cryoEM density maps when multiple conformations are found during classification of the particle stack. But to date, there have been no systematic explorations of how well different structure predictors respond to guidance, or of the trade-offs involved in applying this guidance to sample ensembles consistent with the experimental data. To simplify and generalize experiments that generate ensemble predictions and use ensemble data, we introduce Sampleworks. 

## **What is Sampleworks?**

Sampleworks is a framework for integrating structural biology observables, structure predictors, and guidance to improve the modeling of conformational ensembles. Sampleworks does this by defining a common interface for structure predictors and linking that interface to methods for computing experimental observables, like an X-ray electron density map. Sampleworks then applies existing methods to guide generative models during inference, steering sample generation towards an ensemble that reflects the data.

To date, we’ve implemented: 

* Two guidance methods: diffusion posterior sampling ([Chung et al., 2024](https://arxiv.org/abs/2209.14687); [Levy et al., 2024](http://arxiv.org/abs/2406.04239)) and Feynman-Kaç steering ([Singhal et al., 2025](http://arxiv.org/abs/2501.06848))  
* Wrappers for [Boltz-1 and \-2](https://github.com/jwohlwend/boltz); [Protenix](https://github.com/bytedance/Protenix); and [RosettaFold3](https://github.com/RosettaCommons/foundry).   
* Guidance based on real-space electron density maps.

We will continue to expand the guidance methods, structure predictors, and the kinds of experimental data used for guidance, and we welcome contributions from this community. You can use Sampleworks, follow our progress, and contribute [here](https://github.com/prism-science/sampleworks)\!

## **Where we're at**

Sampleworks’s first goal is to benchmark the extent to which diffusion-based structure predictors can be guided to generate accurate structural ensembles. Specifically, we ask whether these models can produce out-of-distribution conformations and, when they do, how well those conformations balance between fit to experimental data and geometric quality.

Since these structure predictors' training data were on single state structures, this is a natural test of their ability to generalize. In this first test, we guide the predictors using synthetic electron density maps that mix two conformations. We evaluate how well each predictor recovers the synthetic ensemble while still satisfying protein-geometry constraints.

![6B8X With and Without Guidance](/assets/images/posts/6b8x_w_wo.png)

*(Left) Without guidance, Boltz-2 does not predict the two conformations (grey) in 6B8X when run with multiple random seeds. (Right) Guidance using synthetic density representing the two conformations enables Boltz-2 to predict both.*

We’ve now tested our initial structure predictors with guidance for 40 different structures from the PDB that have known alternate conformations in the original depositions. In the example above, for the protein phosphatase PTP1B (PDB code 6B8X), the predictor, without guidance, falls back on its training data and can only generate structures in one of the two known conformations. Encouragingly, when incorporating guidance with electron density representing both conformations, we observe the structure predictors now predicting two states. However, this is not universally true across different proteins and models. Because Sampleworks is modular and easily accommodates different structure predictors, we can quickly test them all at different guidance levels across a wide range of proteins. 

<div style="display: flex; gap: 10px;">
  <img src="/assets/images/posts/17_tradeoff_conceptual_weak_zoomed.png" alt="Tradeoff Weak" style="width: 50%;" />
  <img src="/assets/images/posts/18_tradeoff_conceptual_strong.png" alt="Tradeoff Strong" style="width: 50%;" />
</div>

*Geometry penalty vs. fit to data for each model’s ensemble prediction on 40 examples of multiple conformations when guided with synthetic density. (Left) Weak guidance, zoomed close to show differences between models. (Right) Strong guidance, resulting in much larger geometry penalties.*

We also assessed the trade-offs between fit to electron-density data and geometry. To determine fit to electron density, we use the Real Space Correlation Coefficient (RSCC). We also compute a conglomerate geometry score, which becomes larger with increased clashes, bad backbone dihedrals, or unrealistic bond lengths. With relatively weak guidance, we can see that the models are all able to improve RSCC without incurring too much cost to protein geometry. Paradoxically, when we use stronger guidance, most structure predictors fall apart completely, and the RSCC gets worse\! This probably means that strong guidance pushes the predictors’ trajectories outside what they’ve been trained on, far enough that they cannot recover. Despite their very similar architectures and training data, these structure predictors differ in how they respond to guidance. 

We are just beginning to learn how best to guide each model to better model biologically relevant ensembles. We are already seeing signs that the models are limited in their current forms, and we will be working to explore and overcome those limitations. In the coming months, we’ll have more to share about the first results shown above and about the experiments in progress now. We’ll be looking to expand the range of predictors and experimental data we can work with, and to engage with the community to make protein conformational ensembles more accessible for everyone. 
