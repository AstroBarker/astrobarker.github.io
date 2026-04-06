---
layout: term
title: astrobarker.github.io
cmd: cat research.md
---

Research
========

> Splendors of elemental strife;
> Smit suns that startle back the gloom;
> New light whose tale of stellar doom
> Fares to uncomprehending life; 
> -- George Sterling, The Testimony of the Suns, 1907

The transient sky is diverse and ever-changing.
Supernovae, having been observed and recorded by humanity for the 
whole of our species' history, are among the most prolific phenomena 
observed in the night sky. These are magnificent explosions following 
stellar death. They are, literally, the last testimony of a dying star.
It is our charge as practitioners of stellar astrophysics to interpret 
these testimonies: what is the star trying to tell us? What can we learn
about its life, death, and environment?
My work involves deploying and developing computational models 
to interpret these testimonies.

## Open Source Simulation Codes

As we move into the era of exascale computing, we need modern simulation codes 
that can take full advantage of these architectures. 
This poses a significant engineering challenge as the number of programming 
models continues to grow.

**[Athelas][athelas]** is being developed to simulate the electromagnetic emission 
from transients, primarily supernovae. ``Athelas`` evolves Lagrangian hydrodynamics 
coupled to a two moment radiation transport model. 
It leverages a discontinuous Galerkin spatial 
discretization of the fluid and radiation fields to acheive robust solutions 
Time integration is implemented with high-order, fully coupled implicit-explicit (IMEX) 
methods -- no operator splitting is required.
at high order accuracy. ``Athelas`` includes Saha ionization coupled to the 
equation of state, a radioactive decay network for nickel heating, and can artificially 
drive explosions. In the near future it will incorporate a Rayleigh Taylor mixing model.
``Athelas`` includes a very flexible ``package`` system for building up the partial 
differential equations being solved, automatically threading physics into the IMEX
integrator, making it very simple to add new physics. ``Athelas`` includes 
the capability to map outputs from the ``MESA`` stellar evolutionary code into 
its input format to make robust predictions.

**[Phoebus][phoebus]** is developed to tackle a range of problems in relativistic astrophysics, with emphasis on core-collapse supernovae, 
neutron star mergers, and black hole accretion. It is developed from the ground using a GPU-first development strategy. 
To facilitate performance portability, Phoebus is built on [Kokkos][kokkos], a parallelization abstraction layer that allows 
Phoebus to run on any GPU or CPU architecture by simply changing compile-time options. 

**[Thornado][thornado]** is a GPU-capable code utilizing a discontinuous 
Galerkin phase-space discretization developed primarily for modeling core-collapse 
supernovae. By using discontinuous Galerkin methods for both hydrodynamics and 
neutrino radiation transport, thornado can achieve high order accurate solutions for 
both the fluid and radiation fields, capturing the complex flows that assist in 
shock revival, and ensure realizability of the fermionic neutrino distribution 
functions. Thornado provides neutrino transport capabilities to the 
multiphysics code [Flash-X][flashx].

I contribute to a number of other frameworks that support downstream
science production codes such as the [parthenon][parthenon] adaptive
mesh refinement framework and the [singularity-eos][singularity-eos]
performance portable equation of state library.

On my [GitHub][github] you may find software that I 
have produced, including codes for protytyping and exploring methods.

* * *

## Discontinuous Galerkin Finite Element Method

Discontinuous Galerkin methods are a very promising method for simulating 
astrophysical phenomena. They can be thought of as the high-order 
love child of finite volume and finite element methods.
Similar to finite elements, the solution is represented as a basis expansion.
However, unlike finite elements, these basis representations may be discontinuous 
across cells. Neighboring cells are connected via numerical fluxes  -- 
Riemann solvers -- identical to finite volume methods.
By evolving a high-order approximation 
of the solution on each cell instead of cell averages we avoid
the need for complicated reconstruction steps. As a result, the 
computational stencil is independent of the order of accuracy — only 
nearest-neighbor communication is needed, making them especially parallelizable. 
Discontinuous Galerkin methods have a number of desirable qualitities, 
including improved angular momentum conservation, more natural capturing 
of asymptotic limits in radiation transport, and polyunomial order adaptivity 
in space. They are high resolution shock capturing schemes that are conservative 
of the cell average in the finite volume sense.

* * *

## Using Realistic Explosion Models To Interpret Core-Collapse Supernovae Observations

Observations of core-collapse supernovae (CCSNe) reveal a wealth of information about the dynamics of the supernova ejecta and composition 
but tell little of the progenitor star without invoking a theoretical model. Until recently, one-dimensional (1D) theoretical 
CCSN models did not include a robust treatment of the core physics, resorting instead to artificial thermal bomb explosions. 
These simplified methods input arbitrary explosion energy into a progenitor to induce an explosion.

