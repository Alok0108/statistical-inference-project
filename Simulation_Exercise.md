Overview
--------

We will investigate the exponential distribution in R and compare it
with the Central Limit Theorem. The exponential distribution can be
simulated in R with rexp(n, lambda) where lambda is the rate parameter.
The mean of exponential distribution is 1/lambda and the standard
deviation is also 1/lambda. Set lambda = 0.2 for all of the simulations.
We will investigate the distribution of averages of 40 exponentials.
Note that we will need to do a thousand simulations.

Simulations
-----------

Set the simulation variables lambda, exponentials, and seed.

    ECHO=TRUE
    set.seed(1337)
    lambda = 0.2
    exponentials = 40

Run Simulations with variables

    sMean = NULL
    for (i in 1 : 1000) sMean = c(sMean, mean(rexp(exponentials, lambda)))

Sample Mean versus Theoretical Mean
-----------------------------------

#### Sample Mean

Calculating the mean from the simulations with give the sample mean.

    mean(sMean)

    ## [1] 5.055995

#### Theoretical Mean

The theoretical mean of an exponential distribution is lambda^-1.

    lambda^-1

    ## [1] 5

#### Comparison

There is only a slight difference between the simulations sample mean
and the exponential distribution theoretical mean.

    abs(mean(sMean)-lambda^-1)

    ## [1] 0.05599526

Sample Variance versus Theoretical Variance
-------------------------------------------

#### Sample Variance

Calculating the variance from the simulation means with give the sample
variance.

    var(sMean)

    ## [1] 0.6543703

#### Theoretical Variance

The theoretical variance of an exponential distribution is (lambda \*
sqrt(n))^-2.

    (lambda * sqrt(exponentials))^-2

    ## [1] 0.625

#### Comparison

There is only a marginal difference between the simulations sample
variance and the exponential distribution theoretical variance.

    abs(var(sMean)-(lambda * sqrt(exponentials))^-2)

    ## [1] 0.0293703

Distribution
------------

This is a density histogram of the 1000 simulations. There is an overlay
with a normal distribution that has a mean of lambda^-1 and standard
deviation of (lambda\*sqrt(n))^-1, the theoretical normal distribution
for the simulations.

    library(ggplot2)
    ggplot(data.frame(y=sMean), aes(x=y)) + 
      geom_histogram(aes(y=..density..), binwidth=0.2, fill="#0072B2", 
                     color="black") +
      stat_function(fun=dnorm, args=list(mean=lambda^-1, 
                                        sd=(lambda*sqrt(exponentials))^-1), 
                    size=2) +
      labs(title="Plot of the Simulations", x="Simulation Mean")

![](Simulation_Exercise_files/figure-markdown_strict/unnamed-chunk-8-1.png)
