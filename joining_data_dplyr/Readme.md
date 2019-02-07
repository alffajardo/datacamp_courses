# A second join

You should always check the output of your joins. Just because a join worked, doesn't mean that it worked as you expected.

For example, the code in the editor joins the same two datasets that  you joined in the previous exercise, but it returns a different result.  Can you tell what went wrong?

##### Instructions

100 XP

The result from the previous exercise, `bands2`, is loaded in your workspace.

- Examine the output from the code provided in the editor. How is it different from `bands2`?

- Fix the code so that the result is identical to `bands2`.

  ```R
  left_join(bands, artists, by = c("first","last"))
  ```

  # A right join

  There  is more than one way to execute a left join. Knowing multiple methods  will make you a more versatile data scientist, especially as you try to  fit joins into pipes created with `%>%`.

  In this exercise, you'll recreate `bands2` once more, but this time without using a `left_join()`.

  ##### Instructions

  100 XP

  - Use `right_join()` to create `bands3`, a new dataset that contains the same information as `bands2`.
  - Use `setequal()` to check that the datasets are the same.

```R
# Finish the code below to recreate bands3 with a right join
bands2 <- left_join(bands, artists, by = c("first", "last"))
bands3 <- right_join(artists, bands, by = c("first", "last"))

# Check that bands3 is equal to bands2
setequal(bands2, bands3)
```

# Inner joins and full joins

You may have noticed that some of the songs in `songs` correspond to some of the albums in `albums`. Suppose you want a new dataset that contains all of the songs for which you have data from both `albums` and `songs`. How would you make it? 

The `artists` and `bands` datasets also share  some information. What if you want to join these two datasets in such a  way that you retain all of the information available in both tables,  without throwing anything away?

You can think of inner joins as the most strict type of join: they  only retain observations that appear in both datasets. In contrast, full  joins are the most permissive type of join: they return all of the data  that appears in both datasets (often resulting in many missing values).

Recall that, `*_join(x, y)` joins `y` **to** `x`. The second dataset you specify is joined to the first dataset.

##### Instructions

100 XP

- Join `albums` to `songs` in a way that returns only rows that contain information about both songs and albums.
- Join `bands` to `artists` to create a single table that contains *all* of the available data.

```R
# Join albums to songs using inner_join()
inner_join(songs,albums)

# Join bands to artists using full_join()
full_join(artists,bands)
```

# Pipes

You can combine `dplyr` functions together with the pipe operator, `%>%`, to build up an analysis step-by-step. `%>%`  takes the result of the code that comes before it and "pipes" it into  the function that comes after it as the first argument of the function.

So for example, the two pieces of code below do the same thing:

```
full_join(artists, bands, 
          by = c("first", "last"))

artists %>% 
  full_join(bands, by = c("first", "last"))
```

Pipes are so efficient for multi-step analysis that you will use them  for the remainder of the exercises in this course. (If you need a  refresher on the pipe operator, check out [Data Manipulation in R with dplyr](https://www.datacamp.com/courses/dplyr-data-manipulation-r-tutorial) course!)

##### Instructions

100 XP

The code in the editor finds all of the known guitarists in the `bands` dataset. Rewrite the code to use `%>%`s instead of multiple function calls. The pipe `%>%` should be used three times and `temp` zero times.

```R
# Find guitarists in bands dataset (don't change)
temp <- left_join(bands, artists, by = c("first", "last"))
temp <- filter(temp, instrument == "Guitar")
select(temp, first, last, band)

# Reproduce code above using pipes
bands %>% 
left_join(artists,by = c("first","last")) %>%
  filter(instrument== "Guitar")%>%
  select(first, last, band)
```

# Practice with pipes and joins

We've created a data frame for you called `goal`.  It's available in your workspace, so go ahead and take a look. Your  mission, if you choose to accept it, is to create a dataset that's  identical to `goal`.

##### Instructions

100 XP

- Examine the `goal` dataset by printing it to the console.

- Write a pipe that uses a full join and an inner join to combine `artists`, `bands`, and `songs` into `goal2`, a dataset identical to `goal`.

- Use `setequal()` to check that `goal` is identical to `goal2`

  # Choose your joins

  You're getting the hang of pipes now! They are a very useful way to combine multiple joins to make a single dataset. 

  Let's craft one more dataset before moving to Chapter 2. One of the  most useful ways to combine data is to place all of the values of all of  the datasets into a single table.

  ##### Instructions

  100 XP

  Write a pipe that combines `artists`, `bands`, `songs`, and `albums` (in that order) into a single table, such that it contains *all* of the information in the datasets.

```R
# Create one table that combines all information
artists %>% 
  full_join(bands, by = c("first", "last")) %>% 
  full_join(songs, by = c("first", "last")) %>% 
  full_join(albums, by = c("album", "band"))
```

# Apply a semi-join

As you saw in the video, semi-joins provide a concise way to filter data from the first dataset based on information in a second dataset.

For example, the code in the editor uses `semi_join()` to create a data frame of the artists in `artists` who have written a song in `songs`.

##### Instructions

100 XP

- Run the `semi_join()` command to see its output.

- Then fill in the blanks of the `right_join()`, `filter()`, and `select()` calls to create the same result (but with the rows in a different order).

  ```R
  # View the output of semi_join()
  artists %>% 
    semi_join(songs, by = c("first", "last"))
  
  # Create the same result
  artists %>% 
    right_join(songs, by = c("first", "last")) %>% 
    filter(!is.na(instrument)) %>% 
    select(first, last, instrument)
  ```

  # Exploring with semi-joins

  Semi-joins provide a useful way to explore the connections between multiple tables of data.

  For example, you can use a semi-join to determine the number of albums in the `albums` dataset that were made by a band in the `bands` dataset.

  ##### Instructions

  100 XP

  - For the first pipe, use `semi_join()` to collect the albums in `albums` that were made by a band in `bands`.
  - For the second pipe, use [`nrow()`](https://www.rdocumentation.org/packages/base/topics/nrow) to count how many albums were made by a band in the dataset.

  - ```R
    albums %>% 
      # Collect the albums made by a band
      semi_join(bands,by="band") %>% 
      # Count the albums made by a band
      nrow()
    ```

  - # Apply an anti-join

  - As Garrett mentioned in the video, anti-joins provide a useful way to reason about how a mutating join will work before you apply the join.

  - For example, you can use an anti-join to see which rows will not be matched to a second dataset by a join.

  - ##### Instructions

  - 100 XP

  - Use an `anti_join()` to return the rows of `artists` for which you don't have any `bands` info. *Note: Don't forget to mention the by argument.*  

```
artists %>% 
  anti_join(bands,by=c("first","last"))
```

# Apply another anti-join

Anti-joins with `anti_join()` also provide a great way to diagnose joins that go wrong.

For example, they can help you zero-in on rows that have capitalization or spelling errors in the keys. These things will make your primary and secondary keys appear different to R, even though you know they refer to the same thing.

##### Instructions

100 XP

`labels` describes the record labels of the albums in `albums`. Compare the spellings of album names in `labels` with the names in `albums`. Are any of the album names of `labels` mis-entered? Use `anti_join()` to check. *Note: Don't forget to mention the by argument.*

