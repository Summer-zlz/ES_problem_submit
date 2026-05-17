# Energy System Optimization with MPEC and Gurobi

This project implements an energy system optimization model using MPEC (Mathematical Programs with Equilibrium Constraints) framework and Gurobi solver. The model incorporates typical days, wind generation, gas generators, and energy storage systems to optimize day-ahead and real-time market bidding strategies.

## Project Structure

### Files Overview

- **model.ipynb** - Main optimization workflow

  - Loads demand data and wind generation parameters
  - Constructs the MPEC optimization model
  - Solves using Gurobi solver
  - Saves optimization results to output files for visualization
- **figure.ipynb** - Visualization and analysis

  - Reads results from model.ipynb
  - Generates plots and charts for result analysis
  - Produces summary reports and statistics
- **requirements.txt** - Python dependencies

  - Contains all required libraries for running the project
  - See "Installation" section below

### Input Data Files

- **demand_data.csv** - Electricity demand data

  - Format: 24 hourly demand values per typical day
  - Data source: Australian NEM (National Electricity Market) NSW region
  - Averaged from 5-minute resolution data from Jan/Apr/Jul/Oct 2025
- **para_generation_typical_days.xlsx** - Wind generation parameters

  - Contains: Time index, generator parameters, power output (Volume)
  - 4 typical days × 24 hours = 96 rows of wind turbine data
  - Real-time and forecast power output values

## Installation

1. Ensure Python 3.11+ is installed
2. Install required dependencies:

   ```bash
   pip install -r requirements.txt
   ```
3. Install Gurobi solver (commercial solver required for optimization):

   - Download from: https://www.gurobi.com/
   - License required (free academic licenses available)

## Usage

### Step 1: Run Optimization Model

Open and run **model.ipynb** in Jupyter Notebook:

```bash
jupyter notebook model.ipynb
```

This notebook will:

- Load `demand_data.csv` and `para_generation_typical_days.xlsx`
- Build the MPEC model with typical days, gas generators, wind turbines, and storage units
- Solve optimization problem using Benders decomposition
- Save results (optimal investments, bidding decisions, profits) to output files

### Step 2: Visualize Results

Open and run **figure.ipynb** in Jupyter Notebook:

```bash
jupyter notebook figure.ipynb
```

This notebook will:

- Load optimization results from model.ipynb outputs
- Generate visualization plots and analysis charts
- Display summary statistics and performance metrics

## Model Overview

### Key Components

- **Typical Days**: 4 representative days (each with equal 0.25 weight)
- **Storage Systems**:
  - s1: Energy-type battery
  - s2: Power-type battery
- **Wind Generators**: 4 wind turbines (w1-w4) with forecast and real-time data
- **Gas Generators**: 8 thermal units (g1-g8) with varying costs and capacities
- **Time Horizon**: 24-hour period per typical day

### Key Parameters

- SOC range: 5% - 95% of capacity
- Charging/Discharging efficiency: 95%
- Reserve requirements: 5% of demand + 3% of wind forecast
- Optimization objective: Maximize profit from energy and reserve markets

## Output Files

Optimization results are saved to:

- Investment decisions (storage capacity allocation)
- Day-ahead market bidding quantities
- Real-time market adjustments
- Profit breakdown and financial metrics

## Requirements

- Python 3.11+
- Pyomo 6.4+ (optimization modeling framework)
- Gurobi solver (commercial license required)
- Pandas, NumPy, Matplotlib (data processing and visualization)

See `requirements.txt` for complete dependency list.

## References

- Pyomo Documentation: https://pyomo.readthedocs.io/
- Gurobi Solver: https://www.gurobi.com/
- AEMO Data: https://www.aemo.com.au/

## Notes

- Model requires Gurobi solver with valid license for optimization
- Input data files (CSV and XLSX) must be in the same directory as notebooks
- Typical day weights can be modified in model.ipynb for sensitivity analysis
- Computation time depends on model size and solver performance
