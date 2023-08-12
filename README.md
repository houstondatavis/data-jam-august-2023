# BCycle Trip Data

The dataset was provided by Houston BikeShare that operates Houston BCycle, a bicycle sharing system. 

## The Data

The data is located in data/BikeShare Trips.



### Option to combine files

If helpful, here's some R code to combine csv's into one dataframe.
It's a lot of data so feel free to adjust how much you read in at a time.
By default it reads the data in as characters, so be sure to adjust the column types as needed.

```
library(readr)
library(dplyr)


combine_csvs <- function(folder_path) {
  # Get list of file paths of eah csv
  file_paths <- list.files(path = folder_path, 
                           pattern = "*.csv", 
                            full.names = TRUE)
                           
  data_list <- list()

  # Read in each csv as a dataframe
  for (file_path in file_paths) {
    data <- read_csv(file_path, col_types = cols(.default = "c"))
    
    data_list[[file_path]] <- data
  }
  
  data <- bind_rows(data_list)
  return(data)
}

df <- combine_csvs("data/BikeShareTrips/")
```

### Other Related Data

A google sheet that has on its right side demographics data calculated for bike stations
https://docs.google.com/spreadsheets/d/1v6nwIHXWr8oG-NAxIRwOjZEQamURJpEXcgNJtlO1lQI/edit?usp=sharing
This uses the "magic spreadsheet" shown here: https://source.opennews.org/articles/magic-spreadsheets-neighborhood-inequities/
