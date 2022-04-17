I provide three ways to assess the data.

1. The file "cleaned_dataset.csv" is the dataset after cleaning and data manipulation. This is the dataset I used to perform EDA, analyzing, and modeling. You can use read_csv() to directly read this data into R.

2. We also provided the raw data in this directory. You can apply read_csv() directly on the path 'data/rankings_1973-2017_csv.csv' and 'player_overviews_unindexed_csv.csv' after unzipping the zip file "player_overviews_unindexed_csv.zip" in data directory. If you are in the top level of the directory, the code to load these raw dataset is given below:
```{r}
data_raw1 <- read_csv('data/player_overviews_unindexed_csv.csv')
data_raw2 <- readr::read_csv(unzip('data/rankings_1973-2017_csv.zip'))
```

3. Lastly, we provided a way to download the dataset from website. Run the following code to download the raw datasets.
```{r}
library("jsonlite")

# Obtain the json file
json_file <- 'https://datahub.io/sports-data/atp-world-tour-tennis-data/datapackage.json'
json_data <- fromJSON(paste(readLines(json_file), collapse=""))

# get list of all resources:
print(json_data$resources$name)

# from the list of all resources, we found that the file describing the rankings of players from 1973 to 2017 is at index 9. Then we obtain the path of the 9th file, and load it.
path_to_file = json_data$resources$path[9]
data_raw2 <- read.csv(url(path_to_file))

# from the list of all resources, we found that the file describing the physical characteristic of players is at index 10. Then we obtain the path of the 10th file, and load it.
path_to_file = json_data$resources$path[10]
data_raw1 <- read.csv(url(path_to_file))
```