Homework 1 by Sofiya Babok
================

## Data

``` r
library(data.table)
library(ggplot2)
library(cowplot)
library(ggpubr)
```

    ## 
    ## Attaching package: 'ggpubr'

    ## The following object is masked from 'package:cowplot':
    ## 
    ##     get_legend

``` r
data1 <- fread("file.txt")
data1 <- data1[order(percentage) , ]
data1
```

    ##                     label percentage mortality_per_100000
    ## 1:                 cancer          3                158.3
    ## 2:     neurologic_disease          5                 32.9
    ## 3:   chronic_lung_disease          9                 35.8
    ## 4: chronic_kidney_disease         16                 59.0
    ## 5: ischemic_heart_disease         26                 73.6
    ## 6:      diabetes_mellitus         35                 20.9
    ## 7:           hypertension         41                 11.1

\#\#Plots

``` r
ggplot(data1, aes(reorder(label, percentage), percentage))+
     geom_col(aes(fill = mortality_per_100000)) + 
     scale_fill_gradient2(low = "white", 
                       high = "red3", 
                       midpoint = 2)+
     coord_flip() + 
     labs(x = "Type of disease", y = "percentage")+
     theme_cowplot()
```

![](README_files/figure-gfm/graph%201-1.png)<!-- -->

``` r
n = mean(data1$mortality_per_100000)
label1 = paste("average",round(n,2))
ggplot(data1, aes(reorder(label, mortality_per_100000), mortality_per_100000))+
     geom_bar(stat="identity", fill = "skyblue2") + 
     geom_text(aes(label= mortality_per_100000), position=position_dodge(width=0.9), vjust=-0.25)+
     labs(x = "Type of disease", y = "mortality per 100000")+
     ylim(0,170)+
     geom_hline(yintercept=n, linetype="dashed")+
     geom_text(aes(1,n,label = label1, vjust = -0.5))+   
     theme_cowplot()+
     theme(axis.text.x = element_text(angle = 60, hjust = 1))
```

![](README_files/figure-gfm/graph%202-1.png)<!-- -->

``` r
h = mean(data1$percentage)
labell = paste('average',round(h,2))
ggplot(data1, aes(reorder(label, percentage), percentage))+
     geom_bar(stat="identity", fill = "red3") + 
     geom_text(aes(label= percentage), position=position_dodge(width=0.9), vjust=-0.25)+
     labs(x = "Type of disease", y = "percentage")+
     ylim(0,44)+
     geom_hline(yintercept=h, linetype="dashed")+
     geom_text(aes(1,h,label = labell, vjust = -0.5))+
     theme_cowplot()+
     theme(axis.text.x = element_text(angle = 60, hjust = 1))
```

![](README_files/figure-gfm/graph%203-1.png)<!-- -->
