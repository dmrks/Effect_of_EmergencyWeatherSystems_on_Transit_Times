# Effect_of_EmergencyWeatherSystems_on_Transit_Times

As of the year 2018, 55% of the world’s population lived in urban areas. By 2050, the United Nations expects this number to jump to 68%. 
Major metropolitan areas will have to adapt and become more efficient in order to accommodate billions of new residents in the coming decades. 
One infrastructure system in particular that will feel the burden of growing urban populations is transportation.

Imagine a large, growing city that is located in an area that gets heavy snowfall in the fall and winter seasons. 
City officials have partnered with a large tech company to collect anonymous navigation data about residents’ transit times during peak rush hours.

Preliminary data seems to verify what city officials suspected: transit times are substantially longer in the winter months when the city gets a lot of snow. 
The city officials decide to institute a “snow emergency” system between the months of November and March intended to reduce average transit times during severe weather. 
A snow emergency will be issued whenever the city experiences at least 4 inches of snow in a 24-hour period. 
During snow emergencies, the city will restrict car traffic to only major roads and will waive fares for public transportation.

The leaders hope that these actions will incentivize people to use the city’s efficient train system instead of commuting via car, which will reduce traffic congestion and transit times. 
After three winter seasons, the city decides to analyze the navigation data to see whether the snow emergency system was effective at reducing transit times.

In this project, you will use regression discontinuity design (RDD) to assess the system’s effectiveness. 

# Data Exploration

1.
First, let’s import the dataset for this project. We’ve provided a file named snow.csv in the workspace. Load this file into a dataframe named snow_df.

2.

Now that the dataset is imported and ready to work with, let’s take a look at the first few rows of the dataframe snow_df. This dataset contains several variables:

Forcing Variable
snowfall: The amount of snowfall on recorded date (inches)
Treatment Variable
emergency: Whether or not a snow emergency was issued on the recorded date (“Emergency” vs. “No Emergency”)
Outcome Variable
minutes: Average commute time on recorded date (minutes)
Others
date: Recorded date


# Assessing RDD Assumptions
3.
Use the ggplot2 package to create a scatter plot of the data with the forcing variable on the x-axis and the outcome variable on the y-axis. Use colors and shapes to distinguish between dates with a snow emergency and dates without a snow emergency.

Save the base plot as scatter_base and view the plot.


4.
Let’s add a little more detail to the plot. Add a vertical dashed line to scatter_base at the snowfall cutoff that determines emergency status. Save the updated plot to scatter_cutpoint and print it to the console to view the plot.

Does it look like this is a sharp RDD or a fuzzy RDD?


5.
To verify that there is actually a discontinuity in the outcome at the cutpoint, add linear best fit lines to scatter_cutpoint. Separate best fit lines should be plotted for dates with a snow emergency and dates without a snow emergency. Save this plot as scatter_fit and print it to view the plot.

Does there appear to be a discontinuity in the outcome variable around the cutpoint?



# Calculating IK Bandwidth

6.
Calculate the optimal IK bandwidth for the data and save the result to snow_ik_bw. Print snow_ik_bw to the console. Is the bandwidth large or small relative to the scale of the forcing variable?


7.
Add solid vertical lines to scatter_cutpoint to plot the range of the optimal bandwidth stored in snow_ik_bw. Save the updated plot to scatter_bw and print it to the console to view the plot.

Does a lot of the data fall outside of the bandwidth? How do you think this could affect the treatment effect estimate?


# Estimating Causal Treatment Effect

8.
Using the correct cutpoint and optimal bandwidth you just calculated, fit a local linear regression model using the RDestimate() function. Save the results to snow_rdd.



9.
Print the results of the local linear regression results stored in snow_rdd. Take note of the estimate of the LATE across different bandwidths. Are the values similar?


# Standard Errors and Conclusion
10.
Print the number of observations in each of the three bandwidths provided in snow_rdd. How does sample size change across the optimal bandwidth, half the bandwidth, and double the bandwidth?



11.
Print the standard errors of the LATE estimates at each bandwidth provided in snow_rdd. How did the standard errors change as the sample size increased?



12.
Great job! Using the optimal bandwidth of 2.63 inches, we calculated a local average treatment effect (LATE) of -11.04. 
This means that in this dataset, 
the use of the snow emergency system resulted in an average decrease in commute time of 11.04 minutes.

Given what we know about interpreting the LATE, think about where this causal effect is generalizable — do you think the bandwidth was wide enough to cover many different snowfall events?
