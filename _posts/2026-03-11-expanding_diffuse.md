---
title:  Expanding The DiffUSE Project
layout: single
author: stephaniewankowicz
excerpt: Expanding The DiffUSE Project
categories:
  - posts
tags:
  - meta
comments: true
---


Biology is motion. From ecosystems to molecules, nothing is ever still. Life relies on this constant motion to function. Yet we tend to study biology through static snapshots. In structural biology, we often interpret macromolecules as single, static structures. These static structures have been transformative, enabling decades of progress in drug design, disease understanding, and protein engineering. But we are reaching a plateau in the questions we can answer with them. Because proteins do not function as single structures. They function through their conformational ensemble, the range of states a macromolecule can sample. And yet, we have almost no data on these ensembles. The tools to collect and model it at scale do not exist. The infrastructure to share and interpret it has not been built. 

**What could we discover about biology if we had protein ensembles at the scale of the Protein Data Bank?**

*Could we understand how drug efficacy and resistance arise? Could we better explain why mutations cause disease, or what makes a designed enzyme functional? Could we deliberately engineer dynamics to bias cell signaling?*

Today, we are excited to announce that the DiffUSE Project is expanding. We are building the infrastructure to collect and analyze protein ensembles at the scale of the Protein Data Bank. Because many of the most important biological questions can only be answered through ensembles.

