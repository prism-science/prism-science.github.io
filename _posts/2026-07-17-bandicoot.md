---
layout: single
title: 'BANDICOOT: Coot 0.9 That Runs on MacOS Tahoe'
author: lyubimov-art
date: 2026-07-17
classes: wide
categories:
  - post
tags:
  - coot
  - molecular modeling
  - macos
gallery1:
    - url: /assets/images/posts/2026-07-17/bandicoot_screenshot.png
      image_path: /assets/images/posts/2026-07-17/bandicoot_screenshot.png
      title: "Bandicoot 0.1.4.8 running on MacOS Tahoe"
excerpt: "Reviving Coot 0.9 for MacOS Tahoe as Bandicoot, a bespoke and integrated molecular modeling environment."
comments: true
---

The Crystallographic Object-Oriented Tool (Coot) is the pre-eminent molecular modeling environment, used by structural biologists worldwide for the past twenty years. Developed by Paul Emsley of the MRC Laboratory of Molecular Biology in Cambridge, Coot revolutionized molecular modeling by introducing real-space refinement, integration with other software (e.g. Phenix and Refmac5), and a highly modifiable Python-based environment. With these changes, Paul made model building, a skill that used to require months and years of practice, intuitive and quick, in turn rapidly accelerating the pace of structural biology itself. To this day I remember Paul's presentation of Coot at the 2005 American Crystallographic Association meeting, which elicited an audible gasp as the audience saw an ADP molecule crawl like a lizard and automatically pop into electron density.

In recent years, Coot underwent an extensive rebuild, with the user interface, model rendering, and under-the-hood libraries receiving extensive upgrades and often redesigned and rebuilt in their entirety. The necessity for such a major upgrade became apparent when MacOS 26.x (Tahoe) was released with major changes to graphics, rendering Coot < 1 completely unusable within this operating system. This problem affected not just the immediate predecessor to Coot 1 (version 0.9.8.95), but all of Coot < 1 versions.

With Coot 1 running perfectly well on MacOS Tahoe, it would seem that time has come to bid adieu to all the preceding versions. However, Coot 1 development remains in relatively early stages, which, unfortunately, makes it incompatible with third-party software that used to be integrated with earlier versions. In other words, many users were not yet ready to let go of Coot 0.9, and some (e.g. panDDA users) were still reliant on Coot 0.8. There was a clear need to bring back the old Coot. Modifying Coot 0.9 binaries did not solve the problem and neither did re-compiling Coot 0.9 on MacOS Tahoe from source code. It quickly became apparent that Coot 0.9 could only come back to MacOS with major modifications.

With a heavy assist from Claude Code, I took on this challenge. Very quickly I discovered why Coot 1 had to be built from the ground up: Coot 0.9 was reliant on many extremely old libraries, some deprecated, others only available if built from source code. Quite a few features had to be completely re-done to make them work. The many required modifications include but are not limited to rebuilding all the toolbars, converting many UI elements from Python 2 to C++, changing how text labels were displayed, and making adjustments to atom picking. Later on, new functionality was added, such as built-in support for pandda.inspect and ligand generation from SMILES strings. The changes were extensive enough that it became clear that we could not call this new program "Coot" anymore. Thus, this MacOS-capable molecular modeling environment was renamed the Bespoke AND Integrated Crystallographic Object-Oriented Tool, or Bandicoot.

{% include gallery id="gallery1" caption="Bandicoot 0.1.4.8 running on MacOS Tahoe." %}

Bandicoot, same as Coot, is an open-source project. Source code and binary releases are available for download from the public repository at [https://github.com/fraser-lab/bandicoot](https://github.com/fraser-lab/bandicoot). Currently, Bandicoot runs on only on MacOS (tested on Tahoe but runnable on previous MacOS versions as well). It's a work in progress and thus is a bit rough around the edges. Users are encouraged to report any issues and submit pull requests.
