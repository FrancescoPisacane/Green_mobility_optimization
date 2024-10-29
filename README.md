# Strategic Optimization for EV Charging Stations Installation

This project aims to optimize the placement of electric vehicle (EV) charging stations across specific Points of Interest (POIs), minimizing installation costs while adhering to energy consumption constraints between consecutive stations. The approach uses graph analysis with `networkx` for visualization and `mip` for linear programming to determine the optimal POIs for installation.

## Project Overview

The project addresses two main objectives:
1. **Cost Minimization**: Minimize the total installation cost of charging stations across selected POIs.
2. **Energy Consumption Constraints**: Ensure that the energy consumption between any two consecutive stations does not exceed a specified threshold, requiring at least one station within certain ranges.

Two optimization scenarios are presented, resulting in slightly different placements due to varying consumption data.

## Key Components and Methodology

1. **Graph Representation**: Using `networkx`, the POIs and energy consumption constraints are represented as nodes and edges in a directed graph. This allows for visual analysis and straightforward representation of constraints.

2. **Linear Programming Model**: Built with `mip`, the model includes:
   - **Variables**: Binary variables representing whether a station is installed at each POI.
   - **Constraints**: A key constraint ensuring that the energy consumption between two consecutive stations does not exceed a maximum value. This is mathematically represented as:
     \[
     \sum_{i < k < j} x_k \geq \frac{1}{1000} * (d_{i, j} - \Delta)
     \]
   - **Objective Function**: The objective is to minimize installation costs, defined as:
     \[
     \min{\sum_{i \in H} x_i * c_i}
     \]
     where \( c_i \) represents installation costs at each POI.

3. **Optimization Process**:
   - The model uses `mip` to identify the minimum-cost configuration while satisfying the energy constraints.
   - After optimization, results are displayed graphically, with POIs where stations are installed highlighted in green.

## Results Summary

The two scenarios yield different solutions due to variations in energy consumption data. This is demonstrated by slightly different configurations for each scenario, emphasizing how data inputs (e.g., terrain morphology) influence the optimal installation strategy.

### Scenario 1
- **Stations Installed**: 8
- **Total Cost**: 12348
- **Installed at POIs**: 2', 4', 5', 7', 8', 10', 12', 14'

### Scenario 2
- **Stations Installed**: 8
- **Total Cost**: 12924
- **Installed at POIs**: 2', 4', 5', 6', 8', 10', 12', 13'

## Code Explanation

1. **Graph Visualization**:
   - The nodes (POIs) and edges (energy consumption constraints) are visualized using `networkx`.
   - Nodes are assigned coordinates and edge weights, then displayed with color-coded POIs (green for installations).

2. **Optimization Model**:
   - **Variables**: Each POI has a binary variable indicating station installation.
   - **Constraints**: Ensures no excessive energy consumption between consecutive stations.
   - **Objective Function**: Minimizes total installation cost based on linear programming.

3. **Final Visualization**:
   - The solution is plotted on the graph, highlighting the POIs with stations in green for easy interpretation.

This project showcases a practical approach to optimizing EV charging station placements with cost and energy constraints, providing a scalable solution adaptable to real-world scenarios.
