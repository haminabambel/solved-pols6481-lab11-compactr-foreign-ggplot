Download Link: https://assignmentchef.com/product/solved-pols6481-lab11-compactr-foreign-ggplot
<br>
The primary objective is to explore interactions among variables in linear regression models. Interpretation of regression coefficients is complicated by the fact that each variable’s marginal effects will be conditional on the value of any variable it is interacted with, and by the fact that each coefficient can only be interpreted as the marginal effect of a variable when any variable it is interacted with equals zero.

<ol>

 <li><strong> Dataset</strong>: <em>alexseev.dta</em></li>

</ol>

<strong>III. Packages</strong>:  <em>compactr</em>, <em>foreign</em>, <em>ggplot</em>

<ol>

 <li><strong> Preparation</strong></li>

</ol>

1) Open RStudio by double-clicking the icon or selecting RStudio from the Windows Start menu.

2) Open the POLS6481-Spring2021-UH-lab Project and perform a Git pull.

3) If not using Projects, Git, and <em>here </em>download files, place in working directory, and make changes as needed.

4) Open the R script by typing <em>Ctrl</em>+<em>O</em> or by clicking on File in the upper-left corner, using the dropdown menu, and navigating to the script in your working directory.

5) Open the R script by typing <em>Ctrl</em>+<em>O</em> or by clicking on File in the upper-left corner, using the dropdown menu, and navigating to the script in your working directory.

6) If you are missing any packages from the script, you should see a message similar to the one in the screenshot below (this screenshot is also available full size in the lab folder). Click install or install any needed packages manually:

7) Run line 1 in the script to allow easier loading of the data files or, alternately, manually edit line 5.

8) Run lines 2-4 in the R script to load packages that you can use to make more attractive figures and the package that you will need to open the dataset.




<ol>

 <li><strong> Instructions for Lab 11</strong></li>

</ol>




You will use data on ethnocentric (anti-immigrant) voting during the 2003 Russian State Duma elections. This data was collected by Mikhail Alexseev and for his 2006 <em>Political Behavior </em>article, “Ballot-Box Vigilantism: Ethnic Population Shifts and Xenophobic Voting in Post-Soviet Russia.” William Berry, Matt Golder, and Daniel Milton re-analyzed the data on pages 665–668 of their 2012 <em>Journal of Politics </em>article, “Improving Tests of Theories Positing Interactions.” I posted both articles in Blackboard.




Load the dataset by running lines 5–6, changing the directory if needed. The dataset that can be downloaded from the internet has two additional lines of NA values, which create some trouble in trying to find means and other summary statistics. You will work with a data frame named alexseev.




The main dependent variable, <em>e03ld</em>, is the percent of votes cast for the extreme nationalist party, Zhirinovsky Bloc, in 2003. The main party in this bloc, LDPR, persistently ran on a campaign platform of “Russia for Ethnic Russians.”




Run lines 7–8 to examine the normality of the dependent variable (<em>e03ld</em>) visually. In line 7, you generate the normal quantile plot of <em>e03ld</em> against the normal distribution; any deviation from a straight line indicates a non-normal distribution. In line 8, you generate a histogram of <em>e03ld</em>; any deviation from a bell curve would indicate a non-normal distribution.

&gt; qqnorm(alexseev$e03ld)

&gt; hist(alexseev$e03ld, freq = FALSE, breaks=19)

One reason for concern about the distribution of the dependent variable is that it is truncated below at 0.




The two main independent variables are <em>slav89</em>, which is the percent of the population that belonged to the dominant ethnic group (Slavs) in 1989, and <em>nonslav8</em>, which the <u>change</u> in the percentage of the population accounted for by ethnic minorities between 1989 and 2002.




Alexseev’s preferred theory, named the “Defended Nationhood” hypothesis, posits that a greater Slavic share of the population should be positively associated with the Zhirinovsky Bloc’s vote share <u>and</u> that this effect should be enhanced by a large influx of ethnic minorities, hence the inclusion of a multiplicative interaction term.




Alexseev also argues that greater increases in the percentage of ethnic minorities should increase support for anti-immigrant parties regardless of Slavic population.<a href="#_ftn1" name="_ftnref1">[1]</a>




Alexseev also includes six control variables:

<ul>

 <li><em>inc9903</em> is a measure of change in average personal income from 1999 to 2003;</li>

 <li><em>eduhi02</em> is the percent of the population with a college education in 2002;</li>

 <li><em>unemp02</em> is the percent of the working age population claiming unemployment benefits in 2002;</li>

 <li><em>apt9200</em> is the percent of apartments or houses converted to private ownership from the start of privatization in 1992 to 2000;</li>

 <li><em>vsall03</em> is a region’s population size; and</li>

 <li><em>brdcont</em> is a dummy variable identifying regions located along Russia’s borders over which it had a dispute with a neighboring state at any time between 1991 and 2003.</li>

