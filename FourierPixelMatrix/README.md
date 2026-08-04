# Fourier Pixel Matrix Simulator

Interactive HTML5/JavaScript simulator of a **lensless Fourier pixel matrix** based on wave optics.

The project demonstrates the principle of recording and reconstructing a complex optical wavefront using amplitude and phase information without traditional glass lenses.

This is an independent educational simulation inspired by modern research in lensless computational imaging and nanophotonic systems.

---

# Overview

Traditional optical systems rely on lenses to transform and focus light.

A lensless Fourier pixel system replaces classical optics with computational reconstruction:

1. Light from an object creates a complex wavefront.
2. A pixel matrix records amplitude and phase information.
3. The recorded field is numerically propagated to reconstruct the original spatial structure.

The simulator visualizes this process using classical wave optics equations.

---

# Features

- Interactive object movement using touch or mouse.
- Multiple optical objects:
  - Cross
  - Square
  - Line
  - Letter F
- Adjustable wavelength.
- Adjustable Fourier pixel matrix density.
- Adjustable reconstruction brightness.
- Real-time CPU rendering.
- No WebGL.
- No external libraries.
- Single HTML file.

---

# Physical Model

The simulator is based on scalar wave optics.

Each point of the object is treated as a coherent secondary spherical wave source according to the **Huygens–Fresnel principle**.

The total optical field is obtained through wave superposition.

---

# Simulation Pipeline

The simulation consists of three stages.

---

## 1. Object Wave Generation

The object is represented as a collection of emitting points.

Each point generates a spherical wave:

$$
U_i(r)=\frac{A_i}{r}e^{-ikr}
$$

where:

- $A_i$ — source amplitude;
- $r$ — propagation distance;
- $k$ — wave number.

The wave number is:

$$
k=\frac{2\pi}{\lambda}
$$

where:

- $\lambda$ — wavelength of light.

---

# 2. Fourier Pixel Matrix Recording

Each Fourier pixel receives contributions from all object points.

The complex optical field at a pixel is:

$$
U_j=\sum_{i=1}^{N}
\frac{A_i}{r_{ij}}
e^{-ikr_{ij}}
$$

where:

- $N$ — number of object points;
- $r_{ij}$ — distance between object point $i$ and matrix pixel $j$.

The complex field is represented as:

$$
U=Re+iIm
$$

where:

- $Re$ — real component;
- $Im$ — imaginary component.

After summation, the pixel stores:

## Amplitude

$$
A=|U|
$$

or:

$$
A=\sqrt{Re^2+Im^2}
$$


## Phase

$$
\phi=\operatorname{atan2}(Im,Re)
$$

The matrix therefore contains information about the optical wavefront.

---

# 3. Lensless Reconstruction

The recorded field is propagated backwards.

Each Fourier pixel acts as a secondary emitter.

The reconstructed field at a point $(x,y)$ is:

$$
U(x,y)=
\sum_{j=1}^{M}
\frac{A_j}{r_j}
e^{i(kr_j+\phi_j)}
$$

where:

- $M$ — number of Fourier pixels;
- $r_j$ — distance from matrix pixel to reconstruction point;
- $\phi_j$ — recorded phase.

Interference between reconstructed waves creates the final image.

---

# Image Formation

A camera or human eye detects intensity, not the electric field itself.

The visible intensity is:

$$
I(x,y)=|U(x,y)|^2
$$

or:

$$
I(x,y)=Re(U)^2+Im(U)^2
$$

The simulator converts this intensity into screen brightness.

---

# Architecture

The simulation interface is divided into three zones.

---

## Zone 1 — Object and Incoming Waves

The upper area contains the optical object.

The object generates coherent waves that propagate toward the Fourier matrix.

Visualized effects:

- spherical wave propagation;
- interference;
- phase-dependent oscillations.

---

## Zone 2 — Lensless Reconstruction

The central area displays the reconstructed image.

The reconstruction is generated only from:

- recorded amplitude;
- recorded phase.

The original object coordinates are not used during reconstruction.

---

## Zone 3 — Fourier Pixel Matrix

The lower area displays the simulated pixel matrix.

Each pixel represents:

- optical amplitude;
- optical phase.

The phase is visualized through color variation.

---

# Mathematical Principles Used

The simulator implements:

## Huygens–Fresnel principle

Every point of a wavefront behaves as a secondary wave source.

---

## Principle of Superposition

The total field is the sum of all individual contributions:

$$
U_{total}=\sum_i U_i
$$

---

## Complex Wave Representation

Light is represented as:

$$
U=Ae^{i\phi}
$$

or:

$$
U=Re+iIm
$$

---

## Optical Phase Propagation

The phase changes according to travelled distance:

$$
\Delta\phi=k\Delta r
$$

---

## Interference

The final intensity appears due to constructive and destructive interference:

$$
I=|U_1+U_2+...+U_n|^2
$$

---

# Performance Optimization

The simulator is designed for real-time execution on common devices.

Implemented optimizations:

- Canvas 2D rendering.
- ImageData direct pixel manipulation.
- CPU-based calculations.
- Reduced internal rendering resolution.
- Dynamic object point generation.
- Minimal memory allocation inside the render loop.

---

# Current Limitations

This is an educational physical visualization, not a precision optical simulator.

The following effects are simplified or not implemented:

- Vector electromagnetic fields.
- Full Maxwell equations.
- Polarization.
- Real nanophotonic structures.
- Plasmonic effects.
- Detector noise.
- Quantum efficiency.
- Real semiconductor pixel physics.
- FFT acceleration.
- Angular Spectrum Method.
- Rayleigh–Sommerfeld diffraction.
- Material optical properties.

Real lensless imaging systems require much more complex electromagnetic and computational models.

---

# Technologies

Built with:

- HTML5
- JavaScript
- Canvas 2D API

No external dependencies.

---

# Controls

- Move the object with touch or mouse.
- Select object geometry.
- Change wavelength.
- Increase or decrease matrix resolution.
- Adjust reconstruction brightness.

---

# Project Purpose

This simulator is intended for:

- learning wave optics;
- visualization of interference phenomena;
- studying phase information in light;
- exploring lensless imaging concepts;
- educational experiments with computational optics.

---

# Disclaimer

This project is an independent educational simulation.

It demonstrates theoretical principles of wavefront recording and reconstruction but does not reproduce the complete operation of real commercial or research-grade Fourier pixel devices.

Real systems involve advanced nanophotonics, semiconductor fabrication, electromagnetic simulation and specialized reconstruction algorithms.
