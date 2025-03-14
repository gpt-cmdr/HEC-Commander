<p align="center">
 <img src="../misc/DSS-Commander.png" width="300">
</p>

Author: [William (Bill) Katzenmeyer, P.E., C.F.M.](https://engineeringwithllms.info)

# DSS-Commander

DSS-Commander is a Python script for plotting HEC-RAS 1D results from DSS files against gauge data, creating interactive HTML plots using Bokeh. It also calculates calibration statistics (RMSE, r, PBIAS, NSE) for each plotted location to assess model performance.

This script is built on the functionality of [pydsstools by gyanz](https://github.com/gyanz/pydsstools).

## Features

- Plots HEC-RAS 1D results from DSS files against gauge data
- Generates interactive HTML plots using Bokeh for easy data exploration
- Calculates calibration statistics (RMSE, r, PBIAS, NSE) for each plotted location
- Supports both STAGE and FLOW time series
- Customizable plot dimensions and appearance
- Filters DSS pathnames based on user-defined criteria to create grouped plots

## Calibration Statistics

DSS-Commander calculates the following calibration statistics for each plotted location:

- **RMSE (Root Mean Square Error)**: Measure of the average magnitude of the errors between modeled and observed values.
  - For STAGE time series, RMSE is calculated using the mean depth of all gauged values.
  - For FLOW time series, RMSE is calculated using the peak flow of all gauged values.

- **r (Pearson Correlation Coefficient)**: Measure of the linear correlation between modeled and observed values, ranging from -1 to 1.

- **PBIAS (Percent Bias)**: Measure of the average tendency of the modeled values to be larger or smaller than their observed counterparts, expressed as a percentage.

- **NSE (Nash-Sutcliffe Efficiency)**: Measure of how well the model predicts observed values relative to simply using the mean of observed values, ranging from -∞ to 1.

These statistics provide a quantitative assessment of model performance and can help guide calibration efforts.

## User Inputs

DSS-Commander requires the following user inputs:

- `DSS_Source_Path`: The path to the directory containing the DSS files to plot.

- `gauge_csv_file_name`: The name of the CSV file containing gauge data. This file must be located in the `DSS_Source_Path` directory.

- `river_stations`: A list of river station IDs to plot. These should match the station IDs used in the DSS pathnames.

- `search_word`: A word to filter the DSS pathnames. Only pathnames containing this word will be included in the plots.

- `plot_window_start`, `plot_window_end`: The start and end timestamps for the plot window, in the format "DDMMMYYYY HH:MM:SS".

- `base_condition_dss`: A search phrase to identify the base condition DSS time series. Time series matching this phrase will be plotted in blue.

- `search_parameter1`, `search_parameter2`: The time series types to plot, typically "STAGE" and "FLOW".

- `bokeh_plot_width`, `bokeh_plot_height`: The width and height of the Bokeh plots, in pixels.

- `bokeh_table_width`, `bokeh_table_height`: The width and height of the Bokeh tables displaying calibration statistics, in pixels.

- `output_html_file_name`: The name of the output HTML file containing the plots.

- `bokeh_plot_title`: The title for the Bokeh plots.

- `chan_bottom_elevation_dict`: A dictionary mapping river station IDs to their corresponding channel bottom elevations. This is used to calculate depth for stage time series.

For best results, ensure that the gauge data and DSS files fully cover the specified plot window.

## Gauge Data CSV Format

DSS-Commander requires a gauge data CSV file with the same timestamps and interval as the DSS files. The CSV file must have the following format:
```
River Station,89804,89804,117188,110449,110449
STAGE or FLOW,STAGE,FLOW,STAGE,STAGE,FLOW
Date,USGS_STA_NUM1,USGS_STA_NUM1,USGS_STA_NUM2,USGS_STA_NUM3,USGS_STA_NUM3
3/28/2018 0:00,116.8,60.7,95.195,50.146,371
3/28/2018 1:00,116.8,60.7,95.195,50.126,368
3/28/2018 2:00,116.79,60.1,95.195,50.136,369
```
The first row should contain the river station IDs, the second row should indicate whether each column contains STAGE or FLOW data, and the third row should provide the gauge station numbers or names. The remaining rows should contain the timestamp and corresponding gauge values.

## Installation and Setup

1. Install Python using Anaconda Navigator (download via https://www.anaconda.com/).

2. Create a Python 3.11 environment in Anaconda Navigator:
   - Open Anaconda Navigator
   - Go to Environments > Create
   - Create a Python 3.11 environment
   - Open a terminal in the new environment

3. Install the required dependencies by running the following command in the terminal:
   
   pip install pydsstools bokeh pandas numpy sklearn openpyxl 

4. Install Visual Studio Code (download via https://code.visualstudio.com/Download).

5. Install the following Visual Studio Code extensions:
   - Jupyter
   - Python
   - Python Environment Manager
  
 6. Install C++ Build Tools for Visual Studio 2019 (for DSS-Commander)**
[https://aka.ms/vs/17/release/vs_BuildTools.exe](https://aka.ms/vs/17/release/vs_BuildTools.exe) 
When installing, select the "C++ Build Tools for Visual Studio 2019" option

7. Open the DSS-Commander script in Visual Studio Code and update the user inputs section according to your project's requirements.  If the required prerequisites are present, the script will handle installation of gdal, pydss and other python libraries necessary for the script operation.  

8. Run the script to generate the HTML plots and calibration statistics.

The generated HTML plots will be saved in the `DSS_Source_Path` directory, along with Excel files containing the plotted data and calibration statistics.

## License

DSS-Commander is released under the MIT License. See `LICENSE` for more information.

## Acknowledgements

DSS-Commander is built on the functionality of [pydsstools by gyanz](https://github.com/gyanz/pydsstools).

## Contact

For questions, suggestions, or issues, please contact the author or open an issue on the GitHub repository.
