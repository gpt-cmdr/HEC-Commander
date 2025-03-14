# Atlas 14 Spatial Variance Analysis Tools

This repository contains a series of Python notebooks for analyzing spatial variance in NOAA Atlas 14 precipitation data across watersheds. The tools automate the download, processing, and analysis of Atlas 14 data to support hydrologic and hydraulic modeling efforts.

## Purpose

Accurate representation of precipitation inputs is crucial for effective hydrologic and hydraulic modeling, especially for large watersheds spanning multiple states. This toolset addresses the challenge of applying NOAA Atlas 14 precipitation frequency estimates to large-scale watershed models where a mix of HMS and RAS 2D models are used (which both have differing capabilities and available toolsets for discretizing Atlas 14 values within model boundaries).  Balancing spatial detail with computational efficiency and software limitations requires data analysis to inform users as to whether such discretization is significant over the chosen model domain.
These  tools provide a comprehensive approach to analyzing and discretizing Atlas 14 data for use in both HEC-HMS and HEC-RAS models. They bridge the gap between fully distributed precipitation inputs and practical constraints of current modeling software.

## Notebooks

1. [Atlas14_1_Download_NOAA_ASC_Grids.ipynb](./Atlas14_1_Download_NOAA_ASC_Grids.ipynb): Downloads Atlas 14 ASC grid files from NOAA.
2. [Atlas14_2_Post-Process_Statistics_by_Polygon.ipynb](Atlas14_2_Post-Process_Statistics_by_Polygon.ipynb): Processes downloaded grids and calculates statistics for defined watershed polygons.
3. [Atlas14_3_Variance_and_Data_Analysis.ipynb](Atlas14_3_Variance_and_Data_Analysis.ipynb): Performs further analysis and visualization of the processed data.

## Limitation

The scripts only work with multi-state datasets.  This was due to the fact that this tool was originally designed for Region 4 of the Louisiana Watershed Initiative, which spans multiple states.  In fact, all but 2 of the LWI Regions have inflows from out of state.  However, for study areas that are only contained within one state, the script can still be utilized as long as an adjacent state is specified.  The additional data will simply be ignored as it is not within the study area.  Alternately, manually editing of the notebooks can be performed skip the steps to combine the ASC grids and redirect data analysis to use the correct state grids.

Additionally, the script does not analyze the upper and lower bound datasets available from NOAA.  Only the recommended mean values are analyzed. 

## Setup and Usage

### 1. Atlas14_1_Download_NOAA_ASC_Grids_robust.ipynb

This notebook downloads Atlas 14 ASC grid files from the NOAA website.

User input block:
```python
#1 User Input: Base URL, State Datasets, and Output Directory
HDSC_DATA_URL = "https://hdsc.nws.noaa.gov/pub/hdsc/data/"
STATE_DIR_1 = "hdsc_tx_data"
STATE_DIR_2 = "hdsc_se_data"
# Open the base url in your browser to choose directory names

# User-defined number of concurrent HTTP requests
num_concurrent_requests = 4

# Define destination directory for unzipped files
dest_dir = "LWI_Region4"
```

Explanation:
- `HDSC_DATA_URL`: Base URL for NOAA's Hydrometeorological Design Studies Center data.
- `STATE_DIR_1` and `STATE_DIR_2`: Directories for specific state datasets (e.g., Texas and Southeast).
- `num_concurrent_requests`: Number of simultaneous download requests to make.
- `dest_dir`: Local directory where downloaded and unzipped files will be stored.

### 2. Atlas14_2_Post-Process_Statistics_by_Polygon_robust.ipynb

This notebook processes the downloaded grids and calculates statistics for defined watershed polygons.

