[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

**Exercise 3.1**
Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample. Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household. Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household. Plot the actual and biased distributions, and compute their means. As a starting place, you can use chap03ex.ipynb.

*************

Import the relevant libraries.

    import nsfg
    import thinkstats2
    import thinkplot

Read in and save the respondents dataset.

    resp = nsfg.ReadFemResp()

Look at frequencies and plot a histogram and a probability mass function to see the distribution of number of children under 18 in the household.

    resp.numkdhh.value_counts()

    numkid_hist = thinkstats2.Hist(resp.numkdhh)
    thinkplot.Hist(numkid_hist)

    numkid_pmf = thinkstats2.Pmf(resp.numkdhh, label = 'actual')
    thinkplot.Hist(numkid_pmf)

Calculate the mean number of children under age 18 in the household.

    print('mean', numkid_pmf.Mean())

Mean number of children under age 18 in the household is 1.02.

Define a function to bias the distribution and generate a new probability mass function using this biased distribution.

    def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label = label)
    
    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
    new_pmf.Normalize()
    return new_pmf

Plot the probability mass function of the biased distribution, and display it alongside the actual distribution.
    
    biased_pmf = BiasPmf(numkid_pmf, label = 'observed')
    thinkplot.PrePlot(2)
    thinkplot.Pmfs([numkid_pmf, biased_pmf])
    thinkplot.Show(xlabel='number of kids', ylabel = 'PMF')

Calculate the mean number of children under age 18 in the household, using the biased distribution.

    print('mean', biased_pmf.Mean())

Mean number of children under age 18 using the biased sample is 2.40.