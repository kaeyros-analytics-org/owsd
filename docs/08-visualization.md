

# Visualization

## Bar chart
A bar chart is a representation of numerical data in pictorial form of rectangles (or bars) having uniform width and varying heights." They are also known as bar graphs.


```r
#construction of the dataframe
data_barchart <- as.data.frame(table(data_1$`What is your religion?`))
data_barchart <- data_barchart %>%
    dplyr::mutate(percentage = round(100*(Freq/sum(Freq)),2),
                  pct1 = paste0(percentage, "%")) %>%
  rename(Religion=Var1)


#plot the bar chart
plotly::plot_ly(data_barchart, x = ~Religion,
                  type = "bar",
                  y = ~percentage,
                  marker = list(color = "#318CE7"),
                  text = paste(data_barchart$pct1, sep = ""), textposition = 'outside') %>%
    layout(title = "Number of persons by religion"
    )

```


## Pie chart
A pie chart is a type of graph representing data in a circular form, with each slice of the circle representing a fraction or proportionate part of the whole.


```r
#construction of the dataframe
data_piechart <- as.data.frame(table(data_1$Sex))
data_piechart <- data_piechart %>%
    dplyr::mutate(percentage = round(100*(Freq/sum(Freq)),2),
                  pct1 = paste0(percentage, "%"))

#plot the pie chart
plotly::plot_ly(data_piechart, labels= ~Var1,
          values= ~Freq, type="pie",
          hoverinfo = 'text',
          textinfo = 'label+percent',
          insidetextfont = list(color = '#FFFFFF'),
          text = ~paste("Sex :",Var1,
                        "<br>Number of persons :", Freq,
                        "<br>Percentage :", pct1),
          marker = list(colors = c("#318CE7", "#89CFF0"),
                        line = list(color = '#FFFFFF', width = 1),showlegend = FALSE)) %>%
    layout(title="",
           xaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE),
           yaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE))
```


## Histogram
A histogram is a chart that plots the distribution of a numeric variable’s values as a series of bars. Each bar typically covers a range of numeric values called a bin or class; a bar’s height indicates the frequency of data points with a value within the corresponding bin.

```r
library(ggplot2)

# Change colors
p<-ggplot(data_1, aes(x=`How many children do you have?`)) + 
  geom_histogram(color="black", fill="white")
p
```


## Scatter plot\
A scatter plot (or scatter chart, scatter graph) uses dots to represent values for two different numeric variables. The position of each dot on the horizontal and vertical axis indicates values for an individual data point. Scatter plots are used to observe relationships between variables.

```r
time_series <- readxl::read_excel("./data/data_for_workshop2.xls", sheet = "times_series")
ggplot(time_series, aes(x = `Heigh of plant`,
                   y = `Number of roots`)) +
geom_point()
```


## Line chart\
A line chart, also known as a line graph, is a visual representation of data that displays information as a series of data points connected by straight line segments. Line charts are commonly used to show trends or changes over time, making them particularly useful for illustrating temporal patterns or relationships in data. Line charts provide a clear and intuitive way to visualize how values evolve or fluctuate over a specific period. 

```r
ggplot(time_series, aes(x = Month, y = `Heigh of plant`,color = Treatments,group = Treatments)) +
  geom_line()
```


## Map visualization

```r
#load required packages
library(leaflet)
library(sf)
library(readr)


cameroon_geojson <- sf::st_read("./data/cm.json")

#load the data
population <- read_csv("./data/positives_case_covid.csv")

# Joindre les données de population à la carte du Cameroun
cameroon_geojson$population <- population$`Positive Cases`

# Créer la carte Leaflet
leaflet(data = cameroon_geojson) %>%
  addTiles() %>%
  addPolygons(fillColor = ~colorQuantile("Set2", population)(population),
              stroke = FALSE,
              fillOpacity = 0.7,
              label = ~paste(name, " : ", "Positive Cases:", population))
```
