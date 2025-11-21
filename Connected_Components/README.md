# Connected Components Detection - Parallel Graph Algorithm

A high-performance C implementation for detecting connected components in sparse graphs using multiple parallelization strategies. This project implements the **Coloring/Label-Propagation Algorithm** for identifying connected components in large undirected graphs from the SuiteSparse Matrix Collection.

## Description

This is an implementation of the Coloring Algorithm for finding connected components (CC) in undirected graphs. A connected component is a maximal subgraph in which there is a path from each vertex to any other vertex in the subgraph.

The project provides four different implementations to compare performance:

- **Sequential (CC)**: Single-threaded baseline implementation
- **OpenMP**: Parallel implementation using OpenMP directives
- **Cilk**: Parallel implementation using Intel OpenCilk
- **Pthreads**: Manual thread management using POSIX threads

## Algorithm

The algorithm:
1. Initializes each vertex with a unique color (label)
2. Iteratively propagates the minimum color to all neighbors
3. Repeats until no colors change (convergence)
4. Counts unique colors to determine the number of connected components

The algorithm converges when every vertex has the smallest label present in its connected component.

## Features

- **Matrix Market Support**: Reads sparse matrices from standard Matrix Market (.mtx) files
- **COO to CSR Conversion**: Efficient conversion from Coordinate (COO) format to Compressed Sparse Row (CSR) format for memory-efficient graph representation
- **Multiple Parallel Implementations**: Compare different parallelization strategies (OpenMP, OpenCilk, PThreads)
- **Performance Timing**: Accurate timing measurements using `clock_gettime()`
- **Large Graph Support**: Designed to process large undirected graphs from the SuiteSparse Matrix Collection

## Building

### Requirements
- GCC compiler with OpenMP support (for OpenMP version)
- Clang compiler with OpenCilk support (for Cilk version)
- GCC compiler with pthread support (for sequential and pthread versions)

### Compilation

First, navigate to the project directory:
```bash
cd reader-converter-main
```

Then compile the desired version:

```bash
# To build all versions
make compile

# To run all versions automatically (each prints its method name):
make run

# To clean all executables:
make clean


### Example

```bash
make run
```

**Output:**
```
Graph: my_graph.mtx
nzz  : 1234
rows : 567

Number of connected components: 5
~ CC duration: 0.123456 seconds
```

## Configuration

### Thread Count
- **OpenMP**: Modify `thread_num` variable (default: 16)
- **Pthreads**: Modify `num_threads` variable (default: 16)
- **OpenCilk**: Set in Makefile via CIlK_NWORKERS (default: 16)

```c
int thread_num = 16;  // Adjust based on your CPU cores
```

## Limitations

- Does not support directed graphs
- Assumes the graph fits in memory