I use a new model for driving turbulence-aided neutrino-driven core-collapse supernovae in 1D, which contains a high-fidelity 
treatment of the neutrino physics while also accounting for turbulence and convection, which can reproduce properties of 3D 
simulations. Moreover, our light curve features agree very well with a population of observed Type IIP supernovae. 
With this, I can begin to connect explosion and progenitor properties for a realistic population of CCSNe to apply to observed CCSNe. 
This is especially exciting as LSST and other next-generation surveys prepare to collect unprecedented amounts of data.

The use of realistic explosion models is important for understanding observables and connecting back to the progenitor star. 
It is becoming clear that explosion properties inferred from light curves are not unique (e.g., Goldberg 2019) — many progenitor 
and explosion energy combinations can reproduce a light curve. Using a realistic explosion model — where the explosion energy is 
determined naturally by properties of the progenitor and neutrino physics — could help to reduce this problem by excluding 
progenitor-explosion energy combinations that cannot be achieved by more physical models.

An initial paper has been published where we explore this method for a suite of over 100 progenitors. We find excellent 
bulk agreement with observations of other Type IIP supernovae, notable differences in estimated progenitor properties when 
trying to infer properties from observed light curves, and a strong, linear relationship between plateau luminosity and iron core mass.

Following up on this, we used these results with real observations to infer iron core masses for a population of SNe. 
In this paper, we apply Bayesian inference methods to connect the inferred iron core mass distribution to ZAMS mass properties, 
finding evidence of very high red supergiant progenitors.

* * *


## Equation of State Dependence of Core-Collapse Supernova Observables

The outcomes of core-collapse supernova (CCSN) simulations can depend sensitively on the nuclear physics of dense matter through 
the equation of state (EOS). In the simulation of core-collapse supernovae, the EOS of nuclear matter is included through 
phenomenological models and encoded in an EOS table for use in our simulations as a relationship between the thermodynamical 
variables. Due to limitations in our understanding and in computational feasibility, there are many different models 
for the nuclear force, resulting in many different tables that we may include in our simulations. Therefore, a quantitative 
understanding of how different EOS tables affect the outcome of core collapse is crucial to our ability to make predictions. 
1D CCSN simulations are ideal tools for understanding this sensitivity, as we can run thousands of 1D simulations to explore 
the parameter space meaningfully. Using a new model for creating physical explosions in 1D, I explored the sensitivity of 
CCSNe to variations in input nuclear physics by performing a population study using nine open-source EOS tables and 138 
progenitor stars with ZAMS masses ranging from 9 to 120 solar masses. I tested the sensitivities of the observable signals 
to the nuclear equation of state and explored correlations of the signals with fundamental nuclear physics quantities, 
such as the symmetry energy and effective nucleon mass.

* * *

## Prospects for High Energy Follow-up Studies of Gravitational Wave Transients

Many of the most violent and energetic events in the cosmos, in particular the merger of compact objects and 
core-collapse supernovae, are sources of gravitational waves and are also believed to be connected with 
Gamma Ray Bursts. Joint observations of electromagnetic and gravitational wave signals will provide an ideal 
opportunity to study the physics of these transient events and their progenitors. In particular, gamma-ray 
observatories such as Fermi, coupled with precise sky localization, will be crucial to observe the high-energy 
electromagnetic counterparts to gravitational wave signals. We constructed joint binary neutron star and gamma-ray 
burst detection rate estimates using an analysis pipeline and report on the results of this analysis. Moreover, 
I extended the analysis to include a catalog of real galaxies appropriate for such a follow-up study (the GLADE Catalog).

* * *

## Other Research

- **The Nature of Supernova Shock Revival:** After the onset of core collapse, the shock responsible for tearing the 
star apart and driving the explosion runs out of energy and stalls. The exact nature of how the shock is revived is 
still a matter of active research. I developed data analysis tools to investigate the relative contributions of 
neutrino-driven convection and the standing accretion shock instability to shock revival.

* * *

[singularity-eos]: https://github.com/lanl/singularity-eos
[parthenon]: https://github.com/parthenon-hpc-lab/parthenon/
[github]: https://github.com/astrobarker
[flashx]: https://flash-x.org/
[athelas]: https://github.com/athelas-astro/athelas
[phoebus]: https://github.com/lanl/phoebus
[thornado]: https://github.com/endeve/thornado
[kokkos]: https://github.com/kokkos/kokkos
