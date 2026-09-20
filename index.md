---
layout: term
title: brandon's website
cmd: cat index.md
tree:
  - { name: research.md, href: /research,   kind: file, desc: my work! }
  - { name: about.md,    href: /aboutme,    kind: file, desc: more about me }
  - { name: resources,   href: /resources,  kind: dir,  desc: "fellowship materials and technical notes (%posts% posts)" }
  - { name: outreach.md, href: /outreach,   kind: file, desc: community work }
  - { name: cv.pdf,      href: /blb_cv.pdf, kind: file }
---

> "To whom the unceasing suns belong, \\
> And cause is one with consequence,- \\
> To whose divine, inclusive sense \\
> The moan is blended with the song,-" \\
> -- Ambrose Bierce, Invocation

# Brandon L. Barker, PhD

{% include term-profile.html file="barker.yaml" %}

Welcome to the home page of Brandon L. Barker, PhD -- the best stop on the information superhighway!

I am a computational astrophysicist and research software engineer at Los Alamos
National Laboratory in the Computational Physics and Methods group.
I develop and deploy modern, high performance multiphysics scientific 
simulation software to model high energy density plasmas for both 
terrestrial and astrophysical environments. My interests include 
astrophysical transients (primarily supernovae!), nuceosynthesis sites, 
high order numerical methods, radiation hydrodynamics, and multiphysics 
coupling.

Find out more about me and my work:

{% include term-tree.html entries=page.tree root="~" %}
