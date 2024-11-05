# 🎶 Analyzing Trends in Spotify's Top Songs of 2023 using Exploratory Data Analysis

> This project explores Spotify's top songs of 2023 by performing an exploratory data analysis (EDA). With the help of Python, we'll be able to examine the trends, correlations, and key factors such as the number of streams, release dates, and musical attributes. Findings from this analysis aim to offer valuable insights into the elements that drive a track’s success on streaming platforms.

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
  rows, columns = df.shape # Provide the number of rows and columns of the DataFrame
  print("The dataset contains", rows, "rows and", columns, "columns.")
  ```
  **Output**:
  ```
  The dataset contains 953 rows and 24 columns.
  ```
  > Dataset consists of 953 rows and 24 columns.
 
- What are the data types of each column? Are there any missing values?
  ```python
  print("Data types of each column:")
  print(df.dtypes) # Describe each column’s data type.

  missing_values = df.isnull().sum() # Count the number of missing values on the dataset.
  print("\nMissing values in each column:")
  print(missing_values)
  ```
  **Output**:
  ```
  Data types of each column:
  track_name              object
  artist(s)_name          object
  artist_count             int64
  released_year            int64
  released_month           int64
  released_day             int64
  in_spotify_playlists     int64
  in_spotify_charts        int64
  streams                 object
  in_apple_playlists       int64
  in_apple_charts          int64
  in_deezer_playlists     object
  in_deezer_charts         int64
  in_shazam_charts        object
  bpm                      int64
  key                     object
  mode                    object
  danceability_%           int64
  valence_%                int64
  energy_%                 int64
  acousticness_%           int64
  instrumentalness_%       int64
  liveness_%               int64
  speechiness_%            int64
  dtype: object

  Missing values in each column:
  track_name               0
  artist(s)_name           0
  artist_count             0
  released_year            0
  released_month           0
  released_day             0
  in_spotify_playlists     0
  in_spotify_charts        0
  streams                  0
  in_apple_playlists       0
  in_apple_charts          0
  in_deezer_playlists      0
  in_deezer_charts         0
  in_shazam_charts        50
  bpm                      0
  key                     95
  mode                     0
  danceability_%           0
  valence_%                0
  energy_%                 0
  acousticness_%           0
  instrumentalness_%       0
  liveness_%               0
  speechiness_%            0
  dtype: int64
  ```
  > We can observe that certain columns display their data type as “int64” and “object.” Now, for the “in_shazam_charts” column, there’s a missing value of 50, while the “key” column has a missing value of 95.

## Basic Descriptive Statistics
- What are the mean, median, and standard deviation of the streams column?
  ```python
  # Convert the 'streams' column to numeric values, coercing any errors to NaN
  df['streams'] = pd.to_numeric(df['streams'], errors='coerce')
  df = df.dropna(subset=['streams'])

  # Show the summary statistics for each column
  df.describe()
  statsum = df['streams'].describe() # Shows the statistics of the 'streams' column
  print("Summary of Streams: ")
  print(statsum)
  ```
  **Output**:
  ```
  Summary of Streams: 
  count    9.520000e+02
  mean     5.141374e+08
  std      5.668569e+08
  min      2.762000e+03
  25%      1.416362e+08
  50%      2.905309e+08
  75%      6.738690e+08
  max      3.703895e+09
  Name: streams, dtype: float64
  ```
  > With the provided output, we can get the mean value as 5.141374e+08, the median (50%) as 2.905309e+08, and the standard deviation as 5.668569e+08.
  
- What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?
  ```python
  fig, axes = plt.subplots(2, 2, figsize=(14, 10))

  # Histogram for 'released_year'
  sns.histplot(df['released_year'], bins=20, stat='count', ax=axes[0, 0], color='skyblue')
  axes[0, 0].set_title('Released Year')
  axes[0, 0].set_xlabel('Released Year')

  # Box plot for 'released_year'
  sns.boxplot(x=df['released_year'], ax=axes[1, 0], color='lightblue', width=0.6)
  axes[1, 0].set_title('Released Year - Outliers')

  # Histogram for 'artist_count'
  sns.histplot(df['artist_count'], bins=15, stat='count', ax=axes[0, 1], color='salmon')
  axes[0, 1].set_title('Artist Count')
  axes[0, 1].set_xlabel('Artist Count')

  # Box plot for 'artist_count'
  sns.boxplot(x=df['artist_count'], ax=axes[1, 1], color='lightcoral', width=0.6)
  axes[1, 1].set_title('Artist Count - Outliers')

  plt.tight_layout()
  plt.show()
  ```
  **Output**:

  ![Screenshot 2024-11-05 at 1 03 36 PM](https://github.com/user-attachments/assets/417beab2-9802-457e-90e8-5743f7ad1290)

  > With the gathered information for the Top Hits, most songs are concentrated towards recent years, especially from the 2000s onward. This suggests that the most popular streamed songs in the dataset are recent. Outliers exist in earlier years, going back to the 1940s, which could represent older classic songs that have remained popular or experienced a resurgence in streaming popularity. Clustering for recent years indicates that more recent releases are more commonly represented among popular streams. Most songs have an artist count between 1 and 3, with a strong concentration around single-artist songs. Outliers with higher artist counts, up to 8, likely indicate collaborations or songs with multiple featured artists, which may be less common. The high concentration of single-artist entries aligns with the music industry trend of individual artist dominance, but the presence of outliers suggests the popularity of collaborative tracks in recent years.
 
## Top Performers
- Which track has the highest number of streams? Display the top 5 most streamed tracks.
  ```python
  df.sort_values(by=["streams"],ascending=False).head() # Sorts by 'streams' in descending order and display the top 5 rows.
  ```
  **Output**:
  
  | track_name       | artist(s)_name             | artist_count | released_year | released_month | released_day | in_spotify_playlists | in_spotify_charts | streams     | in_apple_playlists | bpm | key | mode | danceability_% | valence_% | energy_% | acousticness_% | instrumentalness_% | liveness_% | speechiness_% |
  |------------------|----------------------------|--------------|---------------|----------------|--------------|----------------------|-------------------|-------------|--------------------|-----|-----|------|----------------|-----------|----------|----------------|--------------------|------------|---------------|
  | Blinding Lights | The Weeknd                 | 1            | 2019          | 11             | 29           | 43899               | 69                | 3.7039e+09  | 672 | 171 | C#  | Major | 50             | 38        | 80       | 0              | 0                  | 9          | 7             |
  | Shape of You    | Ed Sheeran                 | 1            | 2017          | 1              | 6            | 32181               | 10                | 3.5625e+09  | 33 |96  | C#  | Minor | 83             | 93        | 65       | 58             | 0                  | 9          | 8             |
  | Someone You Loved | Lewis Capaldi            | 1            | 2018          | 11             | 8            | 17836               | 53                | 2.8872e+09  | 440 |110 | C#  | Major | 50             | 45        | 41       | 75             | 0                  | 11         | 3             |
  | Dance Monkey    | Tones and I                | 1            | 2019          | 5              | 10           | 24529               | 0                 | 2.8648e+09  | 533 |98  | F#  | Minor | 82             | 54        | 59       | 69             | 0                  | 18         | 10            |
  | Sunflower - Spider-Man: Into the Spider-Verse | Post Malone, Swae Lee | 2 | 2018 | 10 | 9 | 24094 | 78 | 2.8081e+09 | 372 | 90 | D | Major | 76 | 91 | 50 | 54 | 0 | 7 | 5 |

  > The most popular tracks are:
  > 1. Blinding Lights by The Weeknd with the streams of 3.7039e+09.
  > 2. Shape of You by Ed Sheeran with the streams of 3.5625e+09.
  > 3. Someone You Loved by Lewis Capaldi with the streams of 2.887242e+09.	
  > 4. Dance Monkey by Tones and I with the streams of 2.864792e+09.
  > 5. Sunflower - Spider-Man: Into the Spider-Verse by Post Malone, Swae Lee with the streams of 2.808097e+09.

- Who are the top 5 most frequent artists based on the number of tracks in the dataset?
  ```python
  artists = df['artist(s)_name']
  artist = []

  # Separate multiple artists by commas, stripping extra spaces.
  for i in artists:
    for ix in i.split(','):
        artist.append(ix.strip()) 

  # Determines the top 5 frequent artists.
  freq_art = pd.DataFrame(artist, columns=['Artists']).value_counts().reset_index(name='Number of Songs').iloc[:5]

  sns.barplot(x='Artists', y='Number of Songs', data=freq_art)
  plt.show()
  ```
  **Output**:
  
  ![Screenshot 2024-11-04 at 10 17 36 PM](https://github.com/user-attachments/assets/02ad062c-3c1f-48aa-9b65-aa613fae7540)

  > By combining all the artists in the dataset and sorting it in descending order, we can determine the top 5 most frequent artists based on the number of tracks they have.
  > 1. Bad Bunny
  > 2. Taylor Swift
  > 3. The Weeknd
  > 4. Kendrick Lamar
  > 5. SZA

## Temporal Trends
- Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.
  ```python
  spotify_yr = df.groupby('released_year').size() # Count the songs per release year.

  plt.plot(spotify_yr) # Plot the number of songs released each year as a line plot.
  ```
  **Output**:
  
  ![Screenshot 2024-11-03 at 2 12 15 PM](https://github.com/user-attachments/assets/fc78cf7b-108a-4d24-a99e-79090499bc82)

  > We can observe a significant increase in the number of tracks released in the year 2020. This surge might be attributed to the data collected and the specific year of release.
  
- Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?
  ```python
  month_pattern = df.groupby('released_month').size() # Group the data by 'released_month' column and count the number of occurences for each month.
  
  plt.plot(month_pattern) # Plot the pattern of the data.
  ```
  **Output**:
  
  ![Screenshot 2024-11-03 at 10 48 23 PM](https://github.com/user-attachments/assets/9bc033ed-eaa1-4d56-b90b-09b3c6ec4131)

  > It appears that January and May are the best months for releasing new songs, as they have the highest number of releases compared to August, which has the lowest.
 
## Genre and Music Characteristics
- Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?
  ```python
  features = ['bpm', 'danceability_%', 'energy_%', 'valence_%', 'acousticness_%', 'instrumentalness_%', 'liveness_%', 'speechiness_%']

  fig, axes = plt.subplots(4, 2, figsize=(20, 14)) # Create subplots for each feature
  axes = axes.flatten()

  for i, feature in enumerate(features): # Plot streams for each feature
    df.groupby(feature)['streams'].sum().sort_index().plot(ax=axes[i], label=feature)
    axes[i].legend()

  plt.tight_layout()
  plt.show()
  ```
  **Output**:

  ![Screenshot 2024-11-05 at 12 17 24 AM](https://github.com/user-attachments/assets/40c99974-c7e3-4890-bc45-d6c6ec254e65)

  > The plots demonstrate the correlation between streams and various musical attributes. For instance, the beats per minute (BPM) reached a peak of 120. The danceability percentage peaked at 60% and 80%. Users generally prefer music with higher energy levels. The valence was predominantly distributed around 50%. The acousticness gradually decreased as acousticness increased. Individuals preferred music with minimal instrumental elements. The liveliness reached a peak of 10 but subsequently declined. Lastly, the speechiness was only 5% initially but rapidly decreased as it increased.

- Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?
  ```python
  musical_attr = df[features]

  # Customize the pairplot
  sns.pairplot(
    musical_attr,
    plot_kws={
        'alpha': 0.3,        
        's': 70,
        'marker': 'o'
    }
  )
  ```
  **Output**:

  ![Screenshot 2024-11-03 at 11 09 54 PM](https://github.com/user-attachments/assets/e69d0787-6e98-4005-a4c0-b19eaa91c880)

  > Based on the output generated by the pairplot, it appears that there exists a correlation between danceability_% and energy_%. Specifically, a higher energy level is associated with a higher danceability_%. Furthermore, valence_% and danceability_% exhibit a stronger positive correlation compared to danceability_% and energy_%. Additionally, there is a significantly stronger positive correlation between valence and energy.

## Platform Popularity
- How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?
  ```python
  sources = ['in_spotify_playlists','in_spotify_charts', 'in_apple_playlists']

  track_sums = [df[src].sum() for src in sources] # Sum the tracks for each source

  data = pd.DataFrame({'Platform': sources, 'Tracks': track_sums})

  sns.barplot(x='Platform', y='Tracks', data=data); # Plot the results
  ```
  **Output**:

  ![Screenshot 2024-11-03 at 2 19 37 PM](https://github.com/user-attachments/assets/f339c3af-0776-4f9c-9703-e9be94ab21d0)

  > It appears that Spotify offers the most favorable platform for the most popular tracks.
  
## Advanced Analysis
- Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?
  ```python
  # Get the sum of all streams per key
  strkey = df.groupby('key')['streams'].sum()

  strms_df = strkey.reset_index()
  strkey.columns = ['key', 'streams']

  sns.barplot(x='key', y='streams', data=strms_df);
  ```
  **Output**:

  ![Screenshot 2024-11-05 at 12 08 05 AM](https://github.com/user-attachments/assets/2d8a8967-b05e-4f86-9efc-a1220f1aef13)

  > C# dominates all keys, making it the most frequently used key in streamed songs. Also, some keys have the same amount of use.

- Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.
  ```python
  filtered_df = df.copy()  # Make a copy of the original DataFrame

  platforms = [
    'in_spotify_playlists', 
    'in_spotify_charts', 
    'in_apple_playlists', 
    'in_apple_charts', 
    'in_deezer_playlists',
    'in_deezer_charts',
    'in_shazam_charts'
  ]

  # Create subplots for each platform
  fig, axes = plt.subplots(4, 2, figsize=(20, 18)) 
  axes = axes.flatten()

  for i, platform in enumerate(platforms):
    # Ensure the column is numeric and handle missing values
    filtered_df[platform] = pd.to_numeric(filtered_df[platform], errors='coerce').fillna(0)

    # Group, sum, and sort values.
    artists = filtered_df.groupby('artist(s)_name')[platform].sum().sort_values(ascending=False).reset_index()
    
    sns.barplot(x='artist(s)_name', y=platform, data=artists.head(), ax=axes[i])

  for j in range(len(platforms), len(axes)):
    axes[j].axis('off')

  plt.tight_layout()  
  plt.show()  
  ```
  **Output**:

  ![Screenshot 2024-11-05 at 12 46 30 AM](https://github.com/user-attachments/assets/e3fa5ce2-362e-4aae-842a-4860001b8c09)

  > Artists seem to be more prominent in playlists and charts. Among all playlists, Taylor Swift, The Weeknd, and Harry Styles are featured on every playlist. Ed Sheeran appears twice, while Eminem, Dua Lipa, Bruno Mars, and Maneskin appear once. In charts, Taylor Swift dominates, appearing on all charts, while Bad Bunny appears thrice, The Weeknd appears twice, Arctic Monkeys, Harry Styles, SZA, New Jeans, Miley Cyrus, One Republic, Olivia Rodrigo, Dr. Dre Snoop Dogg, Gurma, Central Cee, and only one other artist, Gurma, appear only once.

---

## Conclusion

  Our analysis of the Most Streamed Spotify Songs 2023 dataset has provided valuable insights into what makes a track popular on different streaming platforms. By examining trends, musical characteristics, and platform comparisons, we identified several factors that contribute to the success of these top tracks.

  - Key: C# is identified as the most popular key, with the highest number of streams associated with it.
  - Mode: Tracks in the Major mode tend to be preferred in terms of popularity.
  - BPM: A tempo within the heart rate range, ideally around 120 BPM, is recommended for wider appeal, as it's upbeat but not overly fast.
  - Energy: For a song to gain popularity, it should have moderate to high energy, generally within the 50-80% range.
  - Danceability: Songs that are danceable are generally better suited to capture and retain an audience.
  - Valence: Adding a positive feel or "vibe" to your song can increase its appeal, as listeners tend to favor songs with an upbeat tone.
  - Acousticness: Lowering acousticness can be beneficial, as highly acoustic tracks typically don't perform as well in terms of popularity.
  - Instrumentalness: Minimizing instrumental elements can make the track more relatable to a wider audience, as fully instrumental tracks may not connect as strongly with listeners.
  - Liveness: Tracks with lower liveness values tend to perform better, as high liveness can detract from mainstream appeal.
  - Speechiness: Similar to liveness, keeping speechiness low can make the song more appealing to listeners.
  - Platform Choice: Selecting the right streaming platform is crucial for reaching a broad audience and enhancing a song’s popularity.

  As streaming continues to shape the music industry, leveraging these insights can help artists create tracks that resonate widely and stand out in an increasingly competitive digital landscape.

---

## Version History
| Version | Description                                      | Date       |
| ------- | -------------------------------------------------| ---------- |
| 1.0.0   | Initial commit                                   | 10-20-2024 |
| 1.1.0   | Updated README.md                                | 10-29-2024 |
| 1.2.0   | Updated README.md                                | 11-02-2024 |
| 1.3.0   | Updated README.md and uploaded a csv file.       | 11-03-2024 |
| 1.4.0   | Updated README.md                                | 11-04-2024 |
| 1.5.0   | Updated README.md and uploaded the ipynb file.   | 11-05-2024 |
