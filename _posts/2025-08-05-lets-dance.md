---
title: Let's dance!
layout: single
author: mewall
excerpt: Molecular-dynamics simulations of diffuse scattering
categories:
  - post
tags:
  - meta
gallery:
    - url: /assets/movies/posts/20250805_Mac1_MD.gif
      image_path: /assets/movies/posts/20250805_Mac1_MD.gif
      alt: "Visualization of Mac1 MD trajectory"
      title: "Visualization of Mac1 MD trajectory"
    - url: /assets/images/posts/20250805_Mac1_Bragg.jpg
      image_path: /assets/images/posts/20250805_Mac1_Bragg.jpg
      alt: "Electron density from simulated Bragg at 1-sigma"
      title: "Electron density from simulated Bragg at 1-sigma"
    - url: /assets/images/posts/20250805_Mac1_diffuse.png
      image_path: /assets/images/posts/20250805_Mac1_diffuse.png
      alt: "Slice through the simulated diffuse map"
      title: "Slice through the simulated diffuse map"
comments: true
---


{% include gallery caption="First diffUSE MD simulations of diffraction. (Left) Visualization of the MD trajectory. (Center) Electron density from simulated Bragg data at 1\-sigma (yellow) overlaid with experimental 2FoFc (blue). (Right) Slice through the computed diffuse scattering map." %}

We want to know all about how proteins "dance" in the crystal. In addition to having their own individual moves (see the [DaVinci Dude Dance]({% post_url 2025-07-29-davinci %}) post), different proteins can't occupy the same space at the same time, and sense and respond to their neighbors, even at a distance. 

Molecular-dynamics simulations give us a picture of the whole choreography. Starting with the crystal structure, our simulations evolve using assumptions about the underlying physics. The motions appear random but follow patterns that show up in the diffraction. Right now researchers can make molecular-dynamics simulations agree reasonably well with the diffraction data, but the agreement isn't perfect. In particular, so far the simulations haven't done a very good job of modeling both the Bragg and diffuse data simultaneously.

We're working to fix this problem.

Our first simulations are especially important, as they'll serve as a reference to assess our progress. Inspired by the project's first experiments during the diffUSE kickoff meeting (see [Getting our feet wet]({% post_url 2025-07-30-wetfeet %}) post), we're performing simulations of SARS-Cov-2 Nsp3 macrodomain, the subject of a beautiful [neutron crystallography study](https://pmc.ncbi.nlm.nih.gov/articles/PMC9140965/) done in the Fraser lab. 


Above is a first look at the initial results. In the movie, the waters look like swarming gnats, the ions are balls, and the proteins are cartoon ribbons. The proteins wave around and also jostle their neighbors. Waters and ions diffuse and sometimes stick to the protein for a while. 

The simulated electron density in the center panel shows the average picture. It doesn't give us information about how atoms move together, but diffuse scattering does (right panel). Combining both will enable us to develop more accurate MD models of protein crystals.

*Methods*

The [lunus](http://github.com.lanl/lunus) repository has some examples of how to [prepare](https://github.com/lanl/lunus/tree/master/examples/tutorials/crystalline_MD_prep) crystalline MD simulations and use them to analyze [Bragg](https://github.com/lanl/lunus/tree/master/examples/tutorials/crystalline_MD_analysis_bragg) and [diffuse](https://github.com/lanl/lunus/tree/master/examples/tutorials/crystalline_MD_analysis_diffuse) data. 
