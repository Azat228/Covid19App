# COVID-19 Data Analysis Application

A comprehensive MATLAB GUI application for visualizing and analyzing COVID-19 pandemic data across global, national, and state-level statistics.

## Overview

COVID-19 App is a standalone MATLAB application designed to track and display COVID-19 statistics including confirmed cases and death rates. The application provides an intuitive interface for exploring pandemic trends across different geographic regions, from global data down to individual states.

## Features

- **Global Statistics**: View worldwide COVID-19 case and death counts
- **Country-Level Analysis**: Analyze COVID-19 data for specific countries
- **State-Level Breakdown**: Drill down into state-level statistics where available
- **Cumulative Metrics**: Track total confirmed cases and deaths over time
- **Daily Metrics**: Monitor daily new cases and deaths to identify trends
- **Time-Series Data**: Access historical data to track disease progression
- **Interactive Visualization**: User-friendly GUI for easy navigation and data exploration

## System Requirements

### For Running the Compiled Application
- **Operating System**: Windows 7 or later
- **MATLAB Runtime (MCR)**: Version R2021a
  - Download: [MATLAB Runtime R2021a](https://www.mathworks.com/products/compiler/matlab-runtime.html)
  - The web-based installer will automatically download and install the required runtime

### For Development
- **MATLAB**: R2021a or later
- **Toolboxes**: 
  - MATLAB Coder (optional, for code generation)
  - Embedded Coder (optional, for embedded system generation)

## Installation & Usage

### Option 1: Web-Based Installer (Recommended)
1. Download `MyAppInstaller_web.exe` from the `for_redistribution` folder
2. Run the installer - it will automatically download and install MATLAB Runtime if needed
3. Follow the on-screen instructions to complete installation
4. Launch COVID-19 App from Start Menu

### Option 2: Standalone Executable
1. Extract files from `for_redistribution_files_only` folder
2. Ensure MATLAB Runtime R2021a is installed
3. Run `Covid19App.exe` directly

### Option 3: Run from MATLAB
1. Open MATLAB R2021a or later
2. Navigate to the project directory
3. Open `MyCovid19App.mlapp` with MATLAB App Designer
4. Click **Run** to launch the application

## Project Structure

```
Covid19App/
├── MyCovid19App.mlapp          # Main GUI application (built with App Designer)
├── Statistics.m                 # Base class for statistical calculations
├── CovidCountryData.m           # Country-level data management
├── CovidStateData.m             # State-level data management
├── covid_data.mat               # COVID-19 dataset
├── Covid19App.prj               # MATLAB project file
├── for_redistribution/          # Web-based installer and files
├── for_redistribution_files_only/ # Standalone executable files
├── for_testing/                 # Test build outputs
└── README.md                    # This file
```

## Architecture

### Class Hierarchy

```
Statistics (Base Class)
├── Properties
│   ├── Dates (cell array of date values)
│   ├── CumulativeCases (vector of cumulative case counts)
│   ├── DailyCases (vector of daily new cases)
│   ├── CumulativeDeaths (vector of cumulative death counts)
│   └── DailyDeaths (vector of daily new deaths)
└── Methods
    ├── Calculations for daily metrics from cumulative data
    └── Getters for all properties

CovidCountryData (Extends Statistics)
├── Properties
│   ├── Name (country name)
│   ├── IndexOfCountryIncludingGlobal
│   ├── IndexOfCountryExcludingGlobal
│   ├── CountOfCountry
│   ├── NumberOfStates
│   ├── ListOfStates (array of CovidStateData objects)
│   └── ListOfStateNames (state name references)
└── Methods
    └── Constructor: Initialize country with hierarchical state data

CovidStateData (Extends Statistics)
├── Properties
│   ├── Name (state name)
│   └── IndexOfState
└── Methods
    └── Constructor: Initialize state with statistical data
```

## Data Format

The `covid_data.mat` file contains structured COVID-19 information with the following format:
- Column 1: Geographic Region Name (Global, Country, or State)
- Column 2: Sub-region (State name for country data, empty for global)
- Columns 3+: Time-series data with [CumulativeCases, CumulativeDeaths] pairs for each date

The application automatically processes this data to calculate:
- **Daily Cases**: Daily new infections (calculated as difference from previous day)
- **Daily Deaths**: Daily new deaths (calculated as difference from previous day)
- **Cumulative Cases**: Total infections from day one
- **Cumulative Deaths**: Total deaths from day one

## Key Features of the Data Model

1. **Hierarchical Structure**: Data is organized from global → country → state level
2. **Automatic Aggregation**: Country data aggregates all state data; global data aggregates all countries
3. **Time-Series Tracking**: All metrics tracked across complete pandemic timeline
4. **Data Validation**: Daily metrics are set to 0 if negative (preventing data inconsistencies)

## Usage Guide

### Launching the Application
- Double-click `Covid19App.exe` or launch from Start Menu after installation

### Navigating the Interface
1. **Select Geographic Level**: Choose between Global, Country, or State view
2. **View Statistics**: Select which metrics to display (cases/deaths, cumulative/daily)
3. **Analyze Trends**: Explore time-series graphs to identify pandemic patterns
4. **Compare Regions**: Switch between different countries/states for comparison

## Troubleshooting

### Application Won't Start
- **Issue**: "MATLAB Runtime not found"
  - **Solution**: Install MATLAB Runtime R2021a from the web installer or download separately
- **Issue**: "Missing data file"
  - **Solution**: Ensure `covid_data.mat` is in the same directory as the executable

### No Data Displayed
- Verify the `covid_data.mat` file is properly formatted
- Check that the application has read permissions for the data file

### Runtime Error
- Ensure you're using MATLAB Runtime R2021a (version 9.10) or MATLAB R2021a
- Try reinstalling the application using the web-based installer

## Development & Modification

### Building the Application in MATLAB
1. Open `Covid19App.prj` in MATLAB
2. Navigate to **App Designer** and edit `MyCovid19App.mlapp`
3. Modify the Statistics or Country/State Data classes as needed
4. Click **Package** to rebuild the standalone application

### Modifying the Data
1. Edit the data structure in `covid_data.mat` using MATLAB
2. Ensure the format matches the expected structure
3. Rebuild and repackage the application

### Adding New Features
- Extend the `Statistics` class for new calculations
- Add visualization features in the MATLAB App Designer GUI
- Implement additional geographic levels by extending `CovidCountryData`

## Application Metadata

- **Application Name**: Covid19App
- **Version**: 1.0
- **Build Environment**: MATLAB R2021a (Compiler v8.2)
- **Target Platform**: Windows (7 and later)
- **Application Type**: Standalone GUI Application
- **License**: [Add your license information here]

## Data Source

[Add information about the COVID-19 data source and last update date]

## Support & Contact

For issues, questions, or suggestions, please contact the development team.

## Disclaimer

This application is provided for educational and analytical purposes. The COVID-19 data is historical and should be cross-referenced with official health organization sources for current information.

---

**Last Updated**: July 2024  
**Version**: 1.0
