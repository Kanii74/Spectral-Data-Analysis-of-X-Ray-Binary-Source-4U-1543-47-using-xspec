# Spectral Data Analysis of X-Ray Binary: 4U 1543-47

This repository contains the work carried out during a **summer internship project at the Indian Institute of Space Science and Technology (IIST)**.

The project focuses on the **spectral analysis of the X-ray binary system 4U 1543-47** using observational data from the **NuSTAR X-ray telescope**. The analysis was performed using **XSPEC**, a widely used software tool for modeling X-ray spectra in high-energy astrophysics.

The main goal of this work was to model the observed X-ray spectrum and extract **physical parameters describing the accretion environment around a stellar-mass black hole**.

---

# Scientific Background

## X-Ray Binaries

X-ray binaries are systems consisting of two main components:

- A **compact object** (black hole or neutron star)
- A **normal companion star**

Matter from the companion star is transferred to the compact object through **accretion**, forming an **accretion disk**. As matter spirals inward, gravitational energy is converted into heat and radiation, producing strong **X-ray emission**.

These systems provide an excellent laboratory for studying:

- Black hole physics  
- Accretion disk dynamics  
- High-energy radiation processes  

---

# The Source: 4U 1543-47

4U 1543-47 is a **stellar-mass black hole X-ray binary** originally detected in the **Uhuru X-ray catalog**.

Important properties of the system include:

| Property | Value |
|--------|--------|
| Source Name | 4U 1543-47 |
| Type | Black Hole X-ray Binary |
| Black Hole Mass | ~9.4 ± 2 Solar Masses |
| Distance | ~7.5 ± 1 kpc |
| Right Ascension | 15h 47m 08s |
| Declination | −47° 40′ 12″ |

The observations analyzed correspond to the **2021 outburst of the source**, during which the X-ray flux gradually decreases over time.

---

# Data

The spectral data analyzed in this project comes from the **NuSTAR (Nuclear Spectroscopic Telescope Array)** mission.

NuSTAR observes the universe in the **hard X-ray band from 3–79 keV** and is particularly well suited for studying compact objects such as black holes.

Observation IDs used in this analysis:

| Observation ID |
|----------------|
| 80702317002 |
| 80702317004 |
| 80702317006 |
| 80702317008 |
| 90702326002 |
| 90702326004 |
| 90702326006 |
| 90702326008 |
| 90702326010 |
| 90702326012 |

These observations capture the **spectral evolution of the system during its outburst phase**.

---

# Software and Tools

The analysis used the following software tools:

- HEASOFT
- XSPEC
- NuSTAR observational data products
- relxill reflection model

XSPEC is a standard tool in **X-ray astronomy used for spectral fitting and statistical analysis**.

---

# Spectral Model

The spectra were modeled using the following XSPEC model:

```
tbabs*zxipcf*(diskbb + relxill)
```

Each component represents a different physical process occurring in the system.

---

# Model Components

## tbabs

Models **interstellar absorption** due to neutral hydrogen along the line of sight.

Parameter:

| Parameter | Description |
|----------|-------------|
| nH | Hydrogen column density |

---

## zxipcf

Models **ionized absorption with partial covering**.

Parameters:

| Parameter | Description |
|----------|-------------|
| NH | Column density |
| log xi | Ionization parameter |
| Covering Fraction | Fraction of source covered |
| Redshift | Source redshift |

---

## diskbb

Represents **thermal emission from the accretion disk**.

The model assumes a **multi-temperature blackbody disk**.

Parameters:

| Parameter | Description |
|----------|-------------|
| Tin | Inner disk temperature |
| norm | Disk normalization |

---

## relxill

The **relxill model** describes **relativistic reflection from the accretion disk near a black hole**.

This model combines:

- xillver (reflection spectrum calculations)
- relline (relativistic ray tracing)

It includes relativistic effects such as:

- gravitational redshift  
- Doppler broadening  
- light bending near the black hole  

Important parameters include:

| Parameter | Description |
|----------|-------------|
| Spin | Black hole spin |
| Inclination | Disk inclination angle |
| Inner Radius | Inner disk radius |
| Gamma | Photon index |
| log xi | Disk ionization |
| Iron Abundance | Iron abundance in disk |
| Energy Cutoff | High-energy cutoff |
| Reflection Fraction | Strength of reflection |

---

# Spectral Fitting Procedure

The spectral fitting process followed these steps:

1. Load spectral data into XSPEC
2. Define the physical model
3. Set initial parameter values
4. Fit the model to the data
5. Evaluate goodness of fit using chi-squared statistics
6. Estimate parameter uncertainties

Example XSPEC commands used during the analysis:

```
data spectrumfile
response responsefile
backgrnd backgroundfile

model tbabs*zxipcf*(diskbb + relxill)

fit
plot data
plot model
show parameters
```

---

# Parameter Estimation Using MCMC

To estimate uncertainties in the fitted parameters, **Markov Chain Monte Carlo (MCMC)** techniques were used.

MCMC allows a more complete exploration of parameter space and produces reliable confidence intervals.

Example XSPEC commands:

```
chain type gw
chain walkers 8
parallel walkers 4
chain length 100000
chain run chainfile.fits
chain burn 10000
plot chain
```

This method generates probability distributions for each parameter and provides robust uncertainty estimates.

---

# Physical Interpretation

The spectral fits indicate the presence of:

- A **thermal disk component** from the accretion disk
- A **power-law continuum** produced by Comptonization in the corona
- **Relativistic reflection features** originating from the inner disk

The power-law emission originates from a **hot corona**, where soft photons from the accretion disk are upscattered by energetic electrons through **inverse Compton scattering**.

Reflection features appear when coronal X-rays illuminate the disk and are reflected back toward the observer.

Important diagnostic signatures include:

- Iron emission lines around **6–7 keV**
- Compton reflection hump
- Relativistic broadening of spectral lines

These features allow constraints on:

- Black hole spin
- Disk inclination
- Ionization state of the disk
- Inner radius of the accretion disk

---

# Accretion Disk Physics

The accretion disk forms when matter from the companion star spirals inward toward the black hole.

Key physical processes governing the disk include:

- Viscous transport of angular momentum
- Gravitational energy conversion into radiation
- Magnetic turbulence driving accretion
- Radiative cooling balancing heating

The disk temperature increases toward the inner regions, producing the **multi-temperature blackbody spectrum** modeled using the `diskbb` component.

---

# Challenges in X-Ray Spectral Analysis

X-ray spectral modeling involves several challenges:

### Instrument Response

Detector response must be included because instruments do not measure photon energy directly.

### Model Degeneracy

Different models may produce similar spectra, making interpretation difficult.

### Computational Cost

Advanced models combined with MCMC methods require significant computational resources.

---



