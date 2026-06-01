# DARP

This repository is a C++ implementation for the paper <a href="[https://doi.org/10.1080/21680566.2025.2552884](https://www.sciencedirect.com/science/article/pii/S2352146525002613)">Joint Design of Conventional Public Transport Network and Mobility on Demand
</a>. The project focuses on an integrated dial-a-ride setting where users may combine walking, public transport, and ride-sharing services.

The method optimizes public transport line design and ride-sharing operations using Particle Swarm Optimization (PSO), Large Neighborhood Search (LNS), and Integrated Dial-a-Ride Problem (IDARP) modeling.

## Overview

Conventional public transport can be inefficient in low-demand areas, where fixed routes and high coverage may lead to high operating costs and low service quality. Mobility-on-demand and ride-sharing services can complement public transport by serving first-mile and last-mile connections.

This project studies a multimodal transport system composed of:

* Walking
* Public transport
* Ride sharing
* Integrated trips such as Walk → Public Transport → Ride Sharing
* Integrated trips such as Ride Sharing → Public Transport → Walk

The optimization framework jointly considers:

* Stop activation and deactivation
* Public transport line usage
* Ride-sharing vehicle routing
* User assignment to different transport modes
* Operational cost and service quality indicators

## Repository Structure

```text
.
├── input/                         # Input data files
├── result/                        # Output result files
├── definitions.h                  # Global definitions and compilation settings
├── YvesCalculator.h               # Helper calculations
├── project08-07_reconstruct.cpp   # Main C++ source code
├── python_script.py               # Script for running multiple experiments
├── idarp.exe                      # Compiled executable
└── README.md
```

## Compilation

The code can be compiled in either sequential or parallel mode.

To enable parallel mode, open `definitions.h` and set:

```cpp
#define PARALLEL_MODE 1
```

To disable parallel mode, set:

```cpp
#define PARALLEL_MODE 0
```

Parallelization is implemented using OpenMP.

### Linux

To compile on Linux:

```bash
g++ --std=c++17 -g -fopenmp project08-07_reconstruct.cpp -o idarp
```

If your source file uses a different capitalization, adjust the filename accordingly.

### macOS and Windows

For macOS or Windows, use the equivalent C++17 compilation command and make sure OpenMP is correctly installed and linked.

For example, on macOS with Homebrew LLVM, you may need to use `clang++` or `g++` from Homebrew and explicitly link OpenMP.

## Run

An example command is:

```bash
./idarp.exe input/one_hundred_cust.txt input/ListeOfLocations_10000_Cust.txt input/Discretisation_10000_Cust.txt input/load_file.txt 1.5
```

The last argument is the maximum tolerating coefficient.

Depending on your operating system and compilation output, the executable may be called `idarp` instead of `idarp.exe`:

```bash
./idarp input/one_hundred_cust.txt input/ListeOfLocations_10000_Cust.txt input/Discretisation_10000_Cust.txt input/load_file.txt 1.5
```

## Run Multiple Experiments

To run a series of experiments using the Python script:

```bash
python python_script.py
```

## Input Files

The example run uses the following input files:

```text
input/one_hundred_cust.txt
input/ListeOfLocations_10000_Cust.txt
input/Discretisation_10000_Cust.txt
input/load_file.txt
```

These files define the customer requests, locations, discretization settings, and loading information required by the optimization model.

## Output Files

The program writes experiment results to the `result/` directory.

### `Graphic1.txt`

Contains the number of vehicles of the global best particle at each iteration.

### `Graphic2.txt`

Contains the average travel time for each rider of the global best particle at each iteration.

### `Graphic3.txt`

Contains the number of vehicles in each line at each PSO iteration for the best particle of that iteration.

### `Graphic4.txt`

Contains the waiting time for each line across iterations for the best particle.

### `Graphic5.txt`

Contains the number of active stations in each line across iterations for the global best solution.

### `Graphic6.txt`

Contains the number of riders in each rider type at each iteration.

Rider types include:

* `R_W_PT_RS`: riders using Walk → Public Transport → Ride Sharing
* `R_RS_PT_W`: riders using Ride Sharing → Public Transport → Walk
* `R_PT`: riders using public transport
* `R_RS`: riders using ride sharing
* `walk`: riders who only walk

### `Graphic7.txt`

Visualizes the average travel time in public transport and ride sharing from one zone to another across iterations.

### `Graphic8.txt`

Visualizes the number of users of each line.

See the functions:

```text
Visualize_Number_of_users_of_each_line_1
Visualize_Number_of_users_of_each_line_2
```

### `Graphic12.txt`

Records each particle's performance at each iteration.

### `Graphic15.txt`

Records the number of active stations in each line of the global best solution.

### `Graphic19.txt`

Contains the number of riders in each line from one zone to another zone.

## Visualization

The repository includes two visualization options.

### Excel Visualization

```text
plot.xlsx
```

This file can be used to visualize the numerical results generated in the `result/` directory.

### JavaScript Visualization

```text
javascript_visualization/index.html
```

This page visualizes the locations of active and inactive stations.

## Methods

This project combines several optimization components:

* **Particle Swarm Optimization (PSO)** for public transport network design
* **Large Neighborhood Search (LNS)** for ride-sharing routing
* **Integrated Dial-a-Ride Problem (IDARP)** modeling for multimodal user trips
* **OpenMP** for optional parallel computation

## Applications

This framework can be used to study:

* Public transport redesign
* Mobility-on-demand integration
* First-mile and last-mile transport services
* Ride-sharing fleet operations
* Multimodal transport network design
* Operational cost reduction in low-demand public transport systems

## Citation

If you use this code, please cite the following paper:

@article{wu2025joint,
  title={Joint Design of Conventional Public Transport Network and Mobility on Demand},
  author={Wu, X. and Mouhrim, N. and Araldo, A. and Molenbruch, Y. and Feillet, D. and Braekers, K.},
  journal={Transportation Research Procedia},
  volume={86},
  pages={104--112},
  year={2025},
  doi={10.1016/j.trpro.2025.04.014},
  url={https://www.sciencedirect.com/science/article/pii/S2352146525002613}
}

Paper: Joint Design of Conventional Public Transport Network and Mobility on Demand

## Contact

Xiaoyi Wu
Technical University of Denmark
Email: [xiawu@dtu.dk](mailto:xiawu@dtu.dk)
