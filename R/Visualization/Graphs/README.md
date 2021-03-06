* [Ultimate Guide to ggplot2](https://ggplot2-book.org)
* [Color Themes](https://rpubs.com/seslezak/color_schemes)
* [seq, div, and qual aruguments](https://ggplot2.tidyverse.org/reference/scale_brewer.html)
* [Change Facet Labels](https://www.datanovia.com/en/blog/how-to-change-ggplot-facet-labels/)
* [Heat Maps](https://www.r-graph-gallery.com/79-levelplot-with-ggplot2.html)

## ggplot2 Quick Code for Copying and Pasting
```r
library(tidyverse) 	# Includes ggplot2
library(ggthemes)	# Optional Themes

ggplot(
  # Data Frame
	data = ,
			
  # X and Y Variables
		aes(
		   x = ,
		   y = ,
	color = )) +
	  
  # Graph Type
	geom_point() +
	  
  # Graph Theme
	theme_minimal() +
		  
  # Facet Graph by Variables
	facet_grid(	rows = vars(var1),
				cols = vars(var2)) +
	  
  # Graph Labels
	labs(title = "",
		 subtitle = "",
		 caption = "",
		 tag = "Figure 1",
		 x = "",
		 y = "")
	  
  # Save Image
	ggsave("imageTitle.pdf", path = "", width = 10, height = 7)	
```
	
## Show Multiple lines in Plot
* pivot dataset into one column using `pivot_longer`
* Set the desciptive column as the `color` in `ggplot()`

## Sort Axis Vars [Source](https://sebastiansauer.github.io/ordering-bars/)
```r
# Example with Week Days
    df$weekDay <- factor(df$weekDay,
                            levels = c("Monday", 
                                       "Tuesday", 
                                       "Wednesday", 
                                       "Thursday",
                                       "Friday",
                                       "Saturday",
                                       "Sunday"))
```
	

## More Examples

```r	
library(tidyverse)
library(ggthemes)

# Example: mpg dataset (city and highway fuel economy for various makes/models/years of automobiles)

# Basic scatter plot
	ggplot(data = mpg, aes(x = cty, y = hwy)) # this plot is empty because we haven't provided any geom's
	mpg
	ggplot(data = mpg, aes(x = cty, y = hwy), geom_point()) # this won't work because we have to use "+" to add geom's
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_point()
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_jitter()
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_jitter() + theme_bw() # if you don't want a gray theme
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_jitter() + theme_minimal()

# Visualizing additional dimensions through size of dots, colors of dots, labels
	ggplot(data = mpg, aes(x = cty, y = hwy, size=as.factor(manufacturer))) + geom_jitter() + theme_minimal()
	ggplot(data = mpg, aes(x = cty, y = hwy, color=as.factor(manufacturer))) + geom_jitter() + theme_minimal()
	ggplot(data = mpg, aes(x = cty, y = hwy, color=year)) + geom_jitter() + theme_minimal()
	ggplot(data = mpg, aes(x = cty, y = hwy, color=manufacturer)) + geom_jitter() + theme_minimal()
	ggplot(data = mpg, aes(x = cty, y = hwy, color=manufacturer)) + geom_line() + theme_minimal()
	ggplot(data = mpg, aes(x = cty, y = hwy, color=as.factor(year))) + geom_jitter() + theme_minimal()
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_label(manufacturer) + theme_minimal()
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_label(aes(label=manufacturer)) + theme_minimal()


# Other types of plots (univariate and bivariate)
	ggplot(data = mpg, aes(x = cty)) + geom_density() + theme_minimal() # kernel density
	ggplot(data = mpg, aes(x = cty)) + geom_histogram() + theme_minimal() # histogram
	ggplot(data = mpg, aes(x = cty)) + geom_bar() + theme_minimal() # bar
	ggplot(data = mpg, aes(x = cty, y=hwy)) + geom_hex() + theme_minimal() # hex
	ggplot(data = mpg, aes(x = cty, y=hwy)) + geom_bin2d() + theme_minimal() # 2-d histogram
	ggplot(data = mpg, aes(y = cty)) + geom_boxplot() + theme_minimal() # boxplot
	ggplot(data = mpg, aes(y = cty, x=as.factor(year))) + geom_boxplot() + theme_minimal() # boxplot by year
	ggplot(data = mpg, aes(y = cty, x=as.factor(manufacturer))) + geom_boxplot() + theme_minimal() # boxplot by manuf.
	ggplot(data = mpg, aes(y = cty, x=as.factor(manufacturer))) + geom_boxplot() + theme_minimal() + theme(axis.text.x = element_text(angle = 90, hjust = 1)) # change angle of x-axis labels
	ggplot(data = mpg, aes(y = cty, x=as.factor(manufacturer))) + geom_boxplot() + theme_minimal() + theme(axis.text.x = element_text(angle = 45, hjust = 1)) # change angle of x-axis labels
	ggplot(data = mpg, aes(y = cty, x=as.factor(manufacturer))) + geom_boxplot() + theme_minimal() + theme(axis.text.x = element_text(angle = 45, hjust = 1)) + labs(y = "Fuel Economy (City)") # label y axis
	ggplot(data = mpg, aes(y = cty, x=as.factor(manufacturer))) + geom_boxplot() + theme_minimal() + theme(axis.text.x = element_text(angle = 45, hjust = 1)) + labs(y = "Fuel Economy (City)", x = "Manufacturer") # label both axes
	ggplot(data = mpg, aes(y = cty, x=as.factor(manufacturer))) + geom_boxplot() + theme_minimal() + theme(axis.text.x = element_text(angle = 45, hjust = 1)) + labs(y = "Fuel Economy (City)", x = "Manufacturer", caption = paste0("Number of observations: ",dim(mpg)[1])) # add a note explaining number of observations


# Create sub-plots with facet wrap
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_jitter() + theme_minimal() + facet_wrap(vars(as.factor(manufacturer)), ncol = 4)


# Use other themes from ggthemes package
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_jitter() + theme_gdocs() + facet_wrap(vars(as.factor(year)), ncol = 4)
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_jitter() + theme_economist() + facet_wrap(vars(as.factor(year)), ncol = 4)
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_jitter() + theme_economist_white() + facet_wrap(vars(as.factor(year)), ncol = 4)
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_jitter() + theme_fivethirtyeight() + facet_wrap(vars(as.factor(year)), ncol = 4)
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_jitter() + theme_tufte() + facet_wrap(vars(as.factor(year)), ncol = 4)
	ggplot(data = mpg, aes(x = cty, y = hwy)) + geom_jitter() + geom_rangeframe() + theme_tufte() + facet_wrap(vars(as.factor(year)), ncol = 4)

```