User input block:
```python
#1 Define file paths to watershed polygon, state polygon, and example asc files to be used as general figures
watershed_boundary_file = r'Region4_HUC_Boundaries.geojson'
state_boundary_file = r'State_Boundary.geojson'
asc_file_name_1 = r'LWI_Region4/se50yr06ha/se50yr06ha.asc'
asc_file_name_2 = r'LWI_Region4/tx50yr06ha/tx50yr06ha.asc'

# Default CRS assumption for asc files 
asc_file_default_EPSG = "4269"

# Target CRS for all script operations and outputs
reproject_to_epsg = "4269"

# Input Directory with combined ASC File Datasets (this should come from a previous step on revision)
input_directory = r'LWI_Region4'

# Set the base folder path
base_folder = r'LWI_Region4'

# Output Directory for PNG and CSV Outputs
import os
output_directory = os.path.join(input_directory, 'Watershed_Statistical_Analysis')
```

Explanation:
- `watershed_boundary_file` and `state_boundary_file`: GeoJSON files defining watershed and state boundaries.
- `asc_file_name_1` and `asc_file_name_2`: Example ASC files from different states to be combined.
- `asc_file_default_EPSG` and `reproject_to_epsg`: Coordinate reference system information.
- `input_directory` and `base_folder`: Directories containing the ASC files.
- `output_directory`: Where the analysis results will be saved.

### 3. Atlas14_3_Variance_and_Data_Analysis_robust.ipynb

This notebook performs further analysis and visualization of the processed data.

User input block:
```python
# Provide path to a CSV file from previous script so we can continue data analysis

# Load the data from the CSV file (use an example file for the example plot)
file_path = r'output_csv_by_polygon\Lower_Calcasieu.csv'
csv_data = pd.read_csv(file_path)

# Display the first few rows of the dataframe to understand its structure
display(csv_data)
```

Explanation:
- `file_path`: Path to a CSV file generated by the previous notebook, containing processed data for a specific polygon (e.g., Lower Calcasieu watershed).

## Requirements

- GeoJSON with watershed boundaries for analysis
    - GeoJSON should have a "name" attribute column containing your watershed name (if report figures are desired)
    - Polygons should be single part, not multipart polygons
    - NOAA ASC grids are in EPSG 6479, convert all input GeoJSONS to this projection before processing with script
- Tested with Python 3.11 using Anaconda and VS Code
- Auto Installed Libraries: pandas, numpy, matplotlib, geopandas, rasterio, requests, beautifulsoup4, tqdm, IPython

## Usage Notes

1. Run the notebooks in order (1, 2, 3) to ensure all necessary data is downloaded and processed before analysis.
2. Adjust input parameters as needed for your specific watershed and data requirements.
3. Ensure you have necessary permissions and disk space for downloading and processing large datasets.

## Authors

William (Bill) Katzenmeyer, P.E., C.F.M. 


## Example Outputs

Below are example outputs from Region 4 and the West Fork 2D watershed area:

### Plots and Charts

<p align="center">
  <img src="img/sample_regional_plot.png" width=60%>
</p>


<p align="center">
  <img src="img/sample_watershed_pixel_plot.png" width=60%>
</p>


<p align="center">
  <img src="img/sample_watershed_duration_chart.png" width=60%>
</p>


### Tabular CSV Output

| File Name            | Max (inches) | Min (inches) | Mean (inches) | Range (%)         | polygon_name | Results_name            | Return Interval | Duration | Duration Units | Duration Hours |
|----------------------|--------------|--------------|---------------|-------------------|--------------|-------------------------|-----------------|----------|----------------|----------------|
| cb100yr06ha.asc      | 10.119       | 9.414        | 9.776802063   | 6.967099981047149 | West Fork    | West Fork cb100yr06ha.asc | 100             | 6        | ha             | 360            |
| cb100yr12ha.asc      | 12.846       | 11.511       | 12.0398511887 | 10.39234055334938 | West Fork    | West Fork cb100yr12ha.asc | 100             | 12       | ha             | 720            |
| cb100yr24ha.asc      | 15.293       | 13.374       | 14.1577539444 | 12.548228587243116| West Fork    | West Fork cb100yr24ha.asc | 100             | 24       | ha             | 1440           |
| cb100yr48ha.asc      | 17.159       | 15.007       | 16.0515098572 | 12.541525598754506| West Fork    | West Fork cb100yr48ha.asc | 100             | 48       | ha             | 2880           |






