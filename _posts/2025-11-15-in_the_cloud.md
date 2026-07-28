---
layout: single
title: 'In the Cloud'
author: mewall
date: 2025-11-15
classes: wide
categories:
  - post
tags:
  - diffuse scattering
  - molecular dynamics
  - clouds
  - planning
  - open science
  - meta
gallery:
    - url: /assets/images/posts/Clouds.jpg
      image_path: /assets/images/posts/Clouds.jpg
      alt: "Cloudy diffuse features in the sky"
      title: "Cloudy diffuse features in the sky"
    - url: /assets/images/posts/DiffuseClouds.png
      image_path: /assets/images/posts/DiffuseClouds.png
      alt: "MD simulation of cloudy diffuse features"
      title: "MD simulation of cloudy diffuse features"
excerpt: >
  Next steps in diffUSE MD simulations
comments: true
---


{% include gallery caption="(Left) Cloudy diffuse features in the sky. (Right) MD simulation of cloudy diffuse features." %}

## Diffuse Scattering in the Cloud 

While out on a walk, as I looked up at the sky, a certain cloud formation (above left) reminded me of the *l* = 0 slice through the MD simulation of Mac1 diffuse scattering (above right). That got me thinking about the next steps for the diffUSE MD simulations (which are, of course, being performed using [cloud computing resources](https://www.voltagepark.com)).

As described in the [Quarterly All Hands Meeting]({% post_url 2025-11-10-allhands %}) post, we recently shared our short-term plans for the various components of the diffUSE project. We've already performed baseline comparisons of crystalline MD simulations of Nsp3 macrodomain (Mac1) to diffuse scattering data (see the [3-2-1 Contact]({% post_url 2025-10-20-3-2-1-contact %}) post). Now we want to improve the models and see what happens in the simulations when we make changes. With this in mind, we're planning to: (1) improve the current MD model of Mac1; (2) simulate Mac1 crystals under different conditions; and (3) develop a model of a new system.

Thinking about (2), I contacted James Fraser to chat about what to do for the next MD simulations of Mac1. We decided to look at Mac1 in complex with ADP-ribose. This choice is timely, as Kara Zielinski just collected diffUSE diffraction data from crystals of this complex at the Cornell High-Energy Synchrotron Source (CHESS), during a recent trip from UCSF to Nozomi Ando’s lab at the Cornell. 

What will the MD simulation of diffuse scattering from crystals of Mac1 in complex with ADPr look like? Probably a lot like the ones we've done already, with some small changes. We're planning to analyze the differences and find out what happens to the dynamics when different ligands bind. But we don't really know yet what we'll see. These moments of suspense are very common in science, but they're absent from the stories we usually tell in the literature. The open science model we're using on the diffUSE project enables us to document these periods of uncertainty as a part of the public narrative of the project. It feels kind of liberating.

---
