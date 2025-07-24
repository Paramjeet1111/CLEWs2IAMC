# CLEWs2IAMC

CLEWs2IAMC is a Python toolkit that automates the conversion of (Climate, Land, Energy and Water ) CLEWs model inputs and results into IAMC-compliant Excel files  by Using YAML configuration files, it flexibly maps various result types (e.g., investment, emissions, demand, capacity, technology use) from CSVs to the IAMC format. The tool supports both Jupyter notebook and command-line workflows, and relies on osemosys2iamc for processing and configuration.

## Project Structure

```
CLEWs2IAMC/
├── Config/
│   ├── Config_capitalInvestment_results.yaml
│   ├── config_demand_results_Input.yaml
│   ├── config_demand_results.yaml
│   ├── Config_emissions_results.yaml
│   ├── config_file - Copy.yml
│   ├── config_input.yaml
│   ├── config_new_capacity_results.yaml
│   ├── config_prod_tech_result.yaml
│   ├── config_result.yml
│   ├── Config_TotalCapacity_results.yaml
│   ├── config_usebytech_results.yaml
│   └── crop_yield_results.yaml
├── Ethiopia/                           # Results directory
│   ├── AnnualTechnologyEmission.csv
│   ├── CapitalInvestment.csv
│   ├── Demand.csv
│   ├── NewCapacity.csv
│   ├── ProductionByTechnologyByMode.csv
│   ├── TotalCapacityAnnual.csv
│   └── UseByTechnologyByMode.csv
├── inputs_path/                        # Input data directory
│   ├── AccumulatedAnnualDemand.csv
│   ├── Annual_average_ws_score.csv
│   ├── AnnualEmissionLimit.csv
│   ├── AvailabilityFactor.csv
│   ├── BHI.csv
│   ├── CapacityFactor.csv
│   ├── CapacityOfOneTechnologyUnit.csv
│   ├── CapacityToActivityUnit.csv
│   ├── CapitalCost.csv
│   ├── CapitalCostStorage.csv
│   ├── COMMODITY.csv
│   ├── Conversionld.csv
│   ├── Conversionlh.csv
│   ├── Conversionls.csv
│   ├── Crop_IDR.csv
│   ├── Crop_Yield.csv
│   ├── DAILYTIMEBRACKET.csv
│   ├── DaysInDayType.csv
│   ├── DaySplit.csv
│   ├── DAYTYPE.csv
│   ├── DiscountRate.csv
│   ├── DiscountRateIdv.csv
│   ├── EMISSION.csv
│   ├── EmissionActivityRatio.csv
│   ├── EmissionsPenalty.csv
│   ├── EmissionToActivityChangeRatio.csv
│   ├── FixedCost.csv
│   ├── Forest_cover.csv
│   ├── Harvested_area.csv
│   ├── HM_area.csv
│   ├── InputActivityRatio.csv
│   ├── InputToNewCapacityRatio.csv
│   ├── InputToTotalCapacityRatio.csv
│   ├── Irrigated_area.csv
│   ├── MinStorageCharge.csv
│   ├── MODE_OF_OPERATION.csv
│   ├── ModelPeriodEmissionLimit.csv
│   ├── Net_emissions.csv
│   ├── OperationalLife.csv
│   ├── OperationalLifeStorage.csv
│   ├── OutputActivityRatio.csv
│   ├── REGION.csv
│   ├── Relative_annual_water_demand.csv
│   ├── ResidualCapacity.csv
│   ├── ResidualStorageCapacity.csv
│   ├── SEASON.csv
│   ├── SpecifiedAnnualDemand.csv
│   ├── SpecifiedDemandProfile.csv
│   ├── STORAGE.csv
│   ├── STORAGEINTRADAY.csv
│   ├── STORAGEINTRAYEAR.csv
│   ├── StorageLevelStart.csv
│   ├── TECHNOLOGY.csv
│   ├── TechnologyActivityByModeLowerLimit.csv
│   ├── TechnologyActivityByModeUpperLimit.csv
│   ├── TechnologyActivityDecreaseByModeLimit.csv
│   ├── TechnologyActivityIncreaseByModeLimit.csv
│   ├── TechnologyFromStorage.csv
│   ├── TechnologyToStorage.csv
│   └── TIMESLICE.csv
├── output_path/                        # IAMC format output directory
└── Ethiopia.ipynb                      # Main notebook for processing

```

## Description

This project provides a framework for converting CLEWs (Climate, Land-use, Energy and Water ) model results and Inputs into the IAMC (Integrated Assessment Modeling Consortium) format. It includes configuration files for different types of results and Inputs and a processing pipeline implemented in Python.

## Prerequisites

- Python 3.x
- Jupyter Notebook

## Dependencies

The project requires the following Python packages:

- `osemosys2iamc` - Main package for conversion
- `pandas` - For data manipulation
- `pyyaml` - For reading configuration files
- `subprocess` - For running command-line operations

## Installation

1. Clone this repository
2. Install required packages:
```bash
pip install osemosys2iamc pandas pyyaml
```

## Usage

1. Place your OSeMOSYS model results in the `Ethiopia/` directory
2. Configure the appropriate YAML files for the type of results you want to convert
3. Run the conversion using either:
   - The Jupyter notebook `Ethiopia.ipynb`
   - Command line interface:
     ```bash
     osemosys2iamc <input_path> <results_path> <config_file> <output_file>
     ```

## Configuration Files

The project includes several configuration files for different types of results (located in the `Config/` directory):

- `Config_capitalInvestment_results.yaml` - For capital investment data
- `config_demand_results.yaml` - For demand-related results
- `Config_emissions_results.yaml` - For emissions data
- `config_new_capacity_results.yaml` - For new capacity additions
- `Config_TotalCapacity_results.yaml` - For total capacity data
- `config_usebytech_results.yaml` - For technology utilization data
- `crop_yield_results.yaml` - For agricultural yields

## Input Data Structure

The `inputs_path/` directory contains all necessary input files for the OSeMOSYS model, organized into:

- Model Parameters (technical and economic parameters)
- Sets (model dimensions and categories)
- Additional Data (supplementary data for CLEWs analysis)

## Output

The converted results in IAMC format are stored in the `output_path/` directory as Excel files.

## License

MIT License

## Contributors

**[S PARAMJEET SINGH](https://github.com/Camilogiu)** - Developer  
**Francesco Gardumi** - Supervisor  
**Camilla Lo Giudice** - Co-supervisor

## Acknowledgements
- [osemosys2iamc](https://github.com/OSeMOSYS/osemosys2iamc)
- [OSeMOSYS](https://www.osemosys.org/)
- [Indicators4CLEWs](https://github.com/Camilogiu/Indicators4CLEWs/)
- MUIO OSeMOSYS User Interface
- [IAMCOMPACT](https://www.iam-compact.eu/) project has received funding from the European Union's HORIZON EUROPE Research and Innovation Programme under grant agreement No 101056306