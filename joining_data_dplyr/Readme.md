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

