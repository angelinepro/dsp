[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

**Exercise 7.1** 

Using data from the NSFG, make a scatter plot of birth weight
versus mother’s age. Plot percentiles of birth weight versus mother’s age.
Compute Pearson’s and Spearman’s correlations. How would you characterize the 
relationship between these variables?

*****

Start by importing the relevant libraries.

    import nsfg
    import thinkplot
    import numpy as np
    import thinkstats2

Read in the relevant dataframe.

    df = nsfg.ReadFemPreg()

Create a scatter plot of birth weight and mother's age.

    thinkplot.Scatter(df.totalwgt_lb, df.ager, alpha = 0.2)

Plot percentiles of birthweight vs. maternal age.

    df_nomissing = df.dropna(subset = ['ager', 'totalwgt_lb'])
    bins = np.arange(15, 45, 3)
    indices = np.digitize(df_nomissing.ager, bins)
    groups = df_nomissing.groupby(indices)

    ages = [group.ager.mean() for i, group in groups]
    cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups]

    for percent in [75, 50, 25]:
        weights = [cdf.Percentile(percent) for cdf in cdfs]
        label = '%dth' % percent
        thinkplot.Plot(ages, weights, label = label)

    thinkstats2.Corr(df_nomissing.ager, df_nomissing.totalwgt_lb)

Compute Pearson's correlation.

    thinkstats2.Corr(df_nomissing.ager, df_nomissing.totalwgt_lb)

Compute Spearman's correlation

    thinkstats2.SpearmanCorr(df_nomissing.ager, df_nomissing.totalwgt_lb)

Maternal age and birthweight don't appear to be correlated, given the low correlation coefficients for using both Pearson's and Spearman's correlation, and the scatter plot. However, based on the plot of percentiles of weight by mother's age, it looks like for those in the 75th percentile of birthweight, birthweight increases with maternal age.