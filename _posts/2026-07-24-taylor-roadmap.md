---
title:  Is it all just the lattice?
layout: single
author: twomack
excerpt: Taylor's update on his work in the diffUSE project and the roadmap to a complete forward model of diffuse scattering.
categories:
  - posts
tags:
  - meta
comments: true
---

## Towards a complete forward model of diffuse scattering

Even when crystallized, proteins move. But each copy in the thousands of unit cells don't all move the same way. Therefore, a protein crystal is in essence a spatial sampling of the thermodynamic ensemble of a protein (within the lattice). These varied internal motions within each unit cell have been identified as a major contribution to the diffuse X-ray scattering intensity. Diffuse scatter is caused by variance in the structure factors between every unit cell in a crystal. X-ray crystallography has therefore always had the potential to detect correlated intraprotein motions, if only we can learn how to interpret the diffuse signal properly[^1]. These correlated motions are likely to underlie many biologically relevant movements.

This is the challenge that the diffUSE team has been working on for the past year, but there's a big complication: internal protein motions aren't the only contribution to the diffuse scattering signal, and they likely aren't even the majority component[^2]. Lattice vibrations known as phonons (basically sound waves) move throughout the crystal lattice and cause long-range disorder that is picked up in the diffuse signal. We can think of these vibrational modes as whole proteins fluctuating around their average positions. Since this disorder is long-range and the vibrations are due to motions of entire unit cells, this type of diffuse scattering mostly shows up as extra intensity concentrated around Bragg peaks, dubbing this feature's name: halos.

Before we can get to interpreting the signal from the (interesting) internal protein motions, we'd like to isolate this vibrational lattice signal. A great way to remove a signal you're not interested in is to have a forward model that generates exactly what that signal is, then simply subtract it. This is exactly what the GOODVIBES lattice dynamics simulator developed by Steve Meisburger, David Case, and Nozomi Ando does[^3]. In earlier studies on hen egg-white lysozyme crystals[^2][^3], these halo features were effectively simulated by rigid-body elastic network models. Residues, domains, or entire protein molecules were treated as stiff objects where a force (or torque!) applied to one atom causes the whole object to move. These rigid bodies are coupled at contact points by springs and vibrate around their equilibria according to two refineable energy potentials:

$$
V^{(\text{Gauss.})}_{ij}=\frac{1}{2}k^\text{G}_{ij}\left|\mathbf{u}_i-\mathbf{u}_j\right|^2
$$


$$
V^{(\text{dir.})}_{ij}=\frac{1}{2}k^\text{d}_{ij}\left((\mathbf{u}_i-\mathbf{u}_j)\cdot\hat{\mathbf{r}}_{ij}\right)^2
$$

where $i$ and $j$ are the indices of the coupled atoms, $\mathbf{u}$ is the displacement vector of an atom from its equilibrium position, the $k_{ij}$s are the respective refineable spring constants between atoms $i$ and $j$, and $\hat{\mathbf{r}}_{ij}$ is the unit vector pointing from atom $i$'s equilibrium position to $j$'s. In this case the complete potential energy of the system is 

$$
V=\sum_{i<j}\left(V^{(\text{Gauss.})}_{ij}+V^{(\text{dir.})}_{ij}\right).
$$

In the harmonic approximation, and for dimensional indices $l\in\lbrace x,y,z\rbrace$, forces on the $i^{\text{th}}$ atom in the $l$ direction due to displacement of the $j^{\text{th}}$ atom along the $l'$ direction are described as 

$$
F_{ij}^{ll{'}}=-\frac{\partial^2V}{\partial u_i^l\partial u_j^{l{'}}}.
$$

Rigid body vibrations can be turned into scattering factors through the one-phonon approximation for thermal diffuse scattering[^4]. Continued improvements to the GOODVIBES model will not only help isolate unwanted lattice vibrations, but may also help describe biologically important domain movements that are well-approximated by rigid bodies (e.g. catalytically-relevant hinge-bending). This work will be continued by the diffUSE East team especially by the Ando Lab's new postdoctoral scholar, Stephen Thornton.

