---
title: "CaseStudy6"
author: "Exode"
date: "6/2/2020"
output: 
  html_document:
    keep_md: true
---

















```r
ggplot(sc, aes(x=lgID.x,y=salary, color=schoolID))+geom_boxplot(aes(group=schoolID))+labs(x="LeagueID",y="Salary in 2017 U.S.Dollars",title="Comparison Between Baseball Professionals \n Who Attended BYU and those Who Attended Other Colleges in Utah",size="Salary(1K)")+facet_wrap(~schoolID)
```

```
## Warning: Removed 155 rows containing non-finite values (stat_boxplot).
```

![](Case6_files/figure-html/unnamed-chunk-5-1.png)<!-- -->




