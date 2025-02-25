---
title: 'orbitize! v3: Orbit fitting for the High-contrast Imaging Community'
tags:
  - Python
  - astronomy
  - Orbit fitting
  - exoplanets
  - high-contrast imaging
authors:
  - name: Sarah Blunt
    orcid: 0000-0002-3199-2888
    corresponding: true
    affiliation: "1,2"
  - name: Jason Jinfei Wang
    orcid: 0000-0003-0774-6502
    affiliation: "1"
  - name: Lea Hirsch
    affiliation: "11"
  - name: Roberto Tejada
    affiliation: "12"
  - name: Vighnesh Nagpal
    orcid: 0000-0001-5909-4433
    affiliation: "13"
  - name: Tirth Dharmesh Surti
    affiliation: "5"
  - name: Sofia Covarrubias
    orcid: 0000-0003-1858-561X
    affiliation: "2"
  - name: Thea McKenna
    orcid: 0009-0008-0290-2143
    affiliation: "1,6,7,8"
  - name: Rodrigo Ferrer Chávez
    affiliation: "1"
  - name: Jorge Llop-Sayson
    orcid: 0000-0002-3414-784X
    affiliation: "4"
  - name: Mireya Arora
    affiliation: "14"
  - name: Amanda Chavez
    affiliation: "1"
  - name: Devin Cody
    orcid: 0000-0002-7713-5937
    affiliation: "9"
  - name: Saanika Choudhary
    affiliation: "1"
  - name: Adam Smith
    affiliation: "15"
  - name: William Balmer
    affiliation: "16"
  - name: Tomas Stolker
    orcid: 0000-0002-5823-3072
    affiliation: "3"
  - name: Hannah Gallamore
    affiliation: "15"
  - name: Clarissa R. Do Ó
    orcid: 0000-0001-5173-2947
    affiliation: "10"
  - name: Eric L. Nielsen
    affiliation: "15"
  - name: Robert J. De Rosa
    orcid: 0000-0002-4918-0247
    affiliation: "17"

affiliations:
 - name: Center for Interdisciplinary Exploration and Research in Astrophysics (CIERA), Northwestern University
   index: 1
 - name: California Institute of Technology
   index: 2
 - name: Leiden Observatory, Leiden University
   index: 3
 - name: Jet Propulsion Laboratory, California Institute of Technology
   index: 4
 - name: Department of Physics/Kavli Institute for Particle Astrophysics and Cosmology, Stanford University
   index: 5
 - name: Southeastern Universities Research Association
   index: 6
 - name: Astronomy Department, Cornell University
   index: 7
 - name: NASA Goddard Space Flight Center, Code 698
   index: 8
 - name: Google LLC
   index: 9
 - name: Department of Astronomy & Astrophysics, University of California San Diego
   index: 10
 - name: Department of Chemical & Physical Sciences, University of Toronto Mississauga
   index: 11
 - name: Department of Astrophysical Sciences, Princeton University
   index: 12
 - name: University of California, Berkeley
   index: 13
 - name: University of Michigan
   index: 14
 - name: New Mexico State University
   index: 15
 - name: Johns Hopkins University
   index: 16
 - name: European Southern Observatory
   index: 17


date: 14 March 2024
bibliography: paper.bib

---

# Summary

`orbitize!` is a package for Bayesian modeling of the orbital parameters of resolved binary 
objects from time series measurements. It was developed with the needs of the high-contrast
imaging community in mind, and has since also become widely used in the binary star community.
A generic `orbitize!` use case involves translating relative astrometric time series, optionally 
combined with radial velocity or astrometric time series, into a set of derived orbital posteriors.

This paper is published alongside the release of `orbitize!` version 3.0, which 
has seen significant enhancements in functionality and accessibility since the 
release of version 1.0 [@Blunt:2020].

# Statement of need

