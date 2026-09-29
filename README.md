# Honest vs. Misleading Visualizations

## Objective
This project shows how axis ranges, time windows and scales change the story a chart tells about the same data.

## Data Sources
- Anscombe's Quartet from seaborn (44 rows, 4 datasets of 11 points each).
- FRED series AHETPI (average hourly earnings of production workers) and CPIAUCSL (consumer price index), monthly from 1964.
- World Bank GDP in current US dollars from the open datasets repository (13,979 country-year rows, 4 columns, 262 economies, 1960 to 2023).

## Methodology
- Recreated Anscombe's Quartet and compared the mean, variance, correlation and regression line of each dataset.
- Plotted all four datasets with the shared line y = 3 + 0.5x to expose the differences the statistics hide.
- Defined the Lie Factor as the size of the effect shown in the graphic divided by the size of the effect in the data.
- Built a truncated-axis and a zero-based revenue chart and computed the Lie Factor by hand.
- Redesigned the revenue chart as a labeled dot plot with a zero-based axis.
- Joined the AHETPI and CPIAUCSL series and deflated earnings to 2020 dollars using the 2020 average CPI as the base.
- Drew four versions of real earnings (full range from $0, truncated axis, cherry-picked window and log scale).
- Ran a four-step EDA checklist on the World Bank data covering structure, distributions, relationships and anomalies.
- Compared raw and log10 GDP histograms and measured skewness before and after the transformation.
- Plotted GDP paths for the USA, China, Japan, Germany and India.
- Built a box plot of log10 GDP by decade and a country by year heatmap of missing data.
- Built an interactive toggler with ipywidgets and matplotlib that switches between nominal and real earnings, raises the y-axis floor, sets the start and end year and switches between linear and log scales while printing a live Lie Factor.

## Key Findings
- All four Anscombe datasets share a mean x of 9.0, a mean y of 7.50, a variance in x of 11.0 and a correlation near 0.816.
- Dataset III has one outlier and Dataset IV has one point at x = 19 that sets its whole slope.
- Removing the outlier in Dataset III raises the correlation from 0.816 to nearly 1.
- A 4.1% revenue increase from 98 to 102 looked like a 200% increase on an axis starting at 96, which gives a Lie Factor of 49.0.
- The zero-based chart and the dot plot show the same growth at its true size.
- Nominal hourly earnings rose from $2.50 in 1964 to $32.53 in August 2026.
- Real earnings rose about 20% from roughly $21 to roughly $25 over the same period.
- Real earnings fell from a peak near $24 in the early 1970s to a low near $19.70 in the mid-1990s before recovering.
- The truncated axis exaggerates swings and the 2015 window hides four decades of decline.
- The log axis in this series stretches the swings much like the truncated axis does.
- Raw GDP has a skewness of 8.4 and the log transformation cuts it to 0.2.
- In 2023 the USA had the largest GDP at about $27 trillion and China ranked second at about $18 trillion among the five economies plotted.
- The long-format GDP data shows 0 missing values and 0 negative values because the file omits gaps as absent rows.
- The pivoted sample of 20 economies shows 74 gaps in 1,280 country-years.
- Those gaps cluster at the start and end of the period and depend on year and economy so the missingness is MAR.
- The toggler reads a Lie Factor of 1.00 with a linear axis and a $0 floor.
- The reading rises as the floor moves up because the Lie Factor equals first value divided by first value minus floor.

## Limitations
- The 262 economies include aggregates such as World and Euro area so country averages would double count.
- FRED revises its series so values may differ slightly on a later run.
- Testing the toggler showed that the AI-generated code capped the y-axis floor at 90% of the lowest value shown so the floor slider did not work above $2.25 for nominal earnings.

## Takeaway
Plot the data before trusting any statistic and check the axis start, the time window, the scale and the price basis before trusting any chart.
