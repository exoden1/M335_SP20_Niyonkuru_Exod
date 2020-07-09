---
title: "Case11"
author: "Exode"
date: "7/9/2020"
output: 
  html_document:
    keep_md: true
    toc: true
    toc_float: true
    fig_caption: true
---



```r
#r<-(devtools::install_github("hathawayj/buildings",force=TRUE))
r<-buildings::permits

states<-us_states()

s <- inner_join(r,states,by=c("StateAbbr"="state_abbr"))

s1 <- s %>%  group_by(StateAbbr,year,variable) %>% summarise(total=sum(value))
```

```
## `summarise()` regrouping output by 'StateAbbr', 'year' (override with `.groups` argument)
```

```r
s2 <- subset(s1,variable=="Single Family")
```


```r
p<-ggplot(s2, aes(x=year, y=total,size=total)) +
  geom_line() +
  facet_geo(~ StateAbbr,grid = "us_state_grid2") +scale_x_continuous(labels = function(x) paste0("", substr(x, 3, 4))) +
  
  labs(y="Single Family Permits",size="",title="Single Family Permits across the USA (1980-2010)")+theme_bw(base_size=20)+theme(axis.text=element_text(size=28),
        axis.title=element_text(size=32,face="bold"))+theme(strip.text.x = element_text(size = 26, colour = "blue"))+theme(legend.position="top",legend.text = element_text(colour="blue", size=40, 
                                     face="bold"))
```



## Summary

Between 2007 and 2009, the number of single family decreased in all states. That was in partly to the financial crisis that was going on during that time.

