# Various Methods to compare means in R

Statistical tests to use for comparing means.

- T-test

- Wilcoxon test

- ANOVA test and

- Kruskal-Wallis test


# One-Sample T-test in R

one-sample t-test is used to compare the mean of one sample ($\mu$) to a known standard (or theoretical/hypothetical) mean ($\mu_0$).


Note that, one-sample t-test can be used only, when the data are normally distributed . This can be checked using Shapiro-Wilk test .


# Research questions and Hypothesis under testing of single mean

 Research Questions

- whether the mean ($\mu$) of the sample is equal to the theoretical mean ($\mu_0$)?

- whether the mean ($\mu$) of the sample is less than the theoretical mean ($\mu_0$)?

- whether the mean ($\mu$) of the sample is greater than the theoretical mean ($\mu_0$)?

# Null and alternative hypothesis

Null hypotheis will be one of the following form

 null hypothesis (H0) as follow:

<center>

1. $H_0:\mu=\mu_0$

2. $H_0:\mu\leq\mu_0$

3. $H_0:\mu\geq\mu_0$

<center>


Corresponding alternative hypotheis are:

<center>

1. $H_0:\mu\neq\mu_0$

2. $H_0:\mu>\mu_0$

3. $H_0:\mu<\mu_0$

<center>

# Syntax for one sample t-test

1. for equality null hypotyhesis:

<center>

**t.test(sample,mu="expected mean",alternative="two.sided")**

<center>


2. for less than or equal to type null hypothesis:
<center>

**t.test(sample,mu="expected mean",alternative="greater")**

<\center>


3. for greater than or equal to null hypotheis:
<center>

**t.test(sample,mu="expected mean",alternative="less")**

<\center>

#Example

Let us create our own data in the form of a data frame which consist of weighs of mices as follows:

```{r}
set.seed(1234)
my_data <- data.frame(
  name = paste0(rep("M_", 10), 1:10),
  weight = round(rnorm(10, 20, 2), 1)
)
```

Let us have look at the data generated

```{r}
head(my_data, 10)
```

# Preleminary test to check one-sample t-test assumptions

Use Shapiro test for normality:

```{r}
shapiro.test(my_data$weight) # => p-value = 0.6993

```

 Since the p- value is greater that accepted level of significance (0.05), there is no reason to reject the null hypohesis that *the data is normally distributed*.
 
#Compute one-sample Wilcox-test

We want to know, if the average weight of the mice differs from 25g (two-tailed test)?


```{r}
# One-sample t-test
res <- t.test(my_data$weight, mu = 25)
# Printing the results
res 
```

#Explanation:

- t is the t-test statistic value (t = -9.078),

- df is the degrees of freedom (df= 9),

- p-value is the significance level of the t-test (p-value = $7.95310^{-6}$).

- conf.int is the confidence interval of the mean at 95% (conf.int = $[17.8172, 20.6828]$);

- sample estimates is he mean value of the sample (mean = 19.25).

**Inference:**

The p-value of the test is $7.95310^{-6}$, which is less than the significance level alpha = 0.05. We can conclude that the mean weight of the mice is significantly different from 25g with a p-value = $7.95310^{-6}$.

# One-Sample Wilcoxon Signed Rank Test in R

The one-sample Wilcoxon signed rank test is a non-parametric alternative to one-sample t-test when the data cannot be assumed to be normally distributed. It's used to determine whether the median of the sample is equal to a known standard value (i.e. theoretical value).

#Research questions and statistical hypotheses

Research Questions

- whether the median ($m$) of the sample is equal to the theoretical median ($m_0$)?

- whether the median ($m$) of the sample is less than the theoretical median ($m_0$)?

- whether the median ($m$) of the sample is greater than the theoretical median ($m_0$)?

#Null and alternative hypothesis

Null hypotheis will be one of the following form

 null hypothesis ($H_0$) as follow:

<center>

1. $H_0:m=m_0$

2. $H_0:m\leq m_0$

3. $H_0:m\geq m_0$

<center>


Corresponding alternative hypotheis are:

<center>

1. $H_0:m\neq m_0$

2. $H_0:m>m_0$

3. $H_0:m<m_0$

<center>

# Syntax for wilcoxon-test

