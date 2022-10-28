# Dynamic-TLFS-contest

R Studio Table Contest 2022 Entry

## About

This is my entry into the R Studio 2022 Table Contest. It uses Tplyr, reactable, shiny and Quarto to present an insights dashboard for clinical trial data analysis. </br> </br> You may view it [here.](https://matt-portfolio.shinyapps.io/dynamic-tlf/)

## Preview

Here is a preview of the dashboard. <strong>Clicking the preview image will take you to a higher resolution video version.</strong>

[![](demo.gif)](https://www.youtube.com/watch?v=Ax1md38X-tI)

## Aims

My aims for this project were two-fold:

1.  Investigate whether we can dynamically create tables which can be used to guide an exploratory analysis. </br></br>The analysis starts with an <strong>anchor table</strong>, where individual cells can be clicked to retrieve the study participants ID's who comprise it. These are subsequently fed into additional tables, listings and figures through reactives. </br></br> In previous work, I've hard coded the anchor table by pre-specifying the variables to be displayed. With this work, you can now **dynamically** specify the anchor table to include any variables you like, which in turn can be used explore subgroups <i>on-the-fly</i>.</br></br> This work is largely enabled by utilizing the metadata building features of the [Tplyr](https://github.com/atorus-research/Tplyr) package.

2.  Currently, no dashboard extension or package exists for Quarto. I used this opportunity to also see if I could (roughly) mimic what `flexdashboard` offers by using Quarto and custom css. My inspiration was the bootswatch `lux` theme.

## Linked TLFs

The linked TLFs are also interactive and share the spirit of "drilling down" and exploration

### Adverse Events Table

-   Uses `reactable`'s groupBy to succinctly present a large table
-   Cells (in the second column) are <strong>hyper-linked</strong> to open a [MedlinePlus](https://http://medlineplus.gov/) search of that term. I found this resource was helpful in learning about medical conditions when analyzing clinical trials data.

### Patient Listing 1

-   Uses `reactable`'s filter + search to navigate a potentially exhaustive table
-   Leverages `reactable`'s columnGroups + formatting to organize the data layout
-   Capable of exporting a list subject identifiers as a CSV file to enable further analyses of interesting subgroups

### Patient Listing 2

-   Uses `reactablefmtr`'s inline visual to show vital signs measured at three times relative to baseline (i.e. percent change)
-   Leverages `reactable`'s columnGroups + formatting to organize the data layout
-   Paired with shiny inputs to enable switching of Blood Pressure Parameters and Visits

### Adverse Event Figure

-   The `highcharter` column chart is a <strong>drill down plot</strong>. The first layer displays the top 4 System Organ Classes for a given subset
-   Clicking each of bars lets you drill down into a stacked column chart for the Preferred Terms x Severity.
-   Customized tool tips to display information more clearly (i.e. severity of adverse event)
-   It's a visual representation of the adverse event linked table, but could be extended to show other data views too.


## Code Organization

For this project, I've used `renv` so that you may recreate this in an offline setting with ease.

While there are many ways to structure this dashboard, I chose not to experiment with modules and and keep things simple until a proper dashboard extension or framework for Quarto is released. I've instead isolated key parts of the code into their own server `chunks` with comments for ease of review.

## Data

The data for this example comes from the [TestDataFactory](https://github.com/phuse-org/TestDataFactory) repository operated by [phuse](https://phuse.global/). This data is not stored in the app deployment or my code repository - it is accessed directly from the source repository.

## Future

This app can be extended in a number of different ways:

- Including additional, linked TLFs; the sky's the limit! Modules?
- Uploading data functionality - the way I've began to structure the server will enable this in the future (i.e. using renderUI)
- More robust control and validation for when the anchor table is updated