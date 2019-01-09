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
- In the second call of [`ggplot()`](http://www.rdocumentation.org/packages/ggplot2/functions/ggplot) **change** the `color` argument in [`aes()`](http://www.rdocumentation.org/packages/ggplot2/functions/aes) (which stands for *aesthetics*). The color should be dependent on the displacement of the car engine, found in `disp`.
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

# base package and ggplot2, part 2 - lm

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

```

```

