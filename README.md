# mouse_challenge

Summary:

Grouped DataFrame: The code begins by creating a DataFrame that identifies the maximum time point for each mouse.

Merging DataFrames: .pyp then merges this grouped DataFrame with the original cleaned DataFrame to get the final tumor volumes.

List and Dictionary: A list of the treatment names is created, and an empty dictionary is set up to hold the tumor volumes for each treatment.

Looping and Appending: The code loops through each treatment, extracting the corresponding tumor volumes and appending them to the dictionary.

Outlier Detection: Finally, .pyp calculates the quartiles, IQR, and determines if there are any outliers based on the calculated bounds.

Explanation of the Print Section:

Loop through outliers: .pyp code iterates over the dictionary of outliers.
Check if there are outliers: For each treatment, .pyp checks if there are any detected outliers. If there are, .pyp prints the treatment name and the corresponding outlier values.
If no outliers: If no outliers are found for a treatment, .pyp simply prints that there are no outliers for that treatment.

GRAPHS:   

BOX PLOT showing the distribution of the final tumor volumes for all mice across the four treatment groups (Capomulin, Ramicane, Infubinol, and Ceftamin).

  The outliers are highlighted in the plot with yellow-colored markers.
  Each box plot shows the median (orange line), interquartile range (IQR, the box itself), and the range of data (whiskers).
  This plot provides a clear visual representation of the tumor volume distribution for each treatment group and highlights    any potential outliers. 

LINE PLOT: This shows the tumor volume versus time point for a single mouse treated with Capomulin. The plot provides a visual representation of how the tumor volume changed over time during the treatment.

SCATTER PLOT: This plot shows the relationship between mouse weight and the average observed tumor volume for all mice treated with Capomulin. This scatter plot helps to understand if there is any correlation between the weight of the mice and the effectiveness of the treatment.

***AI was used for the code to combine the scatterplot with the regressional line***

I had diffiulty with adding the regression line to the scatter graph due to creating the scatter graph first, then creating the regression analysis.   The key was to create both graph codes within the same cell in order that both graphs would be produeced.  

#Group by mouse ID to calculate the average tumor volume and weight per mouse
avg_tumor_volume = capomulin_data.groupby("Mouse ID")[["Weight (g)", "Tumor Volume (mm3)"]].mean()


#perform linear regression
slope, intercept, r_value, p_value, std_err = linregress(
    avg_tumor_volume["Weight (g)"], avg_tumor_volume["Tumor Volume (mm3)"])

#generate the scatter plot
plt.figure(figsize=(8, 5))
plt.scatter(avg_tumor_volume["Weight (g)"], avg_tumor_volume["Tumor Volume (mm3)"], color='blue', label='Data points')

#plot the linear regression line
plt.plot(avg_tumor_volume["Weight (g)"], intercept + slope * avg_tumor_volume["Weight (g)"], color='red', label='Fit line')

#End

Linear regression line: The linear regression line is plotted on top of the scatter plot using plt.plot(), with the equation of the line derived from the slope and intercept values.

#Modifications
Plot Customization: The plot is customized with a title, axis labels, a legend, and a grid for better visualization.
Statistics: The slope, intercept, r-squared value, p-value, and standard error are printed out after the plot is shown.