</ul>




Run lines 10–11 to estimate Alexseev’s main model, which he labels as Test 1 in his Table 2 (2006: 225), and to inspect the results. (You may spend some time inspecting the constant and the control variables’ effects, but our focus in the remainder of lab will be on the <em>slav89</em> and <em>nonslav8</em> variables, and their interaction.) The remaining columns in Table 2 focus on specific non-slavic ethnic groups.




If you have run the model correctly, then you should see the following regarding his main hypothesis:

<ul>

 <li><em>slav89</em> has a positive regression coefficient, which is consistent with Alexseev’s theory, but it is statistically insignificant;</li>

 <li><em>nonslav8</em> has a negative regression coefficient, which is <u>inconsistent</u> with Alexseev’s theory, and it is statistically significant;</li>

 <li>the interaction of <em>slav89</em> and <em>nonslav8</em> has a positive regression coefficient, which is consistent with Alexseev’s theory, but it is statistically insignificant.</li>

</ul>

If you have kept up with the readings, then by now you should be able to answer the following question: Why are these three bulleted findings virtually meaningless – especially the first two?




Recall that when you are examining regression coefficients for variables that are in a multiplicative interaction, the coefficient only tells you the impact when the other variable in the interaction equals zero.

That is, when including an interaction of <em>x</em> and <em>z</em>, the marginal effect of <em>x</em> on <em>y</em> equals <em>β<sub>x</sub></em> + <em>β<sub>xz</sub></em>×<em>z</em>; this implies that the marginal effect equals  only when <em>z </em>= 0. So, it is more useful to examine the marginal effect of each independent variable at their <em>typical </em>values instead. Moreover, multiplicative interactions have a tendency to inflate standard errors, so statements about statistical significance are dubious.




Run lines 13–15 to examine the distribution of the interaction term, <em>sl89nsl8</em>, and its two constituent variables, <em>slav89</em> and <em>nonslav8</em>; save the mean values of the constituent terms, named <em>s.bar</em> and <em>ns.bar</em>:

&gt; s.bar = summary(alexseev$slav89)[4]

&gt; ns.bar = summary(alexseev$nonslav8)[4]

Run line 16 to calculate the interaction of the mean values (which is not equal to the mean of the interaction term). Next, run line 18 to find the marginal effect of <em>slav89</em> when <em>nonslav8</em> is set at its mean value:

&gt; model$coef[2] + model$coef[4]*ns.bar

Then, run line 19 to find the marginal effect of <em>nonslav8</em> when <em>slav89</em> is set at its mean value:

&gt; model$coef[3] + model$coef[4]*s.bar

Later in this lab, we will come back to whether these marginal effects are statistically significant.




To get more insight into the marginal effects, let us explore how the predicted values of vote for the Zhirinovsky Bloc changes when the values of the <em>slav89</em> and <em>nonslav8</em> variables change from their 25<sup>th</sup> percentile to their median, and from their median to the 75<sup>th</sup> percentile.




Begin by running line 21 to define the mean value of all the control variables, and then run line 22 to create a baseline value of <em>e03ld </em>by adding the intercept to the products found by multiplying each coefficient times its respective control variable’s mean value. If you were to inspect the summary of <em>e03ld</em>, then you might discover that the average is about 12.5 percent; our baseline value is a bit low because it implicitly holds the <em>slav89</em> and <em>nonslav8</em> variables, as well as the interaction term, <em>sl89nsl8</em>, equal to zero. You can run line 23 to check an equality that we found back in week 2: the fitted value of the dependent variable holding all independent variables at their averages equals the average value of the dependent variable.




When calculating a bunch of predicted values in order to inspect marginal effects, it is often extremely useful to create a new dataset of inputs. The approach we are about to take is not the most elegant, but it is practical. We are going to have three variables (<em>slav89</em>, <em>nonslav8</em>, and their interaction) set at three different values (first quartile, median, and third quartile), and then calculate predicted values by multiplying each model coefficient times a particular value of the corresponding variable, and adding the baseline value.




If you run lines 25–28, you will create the new data frame. The <em>slav89</em> variable is set at first quartile, median, and third quartile – in that order – three times. The <em>nonslav8</em> variable is set at its first quartile three times, at its median three times, and at its third quartile three times. The interaction is created from the product of <em>slav89</em> and <em>nonslav8</em>. (Therefore, the fifth observation out of nine has all three variables at their median value.)