1. for equality null hypotyhesis:

<center>

**wilcox.test(sample,mu="expected median",alternative="two.sided")**

<center>


2. for less than or equal to type null hypothesis:
<center>

**wilcox.test(sample,mu="expected median",alternative="greater")**

<\center>


3. for greater than or equal to null hypotheis:
<center>

**wilcox.test(sample,mu="expected median",alternative="less")**

<\center>


#Compute one-sample Wilcoxon-test

We want to know, if the average weight of the mice differs from 25g (two-tailed test)?


```{r}
# One-sample t-test
res <- wilcox.test(my_data$weight, mu = 25)
# Printing the results
res 
```

#Explanation:

- p-value is the significance level of the t-test (p-value = $0.005793$).

**Inference:**

The p-value of the test is $0.005793$, which is less than the significance level alpha = 0.05. We can conclude that the mean weight of the mice is significantly different from 25g with a p-value = $0.005793$.

# Unpaired Two-Samples T-test in R

The unpaired two-samples t-test is used to compare the mean of two independent groups.

Note that, unpaired two-samples t-test can be used only under certain conditions:

- when the samples are independent

- when the two groups of samples (A and B), being compared, are normally distributed. This can be checked using Shapiro-Wilk test.

- and when the variances of the two groups are equal. This can be checked using F-test.


#Research questions and statistical hypotheses


- whether the mean of group A ($\mu_1$) is equal to the mean of group B ($\mu_2$)?

- whether the mean of group A ($\mu_1$) is less than the mean of group B ($\mu_2$)?

- whether the mean of group A ($\mu_1$) is greather than the mean of group B ($\mu_2$)?


#Null and alternative hypothesis

Null hypotheis will be one of the following form

 null hypothesis ($H_0$) as follow:

<center>

1. $H_0:\mu_1=\mu_2$

2. $H_0:\mu_1\leq\mu_2$

3. $H_0:\mu_1\geq\mu_2$

<center>


Corresponding alternative hypotheis are:

<center>

1. $H_0:\mu_1\neq\mu_2$

2. $H_0:\mu_1>\mu_2$

3. $H_0:\mu_1<\mu_2$

<center>

# Syntax for unpaired t-test

1. for equality null hypotyhesis:

<center>

**t.test(sample1,sample2,mu="expected mean",alternative="two.sided")**

<center>


2. for less than or equal to type null hypothesis:
<center>

**t.test(sample1,sample2,mu="expected mean",alternative="greater")**

<\center>


3. for greater than or equal to null hypotheis:
<center>

**t.test(sample1,sample2,mu="expected mean",alternative="less")**

<\center> 

# Example

Here, we'll use an example data set, which contains the weight of 18 individuals (9 women and 9 men):

```{r}
# Data in two numeric vectors
women_weight <- c(38.9, 61.2, 73.3, 21.8, 63.4, 64.6, 48.4, 48.8, 48.5)
men_weight <- c(67.8, 60, 63.4, 76, 89.4, 73.3, 67.3, 61.3, 62.4) 
# Create a data frame in long form
my_data <- data.frame( 
                group = rep(c("Woman", "Man"), each = 9),
                weight = c(women_weight,  men_weight)
                )
```

*Objective:* We want to know, if the average women's weight differs from the average men's weight?

#Descriptive analysis

Compute summary statistics by groups:

```{r}
library(dplyr)
group_by(my_data, group) %>%
  summarise(
    count = n(),
    mean = mean(weight, na.rm = TRUE),
    sd = sd(weight, na.rm = TRUE)
  )
```

#Visualization

```{r}
# Plot weight by group and color by group
library("ggpubr")
ggboxplot(my_data, x = "group", y = "weight", 
          color = "group", palette = c("#00AFBB", "#E7B800"),
        ylab = "Weight", xlab = "Groups")
```

#Preleminary test to check independent t-test assumptions


*Assumption 1*: Are the two samples independents?

Ans: Yes, since the samples from men and women are not related.

*Assumtion 2*: Are the data from each of the 2 groups follow a normal distribution?

Ans: We have to verify it with Shapiro test.

```{r}
with(data=my_data,shapiro.test(weight[group == "Man"]))
with(data=my_data,shapiro.test(weight[group == "Woman"]))
```

