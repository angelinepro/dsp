[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

**Exercise 5.1**
 In the BRFSS (see Section 5.4), the distribution of heights is
roughly normal with parameters µ = 178 cm and σ = 7.7 cm for men, and
µ = 163 cm and σ = 7.3 cm for women.
In order to join Blue Man Group, you have to be male between 5’10” and
6’1” (see http://bluemancasting.com). What percentage of the U.S. male
population is in this range? Hint: use scipy.stats.norm.cdf.

****

Start by importing the relevant libraries.

    import scipy

Convert the height range of interest (5'10" - 6'1") to centimeters to facilitate calculation, since the parameters given are in centimeters.

    print("5'10 in cm is", str(((10/12)+5)*30.48), "cm")
    print("6'1 in cm is", ((1/12)+6)*30.48, "cm")

Calculate what percent of the male population has a height below 6'1, or 185.42 cm.

    percent_below_61 = scipy.stats.norm.cdf(185.42, loc = 178, scale = 7.7)

Calculate what percent of the male population has a height below 5'10", or 177.80 cm.

    percent_below_510 = scipy.stats.norm.cdf(177.80, loc = 178, scale = 7.7)

Compute the difference to calculate what percent of the male population has a height between 6'1 and 5'10"

    percent_below_61-percent_below_510

34% of the male population falls within this range.