Run line 29 to create a column of predicted values in the data frame, which is named <em>new.data</em>. If you simply type <em>new.data</em> in the <strong>Console</strong> window, then RStudio will display the data frame for you to view. The first three columns show you the values that were set for the explanatory variables, and the fourth column shows you the predicted value of the dependent variable.




If you focus on the fourth, fifth and sixth predicted values, this shows you how the predicted value of <em>e03ld </em>changes in response to increases in <em>slav89</em>, holding <em>nonslav8</em> at its median. You should observe that increases in <em>slav89</em> correspond to increasing support for the Zhirinovsky Bloc, which is consistent with Alexseev’s theory.




If you focus on the second, fifth and eighth predicted values, this shows you how the predicted value of <em>e03ld </em>changes in response to increases in <em>nonslav8</em>, holding <em>slav89</em> at its median. You should observe that increases in <em>nonslav8</em> actually correspond to slight decreases in support for the Zhirinovsky Bloc, which is inconsistent with Alexseev’s theory.




Demonstrating that predicted support for the Zhirinovsky Bloc increased with increases in <em>slav89</em> or decreased with increases in <em>nonslav8</em> does <u>not</u> prove that either variable has a <u>statistically significant</u> effect on the value of the dependent variable. We will postpone a discussion of statistical significance until after we perform two more tasks and then use R to calculate standard errors. Also, we have not directly addressed the main question of whether increases in <em>nonslav8</em> tend to heighten the effect of changes in <em>slav89</em>.  We can view this indirectly by seeing the following:

<ul>

 <li>when the change in percent minority population is low (<em>nonslav8</em> = 0.1568), <em>yhat</em> increases from 96 to 13.45 as <em>slav89</em> increases from 82.14 to 97.16, a difference of _____</li>

 <li>when the change in percent minority population is high (<em>nonslav8</em> = 2.2550), <em>yhat</em> increases from 59 to 13.34 as <em>slav89</em> increases from 82.14 to 97.16, a difference of _____</li>

</ul>




Three major tasks remain: to put R’s power to work by graphing predicted values, to put the power of R to work by graphing marginal effects, and to perform tests of statistical significance on marginal effects.




You are about to create a new variable with many values of <em>slav89</em>, and then use the basic equation for predicted values, i.e., , to inspect how the value of <em>e03ld</em> is expected to vary as <em>slav89</em> increases, at the same three values of <em>nonslav8</em> identified above.




Run the code in line 31 to create a variable with 101 values, evenly spaced between the minimum and the maximum values of <em>slav89</em>. Next, run lines 32–34 to create predicted vote shares for the Zhirinovsky Bloc for all values in the domain of <em>slav89</em>, using the baseline value we created earlier (line 22), and setting <em>nonslav8</em> equal to its first quartile (line 32), its median (line 33), and its third quartile (line 34). I have included the code from line 33 for your inspection:

&gt; yhat.q2 &lt;- baseline + model$coef[2]*index + model$coef[3]*sumns[3] + model$coef[4]*index*sumns[3]

Thus, you are adding the (a) baseline value, plus (b) the product of the coefficient for <em>slav89 </em>and a value of <em>slav89</em>, plus (c) the product of the coefficient for <em>nonslav8 </em>and the median value of <em>nonslav8</em>, plus (d) the product of the interaction term and the median value for <em>nonslav8</em> and a value of <em>slav89</em>.




Run the code in lines 35-36 to plot the three lines generated when <em>nonslav8</em>’s value is set at its first quartile (shown in red), at its median (shown in black), and at its third quartile (shown in blue). You should have expected to see all three of these lines being upward sloping.




If the posited interaction effect for <em>nonslav8</em> is correct, then the steepest line should be the blue line (more rapid increase in minority population) and the shallowest line should be the red line (slower increase in minority population). Are these expectations met?




If the posited its main effect for <em>nonslav8</em> is correct, the blue line’s value should diverge above the black line as <em>slav89</em>’s value increases, and the red line’s value should diverge below the black line as <em>slav89</em>’s value increases. Are these expectations met?




The next step is to investigate the interaction effect at all values in the domain of <em>nonslav8</em>. To foreshadow, you are about to create a new variable with many values of <em>nonslav8</em>, and then use the basic equation for marginal effects for <em>x</em>, i.e., , to inspect how the value of the partial derivative with respect to <em>slav89</em> (¶ <em>e03ld</em> /¶ <em>slav89</em>) changes as the value of <em>nonslav8</em> increases.




Run the code in line 38 to create a variable with 101 values, evenly spaced between the minimum and the maximum values of <em>nonslav8</em>. Next, run line 39 to create marginal effects for <em>slav89</em> at all values in the domain of <em>nonslav8</em>. I have included the code from line 39 for your inspection:

&gt; dydsl89 &lt;- model$coef[2]+model$coef[4]*smooth