Our ultimate goal is a forward model of the complete diffuse scattering map --- containing features arising from both rigid-body motions and short-ranged atomistic ones. Molecular dynamics (MD) simulations are still the best tool we have to assess conformational flexibility at the atomic scale, and Mike Wall has developed a structure factor calculation script `xtraj.py` in the *Lunus* package (<https://www.github.com/lanl/lunus>) which generates both F_calcs and diffuse intensities from MD trajectories. MD combined with xtraj is currently the best forward model we have for generating diffuse scatter associated with protein internal motions, and the isotropic component of the diffuse signal has been well-characterized using it[^5]. However, MD runs are far too computationally expensive to simulate an entire protein crystal. Therefore, MD diffuse maps are missing lattice vibrational features as discussed above, yet they probably aren't missing all of them. When performing MD simulations of crystals, we need a supercell of several unit cells in order to avoid autocorrelation artifacts. Even in the minimally viable 2x2x2 system, we have a portion of the extended crystal lattice which introduces vibrational elements. To what extent MD recapitulates vibrational features is an open question, and the first system we are using to tackle this question is a 5x5x5 supercell of triclinic lysozyme (6O2H, Figure 1).

![5x5x5 supercell of triclinic lysozyme 6O2H](/assets/images/posts/2026-07-24/6O2H_5x5x5.png "Figure 1")
*Figure 1: (Left) HEW lysozyme 6O2H structure. (Right) Our solvated and equilibrated 5x5x5 triclinic crystal built from 6O2H. This system was used as the basis for production simulations of both restrained and unrestrained dynamics.*

So far, I've simulated this system over 1μs, calculated the relevant structure factors using `xtraj.py`, and generated total scattering diffraction series (Bragg + diffuse) using James Holton's nanoBragg diffraction plotter (Figure 2). I'm working on processing these simulated datasets using the mdx2 diffuse scatter processing pipeline in an attempt to replicate the workflow that we use for experimental data[^6]. After that, I plan to fit my simulated diffuse map to a GOODVIBES elastic network model to see which halo features are present. The overall questions I am trying to answer are:

1. How can we generate accurate total scattering from crystal dynamics simulations and correctly compare it to experimental data?
2. What methods most effectively deconvolve lattice dynamics from internal motions?

![Simulated diffraction image from 6O2H MD trajectory](/assets/images/posts/2026-07-24/6O2H_nB_res-un.jpg "Figure 2")
*Figure 2: Total scattering diffraction images generated from MD trajectories of the 5x5x5 6O2H crystal using nanoBragg. (Left) Image from a restrained MD run in which the protein's heavy atoms were harmonically restrained to their crystallographic coordinates. The Bragg lattice is unrealistically strong and minimal diffuse scatter is observed. (Right) Image from an unrestrained run. The Bragg lattice is weaker and diffuse scatter is evident. It's possible that targeted restraints and tuning of the well-strength are an avenue to isolating specific motions in the crystal.*

If we can identify which vibrations occur in MD, there may be a way to bias the simulation to remove those features while leaving the internal motions unbiased, thus enabling us to simulate a complete diffuse map with MD internal motions and fully realized lattice vibrations from GOODVIBES. Or perhaps constituting the complete diffuse map will be as simple as subtracting out the incomplete vibrational features from MD and adding in the complete ones from a GOODVIBES simulation. These speculations have yet to be clarified, and I am open to feedback and suggestions!

If we can develop an accurate forward model for all the major features of a protein crystal's diffuse scattering map, we will not only have advanced the study of dynamic structural biology on a theoretical level --- we will also enable machine learning and AI tools to use diffuse maps to distinguish between ensembles that produce identical dynamically averaged Bragg data. Tools like the [*sampleworks*](https://thestacks.org/publications/sampleworks-release) platform pioneered by the modeling team within diffUSE. Suffice it to say, diffuse scattering is indeed *not* merely due to lattice vibrations, but the lattice signal is significant and cannot be ignored; my contribution to the diffUSE project begins with moving us towards developing such a complete forward model.

[^1]: Welberry, T. R., & Weber, T. (2016). One hundred years of diffuse scattering. *Crystallography Reviews*, 22(1), 2–78. https://doi.org/10.1080/0889311X.2015.1046853
[^2]: Meisburger, S.P., Case, D.A. & Ando, N. Diffuse X-ray scattering from correlated motions in a protein crystal. *Nat Commun* 11, 1271 (2020). https://doi.org/10.1038/s41467-020-14933-6
[^3]: Meisburger, S.P., Case, D.A. & Ando, N. Robust total X-ray scattering workflow to study correlated motion of proteins in crystals. *Nat Commun* 14, 1228 (2023). https://doi.org/10.1038/s41467-023-36734-3
[^4]: Willis, B. T. M. (2010). Thermal diffuse scattering of X-rays and neutrons. In *International Tables for Crystallography*, Vol. B, ch. 4.1, pp. 484–491. https://doi.org/10.1107/97809553602060000773
[^5]: Wych, D. C. and Wall, M. E. (2023). Molecular-dynamics simulations of macromolecular diffraction, part II: Analysis of protein crystal simulations. In N. Ando (Ed.), *Methods in Enzymology*, Vol. 688, pp. 115–143. Academic Press. https://doi.org/10.1016/bs.mie.2023.06.012
[^6]: Meisburger, S. P. and Ando, N. (2023). Processing macromolecular diffuse scattering data. In N. Ando (Ed.), *Methods in Enzymology*, Vol. 688, pp. 43–86. Academic Press. https://doi.org/10.1016/bs.mie.2023.06.010
