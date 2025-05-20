# SVETlANNa

---

[![OSA-improved](https://img.shields.io/badge/improved%20by-OSA-yellow)](https://github.com/aimclub/OSA)

---

## Overview

SVETlANNa is an open-source library for simulating optical systems and exploring the potential of optical neural networks. It empowers researchers to design, analyze, and optimize innovative setups for light manipulation and computation, accelerating advancements in fields like image processing and machine learning.

---

## Table of Contents

- [Core features](#core-features)
- [Installation](#installation)
- [Getting Started](#getting-started)
- [Examples](#examples)
- [Contributing](#contributing)
- [Citation](#citation)

---
## Core features

1. **Free-Space Optical Setup Simulation**: SVETlANNa enables the simulation of free-space optical setups, allowing users to model and analyze light propagation through various optical components.
2. **Neuromorphic System Modeling**: The library supports modeling neuromorphic systems, specifically Diffractive Neural Networks (DONNs), facilitating research in optical neural networks.
3. **Fourier Optics Foundation**: SVETlANNa is built upon the principles of Fourier optics and provides implementations of propagation models like Angular Spectrum Method and Fresnel Approximation for accurate simulations.
4. **Diffractive Element Optimization**: The library includes algorithms (Gerchberg-Saxton, hybrid input-output) to solve the classical Diffractive Optical Element (DOE)/Spatial Light Modulator (SLM) optimization problem.
5. **PyTorch Integration**: SVETlANNa is built on PyTorch, leveraging its tensor-based computations and efficient parallel processing capabilities for fast simulations.
6. **ONN Architecture Support**: The library supports various free-space Optical Neural Network (ONN) architectures, including feed-forward, autoencoders, and recurrent networks.
7. **GPU Acceleration**: SVETlANNa provides full GPU acceleration for computationally intensive simulations, significantly reducing processing time.

---

## Installation

**Prerequisites:** requires Python ^3.11,<3.12

Install SVETlANNa using one of the following methods:

**Build from source:**

1. Clone the SVETlANNa repository:
```sh
git clone https://github.com/CompPhysLab/SVETlANNa
```

2. Navigate to the project directory:
```sh
cd SVETlANNa
```

---

## Getting Started

To get started, you'll need to install PyTorch and Poetry.

```bash
pip install torch
pip install poetry
```

Then, navigate to the library folder and run:

```bash
poetry install
```

You can then run a simple simulation like this:

```python
import svetlanna
import torch

simulation_parameters = svetlanna.SimulationParameters(
    {
        'W': torch.linspace(-1, 1, 100),
        'H': torch.linspace(-1, 1, 100),
        'wavelength': 2e-1
    }
)

system = svetlanna.LinearOpticalSetup([
    svetlanna.elements.ThinLens(simulation_parameters=simulation_parameters, focal_length=1),
    svetlanna.elements.FreeSpace(simulation_parameters=simulation_parameters, distance=1, method='fresnel'),
    svetlanna.elements.ThinLens(simulation_parameters=simulation_parameters, focal_length=1),
    svetlanna.elements.FreeSpace(simulation_parameters=simulation_parameters, distance=1, method='fresnel'),
    svetlanna.elements.DiffractiveLayer(simulation_parameters=simulation_parameters, mask=torch.rand((100, 100))), 
    svetlanna.elements.Aperture(simulation_parameters=simulation_parameters, mask=torch.rand((100, 100))),
    svetlanna.elements.FreeSpace(simulation_parameters=simulation_parameters, distance=1, method='fresnel'),
    svetlanna.elements.ThinLens(simulation_parameters=simulation_parameters, focal_length=1),
])

system.show()

input_field = svetlanna.Wavefront.plane_wave(simulation_parameters)
system.show_stepwise_forward(input_field, simulation_parameters, types_to_plot=('I', 'phase', 'Re'))
```

---

## Examples

Examples of how this should work and how it should be used are available [here](https://github.com/CompPhysLab/SVETlANNa/tree//examples).

---

## Contributing

- **[Report Issues](https://github.com/CompPhysLab/SVETlANNa/issues)**: Submit bugs found or log feature requests for the project.

---

## Citation

If you use this software, please cite it as below.

### APA format:

     (). SVETlANNa repository [Computer software]. https://github.com/CompPhysLab/SVETlANNa

### BibTeX format:

    @misc{SVETlANNa,

        author = {},

        title = {SVETlANNa repository},

        year = {},

        publisher = {github.com},

        journal = {github.com repository},

        howpublished = {\url{https://github.com/CompPhysLab/SVETlANNa.git}},

        url = {https://github.com/CompPhysLab/SVETlANNa.git}

    }

---