*Conclusion*: From the output, the two p-values are greater than the significance level 0.05 implying that the distribution of the data are not significantly different from the normal distribution. In other words, we can assume the normality.


#Preleminary test to check independent t-test assumptions (Cont...)


*Assumption 3*. Do the two populations have the same variances?

Ans: We have to use *F-test* to verify it.
We'll use F-test to test for homogeneity in variances. This can be performed with the function *var.test()* as follow:



```{r}
res.ftest <- var.test(weight ~ group, data = my_data)
res.ftest
```

*Conclusion*: The p-value of F-test is $p = 0.1713596$. It's greater than the significance level alpha = 0.05. In conclusion, there is no significant difference between the variances of the two sets of data. Therefore, we can use the classic t-test witch assume equality of the two variances.

#Compute unpaired two-samples t-test


*Research Question* : Is there any significant difference between women and men weights?


1.  Compute independent t-test - Method 1: The data are saved in two different numeric vectors.


```{r}
# Compute t-test
res <- t.test(women_weight, men_weight, var.equal = TRUE)
res
```

2.  Compute independent t-test - Method 2: The data are saved in a data frame.

```{r}
# Compute t-test
res <- t.test(weight ~ group, data = my_data, var.equal = TRUE,conf.level=.99)
res
```

*Conclusion*: The p-value of the test is $0.01327$, which is less than the significance level alpha = 0.05. We can conclude that men's average weight is significantly different from women's average weight with a p-value = $0.01327$.

#Takeaway of this session

- For testing of equality of means *independance, normality and same variability* should be ensured.

- Normality of samples can be assured by Shapiro test

- Uniform variability can be ensured by $F-test$.

- Use *t.test()* to calculate t- test.


# Unpaired Two-Samples Wilcoxon Test in R

The unpaired two-samples Wilcoxon test (also known as *Wilcoxon rank sum test* or *Mann-Whitney test*) is a non-parametric alternative to the unpaired two-samples t-test, which can be used to compare two independent groups of samples. It's used when your data are *not normally* distributed.

Syntax is similar to *t-test* except the test name ans parameter. *wilcox.test()* is the function and median is the parameter.

# Example

Let us use the same example in the case of two sample t- test for conveniance.

**Objective**:We want to know, if the median women's weight differs from the median men's weight?


# Compute unpaired two-samples Wilcoxon test


*Research Question* : Is there any significant difference between women and men weights?

1. Compute two-samples Wilcoxon test - Method 1: The data are saved in two different numeric vectors.

```{r}
res <- wilcox.test(women_weight, men_weight,exact = FALSE)
res
```

2. Compute two-samples Wilcoxon test - Method 2: The data are saved in a data frame.


```{r}
res <- wilcox.test(weight ~ group, data = my_data,
                   exact = FALSE)
res
```

**Conclusion**: The p-value of the test is $0.02712$, which is less than the significance level alpha = 0.05. We can conclude that men's median weight is significantly different from women's median weight with a p-value = $0.02712$.

#Takeaway

- if two samples satisfies normality condition along with independence and uniform variability, use t test

- if normality does not hold good, then use Wilcoxon test.

# Paired Samples T-test in R


The paired samples t-test is used to compare the means between two related groups of samples. In this case, you have two values (i.e., pair of values) for the same samples. This session describes how to compute paired samples t-test using R software.

Paired t-test can be used only when the difference d is normally distributed. This can be checked using Shapiro-Wilk test.

#Research questions and statistical hypotheses

Typical research questions are:


- whether the mean difference ($d$) is equal to 0?
- whether the mean difference ($d$) is less than 0?
- whether the mean difference ($d$) is greather than 0?

**Hypotheis are**:

In statistics, we can define the corresponding null hypothesis ($H_0$) as follow:

- $H_0:d=0$

- $H_0:d\leq 0$

-$H_0:d\geq 0$


The corresponding alternative hypotheses ($H_=1$) are as follow:

- $H_0:d\neq 0$

- $H_0:d> 0$

-$H_0:d<0$

#R function to compute paired t-test


Syntax **t.test(beforesample,aftersample,paired=TRUE,alternative="two.sided/greater/less")**

# Example with working rule

