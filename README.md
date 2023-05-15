
# The movement of Mazus miquelii stigma under mechanic force
## PSY6422 Yitong Yang 
[Background and research questions](https://github.com/shenyuan27/PSY6422YitongYang_Mazus-miquelii/blob/main/README.md#background-and-research-questions)

[Experiment and Data collection](https://github.com/shenyuan27/PSY6422YitongYang_Mazus-miquelii/blob/main/README.md#experiment-and-data-collection)

[Data visualization](https://github.com/shenyuan27/PSY6422YitongYang_Mazus-miquelii/blob/main/README.md#data-visualization)

[Conclusion](https://github.com/shenyuan27/PSY6422YitongYang_Mazus-miquelii/blob/main/README.md#conclusion)

[Reference](https://github.com/shenyuan27/PSY6422YitongYang_Mazus-miquelii/blob/main/README.md#reference)
## Background and research questions
Mazus miquelii is a species of herbaceous perennial groundcover native to Japan and China.It spreads rapidly by producing significant amounts of slender stolons which root at the nodes. The leaves are undivided and teethed along the margins. The blue or purple flowers are bilateral and have 5 petals，which emerge during the months of June to August. This species is hermaphroditic and is pollinated by insects.
Interestingly, its bilobed stigma will close under mechanic force made by pollinator and may reopen after a visit. Behavior of a sensitive stigma reflects a special relationship between plants and animals by way of pollination.
The behavior of touch-sensitive stigmas closing after being touched by pollinators reflects a pollination relationship between plants and animals, and is considered to be important for plant reproductive success. Therefore, there have been many studies on stigma touch-sensitivity since the Darwin era. The hypothesis of the adaptive significance of is put forward (Darwin, 1876). For example, closure of touch-sensitive stigmas may help reduce stigma exposure to pollen hindrance of export, the promotion of pollen export. Webb and Lloyd (1986) termed this strategy of avoiding male-female interference "movement" herkogamy. Fetscher (2001)’s research on Mimulus aurantiacus confirmed this point of view. He found that the pollinator hummingbird’s flower-visiting behavior will be affected by the opening and closing of the stigma, so the open stigma hinders the output of pollen; but when the stigma is closed, the hummingbird sucks honey at an angle closer to the top of the flower, thus sticking more pollen, and finally the pollen output of the stigma closed is more than twice that of the stigma closed .

![image](https://github.com/shenyuan27/PSY6422YitongYang_Mazus-miquelii/assets/124840282/b914fa50-3f33-4d1c-8869-a1e8ab94d332)


## Experiment and Data collection
In this research, two wild populations were collected from Donghu Botanical Garden (30°31'N, 114°26'E, 70m) in Hongshan District, Wuhan City, Hubei Province in early March 2022, separated by more than 50m. Plants with good growth were selected for potted cultivation and numbered, with 26 pots in the A population and 14 pots in the B population. Placed in a laboratory in good sunlight, isolated from pollinators, watered every two days; used for observation of floral characteristics and stigma behavior.
The closure of the touch sensitive stigma depends on the touch of the pollinator to a large extent. After the stigma is stimulated, it closes rapidly mainly by the movement of the lower lobes. The closure behavior of tactile stigmas has a certain correlation with pollination effectiveness. Only effective pollination can make stigmas close, but it cannot explain the reason why most stigmas close again. In order to compare the differences in stigma touch sensitivity between different populations, this study recorded the closing process of artificial mechanical touching of the stigma. On a sunny afternoon, plants were randomly selected to conduct in vitro experiments on open flowers from the bottom of the inflorescence. Dsam body tone was used for observation and recording (29.96 frames per second), and the center of the lower lobe edge was manually touched with tweezers. In subsequent analysis, the displacement is calculated from the distance from the lower center edge of the lower lobe to the upper center edge of the upper lobe. All stigmas will be observed for pollen falling before measurement, and only stigmas without pollen falling will be selected for measurement.
dataset_mazus.csv contains sample name, the time of movement(frames) totally and each stage,the inflorescence info, and the length of petal. 

![172620235142328101](https://github.com/shenyuan27/desktop-tutorial/assets/124840282/191161d9-4033-430d-a3a7-9472a355ab7c)

## Data visualization

```
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

```
library(ggplot2)
ggplot(data, aes(total_frame, length.of.petal.0.1mm.))+ geom_point(color="gray",size=4)
```
图片



```
# the speed/proportion of each movement stage 
data$begin<-data$onethird_movement/data$total_frame
data$mid<-data$twothird_movement/data$total_frame
data$end<-data$lastthird_movement/data$total_frame
```

```
# clustering by total movement time and petal length (method 1)
library(cluster)
mcluster <- kmeans(data[,c(5,9)], center=3)
clusplot(data, mcluster$cluster, color=T, shade=T, labels=0, lines=0)
data$cluster1<-mcluster$cluster
```
图片

```
ggplot(data,aes(total_frame,length.of.petal.0.1mm., group=cluster1,colour = cluster1)) +geom_point(colour=data$cluster1,size=1)+geom_smooth(method = "loess", se = FALSE)
```
图片

```
# clustering by each movement stage (method 2)
mcluster2 <- kmeans(data[,10:12], center=3)
clusplot(data, mcluster2$cluster, color=T, shade=T, labels=0, lines=0)
data$cluster2<-mcluster2$cluster
```

```
ggplot(data,aes(total_frame,cluster2, group=cluster1,colour = cluster1)) +geom_point(colour=data$cluster2,size=1)+geom_smooth(method = "loess", se = FALSE)
```

```
ggplot(data,aes(total_frame,cluster2)) +geom_point(colour=data$cluster2,size=1,alpha=0.3)
```

```
#analysis with inflorescence
data$inflorescence_total<-data$inflorescence_close+data$inflorescence_open+data$inflorescence_shedding
data$inflorescence_position<-data$inflorescence_total-data$inflorescence_close
ggplot(data,aes(total_frame,inflorescence_total)) +geom_point(colour=data$cluster2,size=2)
ggplot(data,aes(total_frame,inflorescence_position)) +geom_point(colour=data$cluster2,size=2)
```



## Conclusion

## Reference
1.Stigma Sensitivity and the Duration of Temporary Closure Are Affected by Pollinator Identity in Mazus miquelii (Phrymaceae), a Species with Bilobed Stigma. Front. Plant Sci., 10 May 2017 Sec. Plant Development and EvoDevo Volume 8 - 2017 | https://doi.org/10.3389/fpls.2017.00783
2.K-means clustering Cristian Ramos Lorenzo https://rpubs.com/MrCristianrl/504935
