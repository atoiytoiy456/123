---
title: "Facebook粉絲團分析（分析專頁：蔡英文）"
output: github_document
---

分析蔡英文粉絲團貼文，資料分析區間為2016/01/01至2016/04/11

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

##讀取蔡英文粉絲團資料
```{r cars}
if (!require('Rfacebook')){
    install.packages("Rfacebook")
    library(Rfacebook)
}

token<-'CAACEdEose0cBAA2FECXxSHFxJxGTHQ9z20wEqQGFd5iW20X2dzrJXeZAaZBZBAlBcZAceKZBZAuNSn0lVaHpdreicNqz4rGA9c3c5V733ZASvsLMiMvGtd2ZCrUjlZAl5ZCZBa9fuHZCPNiZBttHJVGDWFHahZA60ZAi7ZBs3lr8ysEuD8igLd94tF8MdCpaT85vCtHPw8pV8HXZAUJ6nbbHAusJWLU2RiIOLfrhCMGcZD'
totalPage<-NULL
lastDate<-Sys.Date()
DateVectorStr<-as.character(seq(as.Date("2016-01-01"),lastDate,by="5 days"))
for(i in 1:(length(DateVectorStr)-1)){
    tempPage<-getPage("tsaiingwen", token,
                      since = DateVectorStr[i],until = DateVectorStr[i+1])
    totalPage<-rbind(totalPage,tempPage)
}
nrow(totalPage)
```
2016/01/01 至 2016/04/11，蔡英文粉絲團一共有 212 篇文章



## 每日發文數分析
分析蔡英文粉絲團每天的發文數
```{r cars}
totalPage$datetime <- as.POSIXct(totalPage$created_time, 
                                 format = "%Y-%m-%dT%H:%M:%S+0000", 
                                 tz = "GMT") 
totalPage$dateTPE <- format(totalPage$datetime, "%Y-%m-%d", 
                            tz = "Asia/Taipei") 
totalPage$weekdays <-weekdays(as.Date(totalPage$dateTPE))
PostCount<-aggregate(id~dateTPE,totalPage,length)
library(knitr)
kable(head(PostCount[order(PostCount$id,decreasing = T),]))
```
2016-01-15(禮拜五)的發文數最多

第一篇為"民進黨可以克服種種困難再起，我跟大家也可以一起克服挑戰"
第二篇為"也許你因為很忙，所以不常回家，也不常想念家鄉。但是"
第三篇為"【活動實況直播訊息】 「點亮台灣每一里」車掃來到最後"
第四篇為"「點亮台灣每一里」車隊掃街，我們用六天的時間，從南到"
第五篇為"【活動實況直播訊息】「迎向勝利<U+30FB>點亮台灣」選"
第六篇為"終於，我們一起走到這裡了。 剛剛，我們在板橋，也就是"
第七篇為"終於，我們一起走到這裡了。 剛剛，我們在板橋，也就是"

2016-01-11、2016-01-14居次

1/11有:

"第三天的全國大掃街，今天從嘉義出發。這裡是農業大縣，"
"每一次聽到吳念真導演的配音，總覺得是我聽過最真誠、感"
"在這樣的冷天裡，雲林和嘉義飄著細細的雨，但看見鄉親們"
"原地踏步不是安定，改革才能帶來安定。 國民黨最近又在"
"原地踏步不是安定，改革才能帶來安定。 國民黨最近又在"
"<U+30FB>「英派革新<U+30FB>台灣好政」http://goo"

1/14有:

"改變台灣，一定要成功！高雄是民主的基地，也是台灣改變"
"「有一蕾花 恬恬開在我介屋下 髻鬃圓圓介遮 遮風抵雨我介"
"民進黨推出的不分區立委，不怕被比較，只怕不比較！從食品"
"終於，我們一起走到了這裡。 四年前的今天，我們坦然面對2"
"這隻苗栗鄉親送我的手指，我一路都帶著它，因為，它是"
"四年前的失敗，沒有讓這個黨倒下去。我們在民主選舉中失"
"1/15(五)「迎向未來<U+30FB>點亮台灣造勢晚會」選前之"


## 每日Likes數分析
分析蔡英文粉絲團每日的點讚數並統計
```{r cars}
LikesCount<-aggregate(likes_count~datetime,totalPage,mean)
library(knitr)
kable(head(LikesCount[order(LikesCount$likes_count,decreasing = T),]))
```
根據資料指出，2016-01-16的"N/A"點讚數最多

其次為2016-01-16的"N/A"
第三為2016-01-16的"中華民國，出發！"
第四為2016-01-16的"謝謝各位國內外的媒體記者朋友，感謝大家的耐心等候。"
第五為2016-01-17的"各位現場的朋友，各位電視機前面的好朋友，網路上收看直"
第六為2016-03-29的"小燈泡 阿姨不會讓你白白犧牲。這個社會破了很多洞，我"




## 每日Comments數分析
分析朱立倫粉絲團每日的討論數並統計
```{r cars}
CommentsCount<-aggregate(comments_count~datetime,totalPage,mean)
library(knitr)
kable(head(CommentsCount[order(CommentsCount$comments_count,decreasing = T),]))
```

第一多為2016-01-20的"選後第一次民進黨中常會，我謝謝大家在選舉中的幫忙，大"
第二多為2016-01-21的"在故鄉屏東感謝大家，有鄉親們的相挺，心中覺得特別溫暖。"
第三多為2016-01-21的"N/A"
第四多為2016-01-15的"【活動實況直播訊息】 「點亮台灣每一里」車掃來到最後"
第五多為2016-01-20的"選舉結束，還沒有開始謝票行程，現在最快樂的，就是終於"
第六多為2016-01-16的"N/A"



## 每日Shares數分析
分析朱立倫粉絲團每日的分享數並做統計
```{r cars}
ShareCount<-aggregate(shares_count~datetime,totalPage,mean)
library(knitr)
kable(head(ShareCount[order(ShareCount$shares_count,decreasing = T),]))
```
第一多為2016-01-16的"各位現場的朋友，各位電視機前面的好朋友，網路上收看直"
第二多為2016-03-29的"給王女士的一封信：敬愛的王女士，昨晚，在電視機前，看見您"
第三多為2016-01-16的"謝謝各位國內外的媒體記者朋友，感謝大家的耐心等候。"
第四多為2016-01-14的"終於，我們一起走到了這裡。 四年前的今天，我們坦然面對"
第五多為2016-01-15的"終於，我們一起走到這裡了。 剛剛，我們在板橋，也就是"
第六多為2016-01-10的"你曾經離開故鄉 故鄉 沒有說話 故鄉 永遠是安靜的 故鄉"



