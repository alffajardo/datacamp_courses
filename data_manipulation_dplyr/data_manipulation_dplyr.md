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

# Logical operators

R comes with a set of logical operators that you can use inside [`filter()`](http://www.rdocumentation.org/packages/dplyr/functions/filter):

- `x < y`, `TRUE` if `x` is *less than* `y`
- `x <= y`, `TRUE` if `x` is *less than or equal to* `y`
- `x == y`, `TRUE` if `x` *equals* `y`
- `x != y`, `TRUE` if `x` *does not equal* `y`
- `x >= y`, `TRUE` if `x` *is greater than or equal to* `y`
- `x > y`, `TRUE` if `x` is *greater than* `y`
- `x %in% c(a, b, c)`, `TRUE` if `x` is in the vector `c(a, b, c)`

The following example filters `df` such that only the observations for which `a` is positive, are kept:

```
filter(df, a > 0)
```

##### Instructions

100 XP

- Print out all flights in `hflights` that traveled 3000 or more miles.
- Print out all flights in `hflights` flown by JetBlue, Southwest, or Delta.
- Extract from `hflights` all flights where taxiing took longer than the actual flight. Avoid the use of [`mutate()`](http://www.rdocumentation.org/packages/dplyr/functions/mutate) and do the math directly in the logical expression of [`filter()`](http://www.rdocumentation.org/packages/dplyr/functions/filter).

- 

- ```R
  # hflights is at your disposal as a tbl, with clean carrier names
  
  # All flights that traveled 3000 miles or more
  filter(hflights, Distance >= 3000)
  
  # All flights flown by JetBlue, Southwest, or Delta
  filter(hflights, UniqueCarrier %in% c("JetBlue", "Southwest", "Delta"))
  
  # All flights where taxiing took longer than flying
  filter(hflights, TaxiIn + TaxiOut > AirTime)
  ```

- 

# Combining tests using boolean operators

R  also comes with a set of boolean operators that you can use to combine  multiple logical tests into a single test. These include `&` (and), `|` (or), and `!` (not). Instead of using the `&` operator, you can also pass several logical tests to [`filter()`](http://www.rdocumentation.org/packages/dplyr/functions/filter), separated by commas. The following two calls are completely equivalent:

```
filter(df, a > 0 & b > 0)
filter(df, a > 0, b > 0)
```

Next, [`is.na()`](http://www.rdocumentation.org/packages/base/functions/NA) will also come in handy. This example keeps the observations in `df` for which the variable `x` is *not* `NA`:

```
filter(df, !is.na(x))
```

##### Instructions

100 XP

- Use R's logical and boolean operators to select just the rows where a  flight left before 5:00 am (500) or arrived after 10:00 pm (2200).

- Print out all of the flights that departed late but arrived ahead of schedule. Use `DepDelay` and `ArrDelay` for this.

- Find all of the flights that were cancelled after being delayed. These are flights that were cancelled, while having a `DepDelay` greater than zero.

  ```R
  # hflights is at your service as a tbl!
  
  # All flights that departed before 5am or arrived after 10pm
  filter(hflights,DepTime<500 | ArrTime > 2200 )
  
  # All flights that departed late but arrived ahead of schedule
  filter(hflights,DepDelay > 0,ArrDelay <0)
  
  # All flights that were cancelled after being delayed
  filter(hflights,DepDelay > 0, Cancelled == 1)
  ```

  # Blend together what you've learned!

  So far, you have learned three data manipulation functions in the `dplyr` package. Time for a summarizing exercise. You will generate a new dataset from the `hflights` dataset that contains some useful information on flights that had JFK airport as their destination. You will need [`select()`](http://www.rdocumentation.org/packages/dplyr/functions/select), [`mutate()`](http://www.rdocumentation.org/packages/dplyr/functions/mutate) and [`filter()`](http://www.rdocumentation.org/packages/dplyr/functions/filter).

  ##### Instructions

  100 XP

  - First, use [`filter()`](http://www.rdocumentation.org/packages/dplyr/functions/filter) to select the flights that had JFK as their destination and save this result to `c1`.
  - Second, add a new column named `Date` to `c1`: [`paste()`](http://www.rdocumentation.org/packages/base/functions/paste) together the `Year`, `Month` and `DayofMonth` variables, separate them by a "-" by using the `sep` attribute of [`paste()`](http://www.rdocumentation.org/packages/base/functions/paste). Save the resulting data frame as `c2`.
  - Finally, select some columns to provide an overview: `Date`, `DepTime`, `ArrTime` and `TailNum`, in this order. Do not assign the resulting data frame to a variable; just print it to the console.

  - ```R
    # hflights is already available in the workspace
    
    # Select the flights that had JFK as their destination: c1
    c1 <- filter(hflights,Dest == "JFK")
    
    # Combine the Year, Month and DayofMonth variables to create a Date column: c2
    c2 <- mutate(c1,Date = paste(Year,Month,DayofMonth,sep="-"))
    
    # Print out a selection of columns of c2
    select(c2,Date,DepTime,ArrTime,TailNum)
    ```

  - 

[`arrange()`](http://www.rdocumentation.org/packages/dplyr/functions/arrange) can be used to rearrange rows according to any type of data. If you pass [`arrange()`](http://www.rdocumentation.org/packages/dplyr/functions/arrange)  a character variable, for example, R will rearrange the rows in  alphabetical order according to values of the variable. If you pass a  factor variable, R will rearrange the rows according to the order of the  levels in your factor (running [`levels()`](http://www.rdocumentation.org/packages/base/functions/levels) on the variable reveals this order).

`dtc` has already been defined on the right. It's up to you to write some `arrange()` expressions to display its contents appropriately!

##### Instructions

100 XP

- Arrange `dtc`, by departure delays so that the shortest departure delay is at the top of the data set.
- Arrange `dtc` so that flights that were cancelled for the same reason appear next to each other.
- Arrange `dtc` so that flights by the same carrier appear  next to each other. Within each carrier, flights that have smaller  departure delays appear before flights that have higher departure  delays. Do this in a one-liner.

```R
# dplyr and the hflights tbl are available

# Definition of dtc
dtc <- filter(hflights, Cancelled == 1, !is.na(DepDelay))

# Arrange dtc by departure delays
arrange(dtc,DepDelay)

# Arrange dtc so that cancellation reasons are grouped
  arrange(dtc,CancellationCode)

# Arrange dtc according to carrier and departure delays
arrange(dtc,UniqueCarrier,DepDelay)
```

# Reverse the order of arranging

By default, [`arrange()`](http://www.rdocumentation.org/packages/dplyr/functions/arrange) arranges the rows from *smallest to largest*. Rows with the smallest value of the variable will appear at the top of the data set. You can reverse this behavior with the [`desc()`](http://www.rdocumentation.org/packages/dplyr/functions/desc) function. [`arrange()`](http://www.rdocumentation.org/packages/dplyr/functions/arrange) will reorder the rows from *largest to smallest* values of a variable if you wrap the variable name in [`desc()`](http://www.rdocumentation.org/packages/dplyr/functions/desc) before passing it to [`arrange()`](http://www.rdocumentation.org/packages/dplyr/functions/arrange).

##### Instructions

100 XP

- Arrange `hflights` so that flights by the same carrier  appear next to each other and within each carrier, flights that have  larger departure delays appear before flights that have smaller  departure delays.
- Arrange the flights in `hflights` by their total delay (the sum of `DepDelay` and `ArrDelay`). Try to do this directly inside [`arrange()`](http://www.rdocumentation.org/packages/dplyr/functions/arrange)

```R
# dplyr and the hflights tbl are available

# Arrange according to carrier and decreasing departure delays
arrange(hflights, UniqueCarrier, desc(DepDelay))

# Arrange flights by total delay (normal order).
arrange(hflights, DepDelay + ArrDelay)
```

```R
# hflights and dplyr are loaded in the workspace

# Print out a summary with variables min_dist and max_dist
summarize(hflights, min_dist = min(Distance), max_dist = max(Distance))

# Print out a summary with variable max_div
summarize(filter(hflights, Diverted == 1), max_div = max(Distance))
```

# Aggregate functions

You can use any function you like in [`summarize()`](http://www.rdocumentation.org/packages/dplyr/functions/summarise) so long as the function can take a vector of data and return a single number. R contains many *aggregating* functions, as `dplyr` calls them:

- [`min(x)`](http://www.rdocumentation.org/packages/base/functions/Extremes) - minimum value of vector `x`.
- [`max(x)`](http://www.rdocumentation.org/packages/base/functions/Extremes) - maximum value of vector `x`.
- [`mean(x)`](http://www.rdocumentation.org/packages/base/functions/mean) - mean value of vector `x`.
- [`median(x)`](http://www.rdocumentation.org/packages/stats/functions/median) - median value of vector `x`.
- [`quantile(x, p)`](http://www.rdocumentation.org/packages/stats/functions/quantile) - `p`th quantile of vector `x`.
- [`sd(x)`](http://www.rdocumentation.org/packages/stats/functions/sd) - standard deviation of vector `x`.
- [`var(x)`](http://www.rdocumentation.org/packages/stats/functions/cor) - variance of vector `x`.
- [`IQR(x)`](http://www.rdocumentation.org/packages/stats/functions/IQR) - Inter Quartile Range (IQR) of vector `x`.
- `diff(range(x))` - total range of vector `x`.

##### Instructions

100 XP

- Remove rows that have `NA`s in the arrival delay column and save the resulting dataset to `temp1`. 

- Print out a summary of `temp1` with the following variables (in this order):

- `earliest`: the minimum arrival delay,

- `average`: the average arrival delay,

- `latest`: the longest arrival delay,

- `sd`: the standard deviation for arrival delays.

- Filter `hflights` such that only rows that have no NA `TaxiIn` *and* no NA `TaxiOut` are kept; save this temporary result to `temp2`. 

- Print out a summary of `temp2`, with one variable, `max_taxi_diff`: the biggest absolute difference in time between `TaxiIn` and `TaxiOut` for a single flight.

  ```R
  # hflights is available
  
  # Remove rows that have NA ArrDelay: temp1
  temp1 <- filter(hflights,!is.na(ArrDelay))
  
  # Generate summary about ArrDelay column of temp1
  summarize(temp1,earliest = min(ArrDelay),
  average = mean(ArrDelay),
  latest = max(ArrDelay),
  sd = sd(ArrDelay))
  
  # Keep rows that have no NA TaxiIn and no NA TaxiOut: temp2
  temp2 <- filter(hflights,!is.na(TaxiIn),!is.na(TaxiOut))
  
  # Print the maximum taxiing difference of temp2 with summarize()
  summarize(temp2,max_taxi_diff= max(abs(TaxiOut - TaxiIn)))
  ```

  

# dplyr aggregate functions

`dplyr` provides several helpful aggregate functions of its own, in addition to the ones that are already defined in R. These include:

- [`first(x)`](http://www.rdocumentation.org/packages/dplyr/functions/nth) - The first element of vector `x`.
- [`last(x)`](http://www.rdocumentation.org/packages/dplyr/functions/nth) - The last element of vector `x`.
- [`nth(x, n)`](http://www.rdocumentation.org/packages/dplyr/functions/nth) - The `n`th element of vector `x`.
- [`n()`](http://www.rdocumentation.org/packages/dplyr/functions/n) - The number of rows in the data.frame or group of observations that [`summarize()`](http://www.rdocumentation.org/packages/dplyr/functions/summarise) describes.
- [`n_distinct(x)`](http://www.rdocumentation.org/packages/dplyr/functions/n_distinct) - The number of unique values in vector `x`.

Next to these `dplyr`-specific functions, you can also turn a logical test into an aggregating function with [`sum()`](http://www.rdocumentation.org/packages/base/functions/sum) or [`mean()`](http://www.rdocumentation.org/packages/base/functions/mean). A logical test returns a vector of `TRUE`'s and `FALSE`'s. When you apply [`sum()`](http://www.rdocumentation.org/packages/base/functions/sum) or [`mean()`](http://www.rdocumentation.org/packages/base/functions/mean) to such a vector, R coerces each `TRUE` to a 1 and each `FALSE` to a 0. [`sum()`](http://www.rdocumentation.org/packages/base/functions/sum) then represents the total number of observations that passed the test; [`mean()`](http://www.rdocumentation.org/packages/base/functions/mean) represents the proportion.

##### Instructions

100 XP

- Print out a summary of `hflights` with the following variables:
- `n_obs`: the total number of observations,
- `n_carrier`: the total number of carriers,
- `n_dest`: the total number of destinations,
- `aa`, a tbl with all flights flown by American Airlines, is already available.
- Print out a summary of `aa` with the following variables:
- `n_flights`: the total number of flights (each observation is a flight),
- `n_canc`: the total number of cancelled flights,
- `avg_delay`: the average arrival delay of flights whose delay is not `NA` (`na.rm = TRUE`).

```R
# hflights is available with full names for the carriers

# Generate summarizing statistics for hflights
summarize(hflights, 
          n_obs = n(), 
          n_carrier = n_distinct(UniqueCarrier), 
          n_dest = n_distinct(Dest))

# All American Airline flights
aa <- filter(hflights, UniqueCarrier == "American")

# Generate summarizing statistics for aa 
summarize(aa, 
          n_flights = n(), 
          n_canc = sum(Cancelled == 1),
          avg_delay = mean(ArrDelay, na.rm = TRUE))
```

# Overview of syntax

As another example of the `%>%`, have a look at the following two commands that are completely equivalent:

```
mean(c(1, 2, 3, NA), na.rm = TRUE)
c(1, 2, 3, NA) %>% mean(na.rm = TRUE)
```

The `%>%` operator allows you to extract the first  argument of a function from the arguments list and put it in front of  it, thus solving the *Dagwood sandwich problem*.

##### Instructions

100 XP

Use `dplyr` functions and the pipe operator to transform the following English sentences into R code:

- Take the hflights data set *and then* ...
- Add a variable named `diff` that is the result of subtracting `TaxiIn` from `TaxiOut`, *and then* ...
- Pick all of the rows whose `diff` value does not equal `NA`, *and then* ...
- Summarize the data set with a value named `avg` that is the mean `diff` value.

- ```R
  # hflights and dplyr are both loaded and ready to serve you
  
  # Write the 'piped' version of the English sentences.
  hflights %>%
  mutate(diff = TaxiOut - TaxiIn) %>%
  filter(!is.na(diff))%>%
  summarize(avg = mean(diff))
  ```


Drive or fly? Part 1 of 2

You can answer sophisticated questions by combining the verbs of dplyr. Over the next few exercises you will examine whether it sometimes makes sense to drive instead of fly. You will begin by making a data set that contains relevant variables. Then, you will find flights whose equivalent average velocity is lower than the velocity when traveling by car.

In the following instructions, you have to carry out a series of dplyr verbs on the hflights dataset. Make sure to use the %>% operator to chain them all together.
Instructions
100 XP

```R
mutate() the hflights dataset and add two variables:
    RealTime: the actual elapsed time plus 100 minutes (for the overhead that flying involves) and
    mph: calculated as 60 times Distance divided by RealTime, then
filter() to keep observations that have an mph that is not NA and that is below 70, finally
summarize() the result by creating four summary variables:
    n_less, the number of observations,
    n_dest, the number of destinations,
    min_dist, the minimum distance and
    max_dist, the maximum distance.
```
```R
# Chain together mutate(), filter() and summarize()
hflights %>%
mutate(RealTime = ActualElapsedTime+ 100,mph = (60*Distance)/RealTime) %>%
filter(!is.na(mph) & mph <70) %>%
summarize(n_less = n(),n_dest = n_distinct(Dest),
min_dist = min(Distance),
max_dist = max(Distance))
```

# Drive or fly? Part 2 of 2

The  previous exercise suggested that some flights might be less efficient  than driving in terms of speed. But is speed all that matters? Flying  imposes burdens on a traveler that driving does not. For example,  airplane tickets are very expensive. Air travelers also need to limit  what they bring on their trip and arrange for a pick up or a drop off.  Given these burdens we might demand that a flight provide a large speed  advantage over driving.

Let's define preferable flights as flights that are at least 50%  faster than driving, i.e. that travel 105 mph or greater in real time.  Also, assume that cancelled or diverted flights are less preferable than  driving. 

The `mutate()` call from the previous exercise is already coded up; can you add more pipes and verbs to the command?

##### Instructions

100 XP

- `filter()` the result of mutate to:
- keep observations that have an `mph` under 105 *or* for which `Cancelled` equals 1 *or* for which `Diverted` equals 1.
- `summarize()` the result by creating four summary variables:
- `n_non`, the number of observations,
- `n_dest`, the number of destinations,
- `min_dist`, the minimum distance and
- `max_dist`, the maximum distance.

```R
# Finish the command with a filter() and summarize() call
hflights %>%
  mutate(
    RealTime = ActualElapsedTime + 100, 
    mph = 60 * Distance / RealTime
  ) %>%
filter(mph < 105 | Cancelled ==1 | Diverted ==1) %>%
summarize(n_non = n(),
n_dest = n_distinct(Dest),
min_dist = min(Distance),
max_dist = max(Distance))
```

# Advanced piping exercise

Let's use `hflights` to answer another question: How many flights were overnight flights?

##### Instructions

100 XP

- `filter()` the `hflights` tbl to keep only observations whose `DepTime` is not `NA`, whose `ArrTime` is not `NA` and for which `DepTime` exceeds `ArrTime`.
- Pipe the result into a `summarize()` call to create a single summary variable: `num`, that simply counts the number of observations.

- ```R
  # hflights and dplyr are loaded
  
  # Count the number of overnight flights
  hflights %>%
  filter(!is.na(DepTime),!is.na(ArrTime),DepTime >ArrTime) %>%
  summarize(num = n())
  
  ```

- ```R
  # hflights is in the workspace as a tbl, with translated carrier names
  
  # Make an ordered per-carrier summary of hflights
  hflights %>%
     group_by(UniqueCarrier) %>%
     summarize(
       p_canc = 100 * mean(Cancelled == 1), 
       avg_delay = mean(ArrDelay, na.rm = TRUE)
     ) %>%
     arrange(avg_delay, p_canc)
  ```

- # Combine group_by with mutate

- You can also combine [`group_by()`](http://www.rdocumentation.org/packages/dplyr/functions/group_by) with [`mutate()`](http://www.rdocumentation.org/packages/dplyr/functions/mutate). When you mutate grouped data, [`mutate()`](http://www.rdocumentation.org/packages/dplyr/functions/mutate) will calculate the new variables independently for each group. This is particularly useful when [`mutate()`](http://www.rdocumentation.org/packages/dplyr/functions/mutate) uses the [`rank()`](http://www.rdocumentation.org/packages/base/functions/rank) function, that calculates within-group rankings. [`rank()`](http://www.rdocumentation.org/packages/base/functions/rank) takes a group of values and calculates the rank of each value within the group, e.g.

- ```
  rank(c(21, 22, 24, 23))
  ```

- has output

- ```
  [1] 1 2 4 3
  ```

- As with [`arrange()`](http://www.rdocumentation.org/packages/dplyr/functions/arrange), [`rank()`](http://www.rdocumentation.org/packages/base/functions/rank) ranks values from the smallest to the largest.

- ##### Instructions

- 100 XP

- - `filter()` the `hflights` tbl to only keep observations for which `ArrDelay` is not `NA` and positive.
  - Use `group_by()` on the result to group by `UniqueCarrier`.
  - Next, use `summarize()` to calculate the average `ArrDelay` per carrier. Call this summary variable `avg`.
  - Feed the result into a `mutate()` call: create a new variable, `rank`, calculated as `rank(avg)`.
  - Finally, arrange by this new `rank` variable

```R
# dplyr is loaded, hflights is loaded with translated carrier names

# Ordered overview of average arrival delays per carrier
hflights %>%
filter(!is.na(ArrDelay),ArrDelay>0) %>%
group_by(UniqueCarrier) %>%
summarize(avg = mean(ArrDelay)) %>%
mutate(rank = rank(avg)) %>%
arrange(rank)
```

# Advanced group_by exercises

By now you've learned the fundamentals of `dplyr`: the five data manipulation verbs and the additional [`group_by()`](http://www.rdocumentation.org/packages/dplyr/functions/group_by)  function to discover interesting group-wise statistics. The next  challenges are an all-encompassing review of the concepts you have  learned about. We already provided you with a template of the piped call  that can solve the exercises. Up to you to finish all `dplyr` calls! For simplicity, you can include cancelled flights in your answers, so you shouldn't filter based on the `Cancelled` column.

##### Instructions

100 XP

- How many airplanes flew to only one destination? The tbl you print out should have a single column, named `nplanes` and a single row.

- Find the most visited destination for each carrier. The tbl you print out should contain four columns:

- `UniqueCarrier` and `Dest`,

- `n`, how often a carrier visited a particular destination,

- `rank`, how each destination ranks per carrier. `rank` should be 1 for every row, as you want to find the most visited destination for each carrier.

  ```R
  # dplyr and hflights (with translated carrier names) are pre-loaded
  
  # How many airplanes only flew to one destination?
  hflights %>%
    group_by(TailNum) %>%
    summarize(ndest = n_distinct(Dest)) %>%
    filter(ndest == 1) %>%
    summarize(nplanes = n())
  
  # Find the most visited destination for each carrier
  hflights %>% 
    group_by(UniqueCarrier, Dest) %>%
    summarize(n = n()) %>%
    mutate(rank = rank(desc(n))) %>%
    filter(rank == 1)
  ```

  # dplyr deals with different types

  `hflights2` is a copy of `hflights` that is saved as a data table. `hflights2` was made available in the background using the following code:

  ```
  library(data.table)
  hflights2 <- as.data.table(hflights)
  ```

  `hflights2` contains all of the same information as `hflights`, but the information is stored in a different data structure. You can see this structure by typing `hflights2` at the command line. 

  Even though `hflights2` is a different data structure, you can use the same `dplyr` functions to manipulate `hflights2` as you used to manipulate `hflights`.

  ##### Instructions

  - Use [`summarize()`](http://www.rdocumentation.org/packages/dplyr/functions/summarise) to calculate `n_carrier`, the total number of unique carriers in `hflights2`. Whether or not you use the pipe is up to you!

  - ```R
    # hflights2 is pre-loaded as a data.table
    
    # Use summarize to calculate n_carrier
    hflights2 %>%
    summarize(n_carrier = n_distinct(UniqueCarrier))
    ```

  - # dplyr and mySQL databases

  - DataCamp  hosts a mySQL database with data about flights that departed from New  York City in 2013. The data is similar to the data in `hflights`, but it does not contain information about cancellations or diversions. With the `tbl()` function, we already created a reference to a table in this information. 

  - Although `nycflights` is a reference to data that lives outside of R, you can use the `dplyr` commands on them as usual. Behind the scenes, `dplyr`  will convert the commands to the database's native language (in this  case, SQL), and return the results. This allows you to pull data that is  too large to fit in R: only the fraction of the data that you need will  actually be downloaded into R, which will usually fit into R without  memory issues.

  - ##### Instructions

  - - Try to understand the code that creates `nycflights`, a reference to a MySQL table.
    - Use `glimpse()` to check out `nycflights`. Although `nycflights` is a reference to a tbl in a remote database, there is no difference in syntax. Look carefully: the variable names in `nycflights` differ from the ones in `hflights`!
    - Group `nycflights` data by `carrier`, then `summarize()` with two variables: `n_flights`, the number of flights flown by each carrier and `avg_delay`, the average arrival delay of flights flown by each carrier. Finally, arrange the carriers by average delay from low to high.

```R
# Set up a connection to the mysql database
my_db <- src_mysql(dbname = "dplyr", 
                   host = "courses.csrrinzqubik.us-east-1.rds.amazonaws.com", 
                   port = 3306, 
                   user = "student",
                   password = "datacamp")

# Reference a table within that source: nycflights
nycflights <- tbl(my_db, "dplyr")

# glimpse at nycflights
glimpse(nycflights)

# Ordered, grouped summary of nycflights
  nycflights %>%
  group_by(carrier) %>%
  summarize(n_flights = n(),avg_delay= mean(arr_delay)) %>%
  arrange(avg_delay)
  
```

