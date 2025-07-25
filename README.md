# CLEWs2IAMC

CLEWs2IAMC is a Python toolkit that automates the conversion of (Climate, Land, Energy and Water ) CLEWs model inputs and results into IAMC-compliant Excel files  by Using YAML configuration files, it flexibly maps various result types (e.g., investment, emissions, demand, capacity, technology use) from CSVs to the IAMC format. The tool supports both Jupyter notebook and command-line workflows, and relies on osemosys2iamc for processing and configuration.

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

1. Clone this repository
2. Install required packages:
```bash
pip install osemosys2iamc pandas pyyaml
```

## Usage

1. Place your OSeMOSYS model results in the `MAIN/` directory
2. Configure the appropriate YAML files for the type of results you want to convert
3. Run the conversion using either:
   - The Jupyter notebook `Ethiopia.ipynb`
   - Command line interface:
     ```bash
     osemosys2iamc <input_path> <results_path> <config_file> <output_file>
     ```

## Configuration Files

The project includes several configuration files for different types of results (located in the `Config/` directory):

### Overview

This tool, implemented in `resultify.py`, converts CLEWs model results and inputs into the IAMC (Integrated Assessment Modeling Consortium) format. It processes input and result CSV files based on a configuration file (`config.yaml`) and outputs the results as an Excel file in IAMC format.

### Configuration File (`config.yaml`)

The `config.yaml` file defines how CLEWs input and result data are mapped to IAMC variables. It specifies the model, scenario, region, and data processing rules for inputs and results, including filtering by technologies, fuels, or emissions, and applying transformations.

#### Key Components

- **Model and Scenario**: Defines the model name (e.g., `CLEWs_Ethopia`) and scenario (e.g., `NDC_Baseline`) for the IAMC output.

- **Region**: Specifies the region name (e.g., `Ethopia`) or naming convention (e.g., ISO codes or `from_csv`) for data processing.

- **Inputs**: Maps input CSV files to IAMC variables, typically for parameters like costs specifications.

- **Results**: Maps result CSV files (e.g., `NewCapacity.csv`) to IAMC variables, specifying filters (e.g., capacity, technology, fuel, emissions) and units (e.g., GW).

- **Transformations**: Optional transformations like `abs` to modify data values (e.g., taking absolute values).

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