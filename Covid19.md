
## Team 11 
## By: Jesina Dangol
## What have we Learned from Last Pandemic ?: Covid-19

A pandemic is a worldwide outbreak of a virus that is distinct from circulating viruses and evolves over time. 

COVID-19 has been one of the deadliest pandemics we've seen in the last decade, and I'll go into more detail about it in the pictures below.

Data source: [https://covid.cdc.gov/covid-data-tracker/?CDC_AA_refVal=https%3A%2F%2Fwww.cdc.gov%2Fcoronavirus%2F2019-ncov%2Fcases-in-us.html#trends_dailycases](https://covid.cdc.gov/covid-data-tracker/?CDC_AA_refVal=https%3A%2F%2Fwww.cdc.gov%2Fcoronavirus%2F2019-ncov%2Fcases-in-us.html#trends_dailycases)
[https://covid.cdc.gov/covid-data-tracker/?CDC_AA_refVal=https%3A%2F%2Fwww.cdc.gov%2Fcoronavirus%2F2019-ncov%2Fcases-in-us.html#trends_dailydeaths](https://covid.cdc.gov/covid-data-tracker/?CDC_AA_refVal=https%3A%2F%2Fwww.cdc.gov%2Fcoronavirus%2F2019-ncov%2Fcases-in-us.html#trends_dailydeaths)

Link: [Dashboard](https://public.tableau.com/app/profile/jesina.dangol/viz/Covid19_Visuals_Final/CovidTest?publish=yes)


```python
import pandas as pd 
import numpy as np
from bokeh.plotting import figure,show
from bokeh.models.tools import HoverTool
from bokeh.models import ColumnDataSource,DatetimeTickFormatter,NumeralTickFormatter
import matplotlib.pyplot as plt
from bokeh.layouts import column
from bokeh.io import curdoc,output_notebook
from bokeh.core.properties import value

df = pd.read_csv('covid19.csv', index_col=0, parse_dates=True)
df = df.dropna()

df1 = pd.read_csv('Covid_death_trend.csv', index_col=0, parse_dates=True) 

death = ColumnDataSource(df1)
case = ColumnDataSource(df)


```


```python
p = figure(title="US COVID-19 Total Cases", x_axis_label="Year", y_axis_label="Number of COVID-19 Cases")
p.line(x= 'Date',y= 'New Cases',source=case, line_width=2,legend=value("New Cases"))
p.line(x= 'Date',y= '7-Day Moving Avg',source=case,line_color="red", line_width=2,legend=value("7-Day Moving Avg"))

hover = HoverTool(
    tooltips=[
    ("New Cases", "@{New Cases}{0,0}"),
    ("7-Day Moving Avg", "@{7-Day Moving Avg}{0,0}"),
    ("Date", "@Date{%Y-%m-%d}"),
    ],
    formatters = {
        "Date": "datetime"
        
        ""
    }
   
)


p.yaxis.formatter = NumeralTickFormatter(format="0,00")
p.xaxis.formatter = DatetimeTickFormatter(months="%b %Y")
p.add_tools(hover)


p1 = figure(title="US COVID-19 Death Cases", x_axis_label="Year", y_axis_label="Number of Death Cases")
p1.line(x= 'Date',y= 'New Deaths',source=death,line_color="grey", line_width=2,legend=value("Deaths"))
p1.line(x= 'Date',y= '7-Day Moving Avg',source=death,line_color="red", line_width=2,legend=value("7-Day Moving Avg"))

h1 = HoverTool(
    tooltips=[
    ("New Death", "@{New Deaths}{0,0}"),
    ("7-Day Moving Avg", "@{7-Day Moving Avg}{0,0}"),
    ("Date", "@Date{%Y-%m-%d}"),
    ],
    formatters = {
        "Date": "datetime"
        
        ""
    }
   
)
p1.yaxis.formatter = NumeralTickFormatter(format="0,00")
p1.xaxis.formatter = DatetimeTickFormatter(months="%b %Y")
p1.add_tools(h1)


output_notebook()

```



    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="1141">Loading BokehJS ...</span>
    </div>





```python
show(column(p,p1))
```








  <div class="bk-root" id="4734768f-3068-4c6c-85a1-b708dd284031"></div>





The Above line graphs shows timeline trends for Cases and Deaths since COVID-19 started in the United States.


```python
%%HTML 
<div class='tableauPlaceholder' id='viz1652048698055' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Co&#47;Covid19_Visuals_Final&#47;CovidTest&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Covid19_Visuals_Final&#47;CovidTest' /><param name='tabs' value='yes' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Co&#47;Covid19_Visuals_Final&#47;CovidTest&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /><param name='filter' value='publish=yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1652048698055');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1000px';vizElement.style.height='850px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1000px';vizElement.style.height='850px';} else { vizElement.style.width='100%';vizElement.style.height='1150px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>
```


<div class='tableauPlaceholder' id='viz1652048698055' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Co&#47;Covid19_Visuals_Final&#47;CovidTest&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Covid19_Visuals_Final&#47;CovidTest' /><param name='tabs' value='yes' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Co&#47;Covid19_Visuals_Final&#47;CovidTest&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /><param name='filter' value='publish=yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1652048698055');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1000px';vizElement.style.height='850px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1000px';vizElement.style.height='850px';} else { vizElement.style.width='100%';vizElement.style.height='1150px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>


