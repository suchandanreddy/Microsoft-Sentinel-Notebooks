# Microsoft Sentinel Data Lake Notebooks

A collection of Jupyter notebooks for analyzing security data from Microsoft Sentinel Data Lake using PySpark.

## Overview

This repository contains analytical notebooks designed to run in the **Microsoft Sentinel notebook runtime** environment. These notebooks leverage the Sentinel Data Lake and PySpark to perform advanced security analytics and data summarization.

## Notebooks

### CommonSecurity_ID_Summary.ipynb

**Purpose:** Summarizes CommonSecurity_ID logs with identity-centric daily security metrics.

**What it does:**
- Reads `CommonSecurity_ID_KQL_CL` events from the Sentinel Data Lake
- Filters data based on a configurable lookback period (default: 30 days)
- Creates an identity-centric daily summary by aggregating events by:
  - Day
  - User
  - Source IP
  - Device
- Calculates security metrics:
  - Event count per identity/device combination
  - Distinct users per day
  - Distinct source IPs per day
  - Distinct devices per day
- Writes summarized results to a new Data Lake table (`CommonSecurity_ID_SPRK`)
- Validates the output by reading back and displaying the results

**Output:** Daily security summary table with aggregated counts and distinct entity metrics

## Prerequisites

- **Microsoft Sentinel workspace** with access to Data Lake
- **[Microsoft Sentinel VS Code Extension](https://marketplace.visualstudio.com/items?itemName=ms-security.ms-sentinel)** 

## Configuration

Before running the notebook, update the following parameters in the first code cell:

```python
workspace_name = "NinjaSOC"              # Your Sentinel workspace name
source_table = "CommonSecurity_ID_KQL_CL"  # Source table to read from
output_table = "CommonSecurity_ID_SPRK"    # Output table name (must have _SPRK suffix)
lookback_days = 30                       # Number of days to look back
```

## How to Use

1. **Open the notebook** in your Microsoft Sentinel notebook environment
2. **Configure parameters** in the first code cell to match your workspace and table names
3. **Run the notebook** sequentially (all cells in order)
4. **Review output** in the final validation cell showing the summarized data

## Notes

- Output table names with the `_SPRK` suffix are recommended for easy identification
- Adjust `lookback_days` parameter based on your analysis needs (higher values = more data, longer runtime)
- The notebook includes validation to confirm successful data write