You can run lines 40–45 or type the following code to plot marginal effects over the domain of <em>nonslav8</em>:

&gt; plot(smooth, dydsl89, cex=.25, xlim=c(min(smooth),max(smooth)))

<strong> </strong>

Take the time to examine closely the equations for creating this plot. Students who have learned calculus will have an easier time understanding that the marginal effect of <em>x</em> is the first derivative with respect to <em>x</em> of the function <em>y</em> = <em>f</em>(<em>x,z</em>) = <em>b</em><sub>0</sub> + <em>b</em><sub>1</sub><em>x + b</em><sub>2</sub><em>z + b</em><sub>3</sub><em>xz</em>; using the rules for derivatives yields ¶<em>y</em>/¶<em>x </em>= <em>b</em><sub>1</sub> + <em>b</em><sub>3</sub><em>z</em>.

So, you must add the coefficient for <em>slav89</em> and the coefficient for the interaction times a given value of <em>nonslav8</em>.




Nine lines of code (47–51 plus 54–57) provide one way to plot marginal effects and confidence intervals around those marginal effects. Recall that in a linear model, the marginal effect equals the regression coefficient, and there is a single confidence interval around that effect. For a model with an interaction, however, the marginal effect will depend on the value of <em>z</em> (as you saw above), but the confidence interval also depends on the value of <em>z</em>. You will start by saving the variance-covariance matrix of the estimators:

&gt; vce=vcov(model)




Next you will save three entries: the variance of the main effect coefficient for <em>slav89</em>, the variance of the interaction effect coefficient, and the covariance of the aforementioned main effect coefficient and the interaction effect coefficient:

&gt; varsl89&lt;-vce[2,2]

&gt; varsl89nsl8&lt;-vce[4,4]

&gt; cova&lt;-vce[2,4]




Next you will combine these three terms using the equation for the standard error for a marginal effect, i.e., , at all 1000 values of <em>nonslav8</em> that you generated earlier:

&gt; sedydsl89&lt;-sqrt(varsl89 + (smooth^2)*varsl89nsl8 + 2*smooth*cova)

If you wish to see how the standard error varies with the value of <em>nonslav8</em>, then you can run line 52.




To generate the confidence intervals around the marginal effect, you will need to multiply a <em>t</em> critical value times the standard error. Many of the scholarship about interaction terms (Kam and Franzese; Matt Golder and his co-authors) advise using a 90% confidence interval. Line 54 provides code for finding the <em>t</em> critical value associated with 5% in the upper tail of the <em>t</em> distribution, for degrees of freedom equal to <em>n</em>–<em>k</em>–1 from the regression model run earlier.

&gt; t.star = qt(.95,model$df.residual)




Run lines 55–56 to create the upper and lower bounds for the confidence interval for the slope; you are adding and subtracting 1.96 times the standard error (computed in line 69) to/from the slope.

&gt; upperci &lt;- dydsl89 + t.star*sedydsl89

&gt; lowerci &lt;- dydsl89 – t.star*sedydsl89




Finally, run line 57 to plot the marginal effect and its confidence interval, with a horizontal line for zero. The curve shown by running line 57 is <u>not</u> the predicted value of <em>e03ld</em> given the value of <em>slav89</em>; rather the curve shows the <u>slope</u> of the function relating share of the population belonging to the ethnic majority to support for the Zhirinovsky Bloc.




When the marginal effect is above zero, it indicates that in this range, increases in <em>slav89</em> have a positive effect on support for the Zhirinovsky Bloc. When the marginal effect plot slopes upward, it indicates that the impact of ethnic majority population on support for the Zhirnovsky Bloc increases as the change in the percent of ethnic minorities increases.




You might be wondering whether someone has automated this process. The answer is yes; the <em>interplot </em>package is one way of doing this. Run line 59 to install the package and run line 60 to activate it.

Run line 61 of to re-estimate the model with an interaction rather than the interaction variable; take a moment to inspect the difference between model (which you ran in line 10) and model2.




You can run lines 62–69 to show a basic plot (most of the code has to do with labels), or alternatively, you can run lines 71–78 to include a histogram of values of <em>nonslav8</em> (the rest of the code is identical). Note that the default is to use a 95% confidence level; this can be changed easily by typing ci = 0.90, inside the first set of parentheses.




Pretty cool, right?




To clear the <strong>Environment</strong>, type rm(list=ls()) or click on the broom icon.

To clear the <strong>Console</strong> window, type Ctrl-<em>l</em>




<a href="#_ftnref1" name="_ftn1">[1]</a> Alexseev’s theory is based on studies of anti-migrant vigilantism in American cities and anti-minority hate crimes in New York’s 51 boroughs, so this is an interesting application of American scholarship to comparative politics.