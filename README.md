# Statistics-hw-1-Sofiya-Babok

---
title: "Untitled"
output: github_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## GitHub Documents

This is an R Markdown format used for publishing markdown documents to GitHub. When you click the **Knit** button all R code chunks are run and a markdown file (.md) suitable for publishing to GitHub is generated.

## Including Code

You can include R code in the document as follows:

```{r libraries}
library(data.table)
library(ggplot2)
library(cowplot)
library(ggpubr)
```

## Including Plots

You can also embed plots, for example:

```{r upload_data}
data1 <- fread("file.txt")
data1 <- data1[order(percentage) , ]
data1
```



```{r graph}
ggplot(data1, aes(reorder(label, percentage), percentage))+
     geom_col(aes(fill = mortality_per_100000)) + 
     scale_fill_gradient2(low = "white", 
                       high = "red3", 
                       midpoint = 2)+
     coord_flip() + 
     labs(x = "Type of disease", y = "percentage")+
     theme_cowplot()

```


```{r graph}
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

```{r graph}
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
