# Floyd–Warshall Route Optimization for Chennai Neighbourhoods

This project implements an end-to-end route optimization workflow using the Floyd–Warshall all-pairs shortest path algorithm. The goal is to compute minimum-distance routes between Chennai neighbourhoods, validate them using machine-learning regression, and visualize selected paths on an interactive Folium map.

The project uses a cleaned neighbourhood dataset (Chennai_neighbourhood_cleaned.csv) as the node set and builds an adjacency matrix to run Floyd–Warshall.

Project Overview
1. Data Loading & Exploration

Load cleaned neighbourhood dataset using Pandas.

Inspect structure and metadata (info(), sampling rows).

This dataset defines:

Node names (locations)

Latitude–longitude pairs

Distance values used for adjacency matrix generation

2. Adjacency Matrix Generation

A custom function constructs an adjacency matrix from the neighbourhood dataset:

Each location becomes a node.

Pairwise distances fill the matrix.

Non-connected nodes are assigned ∞.

This matrix becomes the input for the Floyd–Warshall algorithm.

3. Floyd–Warshall Algorithm Implementation

A complete implementation is provided to compute:

Shortest-path distance matrix

Next-node matrix (for path reconstruction)

Outputs:

shortest_paths_df — DataFrame of final minimum distances

A utility function to reconstruct and print the optimal route between any two nodes

4. Machine Learning Component

A simple regression model (Sklearn) is used to learn the relationship between:

Input features → Encoded node pairs (start, end)

Target → Floyd–Warshall shortest path distance

Pipeline includes:

Feature creation from node indices

Train–test split

Model fitting and prediction

Sample outputs to verify correctness

This serves as a proof-of-concept for ML-assisted route prediction.

5. Route Visualization (Folium)

The project includes an interactive map-plotting function using Folium:

Input: start location, end location

Internally queries shortest-path matrix

Plots:

Markers for each step

Polyline connecting the optimal route

Displays the map inside Jupyter Notebook

This helps visualize the computed optimal path directly on a map of Chennai.

Folder Structure
/project
│
├── floyds-1.ipynb                 # Main notebook
├── Chennai_neighbourhood_cleaned.csv
└── README.md                      # (This file)

Technologies Used

Python

NumPy — matrix operations

Pandas — data processing

Floyd–Warshall Algorithm — APSP

Scikit-learn — regression model

Folium — map visualization

Seaborn / Matplotlib — EDA plots

How to Run

Install required libraries:

pip install pandas numpy seaborn matplotlib folium scikit-learn


Open the Jupyter notebook:

jupyter notebook floyds-1.ipynb


Run the notebook sequentially.

Key Functions
generate_adjacency_matrix(df)

Builds an adjacency matrix from neighbourhood dataset.

floyd_warshall(adj_matrix)

Implements APSP and returns:

shortest_dist

next_node

predict_shortest_path(start, end)

Uses ML model to estimate distance.

show_shortest_path_map(start, end)

Displays interactive Folium route visualization.

Example Usage
start = "Adyar"
end = "Velachery"

show_shortest_path_map(start, end)

Future Extensions

Real-time traffic integration

Dijkstra-based dynamic routing

API deployment (FastAPI / Flask)

Multi-objective optimization (time, distance, cost)
