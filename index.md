---
layout: term
title: brandon's website
cmd: cat about.md
---

# Brandon L. Barker, PhD

Welcome to homepage of Brandon L. Barker, PhD -- the best stop on the information superhighway!
My current state:

- Metropolis Postdoctoral Fellow
- Computing and Artificial Intelligence Division
- Computational Physics and Methods Group (CAI-2)
- Center for Theoretical Astrophysics
- Los Alamos National Laboratory
- PhD, Astronomy and Astrophysics and Computational Mathematics, Sciences, and Engineering

Here you can find out more [about me](#about-me) and my [research](#research), [resources](resources) I
have produced, [code](#code) I have worked on, and more.

* * *

## About Me
I am a computational (astro)physicist focused on multi-physics, multi-scale 
modeling of high energy density plasmas. As an astrophysicist my work centers
around understanding the origins of high-energy astrophysical transients --
primarily supernovae and kilonovae.
I am greatly interested in the development and 
implementation of high-order accurate numerical methods in these contexts.
I am passionate about the development and support of open source community codes.

Currently, I am a Metropolis computational physics postdoctoral 
fellow at Los Alamos National Laboratory in the Computational Physics 
and Methods group.
My work now focuses on the development of novel multiphysics algorithms to support 
a wide range of applications from high energy astrophysics to terrestrial 
experimental design.
Broadly, I am interested in numerical relativity, 
numerical methods, multi-physics problems, and the development of open-source scientific software. 

Previously I was a NSF Graduate Research Fellow at Michigan State University working with Sean Couch. 
My work PhD involved high-fidelity modeling of core-collapse supernovae and connecting neutrino-driven 
models to observations.
 
Outside of work, I enjoy backpacking, kayaking, nature photography, cooking, 
perfecting my coffee brew, and writing less useful software.

* * *

## Research
As a computational physicist, my professional time is spent developing, 
implementing, and deploying numerical methods focusing on multiscale problems 
in physics and astronomy. I strive to create computational 
models that are more accurate, efficient, and portable.  

In astrophysics, my interests center around nucleosynthesis sites -- 
especially core-collapse supernovae -- to understand the origins of the 
periodic table. Core-collapse supernovae are some of the most interesting 
events in the universe (though I may be biased on this!). 
They contain a wealth of fundamental physics and allow us to probe environments 
far grander than those accessible to Terrestrial labs in order to understand 
how matter behaves in the most extreme environments. They are responsible 
for the synthesis of many of the elements and drive the evolution of galaxies. 
Understanding these phenomena requires a partnership of observational, 
theoretical, and numerical efforts. My work lies in the theoretical study of 
these events using the most advanced computers available and the 
exploration of how to use modern theory to understand observations. 
I develop open source scientific software 
to model the central engines of these phenomena and explore how, 
through modern numerical methods and software design, we can improve these models.

* * *

## Code

Software is a key piece of the scientific infrastructure. 
By open sourcing software, it may become a tool for the community. 
My primary passion is the development of open-source community codes 
to drive science forward.
The software listed here is a sample of the codes that I have developed.
Also see my [GitHub](https://github.com/astrobarker).

+ **[Athelas][athelas]: A modern transient code**

  `Athelas` is an in-development radiation hydrodynamics code for simulating 
  core-collapse supernovae and creating synthetic light curves. It is built upon 
  conservative, high-order discontinuous Galerkin methods. It supports stellar
  profiles from the MESA stellar evolution code and is nearing production
  capability.

+ **[Phoebus][phoebus]: Performance Portable GRRMHD**

  `Phoebus` is a general relativistic neutrino radiation magnetohydrodynamics code built on the adaptive mesh refinement library `Parthenon`. 
  It supports a general equation of state, several radiation transport algorithms, and analytic and prescribed metrics.
  See the [paper][phoebus-paper]!

+ **[Parthenon][parthenon]: Performance Portable Block-Based Adaptive Mesh Refinement**

  `Parthenon` is a block-structured adaptive mesh refinement library. It is built on [Kokkos], the hardware-agnostic library for on-node parallelism, 
  to provide performance-portable, distributed, adaptive mesh refinement for downstream applications.

+ **[Singularity-eos][singularity-eos]: A Performance Portable Equation of State Library**

  `Singularity-eos` is a performance-portable equation of state library. It leverages on-node parallelism on heterogeneous architectures. 
  At present, Singularity-eos supports over ten equations of state for both terrestrial and astrophysical applications.
  See the [paper][singularity-eos-paper]!

+ **[thornado][thornado]: Discontinuous Galerkin Methods for Supernovae**

  `Thornado` is a neutrino radiation hydrodynamics code built on high-order discontinuous Galerkin methods. 
  It leverages the adaptive mesh refinement library [AMReX](https://amrex-codes.github.io/amrex/) and supports a general equation of state.

+ **[sordine][sordine]: A Hydro Code Verification Suite**

  `sordine` is a (rad-)hydro code verification suite that I am expanding as needed. It includes, specifically, 
  self-similar solutions for Sedov-Taylor blast waves of all families.

+ **[mplcolors][mplcolors]: A Command Line and Python Package Tool for Color Exploration**

  `mplcolors` is a command line and Python 3.x package tool for color exploration. 
  It supports displaying matplotlib colors and colorbars, as well as color complements, triads, and tetrads, in the command line. 
  The same utilities are available as an importable package.

[athelas]: https://github.com/athelas-astro/athelas
[phoebus]: https://github.com/lanl/phoebus
[phoebus-paper]: https://ui.adsabs.harvard.edu/abs/2024arXiv241009146B/abstract
[parthenon]: https://github.com/parthenon-hpc-lab/parthenon
[singularity-eos]: https://github.com/lanl/singularity-eos
[singularity-eos-paper]: https://doi.org/10.21105/joss.06805 
[thornado]: https://github.com/endeve/thornado
[sordine]: https://github.com/astrobarker/sistrum
[mplcolors]: https://github.com/astrobarker/mplcolors
[kokkos]: https://github.com/kokkos/kokkos

* * *

## Resources
My success, however defined, has only been possible because of the support provided to me.
Whenever possible, I try to share my [resources](resources) for others to benefit from.

* * *

## Outreach

Throughout my career I have worked to maintain an involvement in my community. 
This has made for some of the most enriching moments of my education. 
Find out about the [outreach initiatives](outreach) I have been involved in!

* * *

## Elsewhere

A few other corners of the Internet where you can find me include:

+ code on <a class = "dir" href="https://github.com/astrobarker">github</a>
+ posts on <a class = "dir" href = "https://twitter.com/astrobarker">twitter</a>
  and on <a class = "dir" href = "https://bsky.app/profile/astrobarker.bsky.social">Bluesky</a>
+ professionally can be found on <a class = "dir" href = "https://www.linkedin.com/in/brandon-barker-551426116/">LinkedIn</a>

### Contact

+ e-mail: [barker@lanl.gov](mailto:barker@lanl.gov)

* * *