The orbital parameters of directly-imaged planets and binary stars can tell us about
their present-day dynamics and formation histories [@Bowler:2016], as well as about 
their inherent physical characteristics (particularly mass, generally called "dynamical 
mass" when derived from orbital constraints, e.g. @Brandt:2021, @Lacour:2021). 

`orbitize!` is widely used in the exoplanet imaging and binary star communities to translate astrometric data to information about eccentricities [@Bowler:2020], obliquities [@Bryan:2020], 
dynamical masses [@Lacour:2021], and more. 

Each new released version of the `orbitize!` source code is automatically archived on Zenodo [@orbitize].

# Major features added since v1

For a detailed overview of the `orbitize!` API, core functionality (including information 
about our Kepler solver), and initial verification, we refer the reader to @Blunt:2020. 
This section lists major new features that have been added to the 
code since the release of version 1.0 and directs the reader to more information about each of them.
A full descriptive list of modifications to the code is maintained in our 
[changelog](https://orbitize.readthedocs.io/en/latest/#changelog).

Major new features since v1 include:

1. The functionality to jointly fit the radial velocity (RV) time series for the primary star together with the secondary companion (see Section 3 of @Blunt:2023a). For the primary star, the RV data can either be directly input into orbitize! (as explained in the [Radial Velocity Tutorial](https://orbitize.readthedocs.io/en/latest/tutorials/RV_MCMC_Tutorial.html)) or be fitted separately and then used as priors (as detailed in the [Non-orbitize! Posteriors as Priors Tutorial](https://orbitize.readthedocs.io/en/latest/tutorials/Using_nonOrbitize_Posteriors_as_Priors.html)).

2. The ability to jointly fit absolute astrometry of the primary star. `orbitize!` can fit
    the Hipparcos-Gaia catalog of accelerations (@Brandt:2021; see the [HGCA Tutorial](https://orbitize.readthedocs.io/en/latest/tutorials/HGCA_tutorial.html)), as well as Hipparcos intermediate astrometric data and Gaia 
    astrometry, following @Nielsen:2020 (see the [Hipparcos IAD Tutorial](https://orbitize.readthedocs.io/en/latest/tutorials/Hipparcos_IAD.html)). It can also handle arbitrary absolute astrometry (see the [Fitting Arbitrary Astrometry Tutorial](https://orbitize.readthedocs.io/en/latest/tutorials/abs_astrometry.html)).

3. In addition to the MCMC and OFTI posterior computation algorithms documented in @Blunt:2020, 
    `orbitize!` version 3 also implements a nested sampling backend, via `dynesty` (@Speagle:2020; see the [`dynesty` Tutorial](https://github.com/sblunt/orbitize/blob/main/docs/tutorials/dynesty_tutorial.ipynb).)

4. `orbitize!` version 3 implements two prescriptions for handling multi-planet effects. 
    Keplerian epicyclic motion of the primary star due to multiple orbiting bodies, 
    following @Lacour:2021, is discussed in the [Multi-planet Tutorial](https://orbitize.readthedocs.io/en/latest/tutorials/Multiplanet_Tutorial.html), and N-body interactions are discussed in @Covarrubias:2022. The Keplerian epicyclic motion
    prescription only accounts for star-planet interactions, treating the motion of the star as a sum of Keplerian orbit signals, 
    while the N-body prescription models this effect as well as planet-planet interactions.

5. The ability to fit in different orbital bases (@Ferrer-Chavez:2021, @Surti:2023; see the 
    [Changing Bases](https://orbitize.readthedocs.io/en/latest/tutorials/Changing_bases_tutorial.html) tutorial), as well
    as the ability to apply the observation-based priors derived in @ONeil:2019 (see the [Observation-based Priors Tutorial](https://github.com/sblunt/orbitize/blob/main/docs/tutorials/ONeil-ObsPriors.ipynb)).

# Verification and Documentation

`orbitize!` implements a full stack of automated testing and documentation building 
practices. We use GitHub Actions to automatically run a suite of unit tests, maintained in [orbitize/tests](https://github.com/sblunt/orbitize/tree/main/tests),
each time code is committed to the public repository or a pull request is opened. The Jupyter notebook
tutorials, maintained in [orbitize/docs/tutorials](https://github.com/sblunt/orbitize/tree/main/docs/tutorials), are also run automatically when a 
pull request to the `main` branch is opened. Documentation is built using `sphinx`, and hosted
on readthedocs.org at [orbitize.info](https://orbitize.readthedocs.io/en/latest/). We also
maintain a set of longer-running tests in [orbitize/tests/end-to-end-tests](https://github.com/sblunt/orbitize/tree/main/tests/end-to-end-tests) that show real
scientific use cases of the code. These tests are not automatically run.

`orbitize!` is documented through API docstrings describing individual functions, which are accessible on [our readthedocs page](https://orbitize.readthedocs.io/en/latest/api.html), a set of [Jupyter notebook tutorials](https://orbitize.readthedocs.io/en/latest/tutorials.html) walking the user through a particular application, a set of [frequently asked questions](https://orbitize.readthedocs.io/en/latest/faq.html),
and an in-progress ["manual"](https://orbitize.readthedocs.io/en/orbitize-manual/manual.html) describing orbit fitting with `orbitize!` from first principles.

# Comparison to Similar Packages

Since the release of `orbitize!` version 1, other open source packages have been released that have 
similar goals to `orbitize!`, notably `orvara` [@Brandt:2021] and `octofitter` [@Thompson:2023]. This is a wonderful development, as all packages benefit from open sharing of knowledge! `orbitize!`, `orvara`, and `octofitter` can 
do many similar things, but each has unique features and strengths; as an example, `octofitter` is 
extraordinarily fast, and enables joint astrometry extraction and orbit modeling, while `orbitize!` has unique 
abilities to fit arbitrary absolute astrometry (i.e. not from Hipparcos or Gaia) and model data using an N-body backend. 
`orvara` analytically marginalizes over parallax assuming a prior informed by Gaia, a significant speed advantage, while 
`orbitize!` allows different parallax priors to be used. We recommend that users of each package compare the implementations 
of the particular features they wish to use. 

Best practices for orbit fitting, particularly using radial velocities, for which the treatment of stellar 
activity is an active area of research, and absolute astrometry with Gaia and Hipparcos, for which the treatment of 
correlated errors is an active area of research, evolve quickly. The philosophy of `orbitize!`
is to, as much as possible, implement multiple approaches to a problem, evidenced by our multiple
implementations of radial velocity joint fitting and absolute astrometry joint fitting (described above). 
For detailed information about our particular implementations, we refer the reader to our [documentation](https://orbitize.readthedocs.io/en/latest/). 

# Acknowledgements

Our team gratefully acknowledges support from the Heising-Simons Foundation.  S.B. and J.J.W. are supported by NASA Grant 80NSSC23K0280. E.L.N. is supported by NASA Grants 21-ADAP21-0130 and 80NSSC21K0958.


This paper describes additions made to `orbitize!` between versions 1.0.0 and 3.0.0. We are extremely grateful to Isabel Angelo, Henry Ngo, James Graham, Logan Pearce, and Malena Rice, who contribtued code to version 1.0.0, and are included as authors in @Blunt:2020.

# References
