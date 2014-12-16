# peer assesment2
Student  
Monday, December 15, 2014  

##Reproducible Research: Peer Assessment 2

Title: Impact of Severe Weather Events on Public Health and Economy in the United States


Synopsis:
1. Excessive heat and tornado were the main weather related most harmful events to public health such as fatalities and injuries.
2. Wind and Flood related weather events were the main weather events that caused major economic losses.

Data Processing:
#Analyses:

The main aim of this analyses is to assess the different weather events in USA on public health and economy.  This data was collected from U.S. National Oceanic and Atmospheric Administration's (NOAA) from 1950 - 2011.

library(knitr)
setwd("~/R/R_lectures/Data_cousera/reproducible/)
knit(paste0(Peer_assessment2, ".Rmd"), encoding = "utf-8")
system(paste0("pandoc -o ", Peer_assessment2, ".docx ", Peer_assessment2, ".md"))
download.file("https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2FStormData.csv.bz2","~/R/R_lectures/Data_cousera/reproducible/storm_data.zip")


```r
storm_data <- read.csv("~/R/R_lectures/Data_cousera/reproducible/storm_data.zip")
head(storm_data)
```

```
##   STATE__           BGN_DATE BGN_TIME TIME_ZONE COUNTY COUNTYNAME STATE
## 1       1  4/18/1950 0:00:00     0130       CST     97     MOBILE    AL
## 2       1  4/18/1950 0:00:00     0145       CST      3    BALDWIN    AL
## 3       1  2/20/1951 0:00:00     1600       CST     57    FAYETTE    AL
## 4       1   6/8/1951 0:00:00     0900       CST     89    MADISON    AL
## 5       1 11/15/1951 0:00:00     1500       CST     43    CULLMAN    AL
## 6       1 11/15/1951 0:00:00     2000       CST     77 LAUDERDALE    AL
##    EVTYPE BGN_RANGE BGN_AZI BGN_LOCATI END_DATE END_TIME COUNTY_END
## 1 TORNADO         0                                               0
## 2 TORNADO         0                                               0
## 3 TORNADO         0                                               0
## 4 TORNADO         0                                               0
## 5 TORNADO         0                                               0
## 6 TORNADO         0                                               0
##   COUNTYENDN END_RANGE END_AZI END_LOCATI LENGTH WIDTH F MAG FATALITIES
## 1         NA         0                      14.0   100 3   0          0
## 2         NA         0                       2.0   150 2   0          0
## 3         NA         0                       0.1   123 2   0          0
## 4         NA         0                       0.0   100 2   0          0
## 5         NA         0                       0.0   150 2   0          0
## 6         NA         0                       1.5   177 2   0          0
##   INJURIES PROPDMG PROPDMGEXP CROPDMG CROPDMGEXP WFO STATEOFFIC ZONENAMES
## 1       15    25.0          K       0                                    
## 2        0     2.5          K       0                                    
## 3        2    25.0          K       0                                    
## 4        2     2.5          K       0                                    
## 5        2     2.5          K       0                                    
## 6        6     2.5          K       0                                    
##   LATITUDE LONGITUDE LATITUDE_E LONGITUDE_ REMARKS REFNUM
## 1     3040      8812       3051       8806              1
## 2     3042      8755          0          0              2
## 3     3340      8742          0          0              3
## 4     3458      8626          0          0              4
## 5     3412      8642          0          0              5
## 6     3450      8748          0          0              6
```

```r
summary(storm_data)
```

```
##     STATE__                  BGN_DATE             BGN_TIME     
##  Min.   : 1.0   5/25/2011 0:00:00:  1202   12:00:00 AM: 10163  
##  1st Qu.:19.0   4/27/2011 0:00:00:  1193   06:00:00 PM:  7350  
##  Median :30.0   6/9/2011 0:00:00 :  1030   04:00:00 PM:  7261  
##  Mean   :31.2   5/30/2004 0:00:00:  1016   05:00:00 PM:  6891  
##  3rd Qu.:45.0   4/4/2011 0:00:00 :  1009   12:00:00 PM:  6703  
##  Max.   :95.0   4/2/2006 0:00:00 :   981   03:00:00 PM:  6700  
##                 (Other)          :895866   (Other)    :857229  
##    TIME_ZONE          COUNTY         COUNTYNAME         STATE       
##  CST    :547493   Min.   :  0   JEFFERSON :  7840   TX     : 83728  
##  EST    :245558   1st Qu.: 31   WASHINGTON:  7603   KS     : 53440  
##  MST    : 68390   Median : 75   JACKSON   :  6660   OK     : 46802  
##  PST    : 28302   Mean   :101   FRANKLIN  :  6256   MO     : 35648  
##  AST    :  6360   3rd Qu.:131   LINCOLN   :  5937   IA     : 31069  
##  HST    :  2563   Max.   :873   MADISON   :  5632   NE     : 30271  
##  (Other):  3631                 (Other)   :862369   (Other):621339  
##                EVTYPE         BGN_RANGE       BGN_AZI      
##  HAIL             :288661   Min.   :   0          :547332  
##  TSTM WIND        :219940   1st Qu.:   0   N      : 86752  
##  THUNDERSTORM WIND: 82563   Median :   0   W      : 38446  
##  TORNADO          : 60652   Mean   :   1   S      : 37558  
##  FLASH FLOOD      : 54277   3rd Qu.:   1   E      : 33178  
##  FLOOD            : 25326   Max.   :3749   NW     : 24041  
##  (Other)          :170878                  (Other):134990  
##          BGN_LOCATI                  END_DATE             END_TIME     
##               :287743                    :243411              :238978  
##  COUNTYWIDE   : 19680   4/27/2011 0:00:00:  1214   06:00:00 PM:  9802  
##  Countywide   :   993   5/25/2011 0:00:00:  1196   05:00:00 PM:  8314  
##  SPRINGFIELD  :   843   6/9/2011 0:00:00 :  1021   04:00:00 PM:  8104  
##  SOUTH PORTION:   810   4/4/2011 0:00:00 :  1007   12:00:00 PM:  7483  
##  NORTH PORTION:   784   5/30/2004 0:00:00:   998   11:59:00 PM:  7184  
##  (Other)      :591444   (Other)          :653450   (Other)    :622432  
##    COUNTY_END COUNTYENDN       END_RANGE      END_AZI      
##  Min.   :0    Mode:logical   Min.   :  0          :724837  
##  1st Qu.:0    NA's:902297    1st Qu.:  0   N      : 28082  
##  Median :0                   Median :  0   S      : 22510  
##  Mean   :0                   Mean   :  1   W      : 20119  
##  3rd Qu.:0                   3rd Qu.:  0   E      : 20047  
##  Max.   :0                   Max.   :925   NE     : 14606  
##                                            (Other): 72096  
##            END_LOCATI         LENGTH           WIDTH            F         
##                 :499225   Min.   :   0.0   Min.   :   0   Min.   :0       
##  COUNTYWIDE     : 19731   1st Qu.:   0.0   1st Qu.:   0   1st Qu.:0       
##  SOUTH PORTION  :   833   Median :   0.0   Median :   0   Median :1       
##  NORTH PORTION  :   780   Mean   :   0.2   Mean   :   8   Mean   :1       
##  CENTRAL PORTION:   617   3rd Qu.:   0.0   3rd Qu.:   0   3rd Qu.:1       
##  SPRINGFIELD    :   575   Max.   :2315.0   Max.   :4400   Max.   :5       
##  (Other)        :380536                                   NA's   :843563  
##       MAG          FATALITIES     INJURIES         PROPDMG    
##  Min.   :    0   Min.   :  0   Min.   :   0.0   Min.   :   0  
##  1st Qu.:    0   1st Qu.:  0   1st Qu.:   0.0   1st Qu.:   0  
##  Median :   50   Median :  0   Median :   0.0   Median :   0  
##  Mean   :   47   Mean   :  0   Mean   :   0.2   Mean   :  12  
##  3rd Qu.:   75   3rd Qu.:  0   3rd Qu.:   0.0   3rd Qu.:   0  
##  Max.   :22000   Max.   :583   Max.   :1700.0   Max.   :5000  
##                                                               
##    PROPDMGEXP        CROPDMG        CROPDMGEXP          WFO        
##         :465934   Min.   :  0.0          :618413          :142069  
##  K      :424665   1st Qu.:  0.0   K      :281832   OUN    : 17393  
##  M      : 11330   Median :  0.0   M      :  1994   JAN    : 13889  
##  0      :   216   Mean   :  1.5   k      :    21   LWX    : 13174  
##  B      :    40   3rd Qu.:  0.0   0      :    19   PHI    : 12551  
##  5      :    28   Max.   :990.0   B      :     9   TSA    : 12483  
##  (Other):    84                   (Other):     9   (Other):690738  
##                                STATEOFFIC    
##                                     :248769  
##  TEXAS, North                       : 12193  
##  ARKANSAS, Central and North Central: 11738  
##  IOWA, Central                      : 11345  
##  KANSAS, Southwest                  : 11212  
##  GEORGIA, North and Central         : 11120  
##  (Other)                            :595920  
##                                                                                                                                                                                                     ZONENAMES     
##                                                                                                                                                                                                          :594029  
##                                                                                                                                                                                                          :205988  
##  GREATER RENO / CARSON CITY / M - GREATER RENO / CARSON CITY / M                                                                                                                                         :   639  
##  GREATER LAKE TAHOE AREA - GREATER LAKE TAHOE AREA                                                                                                                                                       :   592  
##  JEFFERSON - JEFFERSON                                                                                                                                                                                   :   303  
##  MADISON - MADISON                                                                                                                                                                                       :   302  
##  (Other)                                                                                                                                                                                                 :100444  
##     LATITUDE      LONGITUDE        LATITUDE_E     LONGITUDE_    
##  Min.   :   0   Min.   :-14451   Min.   :   0   Min.   :-14455  
##  1st Qu.:2802   1st Qu.:  7247   1st Qu.:   0   1st Qu.:     0  
##  Median :3540   Median :  8707   Median :   0   Median :     0  
##  Mean   :2875   Mean   :  6940   Mean   :1452   Mean   :  3509  
##  3rd Qu.:4019   3rd Qu.:  9605   3rd Qu.:3549   3rd Qu.:  8735  
##  Max.   :9706   Max.   : 17124   Max.   :9706   Max.   :106220  
##  NA's   :47                      NA's   :40                     
##                                            REMARKS           REFNUM      
##                                                :287433   Min.   :     1  
##                                                : 24013   1st Qu.:225575  
##  Trees down.\n                                 :  1110   Median :451149  
##  Several trees were blown down.\n              :   568   Mean   :451149  
##  Trees were downed.\n                          :   446   3rd Qu.:676723  
##  Large trees and power lines were blown down.\n:   432   Max.   :902297  
##  (Other)                                       :588295
```

```r
#types of events (as indicated in the EVTYPE variable) that are most harmful with respect to population health: fatalities, Injuries, Property damage, crop damage
#Economic damage is total of property damage and crop damage
library(plyr)
storm_data$ECODMG <- storm_data$PROPDMG +storm_data$CROPDMG
storm_data$year <- as.numeric(format(as.Date(storm_data$BGN_DATE, format = "%m/%d/%Y %H:%M:%S"), "%Y"))
#Since most of the datapoints are seen after 1990, the data is filtered for year 1990 and above.
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following objects are masked from 'package:plyr':
## 
##     arrange, count, desc, failwith, id, mutate, rename, summarise,
##     summarize
## 
## The following object is masked from 'package:stats':
## 
##     filter
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
storm_data1 <-filter(storm_data, year>1990)
#This table indicates that most data is captured from this dataset from 1990
```


```r
library(plyr)
Damage_byEvent = ddply(storm_data1,"EVTYPE" , summarize, meanFA = mean(FATALITIES), totalFA = sum(FATALITIES), meanIN = mean(INJURIES), totalIN = sum(INJURIES), meanECO = mean(ECODMG), totalECO = sum(ECODMG))
#Cleanup the event type as the data needs some regular expressions clean up
Damage_byEvent$EVTYPE <- gsub(".*HEAT","HEAT", Damage_byEvent$EVTYPE)
Damage_byEvent$EVTYPE <- gsub("HEAT WAVE","HEAT", Damage_byEvent$EVTYPE)
Damage_byEvent$EVTYPE <- gsub("FLASH FLOOD|HEAVY RAIN", "FLOOD", Damage_byEvent$EVTYPE)
Damage_byEvent$EVTYPE <- gsub("EXTREME COLD","WIND CHILL", Damage_byEvent$EVTYPE)
Damage_byEvent$EVTYPE <- gsub("BLIZZARD|HEAVY SNOW|ICE STORM","WINTER STORM", Damage_byEvent$EVTYPE)
Damage_byEvent$EVTYPE <- gsub("RIP CURRENTS|HIGH SURF","RIP CURRENT",Damage_byEvent$EVTYPE)
Damage_byEvent$EVTYPE <- gsub("WINDS","WIND",Damage_byEvent$EVTYPE)
Damage_byEvent$EVTYPE <- gsub("(.*)WIND","WIND", Damage_byEvent$EVTYPE)
Top_fatal <- Damage_byEvent[order(-Damage_byEvent$totalFA), ][1:10, ]
Top_injury <- Damage_byEvent[order(-Damage_byEvent$totalIN), ][1:10, ]
Top_Economicdamage <- Damage_byEvent[order(-Damage_byEvent$totalECO), ][1:10, ]
```
Results: 
Figure1a : List the number of events by year
Figure 1b: List teh number of events for the recent years
Figure 2a: Number of fatalaties caused by weather events
Figure 2b: Number of injuries caused by weather events
Figure 3: Number of economic damages(property and crop damages) for all weather events

```r
par(mfrow = c(1, 2), mar = c(12, 4, 3, 2), mgp = c(3, 1, 0), cex = 0.8)
hist(storm_data$year, breaks = 30, main = "Weather Events for all years",  col = "green")
hist(storm_data1$year, breaks = 30, main = "Weather Events for from 1990",  col = "green")
```

![plot of chunk unnamed-chunk-3](./peer_assessment_files/figure-html/unnamed-chunk-31.png) 

```r
par(mfrow = c(1, 2), mar = c(12, 4, 3, 2), mgp = c(3, 1, 0), cex = 0.8)
barplot(Top_fatal$totalFA, las = 3, names.arg = Top_fatal$EVTYPE, main = "Weather Events With The Top 10 Highest Fatalities", 
    ylab = "number of fatalities", col = "blue")
barplot(Top_injury$totalIN, las = 3, names.arg = Top_injury$EVTYPE, main = "Weather Events With the Top 10 Highest Injuries", 
    ylab = "number of injuries", col = "blue")
```

![plot of chunk unnamed-chunk-3](./peer_assessment_files/figure-html/unnamed-chunk-32.png) 

```r
    barplot(Top_Economicdamage$totalECO, las = 3, names.arg = Top_Economicdamage$EVTYPE, main ="Economic damage :Property damage and crop damage",ylab = "number of crop and property damages", col = "red")
```

![plot of chunk unnamed-chunk-3](./peer_assessment_files/figure-html/unnamed-chunk-33.png) 