As an example of data, 20 mice received a treatment X during 3 months. We want to know whether the treatment X has an impact on the weight of the mice.

To answer to this question, the weight of the 20 mice has been measured before and after the treatment. This gives us 20 sets of values before treatment and 20 sets of values after treatment from measuring twice the weight of the same mice.

In such situations, paired t-test can be used to compare the mean weights before and after treatment.

Paired t-test analysis is performed as follow:

- Calculate the difference ($d$) between each pair of value

- Compute the mean ($m$) and the standard deviation ($s$) of $d$

- Compare the average difference to $0$. If there is any significant difference between the two pairs of samples, then the mean of $d (m)$ is expected to be far from 0.

# Creating Data

```{r}
# Data in two numeric vectors
# ++++++++++++++++++++++++++
# Weight of the mice before treatment
before <-c(200.1, 190.9, 192.7, 213, 241.4, 196.9, 172.2, 185.5, 205.2, 193.7)
# Weight of the mice after treatment
after <-c(392.9, 393.2, 345.1, 393, 434, 427.9, 422, 383.9, 392.3, 352.2)
# Create a data frame
my_data <- data.frame( 
                group = rep(c("before", "after"), each = 10),
                weight = c(before,  after)
                )
```
**Objective**: We want to know, if there is any significant difference in the mean weights after treatment?
# A glance on data

```{r}
my_data

```



# Pre-tests

Compute summary statistics (mean and sd) by groups using the *dplyr* package.


```{r}
library("dplyr")
group_by(my_data, group) %>%
  summarise(
    count = n(),
    mean = mean(weight, na.rm = TRUE),
    sd = sd(weight, na.rm = TRUE)
  )
```

# Visualization

```{r}
# Plot weight by group and color by group
library("ggpubr")
ggboxplot(my_data, x = "group", y = "weight", 
          color = "group", palette = c("#00AFBB", "#E7B800"),
          order = c("before", "after"),
          ylab = "Weight", xlab = "Groups")
```

#Preleminary test to check paired t-test assumptions


*Assumption 1*: Are the two samples paired?

*ANs*: Yes, since the data have been collected from measuring twice the weight of the same mice.

*Assumption 2*: Is this a large sample?

*Ans*: No, because *n < 30*. Since the sample size is not large enough (less than 30), we need to check whether the differences of the pairs follow a normal distribution.

*Assumption 2*: Is the data normal?

Use Shapiro-Wilk normality test as described at: Normality Test in R.

Null hypothesis: the data are normally distributed
Alternative hypothesis: the data are not normally distributed

# Examining normality of difference $d$

```{r}
# compute the difference
d <- with(my_data, 
        weight[group == "before"] - weight[group == "after"])
# Shapiro-Wilk normality test for the differences
shapiro.test(d) 
```

# Compute paired samples t-test

**Research Question** : Is there any significant changes in the weights of mice after treatment?

1. Compute paired t-test - Method 1: The data are saved in two different numeric vectors.


```{r}
# Compute t-test
res <- t.test(before, after, paired = TRUE)
res
```

2. Compute paired t-test - Method 2: The data are saved in a data frame.


```{r}
# Compute t-test
res <- t.test(weight ~ group, data = my_data, paired = TRUE)
res
```

#  Paired Samples Wilcoxon Test in R

If normality condition will not satisfied for the pair-wise difference distribution, then use Wilcoxon test as in the previous cases. Only difference is that here we use median as parameter and function call changes to *wilcox.text(beforesample,aftersample, paired=TRUE)*


# Example

Let us use the previous example itself.

```{r}
my_data
```

#Compute paired-sample Wilcoxon test

1. Compute paired Wilcoxon test - Method 1: The data are saved in two different numeric vectors.

```{r}
res <- wilcox.test(before, after, paired = TRUE)
res
```

2. Compute paired Wilcoxon-test - Method 2: The data are saved in a data frame.


```{r}
# Compute t-test
res <- wilcox.test(weight ~ group, data = my_data, paired = TRUE)
res
```


# Takeaway notes

- the samples should be paired observations.

- if pair- wise difference follows normal distribution, then use paired t test

- if pair-wise difference does not follow normal distribution, then use Wilcoxon rank test
