# 🎶 Analyzing Trends in Spotify's Top Songs of 2023 using Exploratory Data Analysis

> This project explores Spotify's top songs of 2023 by performing an exploratory data analysis (EDA). With the help of Python, it examines trends, correlations, and key factors such as the number of streams, release dates, and musical attributes. Findings from this analysis aim to offer valuable insights into the elements that drive a track’s success on streaming platforms.

---

## Prerequisites
* Physical server or virtual machine.
* CPU: 2 x 64-bit, 2.8 GHz, 8.00 GT/s CPUs or better.
* Memory: minimum RAM size of 32 GB, or 16 GB RAM with 1600 MHz DDR3 installed, for a typical installation with 50 regular users.
* Client environment may be Windows, macOS or Linux.

## Getting Started

You must first install Anaconda Navigator from https://www.anaconda.com/download to install Jupyter Notebook. 

### OS Versions
<details>
  <summary> 📘 Click Here for Mac Installation Steps </summary>

  <br>
  
  1. Visit the site for Anaconda Navigator.
  2. Press Download and select your Mac Architecture.
     * Intel Processor (This is for devices that have an Intel Processor).
     * Apple ARM M1 or M2 (This is for devices that have Apple Silicon specifically for M1 or later).
  3. Execute the file and it will ask for you if you trust it and press 'Allow'.
  4. Agree to the Terms and Conditions and press Install.
  5. Click continue and you can now delete the installer.
  6. Open Anaconda Navigator and Launch the Jupyter Notebook.
</details>

<br>

<details>
  <summary> 📘 Click Here for ⊞Windows Installation Steps </summary>

  <br>
  
  1. Visit the site for Anaconda Navigator.
  2. Press Download and select Windows.
  3. Save the exe file and run the installer.
  4. Press the next button until you see the Install button and press Install.
  5. Once you’ve installed Anaconda Navigator, open it and launch the Jupyter Notebook.

</details>

<br>

<details>
  <summary> 📘 Click Here for 🐧Linux Installation Steps </summary>

  <br>

  1. Visit the site for Anaconda Navigator.
  2. Select Linux
  3. Copy the bash (.sh file) installer link.
  4. Use wget to download the bash installer.
  5. Run the bash script to install Anaconda3.
  6. source the .bash-rc file to add Anaconda to your PATH.
  7. Start the Python REPL.

</details>

## 📑 Table of Contents
- [Overview of Dataset](#Overview-of-Dataset)
- [Basic Descriptive Statistics](#Basic-Descriptive-Statistics)
- [Top Performers](#Top-Performers)
- [Temporal Trends](#Temporal-Trends)
- [Genre and Music Characteristics](#Genre-and-Music-Characteristics)
- [Platform Popularity](#Platform-Popularity)
- [Advanced Analysis](#Advanced-Analysis)
- [Conclusion](#Conclusion)
- [Version History](#Version-History)

---

Before we begin the Data Analysis, we must first import the required libraries, download the csv file [View CSV Data](https://github.com/joparayno/spotify-insights-2023/blob/main/Most%20Streamed%20Spotify%202023.csv), and use the pd.read_csv() function to load the csv into a Pandas DataFrame.

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("Most Streamed Spotify 2023.csv", encoding='latin-1')
df
```

## Overview of Dataset
- How many rows and columns does the dataset contain?
  ```python
  rows, columns = df.shape
  print("The dataset contains", rows, "rows and", columns, "columns.")
  ```
  **Output**:
  ```
  The dataset contains 953 rows and 24 columns.
  ```
   
- What are the data types of each column? Are there any missing values?
  ```python
  print("Data types of each column:")
  print(df.dtypes)

  missing_values = df.isnull().sum()
  print("\nMissing values in each column:")
  print(missing_values)
  ```
  **Output**:
  ```
  OUTPUT
  ```

## Basic Descriptive Statistics
- What are the mean, median, and standard deviation of the streams column?
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
  
- What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
  
## Top Performers
- Which track has the highest number of streams? Display the top 5 most streamed tracks.
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
   
- Who are the top 5 most frequent artists based on the number of tracks in the dataset?
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
  
## Temporal Trends
- Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
    
- Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
    
## Genre and Music Characteristics
- Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
    
- Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
  
## Platform Popularity
- How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
  
## Advanced Analysis
- Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
  
- Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.
  ```python
  
  ```
  **Output**:
  ```
  OUTPUT
  ```
  
---

## Conclusion

---

## Version History
| Version | Description                        | Date       |
| ------- | ---------------------------------- | ---------- |
| 1.0.0   | Initial commit                     | 10-20-2024 |
| 1.1.0   | Updated README.md                  | 10-29-2024 |
| 1.2.0   | Updated README.md                  | 11-02-2024 |
| 1.3.0   | Updated README.md                  | 11-03-2024 |

