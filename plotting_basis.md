## Introduction

Data is huge and it is everywhere but along with that comes the need to understand data and base our decisions after drawing inferences from data.

One of the major steps that we have in the field in data science is first exploring the data thereby presenting it in the form of informative plots and it is referred to as Data Visualization.

We are very visual creatures as a large portion of brain dedicates itself to visual processing. Images are able to grab our attention easily, we are immediately drawn to them. 

John Tukey was an American mathematician best known for the development of the FFT algorithm and boxplot.Here are some of his notable quotes on the importance of visualization through graphs.

>“The simple graph has brought more information to the data analyst’s mind than any other device.” — John Tukey


### Step 1: installing `ggplot2` library

```{r}
#install.packages("ggplot2") # if not installed
require("ggplot2") # check whether the package is available if not install
library(ggplot2)
```

### Loading the dataset


```{r}
mydata=mtcars #assign the built- in dataframe mtcars into the variable mydata
str(mydata)
```

### Working with `ggplot`


**Scatterplots:**

They are used to represent distribution between different variables in form of points scattered all over. They are are most basic and simple to make and every data point gets a chance to be represented however it becomes somewhat less distinct to see the image unlike the case with a line chart.

**Language of Grammer of Graphics:** A `geom` is a geometrical object that a plot uses to represent data and different plots use different `geoms` like bar chart uses bar `geoms` , line chart uses line `geoms`, boxplot uses boxplot `geoms`.

mappings are used to map different aesthetics (written in the brackets under aes) assigning different axis x and y to variables and other aesthetics like color, fill also associated with other variables to be represented in the plot.


```{r}
ggplot(data = mydata)+
geom_point(mapping = aes (x = mpg, y= cyl))# giving  different axis to different variables 
```


```{r}
ggplot(data = mtcars)+
geom_point(mapping = aes(x = cyl, y = hp))
```

```{r}
ggplot(data = mpg) + 
geom_point(mapping = aes(x = displ, y = hwy), color = "red")
```

```{r}
ggplot(data = mydata)+
geom_point(mapping = aes(x = mpg , y = c(rownames(mydata)),color =gear))
```

**Line chart:**

```{r}
ggplot(data = mydata) + 
geom_smooth(mapping = aes(x = cyl, y = hp))
```


```{r}
ggplot(data = mydata, mapping = aes(x = cyl, y = hp),method=NULL) + 
 geom_point(mapping = aes(color = mpg)) + 
 geom_smooth()
```

**Bar charts:**

```{r}
ggplot(data = mydata) + 
 geom_bar(mapping = aes(x = cyl))
```

```{r}
ggplot(data = mydata) + 
 geom_bar(mapping = aes(x = cyl),fill=unique(mydata$cyl))
```
**Another example:**

```{r}
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = color))
```

```{r}
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = color), position = "fill")
```

```{r}
ggplot(data = diamonds) + 
    geom_bar(mapping = aes(x = cut, fill = color),position = "dodge")
```
**Boxplot:**

They are mainly used to represent outliers and it is their ability to represent the difference between distributions and showing outliers for different categories of a variable.

```{r}
ggplot(data = diamonds, mapping = aes(x = cut, y = x)) + 
  geom_boxplot()
```
```{r}
mydata$cyl=as.factor(mydata$cyl)
p=ggplot(data = mydata, mapping = aes(x = cyl, y = mpg))+
  geom_boxplot()+
  coord_flip()
p+labs(title="Box plot for Mtcars",
        x ="Number of cylinder", y = "Milage")
```
