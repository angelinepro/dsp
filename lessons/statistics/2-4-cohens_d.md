[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

**Exercise 2.4**
Using the variable totalwgt_lb, investigate whether first babies are lighter or heavier than others. Compute Cohen’s d to quantify the difference between the groups. How does it compare to the difference in pregnancy length?

*************

Start by importing the relevant libraries.

    import nsfg
    import thinkstats2
    import math

Read in and save the pregnancy dataset.

    df = nsfg.ReadFemPreg()

Create a separate dataframe using just the live births, since that is the population of interest.

    live = df[df.outcome == 1]

Split the live births into firstborns and others.

    firsts = live[live.birthord == 1]
    others = live[live.birthord != 1]

Define a function to calculate Cohen's Effect Size.

    def CohenEffectSize(group1, group2):
        diff = group1.mean() - group2.mean()    
        var1 = group1.var()
        var2 = group2.var()
        n1, n2 = len(group1), len(group2)
        pooled_var = (n1 * var1 + n2 * var2) / (n1+n2)
        d = diff / math.sqrt(pooled_var)
        return d

Calculate the effect size for length of pregnancy of firstborn children compared to others.

    CohenEffectSize(firsts.prglngth, others.prglngth)

Calculate the effect size for birthweight of firstborn children compared to others. 

    CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)

The effect size for birthweight of firstborn children is -0.09 standard deviations. The negative sign suggests that firstborn children are likely to weigh less than non-firstborn children, however, because the effect size is so small, it's may not be worth reporting, as it's likely not to be clinically significant. To compare, the effect size for pregnancy length for firstborn children is 0.03 standard deviations, suggesting slightly longer pregnancies for firstborn children compared to non-firstborn children, however, again, the effect size is so small that it may not be worth reporting, as it's not likely to be clinically significant. 