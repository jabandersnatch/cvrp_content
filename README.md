# CVRP Content Repository

## Overview

This repository contains all data, documentation, and resources for implementing three variants of the Capacitated Vehicle Routing Problem (CVRP) for **LogistiCo**, a fictional logistics company operating across Colombia.

## 🚀 Quick Start

**IMPORTANT**: You MUST complete the Base Case before attempting any project-specific cases.

### Step 1: Start with the Base Case

Navigate to `Proyecto_Caso_Base/` and solve the standard CVRP to validate your implementation.

### Step 2: Proceed to Your Assigned Project

Once the base case is working, move to your assigned project folder (A, B, or C).

## 📁 Repository Structure

```
cvrp_content/
├── Proyecto_Caso_Base/          ⭐ START HERE - Required for all groups
│   ├── README.md                Complete base CVRP documentation
│   ├── clients.csv              Client locations and demands
│   ├── vehicles.csv             Vehicle fleet specifications
│   ├── depots.csv               Distribution center location
│   └── parameters_base.csv      Reference cost parameters
│
├── project_a/                   🚚 Urban Logistics (Bogotá)
│   ├── Proyecto_A_Caso2/        Simplified: Multiple depots with inventory
│   │   ├── Readme.md            Detailed case documentation
│   │   ├── clients.csv          ~30 urban clients
│   │   ├── vehicles.csv         Mixed fleet (vans, trucks)
│   │   ├── depots.csv           3 distribution centers with capacity limits
│   │   └── parameters_urban.csv Cost parameters for urban operations
│   │
│   └── Proyecto_A_Caso3/        Advanced: 50-100 clients (bonus eligible)
│       ├── Readme.md            Advanced case with competitive bonus info
│       ├── clients.csv          50-100 urban clients
│       ├── vehicles.csv
│       ├── depots.csv
│       └── parameters_urban.csv
│
├── project_b/                   🚁 Rural/Offshore Logistics (La Guajira)
│   ├── Proyecto_B_Caso2/        Simplified: Hybrid fleet + time windows
│   │   ├── Readme.md            Drone & truck fleet documentation
│   │   ├── clients.csv          Remote communities with time windows
│   │   ├── vehicles.csv         Drones and 4x4 trucks
│   │   ├── depots.csv           Single operations depot
│   │   └── parameters_rural.csv Costs for hybrid fleet operations
│   │
│   └── Proyecto_B_Caso3/        Advanced: With resupply logic (bonus eligible)
│       ├── Readme.md            Resupply/re-stocking case documentation
│       ├── clients.csv          More clients requiring resupply strategy
│       ├── vehicles.csv
│       ├── depots.csv
│       └── parameters_rural.csv
│
└── project_c/                   🚛 National Logistics (Colombia-wide)
    ├── Proyecto_C_Caso2/        Simplified: Strategic refueling
    │   ├── Readme.md            Refueling stations case documentation
    │   ├── clients.csv          Municipalities across Colombia
    │   ├── vehicles.csv         Tractomula fleet
    │   ├── depots.csv           Port of Barranquilla (origin)
    │   ├── stations.csv         ⭐ Refueling stations with variable prices
    │   └── parameters_national.csv Long-haul transport costs
    │
    └── Proyecto_C_Caso3/        Advanced: + Tolls + Weight restrictions (bonus eligible)
        ├── Readme.md            Complete national logistics documentation
        ├── clients.csv          Municipalities with weight restrictions
        ├── vehicles.csv
        ├── depots.csv
        ├── stations.csv         Refueling stations
        ├── tolls.csv            ⭐ Toll plazas with weight-based pricing
        └── parameters_national.csv
```

## 📊 Project Breakdown

### Project A: Urban Logistics (Bogotá)

**Division**: LogistiCo Urban Logistics
**Challenge**: Last-mile delivery with multiple distribution centers
**Key Features**:

