# CLEWs2IAMC

CLEWs2IAMC is a Python toolkit that automates the conversion of (Climate, Land, Energy and Water ) CLEWs model inputs and results into IAMC-compliant Excel files by Using YAML configuration files, it flexibly maps various result types (e.g., investment, emissions, demand, capacity, technology use) from CSVs to the IAMC format. The tool supports both Jupyter notebook and command-line workflows, and relies on osemosys2iamc for processing and configuration.

## Project Structure

```
CLEWs2IAMC/                             
├── Config/                             # Config data directory
├── inputs_path/                        # CLEWs Input data directory
├── result_path/                        # CLEWs Result data directory
├── output_path/                        # IAMC format output directory
└── Main.ipynb                          # Main notebook for processing

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
1. Install Anaconda: https://www.anaconda.com/products/distribution

2. Clone this repository

## Usage

1. Place your CLEWs model Inputs and results in the `respective` directory
2. Configure the appropriate YAML files for the type of results you want to convert
3. Paste respective paths
4. Run the conversion using:
   - The Jupyter notebook `MAIN.ipynb`

### Overview

This tool, implemented in `resultify.py`, converts CLEWs model results and inputs into the IAMC (Integrated Assessment Modeling Consortium) format. It processes input and result CSV files based on a configuration file (`config.yaml`) and outputs the results as an Excel file in IAMC format.

## Configuration File (`config.yaml`)

The `config.yaml` file defines how CLEWs input and result data are mapped to IAMC variables. It specifies the model, scenario, region, and data processing rules for inputs and results, including filtering by technologies, fuels, or emissions, and applying transformations.

#### Creating Regex Expressions for Mapping

Regular expressions (regex) are used in the configuration file to filter and map technologies fuels into IAMC reporting formats. Each regex targets specific patterns in the code to identify technologies like wind (WI), hydro (HY), gas (NG), or solar (SO). These filters help categorize and map technologies and fuels correctly.

| Regex       | Example Codes       | Explanation                                                                 |
|-------------|---------------------|-----------------------------------------------------------------------------|
| `^PWRGAS$`  | PWRGAS              | Matches only if the code is exactly "PWRGAS" (used for gas power plant).   |
| `^.{2}(WI)` | DKWI00X00, SEWI01I00| Matches codes where "WI" is in the 3rd–4th position (likely Wind technologies). |
| `^.{2}(HY)` | DEHY01I00, FRHY12X00| "HY" at 3rd–4th position (likely Hydro technologies).                      |
| `^PWRTRN$`  | PWRTRN              | Matches only if the code is exactly "PWRTRN" (used for power transmission).|

#### YAML Examples for Mapping IAMC Variables

Below are Simple Regex examples of YAML configurations for mapping:

```yaml
# Agricultural diesel combustion CO2-equivalent emissions
- iamc_variable: 'Emissions|CO2|Energy|Demand|AFOFI'
  tech_emi: ["^DEMAGRDSL$"]
  emissions: [CO2]
  unit: Mt CO2/yr
  transform: abs
  osemosys_param: "AnnualTechnologyEmission"

# Mapping land use for forest cover based on technology and fuel usage.
- iamc_variable: 'Land Cover|Forest'
  technology: ['^LNDFOR$']
  fuel: ['^LND$']
  unit: million ha
  transform: abs
  osemosys_param: 'UseByTechnologyByMode'

# Mapping electricity demand for end users based on fuel usage across all time slices.
- iamc_variable: 'Final Energy|Electricity'
  osemosys_param: 'Demand'
  demand: ['^ELC002$']
  technology: ['.*']
  unit: PJ
  transform: abs
```

#### Key Components of IAMC Format
The IAMC format, developed by the Integrated Assessment Modeling Consortium, is widely used for comparing results from different models in energy, climate, land and water and sectoral studies (such as Agriculture, Land Use, Water, transport or industry).

It uses a table structure with these columns:  
`model`, `scenario`, `region`, `variable`, `unit`, and time steps.

Each project defines standardized "codelists" for consistent comparison.

A notable example using this format is the AR6 Scenario Explorer for the IPCC’s Sixth Assessment Report.

For more details, see the official IAMC documentation. 

- **Model and Scenario**: Defines the model name (e.g., `CLEWs_Ethopia`) and scenario (e.g., `NDC_Baseline`) for the IAMC output.

- **iamc_variable**: Refers to standardized variable names used in IAMC reporting. A comprehensive list of these variables can be found in the Variable list Folder and [IAMconsortium common definitions repository](https://github.com/IAMconsortium/common-definitions.git).

- **Region**: Specifies the region name (e.g., `Ethopia`) or naming convention (e.g., ISO codes or `from_csv`) for data processing.

- **Inputs**: Maps input CSV files to IAMC variables, typically for parameters like costs specifications.

- **Results**: Maps result CSV files (e.g., `NewCapacity.csv`) to IAMC variables, specifying filters (e.g., capacity, technology, fuel, emissions) and units (e.g., GW).

- **Transformations**: Optional transformations like `abs` to modify data values (e.g., taking absolute values).


## Nomenclature

CLEWs2IAMC uses following  codes for mapping, Detailed List of Nomenclature is present in .CSV file Example:

| Code    | Description                                   |
|---------|-----------------------------------------------|
| MAI     | Maize                                         |
| BEA     | Beans                                         |
| WTRPRC  | Precipitation water                           |
| WTRSUR  | Surface water                                 |
| LND     | Land                                          |
| DSL     | Diesel                                        |
| ELC001  | Electricity for transmission and distribution |
| ELC002  | Electricity for end user                      |

Every Model is Unique and address Namming Conventions As per Indivisual CLEWs Model

## Output

The converted results in IAMC format are stored in the `output_path/` directory as Excel files.

## IAM Data Validation

In Next step outputs generated from CLEWs2IAMC are introduced to The IAM Data Validation app which automates the validation of CLEWs results for Integrated Assessment Models (IAMs). It includes checks for variable and model names, a duplicates finder, and vetting routines based on IPCC AR6 vetting rules.

### Deployment
The app, built with Python and Streamlit, is part of I2AM PARIS, an open-access platform for modelling results. It is available at: [IAM Data Validation App](https://validation.i2am-paris.eu).

## License

MIT License

## Contributors

**[S Paramjeet Singh](https://github.com/Paramjeet1111/CLEWs2IAMC.git)** - Developer 

**[Francesco Gardumi](https://github.com/FraGard)** - Supervisor

**Camilla Lo Giudice** - Co-supervisor

## Acknowledgements
- [osemosys2iamc](https://github.com/OSeMOSYS/osemosys2iamc)
- [OSeMOSYS](https://www.osemosys.org/)
- [IAMconsortium](https://github.com/IAMconsortium/common-definitions.git)
- [i2amparis validation](https://github.com/i2amparis/validation.git)
- [Indicators4CLEWs](https://github.com/Camilogiu/Indicators4CLEWs/)
- MUIO OSeMOSYS User Interface
- [IAMCOMPACT](https://www.iam-compact.eu/) project has received funding from the European Union's HORIZON EUROPE Research and Innovation Programme under grant agreement No 101056306