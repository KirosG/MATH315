_Most of these resources come from [R Graphics Cookbook](www.cookbook-r.com/Graphs/)_ 

# Missing data showing up in ggplot? 
`na.omit()` dat df. Use `dplyr` to select only the variables you are going to plot, then pipe in the `na.omit()` at the end. It will create a temporary data frame (e.g) `plot.data` that you then provide to `ggplot()`.


```
plot.data <- addhealth %>% select(var1, var2) %>% na.omit()
ggplot(plot.data, <stuff>...)
```


# Got numerical binary 0/1 data but want to plot it as categorical? 
* Option 1: Create a second variable `var_factor` for plotting and keep the binary `var` as 0/1 for analysis. 
* Option 2: http://www.cookbook-r.com/Graphs/Legends_(ggplot2)/#changing-the-factor-in-the-data-frame

Consider a continuous variable `total_bill`, and a 0/1 binary variable `sex`. 
```
ggplot(data=df1, 
    aes(x=time, y=total_bill, group=sex, shape=sex, colour=sex)) + 
    geom_line() + geom_point()+ 
    scale_colour_discrete(name  ="Payer",
                          breaks=c("Female", "Male"),
                          labels=c("Woman", "Man"))
```


# Add means to boxplots
Boxplots are great. Even better with violin overlays. Know what makes them even better than butter? Adding a point for the mean. Check out [this stack overflow post](https://stackoverflow.com/questions/23942959/ggplot2-show-separate-mean-values-in-box-plot-for-grouped-data) for context. 

```
ggplot(df, aes(x=b, y=c, fill=a)) +
  geom_boxplot() +
  stat_summary(fun.y="mean", geom="point", size=5,
    position=position_dodge(width=0.75), color="white")
```


# Change the legend title? 
Add the `name=` argument to whatever layer you added that created the legend. 
I.e. if you filed boxplots by a categorical `gender` variable you'd add the layer

```
scale_fill_discrete(name="Gender")
```

# Grouped summary statistics using `dplyr`




# Grouped summary statistics using `tapply`


