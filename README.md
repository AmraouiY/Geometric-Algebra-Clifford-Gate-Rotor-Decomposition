# Geometric Algebra Clifford Gate Rotor Decomposition

A Python implementation for decomposing arbitrary Clifford group elements into products of rotors in geometric algebra, with greedy algorithm optimization.

## Overview

This project explores the decomposition of Clifford group elements (unitary transformations in quantum computing) into basis rotors in geometric algebra. The implementation includes:

- **Pauli Blade arithmetic**: Geometric product computation with proper phase handling
- **Multivector algebra**: Linear combinations of Pauli blades with complex coefficients
- **Greedy decomposition algorithm**: Iteratively finds rotors that minimize support size
- **Comprehensive experiment suite**: Statistical analysis of decomposition properties across algebra dimensions

## Features

### Core Components

- `PauliBlade`: Represents basis elements in Clifford algebra with phase information (1, i, -1, -i)
- `Multivector`: General element of the Clifford algebra with complex-valued basis coefficients
- `rotor()`: Constructs normalized rotors for gate decomposition
- `greedy_decompose()`: Main algorithm for decomposing Clifford elements

### Experiments

- Generates random Clifford elements as products of rotors
- Applies greedy decomposition algorithm
- Collects metrics: decomposition length, convergence, runtime, reconstruction accuracy
- Produces visualization and statistical analysis

### Output

- `experiment_data.jsonl`: Detailed results for all trials (100 trials × 20 lengths × 4 dimensions)
- `appendix_table_statistics.json`: Aggregated statistics by dimension and initial length
- `metadata.json`: Experiment parameters and configuration

## Usage

### Running Experiments

```python
# Generate random Clifford element
original_clifford, generators = random_clifford(Pminus, length=20)

# Decompose using greedy algorithm
decomposition, sigmas = greedy_decompose(original_clifford, Pminus)

# Verify reconstruction
is_correct = check_reconstruction(original_clifford, decomposition)
```

### Analysis and Visualization

The notebook includes four main visualizations:

1. **Main Figure 1**: Average decomposition length vs initial rotor length (by dimension)
2. **Main Figure 2**: Support size trajectories showing convergence behavior
3. **Appendix Figure A1**: Runtime scaling analysis
4. **Appendix Figure A2**: Distribution of decomposition lengths (boxplots by dimension)

## Project Structure

```
├── Clifford_decomp_test.ipynb          # Main notebook with all code and analysis
├── experiment_data.jsonl               # Full experiment results (one JSON per line)
├── appendix_table_statistics.json      # Summary statistics table
├── metadata.json                       # Experiment configuration
├── README.md                           # This file
└── [Generated figures]                 # PNG outputs from analysis
```

## Requirements

- Python 3.8+
- matplotlib
- Standard library modules: dataclasses, collections, json, time, statistics

## Key Algorithms

### Swap Parity

Calculates the sign contribution from reordering basis elements:
```python
parity = swap_parity(mask_left, mask_right)
```

### Canonicalization

Separates phase from basis element to ensure consistent representation:
```python
key, coeff = canonicalize_blade(blade)
```

### Greedy Decomposition

At each step, selects the rotor that minimizes the support size (number of terms):
```python
decomposition, sigmas = greedy_decompose(A, Pminus, max_steps=1000)
```

## Experiment Parameters

- **N**: Number of trials per (n, L) configuration (default: 100)
- **L**: Maximum initial rotor length (default: 20)
- **n_values**: Clifford algebra dimensions tested (default: 1-4)
- **TOL**: Floating-point tolerance (default: 1e-10)

## Mathematical Background

The code implements operations in the geometric algebra (Clifford algebra) framework:
- Blades are basis elements of the form $e_{J} = e_{i_1} \cdots e_{i_k}$
- Multivectors are linear combinations of blades with complex coefficients
- The geometric product follows anticommutation relations: $e_i e_j + e_j e_i = 2\delta_{ij}$

## Results

The experiments investigate:
- How decomposition length scales with initial rotor length
- Support size convergence behavior across dimensions
- Algorithm runtime characteristics
- Success rates and reconstruction accuracy

## Author

Research implementation for geometric algebra and quantum gate decomposition.

## License

[Specify your license here if applicable]
