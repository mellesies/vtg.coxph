# vantage.coxph

## Installation
Run the following in the R console to install the package and its dependencies:
```R
# This also installs the package vantage.infrastructure
devtools::install_github('mellesies/vantage.coxph')
```

## Example use
```R
# Load the package
library(vantage.coxph)

# Function to create a client
setup.client <- function() {
  # Define parameters
  username <- "username@example.com"
  password <- "password"
  collaboration_id <- 1
  host <- 'https://api-test.distributedlearning.ai'
  api_path <- ''
  
  # Create the client
  client <- Client$new(host, api_path=api_path)
  client$authenticate(username, password)
  client$setCollaborationId(collaboration_id)
  
  return(client)
}

# Create a client
client <- setup.client()

# The explanatory variables to include in the model.
expl_vars <- c()

# Time and censor columns ... 
time_col <- "Time"
censor_col <- "Censor"

# vantage.coxph contains the function `dcoxph`.
result <- dcoxph(client, expl_vars, time_col, censor_col)
```

## Example use for testing
```R
# Load the package
library(vantage.coxph)

# Load a dataset
data(SEER)
df <- SEER

# Variables frequently used as input for the RPC calls
expl_vars <- c("Age","Race2","Race3","Mar2","Mar3","Mar4","Mar5","Mar9",
               "Hist8520","hist8522","hist8480","hist8501","hist8201",
               "hist8211","grade","ts","nne","npn","er2","er4")
time_col <- "Time"
censor_col <- "Censor"

result <- dcoxph.mock(df, expl_vars, time_col, censor_col, splits=splits)
```
