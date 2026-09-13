---
layout: term
title: brandon's website
cmd: cat index.md
---

# Brandon L. Barker, PhD

> "To whom the unceasing suns belong,
> And cause is one with consequence,-
> To whose divine, inclusive sense
> The moan is blended with the song" -- Ambrose Bierce, Invocation

Welcome to the home page of Brandon L. Barker, PhD -- the best stop on the information superhighway!

I am a Metropolis Computational Physics Postdoctoral Fellow at Los Alamos
National Laboratory, working in the Computational Physics and Methods group and
the Center for Theoretical Astrophysics.

My current state:

- Metropolis Computational Physics Postdoctoral Fellow
- Computing and Artificial Intelligence Division
- Computational Physics and Methods Group (CAI-2)
- Center for Theoretical Astrophysics
- Los Alamos National Laboratory
- PhD, Astronomy and Astrophysics and Computational Mathematics, Sciences, and Engineering

I work as a research software engineer and computational (astro)physicist. My
primary interests are numerical methods, high-order accurate algorithms,
multiphysics modeling, and open-source scientific software for high-energy
density physics and astrophysical transients.

Start here:

+ [about me](aboutme)
+ [research](research)
+ [resources](resources)
+ [outreach](outreach)
+ [cv.pdf](blb_cv.pdf)

* * *

## Research

I develop computational models and numerical methods for multiscale physics,
with an emphasis on high-energy astrophysical transients such as supernovae and
kilonovae. I am especially interested in high-order discretizations, radiation
hydrodynamics, multiphysics coupling, and the software infrastructure needed
to turn these methods into reliable scientific tools.

More detail is available on my [research page](research).

* * *

## Selected Software

Software is a key piece of the scientific infrastructure.
The projects below are a sample of research software efforts I have developed
or contributed to, spanning radiation hydrodynamics, performance portability,
adaptive mesh refinement, equations of state, and code verification. Also see
my [GitHub](https://github.com/astrobarker).

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
My success, however defined, has only been possible because of the support
provided to me. Whenever possible, I share [resources](resources) for others to
benefit from, including fellowship materials, software notes, and technical
writeups.

* * *

## Outreach

Throughout my career I have worked to stay involved in my community.
Find out about the [outreach initiatives](outreach) I have been involved in.

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
