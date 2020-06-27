---
title: 'Case Study 2: Wealth and Life Expectancy (Gapminder)'
author: "Exode"
date: "5/2/2020"
output: 
  html_document:
    keep_md: true
---


## Background

In this case study, I learned how to use facet_grid() and facet_wrap()


```r
gap <- filter(gapminder, country !="Kuwait")
gap$Population <- gap$pop/100000
```


```r
p<- ggplot(data = gap, mapping = aes(x = lifeExp, y = gdpPercap)) + geom_point(mapping = aes(color = continent, size = Population))+
  facet_grid(~ year) + theme_bw() +scale_y_continuous(trans = "sqrt")
p
```

![](CaseStudy2_files/figure-html/unnamed-chunk-3-1.png)<!-- -->


```r
gap1 <- gap %>% group_by(continent,year) %>% summarise(mean= weighted.mean(gdpPercap),pop=mean(Population))
```

```
## `summarise()` regrouping output by 'continent' (override with `.groups` argument)
```

```r
gap1
```

```
## # A tibble: 60 x 4
## # Groups:   continent [5]
##    continent  year  mean   pop
##    <fct>     <int> <dbl> <dbl>
##  1 Africa     1952 1253.  45.7
##  2 Africa     1957 1385.  50.9
##  3 Africa     1962 1598.  57.0
##  4 Africa     1967 2050.  64.5
##  5 Africa     1972 2340.  73.1
##  6 Africa     1977 2586.  83.3
##  7 Africa     1982 2482.  96.0
##  8 Africa     1987 2283. 111. 
##  9 Africa     1992 2282. 127. 
## 10 Africa     1997 2379. 143. 
## # ... with 50 more rows
```

```r
gap <- filter(gapminder, country !="Kuwait")
gap$Population <- gap$pop/40000
```



```r
ggplot(data = gap1,aes(year, mean))+geom_point(aes(color = continent, size =pop))+facet_wrap(~continent) + theme_bw() +scale_y_continuous(trans = "sqrt")+geom_path(aes(linetype=continent))
```

![](CaseStudy2_files/figure-html/unnamed-chunk-5-1.png)<!-- -->


```r
ggplot(gap, aes(x=year,y=gdpPercap,color=continent))+labs(y="GDP per Cap")+geom_point(mapping=aes(size=Population))+facet_wrap(~continent)+geom_line(aes(x=year,y=gdpPercap,group=country))+theme_bw()+geom_line(data=gap1,aes(y=mean),color="black")+geom_point(data=gap1, aes(y=mean),color="black")+scale_y_continuous(trans = "sqrt")
```

![](CaseStudy2_files/figure-html/unnamed-chunk-6-1.png)<!-- -->



```r
gap1 <- gap %>% group_by(continent) %>% summarise(mean= weighted.mean(gdpPercap))
```

```
## `summarise()` ungrouping output (override with `.groups` argument)
```

```r
gap1
```

```
## # A tibble: 5 x 2
##   continent   mean
##   <fct>      <dbl>
## 1 Africa     2194.
## 2 Americas   7136.
## 3 Asia       6107.
## 4 Europe    14469.
## 5 Oceania   18622.
```



```r
gap <- filter(gapminder, country !="Kuwait")
gap$Population <- gap$pop/40000
ggplot(data = gap,aes(year, gdpPercap))+geom_point(aes(color = continent, size = Population))+facet_wrap(~continent) + theme_bw() +scale_y_continuous(trans = "sqrt")+geom_path(aes(linetype=continent))
```

![](CaseStudy2_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

