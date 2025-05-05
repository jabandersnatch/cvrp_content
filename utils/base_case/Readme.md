# Vehicle Routing Solution Validator

This tool validates vehicle routing solutions by checking route feasibility, capacity constraints, range limitations, and proper client coverage.

## Features

- Validates vehicle routing solutions against capacity and range constraints
- Supports multiple distance calculation methods:
  - **Haversine**: Simple great-circle distance calculation
  - **GeoPy**: Distance calculation using the geodesic method
  - **OSRM**: Real road distances using the Open Source Routing Machine API
- Caches distance calculations to improve performance
- Comprehensive error reporting
- Command-line interface for flexibility

## Installation

### Requirements

```bash
pip install pandas geopy requests
```

### File Structure

Your directory should contain:

- `solution.csv` - The routing solution to validate
- `vehicles.csv` - Vehicle specifications
- `clients.csv` - Client information with coordinates and demands
- `depots.csv` - Depot information with coordinates
- `base_case_verification.py` - The validation script

## Usage

### Basic Usage

```bash
# Validate using Haversine distance (default)
python base_case_verification.py

# Validate using GeoPy distance
python base_case_verification.py --method geopy

# Validate using OSRM API (requires internet connection)
python base_case_verification.py --method osrm

# Specify custom cache file
python base_case_verification.py --cache my_cache.json

# Verbose output
python base_case_verification.py --verbose
```

## Command Line Arguments

| Argument    | Description                                                | Default               |
| ----------- | ---------------------------------------------------------- | --------------------- |
| `--method`  | Distance calculation method (`haversine`, `geopy`, `osrm`) | `haversine`           |
| `--cache`   | Path to distance cache file                                | `distance_cache.json` |
| `--verbose` | Show detailed output                                       | False                 |

## Distance Calculation Methods

### 1. Haversine

- **Pros**: Fast, no external dependencies, offline
- **Cons**: Calculates straight-line distance, not actual road distance
- **Best for**: Quick validation, offline environments

### 2. GeoPy

- **Pros**: More accurate than Haversine for geodesic calculations
- **Cons**: Still not road distance, requires GeoPy library
- **Best for**: When you need more accurate geodesic calculations

### 3. OSRM

- **Pros**: Calculates actual road distances, most accurate
- **Cons**: Requires internet connection, slower (even with caching)
- **Best for**: Final validation, when actual driving distances are critical

## Input File Formats

### solution.csv

```csv
VehicleId,DepotId,InitialLoad,RouteSequence,ClientsServed,DemandsSatisfied,TotalDistance,TotalTime,FuelCost
VEH001,CD1,130,CD1-C001-C002-C003-CD1,3,50-30-20,100.5,300.2,5000
```

### vehicles.csv

```csv
VehicleID,Capacity,Range
1,100,200
2,150,250
```

### clients.csv

```csv
ClientID,LocationID,Demand,Longitude,Latitude
1,2,50,-74.09893,4.59795
2,3,30,-74.07557,4.68782
```

### depots.csv

```csv
LocationID,DepotID,Longitude,Latitude
1,1,-74.153536,4.743359
```

## Validation Checks

The validator performs the following checks:

1. **Route Integrity**: Ensures routes start and end at the correct depot
2. **Capacity Constraints**: Verifies initial load doesn't exceed vehicle capacity
3. **Range Constraints**: Checks if total route distance is within vehicle range
4. **Complete Coverage**: Ensures all clients are visited exactly once
5. **Demand Fulfillment**: Verifies correct demand amounts are delivered
6. **No Duplicate Visits**: Prevents teleportation or subtours

## Output

The validator provides clear feedback:

```
SOLUTION IS FEASIBLE!
All routes satisfy the requirements.
```

Or in case of errors:

```
SOLUTION IS INFEASIBLE!
Errors found:
- Route VEH001 exceeds capacity: 150 > 130
- Client C005 was not visited
- Route VEH002 has duplicate client visits
```

## Performance Tips

- Use `--method haversine` for quick validation
- The cache file speeds up repeated validations significantly
- For final validation, use `--method osrm` for accurate road distances

## Troubleshooting

### Common Issues

1. **"Location not found" errors**: Check that client IDs in RouteSequence match the format in clients.csv
2. **OSRM API timeouts**: Fallback to Haversine is automatic, but slow network may cause delays
3. **File not found errors**: Ensure all required CSV files are in the working directory

### Debug Output

Use `--verbose` flag for additional information during validation.