- Multiple depots with limited inventory capacity
- Heterogeneous vehicle fleet (small/medium vans, light trucks)
- Urban congestion and zone restrictions
- Depot capacity constraints

**Files**: `clients.csv`, `vehicles.csv`, `depots.csv`, `parameters_urban.csv`

### Project B: Rural/Offshore Logistics (La Guajira)

**Division**: LogistiCo Rural/Offshore Logistics
**Challenge**: Critical medical supply delivery to remote communities
**Key Features**:

- Hybrid fleet (drones + 4x4 trucks) with different cost structures
- HARD time windows (no penalties - infeasible if violated)
- Long distances to isolated locations
- Resupply logic in Caso 3 (vehicles can return to depot mid-route)
- Operations start at 07:45

**Files**: `clients.csv` (with TimeWindow), `vehicles.csv` (with Type, Speed), `depots.csv`, `parameters_rural.csv`

### Project C: National Logistics (Colombia)

**Division**: LogistiCo National Logistics
**Challenge**: Port-to-municipality cargo transport across Colombia
**Key Features**:

- Strategic refueling with variable fuel prices by station
- Toll system with base rate + weight-dependent costs (Caso 3)
- Municipal weight restrictions (Caso 3)
- Long-haul tractomula operations
- Dynamic weight tracking affects toll costs

**Files**: `clients.csv` (City/Municipality), `vehicles.csv`, `depots.csv`, `stations.csv`, `tolls.csv` (Caso 3), `parameters_national.csv`

## 🔑 Key Files Explained

### Standard Data Files (All Projects)

**clients.csv** - Delivery locations

- `ClientID`: Numeric identifier (1, 2, 3, ...)
- `StandardizedID`: For verification files (C001, C002, C003, ...)
- `LocationID`: Unified location identifier
- `Latitude`, `Longitude`: Geographic coordinates
- `Demand`: Cargo required (kg)
- Additional columns: `TimeWindow` (Project B), `City/Municipality` (Project C), `MaxWeight` (Project C Caso 3)

**vehicles.csv** - Fleet specifications

- `VehicleID`: Numeric identifier (1, 2, 3, ...)
- `StandardizedID`: For verification files (V001, V002, V003, ...)
- `Capacity`: Maximum load (kg)
- `Range`: Maximum distance (km)
- Additional columns: `Type`, `Speed` (Project B)

**depots.csv** - Distribution centers/ports

- `DepotID`: Numeric identifier (1, 2, 3, ...)
- `StandardizedID`: For verification files (CD01, CD02, CD03, ...)
- `LocationID`: Unified location identifier
- `Latitude`, `Longitude`: Geographic coordinates
- Additional: `Capacity` (Project A - inventory limit)

### Project-Specific Files

**stations.csv** (Project C) - Refueling stations

- `EstationID`, `StandardizedID` (E001, E002, ...), `LocationID`
- `Latitude`, `Longitude`, `FuelCost` (COP/gallon)
- **Key**: Fuel prices VARY - strategic refueling is critical!

**tolls.csv** (Project C Caso 3) - Toll plazas

- `TollID`, `StandardizedID` (P001, P002, ...), `LocationID`
- `TollName`, `BaseRate` (COP), `RatePerTon` (COP/ton)
- **Formula**: Total = BaseRate + (Weight_tons × RatePerTon)

**parameters\_[type].csv** - All cost function parameters

- Format: `Parameter,Value,Unit,Description`
- Contains: Fixed costs, distance costs, time costs, fuel prices, efficiency values
- **No need to search the PDF** - all values are here!

## 📋 Case Progression

### Caso 1: Base Case (15% of grade)

- **Location**: `Proyecto_Caso_Base/`
- **Purpose**: Validate core CVRP implementation
- **Features**: Single depot, homogeneous fleet, basic constraints
- **Required**: Must complete before Caso 2/3

### Caso 2: Simplified Project-Specific (25% of grade)

