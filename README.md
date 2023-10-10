
# The movement of Mazus miquelii stigma under mechanic force
## PSY6422 220241465

## 1.Project introduction

### 1.1Background and research questions
Mazus miquelii is a species of herbaceous perennial groundcover native to Japan and China.It spreads rapidly by producing significant amounts of slender stolons which root at the nodes. The leaves are undivided and teethed along the margins. The blue or purple flowers are bilateral and have 5 petals，which emerge during the months of June to August. This species is hermaphroditic and is pollinated by insects.
Interestingly, its bilobed stigma will close under mechanic force made by pollinator and may reopen after a visit. Behavior of a sensitive stigma reflects a special relationship between plants and animals by way of pollination.
The behavior of touch-sensitive stigmas closing after being touched by pollinators reflects a pollination relationship between plants and animals, and is considered to be important for plant reproductive success. Therefore, there have been many studies on stigma touch-sensitivity since the Darwin era. The hypothesis of the adaptive significance of is put forward (Darwin, 1876). For example, closure of touch-sensitive stigmas may help reduce stigma exposure to pollen hindrance of export, the promotion of pollen export. Webb and Lloyd (1986) termed this strategy of avoiding male-female interference "movement" herkogamy. Fetscher (2001)’s research on Mimulus aurantiacus confirmed this point of view. He found that the pollinator hummingbird’s flower-visiting behavior will be affected by the opening and closing of the stigma, so the open stigma hinders the output of pollen; but when the stigma is closed, the hummingbird sucks honey at an angle closer to the top of the flower, thus sticking more pollen, and finally the pollen output of the stigma closed is more than twice that of the stigma closed .

