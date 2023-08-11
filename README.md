# BCycle Trip Data

The dataset was provided by Houston BikeShare that operates Houston BCycle, a bicycle sharing system. 

## The Data

The data is located in data/BikeShare Trips.



### Option to combine files

If helpful, here's some R code to combine csv's into one dataframe.
It's a lot of data so feel free to adjust how much you read in at a time.

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

## Data Dictionary