- **Purpose**: Introduce project-specific features
- **Complexity**: Moderate, focus on correctness
- **Deliverable**: `verificacion_caso2.csv`

### Caso 3: Advanced Realistic (20% of grade + 20% bonus potential)

- **Purpose**: Realistic scale with all features
- **Complexity**: High (50-100 clients for A, resupply for B, tolls+weights for C)
- **Bonus Eligible**: Top solutions can earn up to +20% additional points
- **Focus**: Scalability, business insights, computational efficiency
- **Deliverable**: `verificacion_caso3.csv` + comprehensive analysis

## ⚠️ Critical Information

### ID Standardization

**ALWAYS use StandardizedID format in verification files:**

- Clients: C001, C002, C003, ...
- Vehicles: V001, V002, V003, ...
- Depots: CD01, CD02, CD03, ...
- Stations: E001, E002, E003, ... (Project C)
- Tolls: P001, P002, P003, ... (Project C Caso 3)

Both numeric IDs and StandardizedID are provided in CSV files - use whichever is convenient for your code, but verification files MUST use StandardizedID.

### Unified Objective Function

All projects implement the same cost structure:

```
min Z = Σ(C_fixed × y_v) + Σ(C_dist × d_v) + Σ(C_time × t_v) + C_fuel + C_special
```

Where C_special = tolls for Project C, 0 for others.

### Verification Files

**Missing or incorrect verification files = significant grade penalty**

Each case requires a `verificacion_casoX.csv` file with specific format (see individual README files).

## 📖 Documentation

Each case folder contains a comprehensive `Readme.md` with:

- ✅ Detailed data file descriptions with units
- ✅ Cost parameters and objective function
- ✅ Project-specific constraints
- ✅ Verification file format with examples
- ✅ Visualization requirements
- ✅ Deliverables checklist
- ✅ Important notes and tips

**Start with the README in each folder - it has everything you need!**

## 🛠️ Getting Started

1. **Read the main project document** (`main.tex` or `main.pdf` in parent directory)
2. **Complete Base Case** (`Proyecto_Caso_Base/`)
3. **Choose your project** (A, B, or C) and read its Caso 2 README
4. **Load data** using provided CSV files
5. **Load parameters** from `parameters_[type].csv`
6. **Implement in Pyomo** following the unified cost function
7. **Create verification files** using StandardizedID format
8. **Visualize results** (maps with Folium, charts, etc.)
9. **Analyze and report** (sensitivity analysis, business insights for Caso 3)

## ✅ Solution Validation

The base case verification script validates your solutions with multiple distance calculation options:

```bash
cd Proyecto_Caso_Base

# Default: Haversine distance (fast, approximate)
python ../utils/base_case/base_case_verification.py --method haversine --verbose

# Geodesic distance via GeoPy (accurate)
python ../utils/base_case/base_case_verification.py --method geopy

# Road network distance via OSRM (realistic, requires internet)
python ../utils/base_case/base_case_verification.py --method osrm

# Precomputed distance matrix (fastest, most consistent)
python ../utils/base_case/base_case_verification.py --method matrix --matrix distances.json

# Custom solution filename
python ../utils/base_case/base_case_verification.py --solution my_solution.csv
```

### Distance Matrix Support

The validator supports precomputed distance matrices as an alternative to calculating distances on-the-fly. This is useful when:

- You have distances from optimization solvers (e.g., Google OR-Tools distance matrix API)
- You want consistent distances across multiple validation runs
- You're using real road network distances pre-calculated offline

#### JSON Format (Recommended)

Create a file with nested dictionaries:

```json
{
  "metadata": {
    "format_version": "1.0",
    "matrix_type": "symmetric",
    "distance_unit": "km",
    "description": "Precomputed distances for CVRP base case"
  },
  "distances": {
    "CD01": {
      "CD01": 0.0,
      "C001": 25.3,
      "C002": 18.7
    },
    "C001": {
      "CD01": 25.3,
      "C001": 0.0,
      "C002": 12.4
    },
    "C002": {
      "CD01": 18.7,
      "C001": 12.4,
      "C002": 0.0
    }
  }
}
```

