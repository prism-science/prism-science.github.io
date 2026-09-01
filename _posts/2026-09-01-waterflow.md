---
title: 'WaterFlow: Predicting Ordered Water Molecule Positions on Protein Structures'
layout: single
author: srivastava-vratin
date: 2026-09-01
classes: wide
categories:
  - posts
tags:
  - water
  - machine learning
  - crystallography
excerpt: "A flow-matching model for predicting ordered water positions on protein structures, and what it reveals about the limits of the data we train it on."
comments: true
---

Water mediates folding and stability of protein structure, bridges ligands to their receptors, and participates directly in catalysis. Interpreting a protein structure in light of its function, or designing a new one, depends on where the waters are. The accuracy needed is demanding too, since hydrogen-bond energies are sensitive to distance: half an angstrom of error changes the interpretation of a water network, and with it any estimate of binding affinity or catalytic geometry that rests on it.

![WaterFlow in one pass: the trained vector field transports prior samples onto candidate sites, the confidence model scores them, and clustering leaves a ranked, discrete set of waters.](/assets/images/posts/2026-09-01/wf_graphical_abstract.png){: .align-center}

*WaterFlow in one pass: Flow ODE integration carries a sampled prior onto candidate water sites; the confidence model scores each candidate, and clustering leaves a ranked, discrete set of kept waters.*

