---
layout: term
title: astrobarker.dev
cmd: cat research.md
toc:
  - { name: open-source-software, href: "#open-source-simulation-codes", kind: file }
  - { name: research-highlights,  href: "#research-highlights",          kind: file }
---

# Research

> Splendors of elemental strife \\
> Smit suns that startle back the gloom \\
> New light whose tale of stellar doom \\
> Fares to uncomprehending life \\
> -- George Sterling, The Testimony of the Suns, 1907

The transient sky is diverse and ever-changing.
Supernovae, having been observed and recorded by humanity for the
whole of our species' history, are among the most prolific phenomena
observed in the night sky. These are magnificent explosions following
stellar death. They are, in a very real sense, the last testimony of a dying
star. It is our charge as practitioners of stellar astrophysics to interpret
these testimonies: what is the star trying to tell us? What can we learn
about its life, death, and environment?
My work involves deploying and developing computational models
to interpret these testimonies.

{% include term-tree.html entries=page.toc root="topics/" %}

## Open Source Simulation Codes

Modern simulation codes must be robust, accurate, and able to exploit exascale
architectures across a growing number of programming models, and they must
outlive the questions they were written to answer. Meeting these demands is
**research software engineering**: the union of domain knowledge, numerical
methods, and modern software development practices. I develop and contribute
to a number of open source codes in this spirit.

+ **[Athelas][athelas]: A modern transient code**

  `Athelas` is a Lagrangian radiation hydrodynamics code for modeling
  core-collapse supernovae and generating synthetic light curves. It combines
  high-order discontinuous Galerkin discretizations with fully coupled
  implicit-explicit time integration, a flexible physics `package` system, and
  M1 transport.

+ **[Phoebus][phoebus]: Performance-portable GRRMHD**

  `Phoebus` is a general relativistic neutrino radiation magnetohydrodynamics
  code for core-collapse supernovae, neutron star mergers, and black hole
  accretion. Built on `Parthenon` and [Kokkos][kokkos], it runs on any GPU or
  CPU architecture. See the [paper][phoebus-paper].

+ **[thornado][thornado]: Discontinuous Galerkin supernova modeling**

  `Thornado` is a GPU-capable neutrino radiation hydrodynamics code using
  high-order discontinuous Galerkin methods for both the fluid and the
  radiation fields, and provides neutrino transport to [Flash-X][flashx].

+ **[Parthenon][parthenon]: Performance-portable adaptive mesh refinement**

  `Parthenon` is a distributed, block-structured adaptive mesh refinement
  framework built on [Kokkos][kokkos] for performance portability across CPUs
  and GPUs.

+ **[Singularity-eos][singularity-eos]: Performance-portable equations of state**

  `Singularity-eos` provides more than ten equations of state for terrestrial
  and astrophysical applications on heterogeneous architectures. See the
  [paper][singularity-eos-paper].

+ **[sordine][sordine]: Hydrodynamics verification**

  `sordine` is a growing radiation hydrodynamics verification suite containing
  self-similar solutions for every family of Sedov-Taylor blast waves.

+ **[mplcolors][mplcolors]: Command-line color tools**

  `mplcolors` is a command-line and Python package for exploring Matplotlib
  colors, colorbars, complements, triads, and tetrads.

More of my work, including codes for prototyping and exploring methods, is on
[GitHub][github].

* * *

## Research Highlights

+ **Discontinuous Galerkin methods**

  High-order shock-capturing schemes that pair the basis expansions of finite
  elements with the Riemann solvers of finite volume methods. The stencil is
  independent of the order of accuracy, so only nearest-neighbor communication
  is needed, and asymptotic limits in radiation transport are captured
  naturally. They are the discretization underlying `Athelas` and `thornado`.

+ **Realistic explosion models for Type IIP supernovae**

  Using a 1D model of turbulence-aided, neutrino-driven explosions in place of
  artificial thermal bombs, I produced light curves for a suite of over 100
  progenitors that agree with observed Type IIP populations and found a strong,
  linear relation between plateau luminosity and iron core mass. Applying
  Bayesian inference to observed supernovae then yielded evidence for high mass
  red supergiant progenitors.

+ **Equation of state dependence of supernova observables**

  A population study of 138 progenitors from 9 to 120 solar masses across nine
  open-source nuclear equation of state tables, quantifying how core-collapse
  observables respond to dense-matter physics and correlating them with
  quantities such as the symmetry energy and effective nucleon mass.

+ **High-energy follow-up of gravitational wave transients**

  Joint detection rate estimates for binary neutron star mergers and gamma-ray
  bursts observed with Fermi, extended to a realistic follow-up strategy using
  the GLADE galaxy catalog.

+ **Supernova shock revival**

  Analysis tools to separate the contributions of neutrino-driven convection
  and the standing accretion shock instability to reviving the stalled
  supernova shock.

* * *

[singularity-eos]: https://github.com/lanl/singularity-eos
[parthenon]: https://github.com/parthenon-hpc-lab/parthenon/
[github]: https://github.com/astrobarker
[flashx]: https://flash-x.org/
[athelas]: https://github.com/athelas-astro/athelas
[phoebus]: https://github.com/lanl/phoebus
[thornado]: https://github.com/endeve/thornado
[kokkos]: https://github.com/kokkos/kokkos
[phoebus-paper]: https://ui.adsabs.harvard.edu/abs/2024arXiv241009146B/abstract
[singularity-eos-paper]: https://doi.org/10.21105/joss.06805
[sordine]: https://github.com/astrobarker/sistrum
[mplcolors]: https://github.com/astrobarker/mplcolors