**Metadata fields (all optional):**

- `format_version`: Version identifier (currently "1.0")
- `matrix_type`: "symmetric" or "asymmetric"
- `distance_unit`: Unit of distance (should be "km")
- `description`: Human-readable description

#### CSV Format (Alternative)

**Three-column format:**

```csv
Origin,Destination,Distance
CD01,CD01,0.0
CD01,C001,25.3
CD01,C002,18.7
C001,CD01,25.3
C001,C001,0.0
C001,C002,12.4
```

**Or traditional matrix format:**

```csv
,CD01,C001,C002
CD01,0.0,25.3,18.7
C001,25.3,0.0,12.4
C002,18.7,12.4,0.0
```

#### ID Format Requirements

**CRITICAL:** Distance matrices MUST use StandardizedID format:

- Depots: `CD01`, `CD02`, `CD03` (NOT "CDA", "1", or numeric)
- Clients: `C001`, `C002`, `C003`, ... (NOT "1", "2", or numeric)

The validator automatically converts legacy formats when looking up distances.

#### Example: Generating a Distance Matrix

```python
import pandas as pd
import json
import math

# Load data
clients = pd.read_csv("clients.csv")
depots = pd.read_csv("depots.csv")

def haversine(lat1, lon1, lat2, lon2):
    R = 6371  # Earth radius in km
    phi1, phi2 = math.radians(lat1), math.radians(lat2)
    dphi = math.radians(lat2 - lat1)
    dlambda = math.radians(lon2 - lon1)
    a = math.sin(dphi/2)**2 + math.cos(phi1) * math.cos(phi2) * math.sin(dlambda/2)**2
    return 2 * R * math.asin(math.sqrt(a))

# Build matrix
matrix = {
    "metadata": {"matrix_type": "symmetric", "distance_unit": "km"},
    "distances": {}
}

# Combine all locations
locations = []
for _, depot in depots.iterrows():
    locations.append((depot["StandardizedID"], depot["Latitude"], depot["Longitude"]))
for _, client in clients.iterrows():
    locations.append((client["StandardizedID"], client["Latitude"], client["Longitude"]))

# Calculate all pairs
for id1, lat1, lon1 in locations:
    matrix["distances"][id1] = {}
    for id2, lat2, lon2 in locations:
        distance = haversine(lat1, lon1, lat2, lon2)
        matrix["distances"][id1][id2] = round(distance, 2)

# Save
with open("distances.json", "w") as f:
    json.dump(matrix, f, indent=2)
```

#### Troubleshooting

**Error: "Distance not found: CD01 → C001"**

- Check that both origin and destination use StandardizedID format
- Ensure your matrix includes all depots and clients from the CSV files
- For symmetric matrices, verify both directions are present

**Error: "Distance matrix file not found"**

- Verify the file path is correct
- Use absolute paths or paths relative to current working directory

**Error: "--matrix argument is required when using --method matrix"**

- You must provide `--matrix <filename>` when using `--method matrix`

## 💡 Tips for Success

- **Start simple**: Get Caso 1 working perfectly before moving on
- **Read the README**: Each case has detailed documentation - use it!
- **Use parameters files**: All cost values are provided in CSV format
- **Test incrementally**: Don't try to solve everything at once
- **Check StandardizedID**: Verification files must use the correct ID format
- **Document everything**: Especially for Caso 3 bonus eligibility
- **Visualize well**: Good maps and charts communicate your solution effectively

## 📞 Support

- Check README files in each case folder first
- Consult `ProyectoEtapa2.pdf` for complete project specifications
- Submit questions via course platform Discord

---

**Good luck with your optimization project! 🚀**

Remember: The base case is your foundation - make sure it works before adding complexity!
