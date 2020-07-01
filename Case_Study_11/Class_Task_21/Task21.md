---
title: "Task 21"
author: "Exode"
date: "6/28/2020"
output: 
  html_document:
    keep_md: true
---




```r
citation("USAboundaries")
```

```
## 
## To cite the USAboundaries package in publications, please cite the
## paper in the Journal of Open Source Software:
## 
##   Lincoln A. Mullen and Jordan Bratt, "USAboundaries: Historical and
##   Contemporary Boundaries of the United States of America," Journal of
##   Open Source Software 3, no. 23 (2018): 314,
##   https://doi.org/10.21105/joss.00314.
## 
## A BibTeX entry for LaTeX users is
## 
##   @Article{,
##     title = {{USAboundaries}: Historical and Contemporary Boundaries
## of the United States of America},
##     author = {Lincoln A. Mullen and Jordan Bratt},
##     journal = {Journal of Open Source Software},
##     year = {2018},
##     volume = {3},
##     issue = {23},
##     pages = {314},
##     url = {https://doi.org/10.21105/joss.00314},
##     doi = {10.21105/joss.00314},
##   }
```


```r
states_2020 <- us_cities()
```

```
## City populations for contemporary data come from the 2010 census.
```

```r
y<-states_2020 %>% extract(geometry, c("Latitude", "Longitude"), "\\(([^,]+), ([^)]+)\\)")
y1 <- st_as_sf(y)
states_20 <- us_states()
states_2<-subset(states_20,state_name!="Alaska"&state_name!="Hawaii"&state_name!= "Puerto Rico")
st <- us_counties(state="idaho")


t <-as.data.frame(states_2020 %>%
group_by(state_name) %>% top_n(3,population))
t2<-st_as_sf(t)
t3 <- subset(t2,state_name!="Alaska"&state_name!="Hawaii"&state_name!= "Puerto Rico")

t3$population<-t3$population/1000
t4 <-as.data.frame(t3 %>%
group_by(state_name) %>% top_n(1,population))
t5<-st_as_sf(t4)
```

```r
m <- ggplot()+geom_sf(data=states_2,fill=NA,size=5)+geom_sf(data=t3,aes(color=city),show.legend = FALSE)+geom_sf(data=st,fill=NA)+geom_point(data=t3,aes(size=population,geometry=geometry),stat="sf_coordinates")+theme_bw(base_size = 120)+scale_size_continuous(range = c(30, 50))+labs(size="Population (1000)",title="U.S Map with the Three Biggest Cities in Each State")+theme(axis.title.x = element_blank(),
          axis.title.y = element_blank())+  geom_sf_label(data=t5,aes(label = city), size=22,color="blue",label.padding = unit(10, "mm"),fontface="bold")
m
```

```
## Warning in st_point_on_surface.sfc(sf::st_zm(x)): st_point_on_surface may not
## give correct results for longitude/latitude data

## Warning in st_point_on_surface.sfc(sf::st_zm(x)): st_point_on_surface may not
## give correct results for longitude/latitude data
```

![](Task21_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
ggsave('~/saved_image.png', width = 40, height = 20, dpi = 200)
```

```
## Warning in st_point_on_surface.sfc(sf::st_zm(x)): st_point_on_surface may not
## give correct results for longitude/latitude data

## Warning in st_point_on_surface.sfc(sf::st_zm(x)): st_point_on_surface may not
## give correct results for longitude/latitude data
```
