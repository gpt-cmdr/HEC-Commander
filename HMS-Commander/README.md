<p align="center">
 <img src="../misc/HMS-Commander-Logo.png" width="300">
</p>

# HMS-Commander

Author: [William (Bill) Katzenmeyer, P.E., C.F.M.](https://engineeringwithllms.info)

HMS-Commander is a python Notebooks for automating HEC-HMS Hydrologic Modeling System workflows, initially developed for LWI Region 4. The provided scripts automate calibration workflows for HEC-HMS models utilizing deficit and constant loss methods, clark unit hydrograph and recession baseflow methods. 

*[Quick Start Guide in PDF Format with screenshots:](https://github.com/gpt-cmdr/HEC-Commander/blob/main/HMS-Commander/Quick%20Start%20Guide%20for%20HMS-Commander.pdf)*

## Scripts

### HMS-Commander - Without Calibration Regions

**[HMS-Commander - Without Calibration Regions.ipynb](./HMS-Commander%20-%20Without%20Calibration%20Regions.ipynb)**

End-to-end handling of HEC-HMS automated execution for a set of calibration parameters that can be defined by the user as an input CSV file.  

Author: William Mark Katzenmeyer, P.E., C.F.M.

This script performs the following steps:
1. Read User Input CSV
2. For each user-defined run whose output file is missing, update the following:
   - Soil and Baseflow Parameters (.basin file)
   - TC and R (.basin file)
   - Output DSS file name (.run file)
   - Impervious Grids if scale >1.0 (.grid file)
3. Execute HEC-HMS using Jython
4. Restore files
5. Repeat until all user runs have been executed

### HMS-Commander - With Calibration Regions

**[HMS-Commander - With Calibration Regions.ipynb](./HMS-Commander%20-%20With%20Calibration%20Regions.ipynb)**

Same features as HMS-Commander, with the ability to create Calibration Regions.

Author: William Mark Katzenmeyer, P.E., C.F.M.

This script performs the following steps:
1. Read User Input CSV
2. Read Calibration Regions Shapefile
3. Determine calibration region for each subbasin
4. (Same as above)

### Quick Start Guide for HEC-Commander

[Quick Start Guide in PDF Format with screenshots:](https://github.com/gpt-cmdr/HEC-Commander/blob/main/Quick%20Start%20Guide%20for%20HEC-Commander.pdf)

**You must ensure that Jython is installed to the default location**: C:\jython2.7.3\

Please use a Python 3.9 environment or higher, and ensure you have the correct version of the Java SDK installed for the version of HEC-HMS you have specified in the script. The script has been tested with HEC-HMS 4.9, Jython 2.4.3 and Java SDK 20.0.1, per the Quick Guide.

## User-Defined Inputs for HMS-Commander Scripts

To successfully run the HMS-Commander scripts for automating the HEC-HMS Hydrologic Modeling System, users need to provide several key inputs. These inputs are essential for the script to function correctly and to achieve the desired outcomes from the hydrologic models.

### HMS Project Directory and Project Name

- **`hms_project_directory`**
  - **Description:** This is the directory where your HEC-HMS project is located.
  - **Example:** `hms_project_directory = r"C:\Your_HMS_Project_Directory"`

### Basin File Name

- **`hms_basin_file`**
  - **Description:** The name of your HEC-HMS basin file.
  - **Example:** `hms_basin_file = "Your_HMS_Basin.basin"`

### Calibration Runs CSV Filename

- **`user_calibration_runs_csv_filename`**
  - **Description:** The name of the CSV file that contains the calibration run parameters. This file should be located in the HMS Project Directory.
  - **Example:** `user_calibration_runs_csv_filename = "Example_Test.csv"`

### HMS Run Names

- **`hms_run_names`**
  - **Description:** A list of run names as defined in your HEC-HMS project. Each name in this list will generate a full set of user-defined runs.
  - **Example:**
    ```python
    hms_run_names = [
        "Your_Run_Name_1",
        # Add more run names as needed
    ]
    ```

### DSS Output File Suffix

- **`hms_dss_suffix`**
  - **Description:** A suffix for the DSS output file to differentiate between various run sets.
  - **Example:**
    ```python
    hms_dss_suffix = "_Batch_Name"  # define your suffix here
    print("DSS Suffix: " + hms_dss_suffix)
    ```
### Override Baseflow Setting

- **`hms_recession_baseflow`**
  - **Description:** A boolean value to determine whether to override the 'Baseflow: None' setting to 'Baseflow: Recession'. Set to True to activate this override.
  - **Example:** `hms_recession_baseflow = True`

Properly specifying these user-defined inputs is crucial for tailoring the HMS-Commander scripts to meet the specific needs of your project.

### Prepare the Run Parameters CSV

The following example input CSV has been provided:

| user_run_number_from_csv | initial_deficit_scale | maximum_deficit_scale | percolation_rate_scale | impervious_area_scale | recession_factor | initial_flow_area_ratio | threshold_flow_to_peak_ratio | time_of_concentration_scale | storage_coefficient_scale |
|--------------------------|-----------------------|-----------------------|------------------------|-----------------------|------------------|-------------------------|------------------------------|-----------------------------|---------------------------|
|                        1 |                   1.0 |                     1 |                   0.06 |                     1 |              0.1 |                       1 |                          0.1 |                           1 |                         1 |
|                        2 |                   0.9 |                     1 |                   0.06 |                     1 |              0.1 |                       1 |                          0.1 |                           1 |                         1 |

The parameters in the CSV are defined as follows:

- `initial_deficit_scale`: Scaling factor for initial deficit.
- `maximum_deficit_scale`: Scaling factor for maximum deficit.
- `percolation_rate_scale`: Scaling factor for percolation rate.
- `impervious_area_scale`: Scaling factor for impervious area.
- `recession_factor`: Recession factor parameter.
- `initial_flow_area_ratio`: Ratio for initial flow area.
- `threshold_flow_to_peak_ratio`: Ratio for threshold flow to peak.
- `time_of_concentration_scale`: Scaling factor for time of concentration.
- `storage_coefficient_scale`: Scaling factor for storage coefficient.

These correspond directly with the entries in the HMS .basin file, with the exception of TC and R scale which are applied through computation by the script. Microsoft Excel can be used to edit the CSV file.

### Baseflow Parameters Handling

If the Baseflow is set as "None" in the basin file, the script will insert recession baseflow parameters with user-defined values for the recession factor, initial flow/area ratio, and threshold flow to peak ratio.

### Impervious Scaling above 1.0 with User-Generated DSS Files

Scaling impervious layers with a scale factor above 1.0 will result in HMS errors if the resulting value is greater than 100% impervious. So, alternate DSS grids must be created where impervious values less than 100% are scaled without producing any values greater than 100%. If the user specifies impervious scale factors greater than 1.0, it is handled as follows:

- Impervious Scale Factor ≤ 1.0: Scaled directly using the impervious area scale value.
- Impervious Scale Factor > 1.0: The script looks for the following user-created files based on the impervious area scale:
  - 1.2: Impervious_1.2_SF.dss
  - 1.4: Impervious_1.4_SF.dss
  - 1.6: Impervious_1.6_SF.dss
  - 1.8: Impervious_1.8_SF.dss
  - 2.0: Impervious_2.0_SF.dss

Ensure that the corresponding .dss files are available in the project directory for the desired impervious area scales.

### File Backup, Restore and Locking

To edit the individual parameters per the CSV runfile, the HMS Basin file must be updated. Updating the TC and R values, in particular, could result in a condition where the original parameters are unknown if the script is interrupted. To avoid this, a file backup and restore scheme was adopted, with code at the beginning and end of the script to handle backups of all files potentially edited by the script, then a lock file is created. If the lock file exists at script startup, it indicates that it did not successfully complete and all files are restored from backup and backup files are deleted. This ensures that user modifications to those files are not overwritten and all files are still restored if the script fails or is halted by the user.

**Users should note that the TC and R values are the only values in the .basin file that cannot be recovered if the backup/restore/lock file logic fails. The user should periodically check their .basin file in the HMS template if the script has been restarted without completing. Automation scripts should always be run on a copy of the HMS project folder to prevent unintended data corruption**

### Run Control by Presence of Output File

To avoid complex logic to control execution of specific runs within the run file, a simple run logic was devised which looks for the output DSS files at runtime. The script will not overwrite existing DSS files, and will instead skip them. This allows the user to control the operation of the script, including updating any single run's parameters by updating the CSV, deleting the output file and re-running the script. Only the missing output file will be created.

## Program Outline using ChatGPT4 with Custom Instructions

This program outline explains the basic functionality of all code cells in natural language, created by ChatGPT-4 Agent using Custom Instructions.

## Additional Instructions for HMS-Commander with Calibration Regions

Due to the use of Geopandas, this version of the HMS-Commander script requires a Python 3.11 environment to run successfully.

## Changes to Input CSV for Calibration Zones

| user_run_number_from_csv | calregion | initial_deficit_scale | maximum_deficit_scale | percolation_rate_scale | impervious_area_scale | recession_factor | initial_flow_area_ratio | threshold_flow_to_peak_ratio | time_of_concentration_scale | storage_coefficient_scale |
|--------------------------|-----------|-----------------------|-----------------------|------------------------|-----------------------|------------------|-------------------------|------------------------------|-----------------------------|---------------------------|
| 1                        | 1         | 0.99                  | 0.91                  | 0.1                    | 0.85                  | 0.11             | 1.01                    | 0.15                         | 0.9                         | 1.1                        |
| 1                        | 2         | 0.98                  | 0.92                  | 0.05                   | 0.84                  | 0.12             | 1.02                    | 0.14                         | 0.8                         | 1.2                        |
| 1                        | 3         | 0.97                  | 0.93                  | 0.01                   | 0.83                  | 0.13             | 1.03                    | 0.13                         | 0.7                         | 1.3                        |
| 2                        | 1         | 0.96                  | 0.94                  | 0.02                   | 0.82                  | 0.14             | 1.04                    | 0.12                         | 0.6                         | 1.4                        |
| 2                        | 2         | 0.95                  | 0.95                  | 0.03                   | 0.81                  | 0.15             | 1.05                    | 0.11                         | 0.5                         | 1.5                        |

`calregion`: Define your calibration region, which corresponds with the "calregion" column in the Calibration Regions shapefile.

## Producing a Calibration Regions Shapefile

- Load the calibration shapefile.
- To create, export subbasins file from HEC-HMS, load in RASMapper, and merge subbasins.
- Then, add a "CalRegion" column and number the calibration regions (1,2,3,etc.).

## Changelog

2023-11-11: Raises an error if `hms_run_name` not present in .run file.

## Contact Information

All inquiries should be directed to [heccommander@gmail.com](mailto:heccommander@gmail.com). 
