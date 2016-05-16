---
title: "1928-1969間，小兒麻痺在美國各州的發生率變化"
output: github_document
--

##次標題1:
#讀進資料

```{r setup, include=FALSE}
polio <- read.csv("POLIO_Incidence.csv",stringsAsFactors = F)
head(polio)
knitr::opts_chunk$set(echo = TRUE)
```


```{r}
install.packages("reshape")
library(reshape)
install.packages("ggplot2")
library(ggplot2)
library(knitr)
```

#寬表格轉為長表格

```{r}
polio.m<-melt(polio,id.vars = c('YEAR','WEEK'))
head(polio.m,15)
kable(head(polio.m))
```
| YEAR| WEEK|variable |value |
|----:|----:|:--------|:-----|
| 1928|    1|ALABAMA  |0     |
| 1928|    2|ALABAMA  |0     |
| 1928|    3|ALABAMA  |0.04  |
| 1928|    4|ALABAMA  |0     |
| 1928|    5|ALABAMA  |0     |
| 1928|    6|ALABAMA  |0     |


#處理缺值&計算年度發生率

```{r}
polio.m[polio.m$value=="-",]$value<-NA 
polio.m$value<-as.numeric(as.character(polio.m$value)) 
polio.sumYear<- 
    aggregate(value~YEAR+variable,data=polio.m,FUN=sum,na.rm=F)
head(polio.sumYear)
kable(head(polio.sumYear))
```
| YEAR|variable | value|
|----:|:--------|-----:|
| 1928|ALABAMA  |  2.39|
| 1929|ALABAMA  |  2.25|
| 1930|ALABAMA  |  2.57|
| 1931|ALABAMA  |  2.07|
| 1932|ALABAMA  |  1.38|
| 1933|ALABAMA  |  1.12|


#次標題2：視覺畫呈現

#程式碼

```{r}
ggplot(polio.sumYear)+ 
    geom_line(aes(x=YEAR,y=value,color=variable))+
    geom_vline(xintercept = 1955,colour="black", linetype = "longdash")

```

解釋如何選擇圖形種類:
這次要同時在圖表上呈現的量有3個，分別是小兒麻痺發生率、年與美國各州。常用的圖表有柱狀圖、圓餅圖與折線圖，由於要同時呈現3個量所以柱狀圖、圓餅圖不適合用來呈現圖表，故以折線圖來表示。

解釋圖形:1955年以前小兒麻痺發生率時高時低，而在開始施打疫苗之後小兒麻痺發生率有明顯的降低的趨勢。

img src="Rplot.png" width="600px"

## GitHub Documents

This is an R Markdown format used for publishing markdown documents to GitHub. When you click the **Knit** button all R code chunks are run and a markdown file (.md) suitable for publishing to GitHub is generated.

## Including Code

You can include R code in the document as follows:

```{r cars}
summary(cars)
```

## Including Plots

You can also embed plots, for example:

```{r pressure, echo=FALSE}
plot(pressure)
```

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
