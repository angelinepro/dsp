[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

**Exercise 4.2** 
The numbers generated by random.random are supposed to be uniform between 0 and 1; that is, every value in the range should have the same probability.
Generate 1000 numbers from random.random and plot their PMF and CDF. Is the distribution uniform?

*******

Import the relevant libraries.

    import nsfg
    import thinkstats2
    import thinkplot
    import random

Generate a list containing 1000 random numbers.

    random_nums = []
    for i in range(1000):
        random_nums.append(random.random())

Plot the cumulative distribution function for these random numbers.
    
    random_cdf = thinkstats2.Cdf(random_nums)
    thinkplot.Cdf(random_cdf)
    thinkplot.Show(xlabel = 'percentile rank', ylabel = 'CDF')

Plot the probability mass functin for these random numbers.

    random_pmf = thinkstats2.Pmf(random_nums)
    thinkplot.Pmf(random_pmf)
    thinkplot.Show(xlabel = 'number', ylabel = 'probability')

Yes, it appears that the function truly is random. The distribution of the pmf indicates that it is uniform (there is an equal probability across all values). The distribution of the cdf also indicates that it is uniform (20% of the sample is below the 20th percentile, 40% of the sample is below the 40th percentile, etc). 