The DiffUSE Project, by [Radial, and funded by the Astera Institute](https://radial.org/), began by asking how we could rethink the pipeline for extracting the faint yet information-rich diffuse scattering signal in the "background" of X-ray crystallography experiments. Diffuse scattering may provide key, but often untapped, information on the heterogeneity of macromolecules in a crystal. With funding and operational support from the [Astera Institute](https://astera.org/), we assembled a purpose-built team spanning expertise across Astera and multiple institutions and began to re-engineer the components needed to fully optimize this, revealing structural ensembles.

But diffuse scattering is just one window into protein conformational ensembles. Different techniques uncover different facets of the same underlying ensemble reality. Cryo-EM captures heterogeneity across length scales. NMR resolves timescale-specific motions. SAXS reports on global shape fluctuations. HDX-MS maps solvent accessibility changes. No single method can reveal the full dynamic landscape. But we do not yet know which techniques, or which combination, will best uncover these ensembles. So we start with a not-so-simple question: which data are most fruitful for understanding biology?

But collecting data is only part of the challenge. Every stage of structural biology today reinforces a static worldview. Algorithms model single conformations. Representations emphasize static structures. Metrics evaluate fit to a single model. Biological interpretations are based on static structures. Addressing any piece in isolation will fall short. The entire pipeline must be redesigned. 

The DiffUSE Project is completely rethinking how we collect, process, model, encode, disseminate, and interpret dynamic structural data. We are designing tools to enable downstream applications that meaningfully impact biology. 

<img width="1920" height="1080" alt="Diffuse Project Areas" src="https://github.com/user-attachments/assets/ecb768aa-789b-4b19-8efc-721e72a28cfe" />

At every step, we are guided by the following questions:
  - What structural ensemble data are we missing, and how do we build the technologies to capture it? 
  - Where will structural ensemble data best help reveal biological function? 
  - How do we create tools that empower everyone, not just specialists, to work with conformational ensembles? 
  - How do we openly disseminate what we build to maximize scientific impact?


We are taking this approach because we cannot get there alone. AlphaFold succeeded because decades of experimental structure determination built the data foundation it needed. No equivalent foundation exists for ensembles. Building that foundation and building the prediction methods must happen together — at a scale no single group can achieve. That is why we are not just generating data ourselves. We are building the tools, methods, and infrastructure to enable the entire community to collect, curate, and benchmark dynamic structural data.

This entire project is also a metascience experiment that asks what it truly takes to tackle a large, systematic, and deeply integrated scientific problem. Some of what lies ahead is engineering. Some of it is science. Some of it is community building. We are pursuing this work both internally at Radial and through a growing network of partnerships and collaborations. Experimenting not only with the science itself but with how best to do it.

**What are we building?**

The DiffUSE project will focus on four areas, each advancing a different part of the dynamic structural pipeline simultaneously. Technique focused spokes will transform specialized dynamics techniques into routine, accessible methods. Algorithms will uncover hidden conformational states and integrate signals across techniques to help reveal the full dynamic landscape and provide key integration points for ensemble prediction. Infrastructure will evolve the PDB from a static archive into a living database capable of storing, validating, and querying dynamic structural data. And Biological Impact will ask questions that help ground our technical advance by asking: how does understanding dynamics actually change what we can understand, predict, design, and discover biology? 

**Technique focused spokes:** Every technique for capturing protein ensembles faces its own barriers to making the data truly usable. We are aiming to experiment with how to overcome these barriers and make these techniques routine and accessible for the broader community. Current methods often discard the dynamic signal, and none were designed to scale to the thousands of ensembles needed to uncover general principles. Each spoke tackles these challenges for a specific technique, producing open algorithms, protocols, models, and metrics, all designed from the start to be adopted and built upon by others. We do not yet know which techniques will generate truly additive data, which approaches will scale, or which will result in the best biological insights. We plan to run parallel experiments, and we will follow the evidence, expanding what works, rethinking what doesn't, and sharing what we learn along the way. 


**Algorithms:** No single technique captures the full picture of how a protein moves. Each method sees a different slice of the conformational landscape. To tackle this, we are developing algorithms along three fronts: guidance frameworks that steer ensemble models using experimental data, machine learning approaches that learn directly from experimental measurements rather than structures, and agentic modeling pipelines that autonomously build, evaluate, and refine ensemble models. Everything we build is open, designed for the community to use, extend, and improve. Our first major algorithm is [Sampleworks](https://github.com/prism-science/sampleworks), a platform for testing new guidance frameworks, stress-testing ensemble predictions, understanding where they fail, and establishing the datasets needed to train the next generation of machine learning models on conformational ensembles rather than static snapshots.


**Infrastructure:** The PDB transformed structural biology by providing the community with a shared, standardized, and trusted platform for depositing and retrieving structures. But the PDB was designed for static structures. Without accessible ensemble data, researchers default to inconsistent practices: ignoring the inherent heterogeneity in the data and training models on static structures that don't reflect how proteins actually behave. These limitations don't stay contained; they propagate through the entire discovery workflow, leading to biased biological conclusions.

We are working on evolving the PDB into a living database that supports dynamic structural data through three advances. First, ensemble-aware validation, because today, when an ensemble model is deposited, only part of it is validated against experimental data. Validation metrics are essential for model deposition and for benchmarking new machine learning models. Second, heterogeneity-aware encoding enables queries that let users do things currently impossible: retrieve only ligand-bound states across the database, find entries where a specific loop adopts multiple conformations, or compare ensemble representations across related proteins. Third, a unified, continually updated repository where experimental data serve as ground truth and the models explaining them improve over time as algorithms advance. The endgame is to enable a virtuous cycle where labs deposit dynamic data, the community builds better ensemble models, those models generate new biological insights, and the standardized data fuels structural ensemble prediction.


**Biological Impact:** We want our efforts to be grounded in a simple, but demanding question: how does understanding dynamics change what we can predict, design, and discover? To answer that, we are building ensemble-aware representations to help quantify metrics for what has long been hard to quantify, conformational and solvent entropy, flexibility, and long-range dynamic coupling, and validating them against real biological problems in binding, enzyme design, and allosteric regulation.
But metrics alone aren't enough. We aim to help understand how dynamics propagate and change protein function. How does a single mutation redistribute an entire conformational ensemble and alter functional output? How do changes in hydration networks reshape binding? Can we trace these effects well enough to use dynamics not just as a descriptor, but as a design principle, such as designing allosteric switches by tuning the dynamic landscape rather than the static structure?


**What’s next?**

I am thrilled to be joining the DiffUSE team full-time as Scientific Program Director. In this role, I will design and direct the roadmap to unlock protein ensembles. I will be directly leading the efforts in algorithms, infrastructure, and biology, and guiding technical deep dives. My passion has always been building tools and working with open data. I see this role and this project as an incredible opportunity to deliver on this vision of unlocking protein ensembles at scale. The biology questions I care most about, the role that ensembles and entropy play in protein function, and how we leverage that understanding for design, can only be answered once we commit to an ensemble point of view. That is exactly what the DiffUSE Project intends to do.
We're also growing the [team](https://diffuse.science/work-with-us/) on the algorithms, infrastructure, and biology team, [engaging with those looking to build open tools to make this shift happen](https://diffuse.science/work-with-us/). And we are doing it all in the [open](https://diffuse.science/publications/). 

Our point is this - *break's over*. 

