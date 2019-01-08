# Data manipulation in R with dplyr

# Load the dplyr and hflights package

Welcome to the interactive exercises part of your `dplyr` course. Here you will learn the ins and outs of working with `dplyr`. `dplyr` is an R package, a collection of functions and data sets that enhance the R language.

Throughout this course you will use `dplyr` to analyze a data set of airline flight data containing flights that departed from Houston. This data is stored in a package called *hflights*.

Both `dplyr` and `hflights` are already installed on DataCamp's servers, so loading them with `library()`will get you up and running.

##### Instructions

100 XP

##### Instructions

100 XP

- Load the `dplyr` package.
- Load the `hflights` package. A variable called `hflights` will become available, a data.frame representing the data set.
- Use both [`head()`](http://www.rdocumentation.org/packages/multivator/functions/head) and [`summary()`](http://www.rdocumentation.org/packages/base/functions/summary) on the `hflights` data frame to get to know the data. Can you guess the meaning of all variables?

- 

- ```R
  # Load the dplyr package
  library(dplyr)
  
  # Load the hflights package
  library(hflights)
  
  # Call both head() and summary() on hflights
  head(hflights)
  summary(hflights)
  ```

- 

# Explore the data set

A data scientist must be familiar with his or her data. Experiment with the data set in the console and maybe try to generate some insightful plots. For your convenience, `hflights` is already loaded into the workspace.

How many observations and how many variables are contained in the `hflights` data set?

# Convert data.frame to tibble

As Garrett explained, a **tbl** (pronounced *tibble*) is just a special kind of data.frame. They make your data easier to look at, but also easier to work with. On top of this, it is straightforward to derive a tbl from a data.frame structure using [`as_tibble()`](http://www.rdocumentation.org/packages/dplyr/functions/as_tibble).

The tbl format changes how R displays your data, but it does not change the data's underlying data structure. A tbl inherits the original class of its input, in this case, a data.frame. This means that you can still manipulate the tbl as if it were a data.frame. In other words, you can do anything with the `hflights` tbl that you could do with the `hflights` data.frame.

##### Instructions

100 XP

- Convert `hflights_df` (which is a data.frame) into a tbl, also named `hflights`.
- Display the new `hflights` in your console window. Notice the easy-to-read layout.
- To see how tbls behave like data.frames, save the `UniqueCarrier` column of `hflights` as an object named `carriers`, using base R syntax only.

- ```R
  # Both the dplyr and hflights packages are loaded
  
  # Convert the hflights_df data.frame into a hflights tbl
  hflights <- as_tibble(hflights_df)
  
  # Display the hflights tbl
  hflights
  
  # Create the object carriers
  carriers <<- hflights$UniqueCarrier
  ```

- # Changing labels of hflights, part 1 of 2

- A bit of cleaning would be a good idea since the `UniqueCarrier` variable of `hflights` uses a confusing code system.

- To do this, let's work with a lookup table, that comes in the form of a named vector. When you subset the lookup table with a character string (like the character strings in `UniqueCarrier`), R will return the values of the lookup table that correspond to the names in the character string. To see how this works, run following code in the console:

- ```
  two <- c("AA", "AS")
  lut <- c("AA" = "American", 
           "AS" = "Alaska", 
           "B6" = "JetBlue")
  two <- lut[two]
  two
  ```

- ##### Instructions

- 100 XP

- ##### Instructions

- 100 XP

- - Add a new `Carrier` column to `hflights` by combining `lut` with the `UniqueCarrier` column of `hflights`.
  - It's rather hard to see if you did things right, since the `Carrier` variable does not appear when you print `hflights`. Use the [`glimpse()`](http://www.rdocumentation.org/packages/dplyr/functions/glimpse) function on `hflights` instead.

```R
# Both the dplyr and hflights packages are loaded into workspace
lut <- c("AA" = "American", "AS" = "Alaska", "B6" = "JetBlue", "CO" = "Continental", 
         "DL" = "Delta", "OO" = "SkyWest", "UA" = "United", "US" = "US_Airways", 
         "WN" = "Southwest", "EV" = "Atlantic_Southeast", "F9" = "Frontier", 
         "FL" = "AirTran", "MQ" = "American_Eagle", "XE" = "ExpressJet", "YV" = "Mesa")

# Add the Carrier column to hflights
hflights$Carrier <- lut[hflights$UniqueCarrier]

# Glimpse at hflights
glimpse(hflights)
```

# Changing labels of hflights, part 2 of 2

Let's try a similar thing, but this time to change the labels in the `CancellationCode` column. This column lists reasons why a flight was cancelled using a non-informative alphabetical code. Execute

```
unique(hflights$CancellationCode)
```

A lookup table `lut` has already been created for you, that converts the alphabetical codes into more meaningful strings.

##### Instructions

100 XP

- Use `lut` to change the labels of the `CancellationCode` column of `hflights`. Store the recoded vector in a new column `Code`.
- As before, check your results by glimpsing at them.

- 

- ```R
  # The hflights tbl you built in the previous exercise is available in the workspace.
  
  # The lookup table
  lut <- c("A" = "carrier", "B" = "weather", "C" = "FFA", "D" = "security", "E" = "not cancelled")
  
  # Add the Code column
  hflights$Code <- lut[hflights$CancellationCode]
  
  # Glimpse at hflights
  glimpse(hflights)
  ```

- 

# The five verbs and their meaning

The `dplyr` package contains five key data manipulation functions, also called verbs:

- [`select()`](http://www.rdocumentation.org/packages/dplyr/functions/select), which returns a subset of the columns,
- [`filter()`](http://www.rdocumentation.org/packages/dplyr/functions/filter), that is able to return a subset of the rows,
- [`arrange()`](http://www.rdocumentation.org/packages/dplyr/functions/arrange), that reorders the rows according to single or multiple variables,
- [`mutate()`](http://www.rdocumentation.org/packages/dplyr/functions/mutate), used to add columns from existing data,
- [`summarize()`](http://www.rdocumentation.org/packages/dplyr/functions/summarise), which reduces each group to a single row by calculating aggregate measures.

If you want to find out more about these functions, consult the documentation by clicking on the functions above. What order of operations should we use to find the average value of the `ArrDelay`(arrival delay) variable for all American Airline flights in the `hflights`tbl?

Feel free to play around in the console; `hflights` is preloaded. From now on, the `UniqueCarrier` column and `CancellationCode` column contain the recoded versions, similar to the cleaning up you did in the previous chapter.

# Choosing is not losing! The select verb

To answer the simple question whether flight delays tend to shrink or grow during a flight, we can safely discard a lot of the variables of each flight. To select only the ones that matter, we can use [`select()`](http://www.rdocumentation.org/packages/dplyr/functions/select).

As an example, take the following call, that selects the variables `var1` and `var2` from the data frame `df`.

```
select(df, var1, var2)
```

You can also use `:` to select a range of variables and `-` to exclude some variables, similar to indexing a data.frame with square brackets. You can use both variable's names as well as integer indexes. This call selects the four first variables except for the second one of a data frame `df`:

```
select(df, 1:4, -2)
```

[`select()`](http://www.rdocumentation.org/packages/dplyr/functions/select) does not change the data frame it is called on; you have to explicitly assign the result of `select()`to a variable to store the result.

##### Instructions

100 XP

- Use [`select()`](http://www.rdocumentation.org/packages/dplyr/functions/select) to print out a tbl that contains only the columns `ActualElapsedTime`, `AirTime`, `ArrDelay` and `DepDelay` of `hflights`.
- Print out a tbl with the columns `Origin` up to and including `Cancelled` of `hflights`.
- Find the most concise way to select: columns `Year` up to and including `DayOfWeek`, columns `ArrDelay` up to and including `Diverted`. You can examine the order of the variables in `hflights` with `names(hflights)` in the console.

```R
# hflights is pre-loaded as a tbl, together with the necessary libraries.

# Print out a tbl with the four columns of hflights related to delay
select(hflights,ActualElapsedTime,
AirTime,ArrDelay,DepDelay)

# Print out the columns Origin up to Cancelled of hflights
select(hflights,Origin:Cancelled)

# Answer to last question: be concise!
select(hflights,1:4,ArrDelay:Diverted)
```

# Helper functions for variable selection

`dplyr` comes with a set of helper functions that can help you select groups of variables inside a [`select()`](http://www.rdocumentation.org/packages/dplyr/functions/select)call:

- `starts_with("X")`: every name that starts with `"X"`,
- `ends_with("X")`: every name that ends with `"X"`,
- `contains("X")`: every name that contains `"X"`,
- `matches("X")`: every name that matches `"X"`, where `"X"` can be a regular expression,
- `num_range("x", 1:5)`: the variables named `x01`, `x02`, `x03`, `x04` and `x05`,
- `one_of(x)`: every name that appears in `x`, which should be a character vector.

Pay attention here: When you refer to columns directly inside [`select()`](http://www.rdocumentation.org/packages/dplyr/functions/select), you don't use quotes. If you use the helper functions, you do use quotes.

##### Instructions

100 XP

##### Instructions

100 XP

- Use [`select()`](http://www.rdocumentation.org/packages/dplyr/functions/select) and a helper function to print out a tbl that contains just `ArrDelay` and `DepDelay` of `hflights`.

- Use a combination of helper functions and variable names to print out only the `UniqueCarrier`, `FlightNum`, `TailNum`, `Cancelled`, and `CancellationCode` columns of `hflights`.

- Find the most concise way to return the following columns with `select` and its helper functions:`DepTime`, `ArrTime`, `ActualElapsedTime`, `AirTime`, `ArrDelay`, `DepDelay`. Use only helper functions!

  ```R
  # As usual, hflights is pre-loaded as a tbl, together with the necessary libraries.
  
  # Print out a tbl containing just ArrDelay and DepDelay
  select(hflights,ends_with("Delay"))
  
  # Print out a tbl as described in the second instruction, using both helper functions and variable names
  select(hflights,7:9,19:20)
  
  # Print out a tbl as described in the third instruction, using only helper functions.
  select(hflights,ends_with("Time"),ends_with("Delay"))
  ```

# Comparison to base R

To see the added value of the `dplyr` package, it is useful to compare its syntax with base R. Up to now, you have only considered functionality that is also available without the use of `dplyr`. The elegance and ease-of-use of `dplyr` is a great plus though.

##### Instructions

100 XP

Finish the `select()` calls to match the results of the base R commands. Try to make your calls as concise as possible.

```R
# both hflights and dplyr are available

# Finish select call so that ex1d matches ex1r
ex1r <- hflights[c("TaxiIn", "TaxiOut", "Distance")]
ex1d <- select(hflights, contains("Taxi"), Distance)

# Finish select call so that ex2d matches ex2r
ex2r <- hflights[c("Year", "Month", "DayOfWeek", "DepTime", "ArrTime")]
ex2d <- select(hflights, Year:ArrTime, -DayofMonth)

# Finish select call so that ex3d matches ex3r
ex3r <- hflights[c("TailNum", "TaxiIn", "TaxiOut")]
ex3d <- select(hflights, starts_with("T"))
```

# both hflights and dplyr are available

# Finish select call so that ex1d matches ex1r
ex1r <- hflights[c("TaxiIn", "TaxiOut", "Distance")]
ex1d <- select(hflights, contains("Taxi"), Distance)

# Finish select call so that ex2d matches ex2r
ex2r <- hflights[c("Year", "Month", "DayOfWeek", "DepTime", "ArrTime")]
ex2d <- select(hflights, Year:ArrTime, -DayofMonth)

# Finish select call so that ex3d matches ex3r
ex3r <- hflights[c("TailNum", "TaxiIn", "TaxiOut")]
ex3d <- select(hflights, starts_with("T"))

```R
# hflights and dplyr are loaded and ready to serve you.

# Add the new variable ActualGroundTime to a copy of hflights and save the result as g1.
g1 <- mutate(hflights,ActualGroundTime=ActualElapsedTime - AirTime)

# Add the new variable GroundTime to g1. Save the result as g2.
 g2 <- mutate(g1,GroundTime = TaxiIn + TaxiOut)

# Add the new variable AverageSpeed to g2. Save the result as g3.
g3 <- mutate(g2, AverageSpeed = 60 * Distance / AirTime )

# Print out g3
g3
```

# Add multiple variables using mutate

So far you've added variables to hflights one at a time, but you can also use [`mutate()`](http://www.rdocumentation.org/packages/dplyr/functions/mutate) to add multiple variables at once. To create more than one variable, place a comma between each variable that you define inside [`mutate()`](http://www.rdocumentation.org/packages/dplyr/functions/mutate).

[`mutate()`](http://www.rdocumentation.org/packages/dplyr/functions/mutate) even allows you to use a new variable while creating a next variable in the same call. In this example, the new variable `x` is directly reused to create the new variable `y`:

```
mutate(my_df, x = a + b, y = x + c)
```

##### Instructions

100 XP

##### Instructions

100 XP

- Adapt the code that builds `m1`: add a variable `loss_ratio`, which is the ratio of `loss` to `DepDelay`.
- Create a tbl `m2` from `hflights` by adding three variables:
- `TotalTaxi`, which is the sum of `TaxiIn` and `TaxiOut`;
- `ActualGroundTime`, which is the difference of `ActualElapsedTime` and `AirTime`;
- `Diff`, the difference between the two newly created variables. This column should be zero for all observations!

```R
# hflights and dplyr are ready, are you?

# Add a second variable loss_ratio to the dataset: m1
m1 <- mutate(hflights, loss = ArrDelay - DepDelay,
loss_ratio = loss/DepDelay)

# Add the three variables as described in the third instruction: m2
m2 <- mutate(hflights,TotalTaxi = TaxiIn+TaxiOut,
ActualGroundTime = ActualElapsedTime - AirTime,
Diff = TotalTaxi - ActualGroundTime)
```

