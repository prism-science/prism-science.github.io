---
title: 'qFitLatent: Learning the Motions of Multiconformers'
layout: single
author: alanclayrichard
date: 2026-09-01
classes: wide
categories:
  - posts
tags:
  - machine learning
  - protein dynamics
  - crystallography
excerpt: "Learning a latent representation of qFit multiconformers to capture the local dynamics that crystallography usually discards."
comments: true
---

Modeling proteins in the true manner in which they occur is a grand challenge of the biological puzzle, and protein dynamics is an essential piece of it. To better account for local dynamic motions that are captured but typically discarded in crystallography, an algorithm called qFit refits atomic models of proteins into underexplored regions of electron density. The resulting multiconformer protein models represent a more complete picture of the intricate fluctuations that allow proteins to function. Transforming these multiconformer models into a latent representation would enable the use of a unique dynamics modality for downstream representation learning and structural biology projects.

qFitLatent seeks to learn a latent vector that is capable of producing the qFit multiconformers with fidelity to the side chain ensembles. Fundamentally, by treating the multiconformers as the ground truth, a distribution of side chain conformations arises out of the atomic positions, occupancies, and B-factors. These experimental representations lend themselves naturally to a Gaussian mixture of states, where each side chain rotamer is treated as a single state with probability and variance. This Gaussian mixture can then be mapped directly to the input multiconformers, and the two distributions can be compared.

To learn a representation capable of recapitulating the side chain ensembles, we adopt an invariant point attention backbone to operate on sequence embeddings, such that the model has knowledge of the amino acid identities and the relevant structural biology driving local dynamics. We are experimenting with multiple formulations of the model, including a generative version conditioned on sequence and backbone only, as well as a variational autoencoder that masks residues/regions and reconstructs them from the latent vectors. The goal of this project is to craft a latent manifold that practically models the multiconformers created by unused density. An accurate representation of local dynamics through the lens of multiconformers unlocks an untapped but complementary dynamics representation: another piece of the puzzle.

![qFitLatent reconstruction of side chain multiconformers in a validation protein not seen during training. The rotamer of the ground truth (qFit, purple) central valine is correctly predicted by the model (qFitLatent, salmon).](/assets/images/posts/2026-09-01/qfitlatent_validation.gif){: .align-center width="360"}

*Figure 1. qFitLatent reconstruction of side chain multiconformers in a validation protein not seen during training. The rotamer of the ground truth (qFit, purple) central valine is correctly predicted by the model (qFitLatent, salmon).*

Check out the code [here](https://github.com/diff-use/qFitLatent).
