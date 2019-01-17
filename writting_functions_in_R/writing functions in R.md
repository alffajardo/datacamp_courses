---
output:
  pdf_document: default
  html_document: default
---
Creating functions in R

## Data Camp course

# Writing a function

The function template is a useful way to start writing a function:

```
my_fun <- function(arg1, arg2) {
  # body
}
```

`my_fun` is the variable that you want to assign your function to, `arg1` and `arg2` are arguments to the function. The template has two arguments, but you can specify any number of arguments, each separated by a comma. You then replace `# body` with the R code that your function will execute, referring to the inputs by the argument names you specified.

Let's get to writing functions!

##### INSTRUCTIONS

100 XP

- Using the function template, write a function `ratio()` that takes arguments `x` and `y` and returns their ratio, `x / y`.
- Check your function by calling it with the arguments 3 and 4.

```
# Define ratio() function
ratio <- function(x, y) {
  x / y 
}

# Call ratio() with arguments 3 and 4
ratio(3,4)
```



- 

- Take Hint (-30 XP)

# Arguments

How did you call your function `ratio()` in the previous exercise? Do you remember the two ways to specify the arguments? (If you have forgotten it might be useful to review the video from [Intermediate R](http://campus.datacamp.com/courses/intermediate-r/chapter-3-functions?ex=1))

You probably either did `ratio(3, 4)`, which relies on matching by position, or `ratio(x = 3, y = 4)`, which relies on matching by name.

For functions you and others use often, it's okay to use positional matching for the first one or two arguments. These are usually the data to be computed on. Good examples are the `x` argument to the summary functions (`mean()`, `sd()`, etc.) and the `x` and `y`arguments to plotting functions.

However, beyond the first couple of arguments you should always use matching by name. It makes your code much easier for you and others to read. This is particularly important if the argument is optional, because it has a default. When overriding a default value, it's good practice to use the name.

Notice that when you call a function, you should place a space around `=` in function calls, and always put a space after a comma, not before (just like in regular English). Using whitespace makes it easier to skim the function for the important components.

##### INSTRUCTIONS

100 XP

Here's a rather cryptic call to `mean()`. Rewrite the call to follow the best practices we just discussed. Use the natural ordering of the arguments, which you can find by typing `?mean` in the console.

```R
# Rewrite the call to follow best practices
mean(0.1,x=c(1:9, NA),TRUE)

mean(c(1:9,NA),trim=0.1,na.rm = TRUE)
```



- 

- Take Hint (-30 XP)

# Testing your understanding of scoping (1)

The next few questions are designed to test your understanding of scoping. For first timers, these concepts will be hard and you might not get it the first time through. We decided to include it in the first chapter because it's good to know now, so when something unexpected happens, you know what to come back to and review.

For now, take a careful look at the function featured in each question. Try to predict what the function will return without running it! Being able to reason about a function is an important skill for R programmers.

Consider the following:

```
y <- 10
f <- function(x) {
  x + y
}
```

What will `f(10)` return?

##### INSTRUCTIONS

50 XP

##### Possible Answers

Click or Press Ctrl+1 to focus

- 

  An error

  press 1

- 

  10

  press 2

- 

  15

  press 3

- 

  20

  press 4

  # Subsetting lists

  There are a few ways to subset a list. Throughout the course we'll mostly use double bracket (`[[]]`) subsetting by index and by name.

  That is, `my_list[[1]]` extracts the first element of the list `my_list`, and `my_list[["name"]]` extracts the element in `my_list` that is called `name`. If the list is nested you can travel down the hierarchy by recursive subsetting. For example, `mylist[[1]][["name"]]` is the element called `name` inside the first element of `my_list`.

  A data frame is just a special kind of list, so you can use double bracket subsetting on data frames too.`my_df[[1]]` will extract the first column of a data frame and `my_df[["name"]]` will extract the column named `name` from the data frame.

  I've set up a list called `tricky_list` in your workspace. Use the function `typeof()` combined with double bracket subsetting to answer the following questions.

  ```R
  # 2nd element in tricky_list
  typeof(tricky_list[[2]])
  
  # Element called x in tricky_list
  typeof(tricky_list[["x"]])
  
  # 2nd element inside the element called x in tricky_list
  typeof(tricky_list[["x"]][[2]])
  ```


# Exploring lists

Often you won't know exactly what is inside a list. But, you'll need to figure it out to get some useful piece of data. Extracting elements from the output of the `names()` and `str()` functions is a great way to explore the structure of a list.

Calling `names()` on a list will give you names at the top level of the list and `str()` will give you a full description of the entire list (which can sometimes be a little overwhelming).

`tricky_list` has a regression model stored in it. Let's see if we can drill down and pull out the slope estimate corresponding to the `wt` variable.

- Use `names()` on `tricky_list` to guess where the regression model is stored.
- Use `names()` and `str()` on the `model` element of `tricky_list`.
- Extract the `coefficients` element of the `model`element of `tricky_list`.
- Extract the `wt` element of the `coefficients`element of the `model` element of `tricky_list`.

*Note: Use the double bracket notation to extract elements of the list.*

```R
# Guess where the regression model is stored
names(tricky_list)

# Use names() and str() on the model element
names(tricky_list[["model"]])
str(tricky_list[["model"]])

# Subset the coefficients element
tricky_list[["model"]][["coefficients"]]

# Subset the wt element
tricky_list[["model"]][["coefficients"]][["wt"]]
```

# A safer way to create the sequence

Let's take a look at the sequence component of our `for`loop:

```
i in 1:ncol(df)
```

Each time our `for` loop iterates, `i` takes the next value in `1:ncol(df)`. This is a pretty common model for a sequence: a sequence of consecutive integers designed to index over one dimension of our data.

What might surprise you is that this isn't the best way to generate such a sequence, especially when you are using `for` loops inside your own functions. Let's look at an example where `df` is an empty data frame:

```
df <- data.frame()
1:ncol(df)

for (i in 1:ncol(df)) {
  print(median(df[[i]]))
}
```

Our sequence is now the somewhat non-sensical: 1, 0. You might think you wouldn't be silly enough to use a `for` loop with an empty data frame, but once you start writing your own functions, there's no telling what the input will be.

A better method is to use the `seq_along()` function. This function generates a sequence along the index of the object passed to it, but handles the empty case much better.

##### INSTRUCTIONS

- Run the `for` loop code that is provided.
- Replace the `1:ncol(df)` sequence in our `for` loop with `seq_along(df)`.
- Create an empty data frame, `empty_df`.
- Repeat the `for` loop on `empty_df` to verify there is no error.

```R
for (i in seq_along(df)) {
  print(median(df[[i]]))
}

# Create an empty data frame
empty_df <- data.frame()

# Repeat for loop to verify there is no error
for (i in seq_along(empty_df)) {
  print(median(empty_df[[i]]))
}
```

# Keeping output

Our `for` loop does a good job displaying the column medians, but we might want to store these medians in a vector for future use.

Before you start the loop, you must always allocate sufficient space for the output, let's say an object called `output`. This is very important for efficiency: if you grow the `for` loop at each iteration (e.g. using `c()`), your `for` loop will be very slow.

A general way of creating an empty vector of given length is the `vector()` function. It has two arguments: the type of the vector (`"logical"`, `"integer"`, `"double"`, `"character"`, etc.) and the `length` of the vector.

Then, at each iteration of the loop you must store the output in the corresponding entry of the `output`vector, i.e. assign the result to `output[[i]]`. (You might ask why we are using double brackets here when `output` is a vector. It's primarily for generalizability: this subsetting will work whether `output` is a vector or a list.)

Let's edit our loop to store the medians, rather than printing them to the console.

```R
# Create new double vector: output
output <- vector("double",ncol(df))

# Alter the loop
for (i in seq_along(df)) {
  # Change code to store result in output
  output[[i ]] <- print(median(df[[i]]))
 
  
}

# Print output
output
```

# Start with a snippet of code

We have a snippet of code that successfully rescales a column to be between 0 and 1:

```
(df$a - min(df$a, na.rm = TRUE)) /  
  (max(df$a, na.rm = TRUE) - min(df$a, na.rm = TRUE))
```

Our goal over the next few exercises is to turn this snippet, written to work on the `a` column in the data frame `df`, into a general purpose `rescale01()`function that we can apply to any vector.

The first step of turning a snippet into a function is to examine the snippet and decide how many inputs there are, then rewrite the snippet to refer to these inputs using temporary names. These inputs will become the arguments to our function, so choosing good names for them is important. (We'll talk more about naming arguments in a later exercise.)

In this snippet, there is one input: the numeric vector to be rescaled (currently `df$a`). What would be a good name for this input? It's quite common in R to refer to a vector of data simply as `x` (like in the [`mean`](http://www.rdocumentation.org/packages/base/functions/mean) function), so we will follow that convention here.

##### INSTRUCTIONS

100 XP

- To help you test your code, create a vector `x`containing the numbers 1 through 10.

- Rewrite the code snippet to use the temporary variable `x` instead of referring to the data frame column `df$a`.

- ```R
  # Define example vector x
  x <- 1:10
  
  # Rewrite this snippet to refer to x
  (x - min(x, na.rm = TRUE)) /
    (max(x, na.rm = TRUE) - min(x, na.rm = TRUE))
  ```

# Rewrite for clarity

Our next step is to examine our snippet and see if we can write it more clearly.

Take a close look at our rewritten snippet. Do you see any duplication?

```
(x - min(x, na.rm = TRUE)) /
  (max(x, na.rm = TRUE) - min(x, na.rm = TRUE))
```

One obviously duplicated statement is `min(x, na.rm = TRUE)`. It makes more sense for us just to calculate it once, store the result, and then refer to it when needed. In fact, since we also need the maximum value of `x`, it would be even better to calculate the *range* once, then refer to the first and second elements when they are needed.

What should we call this intermediate variable? You'll soon get the message that using good names is an important part of writing clear code! I suggest we call it `rng` (for "range").

##### INSTRUCTIONS

100 XP

- Define the intermediate variable `rng` to contain the range of `x` using the function `range()`. Specify the `na.rm()` argument to automatically ignore any `NA`s in the vector.
- Rewrite the snippet to refer to this intermediate variable.

```R
# Define example vector x
x <- 1:10

# Define rng
rng <- range(x,na.rm=T)

# Rewrite this snippet to refer to the elements of rng
(x - rng[1]) /
  (rng[2] - rng[1])
```



- # Finally turn it into a function!

- What do you need to write a function? You need a **name**for the function, you need to know the **arguments** to the function, and you need code that forms the **body** of the function.

- We now have all these pieces ready to put together. It's time to write the function!

- ##### INSTRUCTIONS

- 100 XP

- - Use the function template to create a function called `rescale01()`:
  - The function should take a single argument `x`.
  - The body of the function should be our rewritten snippet from the previous exercise: `rng <- range(x, na.rm = TRUE) (x - rng[1]) / (rng[2] - rng[1])`
  - Once you've written the function, test it out by calling it on the `x` we've already defined.

- ```R
  # Define example vector x
  x <- 1:10 
  
  # Use the function template to create the rescale01 function
  rescale01 <- function(x) {
    # body
    rng <- range(x, na.rm = TRUE) 
    (x - rng[1]) / (rng[2] - rng[1])
  }
  
  # Test your function, call rescale01 using the vector x as the argument
  rescale01(x)
  ```

- # Start with a simple problem

- Let's tackle a new problem. We want to write a function, `both_na()` that counts at how many positions two vectors, `x` and `y`, both have a missing value.

- How do we get started? Should we start writing our function?

- ```
  both_na <- function(x, y) {
    # something goes here?
  }
  ```

- **No!** We should start by solving a simple example problem first. Let's define an `x` and `y` where we know what the answer `both_na(x, y)` should be.

- Let's start with:

- ```
  x <- c( 1, 2, NA, 3, NA)
  y <- c(NA, 3, NA, 3,  4)
  ```

- Then `both_na(x, y)` should return 1, since there is only one element that is missing in both `x` and `y`, the third element.

- (Notice we introduced a couple of extra spaces to each vector. Adding spaces to `x` and `y` to make them match up makes it much easier to see what the correct result is. Code formatting is an important aspect of writing clear code.)

- Your first task is to write a line of code that gets to that answer.

- ##### INSTRUCTIONS

- 100 XP

- Write a line of code that finds the number of positions where both `x` and `y` have missing values. You may find the `is.na()` and `sum()` functions useful, as well as the `&` operator.

- ```
  # Define example vectors x and y
  x <- c( 1, 2, NA, 3, NA)
  y <- c(NA, 3, NA, 3,  4)
  
  # Count how many elements are missing in both x and y
  sum (is.na(x) & is.na(y)) 
  ```

- Great! You now have a snippet of code that works:

- ```
  sum(is.na(x) & is.na(y))
  ```

- You've already figured out it should have two inputs (the two vectors to compare) and we've even given them reasonable names: `x` and `y`. Our snippet is also so simple we can't write it any clearer.

- So, let's go ahead and turn this snippet into a function!

- ##### INSTRUCTIONS

- 100 XP

- - This time, instead of using the function template, we've provided the body of the function. Wrap the body with function assignment and curly braces.
  - Assign the function to the name `both_na()`.
  - `both_na()` should take two arguments, `x` and `y`.

- ```
  # Define example vectors x and y
  x <- c( 1, 2, NA, 3, NA)
  y <- c(NA, 3, NA, 3,  4)
  
  # Turn this snippet into a function: both_na()
  both_na <- function (x,y){
    sum(is.na(x) & is.na(y))
  }
  ```

- 

- - 

  - # Put our function to use

  - We have a function that works in at least one situation, but we should probably check it works in others.

  - Consider the following vectors:

  - ```
    x <-  c(NA, NA, NA)
    y1 <- c( 1, NA, NA)
    y2 <- c( 1, NA, NA, NA)
    ```

  - What would you expect `both_na(x, y1)` to return? What about `both_na(x, y2)`? Does your function return what you expected? Try it and see!

  - ##### INSTRUCTIONS

  - 100 XP

  - - Create the vectors `x`, `y1` and `y2` according the above examples.

    - Call `both_na()` with `x` and `y1`.

    - Call `both_na()` with `x` and `y2`.

    - ```R
      # Define x, y1 and y2
      x <-  c(NA, NA, NA)
      y1 <- c( 1, NA, NA)
      y2 <- c( 1, NA, NA, NA)
      
      
      
      # Call both_na on x, y1
      both_na(x,y1)
      
      # Call both_na on x, y2
      both_na(x,y2)
      ```

# Argument names

It's not just your function that needs a good name. Your arguments need good names too!

Take a look at this function, which calculates a confidence interval for a population mean:

```
mean_ci <- function(c, nums) {
  se <- sd(nums) / sqrt(length(nums))
  alpha <- 1 - c
  mean(nums) + se * qnorm(c(alpha / 2, 1 - alpha / 2))
}
```

The argument `nums` is a sample of data and the argument `c` controls the level of the confidence interval. For example, if `c = 0.95`, we get a 95% confidence interval. Are `c` and `nums` good arguments names?

`c` is a particularly bad name. It is completely non-descriptive and it's the name of an existing function in R. What might be better? Maybe something like `confidence`, since it reveals the purpose of the argument: to control the level of **confidence** for the interval. Another option might be `level`, since it's the same name used for the `confint` function in base R and your users may already be familiar with that name for this parameter.

`nums` is not inherently bad, but since it's the placeholder for the vector of data, a name like `x` would be more recognizable to users.

##### INSTRUCTIONS

100 XP

Rewrite the `mean_ci()` function to take arguments named `level` and `x` instead of `c` and `nums`, in that order for now.

```
# Rewrite mean_ci to take arguments named level and x
mean_ci <- function(level, x) {
  se <- sd(x) / sqrt(length(x))
  alpha <- 1 - level
  mean(x) + se * qnorm(c(alpha / 2, level / 2))
```

# Argument order

Aside from giving your arguments good names, you should put some thought into what order your arguments are in and if they should have defaults or not.

Arguments are often one of two types:

- **Data arguments** supply the data to compute on.
- **Detail arguments** control the details of how the computation is done.

Generally, data arguments should come first. Detail arguments should go on the end, and usually should have default values.

Take another look at our function:

```
mean_ci <- function(level, x) {
  se <- sd(x) / sqrt(length(x))
  alpha <- 1 - level
  mean(x) + se * qnorm(c(alpha / 2, 1 - alpha / 2))
}
```

`x` is the data to be used for the calculation, so it's a data argument and should come first.

`level` is a detail argument; it just controls the level of confidence for which the interval is constructed. It should come after the data arguments and we should give it a default value, say 0.95, since it is common to want a 95% confidence interval.

##### INSTRUCTIONS



- Move the data argument, `x`, to the front.
- Move the detail argument, `level`, to the end and give it the default value 0.95.

```R
# Alter the arguments to mean_ci
mean_ci <- function(x, level = 0.95) {
  se <- sd(x) / sqrt(length(x))
  alpha <- 1 - level
  mean(x) + se * qnorm(c(alpha / 2, 1 - alpha / 2))
}
```



- # Return statements

- One of your colleagues has noticed if you pass `mean_ci()` an empty vector it returns a confidence interval with missing values at both ends (try it: `mean_ci(numeric(0))`). In this case, they decided it would make more sense to produce a warning `"x was empty"` and return `c(-Inf, Inf)` and have edited the function to be:

- ```
  mean_ci <- function(x, level = 0.95) {
    if (length(x) == 0) {
      warning("`x` was empty", call. = FALSE)
      interval <- c(-Inf, Inf)
    } else { 
      se <- sd(x) / sqrt(length(x))
      alpha <- 1 - level
      interval <- mean(x) + 
        se * qnorm(c(alpha / 2, 1 - alpha / 2))
    }
    interval
  }
  ```

- Notice how hard it is now to follow the logic of the function. If you want to know what happens in the empty `x` case, you need to read the entire function to check if anything happens to `interval` before the function returns. There isn't much to read in this case, but if this was a longer function you might be scrolling through pages of code.

- This is a case where an early `return()` makes sense. If `x` is empty, the function should immediately return `c(-Inf, Inf)`.

```
# Alter the mean_ci function
mean_ci <- function(x, level = 0.95) {
  
  if(length(x)==0){
    return(c(-Inf,Inf))
  }
  se <- sd(x) / sqrt(length(x))
  alpha <- 1 - level
  mean(x) + se * qnorm(c(alpha / 2, 1 - alpha / 2))
}
```

# What does this function do?

Over the next few exercises, we'll practice everything you've learned so far. Here's a poorly written function, which is also available in your workspace:

```
f <- function(x, y) {
  x[is.na(x)] <- y
  cat(sum(is.na(x)), y, "\n")
  x
}
```

Your job is to turn it in to a nicely written function.

What does this function do? Let's try to figure it out by passing in some arguments.

```R
# Define a numeric vector x with the values 1, 2, NA, 4 and 5
x <- c(1,2,NA,4,5)

# Call f() with the arguments x = x and y = 3
f(x=x,y=3)

# Call f() with the arguments x = x and y = 10
f(x=x, y = 10)
```

# Let's make it clear from its name

Did you figure out what `f()` does? `f()` takes a vector `x` and replaces any missing values in it with the value `y`.

Imagine you came across the line `df$z <- f(df$z, 0)` a little further on in the code. What does that line do? Now you know, it replaces any missing values in the column `df$z` with the value 0. But anyone else who comes across that line is going to have to go back and find the definition of `f` and see if they can reason it out.

Let's rename our function and arguments to make it obvious to everyone what we are trying to achieve

- Rename the function `f()` to `replace_missings()`.

- Change the name of the `y` argument to `replacement`.

- Now replace the missing values of `df$z` with 0's using your new function. Make sure you assign the result back to `df$z`.

- ```
  eplace_missings <- function(x, replacement) {
    # Change the name of the y argument to replacement
    x[is.na(x)] <- replacement
    cat(sum(is.na(x)), replacement, "\n")
    x
  }
  
  # Rewrite the call on df$z to match our new names
  df$z <- replace_missings(df$z, replacement = 0)
  ```

# Make the body more understandable

Great! Now when someone comes across

```
df$z <- replace_missings(df$z, replacement = 0)
```

in your code, it's pretty obvious what you are trying to achieve. The body of our `replace_missings()`function is still a little messy. There is certainly some unnecessary duplication.

##### INSTRUCTIONS

100 XP

- Define `is_miss`, a logical vector that identifies the missing values in `x`.
- To reduce unncessary duplication, alter the rest of function to refer to `is_miss` instead of `is.na(x)`.

```R
replace_missings <- function(x, replacement) {
  # Define is_miss
  
  
  # Rewrite rest of function to refer to is_miss
  is_miss <- is.na(x)
  x[is_miss] <- replacement
  cat(sum(is_miss), replacement, "\n")
  x
```

# Much better! But a few more tweaks...

Did you notice `replace_missings()` prints some output to the console? Try it:

```
replace_missings(df$z, replacement = 0)
```

That output isn't exactly self-explanatory. It would be much nicer to say "2 missing values replaced by the value 0".

It is also bad practice to use `cat()` for anything other than a `print()` method (a function designed just to display output). Having an important message just print to the screen makes it very hard for other people who might be programming with your function to capture the output and handle it appropriately.

The official R way to supply simple diagnostic information is the `message()` function. The unnamed arguments are pasted together with no separator (and no need for a newline at the end) and by default are printed to the screen.

Let's make our function nicer for users by using  `message()` and making the output self-contained.

# Using a for loop to remove duplication

Imagine we have a data frame called `df`:

```
df <- data.frame(
  a = rnorm(10),
  b = rnorm(10),
  c = rnorm(10),
  d = rnorm(10)
)
```

We want to compute the median of each column. You could do this with copy and paste (`df` is available in your workspace, so go ahead and try it in the console):

```
median(df[[1]])
median(df[[2]])
median(df[[3]])
median(df[[4]])
```

But that's a lot of repetition! Let's start by seeing how we could reduce the duplication by using a `for` loop.

```R
replace_missings <- function(x, replacement) {
  is_miss <- is.na(x)
  x[is_miss] <- replacement
  
  # Rewrite to use message()
  message(sum(is_miss), replacement, "\n")
  x
}

# Check your new function by running on df$z
replace_missings(df$z,0)
```



##### INSTRUCTIONS

100 XP

We've provided some code to get you started. Fill in the body of the `for` loop to calculate the median of each column and store the results in `output`.

```R
# Initialize output vector
output <- vector("double", ncol(df))  

# Fill in the body of the for loop
for (i in seq_along(df)) {            
output[[i]] <- median(df[[i]])
}

# View the result
output
```

# Turning the for loop into a function

Now, imagine you need to do this to another data frame `df2`. You copy and paste the `for` loop, and edit every reference to `df` to be `df2` instead.

```R
output <- vector("double", ncol(df2))  
for (i in seq_along(df2)) {            
  output[[i]] <- median(df2[[i]])      
}
output
```

And then you realize you have another data frame `df3`for which you also want the column medians. You copy and paste...and realize you've copied and pasted two times. Time to write a function!

```R
# Turn this code into col_median()
col_median <- function (df) {
output <- vector("double", ncol(df))  
for (i in seq_along(df)) {            
  output[[i]] <- median(df[[i]])  
}
output
}

```

# What about column means?

What if instead of medians of every column you actually want means?

Let's write a `col_mean()` function that returns the vector of column means.

```R
# Create col_mean() function to find column means
col_mean <- function(df) {
  output <- numeric(length(df))
  for (i in seq_along(df)) {
    output[[i]] <- mean(df[[i]])
  }
  output
}
```

# What about column standard deviations?

You now have functions for column medians and means, what about one for standard deviations?

```
col_median <- function(df) {
  output <- numeric(length(df))
  for (i in seq_along(df)) {
    output[[i]] <- median(df[[i]])
  }
  output
}

col_mean <- function(df) {
  output <- numeric(length(df))
  for (i in seq_along(df)) {
    output[[i]] <- mean(df[[i]])
  }
  output
}
```

##### INSTRUCTIONS

100 XP

- Copy and paste the `col_median` function into the editor.
- Edit `col_median` function to find the column standard deviations instead.
- Use the name `col_sd` for your new function.

```R
# Define col_sd() function
col_sd <- function(df) {
  output <- numeric(length(df))
  for (i in seq_along(df)) {
    output[[i]] <- sd(df[[i]])
  }
  output
}
```



- # Uh oh...time to write a function again

- We just copied and pasted the function `col_median`two times. That's a sure sign we need to write a function. How can we write a function that will take column summaries for *any* summary function we provide?

- Let's look at a simpler example first. Consider the functions `f1()`, `f2()` and `f3()` that take a vector `x` and return deviations from the mean value raised to the powers 1, 2, and 3 respectively:

- ```
  f1 <- function(x) abs(x - mean(x)) ^ 1
  f2 <- function(x) abs(x - mean(x)) ^ 2
  f3 <- function(x) abs(x - mean(x)) ^ 3
  ```

- How could you remove the duplication in this set of function definitions?

- Hopefully, you would suggest writing a single function with two arguments: `x` *and* `power`. That way, one function reproduces all the functionality of `f1()`, `f2()` and `f3()`, and more.

- ```
  # Add a second argument called power
  f <- function(x,power) {
      # Edit the body to return absolute deviations raised to power
      abs(x - mean(x))^power
  }
  ```

- 

# The map functions

All the map functions in `purrr` take a vector, `.x`, as the first argument, then return `.f` applied to each element of `.x`. The type of object that is returned is determined by function suffix (the part after `_`):

- `map()` returns a list or data frame
- `map_lgl()` returns a logical vector
- `map_int()` returns a integer vector
- `map_dbl()` returns a double vector
- `map_chr()` returns a character vector

Let's repeat our column summaries using a map function instead of our `col_summary()` function.

Which map function shall we use? In our case, every summary we calculated returned a single numeric value, so we'll use `map_dbl()`.

##### INSTRUCTIONS

100 XP

Use `map_dbl()` to find the...

- Column means of the data frame `df`.
- Column medians of the data frame `df`.
- Column standard deviations of the data frame `df`.



```
# Load the purrr package
library(purrr)

# Use map_dbl() to find column means
map_dbl(df,mean)

# Use map_dbl() to column medians
map_dbl(df,median)

# Use map_dbl() to find column standard deviations
map_dbl(df,sd)
```



- # The ... argument to the map functions

- The map functions use the `...` ("dot dot dot") argument to pass along additional arguments to `.f`each time it’s called. For example, we can pass the `trim`argument to the `mean()` function:

- ```
  map_dbl(df, mean, trim = 0.5)
  ```

- Multiple arguments can be passed along using commas to separate them. For example, we can also pass the `na.rm` argument to `mean()`:

- ```
  map_dbl(df, mean, trim = 0.5, na.rm = TRUE)
  ```

- You don't have to specify the arguments by name, but it is good practice!

- You may be wondering why the arguments to `map()`are `.x` and `.f` and not `x` and `f`? It's because `.x` and `.f` are very unlikely to be argument names you might pass through the `...`, thereby preventing confusion about whether an argument belongs to `map()` or to the function being mapped.

- Let's get a bit of practice with this. We'll apply our new knowledge to a subset of the `planes` data frame available in the `nycflights13` package. Use `map_dbl()` to find the average and 5th percentile of each column in `planes`.

- ```R
  # Find the mean of each column
  map_dbl(.x=planes,.f=mean)
  
  # Find the mean of each column, excluding missing values
  map_dbl(.x=planes,.f=mean,na.rm=TRUE)
  
  # Find the 5th percentile of each column, excluding missing values
  map_dbl(.x=planes,.f=quantile,probs=0.05,na.rm=TRUE)
  ```

- # Picking the right map function

- Choosing the right map function is important. You can always use `map()`, which will return a list. However, if you know what type of output you expect, you are better to use the corresponding function. That way, if you expect one thing and get another, you'll know immediately because the map function will return an error.

- For example, try running:

- ```
  map_lgl(df, mean)
  ```

- The map functions are what we call **type consistent**. This means you know exactly what type of output to expect regardless of the input. `map_lgl()` either returns either a logical vector or an error. `map_dbl()` returns either a double or an error.

- One way to check the output type is to run the corresponding function on the first element. For example, `mean(df[[1]])` returns a single numeric value, suggesting `map_dbl()`.

- Let's get some more practice with the map functions. We've created a new data frame, `df3`, in your workspace. Use a map function to find which columns are numeric, the type of each column, and a summary of each column.

- ##### INSTRUCTIONS

- 100 XP

- ##### INSTRUCTIONS

- 100 XP

- Remember to choose the appropriate map function based on the output you expect for each of the following:

- - Find which columns are numeric in `df3` by combining a map function with `is.numeric()`.
  - Find the type of each column in `df3` by combining a map function with `typeof()`.
  - Find a summary of each column in `df3` by combining a map function with `summary()`.

- ```
  # Find the columns that are numeric
  map_lgl(df,is.numeric)
  
  # Find the type of each column
  map_chr(df,typeof)
  
  # Find a summary of each column
  map(df,summary)
  ```


# Using a string

There are also some useful shortcuts that come in handy when you want to subset each element of the `.x`argument. If the `.f` argument to a map function is set equal to a string, let's say `"name"`, then `purrr`extracts the `"name"` element from every element of `.x`.

This is a really common situation you find yourself in when you work with nested lists. For example, if we have a list of where every element contains an `a` and `b`element:

```
list_of_results <- list(
  list(a = 1, b = "A"), 
  list(a = 2, b = "C"), 
  list(a = 3, b = "D")
)
```

We might want to pull out the `a` element from every entry. We could do it with the string shortcut like this:

```
map(list_of_results, "a")
```

Now take our list of regresssion models:

```
map(cyl, ~ lm(mpg ~ wt, data = .))
```

It might be nice to extract the slope coefficient from each model. You'll do this in a few steps: first fit the models, then get the coefficients from each model using the `coef()` function, then pull out the `wt` estimate using the string shortcut.

##### Instructions

100 XP

##### Instructions

100 XP

- Assign the result from the previous exercise to the variable `models`.
- Use `map` and the `coef()` function to extract the coefficients from each model, and save it in the variable `coefs`.
- Use `map` and the string shortcut to extract the slope `wt` element from coefficients vectors.

- ```R
  # Save the result from the previous exercise to the variable models
  models <- map(cyl, ~ lm(mpg ~ wt, data = .))
  
  # Use map and coef to get the coefficients for each model: coefs
  coefs <- map(models, coef)
  
  # Use string shortcut to extract the wt coefficient 
  map(coefs, "wt")
  ```

# Using a numeric vector

Another useful shortcut for subsetting is to pass a numeric vector as the `.f` argument. This works just like passing a string but subsets by index rather than name. For example, with your previous `list_of_results`:

```
list_of_results <- list(
  list(a = 1, b = "A"), 
  list(a = 2, b = "C"), 
  list(a = 3, b = "D")
)
```

Another way to pull out the `a` element from each list, is to pull out the first element:

```
map(list_of_results, 1)
```

Let's pull out the slopes from our models again, but this time using numeric subsetting. Also, since we are pulling out a single numeric value from each element, let's use `map_dbl()`.

##### Instructions

100 XP

- Extract the second element from each vector in `coefs` using the numeric shortcut and `map_dbl()`.

- ```R
  coefs <- map(models, coef)
  
  # use map_dbl with the numeric shortcut to pull out the second element
  map_dbl(coefs,2)R
  ```

- # Putting it together with pipes

- `purrr` also includes a pipe operator: `%>%`. The pipe operator is another shortcut that saves typing, but also increases readability. The explanation of the pipe operator is quite simple: `x %>% f(y)` is another way of writing `f(x, y)`. That is, the left hand side of the pipe, `x`, becomes the first argument to the function, `f()`, on the right hand side of the pipe.

- Take a look at our code to get our list of models:

- ```
  cyl <- split(mtcars, mtcars$cyl) 
  map(cyl, ~ lm(mpg ~ wt, data = .))
  ```

- We split the data frame `mtcars` and save it as the variable `cyl`. We then pass `cyl` as the first argument to `map` to fit the models. We could rewrite this using the pipe operator as:

- ```
  split(mtcars, mtcars$cyl) %>% 
    map(~ lm(mpg ~ wt, data = .))
  ```

- We read this as "split the data frame `mtcars` on `cyl`, *then* use `map()` on the result."

- One of the powerful things about the pipe is we can chain together many operations. Here is our complete code, written with pipes, instead assigning each step to a variable and using it in the next step:

- ```
  mtcars %>% 
    split(mtcars$cyl) %>%
    map(~ lm(mpg ~ wt, data = .)) %>%
    map(coef) %>% 
    map_dbl("wt")
  ```

- We've written some code in the editor to pull out the R2R2from each model. Rewrite the last two lines to use a pipe instead.

- ##### Instructions

- 100 XP

- Rewrite the last two lines to use a pipe instead.

- - 

  - Take Hint (-30 XP)

```R
# Define models (don't change)
models <- mtcars %>% 
  split(mtcars$cyl) %>%
  map(~ lm(mpg ~ wt, data = .))

# Rewrite to be a single command using pipes 
models %>% 
  map(summary) %>%
  map_dbl("r.squared")
```

# Creating a safe function

`safely()` is an adverb; it takes a verb and modifies it. That is, it takes a function as an argument and it returns a function as its output. The function that is returned is modified so it never throws an error (and never stops the rest of your computation!).

Instead, it always returns a list with two elements:

1. `result` is the original result. If there was an error, this will be `NULL`.
2. `error` is an error object. If the operation was successful this will be `NULL`.

Let's try to make the `readLines()` function safe.

##### Instructions

100 XP

- Pass the `readLines()` function, without parentheses, to `safely()`, and assign the output to `safe_readLines`.
- Use `safe_readLines()` on the string `"http://example.org"` to read the example homepage HTML file.
- Use `safe_readLines()` on `"http://asdfasdasdkfjlda"`, a nonsense web address that shouldn't be found.

- 

- Take Hint (-30 XP)

```R
# Create safe_readLines() by passing readLines() to safely()
safe_readLines <- safely(readLines)

# Call safe_readLines() on "http://example.org"
example_lines <- safe_readLines("http://example.org")
example_lines

# Call safe_readLines() on "http://asdfasdasdkfjlda"
nonsense_lines <- safe_readLines("http://asdfasdasdkfjlda")
nonsense_lines
```

# Using map safely

One feature of `safely()` is that it plays nicely with the `map()` functions. Consider this list containing the two URLs from the last exercise, plus one additional URL to make things more interesting:

```
urls <- list(
  example = "http://example.org",
  rproj = "http://www.r-project.org",
  asdf = "http://asdfasdasdkfjlda"
)
```

We are interested in quickly downloading the HTML files at each URL. You might try:

```
map(urls, readLines)
```

But it results in an error, `Error in file(con, "r") : cannot open the connection`, and no output for any of the URLs. Go on, try it!

We can solve this problem by using our `safe_readLines()` instead.

##### Instructions

100 XP

- Use `map()` on `urls` with the `safe_readLines()`function instead and assign the results to `html`.
- Call `str()` on `html` to examine the output.
- Extract the `result` from one of the two elements that was successful using double square bracket subsetting.
- Extract the `error` from the element that was unsuccessful, again using double square bracket subsetting.

- ```R
  # Define safe_readLines()
  safe_readLines <- safely(readLines)
  
  # Use the safe_readLines() function with map(): html
  html <- map(urls,safe_readLines)
  
  # Call str() on html
  str(html)
  
  # Extract the result from one of the successful elements
  # html[[1]]
  html[[1]]
  # Extract the error from the element that was unsuccessful
  html[[3]]r
  ```

- # Working with safe output

- We now have output that contains the HTML for each of the two URLs on which `readLines()` was successful and the error for the other. But the output isn't that easy to work with, since the results and errors are buried in the inner-most level of the list.

- `purrr` provides a function `transpose()` that reshapes a list so the inner-most level becomes the outer-most level. In otherwords, it turns a list-of-lists "inside-out". Consider the following list:

- ```
  nested_list <- list(
     x1 = list(a = 1, b = 2),
     x2 = list(a = 3, b = 4)
  )
  ```

- If I need to extract the `a` element in `x1`, I could do `nested_list[["x1"]][["a"]]`. However, if I transpose the list first, the order of subsetting reverses. That is, to extract the same element I could also do `transpose(nested_list)[["a"]][["x1"]]`.

- This is really handy for safe output, since we can grab all the results or all the errors really easily.

- ##### Instructions

- 100 XP

- - Examine the structure of `transpose(html)`.
  - Pull out all the results by subsetting `transpose(html)` and assign to the variable `res`.
  - Pull out all the errors by subsetting `transpose(html)` and assign to the variable `errs`.

-   

- ```R
  # Define safe_readLines() and html
  safe_readLines <- safely(readLines)
  html <- map(urls, safe_readLines)
  
  # Examine the structure of transpose(html)
  str(transpose(html))
  
  # Extract the results: res
  res <- transpose(html)[["result"]]
  
  # Extract the errors: errs
  errs <- transpose(html)[["error"]]
  ```

- # Working with errors and results

- What you do with the errors and results is up to you. But, commonly you'll want to collect all the results for the elements that were successful and examine the inputs for all those that weren't.

- ##### Instructions

- 100 XP

- - Combine `map_lgl()` with `is_null()` to create a `logical` vector, `is_ok`, that is `TRUE` when `errs` is `NULL`.
  - Extract the successful results by subsetting `res` with `is_ok`.
  - Find the unsuccessful URLs by subsetting `urls` with `!is_ok`.

- - ```R
    # Initialize some objects
    safe_readLines <- safely(readLines)
    html <- map(urls, safe_readLines)
    res <- transpose(html)[["result"]]
    errs <- transpose(html)[["error"]]
    
    # Create a logical vector is_ok
    is_ok <- map_lgl(errs, is_null)
    
    # Extract the successful results
    res[is_ok]
    
    # Find the URLs that were unsuccessful
    urls[!is_ok]
    ```

- # MAPPING WITH SEVERAL ARGUMENTS

- # Getting started

- We'll use random number generation as an example throughout the remaining exercises in this chapter. To get started, let's imagine simulating 5 random numbers from a Normal distribution. You can do this in R with the `rnorm()` function. For example, to generate 5 random numbers from a Normal distribution with mean zero, we can do:

- ```
  rnorm(n = 5)
  ```

- Now, imagine you want to do this three times, but each time with a different sample size. You already know how! Let's use the `map()` function to get it done.

- ##### Instructions

- 100 XP

- - Create a list `n` containing the values: 5, 10, and 20.
  - Use `map()` to iterate over `n`, each time applying the function `rnorm()`.

- - ```R
    # Create a list n containing the values: 5, 10, and 20
    n <- list(5,10,20)
    
    # Call map() on n with rnorm() to simulate three samples
    map(n,rnorm)
    ```

  - 

# Mapping over two arguments

Ok, but now imagine we don't just want to vary the sample size, we also want to vary the mean. The mean can be specified in `rnorm()` by the argument `mean`. Now there are two arguments to `rnorm()` we want to vary: `n` and `mean`.

The `map2()` function is designed exactly for this purpose; it allows iteration over two objects. The first two arguments to `map2()` are the objects to iterate over and the third argument `.f` is the function to apply.

Let's use `map2()` to simulate three samples with different sample sizes and different means.

##### Instructions

100 XP

##### Instructions

100 XP

- Create a list `mu` containing the values: 1, 5, and 10.
- Edit the `map()` call to use `map2()` with both `n`and `mu`.

- ```
  # Initialize n
  n <- list(5, 10, 20)
  
  # Create a list mu containing the values: 1, 5, and 10
  mu <- list(1,5,10)
  
  # Edit to call map2() on n and mu with rnorm() to simulate three samples
  map2(n,mu,rnorm)
  ```

- 
    Mapping over more than two arguments

- But wait, there's another argument to `rnorm()` we might want to vary: `sd`, the standard deviation of the Normal distribution. You might think there is a `map3()`function, but there isn't. Instead `purrr` provides a `pmap()` function that iterates over 2 or more arguments.

- First, let's take a look at `pmap()` for the situation we just solved: iterating over two arguments. Instead of providing each item to iterate over as arguments, `pmap()` takes a list of arguments as its input. For example, we could replicate our previous example, 

```R
# Initialize n and mu
n <- list(5, 10, 20)
mu <- list(1, 5, 10)

# Create a sd list with the values: 0.1, 1 and 0.1
sd <- list(0.1,1,0.1)

# Edit this call to pmap() to iterate over the sd list as well
pmap(list(n, mu,sd), rnorm)
```

​	Argument matching

Compare the following two calls to `pmap()` (run them in the console and compare their output too!):

```
pmap(list(n, mu, sd), rnorm)
pmap(list(mu, n, sd), rnorm)
```

What's the difference? By default `pmap()` matches the elements of the list to the arguments in the function by position. In the first case, `n` to the `n` argument of `rnorm()`, `mu` to the `mean` argument of `rnorm()`, and `sd` to the `sd` argument of `rnorm()`. In the second case `mu` gets matched to the `n` argument of `rnorm()`, which is clearly not what we intended!

Instead of relying on this positional matching, a safer alternative is to provide names in our list. The name of each element should be the argument name we want to match it to.

Let's fix up that second call.

##### Instructions

100 XP

##### Instructions

100 XP

Without changing their ordering, simply name the elements of the argument list to properly match the arguments of `rnorm()`.

```R
# Name the elements of the argument list
  pmap(list(mean=mu,n= n,sd= sd), rnorm)
```

# Mapping over functions and their arguments

Sometimes it's not the arguments to a function you want to iterate over, but a set of functions themselves. Imagine that instead of varying the parameters to `rnorm()` we want to simulate from different distributions, say, using `rnorm()`, `runif()`, and `rexp()`. How do we iterate over calling these functions?

In `purrr`, this is handled by the `invoke_map()`function. The first argument is a list of functions. In our example, something like:

```
funs <- list("rnorm", "runif", "rexp")
```

The second argument specifies the arguments to the functions. In the simplest case, all the functions take the same argument, and we can specify it directly, relying on `...` to pass it to each function. In this case, call each function with the argument `n = 5`:

```
invoke_map(funs, n = 5)
```

In more complicated cases, the functions may take different arguments, or we may want to pass different values to each function. In this case, we need to supply `invoke_map()` with a list, where each element specifies the arguments to the corresponding function.

Let's use this approach to simulate three samples from the following three distributions: Normal(10, 1), Uniform(0, 5), and Exponential(5).

```R
# Define list of functions
funs <- list("rnorm", "runif", "rexp")

# Parameter list for rnorm()
rnorm_params <- list(mean = 10)

# Add a min element with value 0 and max element with value 5
runif_params <- list(min=0,max=5)

# Add a rate element with value 5
rexp_params <- list(rate=5)

# Define params for each function
params <- list(
  rnorm_params,
  runif_params,
  rexp_params
)

# Call invoke_map() on funs supplying params and setting n to 5
invoke_map(funs,params, n=5)
```

# Walk

`walk()` operates just like `map()` except it's designed for functions that don't return anything. You use `walk()` for functions with side effects like printing, plotting or saving.

Let's check that our simulated samples are in fact what we think they are by plotting a histogram for each one.

```R
# Define list of functions
funs <- list(Normal = "rnorm", Uniform = "runif", Exp = "rexp")

# Define params
params <- list(
  Normal = list(mean = 10),
  Uniform = list(min = 0, max = 5),
  Exp = list(rate = 5)
)

# Assign the simulated samples to sims
sims <- invoke_map(funs, params, n = 50)

# Use walk() to make a histogram of each element in sims
walk(sims,hist)
```

# Walking over two or more arguments

Those histograms were pretty good, but they really needed better breaks for the bins on the x-axis. That means we need to vary two arguments to `hist()`: `x`and `breaks`. Remember `map2()`? That allowed us to iterate over two arguments. Guess what? There is a `walk2()`, too!

Let's use `walk2()` to improve those histograms with better breaks.

##### Instructions

100 XP

We've loaded `sims` in your workspace.

- The default value for the `breaks` argument to `hist()` is `"Sturges"`. Replace `"Sturges"` in the `breaks_list` list with reasonable breaks for the histograms. Let's use `seq(6, 16, 0.5)` for the Normal, `seq(0, 5, 0.25)` for the Uniform and `seq(0, 1.5, 0.1)` for the Exponential.

- Use `walk2()` to create a histogram for each sample with the breaks in `breaks_list`.

  ```R
  # Replace "Sturges" with reasonable breaks for each sample
  breaks_list <- list(
    Normal = seq(6, 16, 0.5),
    Uniform = seq(0, 5, 0.25),
    Exp = seq(0, 1.5, 0.1))
  
  # Use walk2() to make histograms with the right breaks
  walk2(sims,breaks_list,hist)
  ```

  # Putting together writing functions and walk

  In the previous exercise, we hard-coded the breaks, but that was a little lazy. Those breaks probably won't be great if we change the parameters of our simulation.

  A better idea would be to generate reasonable breaks based on the actual values in our simulated samples. This is a great chance to review our function writing skills and combine our own function with `purrr`.

  Let's start by writing our own function `find_breaks()`, which copies the default breaks in the `ggplot2`package: break the range of the data in 30 bins.

  How do we start? Simple, of course! Here's a snippet of code that works for the first sample:

  ```
  rng <- range(sims[[1]], na.rm = TRUE)
  seq(rng[1], rng[2], length.out = 30)
  ```

  Your job in this exercise is to turn that snippet into a function.

  In the next exercise, we'll combine `find_breaks()`with `map()` and `walk2()` to create histograms with sensible breaks.

  ##### Instructions

  100 XP

  - Turn the snippet above into a function called `find_breaks()`, which takes a single argument `x`and return the sequence of breaks.

  - Check that your function works by calling `find_breaks()` on `sims[[1]]`.

    ```R
    # Turn this snippet into find_breaks()
    
      find_breaks <- function(x){
        
        rng <- range(x, na.rm = TRUE)
    seq(rng[1], rng[2], length.out = 30)
      }
    
    # Call find_breaks() on sims[[1]]
    find_breaks(sims[[1]])
    ```


# Nice breaks for all

Now that we have `find_breaks()`, we can find nice breaks for all the samples using `map()`. Then, pass the result into `walk2()` to get nice (but custom breaks) for our samples.

##### Instructions

100 XP

- Use `map()` to iterate `find_breaks()` over `sims`and assign the result to `nice_breaks`.
- Use `nice_breaks` as the second argument to `walk2()` to iterate over both the simulations and calculated breaks to plot histograms.

- ```R
  # Use map() to iterate find_breaks() over sims: nice_breaks
  nice_breaks <- map(sims,find_breaks)
  
  # Use nice_breaks as the second argument to walk2()
  walk2(sims,nice_breaks,hist)
  ```

- # Walking with many arguments: pwalk

- Ugh! Nice breaks but those plots had UUUUGLY labels and titles. The x-axis labels are easy to fix if we don't mind every plot having its x-axis labeled the same way. We can use the `...` argument to any of the `map()` or `walk()` functions to pass in further arguments to the function `.f`. In this case, we might decide we don't want any labels on the x-axis, in which case we need to pass an empty string to the `xlab` argument of `hist()`:

- ```
  walk2(sims, nice_breaks, hist, xlab = "")
  ```

- But, what about the titles? We don't want them to be the same for each plot. How can we iterate over the arguments `x`, `breaks` and `main`? You guessed it, there is a `pwalk()` function that works just like `pmap()`.

- Let's use `pwalk()` to tidy up these plots. Also, let's increase our sample size to 1000.

- ##### Instructions

- 100 XP

- - Increase the sample size to 1000.
  - Create a vector `nice_titles` that contains the character strings: `"Normal(10, 1)"`, `"Uniform(0, 5)"` and `"Exp(5)"`.
  - Use `pwalk()` instead of `walk2()` to iterate over the `x`, `breaks` and `main` arguments to `hist()`. Like for `pmap()`, the first argument to `pwalk()`should be a `list()` of arguments to `hist()` using matching by name. Keep the `xlab = ""` argument as-is to keep things clean.

- - ```R
    # Increase sample size to 1000
    sims <- invoke_map(funs, params, n = 1000)
    
    # Compute nice_breaks (don't change this)
    nice_breaks <- map(sims, find_breaks)
    
    # Create a vector nice_titles
    nice_titles <- c("Normal(10, 1)", "Uniform(0, 5)", "Exp(5)")
    
    # Use pwalk() instead of walk2()
    pwalk(list(x = sims, breaks = nice_breaks, main = nice_titles), hist, xlab = "")
    ```

  - # Walking with pipes

  - One of the nice things about the `walk()` functions is that they return the object you passed to them. This means they can easily be used in pipelines (a pipeline is just a short way of saying "a statement with lots of pipes").

  - To illustrate, we'll return to our first example of making histograms for each sample:

  - ```
    walk(sims, hist)
    ```

  - Take a look at what gets returned:

  - ```
    tmp <- walk(sims, hist)
    str(tmp)
    ```

  - It's our original `sims` object. That means we can pipe the `sims` object along to other functions. For example, we might want some basic summary statistics on each sample as well as our histograms.

  - ##### Instructions

  - 100 XP

  - We've converted `walk(sims, hist)` to a piped statement: `sims %>% walk(hist)`. Pipe the result into `map` using `summary()` as the `.f` argument.

  - - ```
      # Pipe this along to map(), using summary() as .f
      sims %>%
        walk(hist) %>%
      map(.,summary)
      ```

    - 

# An error is better than a surprise

Recall our `both_na()` function from Chapter 2, that finds the number of entries where vectors `x` and `y`both have missing values:

```
both_na <- function(x, y) {
  sum(is.na(x) & is.na(y))
}
```

We had an example where the behavior was a little surprising:

```
x <- c(NA, NA, NA)
y <- c( 1, NA, NA, NA)
both_na(x, y)
```

The function works and returns `3`, but we certainly didn't design this function with the idea that people could pass in different length arguments.

Using `stopifnot()` is a quick way to have your function stop, if a condition isn't met. `stopifnot()`takes logical expressions as arguments and if any are `FALSE` an error will occur.

##### Instructions

100 XP

- Add a call to `stopifnot()` to `both_na()` that checks arguments `x` and `y` have the same length.
- Run the call to `both_na()` to verify it returns an error.

- ```R
  # Define troublesome x and y
  x <- c(NA, NA, NA)
  y <- c( 1, NA, NA, NA)
  
  both_na <- function(x, y) {
    # Add stopifnot() to check length of x and y
    stopifnot(length(x)==length(y))
    
    sum(is.na(x) & is.na(y))
  }
  
  # Call both_na() on x and y
  both_na(x, y)
  ```

- 

# An informative error is even better

Using `stop()` instead of `stopifnot()` allows you to specify a more informative error message. Recall the general pattern for using `stop()` is:

```
if (condition) {
  stop("Error", call. = FALSE)
}
```

Writing good error messages is an important part of writing a good function! We recommend your error tells the user what should be true, not what is false. For example, here a good error would be `"x and y must have the same length"`, rather than the bad error `"x and y don't have the same length"`.

Let's use this pattern to write a better check for the length of `x` and `y`.

##### Instructions

100 XP

- Replace `condition` with a logical statement that evaluates to `TRUE` when `x` and `y` have different lengths.
- Change the error message to `"x and y must have the same length"`.
- Run the call to `both_na()` to verify it returns a more informative error.

```R
# Define troublesome x and y
x <- c(NA, NA, NA)
y <- c( 1, NA, NA, NA)

both_na <- function(x, y) {
  # Replace condition with logical
  if (length(x)!=length(y)) {
    # Replace "Error" with better message
    stop("x and y must have the same length", call. = FALSE)
  }  
  
  sum(is.na(x) & is.na(y))
}

# Call both_na() 
both_na(x, y)
```

# Using purrr solves the problem

This unpredictable behaviour is a sign that you shouldn't rely on `sapply()` inside your own functions.

So, what do you do? Use alternate functions that are type consistent! And you already know a whole set: the `map()` functions in `purrr`.

In this example, when we call `class()` on the columns of the data frame we are expecting character output, so our function of choice should be: `map_chr()`:

```
df <- data.frame(
  a = 1L,
  b = 1.5,
  y = Sys.time(),
  z = ordered(1)
)

A <- map_chr(df[1:4], class) 
B <- map_chr(df[3:4], class)
```

Except that gives us errors. This is a good thing! It alerts us that our assumption (that `class()` would return purely character output) is wrong.

Let's look at a couple of solutions. First, we could use `map()` instead of `map_chr()`. Our result will always be a list, no matter the input.

##### Instructions

100 XP

The first two chunks give some `sapply()` calls, and demonstrate the type inconsistency by calling `str()` on each result.

- Define `X`, `Y` and `Z` using `map()` instead of `sapply()`.
- Call `str()` on your `X`, `Y` and `Z` to demonstrate type consistency of `map()`.



```R
# sapply calls
A <- sapply(df[1:4], class) 
B <- sapply(df[3:4], class)
C <- sapply(df[1:2], class) 

# Demonstrate type inconsistency
str(A)
```

# A type consistent solution

If we wrap our solution into a function, we can be confident that this function will always return a list because we've used a type consistent function, `map()`:

```
col_classes <- function(df) {
  map(df, class)
}
```

But what if you wanted this function to always return a character string?

One option would be to decide what should happen if `class()` returns something longer than length 1. For example, we might simply take the first element of the vector returned by `class()`.

##### Instructions

100 XP

- Assign the body of our previous function to the variable `class_list`.
- Use `map_chr()` along with the numeric subsetting shortcut, to extract the first element from every item in `class_list`.
- Run the final three lines to verify our new function always returns a character vector.

```R
col_classes <- function(df) {
  # Assign list output to class_list
  class_list <- map(df, class)
  
  # Use map_chr() to extract first element in class_list
  map_chr(class_list,1)
}

# Check that our new function is type consistent
df %>% col_classes() %>% str()
df[3:4] %>% col_classes() %>% str()
df[1:2] %>% col_classes() %>% str()
```

# Or fail early if something goes wrong

Another option would be to simply fail. We could rely on `map_chr()`'s type consistency to fail for us:

```
col_classes <- function(df) {
  map_chr(df, class)
}

df %>% col_classes() %>% str()
```

Or, check the condition ourselves and return an informative error message. We'll implement this approach in this exercise.

As you write more functions, you'll find you often come across this tension between implementing a function that does something sensible when something surprising happens, or simply fails when something surprising happens. Our recommendation is to fail when you are writing functions that you'll use behind the scenes for programming and to do something sensible when writing functions for users to use interactively.

(And by the way, `flatten_chr()` is yet another useful function in `purrr`. It takes a list and removes its hierarchy. The suffix `_chr` indicates that this is another type consistent function, and will either return a character string or an error message.)

##### Instructions

100 XP

- Replace `condition` with a logical statement that uses `any()` and `map_dbl()` to check if any element in `class_list` has length greater than 1.
- Run the final three lines to verify an informative error is thrown.

- ```R
  col_classes <- function(df) {
    class_list <- map(df, class)
    
    # Add a check that no element of class_list has length > 1
    if (any(map_dbl(class_list, length) > 1)) {
      stop("Some columns have more than one class", call. = FALSE)
    }
    
    # Use flatten_chr() to return a character vector
    flatten_chr(class_list)
  }
  
  # Check that our new function is type consistent
  df %>% col_classes() %>% str()
  df[3:4] %>% col_classes() %>% str()
  df[1:2] %>% col_classes() %>% str()
  ```

- ```R
  # Use big_x() to find rows in diamonds_sub where x > 7
  big_x(diamonds_sub,7)
  ```

- 

# When things go wrong

Now, let's see how this function might fail. There are two instances in which the non-standard evaluation of `filter()` could cause surprising results:

1. The `x` column doesn't exist in `df`.
2. There is a `threshold` column in `df`.

Let's illustrate these failures. In each case we'll use `big_x()` in the same way as the previous exercise, so we should expect the same output. However, not only do we get unexpected outputs, there is no indication (i.e. error message) that lets us know something might have gone wrong.

##### Instructions 1/2

50 XP

- 

  - Ideally, `big_x()` should fail if there is no `x`column in `df`. Test what happens if the `x` column is deleted, but there is another variable named `x`.

    - Create a variable `x` and give it the value `1`.
    - Use `big_x()` to find all rows in `diamonds_sub`where the `x` column is greater than `7`.

  - 

    [2](javascript:void(0))

    The `x` column of `df` has been restored. Ideally, `big_x()` should always use its `threshold`argument. Test what happens if there is a `threshold` column in `df`.

    - Create a `threshold` column in `diamonds_sub`with the value `100`.
    - Use `big_x()` to find all rows in `diamonds_sub`where the `x` column is greater than `7`.

# What to do?

To avoid the problems caused by non-standard evaluation functions, you could avoid using them. In our example, we could achieve the same results by using standard subsetting (i.e. `[]`) instead of `filter()`. For more insight into dealing with NSE and how to write your own non-standard evaluation functions, we recommend reading Hadley's [vignette](http://rpubs.com/hadley/157957) on the topic. Also, programming with the NSE functions in `dplyr` will be easier in a future version.

If you do need to use non-standard evaluation functions, it's up to you to provide protection against the problem cases. That means you need to know what the problem cases are, to check for them, and to fail explicitly.

To see what that might look like, let's rewrite `big_x()`to fail for our problem cases.

##### Instructions

100 XP

##### Instructions

100 XP

Write a check for each of the following:

- If `x` is not in `colnames(df)`, stop with the message `"df must contain variable called x"`.
- If `threshold` is in `colnames(df)`, stop with the message `"df must not contain variable called threshold"`.

Remember to use the argument `call. = FALSE` in each call to `stop()` so that the call is not a part of the error message.

```R
big_x <- function(df, threshold) {
  # Write a check for x not being in df
  
  
  
  
  # Write a check for threshold being in df
  if(any(names(df)=="threshold")){
    stop("df must not contain variable called threshold",call.=FALSE)
    
  }
  
  
  
  dplyr::filter(df, x > threshold)
}
```

# A hidden dependence

A classic example of a hidden dependence is the `stringsAsFactors` argument to the `read.csv()`function (and a few other data frame functions.)

When you see the following code, you don't know exactly what the result will be:

```
pools <- read.csv("swimming_pools.csv")
```

That's because if the argument `stringsAsFactors`isn't specified, it inherits its value from `getOption("stringsAsFactors")`, a global option that a user may change.

Just to prove that this is the case, let's illustrate the problem.

```R
# This is the default behavior
options(stringsAsFactors = TRUE)

# Read in the swimming_pools.csv to pools
pools <- read.csv("swimming_pools.csv")

# Examine the structure of pools
str(pools)

# Change the global stringsAsFactors option to FALSE
options(stringsAsFactors = FALSE)

# Read in the swimming_pools.csv to pools2
pools2 <- read.csv("swimming_pools.csv")

# Examine the structure of pools2
str(pools2)
```

# Legitimate use of options

In general, you want to avoid having the return value of your own functions depend on any global options. That way, you and others can reason about your functions without needing to know the current state of the options.

It is, however, okay to have side effects of a function depend on global options. For example, the `print()`function uses `getOption("digits")` as the default for the `digits` argument. This gives users some control over how results are displayed, but doesn't change the underlying computation.

Let's take a look at an example function that uses a global default sensibly. The `print.lm()` function has the options `digits` with default `max(3, getOption("digits") - 3)`.

##### Instructions

100 XP

##### Instructions

100 XP

We've fit a regression model of fuel efficiency on weight using the `mtcars` dataset.

- Use `summary()` to take a look at the fitted regression model. Pay particular attention to number of decimal places reported.
- Set the global `digits` option to 2: `options(digits = 2)`.
- Take another look at the fitted model using `summary()`. Notice the number of decimal places has changed, but there is no change to the underlying `fit`object.

- ```R
  # Start with this
  options(digits = 8)
  
  # Fit a regression model
  fit <- lm(mpg ~ wt, data = mtcars)
  
  # Look at the summary of the model
  summary(fit)
  
  # Set the global digits option to 2
  options(digits = 8)
  
  # Take another look at the summary
  summary(fit)
  ```

- 
    