![image](https://github.com/shenyuan27/PSY6422YitongYang_Mazus-miquelii/assets/124840282/b914fa50-3f33-4d1c-8869-a1e8ab94d332)


# 1.2Experiment and Data collection
The data comes from my undergraduate thesis, and the data can be queried in the Wuhan University thesis database.（https://www.lib.whu.edu.cn/web/index.asp?obj_id=313）This is also part of a follow-up study to Reference 1.
In this research, two wild populations were collected from Donghu Botanical Garden (30°31'N, 114°26'E, 70m) in Hongshan District, Wuhan City, Hubei Province in early March 2022, separated by more than 50m. Plants with good growth were selected for potted cultivation and numbered, with 26 pots in the A population and 14 pots in the B population. Placed in a laboratory in good sunlight, isolated from pollinators, watered every two days; used for observation of floral characteristics and stigma behavior.
The closure of the touch sensitive stigma depends on the touch of the pollinator to a large extent. After the stigma is stimulated, it closes rapidly mainly by the movement of the lower lobes. The closure behavior of tactile stigmas has a certain correlation with pollination effectiveness. Only effective pollination can make stigmas close, but it cannot explain the reason why most stigmas close again. In order to compare the differences in stigma touch sensitivity between different populations, this study recorded the closing process of artificial mechanical touching of the stigma. On a sunny afternoon, plants were randomly selected to conduct in vitro experiments on open flowers from the bottom of the inflorescence. Dsam body tone was used for observation and recording (29.96 frames per second), and the center of the lower lobe edge was manually touched with tweezers. In subsequent analysis, the displacement is calculated from the distance from the lower center edge of the lower lobe to the upper center edge of the upper lobe. All stigmas will be observed for pollen falling before measurement, and only stigmas without pollen falling will be selected for measurement.
dataset_mazus.csv contains sample name, the time of movement(frames) totally and each stage,the inflorescence info, and the length of petal. 

![172620235142328101](https://github.com/shenyuan27/desktop-tutorial/assets/124840282/191161d9-4033-430d-a3a7-9472a355ab7c)


## 2 Data visualization

### 2.1 Overview: Histogram shows the corolla length, inflorescence position and stigma closure time of the samples


```{r, fig.height = 8,fig.with = 6}
data <- read.csv(file="dataset_mazus.csv")
head(data)
```

```
                 filename onethird_movement twothird_movement lastthird_movement total_frame inflorescence_close
1 VID_20220405_144933.mp4               190               120                255         565                   1
2 VID_20220405_145131.mp4                72                58                172         302                   1
3 VID_20220405_145540.mp4                86                66                107         259                   2
4 VID_20220405_145650.mp4                52                47                 97         196                   2
5 VID_20220405_145937.mp4                73                64                123         260                   2
6 VID_20220405_151235.mp4               131               103                245         479                   0
```

```{r, fig.height = 8,fig.with = 6}
library(ggplot2)

data$inflorescence_total<-data$inflorescence_close+data$inflorescence_open+data$inflorescence_shedding
data$inflorescence_position<-data$inflorescence_total-data$inflorescence_close
data$inflorescence_position_p<-data$inflorescence_position/data$inflorescence_total

ggplot(data, aes(x=total_frame)) +
    geom_histogram(binwidth = 50, fill = "lightblue", color = "black") +
    labs(title = "Histogram of stigma closing time (number of frames)", x = "Frequency", y = "Value") +
    xlim(0, 750)

ggplot(data, aes(x=length.of.petal.0.1mm.)) +
    geom_histogram(binwidth = 10, fill = "lightblue", color = "black") +
    labs(title = "Histogram of petal widths", x = "Frequency", y = "Value") +
    xlim(0, 200)

ggplot(data, aes(x=inflorescence_position)) +
    geom_histogram(binwidth = 1, fill = "lightblue", color = "black") +
    labs(title = "Histogram of inflorescence position", x = "Frequency", y = "Value") +
    xlim(0, 20)

```
![(M)NAXQ )G@K8W0`85U6Z3X](https://github.com/shenyuan27/PSY6422_220241465_Mazus-miquelii_improve/assets/124840282/bc089d60-a88b-445a-9b22-f9455da5e1cc)

![6`%TOSCQFD VPS@`AS~Y}I](https://github.com/shenyuan27/PSY6422_220241465_Mazus-miquelii_improve/assets/124840282/fecb3cd9-af44-4789-aa0a-6f76841e3da1)

![8FW24(E0ONATU4FC@FYQ2XR](https://github.com/shenyuan27/PSY6422_220241465_Mazus-miquelii_improve/assets/124840282/115c06a3-4a9d-473d-af97-ac2ba2fecc60)


Here, the three most important variables of each sample (that is, the stigma of each flower) in the experiment are displayed through a histogram: the time when the stigma closes, the position on the inflorescence, and the width of the petals. In nature, different pollinators may have different priorities for visiting flowers due to the shape of the petals or the position of the inflorescence (such as closer to the top).


### 2.2 Correlation analysis between stigma closure time, corolla length and inflorescence position

```{r, fig.height = 8,fig.with = 6}
ggplot(data, aes(total_frame, length.of.petal.0.1mm.))+ geom_point(color="gray",size=4) +
    labs(title = "Scatter plot of petal length and stigma closure time", x = "stigma closing time(frames)", y = "petal length")


#ggplot(data, aes(inflorescence_position_p, length.of.petal.0.1mm.))+ geom_point(color="gray",size=4) +
#    labs(title = "Scatter plot of petal length and inflorescence position", x = "inflorescence position", y = "petal length")

ggplot(data, aes(inflorescence_position_p, total_frame))+ geom_point(color="gray",size=4) +
    labs(title = "Scatter plot of petal length and inflorescence position", x = "inflorescence position", y = "stigma closing time(frames)")

```
![SYE3C F~@ K1K$B85T$L903](https://github.com/shenyuan27/PSY6422_220241465_Mazus-miquelii_improve/assets/124840282/eb53e871-ea7d-4ce6-ac69-47e4a025734a)

![M }GMQ$9`MJZM`729G8)Q2C](https://github.com/shenyuan27/PSY6422_220241465_Mazus-miquelii_improve/assets/124840282/1a0cf851-7f4b-406f-9c65-fab4884c8db1)


```{r, fig.height = 8,fig.with = 6}
# the speed/proportion of each movement stage 
data$begin<-data$onethird_movement/data$total_frame
data$mid<-data$twothird_movement/data$total_frame
data$end<-data$lastthird_movement/data$total_frame
# clustering by total movement time and petal length (method 1)
library(cluster)
mcluster <- kmeans(data[,c(5,9)], center=3)
clusplot(data, mcluster$cluster, color=T, shade=T, labels=0, lines=0)
data$cluster1<-mcluster$cluster


```
![3L@}E_{T0KAS F_E5F`5(5D](https://github.com/shenyuan27/PSY6422_220241465_Mazus-miquelii_improve/assets/124840282/0dce65d8-45a5-4336-b054-892ca291f0dc)


```{r, fig.height = 8,fig.with = 6}

ggplot(data,aes(total_frame,length.of.petal.0.1mm., group=cluster1,colour = cluster1)) +geom_point(colour=data$cluster1,size=3)+
    labs(title = "Scatter plot of petal length and stigma closure time based on cluster analysis", x = "stigma closing time(frames)", y = "petal length")


```
![PC3T(NB`92_1S9{)1K0WYTE](https://github.com/shenyuan27/PSY6422_220241465_Mazus-miquelii_improve/assets/124840282/d2b64458-090c-4ffa-8019-36c4b7b9a49d)




```{r, fig.height = 8,fig.with = 6}

correlation <- cor(data$inflorescence_position_p, data$total_frame)

cat("Pearson correlation between inflorescence position and stigma closure time:", correlation, "\n")

correlation <- cor(data$length.of.petal.0.1mm., data$total_frame)

cat("Pearson correlation between petal width and stigma closure time:", correlation, "\n")

```

```
Pearson correlation between inflorescence position and stigma closure time: 0.268913 
Pearson correlation between petal width and stigma closure time: -0.2166247 
```

It can be found that there is a weak positive correlation between the stigma closing time and the position of the inflorescence, that is, the closer to the bottom of the inflorescence, the longer the closing time; and there is a weak negative correlation with the petal width, the smaller the petal, the shorter the closing time.

### 2.3 Classify the movement patterns of stigma closure


```{r, fig.height = 8,fig.with = 6}

mcluster2 <- kmeans(data[,13:15], center=3)
clusplot(data, mcluster2$cluster, color=T, shade=T, labels=0, lines=0)
data$cluster2<-mcluster2$cluster

```



```{r, fig.height = 8,fig.with = 6}

library(rgl)
plot3d(data$onethird_movement, data$twothird_movement, data$lastthird_movement, type = "s", col = "blue", size = 3,xlab ="onethird_movement", 
       ylab = "twothird_movement", zlab = "lastthird_movement")

play3d(spin3d(axis = c(0.5,0.5,0.5), rpm = 4),duration = 100)

```
![3](https://github.com/shenyuan27/PSY6422_220241465_Mazus-miquelii_improve/assets/124840282/f93805fb-8cea-41b8-aa1d-aa859283d476)



```{r, fig.height = 8,fig.with = 6}
data$cluster2<-as.character(data$cluster2)

ggplot(data,aes(onethird_movement,lastthird_movement, group=cluster2,colour = cluster2)) +geom_point(colour=data$cluster2,size=2)+geom_smooth(method = "loess",se = FALSE) +
  scale_color_manual(values = c("1" = "blue", "2" = "cyan","3" = "purple"))

```
![PSY1](https://github.com/shenyuan27/PSY6422_220241465_Mazus-miquelii_improve/assets/124840282/b37be078-95e3-4102-89af-e8b42540dbde)


In this experiment, the time spent in the front, middle, and back segments of each stigma closure was also counted; described here as onethird_movement, twothird_movement, and lastthird_movement. It can be observed in the three-dimensional scatter plot that, just like the total time, there are large differences in the movement patterns in different samples. Here, through cluster analysis, the movement patterns are divided into three categories, which can be described as fast first and then slow (onethird_movement value is small), moderate speed, slow first and then fast (onethird_movement value is large). It also shows that three motion patterns exist regardless of whether the total time is long or short.

```{r, fig.height = 8,fig.with = 6}

ggplot(data,aes(inflorescence_position_p, length.of.petal.0.1mm., group=cluster2,colour = cluster2)) +geom_point(colour=data$cluster2,size=3)+labs(title = "Scatter plot of petal length and inflorescence position", x = "inflorescence position", y = "petal length")

```
![UG VHWV5L}N 8HQ}(FXQ(QA](https://github.com/shenyuan27/PSY6422_220241465_Mazus-miquelii_improve/assets/124840282/ac81b265-5eb1-4766-9c8b-89af6c7c69be)


Unfortunately, the movement pattern of stigma closure does not appear to be clearly related to inflorescence position and petal width.But this may be related to ecological adaptation strategies, such as the existence of deliberately random genotypes, which requires more research to explain.


## 3.Conclusion
According to 2.3 , it can be observed that the stigma of mazus miquelli may have significantly different movement patterns in different individuals, and this pattern has no obvious relationship with the total movement time or corolla length.
From the analysis of the combination of inflorescence and movement characteristics, the total movement time of the inflorescence with less flowering (this is related to the plant microenvironment such as sunlight, water, insect pests, etc., and may also be related to genotype) is shorter. From the perspective of experimental improvement, flowering time and inflorescence growth time can be included in the records to obtain more convincing evidence on the ecological significance and adaptability of stigma behavior to plants.

## Reference
1.Stigma Sensitivity and the Duration of Temporary Closure Are Affected by Pollinator Identity in Mazus miquelii (Phrymaceae), a Species with Bilobed Stigma. Front. Plant Sci., 10 May 2017 Sec. Plant Development and EvoDevo Volume 8 - 2017 | https://doi.org/10.3389/fpls.2017.00783
2.K-means clustering Cristian Ramos Lorenzo https://rpubs.com/MrCristianrl/504935



