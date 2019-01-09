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

