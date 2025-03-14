# Terrain Modification Profile Generator

Author: [William (Bill) Katzenmeyer, P.E., C.F.M.](https://engineeringwithllms.info)


<p align="center">
  <img src="https://github.com/gpt-cmdr/HEC-Commander/blob/main/RAS-Commander/img/Terrain_Profiler_Logo.png" width="30%">
</p>


**[Link to Notebook](https://github.com/gpt-cmdr/HEC-Commander/blob/main/RAS-Commander/Terrain_Mod_Profiler/Terrain_Mod_Profile_Generator.ipynb)**

# Terrain Modification Profile Generator

This Python notebook provides utilities to generate detailed terrain profiles for enhancing the accuracy and stability of HEC-RAS models, particularly those utilizing LiDAR-derived channels.

## Background

LiDAR-derived channels in HEC-RAS can have noisy or flat-bottom profiles, leading to computational difficulties and longer run times. The performance and stability of the model can often be significantly improved by introducing a defined pilot channel, especially in low-flow conditions. This approach, recommended in [Making Your HEC-RAS Model Run Faster](https://www.hec.usace.army.mil/confluence/rasdocs/hgt/files/latest/91881845/105585053/2/1658159468274/Making+HEC-RASModels+Run+Faster.pdf), leverages the RASMapper Terrain Modifications layer to efficiently define these pilot channels.  This script facilitates the creation of STA-Elevation pairs to define the bottom profile of the terrain modifications at a specified sampling and grouping interval. 

## Core Functionalities

- Reads terrain modification data.
- Extracts terrain information from LiDAR-based terrain models (TIFF).
- Generates detailed terrain profiles with user-defined adjustments.
- Facilitates the creation of pilot channels, optimizing model performance.
- Exports processed profiles as CSV files for direct use in RASMapper.

## Usage Instructions

### Specify Input Files:

1. **GeoJSON for Terrain Modifications:** Provide the path to your GeoJSON file containing terrain modification polylines.
2. **LiDAR-derived Terrain TIFF:** Include the path to your terrain TIFF file.

### Set User-Defined Variables:

- **Profile_Segment_Length:** Length of each segment for defining the lowest points (in meters).
- **Profile_Vertical_Adjust:** Vertical adjustment applied to the defined lowest points.
- **Sampling_Interval:** Raster sampling interval (in meters).
- **Projection_File_Path:** Projection file for HEC-RAS RASMapper.
  
<p align="center">
  <img src="https://github.com/gpt-cmdr/HEC-Commander/blob/main/RAS-Commander/img/Terrain_Profiler_1.png" width="50%">
</p>


### Run the Notebook:

- The script will generate a CSV file containing the terrain modification profiles.
- Import the CSV into RASMapper's terrain modification editor.


## User Inputs

### User-Defined Variables

Users are required to input the following variables for the script to function correctly:

| Variable                | Description                                                  |
|-------------------------|--------------------------------------------------------------|
| Profile_Segment_Length  | Length of Segment for Lowest Point Groupings (in meters)     |
| Profile_Vertical_Adjust | Vertical Adjustment Applied to Lowest Points = -0.25         |
| Sampling_Interval       | Raster Sampling Interval (in meters)                         |
| Projection_File_Path    | HEC-RAS RASMapper Projection File                            |

### File Paths for Terrain Modifications and Terrain TIFFs

You must specify the paths to your terrain modifications and terrain TIFF files:

| Variable          | Description                                       |
|-------------------|---------------------------------------------------|
| RASTerrainMods    | GEOJSON containing terrain modification polylines |
| RASTerrainTiff1   | HEC-RAS RASMapper Terrain TIFF file               |

## Script Output

The script generates a CSV file containing a profile for each terrain modification polyline. 

<p align="center">
  <img src="https://github.com/gpt-cmdr/HEC-Commander/blob/main/RAS-Commander/img/Terrain_Profiler_2.png" width="75%">
</p>

Example of output format:

| PolylineID      | STA      | Elevation |
|-----------------|----------|-----------|
| Profile Line 1  | 0        | 43.46875  |
| Profile Line 1  | 2963.51  | 33.21875  |
| ...             | ...      | ...       |
| Profile Line 2  | 0        | 43.46875  |
| Profile Line 2  | 2963.51  | 33.21875  |
| ...             | ...      | ...       |

These profiles can be directly used in the terrain modification editor in RASMapper.

## Designing this Script with ChatGPT

I would be remiss if I didn't mention that this script was coded 100% with GPT-4 using my Water Resources Python Notebook Assistant, Markdown Text Assistant (GH Flavor), and Jupyter Notebook Portability Enhancer.

- **Water Resources Python Notebook Assistant:** [Visit here](https://chat.openai.com/g/g-WFn2bkuya-water-resources-python-notebook-assistant)
- **Markdown Text Assistant (GH Flavor):** [Visit here](https://chat.openai.com/g/g-tuwysm1j4-markdown-text-assistant-gh-flavor)
- **Jupyter Notebook Portability Enhancer:** [Visit here](https://chat.openai.com/g/g-oazhMdfSF-jupyter-notebook-portability-enhancer)

### Chat Examples

Here are some representative examples of the conversations that contributed to the development of this script:

- Initial Code Description in Plain Language >> Python Function Generation: [View conversation](https://chat.openai.com/share/b9dfe6e4-60b2-4f28-b8dd-fe4730759c19)
- Incorporating Logic for First and Last points: [View conversation](https://chat.openai.com/share/2c009eb2-b89f-4bac-84f8-e5cf34348abb)
- Automating the package installation: [View conversation](https://chat.openai.com/share/d8e06227-ceb5-4e84-8f32-6a64f7b08946)
- Writing a README: [View conversation](https://chat.openai.com/share/c3a8a68f-2453-4cd7-9eb3-8ed2c1c4c827)
