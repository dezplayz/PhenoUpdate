# PhenoModel Docker Repair

## Overview

This repository provides a containerized setup for running phenological modeling using the Springtime library. It adresses compatibility issues on Windows by using Docker. This functions as a repair to the original replication project [title](https://www.example.com) with the goal of enhancing reproducibility through Docker.

## Objective

Creating a robust and platform independant replication of using phenological model through Springtime library by using Docker

## Docker setup

### Requirements

- Windows 10/11 with WSL installed
- Docker Desktop, installed and logged in
- Docker set to use WSL2 backend

### 1. Pull Springtime Docker Image

`docker pull ghcr.io/phenology/springtime:latest`

### 2. Run Container and Expose Port 8888

`docker run -p 8888:8888 -it ghcr.io/phenology/springtime:latest`

### 3. Launch Jupyter Notebook

Inside container:
`jupyter notebook --ip=0.0.0.0 --port=8888 --allow-root`

Then, open http://localhost:8888 in your browser.

### 4. Install rpy2 inside the Container

`%pip install rpy2`

**Unlike on native Windows, this works flawlessly in Docker**

## Data Sources

The two main data sources are both accessed via Springtime library

- USA National Phenology Network (USA-NPN): Provides phenological observation data (e.g., leaf emergence).

- Daymet: Provides daily gridded weather data, including Tmax, Tmin, solar radiation, and precipitation.

The datasets are accessed through Springtime modules:
- `springtime.datasets.rnpn.get_data()` for the phenological data, in this case Acer Rubrum, 2011-2021.
- `springtime.datasets.daymet.get_data()` for climate data filtered to NY, IL, and MN.

The two datasets are merged using a temporal join through pandas, based on their shared location and date values. 
A sample of the merged dataset (OutputFile.csv) is included in the repository as reference to the expected output structure and was used from the original PhenoModel repository [title](https://www.example.com).

## Structure of the Repository
README.md 
