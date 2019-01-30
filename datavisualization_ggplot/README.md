# Exploring ggplot2, part 1

To get a first feel for `ggplot2`, let's try to run some basic `ggplot2` commands. Together, they build a plot of the `mtcars`  dataset that contains information about 32 cars from a 1973 Motor Trend  magazine. This dataset is small, intuitive, and contains a variety of  continuous and categorical variables.

##### Instructions

100 XP

- Load the `ggplot2` package using [`library()`](http://www.rdocumentation.org/packages/base/functions/library). It is already installed on DataCamp's servers.
- Use [`str()`](http://www.rdocumentation.org/packages/utils/functions/str) to explore the structure of the `mtcars` dataset.
- Hit *Submit Answer*. This will execute the example code on the right. See if you can understand what `ggplot` does with the data.

- 

```R
# Load the ggplot2 package
library(ggplot2)

# Explore the mtcars data frame with str()
str(mtcars)

# Execute the following command
ggplot(mtcars, aes(x = cyl, y = mpg)) +
  geom_point()
```

# Exploring ggplot2, part 2

The plot from the previous exercise wasn't really satisfying. Although `cyl` (the number of cylinders) is categorical, it is classified as numeric in `mtcars`. You'll have to explicitly tell `ggplot2` that `cyl` is a categorical variable.

##### Instructions

100 XP

- Change the [`ggplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggplot) command by wrapping [`factor()`](http://www.rdocumentation.org/packages/base/functions/factor) around `cyl`.
- Hit *Submit Answer* and see if the resulting plot is better this time.

```R
# Load the ggplot2 package
library(ggplot2)

# Change the command below so that cyl is treated as factor
ggplot(mtcars, aes(x = factor(cyl), y = mpg)) +
  geom_point()
```

# Exploring ggplot2, part 3

We'll  use several datasets throughout the courses to showcase the concepts  discussed in the videos. In the previous exercises, you already got to  know `mtcars`. Let's dive a little deeper to explore the three main topics in this course: The data, aesthetics, and geom layers.

The `mtcars` dataset contains information about 32 cars  from 1973 Motor Trend magazine. This dataset is small, intuitive, and  contains a variety of continuous and categorical variables.

You're encouraged to think about how the examples and concepts we  discuss throughout these data viz courses apply to your own data-sets!

##### Instructions

100 XP

- `ggplot2` has already been loaded for you. Take a look at  the first command. It plots the mpg (miles per gallon) against the  weight (in thousands of pounds). You don't have to change anything about  this command.

- In the second call of [`ggplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggplot) **change** the `color` argument in [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) (which stands for *aesthetics*). The color should be dependent on the displacement of the car engine, found in `disp`.Choosing geoms, part 2 - dotplot

  Some naming conventions:

      Scatter plots:
      Continuous x, continuous y.
      Dot plots:
      Categorical x, continuous y.

  You use geom_point() for both plot types. Jittering position is set in the geom_point() layer.

  However, to make a "true" dot plot, you can use geom_dotplot(). The difference is that unlike geom_point(), geom_dotplot() uses a binning statistic. Binning means to cut up a continuous variable (the y in this case) into discrete "bins". You already saw binning with geom_histogram() (see this exercise for a refresher).

  One thing to notice is that geom_dotplot() uses a different plotting symbol to geom_point(). For these symbols, the color aesthetic changes the color of its border, and the fill aesthetic changes the color of its interior.

  Let's take a look at how the two geoms compare.
  Instructions
  100 XP

  A "basic" dot plot is shown in the viewer (see the code in the editor). Here, cyl (categorical) is mapped onto the x and wt (continuous) is mapped onto the y aesthetic. For this exercise we've already converted am to a factor variable for you.

      1 - Re-draw that plot in the viewer as a "true" dot plot.
          Add a dotplot geom by calling geom_dotplot().
          Set the arguments stackdir = "center" and binaxis = "y". These are our standard settings, but take a look at the help pages and try different settings to get familiar with these arguments.
      2 - Convert the previous ggplot() command to a qplot() command.

- In the third call of [`ggplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggplot) **change** the `size` argument in [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) (which stands for *aesthetics*). The size should be dependent on the displacement of the car engine, found in `disp`.

```R
# A scatter plot has been made for you
ggplot(mtcars, aes(x = wt, y = mpg)) +
  geom_point()

# Replace ___ with the correct column
ggplot(mtcars, aes(x = wt, y = mpg, color = disp)) +
  geom_point()

# Replace ___ with the correct column
ggplot(mtcars, aes(x = wt, y = mpg, size = disp)) +
  geom_point()
```

# Exploring ggplot2, part 4

The `diamonds` data frame contains information on the prices and various metrics of 50,000 diamonds. Among the variables included are `carat` (a measurement of the size of the diamond) and `price`. For the next exercises, you'll be using a subset of 1,000 diamonds.

Here you'll use two common geom layer functions: [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) and [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth). We already saw in the earlier exercises how these are added using the `+` operator.

##### Instructions

100 XP

- Explore the `diamonds` data frame with the [`str()`](http://www.rdocumentation.org/packages/utils/functions/str) function.

- Use the `+` operator to add [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) to the first [`ggplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggplot) command. This will tell `ggplot2` to draw points on the plot.

- Use the `+` operator to add [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) and [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth). These just stack on each other! [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth) will draw a smoothed line over the points. 

  ```R
  # Explore the diamonds data frame with str()
  str(diamonds)
  
  # Add geom_point() with +
  ggplot(diamonds, aes(x = carat, y = price))+
  geom_point()
  
  # Add geom_point() and geom_smooth() with +
  ggplot(diamonds, aes(x = carat, y = price))+
  geom_point()+
  geom_smooth()
  ```

  Exploring ggplot2, part 5

  The code for the last plot of the previous exercise is available in the script on the right. It builds a scatter plot of the diamonds dataset, with carat on the x-axis and price on the y-axis. geom_smooth() is used to add a smooth line.

  With this plot as a starting point, let's explore some more possibilities of combining geoms.
  Instructions
  100 XP

      Plot 2 - Copy and paste plot 1, but show only the smooth line, no points.
      Plot 3 - Show only the smooth line, but color according to clarity by placing the argument color = clarity in the aes() function of your ggplot() call.
      Plot 4 - Draw translucent colored points.
          Copy the ggplot() command from plot 3 (with clarity mapped to color).
          Remove the smooth layer.
          Add the points layer back in.
          Set alpha = 0.4 inside geom_point(). This will make the points 60% transparent/40% visible.

```R
# 1 - The plot you created in the previous exercise
ggplot(diamonds, aes(x = carat, y = price)) +
  geom_point() +
  geom_smooth()

# 2 - Copy the above command but show only the smooth line
ggplot(diamonds, aes(x = carat, y = price)) +
  geom_smooth()


# 3 - Copy the above command and assign the correct value to col in aes()
ggplot(diamonds, aes(x = carat, y = price,color=clarity)) +
  geom_smooth()


# 4 - Keep the color settings from previous command. Plot only the points with argument alpha.
ggplot(diamonds, aes(x = carat, y = price,color=clarity)) +
geom_point(alpha=0.4)
```

# Understanding the grammar, part 1

Here  you'll explore some of the different grammatical elements. Throughout  this course, you'll discover how they can be combined in all sorts of  ways to develop unique plots.

In the following instructions, you'll start by creating a `ggplot` object from the `diamonds` dataset. Next, you'll add layers onto this object to build beautiful & informative plots.

##### Instructions

100 XP

- Define the data (`diamonds`) and aesthetics layers. Map `carat` on the x axis and `price` on the y axis. Assign it to an object: `dia_plot`.
- Using `+`, add a [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) layer (with no arguments), to the `dia_plot` object. This can be in a single or multiple lines.
- Note that you can also call [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) *within* the [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) function. Map `clarity` to the `color` argument in this way.

```R
# Create the object containing the data and aes layers: dia_plot
dia_plot <- ggplot(diamonds, aes(x = carat, y = price))

# Add a geom layer with + and geom_point()
dia_plot + geom_point()

# Add the same geom layer, but with aes() inside
dia_plot + geom_point(aes(color = clarity))

```

# Understanding the grammar, part 2

Continuing with the previous exercise, here you'll explore mixing arguments and aesthetics in a single geometry.

You're still working on the `diamonds` dataset.

##### Instructions

100 XP

- 1 - The `dia_plot` object has been created for you.
- 2 - Update `dia_plot` so that it contains all the functions to make a scatter plot by using [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) for the geom layer. Set `alpha = 0.2`.
- 3 - Using `+`, plot the `dia_plot` object with a [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth) layer on top. You don't want any error shading, which can be achieved by setting the `se = FALSE` in [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth).
- 4 - Modify the [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth) function from the previous instruction so that it contains [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) and map `clarity` to the `col` argument.

- ```R
  # 1 - The dia_plot object has been created for you
  dia_plot <- ggplot(diamonds, aes(x = carat, y = price))
  
  # 2 - Expand dia_plot by adding geom_point() with alpha set to 0.2
  dia_plot <- dia_plot + geom_point(alpha = 0.2)
  
  # 3 - Plot dia_plot with additional geom_smooth() with se set to FALSE
  dia_plot + geom_smooth(se = FALSE)
  
  # 4 - Copy the command from above and add aes() with the correct mapping to geom_smooth()
  dia_plot + geom_smooth(aes(col = clarity), se = FALSE)
  ```

- 

# base package and ggplot2, part 1 - plot

These  courses are about understanding data visualization in the context of  the grammar of graphics. To gain a better appreciation of `ggplot2` and to understand how it operates differently from base package, it's useful to make some comparisons.

In the video, you already saw one example of how to make a (poor)  multivariate plot in base package. In this series of exercises you'll  take a look at a better way using the equivalent version in ggplot2.

First, let's focus on base package. You want to make a plot of `mpg` (miles per gallon) against `wt` (weight in thousands of pounds) in the `mtcars` data frame, but this time you want the dots colored according to the number of cylinders, `cyl`. How would you do that in base package? You can use a little trick to color the dots by specifying a `factor` variable as a color. This works because factors are just a special class of the `integer` type.

##### Instructions

100 XP

- Using the base package [`plot()`](http://www.rdocumentation.org/packages/graphics/functions/plot), make a scatter plot with `mtcars$wt` on the *x-axis* and `mtcars$mpg` on the *y-axis*, colored  according to `mtcars$cyl` (use the `col` argument). You can specify `data =` but you'll just do it the long way here.
- Add a new column, `fcyl`, to the `mtcars` data frame. This should be `cyl` converted to a factor.
- Create a similar plot to instruction 1, but this time, use `fcyl` (which is `cyl` as a factor) to set the `col`.

```R
# Plot the correct variables of mtcars
plot(mtcars$wt, mtcars$mpg, col = mtcars$cyl)

# Change cyl inside mtcars to a factor
mtcars$fcyl <- as.factor(mtcars$cyl)

# Make the same plot as in the first instruction
plot(mtcars$wt, mtcars$mpg, col = mtcars$fcyl)
```

# base package and ggplot2, pChoosing geoms, part 2 - dotplot

Some naming conventions:

    Scatter plots:
    Continuous x, continuous y.
    Dot plots:
    Categorical x, continuous y.

You use geom_point() for both plot types. Jittering position is set in the geom_point() layer.

However, to make a "true" dot plot, you can use geom_dotplot(). The difference is that unlike geom_point(), geom_dotplot() uses a binning statistic. Binning means to cut up a continuous variable (the y in this case) into discrete "bins". You already saw binning with geom_histogram() (see this exercise for a refresher).

One thing to notice is that geom_dotplot() uses a different plotting symbol to geom_point(). For these symbols, the color aesthetic changes the color of its border, and the fill aesthetic changes the color of its interior.

Let's take a look at how the two geoms compare.
Instructions
100 XP

A "basic" dot plot is shown in the viewer (see the code in the editor). Here, cyl (categorical) is mapped onto the x and wt (continuous) is mapped onto the y aesthetic. For this exercise we've already converted am to a factor variable for you.

    1 - Re-draw that plot in the viewer as a "true" dot plot.
        Add a dotplot geom by calling geom_dotplot().
        Set the arguments stackdir = "center" and binaxis = "y". These are our standard settings, but take a look at the help pages and try different settings to get familiar with these arguments.
    2 - Convert the previous ggplot() command to a qplot() command.art 2 - lm
If you want to add a linear model to your plot, shown right, you can define it with [`lm()`](http://www.rdocumentation.org/packages/stats/functions/lm) and then plot the resulting linear model with [`abline()`](http://www.rdocumentation.org/packages/graphics/functions/abline). However, if you want a model for each subgroup, according to cylinders, then you have a couple of options.

You can subset your data, and then calculate the [`lm()`](http://www.rdocumentation.org/packages/stats/functions/lm) and plot each subset separately. Alternatively, you can vectorize over the `cyl` variable using [`lapply()`](http://www.rdocumentation.org/packages/base/functions/lapply) and combine this all in one step. This option is already prepared for you.

The code to the right contains a call to the function `lapply()`, which you might not have seen before. This function takes as input a vector and a function. Then `lapply()` *applies* the function it was given to each element of the vector and returns the results in a list. In this case, `lapply()` takes each element of `mtcars$cyl` and calls the function defined in the second argument. This function takes a value of `mtcars$cyl` and then subsets the data so that only rows with `cyl == x` are used. Then it fits a linear model to the filtered dataset and uses that model to add a line to the plot with the `abline()` function.

Now that you have an interesting plot, there is a very important aspect missing - the legend!

In base package you have to take care of this using the `legend()` function. This has been done for you in the predefined code.

##### Instructions

100 XP

##### Instructions

100 XP

1. Fill in the [`lm()`](http://www.rdocumentation.org/packages/stats/functions/lm) function to calculate a linear model of `mpg` *described by* `wt` and save it as an object called `carModel`.
2. Draw the linear model on the scatterplot.
   - Write code that calls [`abline()`](http://www.rdocumentation.org/packages/graphics/functions/abline) with `carModel` as the first argument. Set the line type by passing the argument `lty = 2`.
   - Run the code that generates the basic plot and the call to `abline()` all at once by highlighting both parts of the script and hitting `control/command` + `enter` on your keyboard. These lines must all be run together in the DataCamp R console so that R will be able to find the plot you want to add a line to.
3. Run the code already given to generate the plot with a different model for each group. You don't need to modify any of this.

- 

- ```R
  # Use lm() to calculate a linear model and save it as carModel
  carModel <- lm(mpg ~ wt, data = mtcars)
  
  # Basic plot
  mtcars$cyl <- as.factor(mtcars$cyl)
  plot(mtcars$wt, mtcars$mpg, col = mtcars$cyl)
  
  # Call abline() with carModel as first argument and set lty to 2
  abline(carModel, lty = 2)
  
  # Plot each subset efficiently with lapply
  # You don't have to edit this code
  plot(mtcars$wt, mtcars$mpg, col = mtcars$cyl)
  lapply(mtcars$cyl, function(x) {
    abline(lm(mpg ~ wt, mtcars, subset = (cyl == x)), col = x)
    })
  
  # This code will draw the legend of the plot
  # You don't have to edit this code
  legend(x = 5, y = 33, legend = levels(mtcars$cyl),
         col = 1:3, pch = 1, bty = "n")
  ```

- 

# base package and ggplot2, part 3

In this exercise you'll recreate the base package plot in `ggplot2`.

The code for base `R` plotting is given at the top. The first line of code already converts the `cyl` variable of `mtcars` to a factor.

##### Instructions

100 XP

##### Instructions

100 XP

- Plot 1: add [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) in order to make a scatter plot.
- Plot 2: copy and paste Plot 1.
- Add a linear model for each subset according to `cyl` by adding a [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth) layer.
- Inside this [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth), set `method` to `"lm"` and `se` to `FALSE`.
- **Note**: `geom_smooth()` will automatically draw a line per `cyl` subset. It recognizes the groups you want to identify by color in the [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) call within the [`ggplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggplot) command.
- Plot 3: copy and paste Plot 2.
- Plot a linear model for the entire dataset, do this by adding another [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth) layer.
- Set the `group` aesthetic inside this [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth) layer to 1. This has to be set within the [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) function.
- Set `method` to `"lm"`, `se` to `FALSE` and `linetype` to 2. These have to be set **outside** [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) of the [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth).
- **Note**: the `group` aesthetic will tell [`ggplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggplot) to draw a single linear model through all the points.

- 

- ```R
  # Convert cyl to factor (don't need to change)
  mtcars$cyl <- as.factor(mtcars$cyl)
  
  # Example from base R (don't need to change)
  plot(mtcars$wt, mtcars$mpg, col = mtcars$cyl)
  abline(lm(mpg ~ wt, data = mtcars), lty = 2)
  lapply(mtcars$cyl, function(x) {
    abline(lm(mpg ~ wt, mtcars, subset = (cyl == x)), col = x)
    })
  legend(x = 5, y = 33, legend = levels(mtcars$cyl),
         col = 1:3, pch = 1, bty = "n")
  
  # Plot 1: add geom_point() to this command to create a scatter plot
  ggplot(mtcars, aes(x = wt, y = mpg, col = cyl)) +
    geom_point()
  
  # Plot 2: include the lines of the linear models, per cyl
  ggplot(mtcars, aes(x = wt, y = mpg, col = cyl)) +
    geom_point() +
    geom_smooth(method = "lm", se = FALSE)
  
  # Plot 3: include a lm for the entire dataset in its whole
  ggplot(mtcars, aes(x = wt, y = mpg, col = cyl)) +
    geom_point() +
    geom_smooth(method = "lm", se = FALSE) +
    geom_smooth(aes(group = 1), method = "lm", se = FALSE, linetype = 2)
  ```

- # Variables to visuals, part 1

- So far you've seen four different forms of the iris dataset: `iris`, `iris.wide`, `iris.wide2` and `iris.tidy`. Don't let all these different forms confuse you! It's exactly the same data, just rearranged so that your plotting functions become easier.

- To see this in action, consider the plot in the graphics device at right. Which form of the dataset would be the most appropriate to use here?

- ##### Instructions

- 100 XP

- - Look at the structures of `iris`, `iris.wide` and `iris.tidy` using [`str()`](http://www.rdocumentation.org/packages/utils/functions/str).
  - Fill in the `ggplot` function with the appropriate data frame and variable names. The variable names of the aesthetics of the plot will match the ones you found using the [`str()`](http://www.rdocumentation.org/packages/utils/functions/str) command in the previous step.

- - ```R
    # Consider the structure of iris, iris.wide and iris.tidy (in that order)
    str(iris)
    str(iris.wide)
    str(iris.tidy)
    
    # Think about which dataset you would use to get the plot shown right
    # Fill in the ___ to produce the plot given to the right
    ggplot(iris.tidy, aes(x = Species, y = Value, col = Part)) +
      geom_jitter() +
      facet_grid(. ~ Measure)
    ```

  - 

# Variables to visuals, part 1b

In the last exercise you saw how `iris.tidy` was used to make a specific plot. It's important to know how to rearrange your data in this way so that your plotting functions become easier. In this exercise you'll use functions from the `tidyr`package to convert `iris` to `iris.tidy`.

The resulting `iris.tidy` data should look as follows:

```
      Species  Part Measure Value
    1  setosa Sepal  Length   5.1
    2  setosa Sepal  Length   4.9
    3  setosa Sepal  Length   4.7
    4  setosa Sepal  Length   4.6
    5  setosa Sepal  Length   5.0
    6  setosa Sepal  Length   5.4
    ...
```

You can have a look at the `iris` dataset by typing `head(iris)` in the console.

*Note:* If you're not familiar with `%>%`, `gather()` and `separate()`, you may want to take the [*Cleaning Data in R*](https://www.datacamp.com/courses/cleaning-data-in-r) course. In a nutshell, a dataset is called tidy when every row is an observation and every column is a variable. The `gather()`function moves information from the columns to the rows. It takes multiple columns and *gathers* them into a single column by adding rows. The `separate()`function splits one column into two or more columns according to a pattern you define. Lastly, the `%>%` (or "pipe") operator passes the result of the left-hand side as the first argument of the function on the right-hand side.

```R
# Load the tidyr package
library(tidyr)

# Fill in the ___ to produce to the correct iris.tidy dataset
iris.tidy <- iris %>%
gather(key, Value, - Species) %>%
  separate(key, c("Part", "Measure"), "\\.")
```

# Variables to visuals, part 2

Here you'll take a look at another plot variant, shown on the right. Which of your data frames would be used to produce this plot?

##### Instructions

100 XP

- Look at the heads of `iris`, `iris.wide` and `iris.tidy` using [`head()`](http://www.rdocumentation.org/packages/utils/functions/head).
- Fill in the `ggplot` function with the appropriate data frame and variable names. The names of the aesthetics of the plot will match with variable names in your dataset. The previous instruction will help you match variable names in datasets with the ones in the plot.

- ```R
  # The 3 data frames (iris, iris.wide and iris.tidy) are available in your environment
  # Execute head() on iris, iris.wide and iris.tidy (in that order)
  head(iris)
  head(iris.wide)
  head(iris.tidy)
  
  # Think about which dataset you would use to get the plot shown right
  # Fill in the ___ to produce the plot given to the right
  ggplot(iris.wide, aes(x = Length, y = Width, color = Part)) +
    geom_jitter() +
    facet_grid(. ~ Species)
  ```

- 

# Variables to visuals, part 2b

In the last exercise you saw how `iris.wide` was used to make a specific plot. You also saw previously how you can derive `iris.tidy` from `iris`. Now you'll move on to produce `iris.wide`.

The head of the `iris.wide` should look like this in the end:

```
  Species  Part Length Width
1  setosa Petal    1.4   0.2
2  setosa Petal    1.4   0.2
3  setosa Petal    1.3   0.2
4  setosa Petal    1.5   0.2
5  setosa Petal    1.4   0.2
6  setosa Petal    1.7   0.4
...
```

You can have a look at the `iris` dataset by typing `head(iris)` in the console.

##### Instructions



- Before you begin, you need to add a new column called `Flower` that contains a unique identifier for each row in the data frame. This is because you'll rearrange the data frame afterwards and you need to keep track of which row, or which specific flower, each value came from. It's done for you, no need to add anything yourself.

- `gather()` rearranges the data frame by specifying the columns that are categorical variables with a `-` notation. In this case, `Species` and `Flower`are categorical. Complete the command.

- `separate()` splits up the new `key` column, which contains the former headers, according to `.`. The new column names `"Part"` and `"Measure"`are given in a character vector.

- The last step is to use [`spread()`](http://www.rdocumentation.org/packages/tidyr/functions/spread) to distribute the new `Measure` column and associated `value` column into two columns.

  ```R
  # Load the tidyr package
  library(tidyr)
  
  # Add column with unique ids (don't need to change)
  iris$Flower <- 1:nrow(iris)
  
  # Fill in the ___ to produce to the correct iris.wide dataset
  iris.wide <- iris %>%
    gather(key, value, -Species, -Flower) %>%
    separate(key, c("Part","Measure"), "\\.") %>%
    spread(Measure, value)
  ```



  # All about aesthetics, part 1

  In the video you saw 9 visible aesthetics. Let's apply them to a categorical variable - the cylinders in `mtcars`, `cyl`.

  (You'll consider line type when you encounter line plots in the next chapter).

  These are the aesthetics you can consider within [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) in this chapter: `x`, `y`, `color`, `fill`, `size`, `alpha`, `labels` and `shape`.

  In the following exercise you can assume that the `cyl` column is categorical. It has already been transformed into a `factor` for you.

  ##### Instructions

  100 XP

  The `mtcars` data frame is available in your workspace. For each of the following four plots, use [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point):

  - 1 - Map `mpg` onto the `x` aesthetic, and `cyl` onto the `y`.
  - 2 - Reverse the mappings of the first plot.
  - 3 - Map `wt` onto `x`, `mpg` onto `y`, and `cyl` onto `color`.
  - Modify the previous plot by changing the `shape` argument of the geom to `1`and increase the `size` to `4`. These are attributes that you should specify inside [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point).

```R
# 1 - Map mpg to x and cyl to y
ggplot(mtcars, aes(x= mpg,y= cyl)) +
  geom_point()
  
# 2 - Reverse: Map cyl to x and mpg to y
ggplot(mtcars, aes(x = cyl, y = mpg)) +
  geom_point()

# 3 - Map wt to x, mpg to y and cyl to col
ggplot(mtcars, aes(x = wt,y = mpg,col = cyl)) +
  geom_point()

# 4 - Change shape and size of the points in the above plot
ggplot(mtcars, aes(mtcars,x= wt,y = mpg,col=cyl)) +
  geom_point(shape=1, cex=4)
```



# All about aesthetics, part 2

The `color` aesthetic typically changes the outside outline of an object and the `fill` aesthetic is typically the inside shading. However, as you saw in the last exercise, `geom_point()` is an exception. Here you use `color`, instead of `fill` for the inside of the point. But it's a bit subtler than that.

**Which shape to use?** The default `geom_point()` uses `shape = 19` (a solid circle with an outline the same colour as the inside). Good alternatives are `shape = 1` (hollow) and `shape = 16` (solid, no outline). These all use the `col` aesthetic (don't forget to set `alpha` for solid points).

A really nice alternative is `shape = 21` which allows you to use *both* `fill` for the inside *and* `col` for the outline! This is a great little trick for when you want to map two aesthetics to a dot.

What happens when you use the wrong aesthetic mapping? This is a very common mistake! The code from the previous exercise is in the editor. Using this as your starting point complete the instructions.



**Note:** In the `mtcars` dataset, `cyl` and `am` have been converted to `factor`for you.

- 1 - Copy & paste the first plot's code. Change the aesthetics so that `cyl` maps to `fill` rather than `col`.

- 2 - Copy & paste the second plot's code. In `geom_point()` change the `shape`argument to `21` and add an `alpha` argument set to `0.6`.

- 3 - Copy & paste the third plot's code. In the `ggplot()` aesthetics, map `am` to `col`.

- ```
  # am and cyl are factors, wt is numeric
  class(mtcars$am)
  class(mtcars$cyl)
  class(mtcars$wt)
  
  # Given from the previous exercise
  ggplot(mtcars, aes(x = wt, y = mpg, col = cyl)) +
    geom_point(shape = 1, size = 4)
  
  # 1 - Map cyl to fill
  ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl)) +
    geom_point(shape = 1, size = 4)
  
  # 2 - Change shape and alpha of the points in the above plot
  ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl)) +
    geom_point(shape = 21, size = 4, alpha = 0.6)
    
  # 3 - Map am to col in the above plot
  ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl, col = am)) +
    geom_point(shape = 21, size = 4, alpha = 0.6)
  ```



  # All about aesthetics, part 3

  Now that you've got some practice with incrementally building up plots, you can try to do it from scratch! The `mtcars` dataset is pre-loaded in the workspace.

  ##### Instructions

  100 XP

  Use `ggplot()` to create a basic scatter plot. Inside `aes()`, map `wt` onto `x`and `mpg` onto `y`. Typically, you would say "mpg described by wt" or "mpg vs wt", but in `aes()`, it's `x` first, `y` second. Use [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) to make three scatter plots:

  - `cyl` on `size`
  - `cyl` on `alpha`
  - `cyl` on `shape`

  Try this last variant:

  - `cyl` on `label`. In order to correctly show the text (i.e. `label`), use [`geom_text()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_text).

```R
# Map cyl to size
ggplot(mtcars,aes(x = wt, y = mpg,size = cyl))+
geom_point()


# Map cyl to alpha
ggplot(mtcars,aes(x = wt , y = mpg, alpha = cyl))+
geom_point()


# Map cyl to shape 
ggplot(mtcars,aes(x = wt, y = mpg,shape = cyl))+
geom_point()



# Map cyl to label
ggplot(mtcars,aes(x = wt, y = mpg,label = cyl))+
geom_point()+
geom_text()
```

# All about attributes, part 1

In  the video you saw that you can use all the aesthetics as attributes.  Let's see how this works with the aesthetics you used in the previous  exercises: `x`, `y`, `color`, `fill`, `size`, `alpha`, `label` and `shape`. 

This time you'll use these arguments to set attributes of the plot,  not aesthetics. However, there are some pitfalls you'll have to watch  out for: these attributes can overwrite the aesthetics of your plot!

**A word about shapes:** In the exercise "All about aesthetics, part 2", you saw that `shape = 21` results in a point that has a fill *and* an outline. Shapes in R can have a value from 1-25. Shapes 1-20 can only accept a `color` aesthetic, but shapes 21-25 have both a `color` *and* a `fill` aesthetic. See the `pch` argument in [`par()`](https://www.rdocumentation.org/packages/graphics/versions/3.4.0/topics/par) for further discussion.

**A word about hexadecimal colours:** Hexadecimal,  literally "related to 16", is a base-16 alphanumeric counting system.  Individual values come from the ranges 0-9 and A-F. This means there are  256 possible two-digit values (i.e. 00 - FF). Hexadecimal colours use  this system to specify a six-digit code for Red, Green and Blue values (`"#RRGGBB"`) of a colour (i.e. Pure blue: `"#0000FF"`, black: `"#000000"`, white: `"#FFFFFF"`). R can accept hex codes as valid colours.

##### Instructions

100 XP

- 1 - You will continue to work with `mtcars`. Use `ggplot()` to create a basic scatter plot: map `wt` onto `x`, `mpg` onto `y` and `cyl` onto `color`.

- 2 - Overwrite the color of the points inside [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) to `my_color`. Notice how this cancels out the colors given to the points by the number of cylinders!

- 3 - Starting with plot 2, map `cyl` to `fill` instead of `col` and set the attributes `size` to `10`, `shape` to `23` and `color` to `my_color` inside [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point).

  ```R
  # Define a hexadecimal color
  my_color <- "#4ABEFF"
  
  # Draw a scatter plot with color *aesthetic*
  ggplot(data = mtcars, mapping = aes(x = wt , y = mpg, col = cyl)) +
  geom_point()
  
  
  # Same, but set color *attribute* in geom layer 
  ggplot(data = mtcars, mapping = aes(x = wt , y = mpg, col = cyl)) +
  geom_point(col = my_color)
  
  
  
  # Set the fill aesthetic; color, size and shape attributes
  ggplot(data = mtcars, mapping = aes(x = wt , y = mpg, fill = cyl)) +
  geom_point(col = my_color, size = 10, shape = 23)
  ```

  # All about attributes, part 2

  In  the videos you saw that you can use all the aesthetics as attributes.  Let's see how this works with the aesthetics you used in the previous  exercises: `x`, `y`, `color`, `fill`, `size`, `alpha`, `label` and `shape`. 

  In this exercise you will set all kinds of attributes of the points!

  You will continue to work with `mtcars`.

  ##### Instructions

  100 XP

  - Add to the first command: draw points with `alpha` set to `0.5`. 
  - Add to the second command: draw points of shape `24` in the color `yellow`. 
  - Add to the third command: draw text with label `rownames(mtcars)` in the color `red`. Don't use [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) here! You should get a scatter plot with the names of the cars instead of points.

  **Note:** Remember to specify characters with quotation marks (`"yellow"`, not `yellow`).

```R
# Expand to draw points with alpha 0.5
ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl))+
geom_point(alpha = 0.5)

  
# Expand to draw points with shape 24 and color yellow
ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl)) +
geom_point(shape = 24, col = "yellow")
  
# Expand to draw text with label rownames(mtcars) and color red
ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl))+
geom_text( label = rownames(mtcars), col = "red")
```

# Going all out

In this exercise, you will gradually add more aesthetics layers to the plot. You're still working with the `mtcars`  dataset, but this time you're using more features of the cars. For  completeness, here is a list of all the features of the observations in `mtcars`:

- `mpg` -- Miles/(US) gallon
- `cyl` -- Number of cylinders
- `disp` -- Displacement (cu.in.)
- `hp` -- Gross horsepower
- `drat` -- Rear axle ratio
- `wt` -- Weight (lb/1000)
- `qsec` -- 1/4 mile time
- `vs` -- V/S engine.
- `am` -- Transmission (0 = automatic, 1 = manual)
- `gear` -- Number of forward gears
- `carb` -- Number of carburetors

Notice that adding more aesthetics to your plot is not always a good  idea. Adding aesthetic mappings to a plot will increase its complexity,  and thus decrease its readability.

##### Instructions

100 XP

**Note:** In this chapter you saw *aesthetics* and *attributes*. Variables in a data frame are *mapped* to aesthetics in `aes()`. (e.g. `aes(col = cyl)`) within `ggplot()`. Visual elements are *set* by attributes in specific geom layers (`geom_point(col = "red")`). Don't confuse these two things - here you're focusing on aesthetic mappings.

- Draw a scatter plot of `mtcars` with `mpg` on the x-axis, `qsec` on the y-axis and `factor(cyl)` as colors.

- Copy the previous plot and expand to include `factor(am)` as the shape of the points. 

- Copy the previous plot and expand to include the ratio of horsepower to weight (i.e. `(hp/wt)`) as the size of the points.

  ```R
  # Map mpg onto x, qsec onto y and factor(cyl) onto col (3 aesthetics):
  ggplot(mtcars, aes(x = mpg, y = qsec, col = factor(cyl))) +
    geom_point()
  
  # Add mapping: factor(am) onto shape (now 4 aesthetics):
  ggplot(mtcars, aes(x = mpg, y = qsec, col = factor(cyl), shape = factor(am))) +
    geom_point()
  
  # Add mapping: (hp/wt) onto size (now 5 aesthetics):
  ggplot(mtcars, aes(x = mpg, y = qsec, col = factor(cyl), shape = factor(am), size = (hp/wt))) +
    geom_point()
  ```

  # Position

  You  saw how jittering worked in the video, but bar plots suffer from their  own issues of overplotting, as you'll see here. Use the `"stack"`, `"fill"` and `"dodge"` positions to reproduce the plot in the viewer.

  The `ggplot2` base layers (data and aesthetics) have already been coded; they're stored in a variable `cyl.am`. It looks like this:

  ```
  cyl.am <- ggplot(mtcars, aes(x = factor(cyl), fill = factor(am)))
  ```

  ##### Instructions

  100 XP

  - Add a [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar) call to `cyl.am`. By default, the `position` will be set to `"stack"`.

  - Fill in the second `ggplot` command. Explicitly set `position` to `"fill"` inside [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar).

  - Fill in the third `ggplot` command. Set `position` to `"dodge"`.

  - The `position = "dodge"` version seems most appropriate. Finish off the fourth `ggplot` command by completing the three `scale_` functions:

  - [`scale_x_discrete()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_discrete) takes as its only argument the x-axis label: `"Cylinders"`.

  - [`scale_y_continuous()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_continuous) takes as its only argument the y-axis label: `"Number"`.

  - [`scale_fill_manual()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_manual) fixes the legend. The first argument is the title of the legend: `"Transmission"`. Next, `values` and `labels` are set to predefined values for you. These are the colors and the labels in the legend.

    ```R
    # The base layer, cyl.am, is available for you
    # Add geom (position = "stack" by default)
    cyl.am + 
      geom_bar()
    
    # Fill - show proportion
    cyl.am + 
      geom_bar(position = "fill")  
    
    # Dodging - principles of similarity and proximity
    cyl.am +
      geom_bar(position = "dodge") 
    
    # Clean up the axes with scale_ functions
    val = c("#E41A1C", "#377EB8")
    lab = c("Manual", "Automatic")
    cyl.am +
      geom_bar(position = "dodge") +
      scale_x_discrete("Cylinders") + 
      scale_y_continuous("Number") +
      scale_fill_manual("Transmission", 
                        values = val,
                        labels = lab) 
    ```

    # Setting a dummy aesthetic

    In  the last chapter you saw that all the visible aesthetics can serve as  attributes and aesthetics, but I very conveniently left out x and y.  That's because although you can make univariate plots (such as  histograms, which you'll get to in the next chapter), a y-axis will  always be provided, even if you didn't ask for it.

    In the `base` package you can make univariate plots with [`stripchart()`](http://www.rdocumentation.org/packages/graphics/functions/stripchart)  (shown in the viewer) directly and it will take care of a fake y axis  for us. Since this is univariate data, there is no real y axis.

    You can get the same thing in `ggplot2`, but it's a bit  more cumbersome. The only reason you'd really want to do this is if you  were making many plots and you wanted them to be in the same style, or  you wanted to take advantage of an aesthetic mapping (e.g. colour).

    ##### Instructions

    100 XP

    - Try to run `ggplot(mtcars, aes(x = mpg)) + geom_point()` in the console. `x` is only one of the two essential aesthetics for [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point), which is why you get an error message.

    - 1 - To fix this, map a value, e.g. `0`, instead of a variable, onto `y`. Use [`geom_jitter()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_jitter) to avoid having all the points on a horizontal line.

    - 2 - To make everything look nicer, copy & paste the code for  plot 1 and change the limits of the y axis using the appropriate `scale_y_...()` function. Set the `limits` argument to `c(-2, 2)`.Setting a dummy aesthetic

      In  the last chapter you saw that all the visible aesthetics can serve as  attributes and aesthetics, but I very conveniently left out x and y.  That's because although you can make univariate plots (such as  histograms, which you'll get to in the next chapter), a y-axis will  always be provided, even if you didn't ask for it.

      In the `base` package you can make univariate plots with [`stripchart()`](http://www.rdocumentation.org/packages/graphics/functions/stripchart)  (shown in the viewer) directly and it will take care of a fake y axis  for us. Since this is univariate data, there is no real y axis.

      You can get the same thing in `ggplot2`, but it's a bit  more cumbersome. The only reason you'd really want to do this is if you  were making many plots and you wanted them to be in the same style, or  you wanted to take advantage of an aesthetic mapping (e.g. colour).

      ##### Instructions

      100 XP

      - Try to run `ggplot(mtcars, aes(x = mpg)) + geom_point()` in the console. `x` is only one of the two essential aesthetics for [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point), which is why you get an error message.
      - 1 - To fix this, map a value, e.g. `0`, instead of a variable, onto `y`. Use [`geom_jitter()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_jitter) to avoid having all the points on a horizontal line.
      - 2 - To make everything look nicer, copy & paste the code for  plot 1 and change the limits of the y axis using the appropriate `scale_y_...()` function. Set the `limits` argument to `c(-2, 2)`.

```R
# 1 - Create jittered plot of mtcars, mpg onto x, 0 onto y
ggplot(mtcars, aes(x = mpg, y = 0)) +
  geom_jitter()

# 2 - Add function to change y axis limits
ggplot(mtcars, aes(x = mpg, y = 0)) +
  geom_jitter()+
scale_y_continuous(limits = c(-2,2))

```

# Overplotting 1 - Point shape and transparency

In  the previous section you saw that there are lots of ways to use  aesthetics. Perhaps too many, because although they are possible, they  are not all recommended. Let's take a look at what works and what  doesn't.

So far you've focused on scatter plots since they are intuitive,  easily understood and very common. A major consideration in any scatter  plot is dealing with **overplotting**. You'll encounter this topic again in the geometries layer, but you can already make some adjustments here.

You'll have to deal with overplotting when you have:

1. Large datasets,
2. Imprecise data and so points are not clearly separated on your plot (you saw this in the video with the `iris` dataset),
3. Interval data (i.e. data appears at fixed values), or
4. Aligned data values on a single axis.

One very common technique that I'd recommend to always use when you  have solid shapes it to use alpha blending (i.e. adding transparency).  An alternative is to use hollow shapes. These are adjustments to make  before even worrying about positioning. This addresses the first point  as above, which you'll see again in the next exercise.

##### Instructions

100 XP

- Begin by making a basic scatter plot of `mpg` (y) vs. `wt` (x), map `cyl` to `color` and make the `size = 4`. `cyl` has already been converted to a factor variable for you.
- Modify the above plot to set `shape` to `1`. This allows for hollow circles.
- Modify the first plot to set `alpha` to `0.6`.

```R
# Basic scatter plot of wt on x-axis and mpg on y-axis; map cyl to col
ggplot(mtcars, aes(x = wt, y = mpg, color = cyl)) +
  geom_point(size = 4)

# Hollow circles - an improvement
ggplot(mtcars, aes(x = wt, y = mpg, color = cyl)) +
  geom_point(size = 4, shape = 1)

# Add transparency - very nice
ggplot(mtcars, aes(x = wt, y = mpg, color = cyl)) +
  geom_point(size = 4, alpha = 0.6)
```

# Overplotting 2 - alpha with large datasets

In  a previous exercise we defined four situations in which you'd have to  adjust for overplotting. You'll consider the last two here with the `diamonds` dataset:

1. Large datasets.
2. Aligned data values on a single axis

##### Instructions

100 XP

- The `diamonds` data frame is available in the `ggplot2` package. Begin by making a basic scatter plot of `price` (y) vs. `carat` (x) and map `clarity` onto `color`.

- Copy the above functions and set the alpha to `0.5`. This is a good start to dealing with the large dataset.

- Align all the diamonds within a `clarity` class, by plotting `carat` (y) vs. `clarity` (x). Map `price` onto `color`. `alpha` should still be `0.5`. 

- In the previous plot, all the individual values line up on a single axis within each `clarity` category, so you have not overcome overplotting. Modify the above plot to use the `position = "jitter"` inside [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point).

  ```R
  # Scatter plot: carat (x), price (y), clarity (color)
  ggplot(data = diamonds, mapping = aes(x = carat, y = price, color = clarity))+
  geom_point()
  
  
  # Adjust for overplotting
  ggplot(data = diamonds, mapping = aes(x = carat, y = price, color = clarity))+
  geom_point(alpha = 0.5)
  
  
  
  # Scatter plot: clarity (x), carat (y), price (color)
  ggplot(data = diamonds, mapping = aes(x = clarity, y = carat,
  color = price))+
  geom_point(alpha = 0.5)
  
  
  # Dot plot with jittering
  ggplot(data = diamonds, mapping = aes(x = clarity, y = carat,
  color = price))+
  geom_point(alpha = 0.5, position = "jitter")
  ```

  # Scatter plots and jittering (1)

  You already saw a few examples using [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) where the result was *not* a scatter plot. For example, in the plot shown in the viewer a continuous variable, `wt`, is mapped to the `y` aesthetic, and a categorical variable, `cyl`, is mapped to the `x` aesthetic. This also leads to over-plotting, since the points are arranged on a single `x` position. You previously dealt with overplotting by setting the `position = jitter` inside [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point). Let's look at some other solutions here.

  ##### Instructions

  100 XP

  Beginning with the code for the plot in the viewer (given), make these modifications

  - 1 - Use a shortcut geom, [`geom_jitter()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_jitter), instead of [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point).
  - 2 - Unfortunately, the *width* of the jitter is a bit too wide to be useful. Adjust this by setting the argument `width = 0.1` inside [`geom_jitter()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_jitter).
  - 3 - Finally, return to [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point) and set the `position` argument here to `position_jitter(0.1)`, which will set the jittering width directly inside a points layer.

  **Note:** For convenience, you could have saved the data and aesthetic layers as a `ggplot2` object and re-used it in all solutions. We've made each plot explicit so that you can see all plotting instructions.

  - ```R
    # Shown in the viewer:
    ggplot(mtcars, aes(x = cyl, y = wt)) +
      geom_point()
    
    # Solutions:
    # 1 - With geom_jitter()
    ggplot(mtcars, aes(x = cyl, y = wt)) +
      geom_jitter()
    
    # 2 - Set width in geom_jitter()
    ggplot(mtcars, aes(x = cyl, y = wt)) +
      geom_jitter(width = 0.1)
    
    # 3 - Set position = position_jitter() in geom_point() ()
    ggplot(mtcars, aes(x = cyl, y = wt)) +
      geom_point(position = position_jitter(0.1))
    ```

  - # Scatter plots and jittering (2)

  - In  the chapter on aesthetics you saw different ways in which you will have  to compensate for overplotting. In the video you saw a dataset that  suffered from overplotting because of the precision of the dataset.

  - Another example you saw is when you have integer data. This can be continuous data measured on an `integer` (i.e. 1 ,2, 3 ...), as opposed to `numeric` (i.e. 1.1, 1.4, 1.5, ...), scale, or two categorical (e.g. `factor`) variables, which are just type `integer` under-the-hood.

  - In such a case you'll have a small, defined number of intersections between the two variables.

  - You will be using the `Vocab` dataset. The `Vocab`  dataset contains information about the years of education and integer  score on a vocabulary test for over 21,000 individuals based on US  General Social Surveys from 1972-2004.

  - ##### Instructions

  - 100 XP

  - - The `Vocab` data frame has been loaded for you. Both the `education` and `vocabulary`  variables are classified as integers. You can imagine these as factor  variables, but here, integers are more convenient to work with. First,  get familiar with the dataset by looking at its structure with [`str()`](http://www.rdocumentation.org/packages/utils/functions/str).
    - Make a basic scatter plot of `vocabulary` (y) vs. `education` (x). Here it becomes apparent that you have issues with overplotting because of the integer scales.
    - Use [`geom_jitter()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_jitter) instead of [`geom_point()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_point).
    - Using the jittered plot, set `alpha` to `0.2` (very low).
    - Using the jittered plot, set `shape` to `1`.

```R
library(carData)
# Examine the structure of Vocab
str(Vocab)

# Basic scatter plot of vocabulary (y) against education (x). Use geom_point()
ggplot(data = Vocab, mapping = aes (x= education, y = vocabulary))+
geom_point()


# Use geom_jitter() instead of geom_point()
ggplot(data = Vocab, mapping = aes (x= education, y = vocabulary))+
geom_jitter()

# Using the above plotting command, set alpha to a very low 0.2
# Use geom_jitter() instead of geom_point()
ggplot(data = Vocab, mapping = aes (x= education, y = vocabulary))+
geom_jitter(alpha = 0.2)


# Using the above plotting command, set the shape to 1
ggplot(data = Vocab, mapping = aes (x= education, y = vocabulary))+
geom_jitter(shape = 1)
```

# Histograms

Histograms are one of the most common and intuitive ways of showing distributions. In this exercise you'll use the `mtcars` data frame to explore typical variations of simple histograms. But first, some background:

**The x axis/aesthetic:** The documentation for [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram) states the argument `stat = "bin"`  as a default. Recall that histograms cut up a continuous variable into  discrete bins - that's what the stat "bin" is doing. You always get 30  evenly-sized bins by default, which is specified with the default  argument `binwidth = range/30`. This is a pretty good starting point if you don't know anything about the variable being ploted and want to start exploring.

**The y axis/aesthetic:** [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram) only requires *one* aesthetic: `x`. But there is clearly a `y` axis on your plot, so where does it come from? Actually, there is a variable mapped to the `y` aesthetic, it's called `..count..`. When [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram) executed the binning statistic (see above), it not only cut up the data into discrete bins, but it also *counted* how many values are in each bin. So there is an *internal* data frame where this information is stored. The `..` calls the variable `count` from this *internal* data frame. This is what appears on the `y` aesthetic. But it gets better! The *density* has also been calculated. This is the *proportional frequency* of this bin in relation to the whole data set. You use `..density..` to access this information.

##### Instructions

100 XP

- 1 - Use the `mtcars` data frame and make a univariate histogram by **mapping** `mpg` onto the `x` aesthetic. Use [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram) for the geom layer.
- 2 - Take plot 1 and manually create 1-unit wide bins with the `binwidth = 1` argument in [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram).
- 3 - Take plot 2, and **map** `..density..` onto the `y` aesthetic (i.e. inside an `aes()`) *inside* [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram). You'll have two `aes()` functions: one inside `ggplot()` and another inside [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram). (See the intro text for a discussion of `..density..`).
  - 4 - Take plot 3 and **set** the **attribute** `fill`, the inside of the bars, to the value `"#377EB8"` in [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram). This should *not* appear in `aes()`, since it's an attribute, not an aesthetic mapping.

```R
# 1 - Make a univariate histogram
ggplot(mtcars, aes(mpg)) +
  geom_histogram()

# 2 - Plot 1, plus set binwidth to 1 in the geom layer
ggplot(mtcars, aes(mpg)) +
  geom_histogram(binwidth = 1)

# 3 - Plot 2, plus MAP ..density.. to the y aesthetic (i.e. in a second aes() function)
ggplot(mtcars, aes(mpg)) +
  geom_histogram(aes(y = ..density..), binwidth = 1)

# 4 - plot 3, plus SET the fill attribute to "#377EB8"
ggplot(mtcars, aes(mpg)) +
  geom_histogram(aes(y = ..density..), binwidth = 1, fill = "#377EB8")
```

# Position

In the previous chapter you saw that there are lots of ways to position scatter plots. Likewise, the [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar) and [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram) geoms also have a `position` argument, which you can use to specify how to draw the bars of the plot.

Three `position` arguments will be introduced here:

- `stack`: place the bars on top of each other. Counts are used. **This is the default position**.
- `fill`: place the bars on top of each other, but this time use proportions.
- `dodge`: place the bars next to each other. Counts are used.

In this exercise you'll draw the total count of cars having a given number of cylinders (`cyl`), according to manual or automatic transmission type (`am`) - as shown in the viewer.

Since, in the built-in `mtcars` data set, `cyl` and `am` are integers, they have already been converted to factor variables for you.

##### Instructions

100 XP

- 1 - Using `mtcars`, map `cyl` onto the `x` aesthetic and `am` onto `fill`. Use [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar) to make a bar plot.

- 2 - Take plot 1 and explicitly set `position = "stack"` in [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar). This doesn't change anything, does it? It was mentioned above that `"stack"` is the default.

- 3 - Take plot 2 and set `position = "fill"` in [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar).

- 4 - Take plot 3 and set `position = "dodge"` in [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar).

  ```R
  # Draw a bar plot of cyl, filled according to am
  ggplot(mtcars, aes(x = cyl, fill = am)) +
    geom_bar()
  
  # Change the position argument to stack
  ggplot(mtcars, aes(x = cyl, fill = am)) +
    geom_bar(position = "stack")
  
  
  # Change the position argument to fill
  ggplot(mtcars, aes(x = cyl, fill = am)) +
    geom_bar(position = "fill")
  
  
  # Change the position argument to dodge
  ggplot(mtcars, aes(x = cyl, fill = am)) +
    geom_bar(position = "dodge")
  
  ```

  So far you've seen three different positions for bar plots: `stack` (the default), `dodge` (preferred), and `fill` (to show proportions).

  However, you can go one step further by adjusting the dodging, so  that your bars partially overlap each other. For this example you'll  again use the `mtcars` dataset. Like last time `cyl` and `am` are already available as factors inside `mtcars`.

  Instead of using `position = "dodge"` you're going to use `position_dodge()`, like you did with `position_jitter()` in the [Scatter plots and jittering (1)](https://campus.datacamp.com/courses/774/1833?ex=2) exercise. Here, you'll save this as an object, `posn_d`, so that you can easily reuse it.

  Remember, the reason you want to use `position_dodge()` (and `position_jitter()`) is to specify *how much* dodging (or jittering) you want.

  ##### Instructions

  100 XP

  - 1 - The last plot from the last exercise has been provided for you.
  - 2 - Define a new object called `posn_d` by calling [`position_dodge()`](http://www.rdocumentation.org/packages/ggplot2/functions/position_dodge) with the argument `width = 0.2`.
  - 3 - Take plot 1 and make slightly overlapping bars by using the `position = posn_d` argument.
  - 4 - Take plot 3 and set `alpha = 0.6` to see the overlap in bars.

```R
# 1 - The last plot form the previous exercise
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar(position = "dodge")

# 2 - Define posn_d with position_dodge()
posn_d <- position_dodge(width = 0.2)

# 3 - Change the position argument to posn_d
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar(position = posn_d)



# 4 - Use posn_d as position and adjust alpha to 0.6
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar(position = posn_d,alpha = 0.6)
```

# Overlapping histograms

Overlapping histograms pose similar problems to overlapping bar plots, but there is a unique solution here: a frequency polygon.

This is a geom specific to binned data that draws a line connecting the value of each bin. Like [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram), it takes a `binwidth` argument and by default `stat = "bin"` and `position = "identity"`.

##### Instructions

100 XP

- The code for a basic histogram of `mpg`, which you've already seen, is provided. Extend the code to map `cyl` onto `fill` inside [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes).

- The default position for histograms is `"stack"`. Copy your solution to the first exercise and set the position for the histogram bars to `"identity"`.

- Using the same data and base layers as in the previous two plots, create a plot with a [`geom_freqpoly()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram). Because you're no longer working with bars, change the [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) function: `cyl` should be mapped onto `color`, not onto `fill`. This will correctly color the geom.

  ```R
   A basic histogram, add coloring defined by cyl
  ggplot(mtcars, aes(mpg, fill = cyl)) +
    geom_histogram(binwidth = 1)
  
  # Change position to identity
  ggplot(mtcars, aes(mpg, fill = cyl)) +
    geom_histogram(binwidth = 1, position = "identity")
  
  # Change geom to freqpoly (position is identity by default)
  ggplot(mtcars, aes(mpg, color = cyl)) +
    geom_freqpoly(binwidth = 1)
  ```

  Bar plots with color ramp, part 1

  In this example of a bar plot, you'll fill each segment according to an ordinal variable. The best way to do that is with a sequential color series.

  You'll be using the Vocab dataset from earlier. Since this is a much larger dataset with more categories, you'll also compare it to a simpler dataset, mtcars. Both datasets are ordinal.
  Instructions
  100 XP

  ```R
  The bar plot from the previous exercise is provided - cyl is on the x-axis and filled according to transmission type, am. Notice how you can set the color palette used to fill the bars with scale_fill_brewer(). For a full list of possible color sets, have a look at ?brewer.pal.
  Explore Vocab with str(). Notice that the education and vocabulary variables have already been converted to factor variables for you.
  Make a filled bar chart with the Vocab dataset.
      Map education to x and vocabulary to fill.
      Inside geom_bar(), make sure to set position = "fill".
      Allow color brewer to choose a default color palette by using the appropriate scale function, without arguments. Notice how this generates a warning message and an incomplete plot.
  ```

```R
# Example of how to use a brewed color palette
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar() +
  scale_fill_brewer(palette = "Set1")

# Use str() on Vocab to check out the structure
str(Vocab)

# Plot education on x and vocabulary on fill
# Use the default brewed color palette
ggplot(data = Vocab,mapping = aes(x = education, fill = vocabulary))+
geom_bar(position = "fill")+
scale_fill_brewer()
```

# Bar plots with color ramp, part 2

In the previous exercise, you ended up with an incomplete bar plot. This was because for continuous data, the default `RColorBrewer` palette that  [`scale_fill_brewer()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_brewer) calls is `"Blues"`. There are only 9 colours in the palette, and since you have 11 categories, your plot looked strange.

In this exercise, you'll manually create a color palette that can  generate all the colours you need. To do this you'll use a function  called [`colorRampPalette()`](http://www.rdocumentation.org/packages/grDevices/functions/colorRamp).

The *input* is a character vector of 2 or more colour values, e.g. `"#FFFFFF"` (white) and `"#0000FF"` (pure blue). (See [this](https://campus.datacamp.com/courses/data-visualization-with-ggplot2-1/chapter-3-aesthetics?ex=5) exercise for a discussion on hexadecimal codes).

The *output* is itself a function! So when you assign it to an  object, that object should be used as a function. To see what we mean,  execute the following three lines in the console:

```
new_col <- colorRampPalette(c("#FFFFFF", "#0000FF"))
new_col(4) # the newly extrapolated colours
munsell::plot_hex(new_col(4)) # Quick and dirty plot
```

`new_col()` is a function that takes one argument: the  number of colours you want to extrapolate. You want to use nicer  colours, so we've assigned the entire `"Blues"` colour palette from the `RColorBrewer` package to the character vector `blues`.

##### Instructions

100 XP

- 1 - Like in the example code above, create a new function called `blue_range` that uses [`colorRampPalette()`](http://www.rdocumentation.org/packages/grDevices/functions/colorRamp) to extrapolate over all 9 values of the `blues` character vector.
- 2 - Take the plot code from the last exercise (provided), and change [`scale_fill_brewer()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_brewer) to be [`scale_fill_manual()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_manual). Set the argument `values = blue_range(11)` inside [`scale_fill_manual()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_manual).

```R
# Final plot of last exercise
ggplot(Vocab, aes(x = education, fill = vocabulary)) +
  geom_bar(position = "fill") +
  scale_fill_brewer()

# Definition of a set of blue colors
blues <- brewer.pal(9, "Blues")

# Make a color range using colorRampPalette() and the set of blues
blue_range <- colorRampPalette(blues)

# Use blue_range to adjust the color of the bars, use scale_fill_manual()
ggplot(Vocab, aes(x = education, fill = vocabulary)) +
  geom_bar(position = "fill") +
  scale_fill_manual(values = blue_range(11))
```

# Overlapping histograms (2)

As  a last example of bar plots, you'll return to histograms (which you now  see are just a special type of bar plot). You saw a nice trick in a  previous exercise of how to slightly overlap bars, but now you'll see  how to overlap them completely. This would be nice for multiple  histograms, as long as there are not too many different overlaps!

You'll make a histogram using the `mpg` variable in the `mtcars` data frame.

##### Instructions

100 XP

- 1 - A basic histogram plot is provided.
- 2 - Take plot 1 and map `am` onto `fill` within the [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) function. The default position is `"stack"`.
- 3 - Take plot 2 and add the `position` argument within [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram). Set it to `"dodge"`.
- 4 - Take plot 3 and change the `position` argument to `"fill"`. In this case, none of these positions really work well, because it's difficult to compare the distributions directly.
- 5 - Take plot 4 and change the `position` argument to `"identity"` and set `alpha = 0.4`. This produces overlapping bars.
- 6 - Take plot 5 and change the aesthetic mapping. Map `cyl` onto `fill`.

```R
# 1 - Basic histogram plot command
ggplot(mtcars, aes(mpg)) +
  geom_histogram(binwidth = 1)

# 2 - Plot 1, Expand aesthetics: am onto fill
ggplot(mtcars, aes(mpg,fill = am)) +
  geom_histogram(binwidth = 1, position = "stack")


# 3 - Plot 2, change position = "dodge"
ggplot(mtcars, aes(mpg,fill = am)) +
  geom_histogram(binwidth = 1, position = "dodge")


# 4 - Plot 3, change position = "fill"
# 3 - Plot 2, change position = "dodge"
ggplot(mtcars, aes(mpg,fill = am)) +
  geom_histogram(binwidth = 1, position = "fill")


# 5 - Plot 4, plus change position = "identity" and alpha = 0.4
ggplot(mtcars, aes(mpg,fill = am)) +
  geom_histogram(binwidth = 1, position = "identity",alpha = 0.4)


# 6 - Plot 5, plus change mapping: cyl onto fill
ggplot(mtcars, aes(mpg,fill = cyl)) +
  geom_histogram(binwidth = 1, position = "identity",alpha = 0.4)
```

## Line plots

In the video you saw how to make line plots using time series data. To explore this topic, you'll use the `economics`  data frame, which contains time series for unemployment and population  statistics from the Federal Reserve Bank of St. Louis in the US. The  data is contained in the `ggplot2` package.

To begin with, you can look at how the median unemployment time and  the unemployment rate (the number of unemployed people as a proportion  of the population) change over time.

In the next exercises, you'll explore to how add embellishments to the line plots, such as recession periods.

##### Instructions

100 XP

- Print out the [`head()`](http://www.rdocumentation.org/packages/utils/functions/head) of the `economics` data frame.
- Use the `economics` data frame to plot `date` on the x axis and `unemploy` on the y-axis. Use [`geom_line()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_path).
- Copy, paste and adjust the code for the previous instruction: instead of `unemploy`, plot `unemploy/pop` to represent the fraction of the total population that is unemployed.

```R
# Print out head of economics
head(economics)

# Plot unemploy as a function of date using a line plot
ggplot(economics, aes(x = date, y = unemploy)) +
geom_line()


# Adjust plot to represent the fraction of total population that is unemployed
ggplot(economics, aes(x = date, y = unemploy/pop)) +
geom_line()

```

​	Periods of recession

By  themselves, time series often contain enough valuable information, but  you always want to maximize the number of variables you can show in a  plot. This allows you (and your viewers) to begin making comparisons  between those variables that would otherwise be difficult or impossible.

Here, you'll add shaded regions to the background to indicate  recession periods. How do unemployment rate and recession period  interact with each other?

In addition to the `economics` dataset from before, you'll also use the `recess` dataset for the periods of recession. The `recess` data frame contains 2 variables: the `begin` period of the recession and the `end`. It's already available in your workspace.

##### Instructions

100 XP

Expand the command from the previous exercise with [`geom_rect()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_tile). You will use this geom layer to draw rectangles across the recession periods. There are a few pitfalls here:

- [`geom_rect()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_tile) uses the `recess` dataset, so pass this directly as `data = recess` inside [`geom_rect()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_tile).

- The [`geom_rect()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_tile) command shouldn't inherit aesthetics from the base [`ggplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggplot) command it belongs to. It would result in an error, since you're using a different dataset and it doesn't contain `unemploy` or `pop`. That's why you should specify `inherit.aes = FALSE` in [`geom_rect()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_tile).

- [`geom_rect()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_tile) needs four aesthetics: `xmin`, `xmax`, `ymin` and `ymax`. These should be set to `begin`, `end` and `-Inf`, `+Inf`, respectively. Define them within `aes()`.

- The rectangles you add will be black and opaque by default. Set `fill` to `"red"` and `alpha` to `0.2` to improve this. Define them outside `aes()`.

  ```R
  # Basic line plot
  ggplot(economics, aes(x = date, y = unemploy/pop)) +
    geom_line()
  
  # Expand the following command with geom_rect() to draw the recess periods
  ggplot(economics, aes(x = date, y = unemploy/pop)) +
    geom_rect(data= recess,
           aes( xmin=  begin , xmax = end, ymin = -Inf, ymax = +Inf),
           inherit.aes = FALSE, color= "red", alpha= 0.2) +
    geom_line()
  ```

  # Multiple time series, part 1

  In  the data chapter we discussed how the form of your data affects how you  can plot it. Here, you'll explore that topic in the context of multiple  time series.

  The dataset you'll use contains the global capture rates of seven salmon species from 1950 - 2010.

  In your workspace, the following dataset is available:

  - `fish.species`: Each variable (column) is a Salmon `Species` and each observation (row) is one `Year`.

  To get a multiple time series plot, however, both `Year` and `Species`  should be in their own column. You need tidy data: one variable per  column. Once you have that you can get the plot shown in the viewer by  mapping `Year` to the x aesthetic and `Species` to the color aesthetic.

  You'll use the `gather()` function of the `tidyr` package, which is already loaded for you.

  ##### Instructions

  100 XP

  - Use [`gather()`](http://www.rdocumentation.org/packages/tidyr/functions/gather) to move from `fish.species` to a tidy data frame, `fish.tidy`. This data frame should have three columns: `Year` (int), `Species` (factor) and `Capture` (int).

  - [`gather()`](http://www.rdocumentation.org/packages/tidyr/functions/gather) takes four arguments: the original data frame (`fish.species`), the name of the key column (`Species`), the name of the value column (`Capture`) and the name of the grouping variable, with a minus in front (`-Year`). They can all be specified as object names (i.e. no `""`).

    ```R
    # Check the structure as a starting point
    str(fish.species)
    
    # Use gather to go from fish.species to fish.tidy
    fish.tidy <- fish.species %>% gather(Species,Capture, -Year)
    ```

    ## Multiple time series, part 2

    Now that you have tidy data, you're ready to make your plot! The data frame `fish.tidy` is already available in the workspace, so you can start right away!

    ##### Instructions

    100 XP

    Use `ggplot2` and everything you've learned to recreate the plot shown on the right.`

```R
# Recreate the plot shown on the right
ggplot(fish.tidy, aes(x = Year, y = Capture,color = Species)) +
geom_line()
```

# Using qplot

For simple exploratory plots, there are a variety of functions available. `ggplot2` offers a powerful and diverse array of functions, but [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot) allows for quick and dirty plots. Plus, you should also be familiar with basic plotting notation.

##### Instructions

100 XP

- Have a look at the base R plotting function. It plots `mpg` on the y-axis against `wt` on the x-axis. Create the same plot using [`ggplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggplot).
- Create the same plot using [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot).

```R
# The old way (shown)
plot(mpg ~ wt, data = mtcars) # formula notation
with(mtcars, plot(wt, mpg)) # x, y notation

# Using ggplot:
ggplot(mtcars, aes(x = wt, y = mpg)) +
 geom_point()

# Using qplot:
qplot(wt,mpg, data = mtcars)

```

# Using aesthetics

You  already saw how some aesthetics are only applicable to categorical  variables, such as shapes and linetypes. But just because others, such  as size and color (and hence fill), can be applied to both categorical  and continuous variables, doesn't mean that they're suitable for both.

##### Instructions

100 XP

- A basic scatter plot of `mpg` vs. `wt` from the `mtcars` dataset, made with `qplot()`, is provided.
- Using [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot), map the categorical variable `cyl` onto `size`. Remember, you'll have to wrap the variable name in a `factor()` function to convert to a categorical variable.
- Use [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot) again to the same plot, except with `gear` mapped onto `size`.
- Using [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot), map the continuous variable `hp` onto `color`.
- Use [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot) again to the same plot, except with `qsec` mapped onto `color`.

```R
# basic qplot scatter plot:
qplot(wt, mpg, data = mtcars)

# Categorical variable mapped onto size:
# cyl
qplot(wt, mpg, data = mtcars, size =factor(cyl))

# gear
qplot(wt, mpg, data = mtcars, size =factor(gear))

# Continuous variable mapped onto col:
# hp
qplot(wt, mpg, data = mtcars, color = hp)

# qsec
qplot(wt, mpg, data = mtcars, color = qsec)
```

​	Choosing geoms, part 1

`qplot` automatically takes care of assigning a geom to our plot given the type of data, but you can specify the geom yourselves.

##### Instructions

100 XP

- Make a quick plot using [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot). Use the `mtcars` dataset and plot only `factor(cyl)` onto `x`. Which geom does [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot) choose?

- Extend the previous [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot) command so that it maps `factor(vs)` onto `y`. Which geom does [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot) use now?

- The previous plot had overlapping points. For the last instruction, copy the previous [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot), but manually set `geom` to `"jitter"` in [`qplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/qplot).

  ```R
  # qplot() with x only
  qplot(data = mtcars,factor(cyl))
  
  # qplot() with x and y
  qplot(factor(cyl),factor(vs),data=mtcars)
  
  # qplot() with geom set to jitter manually
  qplot(factor(cyl),factor(vs),data=mtcars,geom="jitter")
  ```

  

  Choosing geoms, part 2 - dotplot

  Some naming conventions:

      Scatter plots:
      Continuous x, continuous y.
      Dot plots:
      Categorical x, continuous y.

  You use geom_point() for both plot types. Jittering position is set in the geom_point() layer.

  However, to make a "true" dot plot, you can use geom_dotplot(). The difference is that unlike geom_point(), geom_dotplot() uses a binning statistic. Binning means to cut up a continuous variable (the y in this case) into discrete "bins". You already saw binning with geom_histogram() (see this exercise for a refresher).

  One thing to notice is that geom_dotplot() uses a different plotting symbol to geom_point(). For these symbols, the color aesthetic changes the color of its border, and the fill aesthetic changes the color of its interior.

  Let's take a look at how the two geoms compare.
  Instructions
  100 XP

  A "basic" dot plot is shown in the viewer (see the code in the editor). Here, cyl (categorical) is mapped onto the x and wt (continuous) is mapped onto the y aesthetic. For this exercise we've already converted am to a factor variable for you.

  ```R
  	# qplot() with x only
  qplot(data = mtcars,factor(cyl))
  
  # qplot() with x and y
  qplot(factor(cyl),factor(vs),data=mtcars)
  
  # qplot() with geom set to jitter manually
  qplot(factor(cyl),factor(vs),data=mtcars,geom="jitter")
  ```


# Choosing geoms, part 2 - dotplot

Some naming conventions:

    Scatter plots:
    Continuous x, continuous y.
    Dot plots:
    Categorical x, continuous y.

You use geom_point() for both plot types. Jittering position is set in the geom_point() layer.

However, to make a "true" dot plot, you can use geom_dotplot(). The difference is that unlike geom_point(), geom_dotplot() uses a binning statistic. Binning means to cut up a continuous variable (the y in this case) into discrete "bins". You already saw binning with geom_histogram() (see this exercise for a refresher).

One thing to notice is that geom_dotplot() uses a different plotting symbol to geom_point(). For these symbols, the color aesthetic changes the color of its border, and the fill aesthetic changes the color of its interior.

Let's take a look at how the two geoms compare.
Instructions
100 XP

A "basic" dot plot is shown in the viewer (see the code in the editor). Here, cyl (categorical) is mapped onto the x and wt (continuous) is mapped onto the y aesthetic. For this exercise we've already converted am to a factor variable for you.

    1 - Re-draw that plot in the viewer as a "true" dot plot.
        Add a dotplot geom by calling geom_dotplot().
        Set the arguments stackdir = "center" and binaxis = "y". These are our standard settings, but take a look at the help pages and try different settings to get familiar with these arguments.
    2 - Convert the previous ggplot() command to a qplot() command.
```R
# cyl and am are factors, wt is numeric
class(mtcars$cyl)
class(mtcars$am)
class(mtcars$wt)

# "Basic" dot plot, with geom_point():
ggplot(mtcars, aes(cyl, wt, col = am)) +
  geom_point(position = position_jitter(0.2, 0))

# 1 - "True" dot plot, with geom_dotplot():
ggplot(mtcars, aes(cyl, wt, fill = am)) +
  geom_dotplot( binaxis= "y", stackdir = "center")

# 2 - qplot with geom "dotplot", binaxis = "y" and stackdir = "center"
qplot(
  cyl,wt,
  data = mtcars,
  fill = am,
  geom = "dotplot",
  binaxis = "y",
  stackdir = "center"
)
```

Chicken weight

The ChickWeight dataset is a data frame which represents the progression of weight of several chicks. The little chicklings are each given a specific diet. There are four types of diet and the farmer wants to know which one fattens the chicks the fastest.

It's time to do some exploratory statistics on the data frame using the techniques you learned in this course! Let's do some ggplot-ing!
Instructions
100 XP

1 - Execute head(ChickWeight) to check the first few rows of this dataset. Looks like the data is pretty tidy!
2 - Plot a line for each chick.
​    Use ggplot() and map Time to x and weight to y within the aes() function.
​    Add geom_line() at the end to draw the lines.
​    To draw one line per chick, add group = Chick to the aes() of geom_line().
​    Oops! That looks pretty chaotic and you can't really conclude anything from it. Let's try again.
3 - Take plot 2 and add color = Diet within the aes() of ggplot(). There's some more information here, although it would be better to have some summary statistics as well. What do you think would be helpful?
4 - Take plot 3 and add geom_smooth() with attributes lwd set to 2 and se set to FALSE. Inside geom_line(), set alpha of to 0.3.

```R
# ChickWeight is available in your workspace
# 1 - Check out the head of ChickWeight
head(ChickWeight)

# 2 - Basic line plot
ggplot(ChickWeight, aes(x = Time, y = weight)) +
  geom_line(aes(group = Chick))

# 3 - Take plot 2, map Diet onto col.
# ChickWeight is available in your workspace
# 1 - Check out the head of ChickWeight
head(ChickWeight)

# 2 - Basic line plot
ggplot(ChickWeight, aes(x = Time, y = weight,col=Diet)) +
  geom_line(aes(group = Chick))



# 4 - Take plot 3, add geom_smooth()
ggplot(ChickWeight, aes(x = Time, y = weight,col=Diet)) +
  geom_line(aes(group = Chick),alpha=0.3)+
  geom_smooth(lwd = 2, se = F,)
```
 Titanic

You've watched the movie Titanic by James Cameron (1997) again and after a good portion of sobbing you decide to investigate whether you'd have a chance of surviving this disaster.

To start your investigation, you decide to do some exploratory visualization with ggplot(). You have information on who survived the sinking given their age, sex and passenger class.
Instructions
100 XP

1 - Have a look at the str() of the titanic dataset, which has been loaded into your workspace. Looks like the data is pretty tidy!
2 - Plot the distribution of sexes within the classes of the ship.
​    Use ggplot() with the data layer set to titanic.
​    Map Pclass onto the x axis, Sex onto fill and draw a dodged bar plot using geom_bar(), i.e. set the geom position to "dodge".
3 - These bar plots won't help you estimate your chances of survival. Copy the previous bar plot, but this time add a facet_grid() layer: . ~ Survived.
4 - We've defined a position object for you.
5 - Include Age, the final variable.
​    Take plot 3 and add a mapping of Age onto the y aesthetic.
​    Change geom_bar() to geom_point() and set its attributes size = 3, alpha = 0.5 and position = posn.jd.
​    Make sure that Sex is mapped onto color instead of fill to correctly color the scatter plots. (This was discussed in detail here and here).

```R
# titanic is avaliable in your workspace
# 1 - Check the structure of titanic
str(titanic)

# 2 - Use ggplot() for the first instruction
ggplot(titanic, aes(x = Pclass, fill = Sex))+
  geom_bar(position ="dodge")

# 3 - Plot 2, add facet_grid() layer
ggplot(titanic, aes(x = Pclass, fill = Sex))+
  geom_bar(position ="dodge")+
  facet_grid(.~Survived)

# 4 - Define an object for position jitterdodge, to use below
posn.jd <- position_jitterdodge(0.5, 0, 0.6)

# 5 - Plot 3, but use the position object from instruction 4
ggplot(titanic, aes(x = Pclass,y=Age,color = Sex))+
geom_point(alpha = 0.5, size = 3, position=posn.jd)+
  facet_grid(.~Survived)
```

# Part 2

# Smoothing

Welcome to the exercises for the second `ggplot2` course!

To practice on the remaining four layers (statistics, coordinates,  facets and themes), we'll continue working on several datasets that we  already encountered in the first course.

The `mtcars` dataset contains information for 32 cars from  Motor Trends magazine from 1973. This dataset is small, intuitive, and  contains a variety of continuous and categorical (both nominal and  ordinal) variables.

In the previous course we learned how to effectively use some basic  geometries, such as point, bar and line. In the first chapter of this  course we'll explore statistics associated with specific geoms, for  example, smoothing and lines.

##### Instructions

100 XP

- Familiarize yourself again with the `mtcars` dataset using [`str()`](http://www.rdocumentation.org/packages/utils/functions/str).

- Extend the first ggplot call: add a LOESS smooth to the scatter plot (which is the default) with [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth). We want to have the actual values and the smooth on the same plot.

- Change the previous plot to use an ordinary linear model, by default it will be `y ~ x`, so you don't have to specify a formula. You should set the `method` argument to `"lm"`.

- Modify the previous plot to remove the 95% CI ribbon. You should set the `se` argument to `FALSE`.

- Modify the previous plot to show only the model, and not the underlying dots.Smoothing

  Welcome to the exercises for the second `ggplot2` course!

  To practice on the remaining four layers (statistics, coordinates,  facets and themes), we'll continue working on several datasets that we  already encountered in the first course.

  The `mtcars` dataset contains information for 32 cars from  Motor Trends magazine from 1973. This dataset is small, intuitive, and  contains a variety of continuous and categorical (both nominal and  ordinal) variables.

  In the previous course we learned how to effectively use some basic  geometries, such as point, bar and line. In the first chapter of this  course we'll explore statistics associated with specific geoms, for  example, smoothing and lines.

  ##### Instructions

  100 XP

  - Familiarize yourself again with the `mtcars` dataset using [`str()`](http://www.rdocumentation.org/packages/utils/functions/str).

  - Extend the first ggplot call: add a LOESS smooth to the scatter plot (which is the default) with [`geom_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth). We want to have the actual values and the smooth on the same plot.

  - Change the previous plot to use an ordinary linear model, by default it will be `y ~ x`, so you don't have to specify a formula. You should set the `method` argument to `"lm"`.

  - Modify the previous plot to remove the 95% CI ribbon. You should set the `se` argument to `FALSE`.

  - Modify the previous plot to show only the model, and not the underlying dots.

    ```R
    # ggplot2 is already loaded
    
    # Explore the mtcars data frame with str()
    str(mtcars)
    
    # A scatter plot with LOESS smooth
    ggplot(mtcars, aes(x = wt, y = mpg)) +
      geom_point()+
      geom_smooth()
    
    
    # A scatter plot with an ordinary Least Squares linear model
    ggplot(mtcars, aes(x = wt, y = mpg)) +
      geom_point()+
       geom_smooth(method="lm")
    
    
    # The previous plot, without CI ribbon
    ggplot(mtcars, aes(x = wt, y = mpg)) +
      geom_point()+
      geom_smooth(method="lm",se=F)
    
    
    # The previous plot, without points
    ggplot(mtcars, aes(x = wt, y = mpg)) +
    geom_smooth(method="lm",se=F)
    ```

# Grouping variables

We'll  continue with the previous exercise by considering the situation of  looking at sub-groups in our dataset. For this we'll encounter the  invisible `group` aesthetic.

##### Instructions

100 XP

A plot that maps `cyl` onto the `col` aesthetic is already coded.

- Change `col` so that `factor(cyl)` is mapped onto it instead of just `cyl`.

  **Note**: In this `ggplot` command our smooth is calculated for each subgroup because there is an invisible aesthetic, `group` which inherits from `col`.

- Complete the second `ggplot` command.

- Add another `stat_smooth()` layer with exactly the same attributes (`method` set to `"lm"`, `se` to `FALSE`).

- Add a `group` aesthetic inside the [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) of this new `stat_smooth()`, set it to a dummy variable, `1`.

  ```R
  # ggplot2 is already loaded
  
  # 1 - Define cyl as a factor variable
  ggplot(mtcars, aes(x = wt, y = mpg, col = factor(cyl))) +
    geom_point() +
    stat_smooth(method = "lm", se = FALSE)
  
  # 2 - Plot 1, plus another stat_smooth() containing a nested aes()
  ggplot(mtcars, aes(x = wt, y = mpg, col = factor(cyl))) +
    geom_point() +
    stat_smooth(method = "lm", se = FALSE) +
    stat_smooth(method = "lm", se = FALSE, aes(group = 1))
  ```

  # Modifying stat_smooth

  In the previous exercise we used `se = FALSE` in `stat_smooth()` to remove the 95% Confidence Interval. Here we'll consider another argument, `span`, used in LOESS smoothing, and we'll take a look at a nice scenario of properly mapping different models.

  `ggplot2` is already loaded and several of the linear models we looked at in the two previous exercises are already given.

  ##### Instructions

  100 XP

  - Plot 1: Recall that LOESS smoothing is a non-parametric form of  regression that uses a weighted, sliding-window, average to calculate a  line of best fit. We can control the size of this window with the `span` argument.
    - Add `span`, set it to `0.7`.
  - Plot 2: In this plot, we set a linear model for the entire dataset as well as each subgroup, defined by `cyl`. In the second `stat_smooth()`,
    - Set `method` to `"loess"` (this is the default with a small (n < 1000) data set, but we will specify it explicitly).
    - Add `span`, set it to `0.7`.
  - Plot 3: Plot 2 presents a problem because there is a black line  on our plot that is not included in the legend. To get this, we need to *map* something to `col` as an *aesthetic*, not just *set* `col` as an *attribute*.
    - Add `col` to the `aes()` function in the second `stat_smooth()`, set it to `"All"`. This will name the line properly.
    - Remove the `col` attribute in the second `stat_smooth()`. Otherwise, it will overwrite the `col` aesthetic.
  - Plot 4: Now we should see our "All" model in the legend, but it's not black anymore. 
    - Add a scale layer: [`scale_color_manual()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_manual) with the first argument set to `"Cylinders"` and `values` set to the predefined `myColors` variable.

```R
# Plot 1: change the LOESS span
ggplot(mtcars, aes(x = wt, y = mpg)) +
  geom_point() +
  # Add span below
  geom_smooth(se = FALSE, span = 0.7)

# Plot 2: Set the second stat_smooth() to use LOESS with a span of 0.7
ggplot(mtcars, aes(x = wt, y = mpg, col = factor(cyl))) +
  geom_point() +
  stat_smooth(method = "lm", se = FALSE) +
  # Change method and add span below
  stat_smooth(method = "loess", aes(group = 1),
              se = FALSE, col = "black", span = 0.7)

# Plot 3: Set col to "All", inside the aes layer of stat_smooth()
ggplot(mtcars, aes(x = wt, y = mpg, col = factor(cyl))) +
  geom_point() +
  stat_smooth(method = "lm", se = FALSE) +
  stat_smooth(method = "loess",
              # Add col inside aes()
              aes(group = 1, col = "All"),
              # Remove the col argument below
              se = FALSE, span = 0.7)

# Plot 4: Add scale_color_manual to change the colors
myColors <- c(brewer.pal(3, "Dark2"), "black")
ggplot(mtcars, aes(x = wt, y = mpg, col = factor(cyl))) +
  geom_point() +
  stat_smooth(method = "lm", se = FALSE, span = 0.7) +
  stat_smooth(method = "loess", 
              aes(group = 1, col="All"), 
              se = FALSE, span = 0.7) +
  # Add correct arguments to scale_color_manual
  scale_color_manual("Cylinders", values = myColors)
```

 Modifying stat_smooth (2)

In this exercise we'll take a look at a more subtle example of defining and using linear models. `ggplot2` and the `Vocab` data frame are already loaded for you.

##### Instructions

100 XP

- Plot 1: This code produces a jittered plot of `vocabulary` against `education`, variables from the `Vocab` data frame.

  - Add a [`stat_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth) layer with `method` set to `"lm"`. Hide the CI ribbons by using `se = FALSE`.

- Plot 2: Color by year. 

  - Specify the `col = year` aesthetic to the nested `ggplot(aes())` function.
  - To see why this works, try using only `col = year`, and adding points.

- Plot 3: Linear model for each year.

  - We need to specify `year` as a factor variable if we want to use it as a grouping variable for our linear models. Add the `col = factor(year)` aesthetic to the nested `ggplot(aes())` function.

- Plot 4: Years are ordered, so use a sequential color palette.

  - Add [`scale_color_brewer()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_brewer).
  - Don't add any arguments here. This results in a warning message, since the default palette, `"Blues"`, only has 9 colors. Since we have 16 years, this is not a complete solution!

- Plot 5: To get the proper colors, we can use `col = year`, because the variable `year` is type `integer` and we want a continuous scale. However, we'll need to specify the invisible `group` aesthetic so that our linear models are still calculated appropriately. The scale layer, `scale_color_gradientn()`, has been provided for you - this allows us to map a continuous variable onto a colour scale.

  - Add `group = factor(year)` inside [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes).

  - Inside [`stat_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth), set `alpha = 0.6` and `size = 2`.

    ```R
    # Plot 1: Jittered scatter plot, add a linear model (lm) smooth
    ggplot(Vocab, aes(x = education, y = vocabulary)) +
      geom_jitter(alpha = 0.2) +
      stat_smooth(method = "lm", se = FALSE) # smooth
    
    # Plot 2: points, colored by year
    ggplot(Vocab, aes(x = education, y = vocabulary, col = year)) +
      geom_jitter(alpha = 0.2)
      
    # Plot 3: lm, colored by year
    ggplot(Vocab, aes(x = education, y = vocabulary, col = factor(year))) +
      stat_smooth(method = "lm", se = FALSE) # smooth
    
    # Plot 4: Set a color brewer palette
    ggplot(Vocab, aes(x = education, y = vocabulary, col = factor(year))) +
      stat_smooth(method = "lm", se = FALSE) +  # smooth
      scale_color_brewer()  # colors
    
    # Plot 5: Add the group aes, specify alpha and size
    ggplot(Vocab, aes(x = education, y = vocabulary, col = year, group = factor(year))) +
      stat_smooth(method = "lm", se = FALSE, alpha = 0.6, size = 2) +
      scale_color_gradientn(colors = brewer.pal(9, "YlOrRd"))
    ```

    # Quantiles

    The previous example used the `Vocab` dataset and applied linear models describing `vocabulary` by `education` for different `years`. Here we'll continue with that example by using [`stat_quantile()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_quantile) to apply a quantile regression (method `rq`).

    By default, the 1st, 2nd (i.e. median), and 3rd quartiles are modeled as a response to the predictor variable, in this case `education`. Specific quantiles can be specified with the `quantiles` argument.

    If you want to specify many quantile *and* color according to year, then things get too busy. We'll explore ways of dealing with this in the next chapter.

    ##### Instructions

    100 XP

    The code from the previous exercise, with the linear model and a suitable color palette, is already shown. 

    - Update the plotting code.
      - Change the stat function from [`stat_smooth()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_smooth) to [`stat_quantile()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_quantile). 
      - Get rid of all the arguments except `alpha` and `size`.
    - The resulting plot will be a mess, because there are three quartiles drawn by default. 
      - Copy the code for the previous instruction.
      - Set the `quantiles` argument to `0.5` so that only the median is shown.

# Sum

Another useful stat function is [`stat_sum()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_count). This function calculates the total number of overlapping observations and is another good alternative to overplotting.

##### Instructions

100 XP

`ggplot2` is already loaded. A plot showing jittered points is already provided and stored as `p`. 

- Add [`stat_sum()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_count) to this plotting object `p`. This maps the overall `count` of each dot onto `size`. You don't have to set any arguments; the aesthetics will be inherited from the base plot!

- Add the `size` scale with the generic [`scale_size()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_size) function. Use `range` to set the minimum and maximum dot sizes as `c(1,10)`.


```R
# Plot 1: Jittering only
p <- ggplot(Vocab, aes(x = education, y = vocabulary)) +
  geom_jitter(alpha = 0.2)

# Plot 2: Add stat_sum
p +
  stat_sum() # sum statistic

# Plot 3: Set size range
p +
  stat_sum() + # sum statistic
  scale_size(range = c(1, 10)) # set size scale

```

# Preparations

Here we'll look at [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) in action. We'll build up various plots one-by-one.

In this exercise we'll consider the preparations. That means we'll  make sure the data is in the right format and that all the positions  that we might use in our plots are defined. Lastly, we'll set the base  layer for our plot. `ggplot2` is already loaded, so you can get started straight away!

##### Instructions

100 XP

- Explore the structure of the `mtcars` dataset by executing `str(mtcars)`.

- In `mtcars`, `cyl` and `am` are classified as continuous, but they are actually categorical. Previously we just used [`factor()`](http://www.rdocumentation.org/packages/base/functions/factor), but here we'll modify the actual dataset. Change `cyl` and `am` to be categorical in the `mtcars` data frame using `as.factor`.

- Next we'll set three position objects with convenient names. This  allows us to use the exact positions on multiple layers. Create:

- `posn.d`, using [`position_dodge()`](http://www.rdocumentation.org/packages/ggplot2/functions/position_dodge) with a `width` of `0.1`,

- `posn.jd`, using [`position_jitterdodge()`](http://www.rdocumentation.org/packages/ggplot2/functions/position_jitterdodge) with a `jitter.width` of `0.1` and a `dodge.width` of `0.2`

- `posn.j`, using [`position_jitter()`](http://www.rdocumentation.org/packages/ggplot2/functions/position_jitter) with a width of `0.2`.

- Finally, we'll make our base layers and store it in the object `wt.cyl.am`. Make the base call for ggplot mapping `cyl` to the `x`, `wt` to `y`, `am` to both `col` *and* `fill`. Also set `group = am` inside [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes). The reason for these redundancies will become clear later on.

  ```R
  # Display structure of mtcars
  str(mtcars)
  
  # Convert cyl and am to factors
  mtcars$cyl <- as.factor(mtcars$cyl)
  mtcars$am <- as.factor(mtcars$am)
  
  # Define positions
  posn.d <- position_dodge(0.1)
  posn.jd <- position_jitterdodge(jitter.width = 0.1, dodge.width = 0.2)
  posn.j <- position_jitter(0.2)
  
  # Base layers
  wt.cyl.am <- ggplot(mtcars, aes(x = cyl,
                                  y = wt,
                                  col = am,
                                  fill = am,
                                  group = am))
  ```

  # Plotting variations

  Now that the preparation work is done, let's have a look at at [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary).

  `ggplot2` is already loaded, as is `wt.cyl.am`, which is defined as

  ```
  wt.cyl.am <- ggplot(mtcars, aes(x = cyl,  y = wt, col = am, fill = am, group = am))
  ```

  Also all the position objects of the previous exercise, `posn.d`, `posn.jd` and `posn.j`, are available. For starters, Plot 1 is already coded for you.

  ##### Instructions

  100 XP

  - Plot 2: Add a [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) layer to `wt.cyl.am` and calculate the mean and standard deviation as we did in the video: set `fun.data` to `mean_sdl` and specify `fun.args` to be  `list(mult = 1)`. Set the `position` argument to `posn.d`.
  - Plot 3: Repeat the previous plot, but use the 95% confidence interval instead of the standard deviation. You can use `mean_cl_normal` instead of `mean_sdl` this time. There's no need to specify `fun.args` in this case. Again, set `position` to `posn.d`.
  - The above plots were simple because they implicitly used a default geom, which is `geom_pointrange()`. For Plot 4, fill in the blanks to calculate the mean and standard deviation separately with two [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) functions:
  - For the mean, use `geom = "point"` and set `fun.y = mean`. This time you should use `fun.y` because the point geom uses the `y` aesthetic behind the scenes.
  - Add error bars with another [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) function. Set `geom = "errorbar"` to get the real "T" tips. Set `fun.data = mean_sdl`.

```R
# wt.cyl.am, posn.d, posn.jd and posn.j are available

# Plot 1: Jittered, dodged scatter plot with transparent points
wt.cyl.am +
  geom_point(position = posn.jd, alpha = 0.6)

# Plot 2: Mean and SD - the easy way
wt.cyl.am +
  geom_point(position = posn.d, alpha = 0.6)+
  stat_summary(fun.data = mean_sdl,fun.args= list(mult = 1),
  position = posn.d)

# Plot 3: Mean and 95% CI - the easy way
wt.cyl.am+
stat_summary(fun.data= mean_cl_normal,position = posn.d)


# Plot 4: Mean and SD - with T-tipped error bars - fill in ___
wt.cyl.am +
  stat_summary(geom = "point", fun.y = mean,
               position = posn.d) +
  stat_summary(geom = "errorbar", fun.data = mean_sdl,
               position = posn.d, fun.args = list(mult = 1), width = 0.1)
```

In the video we saw that the only difference between `ggplot2::mean_sdl()` and `Hmisc::smean.sdl()` is the naming convention. In order to use the results of a function directly in `ggplot2` we need to ensure that the names of the variables match the aesthetics needed for our respective geoms.

Here we'll create two new functions in order to create the plot shown  in the viewer. One function will measure the full range of the dataset  and the other will measure the interquartile range.

A play vector, `xx`, has been created for you. Execute

```
mean_sdl(xx, mult = 1)
```

in the R Console and consider the format of the output. You'll have to produce functions which return similar outputs.

##### Instructions

100 XP

- First, change the arguments `ymin` and `ymax` inside the `data.frame()` call of `gg_range()`.

- `ymin` should be the minimum of `x`

- `ymax` should be the maximum of `x`

  Use `min()` and `max()`. Watch out, naming is important here. `gg_range(xx)` should now generate the required output.

- Next, change the arguments `y`, `ymin` and `ymax` inside the `data.frame()` call of `med_IQR()`.

- `y` should be the median of `x`

- `ymin` should be the first quartile

- `ymax` should be the 3rd quartile.

  You should use `median()` and `quantile()`. For example, `quantile()` can be used as follows to give the first quartile: `quantile(x)[2]`. `med_IQR(xx)` should now generate the required output.

# Custom Functions

In the video we saw that the only difference between `ggplot2::mean_sdl()` and `Hmisc::smean.sdl()` is the naming convention. In order to use the results of a function directly in `ggplot2` we need to ensure that the names of the variables match the aesthetics needed for our respective geoms.

Here we'll create two new functions in order to create the plot shown  in the viewer. One function will measure the full range of the dataset  and the other will measure the interquartile range.

A play vector, `xx`, has been created for you. Execute

```
mean_sdl(xx, mult = 1)
```

in the R Console and consider the format of the output. You'll have to produce functions which return similar outputs.

##### Instructions

100 XP

- First, change the arguments `ymin` and `ymax` inside the `data.frame()` call of `gg_range()`.

- `ymin` should be the minimum of `x`

- `ymax` should be the maximum of `x`

  Use `min()` and `max()`. Watch out, naming is important here. `gg_range(xx)` should now generate the required output.

- Next, change the arguments `y`, `ymin` and `ymax` inside the `data.frame()` call of `med_IQR()`.

- `y` should be the median of `x`

- `ymin` should be the first quartile

- `ymax` should be the 3rd quartile.

  You should use `median()` and `quantile()`. For example, `quantile()` can be used as follows to give the first quartile: `quantile(x)[2]`. `med_IQR(xx)` should now generate the required output.

  ```R
  # Play vector xx is available
  
  # Function to save range for use in ggplot
  gg_range <- function(x) {
    # Change x below to return the instructed values
    data.frame(ymin = min(x), # Min
               ymax = max(x)) # Max
  }
  
  gg_range(xx)
  # Required output
  #   ymin ymax
  # 1    1  100
  
  # Function to Custom function:
  med_IQR <- function(x) {
    # Change x below to return the instructed values
    data.frame(y =  median(x), # Median
               ymin = quantile(x)[2], # 1st quartile
               ymax = quantile(x)[4])  # 3rd quartile
  }
  
  med_IQR(xx)
  # Required output
  #        y  ymin  ymax
  # 25% 50.5 25.75 75.25
  ```

  # Custom Functions (2)

  In the last exercise we created functions that will allow us to plot the so-called *five-number summary* (the minimum, 1st quartile, median, 3rd quartile, and the maximum). Here, we'll implement that into a unique plot type.

  All the functions and objects from the previous exercise are available including the updated `mtcars` data frame, the position object `posn.d`, the base layers `wt.cyl.am` and the functions `med_IQR()` and `gg_range()`.

  The plot you'll end up with at the end of this exercise is shown on the right. When using `stat_summary()` recall that the `fun.data` argument requires a properly labelled 3-element long vector, which we saw in the previous exercises. The `fun.y` argument requires only a 1-element long vector.

  ##### Instructions

  0 XP

  Complete the given [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) functions, don't change the predefined arguments:

  - The first [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) layer should have `geom` set to `"linerange"`. `fun.data` argument should be set to `med_IQR`, the function you used in the previous exercise.

  - The second [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) layer also uses the `"linerange"` geom. This time `fun.data` should be `gg_range`, the other function you created. Also set `alpha = 0.4`.

  - For the last [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) layer, use `geom = "point"`. The points should have `col` `"black"` and `shape` `"X"`.

    ```R
    # The base ggplot command; you don't have to change this
    wt.cyl.am <- ggplot(mtcars, aes(x = cyl,y = wt, col = am, fill = am, group = am))
    
    # Add three stat_summary calls to wt.cyl.am
    wt.cyl.am +
      stat_summary(geom = "linerange", fun.data = med_IQR,
                   position = posn.d, size = 3) +
      stat_summary(geom = "linerange", fun.data = gg_range,
                   position = posn.d, size = 3,
                   alpha = 0.4) +
      stat_summary(geom = "point", fun.y = median,
                   position = posn.d, size = 3,
                   col = "black", shape = "X")
    ```

    # Zooming In

    In  the video, you saw different ways of using the coordinates layer to  zoom in. In this exercise, we'll compare some of the techniques again.

    As usual, you'll be working with the `mtcars` dataset, which is already cleaned up for you (`cyl` and `am` are categorical variables). Also `p`, a ggplot object you coded in the previous chapter, is already available. Execute `p` in the console to check it out.

    ##### Instructions

    100 XP

    - Extend `p` with a [`scale_x_continuous()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_continuous) with `limits = c(3, 6)` and `expand = c(0, 0)`. What do you see?
    - Try again, this time with [`coord_cartesian()`](http://www.rdocumentation.org/packages/ggplot2/functions/coord_cartesian): Set the `xlim` argument equal to `c(3, 6)`. Compare the two plots.

```R
# Basic ggplot() command, coded for you
p <- ggplot(mtcars, aes(x = wt, y = hp, col = am)) + geom_point() + geom_smooth()

# Add scale_x_continuous()
p+
scale_x_continuous(limits = c(3,6),expand = c(0,0))

# Add coord_cartesian(): the proper way to zoom in
p+
coord_cartesian(xlim = c(3,6))

```

# Aspect Ratio

We can set the aspect ratio of a plot with [`coord_fixed()`](http://www.rdocumentation.org/packages/ggplot2/functions/coord_fixed) or [`coord_equal()`](http://www.rdocumentation.org/packages/ggplot2/functions/coord_fixed). Both use `ratio = 1` as a default. A 1:1 aspect ratio is most appropriate when two continuous variables are on the same scale, as with the `iris` dataset.

All variables are measured in centimeters, so it only makes sense  that one unit on the plot should be the same physical distance on each  axis. This gives a more truthful depiction of the relationship between  the two variables since the aspect ratio can change the angle of our  smoothing line. This would give an erroneous impression of the data.

Of course the underlying linear models don't change, but our perception can be influenced by the angle drawn.

##### Instructions

100 XP

- Complete the basic scatter plot function using the `iris` data frame to plot `Sepal.Width` onto the `y` aesthetic, `Sepal.Length` onto the `x` and `Species` onto `col`. You should understand all the other functions used in this plot call by now. This is saved in an object called `base.plot`.

- Write `base.plot` on a new line to print it out. Examine it: the plot is drawn to the dimensions of the graphics device.

- Add a [`coord_equal()`](http://www.rdocumentation.org/packages/ggplot2/functions/coord_fixed) layer to force a 1:1 aspect ratio.

  ```R
  # Complete basic scatter plot function
  base.plot <- ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, col = Species)) +
                 geom_jitter() +
                 geom_smooth(method = "lm", se = FALSE)
  
  # Plot base.plot: default aspect ratio
  base.plot
  # Fix aspect ratio (1:1) of base.plot
  base.plot+
  coord_equal(1:1)
  ```

  # Pie Charts

  The [`coord_polar()`](http://www.rdocumentation.org/packages/ggplot2/functions/coord_polar) function converts a planar x-y Cartesian plot to polar coordinates. This can be useful if you are producing pie charts. 

  We can imagine two forms for pie charts - the typical filled circle, or a colored ring.

  As an example, consider the stacked bar chart shown in the viewer.  Imagine that we just take the y axis on the left and bend it until it  loops back on itself, while expanding the right side as we go along.  We'd end up with a pie chart - it's simply a bar chart transformed onto a  polar coordinate system. 

  Typical pie charts omit all of the non-data ink, which we'll learn  about in the next chapter. Pie charts are not really better than stacked  bar charts, but we'll come back to this point in the fourth chapter on  best practices.

  The `mtcars` data frame is available, with `cyl` converted to a factor for you.

  ##### Instructions

  100 XP

  - Create a basic stacked bar plot. Since we have univariate data and [`stat_bin()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram) requires an `x` aesthetic, we'll have to use a dummy variable. Set `x` to `1` and map `cyl` onto `fill`. Assign the bar plot to `wide.bar`.
  - Add a [`coord_polar()`](http://www.rdocumentation.org/packages/ggplot2/functions/coord_polar) layer to `wide.bar`. Set the argument `theta` to `"y"`. This specifies the axis which would be transformed to polar coordinates.
  - Repeat the code for the stacked bar plot, but this time:
    - Set the `width` argument inside the [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar) function to `0.1` and
    - Use `scale_x_continuous()` to set the `limits` argument to `c(0.5,1.5))`. These two steps will add empty space aroung the bar on the x axis.
    - Assign this plot to `thin.bar`.
  - Add a [`coord_polar()`](http://www.rdocumentation.org/packages/ggplot2/functions/coord_polar) layer to `thin.bar`, as you did before. There's a ring structure instead of a pie!

```R
# Create a stacked bar plot: wide.bar
wide.bar <- ggplot(mtcars, aes(x = 1, fill = cyl)) +
              geom_bar()

# Convert wide.bar to pie chart
wide.bar +
  coord_polar(theta = "y")

# Create stacked bar plot: thin.bar
thin.bar <- ggplot(mtcars, aes(x = 1, fill = cyl)) +
              geom_bar(width = .1) +
              scale_x_continuous(limits = c(0.5,1.5))

# Convert thin.bar to "ring" type pie chart
thin.bar +
  coord_polar(theta = "y")
```

# Facets: the basics

The most straightforward way of using facets is [`facet_grid()`](http://www.rdocumentation.org/packages/ggplot2/functions/facet_grid). Here we just need to specify the categorical variable to use on rows and columns using standard R formula notation (`rows ~ columns`).

Notice that we can also take advantage of ordinal variables by  positioning them in the correct order as columns or rows, as is the case  with the number of cylinders. Get some hands-on practice in this  exercise; `ggplot2` is already loaded for you and `mtcars` is available. The variables `cyl` and `am` are factors. However, this is not necessary for facets; ggplot2 will coerce variables to factors in this case.

##### Instructions

100 XP

Starting from the basic scatter plot, use [`facet_grid()`](http://www.rdocumentation.org/packages/ggplot2/functions/facet_grid) and the formula notation to facet the plot in three different ways:

- 1 - Rows by `am`.
- 2 - Columns by `cyl`.
- 3 - Rows and columns by `am` and `cyl`.

Remember, when faceting in only one direction us `.` to specify *nothing* for the unused direction.

```R
# Code to create the cyl_am col and myCol vector
mtcars$cyl_am <- paste(mtcars$cyl, mtcars$am, sep = "_")
myCol <- rbind(brewer.pal(9, "Blues")[c(3,6,8)],
               brewer.pal(9, "Reds")[c(3,6,8)])

# Map cyl_am onto col
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl_am)) +
  geom_point() +
  # Add a manual colour scale
  scale_color_manual(values = myCol)
  
# Grid facet on gear vs. vs
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl_am)) +
  geom_point() +
  scale_color_manual(values = myCol) +
  facet_grid(gear ~ vs)

# Also map disp to size
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl_am, size = disp)) +
  geom_point() +
  scale_color_manual(values = myCol) +
  facet_grid(gear ~ vs)
```

# Dropping levels

When  you have a categorical variable with many levels which are not all  present in each sub-group of another variable, it may be desirable to  drop the unused levels. As an example let's return to the mammalian  sleep dataset, `mamsleep`. It is available in your workspace.

The variables of interest here are `name`, which contains the full popular name of each animal, and `vore`, the eating behavior. Each animal can only be classified under one eating habit, so if we facet according to `vore`, we don't need to repeat the full list in each sub-plot.

##### Instructions

100 XP

- A basic plot, object `p`, is defined for you. `time` is mapped onto the `x`, `name` onto the `y` and `sleep` onto the `col` aesthetics.
- To see the plot execute `p`. 
- Facet `p` by rows according to `vore`. If you look at the resulting plot, you'll notice that there are a lot of lines where no data is available.
- Extend `facet_grid` with `scale = "free_y"` and `space = "free_y"` to leave out rows for which there is no data.

```R
# Basic scatter plot
p <- ggplot(mamsleep, aes(x = time, y = name, col = sleep)) +
  geom_point()
  
# Execute to display plot
p

# Facet rows accoding to vore
p +
facet_grid(vore ~.)

# Specify scale and space arguments to free up rows
p +
  facet_grid(vore ~ ., scale="free_y", space = "free_y")

```

# Rectangles

To understand all the arguments for the themes, you'll modify an existing plot over the next series of exercises.

Here you'll focus on the rectangles of the plotting object `z` that has already been created for you. If you type `z` in the console, you can check it out. The goal is to turn `z` into the plot in the viewer. Do this by following the instructions step by step.

##### Instructions

100 XP

- Plot 1: In the [`theme()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme) function added to `z`, set the `plot.background` argument to `element_rect(fill = myPink)`. `myPink` is already available in the workspace for you.
- Plot 2: Expand your code for Plot 1 by adding a border to the `plot.background`. Do this by adding 2 arguments to the [`element_rect()`](http://www.rdocumentation.org/packages/ggplot2/functions/element_rect) function in `theme()`: `color` and `size`. Set them to `"black"` and `3`, respectively.
- Plot 3: we don't want the plot panels and legend to appear as they are in Plot 2. A short cut is to remove *all* rectangles, as defined in the theme object `no_panels`, and then draw the one we way in the way we want. Copy your `theme()` layer from Plot 2 and add it to `no_panels`.

```R
# Starting point
z

# Plot 1: Change the plot background fill to myPink
z + 
  theme(plot.background = element_rect(fill = myPink))

# Plot 2: Adjust the border to be a black line of size 3
z + 
  theme(plot.background = element_rect(fill = myPink, color = "black", size = 3)) # expanded from plot 1

# Theme to remove all rectangles
no_panels <- theme(rect = element_blank())

# Plot 3: Combine custom themes
z +
  no_panels +
  theme(plot.background = element_rect(fill = myPink, color = "black", size = 3))  # from plot 2Lines
```

# Lines



To change the appearance of lines use the [`element_line()`](http://www.rdocumentation.org/packages/ggplot2/functions/element_line) function. 

The plot you created in the last exercise, with the fancy pink background, is available as the plotting object `z`. Your goal is to produce the plot in the viewer - no grid lines, but red axes and tick marks.

For each of the arguments that specify lines, use [`element_line()`](http://www.rdocumentation.org/packages/ggplot2/functions/element_line) to modify attributes. e.g. `element_line(color = "red")`.

Remember, to remove a non-data element, use `element_blank()`.

##### Instructions

100 XP

Starting with object `z`, add a [`theme()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme) function to:

- remove the grid lines using the `panel.grid` argument.
- add red axis lines using the `axis.line` argument.
- change the tick marks to red using the `axis.ticks` argument, similar to how you specified `axis.line`.

```R
 Starting point
z

# Plot 1: Change the plot background fill to myPink
z + 
  theme(plot.background = element_rect(fill = myPink))

# Plot 2: Adjust the border to be a black line of size 3
z + 
  theme(plot.background = element_rect(fill = myPink, color = "black", size = 3)) # expanded from plot 1

# Theme to remove all rectangles
no_panels <- theme(rect = element_blank())

# Plot 3: Combine custom themes
z +
  no_panels +
  theme(plot.background = element_rect(fill = myPink, color = "black", size = 3))  # from plot 2Lines
```

# Text

Next we can make the text on your plot prettier and easier to spot. You can do this through the [`element_text()`](http://www.rdocumentation.org/packages/ggplot2/functions/element_text) function and by passing the appropriate arguments inside the [`theme()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme) function.

As before, the plot you've created in the previous exercise is available as `z`. The plot you should end up with after successfully completing this exercises is shown in the viewer.

##### Instructions

0 XP

Starting from `z`, add a [`theme()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme) function to:

- Change the appearance of the strip text, that is the text in the facet strips. Specify `strip.text` with [`element_text()`](http://www.rdocumentation.org/packages/ggplot2/functions/element_text). The `size` of the text should be `16`, the `color` should be `myRed`, a color that is predefined for you.
- Change the axis titles. Specify both axes with the `axis.title` argument and use [`element_text()`](http://www.rdocumentation.org/packages/ggplot2/functions/element_text) to set the parameters: `color = myRed`, `hjust = 0` (to put the text in the bottom left corner) and `face = "italic"`.
- Make the axis text black using the `axis.text` argument to do so.



```
# Original plot, color provided
z
myRed

# Extend z with theme() function and 3 args
z +
  theme(strip.text = element_text(size = 16, color = myRed),
        axis.title = element_text(color = myRed, hjust = 0, face = "italic"),
        axis.text = element_text(color = "black"))
```

# Legends

The themes layer also allows you to specify the appearance and location of legends.

The plot you've coded up to now is available as `z`. It's also displayed in the viewer. Solve the instructions and compare the resulting plots with the plot you started with.

##### Instructions

100 XP

- Add a [`theme()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme) function to `z` to change the legend's location. Do this by specifying the `legend.position` argument to be `c(0.85, 0.85)`. This will make the legend appear in the top right of the plot, inside the third facet.
- Instead of a vertical list of legend entries, you might want to have the different entries next to each other. Starting from `z`, add a [`theme()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme) function in which you specify `legend.direction` to be `"horizontal"`.
- You can also change the locations of legends by name: set `legend.position` to `"bottom"`.
- Finally, you can remove the legend entirely, by setting `legend.position` to `"none"`.

```R
# Move legend by position
z +
  theme(legend.position = c(0.85,0.85))

# Change direction
z +
  theme(legend.direction="horizontal")
  
# Change location by name
z +
  theme(legend.position= "bottom")

# Remove legend entirely
z +
  theme(legend.position= "none")
```

# Positions

The  different rectangles of your plot have spacing between them. There's  spacing between the facets, between the axis labels and the plot  rectangle, between the plot rectangle and the entire panel background,  etc. Let's experiment!

The last plot you created in the previous exercise, without a legend, is available as `z`.

##### Instructions

100 XP

- Suppose you want to have more spacing between the different facets. You can control this by specifying `panel.spacing.x` inside a [`theme()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme) function you add to `z`. For the argument value, you should pass a `unit` object. To achieve this, load the `grid` package with [`library()`](http://www.rdocumentation.org/packages/base/functions/library). Next, set `panel.spacing.x` to `unit(2, "cm")`.
- Copy, adapt and paste the plot command for the previous instruction: to adjust the plot margin, set `plot.margin` to `unit(c(1,2,1,1), "cm")` (spacing for top, right, bottom, and left margins).

```R
# Increase spacing between facets
z+
theme(panel.spacing.x = unit(2,"cm"))
library(grid)

# Adjust the plot margin
z+
theme(panel.spacing.x = unit(2,"cm"),
      plot.margin = unit(c(1,2,1,1),"cm"))

```

# Updating Themes

Building  your themes every time from scratch can become a pain and unnecessarily  bloat your scripts. In the following exercises, we'll practice  different ways of managing, updating and saving themes.

A plot object `z2` is already created for you on the right. It shows `mpg` against `wt` for the `mtcars` dataset, faceted according to `cyl`. Also the colors `myPink` and `myRed`  are available. In the previous exercises you've already customized the  rectangles, lines and text on the plot. This theme layer is now  separately stored as `theme_pink`, as shown in the sample code.

[`theme_update()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme_update) updates the default theme used by `ggplot2`. The arguments for [`theme_update()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme_update) are the same as for [`theme()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme). When you call [`theme_update()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme_update) and assign it to an object (e.g. called `old`), that object stores the *current* default theme, and the arguments *update* the default theme. If you want to restore the previous default theme, you can get it back by using [`theme_update()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme_update) again. Let's see how:

##### Instructions

100 XP

- 1 - "Apply" `theme_pink` to `z2` to carry out all customizations.
- 2 - Instead of applying `theme_pink`, use  [`theme_update()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme_update).  This function returns an object that contains the previous theme  settings, so that you can restore it later. Assign the output of [`theme_update()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme_update) to an object called `old`.
- 3 - Plot `z2` again, after the [`theme_update()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme_update) call. The resulting plot has the same appearance as the previous one - but now you don't need to call `theme()` explictly.
- 4 - Restore the old theme using `theme_set(old)` and plot `z2` again. It's back to the original default theme.

```R
# Original plot
z2

# Theme layer saved as an object, theme_pink
theme_pink <- theme(panel.background = element_blank(),
                    legend.key = element_blank(),
                    legend.background = element_blank(),
                    strip.background = element_blank(),
                    plot.background = element_rect(fill = myPink, color = "black", size = 3),
                    panel.grid = element_blank(),
                    axis.line = element_line(color = "red"),
                    axis.ticks = element_line(color = "red"),
                    strip.text = element_text(size = 16, color = myRed),
                    axis.title.y = element_text(color = myRed, hjust = 0, face = "italic"),
                    axis.title.x = element_text(color = myRed, hjust = 0, face = "italic"),
                    axis.text = element_text(color = "black"),
                    legend.position = "none")
  
# 1 - Apply theme_pink to z2
z2 + 
  theme_pink

# 2 - Update the default theme, and at the same time
# assign the old theme to the object old.
old <- theme_update(panel.background = element_blank(),
             legend.key = element_blank(),
             legend.background = element_blank(),
             strip.background = element_blank(),
             plot.background = element_rect(fill = myPink, color = "black", size = 3),
             panel.grid = element_blank(),
             axis.line = element_line(color = "red"),
             axis.ticks = element_line(color = "red"),
             strip.text = element_text(size = 16, color = myRed),
             axis.title.y = element_text(color = myRed, hjust = 0, face = "italic"),
             axis.title.x = element_text(color = myRed, hjust = 0, face = "italic"),
             axis.text = element_text(color = "black"),
             legend.position = "none")

# 3 - Display the plot z2 - new default theme used
z2

# 4 - Restore the old default theme
theme_set(old)

# Display the plot z2 - old theme restored
z2
```

# Exploring ggthemes

There are many themes available by default in `ggplot2`: [`theme_bw()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggtheme), [`theme_classic()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggtheme), [`theme_gray()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggtheme), etc. In the previous exercise, you saw that you can apply these themes to all following plots, with [`theme_set()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme_set):

```
theme_set(theme_bw())
```

But you can also apply them on an individual plot, with:

```
... + theme_bw()
```

You can also extend these themes with your own modifications. In this  exercise, you'll experiment with this and use some preset templates  available from the `ggthemes` package. The workspace already contains the same basic plot from before under the name `z2`.

##### Instructions

100 XP

- Create a custom theme, assigning it to `custom_theme`.
- Call [`theme_tufte()`](http://www.rdocumentation.org/packages/ggthemes/functions/theme_tufte) with no arguments.
- Add a call to [`theme()`](http://www.rdocumentation.org/packages/ggplot2/functions/theme) as follows.
- Set `legend.position` to `c(0.9, 0.9)`.
- Set `legend.title` to an `"italic"` text of size `12`. Use `element_text(face = ___, size = ___)`.
- Set `axis.title` to a `"bold"` text of size `14`. Use `element_text(face = ___, size = ___)`.
- Plot `z2` with the customized theme. (You don't need parentheses.)
- Make `custom_theme` the default by calling [`theme_set()`](https://www.rdocumentation.org/packages/ggplot2/topics/theme_get).
- Plot `z2` again.

```R
# Original plot
z2

# Load ggthemes
library(ggthemes)

# Apply theme_tufte, plot additional modifications
custom_theme <- theme_tufte() +
  theme(legend.position = c(0.9, 0.9),
        legend.title = element_text(face = "italic", size = 12),
        axis.title = element_text(face = "bold", size = 14))

# Draw the customized plot
z2 + custom_theme
 
# Use theme set to set custom theme as default
theme_set(custom_theme)

# Plot z2 again
z2
```

# Bar Plots (2)

In the previous exercise we used the `mtcars` dataset to draw a dynamite plot about the weight of the cars per cylinder type.

In this exercise we will add a distinction between transmission type, `am`, for the dynamite plots.

##### Instructions

100 XP

- Update `m` so that we split the bars according to transmission type, `am`. Note that for bar plots, we want to change the `col` as well as the `fill`.
- Plot 1 is already coded for you, but it is not optimal. Let's fix that in the following instructions.
- Plot 2: copy the code for Plot 1 and set the position to `"dodge"` - this also doesn't work, because the default dodging is different for the different [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) functions.
- Plot 3: copy the code for Plot 2 and set the position to the object `posn.d`, which defines a dodge position using `position_dodge(0.9)`.

```
# Base layers
m <- ggplot(mtcars, aes(x = cyl,y = wt, col = am, fill = am))

# Plot 1: Draw dynamite plot
m +
  stat_summary(fun.y = mean, geom = "bar") +
  stat_summary(fun.data = mean_sdl, fun.args = list(mult = 1), geom = "errorbar", width = 0.1)

# Plot 2: Set position dodge in m +
  m+
  stat_summary(fun.y = mean, geom = "bar", position = "dodge") +
  stat_summary(fun.data = mean_sdl, fun.args = list(mult = 1), 
               geom = "errorbar", width = 0.1, position = "dodge")


# Set your dodge posn manually
posn.d <- position_dodge(0.9)

# Plot 3: Redraw dynamite plot
m +
  stat_summary(fun.y = mean, geom = "bar", position = posn.d) +
  stat_summary(fun.data = mean_sdl, fun.args = list(mult = 1), geom = "errorbar", width = 0.1, position = posn.d)
```

# Bar Plots (3)

If it *is* appropriate to use bar plots (see the video for a discussion!), then it would also be nice to give an impression of the number of values in each group.

`stat_summary()` doesn't keep track of the count. [`stat_sum()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_count) does (that's the whole point), but it's difficult to access. In this case, the most straightforward thing to do is calculate exactly what we want to plot beforehand. For this exercise we've created a summary data frame called `mtcars.cyl` which contains the average (`wt.avg`), standard deviations (`sd`) and count (`n`) of car weights, according to cylinders, `cyl`. It also contains the proportion (`prop`) of each cylinder represented in the entire dataset. Use the console to familiarize yourself with the `mtcars.cyl` data frame.

##### Instructions

100 XP

##### Instructions

100 XP

- Establish the base layers. Use the `mtcars.cyl` dataset and map `cyl` onto `x` and `wt.avg` onto `y`. Call the resulting `ggplot` object `m`.

- Plot 1: Starting from `m`

- Add a [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar) layer

- In this [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar), set the attribute `stat` to `"identity"` and the attribute `fill` to `"skyblue"`.

- Plot 2: `geom_col()` is a shortcut for `geom_bar(stat = "identity")`, for when your data already has counts.

- Add a [`geom_col()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_col) layer. This time just specify the `fill` argument as above. The result should be the same, but here we don't have to specify the `stat` argument.

- Plot 3: Starting from Plot 2,

- Add the argument `width = mtcars.cyl$prop` inside the [`geom_col()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar)layer. `mtcars.cyl$prop` is a column that represents the proportion of each group.

- Plot 4: Starting from Plot 3,

- Add error bars to create a *dynamite* plot using [`geom_errorbar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_linerange)

- Inside [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) of this [`geom_errorbar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_linerange) layer, specify: `ymin = wt.avg - sd` and `ymax = wt.avg + sd`.

- Inside [`geom_errorbar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_linerange), but outside its [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes), set the `width = 0.1` to control the width of the error bars.

  ```R
  # Base layers
  m <- ggplot(mtcars.cyl, aes(x =cyl, y = wt.avg))
  
  # Plot 1: Draw bar plot with geom_bar
  m + geom_bar(stat ="identity", fill = "skyblue")
  
  # Plot 2: Draw bar plot with geom_col
  m + geom_col(stat = "identity",)+
  geom_col(fill="skyblue")
  # Plot 3: geom_col with variable widths.
  m + geom_col(width = mtcars.cyl$prop, fill = "skyblue")
   
  # Plot 4: Add error bars
  m + 
    geom_col(width = mtcars.cyl$prop, fill = "skyblue") +
    geom_errorbar(aes(ymin = wt.avg - sd, ymax= wt.avg + sd), width = 0.1 )
  ```

# Pie Charts (1)

In this example we're going to consider a typical use of pie charts - a categorical variable as the proportion of another categorical variable. For example, the proportion of each transmission type `am`, in each cylinder, `cyl` class.

The first plotting function in the editor should be familiar to you by now. It's a straightforward bar chart with `position = "fill"`, as shown in the viewer. This is already a good solution to the problem at hand! Let's take it one step further and convert this plot in a pie chart.

##### Instructions

100 XP

Adapt the code for the bar chart in the editor to turn it into a good looking pie chart:

- Transform the bar plot into a facetted plot: add a [`facet_grid()`](http://www.rdocumentation.org/packages/ggplot2/functions/facet_grid) call to split columns by `cyl`. Remember to use formula notation here `ROW ~ COL`.

- For the moment, each facet will only have one category because `cyl` is also mapped onto `x`. Use a dummy aesthetic for the `x`. Change the [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes)function such that `factor(1)` maps onto `x`.

- Add a [`coord_polar()`](http://www.rdocumentation.org/packages/ggplot2/functions/coord_polar) call where you specify the `theta` to `"y"`.

- This is already pretty good, but to remove all non-data ink add a `theme_void()` layer. (This is the first time we've seen this theme, but you should be familiar with themes already).

- There's a small hole in the center of the pies. Inside [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar) set `width = 1` so that the bars fill up the entire width resulting in a full pie chart.

  ```R
  # Bar chart
  ggplot(mtcars, aes(x = cyl, fill = am)) +
    geom_bar(position = "fill")
  
  # Convert bar chart to pie chart
  ggplot(mtcars, aes(x = (factor(1)), fill = am)) +
    geom_bar(position = "fill") +
    facet_grid(. ~ cyl) + # Facets
    coord_polar( theta = "y") + # Coordinates
    theme_void() # theme
    
  ```

  # Pie Charts (2)

  In the previous example, we looked at one categorical variable (`am`) as a proportion of another (`cyl`). Here, we're interested in two or more categorical variables, independent of each other. The many pie charts in the viewer is an unsatisfactory visualization. We're interested in the relationship between all these variables (e.g. where are 8 cylinder cars represented on the Transmission, Gear and Carburetor variables?) Perhaps we also want continuous variables, such as weight. How can we combine all this information?

  The trick is to use a parallel coordinates plot, like [this one](https://s3.amazonaws.com/assets.datacamp.com/course/ggplot2/course_2/parallelcoord.png). Each variable is plotted on its own *parallel* axis. Individual observations are connected with lines, colored according to a variable of interest. This is a surprisingly useful visualization since we can combine *many* variables, even if they are on entirely different scales.

  A word of caution though: typically it is very taboo to draw lines in this way. It's the reason why we don't draw lines across levels of a nominal variable - the order, and thus the slope of the line, is meaningless. Parallel plots are a (very useful) exception to the rule!

  ##### Instructions

  100 XP

  - `am` is variable `9` in the `mtcars` data frame. Assign this number to `group_by_am`. The object `my_names_am` will contain a numeric vector from 1 - 11 excluding the column with am. These will be our parallel axes.

  - Fill in the [`ggparcoord()`](http://www.rdocumentation.org/packages/GGally/functions/ggparcoord) function.

  - The first argument is the data frame you're using. `mtcars` in our case.

  - The second argument is the number of the columns to plot (use `my_names_am`),

  - `groupColumn` specifies the column number of the grouping variable (use `group_by_am`)

  - `alpha`, the opacity, should be set to `0.8`

    ```
    # Parallel coordinates plot using GGally
    library(GGally)
    # All columns except am
    group_by_am <- 9
    my_names_am <- (1:11)[-group_by_am]
    
    # Basic parallel plot - each variable plotted as a z-score transformation
    ggparcoord(mtcars, my_names_am, groupColumn = group_by_am, alpha = 0.8)
    ```

    # Heat Maps

    In the video you saw reasons for not using heat maps. Nonetheless, you may encounter a case in which you really do want to use one. Luckily, they're fairly straightforward to produce in `ggplot2`.

    We begin by specifying two categorical variables for the `x` and `y` aesthetics. At the intersection of each category we'll draw a box, except here we call it a tile, using the [`geom_tile()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_tile) layer. Then we will fill each tile with a continuous variable.

    We'll produce the heat map we saw in the video with the built-in `barley`dataset. The `barley` dataset is in the `lattice` package and has already been loaded for you. Begin by exploring the structure of the data in the console using [`str()`](http://www.rdocumentation.org/packages/utils/functions/str).

    ##### Instructions

    100 XP

    ##### Instructions

    100 XP

    Reproduce the heat map shown in the viewer in different steps:

    - Define the data and the aesthetics layer. Using the `barley` dataset, map `year` onto `x`, `variety` onto `y` and `fill` according to `yield`

    - Add a [`geom_tile()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_tile) to build the heat maps.

    - So far the entire dataset is plotted on one heat map. Add a [`facet_wrap()`](http://www.rdocumentation.org/packages/ggplot2/functions/facet_wrap)function to get a facetted plot. Use the formula `~ site` (without the dot!) and set `ncol = 1`. By default, the names of the farms will be above the panels, not to the side (as we get with `facet_grid()`).

    - [`brewer.pal()`](http://www.rdocumentation.org/packages/RColorBrewer/functions/ColorBrewer) from the `RColorBrewer` package has been used to create a `"Reds"` color palette. The hexadecimal color codes are stored in the `myColors` object. Add the [`scale_fill_gradientn()`](http://www.rdocumentation.org/packages/ggplot2/functions/scale_gradient) function and specify the `colors` argument correctly to give the heat maps a reddish look.

      ```R
      # Create color palette
      myColors <- brewer.pal(9, "Reds")
      
      # Build the heat map from scratch
      ggplot(barley, aes(x = year, y = variety,fill = yield)) +
        geom_tile() + # Geom layer
        facet_wrap( ~ site, ncol = 1) + # Facet layer
        scale_fill_gradientn(colors= myColors) # Adjust colors
      ```

      # Heat Maps Alternatives (1)

      There are several alternatives to heat maps. The best choice really depends on the data and the story you want to tell with this data. If there is a time component, the most obvious choice is a line plot like what we see in the viewer. Can you come up with the correct commands to create a similar looking plot?

      The `barley` dataset is already available in the workspace. Feel free to check out its structure before you start!

      ##### Instructions

      100 XP

      - The line plot might be a good alternative:
      - Base layer: same dataset, map `year` onto `x`, `yield` onto `y` and `variety` onto `col` as well as onto `group`!
      - Add the appropriate geom for this **line** plot; no additional arguments are needed.
      - Add facetting with the same formula as in the heat map plot, instead of `ncol`, set `nrow` to `1`.

    - ```R
      # The heat map we want to replace
      # Don't remove, it's here to help you!
      myColors <- brewer.pal(9, "Reds")
      ggplot(barley, aes(x = year, y = variety, fill = yield)) +
        geom_tile() +
        facet_wrap( ~ site, ncol = 1) +
        scale_fill_gradientn(colors = myColors)
      
      # Line plot; set the aes, geom and facet
      ggplot(barley, aes(x = year, y = yield, color = variety, group = variety)) + 
        geom_line() +
        facet_wrap( ~ site, nrow = 1)
      ```

    - # Heat Maps Alternatives (2)

    - In the videos we saw two methods for depicting overlapping measurements of spread. You can use dodged error bars or you can use overlapping transparent ribbons (shown in the viewer). In this exercise we'll try to recreate the second option, the transparent ribbons.

    - The `barley` dataset is available. You can use `str(barley)` to refresh its structure before heading over to the instructions.

    - ##### Instructions

    - 100 XP

    - ##### Instructions

    - 100 XP

    - Create a plot, similar to the one in the viewer, from scratch by following these steps:

    - - Base layer: use the `barley` dataset. Try to come up with the correct mappings for `x`, `y`, `col`, `group` and `fill`.
      - Add a [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) function for the mean. Specify `fun.y` to be `mean` and set `geom` to `"line"`.
      - Add a [`stat_summary()`](http://www.rdocumentation.org/packages/ggplot2/functions/stat_summary) function for the ribbons. Set `fun.data = mean_sdl` and `fun.args = list(mult = 1)` to have a ribbon that spans over one standard deviation in both directions. Use `geom = "ribbon"` and set `col = NA` and `alpha = 0.1`.

  - ```R
    # Create overlapping ribbon plot from scratch
    ggplot(barley, aes(x = year, y = yield, col = site, group = site, fill = site)) +
      stat_summary(fun.y = mean, geom = "line") +
      stat_summary(fun.data = mean_sdl, fun.args = list(mult = 1), geom = "ribbon", alpha = 0.1, col = NA)
    ```

     Exploring Data

    In  this chapter we're going to continuously build on our plotting  functions and understanding to produce a mosaic plot (aka Marimekko  plot). This is a visual representation of a contingency table, comparing  two categorical variables. Essentially, our question is which groups  are over or under represented in our dataset. To visualize this we'll  color groups according to their Pearson residuals from a chi-squared  test. At the end of it all we'll wrap up our script into a flexible  function so that we can look at other variables.

    We'll familiarize ourselves with a small number of variables from the  2009 CHIS adult-response dataset (as opposed to children). We have  selected the following variables to explore:

    - `RBMI`: BMI Category description
    - `BMI_P`: BMI value
    - `RACEHPR2`: race
    - `SRSEX`: sex
    - `SRAGE_P`: age
    - `MARIT2`: Marital status
    - `AB1`: General Health Condition
    - `ASTCUR`: Current Asthma Status
    - `AB51`: Type I or Type II Diabetes
    - `POVLL`: Poverty level

    We'll filter our dataset to plot a more reliable subset (we'll still retain over 95% of the data).

    Before we get into mosaic plots it's worthwhile exploring the dataset using simple distribution plots - i.e. histograms.

    `ggplot2` is already loaded and the dataset, named `adult`, is already available in the workspace.

    ##### Instructions

    100 XP

    - Use the typical commands for exploring the structure of `adult` to get familiar with the variables: [`summary()`](http://www.rdocumentation.org/packages/base/functions/summary) and [`str()`](http://www.rdocumentation.org/packages/utils/functions/str).
    - As a first exploration of the data, plot two histograms using `ggplot2` syntax: one for age (`SRAGE_P`) and one for BMI (`BMI_P`).  The goal is to explore the dataset and get familiar with the  distributions here. Feel free to explore different bin widths. We'll ask  some questions about these in the next exercises.
    - Next plot a binned-distribution of age, filling each bar according to the BMI categorization. Inside [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram), set `binwidth = 1`. You'll want to use [`fill = factor(RBMI)`](http://www.rdocumentation.org/packages/base/functions/factor) since `RBMI` is a categorical variable.

    - 

```R
# Explore the dataset with summary and str
str(adult)
summary(adult)


# Age histogram
ggplot(adult ,aes(x = SRAGE_P))+
geom_histogram()


# BMI value histogram
ggplot(adult,aes(x = BMI_P))+
geom_histogram()


# Age colored by BMI, binwidth = 1
ggplot(data= adult,mapping = aes(x = SRAGE_P,fill = factor(RBMI)))+
geom_histogram(binwidth = 1)
```

# Data Cleaning

Now that we have an idea about our data, let's clean it up.

##### Instructions

100 XP

- You should have noticed in the age distribution that there is an  unusual spike of individuals at 85, which seems like an artifact of data  collection and storage. Solve this by only keeping observations for  which `adult$SRAGE_P` is smaller than or equal to `84`.
- There is a long positive tail on the BMIs that we'd like to remove. Only keep observations for which `adult$BMI_P` is larger than or equal to `16` and `adult$BMI_P` is strictly smaller than `52`.
- We'll focus on the relationship between the BMI score (&  category), age and race. To make plotting easier later on, we'll change  the labels in the dataset. Define `adult$RACEHPR2` as a factor with labels `c("Latino", "Asian", "African American", "White")`. Do the same for `adult$RBMI`, using the labels `c("Under-weight", "Normal-weight", "Over-weight", "Obese")`.

```R
# Keep adults younger than or equal to 84
adult <- adult[adult$SRAGE_P <= 84, ] 

# Keep adults with BMI at least 16 and less than 52
adult <- adult[adult$BMI_P >=  16 & adult$BMI_P < 52, ]

# Relabel the race variable
adult$RACEHPR2 <- factor(adult$RACEHPR2, labels = c("Latino", "Asian", "African American", "White"))

# Relabel the BMI categories variable
adult$RBMI <- factor(adult$RBMI, labels = c("Under-weight", "Normal-weight", "Over-weight", "Obese"))
```

  	Multiple Histograms

When  we introduced histograms we focused on univariate data, which is  exactly what we've been doing here. However, when we want to explore  distributions further there is much more we can do. For example, there  are density plots, which you'll explore in the next course. For now,  we'll look deeper at frequency histograms and begin developing our  mosaic plots.

The `adult` dataset, which is cleaned up by now, is available in the workspace for you.

Two layers have been pre-defined for you: `BMI_fill` is a scale layer which we can add to a `ggplot()` command using `+`: `ggplot(...) + BMI_fill`. `fix_strips` is a `theme()` layer to make nice facet titles.

##### Instructions

100 XP

- The histogram from the first exercise of age colored by BMI has been provided. The predefined `theme()`, `fix_strips` (see above), has been added to the histogram. Add `BMI_fill` to this plot using the `+` operator as well.

- In addition, add the following elements to create a pretty & insightful plot:

- Use [`facet_grid()`](http://www.rdocumentation.org/packages/ggplot2/functions/facet_grid) to facet the rows according to `RBMI` (Remember formula notation `ROWS ~ COL` and use `.` as a place-holder when not facetting in that direction).

- Add the classic theme using [`theme_classic()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggtheme).

  ```
  # The color scale used in the plot
  BMI_fill <- scale_fill_brewer("BMI Category", palette = "Reds")
  
  # Theme to fix category display in faceted plot
  fix_strips <- theme(strip.text.y = element_text(angle = 0, hjust = 0, vjust = 0.1, size = 14),
                      strip.background = element_blank(),
                      legend.position = "none")
  
  # Histogram, add BMI_fill and customizations
  ggplot(adult, aes (x = SRAGE_P, fill= RBMI)) + 
    geom_histogram(binwidth = 1) +
    fix_strips+
    BMI_fill+
    facet_grid(RBMI ~.)+
    theme_classic()
  ```

  In  the previous exercise we looked at different ways of showing the  absolute count of multiple histograms. This is fine, but density would  be a more useful measure if we wanted to see how the frequency of one  variable changes across another. However, there are some difficulties  here, so let's take a closer look at different plots.

  The clean `adult` dataset is available, as is the `BMI_fill` color palette. The first plot simply shows a histogram of counts, without facets, without modified themes. It's denoted `Plot 1`.

  ##### Instructions

  100 XP

  - Plot 2 - Copy, paste and adapt the code for plot 1 so that it shows density. Do this by adding `aes(y = ..density..)` inside the [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram) function. This plot looks really strange, because we get the density within each BMI category, not within each age group!
  - Plot 3 - starting from plot 1, create a faceted histogram. Use `facet_grid()` with the formula: `RBMI ~ .`.
  - Plot 4 - starting from plot 2, create a faceted histogram showing density. Use `facet_grid()` with the formula `RBMI ~ .`. Plots 3 and 4 can be useful if we are interested in the frequency distribution *within* each BMI category.
  - Plot 5 - Change the second plot to have `position = "fill"`. This is not an accurate representation, as density calculates the proportion across *category*, and not across *bin*.
  - Plot 6 - To get an accurate visualization, change Plot 5, but this time, instead of `..density..`, set the `y` aesthetic to `..count../sum(..count..)`.

```

```

n  the previous exercise we looked at different ways of showing the  absolute count of multiple histograms. This is fine, but density would  be a more useful measure if we wanted to see how the frequency of one  variable changes across another. However, there are some difficulties  here, so let's take a closer look at different plots.

The clean `adult` dataset is available, as is the `BMI_fill` color palette. The first plot simply shows a histogram of counts, without facets, without modified themes. It's denoted `Plot 1`.

##### Instructions

100 XP

- Plot 2 - Copy, paste and adapt the code for plot 1 so that it shows density. Do this by adding `aes(y = ..density..)` inside the [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram) function. This plot looks really strange, because we get the density within each BMI category, not within each age group!

- Plot 3 - starting from plot 1, create a faceted histogram. Use `facet_grid()` with the formula: `RBMI ~ .`.

- Plot 4 - starting from plot 2, create a faceted histogram showing density. Use `facet_grid()` with the formula `RBMI ~ .`. Plots 3 and 4 can be useful if we are interested in the frequency distribution *within* each BMI category.

- Plot 5 - Change the second plot to have `position = "fill"`. This is not an accurate representation, as density calculates the proportion across *category*, and not across *bin*.

- Plot 6 - To get an accurate visualization, change Plot 5, but this time, instead of `..density..`, set the `y` aesthetic to `..count../sum(..count..)

  ```R
  # Plot 1 - Count histogram
  ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) +
    geom_histogram(binwidth = 1) +
    BMI_fill
  
  # Plot 2 - Density histogram
  ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) +
    geom_histogram(aes(y = ..density..), binwidth = 1) +
    BMI_fill
  
  # Plot 3 - Faceted count histogram
  ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) +
    geom_histogram(binwidth = 1) +
    BMI_fill +
    facet_grid(RBMI ~ .)
  
  # Plot 4 - Faceted density histogram
  ggplot(adult, aes(x = SRAGE_P, fill= factor(RBMI))) +
    geom_histogram(aes(y = ..density..), binwidth = 1) +
    BMI_fill +
    facet_grid(RBMI ~ .)
  
  # Plot 5 - Density histogram with position = "fill"
  ggplot(adult, aes(x = SRAGE_P, fill= factor(RBMI))) +
    geom_histogram(aes(y = ..density..), binwidth = 1, position = "fill") +
    BMI_fill
  
  # Plot 6 - The accurate histogram
  ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) +
    geom_histogram(aes(y = ..count../sum(..count..)), binwidth = 1, position = "fill") +
    BMI_fill
  ```

# Do Things Manually

In  the previous exercise we looked at how to produce a frequency histogram  when we have many sub-categories. The problem here is that this can't  be facetted because the calculations occur on the fly inside ggplot2.

To overcome this we're going to calculate the proportions *outside* ggplot2. This is the beginning of our flexible script for a mosaic plot.

The dataset `adult` and the `BMI_fill` object  from the previous exercise have been carried over for you. Code that  tries to make the accurate frequency histogram facetted is available.  You should understand these commands by now.

##### Instructions

100 XP

- Use `adult$RBMI` and `adult$SRAGE_P` as arguments in [`table()`](http://www.rdocumentation.org/packages/base/functions/table) to create a contingency table of the two variables. Save this as `DF`.
- Use [`apply()`](http://www.rdocumentation.org/packages/base/functions/apply) To get the frequency of each group. The first argument is `DF`, the second argument `2`, because you want to do calculations on each column. The third argument should be `function(x) x/sum(x)`. Store the result as `DF_freq`.
- Load the `reshape2` package and use the [`melt()`](https://www.rdocumentation.org/packages/reshape2/versions/1.4.2/topics/melt) function on `DF_freq`. Store the result as `DF_melted`. Examine the structure of `DF_freq` and `DF_melted` if you are not familiar with this operation.

**Note:** Here we use `reshape2` instead of the more current `tidyr` because `reshape2::melt()` allows us to work directly on a table. `tidyr::gather()` requires a data frame.

- Use [`names()`](http://www.rdocumentation.org/packages/base/functions/names) to rename the variables in `DF_melted` to be `c("FILL", "X", "value")`, with the prospect of making this a generalized function later on.
- The plotting call at the end uses `DF_melted`. Add code to make it facetted. Use the formula `FILL ~ .`. Note that we use [`geom_col()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar) now, this is just a short-cut to `geom_bar(stat = "identity")`.

```
# An attempt to facet the accurate frequency histogram from before (failed)
ggplot(adult, aes (x = SRAGE_P, fill= factor(RBMI))) +
  geom_histogram(aes(y = ..count../sum(..count..)), binwidth = 1, position = "fill") +
  BMI_fill +
  facet_grid(RBMI ~ .)

# Create DF with table()
DF <- table(adult$RBMI,adult$SRAGE_P)

# Use apply on DF to get frequency of each group
DF_freq <- apply(DF, 2, function(x) x/sum(x))

# Load reshape2 and use melt on DF to create DF_melted
library(reshape2)
DF_melted <- melt(DF_freq)

# Change names of DF_melted
names(DF_melted) <- c("FILL", "X", "value")

# Add code to make this a faceted plot
ggplot(DF_melted, aes(x = X, y = value, fill = FILL)) +
  geom_col(position = "stack") +
  BMI_fill + 
  facet_grid(FILL ~ .) # Facets
```

n  the previous exercise we looked at different ways of showing the  frequency distribution within each BMI category. This is all well and  good, but the absolute number of each age group also has an influence on  if we will consider something as over-represented or not. Here, we will  proceed to change the widths of the bars to show us something about the  n in each group.

This will get a bit more involved, because the aim is not to draw  bars, but rather rectangles, for which we can control the widths. You  may have already realized that bars are simply rectangles, but we don't  have easy access to the `xmin` and `xmax` aesthetics, but in [`geom_rect()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_tile) we do! Likewise, we also have access to `ymin` and `ymax`. So we're going to draw a box for every one of our 268 distinct groups of BMI category and age.

The clean `adult` dataset, as well as `BMI_fill`, are already available. Instead of running [`apply()`](http://www.rdocumentation.org/packages/base/functions/apply) like in the previous exercise, the contingency table has already been transformed to a data frame using [`as.data.frame.matrix()`](http://www.rdocumentation.org/packages/base/functions/as.data.frame).

##### Instructions

100 XP

- To build the rectangle plot, we'll add several variables to `DF`:
- `groupSum`, containing the sum of each row in the `DF`. Use [`rowSums()`](http://www.rdocumentation.org/packages/base/functions/colSums) to calculate this. `groupSum` represents the total number of individuals in each age group.
- `xmax`: the `xmax` value for each rectangle, calculated as `cumsum(DF$groupSum)`
- `xmin`: the `xmin` value for each rectangle, calculated by subtracting the `groupSum` column from the `xmax` column.
- The names of the x axis groups are stored in the row names, which is pretty bad style, so make a *new* variable, `X`, that stores the values of [`row.names()`](http://www.rdocumentation.org/packages/base/functions/row.names) for `DF`.
- Now we are ready to melt the dataset. Load `reshape2` and use `melt()` on `DF`. Specify the `id.vars` variables as `c("X", "xmin", "xmax")` and the `variable.name` argument as `"FILL"`. Store the result as `DF_melted`.
- Have a look at the `dplyr` call that calculates the `ymax` and `ymin` columns of `DF_melted`. It first groups by `X` and then calculates cumulative proportions. The result is stored as `DF_melted` again.
- If all goes well you should see the plot in the viewer when you execute the plotting function at the bottom of the script.

```R
# The initial contingency table
DF <- as.data.frame.matrix(table(adult$SRAGE_P, adult$RBMI))

# Create groupSum, xmax and xmin columns
DF$groupSum <- rowSums(DF)
DF$xmax <- cumsum(DF$groupSum)
DF$xmin <- DF$xmax - DF$groupSum
# The groupSum column needs to be removed; don't remove this line
DF$groupSum <- NULL

# Copy row names to variable X
DF$X <- rownames(DF)

# Melt the dataset
library(reshape2)
DF_melted <- melt(DF, id.vars = c("X","xmin","xmax"), variable.name = "FILL" )

# dplyr call to calculate ymin and ymax - don't change
library(dplyr)
DF_melted <- DF_melted %>%
  group_by(X) %>%
  mutate(ymax = cumsum(value/sum(value)),
         ymin = ymax - value/sum(value))

# Plot rectangles - don't change
library(ggthemes)
ggplot(DF_melted, aes(ymin = ymin,
                 ymax = ymax,
```

# Adding statistics

In  the previous exercise we generated a plot where each individual bar was  plotted separately using rectangles (shown in the viewer). This means  we have access to each piece and we can apply different `fill` parameters.

So let's make some new parameters. To get the Pearson residuals, we'll use the [`chisq.test()`](http://www.rdocumentation.org/packages/stats/functions/chisq.test) function.

The data frames `adult` and `DF_melted`, as well as the object `BMI_fill` that you created throughout this chapter, are all still available. The `reshape2` package is already loaded.

##### Instructions

100 XP

- Use the `adult$RBMI` (corresponding to `FILL`) and `adult$SRAGE_P` (corresponding to `X`) columns inside the [`table()`](http://www.rdocumentation.org/packages/base/functions/table) function that's inside the [`chisq.test()`](http://www.rdocumentation.org/packages/stats/functions/chisq.test) function. Store the result as `results`.
- The residuals can be accessed through `results$residuals`. Apply the `melt()` function on them with no further arguments. Store the resulting data frame as `resid`.
- Change the names of `resid` to `c("FILL", "X", "residual")`. This is so that we have a consistent naming convention similar to how we called our variables in the previous exercises.
- The data frame from the previous exercise, `DF_melted` is already available. Use the [`merge()`](http://www.rdocumentation.org/packages/base/functions/merge) function to bring the two data frames together. Store the result as `DF_all`.
- Adapt the code in the `ggplot` command to use `DF_all` instead of `DF_melted`. Also, map `residual` onto `fill` instead of `FILL`.

```R
# Perform chi.sq test (RBMI and SRAGE_P)
results <- chisq.test(table(adult$RBMI,adult$SRAGE_P))

# Melt results$residuals and store as resid
resid <- melt(results$residuals)

# Change names of resid
names(resid) <- c("FILL", "X", "residual")

# merge the two datasets:
DF_all <- merge(DF_melted,resid)

# Update plot command
library(ggthemes)
ggplot(DF_all, aes(ymin = ymin,
                   ymax = ymax,
                   xmin = xmin,
                   xmax = xmax,
                   fill = residual)) +
  geom_rect() +
  scale_fill_gradient2() +
  scale_x_continuous(expand = c(0,0)) +
  scale_y_continuous(expand = c(0,0)) +
  theme_tufte()
```

# Adding text

Since  we're not coloring according to BMI, we have to add group (and x axis)  labels manually. Our goal is the plot in the viewer.

For this we'll use the `label` aesthetic inside [`geom_text()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_text). The actual labels are found in the `FILL` (BMI category) and `X` (age) columns in the `DF_all` data frame. (Additional attributes have been set inside [`geom_text()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_text) in the exercise for you). 

The labels will be added to the right (BMI category) and top (age)  inner edges of the plot. (We could have also added margin text, but that  is a more advanced topic that we'll encounter in the third course. This  will be a suitable solution for the moment.)

The first two commands show how we got the the four positions for the y axis labels. First, we got the position of the maximum `xmax` values, i.e. at the very right end, stored as `index`. We want to calculate the half difference between each pair of `ymax` and `ymin` (e.g. `(ymax - ymin)/2`) at these `index` positions, then add this value to the `ymin` value. These positions are stored in the variable `yposn`.

We'll begin with the plot thus far, stored as object `p`. In the sample code, `%+% DF_all` refreshes the plot's dataset with the extra columns.

##### Instructions

100 XP

- Plot 1: In the  [`geom_text()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_text) function, define the `x`, `y` and `label` aesthetics.
- Set `x` to `max(xmax)`, so the labels are on the right side of the plot.
- Set the position of `y` to `yposn`.
- Set the `label` text to `FILL`.
- Plot 2: The same thing for the x axis label positions. You don't need to find an index here, since you can use the same `y` position for all these labels: `1`.
- Calculate the half difference between each pair of `xmax` and `xmin` then add this value to `xmin`.
- Complete the plot command by adding the labels in the `xposn` to our plot, the label this time will be `X`, which in this case is the age.

This plot isn't perfect, but it does a pretty good job for an exploratory plot.

```R
# Plot so far
p

# Position for labels on y axis (don't change)
index <- DF_all$xmax == max(DF_all$xmax)
DF_all$yposn <- DF_all$ymin[index] + (DF_all$ymax[index] - DF_all$ymin[index])/2

# Plot 1: geom_text for BMI (i.e. the fill axis)
p1 <- p %+% DF_all + 
  geom_text(aes(x = max(xmax), 
                y = yposn,
                label = FILL),
            size = 3, hjust = 1,
            show.legend  = FALSE)
p1

# Plot 2: Position for labels on x axis
DF_all$xposn <- DF_all$xmin + (DF_all$xmax - DF_all$xmin)/2

# geom_text for ages (i.e. the x axis)
p1 %+% DF_all + 
  geom_text(aes(x = xposn, label = X),
            y = 1, angle = 90,
            size = 3, hjust = 1,
            show.legend = FALSE)
```

# Generalizations

Now  that you've done all the steps necessary to make our mosaic plot, you  can wrap all the steps into a single function that we can use to examine  any two variables of interest in our data frame (or in any other data  frame for that matter). For example, we can use it to examine the `Vocab` data frame we saw earlier in this course.

You've seen all the code in our function, so there shouldn't be  anything surprising there. Notice that the function takes multiple  arguments, such as the data frame of interest and the variables that you  want to create the mosaic plot for. None of the arguments have default  values, so you'll have to specify all three if you want the `mosaicGG()` function to work.

Start by going through the code and see if you understand the function's implementation.

##### Instructions

100 XP

- Print `mosaicGG` and read its contents.
- Calling `mosaicGG(adult, "SRAGE_P","RBMI")` will result  in the plot you've been working on so far. Try this out. This gives you a  mosaic plot where BMI is described by age.
- Test out another combination of variables in the `adult` data frame: Poverty (`POVLL`) described by Age (`SRAGE_P`).
- Try the function on other datasets we've worked with throughout this course:
- `mtcars` dataset: `am` described by `cyl`
- `Vocab` dataset: `vocabulary` described by `education`.

```R
mosaicGG <- function(data, X, FILL) {
  # Proportions in raw data
  DF <- as.data.frame.matrix(table(data[[X]], data[[FILL]]))
  DF$groupSum <- rowSums(DF)
  DF$xmax <- cumsum(DF$groupSum)
  DF$xmin <- DF$xmax - DF$groupSum
  DF$X <- row.names(DF)
  DF$groupSum <- NULL
  DF_melted <- melt(DF, id = c("X", "xmin", "xmax"), variable.name = "FILL")
  DF_melted <- DF_melted %>%
    group_by(X) %>%
    mutate(ymax = cumsum(value/sum(value)),
           ymin = ymax - value/sum(value))

  # Chi-sq test
  results <- chisq.test(table(data[[FILL]], data[[X]])) # fill and then x
  resid <- melt(results$residuals)
  names(resid) <- c("FILL", "X", "residual")

  # Merge data
  DF_all <- merge(DF_melted, resid)

  # Positions for labels
  DF_all$xposn <- DF_all$xmin + (DF_all$xmax - DF_all$xmin)/2
  index <- DF_all$xmax == max(DF_all$xmax)
  DF_all$yposn <- DF_all$ymin[index] + (DF_all$ymax[index] - DF_all$ymin[index])/2

  # Plot
  g <- ggplot(DF_all, aes(ymin = ymin,  ymax = ymax, xmin = xmin,
                          xmax = xmax, fill = residual)) +
  geom_rect(col = "white") +
  geom_text(aes(x = xposn, label = X),
            y = 1, size = 3, angle = 90, hjust = 1, show.legend = FALSE) +
  geom_text(aes(x = max(xmax),  y = yposn, label = FILL),
            size = 3, hjust = 1, show.legend = FALSE) +
  scale_fill_gradient2("Residuals") +
  scale_x_continuous("Individuals", expand = c(0,0)) +
  scale_y_continuous("Proportion", expand = c(0,0)) +
  theme_tufte() +
  theme(legend.position = "bottom")
  print(g)
}
```

# Course III

# Refresher (1)

As a refresher to statistical plots, let's build a scatter plot with an additional statistic layer.

A dataset called `movies_small` is coded in your workspace. It is a random sample of 1000 observations from the larger `movies` dataset, that's inside the `ggplot2movies` package. The dataset contains information on movies from IMDB. The variable `votes` is the number of IMDB users who have rated a movie and the `rating` (converted into a categorical variable) is the average rating for the movie.

##### Instructions

100 XP

- Use `str()` to explore the structure of the dataset `movies_small`, that is available in your workspace.
- Create a scatter plot with a statistics layer on top:
- Use `geom_point()` to make a scatter plot, mapping `votes` onto the `y`, and `rating` onto the `x` aesthetics.
- Add a `stat_summary()` layer that depicts the mean and the 95% CI. Use a `"crossbar"` geom, a `width` of 0.2 and a red `col`.
- Add `scale_y_log10()` to transform the y scale.

```R
# Create movies_small
library(ggplot2movies)
set.seed(123)
movies_small <- movies[sample(nrow(movies), 1000), ]
movies_small$rating <- factor(round(movies_small$rating))

# Explore movies_small with str()
str(movies_small)

# Build a scatter plot with mean and 95% CI
ggplot(movies_small, aes(x = rating, y = votes)) +
  geom_point() +
  stat_summary(fun.data = "mean_cl_normal",
               geom = "crossbar",
               width = 0.2,
               col = "red" ) +
  scale_y_log10()
```

# Refresher (2)

The plot in the graphics device is a variation on an oft-seen `ggplot2` example using the `diamonds` dataset (containing information on several variables of over 50,000 diamonds).

Recall that there are a variety of `scale_` functions. Here, data are transformed or filtered *first*, after which the plot and associated statistics are computed. For example, `scale_y_continuous(limits = c(100, 1000)` will *remove* values outside that range.

Contrast this to `coord_cartesian()`, which computes the statistics *before* plotting. That means that the plot and summary statistics are performed on the raw data. That's why we say that `coord_cartesian(c(100, 1000))` "zooms in" a plot. This was discussed in the chapter on [`coordinates`](https://campus.datacamp.com/courses/data-visualization-with-ggplot2-2/chapter-2-coordinates-and-facets?ex=1) in course 2.

Here we're going to expand on this and introduce `scale_x_log10()` and `scale_y_log10()` which perform log10 transformations, and `coord_equal()`, which sets an aspect ratio of `1` (`coord_fixed()` is also an option).

Your task is to reproduce the plot in the viewer. Before you do this, it might be a good idea to explore `diamonds` in the console if you are not familiar with it.

##### Instructions

100 XP

- We are using three variables from the `diamonds` data set: `carat`, `price`, and `color`. Map them to the appropriate aesthetics as per the plot in the viewer.
- Add a `geom_point()` layer to make a scatter plot. Set the attributes `alpha = 0.5`, `size = 0.5`, `shape = 16`.
- Transform both axes to log10 scales using the aforementioned scale functions. The `limits` are, for x: `c(0.1,10)`, for y: `c(100,100000)`. To get nice formatting we're using the `expression()` function for the labels. Use `expression(log[10](Carat))` for the x axis and `expression(log[10](Price))` for the y axis.
- Use a `coord_equal()` function with no arguments, which will set the aspect ratio to `1`.

- 

- Take Hint (-30 XP)

```R
# Reproduce the plot
ggplot(diamonds, aes(x = carat, y = price, col = color)) +
  geom_point(alpha = 0.5, size = 0.5, shape = 16) +
  scale_x_log10(expression(log[10](Carat)), limits = c(0.1,10)) +
  scale_y_log10(expression(log[10](Price)), limits = c(100,100000)) +
  scale_color_brewer(palette = "YlOrRd") +
  coord_equal() +
  theme_classic()
```