Predicting accurate coordinates for ordered water remains a challenging, unsolved problem. Static structure prediction is close to experimental accuracy, and protein-ligand cofolding is improving quickly, but neither models solvent, so the models return a dry protein. Most water placement is instead physics-based, grounded in molecular dynamics and solvation thermodynamics ([Nguyen et al., 2012](https://doi.org/10.1063/1.4733951)), which is slow and only as accurate as the force field and solvent model underneath. Deep learning and data-driven methods such as GalaxyWater-CNN ([Park & Seok, 2022](https://doi.org/10.1021/acs.jcim.2c00306)), HydraProt ([Zamanos et al., 2024](https://doi.org/10.1021/acs.jcim.3c01559)), and most recently SuperWater ([Kuang et al., 2025](https://doi.org/10.1038/s42004-025-01789-4)) showed a learned model can beat physics-based coverage, but precision and recall trade off steeply: SuperWater recovers only around 27% of deposited waters at high precision, as claimed in their paper.

Our new preprint introduces [WaterFlow](https://doi.org/10.64898/2026.08.26.747373), which outperforms SuperWater at every operating point. We also analyze how much of this gain, and the gap to ideal prediction, lies in the quality of the model itself versus the quality of the data used to train these models.

## What is WaterFlow?

WaterFlow takes a protein structure and returns the same structure with ordered waters added. A **generator**, trained with flow matching ([Lipman et al., 2022](https://arxiv.org/abs/2210.02747)), learns a velocity field that transports points sampled from a prior distribution around the protein onto the water positions observed in crystal structures; at inference, integrating that field yields candidate waters. A **confidence model** then scores each candidate, low-scoring ones are removed, and nearby survivors are merged, leaving a ranked list of waters with confidence scores. Both stages are parametrized by the same equivariant graph neural network ([Jing et al., 2021](https://arxiv.org/abs/2106.03843)), trained on ~67,000 structures from [PDB-REDO](https://pdb-redo.eu/).


![Integrating the learned velocity field carries prior samples onto ordered-water positions.](/assets/images/posts/2026-09-01/wf_inference.gif){: .align-center}

*Integrating the learned velocity field carries prior samples onto ordered-water positions.*

Re-trained on identical sequence- and structure-clustered splits and scored on the same 698-structure holdout, SuperWater reaches a parity F1 of 0.41 at a 1.0 Å acceptance radius; WaterFlow reaches 0.63, and the gap widens at 0.5 Å (0.54 against 0.26). The largest gains are at sub-angstrom localization, the regime that matters for binding free energies and hydrogen-bond geometry.

![Precision-recall on the 698-structure holdout, at 0.5 Å and 1.0 Å acceptance radius, and F1 at 1.0 Å at parity.](/assets/images/posts/2026-09-01/wf_benchmark.png){: .align-center}

*Precision-recall on the 698-structure holdout. WaterFlow outperforms the re-trained SuperWater at every confidence threshold, at both 0.5 Å and 1.0 Å, and reaches an F1 of 63.4% at 1.0 Å at parity versus 40.7% for SuperWater.*

## Crystallographic symmetry matters

Many surface waters are coordinated by atoms from symmetry-related copies of the protein in the crystal lattice, so a model that sees only the asymmetric unit sees an incomplete coordination environment. WaterFlow expands the crystal symmetry and adds residues within 8 Å of the asymmetric unit as context nodes in its graph.

![Left: one bridging water seen from the asymmetric unit alone versus with its symmetry neighbors present. Right: the recall gain from adding symmetry mates is concentrated within hydrogen-bonding range.](/assets/images/posts/2026-09-01/wf_symmetry_mates.png){: .align-center}

*Left: one water, seen from the asymmetric unit alone and with its symmetry neighbors. Right: the recall gain from adding symmetry mates is confined to waters within hydrogen-bonding range of a symmetry mate.*

This raises F1 at parity from 0.57 to 0.63, and the gain is concentrated in the ~10% of waters within hydrogen-bonding range of the lattice, where recall jumps from 0.29 to 0.60. We see this phenomenon emphasized with one bridging water, which scores 0.004 from the asymmetric unit alone, and 0.71 with its symmetry neighbors present. Almost no other structure prediction method encodes this crystallographic information, and the argument extends well past water: proteins, ligands, and ions also form contacts across symmetry-related interfaces.

## Deposited waters are not ground truth

Which waters get modeled into a deposited structure depends on resolution, refinement protocol, and the choices of the crystallographer ([Fraser & Murcko, 2024](https://doi.org/10.1016/j.cell.2024.01.003)), so two crystals of the same protein rarely agree about their solvent. Clustering deposited waters across large sets of isomorphous structures (lysozyme, endothiapepsin, carbonic anhydrase), we find 13-30% of modeled waters are not reproduced in the other structures of the same protein. Treating the consensus positions as ground truth, the best achievable F1 is 0.87-0.94, a ceiling for any model trained and scored against deposited coordinates, ours included. Consistent with that, filtering low-quality waters out of training did not improve the model; rather, more distinct, high-quality structures were more efficient at reaching the same performance.

## Do the predicted waters fit the experimental data?

The more direct test of a predicted water is the experimental density. Measured by EDIA ([Meyder et al., 2017](https://doi.org/10.1021/acs.jcim.7b00391)), predicted waters fit real-space density as well as deposited ones at a confidence threshold of 0.7, and better above it. Novel predictions, those with no deposited water within 1.0 Å, are nominally false positives, but sit on positive mFo-DFc difference density: the fraction above +3σ grows from 11% to 49% with confidence. A significant share of the apparent false positives are therefore waters the deposition omitted.

The predictions also hold up under re-refinement. Re-refining PDB 4RKW with predicted waters lands R-free within 0.012 of the deposited control, and on an apo/ATP-bound pair of LuxO, the model places the two waters bridging ATP to the protein within 0.1 Å of their deposited positions and leaves the ligand-displaced sites empty. These results bring predicted waters within reach of ligand binding analysis, protein design, and automated model building.

## Using WaterFlow

Model setup and prediction commands are in the [README](https://github.com/diff-use/WaterFlow). Two selection methods control how many waters are returned. The default is a **confidence threshold**: every water scoring above the cutoff is kept. The confidence score reflects local disorder, so the model predicts more waters for well-ordered structures and fewer for poorly ordered ones, and the predicted counts fall with resolution much like deposited counts do. Raising the threshold keeps fewer waters with stronger density support; at high thresholds the retained waters are better supported than the deposited ones. A high threshold is appropriate when individual waters matter, for example in QM/MM calculations or as refinement restraints. The second method, **density selection**, sets the water count from the protein size instead of the confidence score. This is useful for comparing hydration across structures of different quality, and on predicted structures, where errors in the input coordinates lower the confidence scores and a threshold would return too few waters.

WaterFlow is trained on static coordinates, while the experimental data average over heterogeneous protein and solvent, so many of the waters it learns from are partially occupied. Getting past that requires training data with partial occupancies and alternative conformers. WaterFlow paired with an experimentally guided ensemble framework like [sampleworks](/posts/sampleworks/), is one future route to generating it. In the meantime, you can use WaterFlow, follow our progress, and contribute [here](https://github.com/diff-use/WaterFlow).
