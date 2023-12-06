# Cars-MPG-Prediction-Linear-Regression

In statistics, **linear regression** is an approach for modeling the relationship between a response variable $y$ and one or more explanatory variables. Linear regression can prove a relationship, but it **cannot prove causality**! 
Furthermore it makes some **assumptions**: 

1. **Linearity**: linear regression assumes our response and explanatory variables are **linearly related**.
2. **Normality**: The residuals of the model should follow a normal distribution.
3. **Independence**: Observations are independent of each other.
4. **Homoscedasticity**: The variance of residual is the same for any value of X.

The formula for a simple linear regression is given by 

$$y_i = b_0 + b_1 x_i + e_i$$  
$$\text{for i = } 1, \dots, n$$

where $y_i$ is the true value for our response variable. The formula for the regression equation is given by 

$$\hat{y}_i = b_0 + b_1 x_i$$ 
$$\text{for i = } 1, \dots, n$$

where $\hat{y}_i$ is the predicted value for our response variable and $b_0$ and $b_1$ are the estimated intercept and slope of the line.

Linear regression is basically just the fancy term for finding the line of best fit. In other words, we are looking for the **intercept** and **slope** that defines a line that fits the data as well as possible. "As well as possible..." often means that we are trying to minimize the sum of squared **residuals** which is also called the **Ordinary Least Squares (OLS)** method.

* **Intercept**: The value for our response variable $y$ when our explanatory variable $x=0$. ($b_0$ in the formula above)
* **Slope**: For each unit increase in $x$, the expected increase or decrease in $y$. This definition is sufficient only in the case of a simple linear regression. In the case of multiple linear regression, we have to add "holding all other explanatory variables constant" to our definition, because there is more than one explanatory variable in the model. ($b_1$ in the formula above)
* **Residual**: The difference between an observed value and the fitted value provided by a model: $e_i = y_i - \hat{y}_i$
* **Ordinary Least Squares (OLS)**: OLS is one of the simplest and most common methods used to find the parameters in a linear regression model. It tries to minimize the sum of squared residuals: $\sum_{i=1}^n e_i^2$.

## Metrics

We can calculate the $R^2$ of the model. It has a simple interpretation: the $R^2$ is the *proportion* of the variance in the target variable (in our case mpg) that can be accounted for by our features.

Mathematically speaking we can define $R^2$ as 

$$R^2 = 1 - \frac{SSR}{SST}$$

where **SSR** is the sum of squared residuals ($\sum_{i=1}^n e_i^2$) and **SST** is the total sum of squares ($\sum_{i=1}^n (y_i - \bar{y})^2$).

The value for $R^2$ can be between 0 and 1. If the model perfectly captures the data the **SSR** will be 0 and $R^2$ will return 1. On the other hand a poor fit of the data will result in a high **SSR** and the $R^2$ will be low or even tend towards 0.

Whenever we deal with multiple linear regression $R^2$ should not be the metric of your choice to evaluate the model fit. By adding new features to our model the $R^2$ will either stay the same or increase, even if those additional features don't have any relationship with our target variable. This leads to an overwhelming temptation to add more and more features into our model.

This is where **adjusted $R^2$** comes to help. Adjusted $R^2$ will penalize us for adding more features that actually don't improve our existing model. For a simple linear regression $R^2$ and adjusted $R^2$ will be the nearly the same. The more non-significant features we add to a model the larger the gap between those two metrics will be. Moreover, the adjusted $R^2$ is a useful metric when we want to compare several models with different amounts of features.

The formula of the adjusted $R^2$ is:
$$R_a^2 = 1 - \frac{(1 - R^2) (n - 1)}{n - p - 1} $$  

where $n$ is the number of observations in the data set and $p$ is the number of features.

Results from notebook. Baseline model is just a simple linear regression model with only one feature. Multiple Reg-1 include 4 features with high correlation and Multiple Reg-2 only include 3 features.

| Baseline Model | Multiple Reg-1 | Multiple Reg-2|
| ---------|----------|----------|
| 60.5 %| 70.5 %| 70.6 % |



## Dataset

This dataset is a slightly modified version of the dataset provided in the StatLib library. The data concerns city-cycle fuel consumption in miles per gallon, to be predicted in terms of 3 multivalued discrete and 5 continuous attributes.

[Kaggle-Auto-mpg Dataset](https://www.kaggle.com/datasets/uciml/autompg-dataset)


- mpg:           continuous
- cylinders:     multi-valued discrete
- displacement:  continuous
- horsepower:    continuous
- weight:        continuous
- acceleration:  continuous
- model year:    multi-valued discrete
- origin:        multi-valued discrete
- car name:      string (unique for each instance)

## Environment 

Please make sure you have forked the repo and set up a new virtual environment. For this purpose you can use the following commands:

```sh
pyenv local 3.11.3
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

The added [requirements file](requirements.txt) contains all libraries and dependencies we need to execute the linear regression notebooks.