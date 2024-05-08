

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


```{=html}
<div class="plotly html-widget html-fill-item" id="htmlwidget-bfcc745891f02bcce3a1" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-bfcc745891f02bcce3a1">{"x":{"visdat":{"63305329542c":["function () ","plotlyVisDat"]},"cur_data":"63305329542c","attrs":{"63305329542c":{"x":{},"y":{},"marker":{"color":"#318CE7"},"text":["0.93%","28.04%","13.08%","1.87%","56.07%"],"textposition":"outside","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"bar"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":"Number of persons by religion","xaxis":{"domain":[0,1],"automargin":true,"title":"Religion","type":"category","categoryorder":"array","categoryarray":["Adventist","Catholic","Muslim","pentecostal","Protestant"]},"yaxis":{"domain":[0,1],"automargin":true,"title":"percentage"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"x":["Adventist","Catholic","Muslim","pentecostal","Protestant"],"y":[0.93000000000000005,28.039999999999999,13.08,1.8700000000000001,56.07],"marker":{"color":"#318CE7","line":{"color":"rgba(31,119,180,1)"}},"text":["0.93%","28.04%","13.08%","1.87%","56.07%"],"textposition":["outside","outside","outside","outside","outside"],"type":"bar","error_y":{"color":"rgba(31,119,180,1)"},"error_x":{"color":"rgba(31,119,180,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.20000000000000001,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
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


```{=html}
<div class="plotly html-widget html-fill-item" id="htmlwidget-7a7274a3d5856f13ce6c" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-7a7274a3d5856f13ce6c">{"x":{"visdat":{"6330566c6309":["function () ","plotlyVisDat"]},"cur_data":"6330566c6309","attrs":{"6330566c6309":{"labels":{},"values":{},"hoverinfo":"text","textinfo":"label+percent","insidetextfont":{"color":"#FFFFFF"},"text":{},"marker":{"colors":["#318CE7","#89CFF0"],"line":{"color":"#FFFFFF","width":1},"showlegend":false},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"pie"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":"","xaxis":{"showgrid":false,"zeroline":false,"showticklabels":false},"yaxis":{"showgrid":false,"zeroline":false,"showticklabels":false},"hovermode":"closest","showlegend":true},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"labels":["Female","Male"],"values":[58,49],"hoverinfo":["text","text"],"textinfo":"label+percent","insidetextfont":{"color":"#FFFFFF"},"text":["Sex : Female <br>Number of persons : 58 <br>Percentage : 54.21%","Sex : Male <br>Number of persons : 49 <br>Percentage : 45.79%"],"marker":{"color":"rgba(31,119,180,1)","colors":["#318CE7","#89CFF0"],"line":{"color":"#FFFFFF","width":1},"showlegend":false},"type":"pie","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.20000000000000001,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```



## Histogram
A histogram is a chart that plots the distribution of a numeric variable’s values as a series of bars. Each bar typically covers a range of numeric values called a bin or class; a bar’s height indicates the frequency of data points with a value within the corresponding bin.

```r
library(ggplot2)

# Change colors
p<-ggplot(data_1, aes(x=`How many children do you have?`)) + 
  geom_histogram(color="black", fill="white")
p
#> `stat_bin()` using `bins = 30`. Pick better value with
#> `binwidth`.
```

<img src="08-visualization_files/figure-html/unnamed-chunk-4-1.png" width="672" />


## Scatter plot

## Line chart

## Map visualization

## Wordcloud
