# CVRP Content Repository

## Structure
This repository contains all the content and resources for solving multiple variations of the Capacitated Vehicle Routing Problem (CVRP) as part of a structured learning project.

```
cvrp_content/
├── Proyecto_Caso_Base/
├── project_a/
├── project_b/
├── project_c/
└── helper/
```

## Folder Descriptions

### `Proyecto_Caso_Base/`
This folder contains the base CVRP case and **must be completed before attempting any of the project folders (A, B, or C)**. It provides the foundational structure and data needed to understand the problem, including CSV files with information on clients, vehicles, and depots.

### `project_a/`
This folder contains data and requirements for **Project A**, which extends the base CVRP to include multiple depots and limited stock at each depot. The dataset builds on the base case and introduces new constraints for modeling.

### `project_b/`
This folder includes the scenario and data for **Project B**, which introduces a **hybrid fleet of drones and ground vehicles**. The dataset provides additional attributes like drone speed, vehicle types, and energy parameters.

### `project_c/`
This folder contains the materials for **Project C**, where the base CVRP is extended with **refueling nodes, range limitations**, and **variable transportation costs**. This scenario requires integrating energy-aware optimization strategies.

### `helper/`
The `helper` folder contains utility scripts and tools that support all projects:
- Scripts to install a more powerful solver than GLPK (e.g., CBC or Gurobi if available).
- Visualization tools to help **plot realistic delivery maps and routes**.
- Helper functions for preprocessing, data validation, and performance logging.

---

## Instructions
1. **Start with `Proyecto_Caso_Base/`** and fully solve the base CVRP.
2. Once completed, got to the project that corresponds to your group (A, B, or C) and begin working on its extended version.
3. Use the `helper/` folder as needed to support your modeling, visualization, or performance improvements.

Each project is self-contained, but all are **built upon the foundational understanding developed in the base case.**

Happy modeling!