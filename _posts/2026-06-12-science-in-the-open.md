---
layout: single
title: 'Open Development for Biomolecular Ensemble Generation'
author: andybphd
date: 2026-06-12
categories:
  - post
tags:
  - meta
excerpt: "The diffUSE Project releases *sampleworks*, moving beyond open science to science in the open"
comments: true
---

This week we shared DiffUSE's first scholarly publication: [*sampleworks:* *Modular Platform for Experimentally Guided Biomolecular Ensemble Generation*](https://doi.org/10.82153/jkxj-tw08)*.* 

*sampleworks* is an open modular software framework for generating and evaluating biomolecular conformational ensembles from structure predictors guided by experimental data (https://github.com/prism-science/sampleworks/). You can swap in different structure predictors, steering/guidance methods, and loss functions. We welcome community contributions to help strengthen the codebase and expand its applications. Development is already underway by the DiffUSE team and external collaborators to integrate new structure prediction models and guidance from reciprocal-space data.

In this first publication, we use *sampleworks* to examine how well current models recover experimentally determined alternative conformations from the Protein Data Bank. Success varied widely across proteins, suggesting that models may be memorizing rather than learning the true distribution of structural states. 

True to [Astera's open-science ethos](https://zenodo.org/records/17873235), we have developed *sampleworks* in the open. The code has lived in a [public Git repository throughout](https://github.com/prism-science/sampleworks/). Alongside it, we documented progress in real time through blog posts such as "[To ensembles and beyond](https://diffuse.science/posts/sampleworks/)". These provided informal dispatches that shared early thinking and invited community engagement. This is highlighted by the forks the GitHub repository already has. While the blog posts offer speed and accessibility, the scholarly publication is a freestanding, reproducible, citable unit that links all underlying research artifacts to the relevant context and is disseminated with a persistent digital object identifier (DOI). Together, these modes of communication embody open science in practice. Blog posts, open development, and scholarly publication each address a different dimension of scientific communication. Their combination makes the whole greater than the sum of its parts. 

The DiffUSE Project is sharing this first publication on [The Stacks](https://thestacks.org/), an experimental publishing platform currently open to select users, to spark broader public discussion than typically done during closed pre-publication review in traditional scientific journals. The work remains both citable and discoverable, so it will receive a persistent identifier and be indexed in Google Scholar and Open Alex. At this moment, The Stacks is not yet open to external submissions and is hosting work produced internally by [Radial](https://radial.org/) and affiliated organizations.

DiffUSE's vision, a world where we can observe, predict, and act on how proteins move, is not a challenge any single team can tackle alone. By openly developing and sharing data and results, we aim to accelerate the field's progress toward establishing conformational ensembles as its foundational layer. With that foundation, we will greatly improve our understanding of life at the molecular level, accelerating our ability to design therapeutics, engineer enzymes, and predict the functional consequences of mutations.
