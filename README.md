# Rayleigh-Benard-Convection

# 2D Rayleigh-Bénard Convection Simulation

A Python implementation of 2D Rayleigh-Bénard convection using finite difference methods, based on the Boussinesq equations used in planetary convection studies.

## Overview

This simulation models thermal convection in a fluid layer heated from below and cooled from above - a fundamental process in fluid dynamics known as Rayleigh-Bénard convection. The implementation is inspired by planetary convection studies, particularly those examining nitrogen ice convection on Pluto's surface.

## Scientific Background

The simulation is based on research from:
- **McKinnon et al. (2016)**: Convection in a volatile nitrogen-ice-rich layer on Pluto
- **Morison et al. (2021)**: Sublimation-driven convection in Sputnik Planitia on Pluto

### Governing Equations

The simulation solves the following dimensionless equations:

1. **Continuity Equation**: ∇·**u** = 0
2. **Momentum Equations** (Boussinesq approximation):
   - ∂u/∂t + **u**·∇u = -∇p/ρ₀ + ν∇²u
   - ∂w/∂t + **u**·∇w = -∇p/ρ₀ + ν∇²w + gαΔT
3. **Energy Equation**: ∂T/∂t + **u**·∇T = κ∇²T

Where:
- **u** = velocity field (u, w)
- p = pressure
- T = temperature
- ρ₀ = reference density
- ν = kinematic viscosity
- κ = thermal diffusivity
- α = thermal expansion coefficient
- g = gravitational acceleration

## Key Features

- **Finite Difference Method**: Uses explicit time stepping with central difference spatial discretization
- **Boussinesq Approximation**: Accounts for buoyancy effects due to temperature variations
- **Flexible Parameters**: Configurable Rayleigh and Prandtl numbers
- **Comprehensive Visualization**: Temperature fields, vorticity, streamlines, and animations
- **Boundary Conditions**:
  - No-slip walls at top and bottom
  - Periodic boundary conditions at sides
  - Fixed temperature: hot bottom (T=1), cold top (T=0)

## Installation

### Prerequisites

```bash
pip install numpy matplotlib scipy
```

### Required Python Packages

- `numpy` - Numerical computations
- `matplotlib` - Plotting and visualization
- `scipy` - Sparse matrix operations for numerical solving

## Usage

### Basic Example

```python
from rayleigh_benard import RayleighBenardConvection2D

# Create simulation instance
conv_sim = RayleighBenardConvection2D(
    nx=128,      # Grid resolution (x-direction)
    ny=64,       # Grid resolution (y-direction)
    Lx=4.0,      # Domain width
    Ly=1.0,      # Domain height
    Ra=50000,    # Rayleigh number
    Pr=0.7       # Prandtl number
)

# Run simulation
T_history, omega_history, psi_history, times = conv_sim.run_simulation(
    steps=2000, 
    save_interval=20
)

# Create visualization
from rayleigh_benard import create_visualization
fig = create_visualization(conv_sim, T_history, omega_history, psi_history, times)
```

### Parameters

| Parameter | Description | Typical Values |
|-----------|-------------|----------------|
| `nx`, `ny` | Grid resolution | 64-256 |
| `Lx`, `Ly` | Domain dimensions | Lx/Ly = 2-4 (aspect ratio) |
| `Ra` | Rayleigh number | 1000-100000 |
| `Pr` | Prandtl number | 0.1-10 |

### Rayleigh Number

The Rayleigh number is defined as:

**Ra = gαΔTH³/(νκ)**

Where:
- g = gravitational acceleration
- α = thermal expansion coefficient  
- ΔT = temperature difference
- H = layer height
- ν = kinematic viscosity
- κ = thermal diffusivity

**Critical Ra ≈ 1708** - Below this value, heat transfer occurs by conduction only. Above this value, convective cells form.

### Prandtl Number

The Prandtl number is defined as:

**Pr = ν/κ**

- **Pr < 1**: Heat diffuses faster than momentum (liquid metals)
- **Pr ≈ 1**: Heat and momentum diffuse at similar rates (gases, water)
- **Pr > 1**: Momentum diffuses faster than heat (oils, viscous fluids)

## Output and Visualization

The simulation generates several types of output:

1. **Temperature Field**: Shows the thermal structure and convection cells
2. **Vorticity Field**: Displays the rotation of fluid elements
3. **Streamlines**: Visualizes the flow patterns
4. **Time Evolution**: Tracks temperature changes at specific points
5. **Animation**: Time-lapse of temperature field evolution

### Example Output Metrics

```
Final Nusselt number estimate: 4.23
Maximum vorticity: 12.345
RMS velocity: 0.1234
```

## Physical Applications

This simulation is relevant for studying:

- **Planetary Science**: Convection in planetary atmospheres and subsurface oceans
- **Geophysics**: Mantle convection and heat transfer in Earth's interior
- **Engineering**: Heat exchangers and thermal management systems
- **Astrophysics**: Convection in stellar atmospheres and accretion disks

## Algorithm Details

### Numerical Method
- **Spatial Discretization**: Central finite differences
- **Time Integration**: Explicit Euler method
- **Stability**: CFL condition automatically enforced
- **Pressure Solver**: Simplified pressure correction (can be improved with proper projection methods)

### Computational Complexity
- **Time Complexity**: O(N×M×steps) where N×M is grid size
- **Memory Complexity**: O(N×M) for field storage
- **Recommended Grid**: 128×64 for good balance of accuracy and speed

## Limitations and Future Improvements

### Current Limitations
- Explicit time stepping limits time step size
- Simplified pressure correction method
- 2D simulation only

### Potential Improvements
- Implement implicit time stepping for larger time steps
- Add proper pressure projection method
- Extend to 3D simulation
- Include non-Boussinesq effects
- Add adaptive mesh refinement

## Contributing

Contributions are welcome! Areas for improvement include:

1. **Numerical Methods**: Implementing more sophisticated solvers
2. **Physical Models**: Adding more complex physics
3. **Visualization**: Enhanced plotting and animation features
4. **Performance**: Optimization and parallelization
5. **Documentation**: Additional examples and tutorials

## License

This project is licensed under the MIT License - see below for details:

```
MIT License

Copyright (c) 2025 Saurabh Shukla

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## References

1. McKinnon, W. B., et al. (2016). Convection in a volatile nitrogen-ice-rich layer on Pluto. *Icarus*, 287, 2-11.

2. Morison, A., et al. (2021). Sublimation-driven convection in Sputnik Planitia on Pluto. *Nature*, 600(7889), 419-423.

3. Chandrasekhar, S. (1961). *Hydrodynamic and hydromagnetic stability*. Oxford University Press.

4. Getling, A. V. (1998). *Rayleigh-Bénard convection: structures and dynamics*. World Scientific.

## Contact

**Saurabh Shukla**  
Email: ss21@kgpian.iitkgp.ac.in  
Institution: Indian Institute of Technology Kharagpur

---

**Note**: This simulation is for educational and research purposes. For production applications, consider using more sophisticated computational fluid dynamics software.
