### Using the data 'mtcars'

```{r}
# Load data
data("mtcars")
dfm <- mtcars
library(ggpubr)
# Convert the cyl variable to a factor
dfm$cyl <- as.factor(dfm$cyl)
# Add the name colums
dfm$name <- rownames(dfm)
# Inspect the data
head(dfm)
```



## Vehicles distribution with number of cylinders 

Create ordered bar plots. Change the fill color by the grouping variable "cyl". Sorting will be done globally, also by groups.

```{r}
ggbarplot(dfm, x = "name", y = "mpg",
          fill = "cyl",               # change fill color by cyl
          color = "white",            # Set bar border colors to white
          palette = "jco",            # jco journal color palett. see ?ggpar
          sort.val = "asc",          # Sort the value in ascending("desc /asc") order
          sort.by.groups = TRUE,      # Don't sort inside each group
          x.text.angle = 90           # Rotate vertically x axis texts
          )
```

## Deviation Plots

The deviation graph shows the deviation of quantitative values to a reference value. In the R code below, we'll plot the mpg z-score from the mtcars data set.

Calculate the z-score of the mpg data: Now we have created a normalized score for 'mpg' measures.

```{r}
# Calculate the z-score of the mpg data
dfm$mpg_z <- (dfm$mpg -mean(dfm$mpg))/sd(dfm$mpg)
dfm$mpg_grp <- factor(ifelse(dfm$mpg_z < 0, "low", "high"), 
                     levels = c("low", "high"))
# Inspect the data
head(dfm[, c("name", "wt", "mpg", "mpg_z", "mpg_grp", "cyl")])
```

## Bar plot with normalized 'mpg' values

```{r}
ggbarplot(dfm, x = "name", y = "mpg_z",
          fill = "cyl",               # change fill color by cyl
          color = "white",            # Set bar border colors to white
          palette = "jco",            # jco journal color palett. see ?ggpar
          sort.val = "asc",          # Sort the value in ascending("desc /asc") order
          sort.by.groups = TRUE,      # Don't sort inside each group
          x.text.angle = 90           # Rotate vertically x axis texts
          )
```


## Catagorized plot based on mpg_grp


```{r}
ggbarplot(dfm, x = "name", y = "mpg_z",
          fill = "mpg_grp",           # change fill color by mpg_level
          color = "white",            # Set bar border colors to white
          palette = "jco",            # jco journal color palett. see ?ggpar
          sort.val = "desc",          # Sort the value in descending order
          sort.by.groups = FALSE,     # Don't sort inside each group
          x.text.angle = 0,           # Rotate vertically x axis texts
          ylab = "MPG z-score",
          legend.title = "MPG Group",
          rotate = TRUE,las=2,
          ggtheme = theme_minimal()
          )
```


## A Density plot

The following is a distribution plot that shows how the milage of the vehicles varies with number of cylinders.

```{r}
# Density plot with mean lines and marginal rug
# :::::::::::::::::::::::::::::::::::::::::::::::::::
# Change outline and fill colors by groups ("cyl")
# Use custom palette
ggdensity(dfm, x = "mpg",
   add = "mean", rug = T,
   color = "cyl", fill = "cyl",
   palette = c("green", "blue","red"))
```


### Alternatives to bar plots

Lollipop chart

Lollipop chart is an alternative to bar plots, when you have a large set of values to visualize.

Lollipop chart colored by the grouping variable "cyl":



## Deviation plot

```{r}
ggdotchart(dfm, x = "name", y = "mpg",
           color = "cyl",                                # Color by groups
           palette = c("#00AFBB", "#E7B800", "#FC4E07"), # Custom color palette
           sorting = "descending",                       # Sort value in descending order
           add = "segments",                             # Add segments from y = 0 to dots
           rotate = TRUE,                                # Rotate vertically
           group = "cyl",                                # Order by groups
           dot.size = 8,                                 # Large dot size
           label = round(dfm$mpg),                        # Add mpg values as dot labels
           font.label = list(color = "white", size = 9, 
                             vjust = 0.5),               # Adjust label parameters
           ggtheme = theme_pubr()                        # ggplot2 theme
           )
```






## Deviation plot in 'lollypop' style

Deviation graph:

Use y = "mpg_z"
Change segment color and size: add.params = list(color = "lightgray", size = 2)

```{r}
ggdotchart(dfm, x = "name", y = "mpg_z",
           color = "cyl",                                # Color by groups
           palette = c("#00AFBB", "#E7B800", "#FC4E07"), # Custom color palette
           sorting = "descending",                       # Sort value in descending order
           add = "segments",                             # Add segments from y = 0 to dots
           add.params = list(color = "lightgray", size = 2), # Change segment color and size
           group = "cyl",                                # Order by groups
           dot.size = 6,                                 # Large dot size
           label = round(dfm$mpg_z,1),                        # Add mpg values as dot labels
           font.label = list(color = "white", size = 9, 
                             vjust = 0.5),               # Adjust label parameters
           ggtheme = theme_pubr()                        # ggplot2 theme
           )+
  geom_hline(yintercept = 0, linetype = 2, color = "lightgray")
```

## Cleveland's dot plot

Color y text by groups. Use y.text.col = TRUE.

```{r}
ggdotchart(dfm, x = "name", y = "mpg",
           color = "cyl",                                # Color by groups
           palette = c("#00AFBB", "#E7B800", "#FC4E07"), # Custom color palette
           sorting = "descending",                       # Sort value in descending order
           rotate = TRUE,                                # Rotate vertically
           dot.size = 2,                                 # Large dot size
           y.text.col = TRUE,                            # Color y text by groups
           ggtheme = theme_pubr()                        # ggplot2 theme
           )+
  theme_cleveland()                                      # Add dashed grids
```



## Creating your own data and publication ready plots

```{r}
library(ggpubr)
# Create some data format
# :::::::::::::::::::::::::::::::::::::::::::::::::::
set.seed(1234)
wdata = data.frame(
   sex = factor(rep(c("F", "M"), each=200)),
   weight = c(rnorm(200, 54), rnorm(200, 58)))
head(wdata, 4)
```

##Creating a denisty plot

```{r}
# Density plot with mean lines and marginal rug
# :::::::::::::::::::::::::::::::::::::::::::::::::::
# Change outline and fill colors by groups ("sex")
# Use custom palette
ggdensity(wdata, x = "weight",
   add = "mean", rug = T,
   color = "sex", fill = "sex",
   palette = c("#00AFBB", "#E7B800"))
```


### A simple multi variable plot


```{r}
#devtools::install_github("kassambara/ggpubr")
#Plot with multiple groups
# +++++++++++++++++++++
# Create some data
df2 <- data.frame(supp=rep(c("VC", "OJ"), each=3),
                  dose=rep(c("D0.5", "D1", "D2"),2),
                  len=c(6.8, 15, 33, 4.2, 10, 29.5))
 
ggdotchart(df2, x = "dose", y = "len",
           color = "supp", 
           size = 3,
           add = "segment",
           add.params = list(color = "lightgray", size = 1.5), 
           position = position_dodge(0.3),
           palette = "jco",
           ggtheme = theme_pubclean()
)
```

