長庚大學 大數據分析方法 作業三
================

網站資料爬取
------------

``` r
#這是R Code Chunk
##第一次使用要先安裝 install.packages("rvest")

#install.packages("rvest")
library(rvest)
```

    ## Warning: package 'rvest' was built under R version 3.3.3

    ## Loading required package: xml2

    ## Warning: package 'xml2' was built under R version 3.3.3

``` r
for(i in 1:5){
  PttUrl <- paste0("https://www.ptt.cc/bbs/Tech_Job/index",i,".html")
  PttTechJob <- PttUrl

  PttContent <- read_html(PttTechJob)
  post_title <- PttContent %>% html_nodes(".title") %>% html_text()
  post_pushnum <- PttContent %>% html_nodes(".nrec") %>% html_text()
  post_author <- PttContent %>% html_nodes(".author") %>% html_text()
  
  assign(paste0("PttPosts",i), data.frame(Title = post_title, PushNum = post_pushnum, Author = post_author))
}

  PttPostsAll<-rbind(PttPosts1,PttPosts2,PttPosts3,PttPosts4,PttPosts5)
  tail(PttPostsAll)
```

    ##                                                                                     Title
    ## 95        \n\t\t\t\n\t\t\t\t[面試] 面試後主動與主管會HR連絡會加深印象嗎??\n\t\t\t\n\t\t\t
    ## 96  \n\t\t\t\n\t\t\t\t[公告]邀請ShortestPath就任精華文章面試區及<U+A420>…\n\t\t\t\n\t\t\t
    ## 97                      \n\t\t\t\n\t\t\t\tRe: Re:工作心得分享(協調會結果)\n\t\t\t\n\t\t\t
    ## 98              \n\t\t\t\n\t\t\t\t[轉錄證明][申請] Tech_Job板申請新增板主\n\t\t\t\n\t\t\t
    ## 99                               \n\t\t\t\n\t\t\t\t[公告] pangyu 警告一次\n\t\t\t\n\t\t\t
    ## 100                        \n\t\t\t\n\t\t\t\t[公告] wonderfulkid 警告一次\n\t\t\t\n\t\t\t
    ##     PushNum       Author
    ## 95        9 freedom70516
    ## 96        6      harrygp
    ## 97       10  paleshelter
    ## 98               harrygp
    ## 99               shaffer
    ## 100              shaffer

``` r
##read_html
##html_nodes
##html_text
```

爬蟲結果呈現
------------

``` r
#這是R Code Chunk
knitr::kable(PttPostsAll[1:100,c("Title","PushNum","Author")])
```

| Title                                                 | PushNum | Author       |
|:------------------------------------------------------|:--------|:-------------|
| \[公告\]有關本板                                      | 1       | Rooney       |
| \[轉錄\]職位中英文                                    | 5       | Rooney       |
| Re: \[轉錄\]\[就可\] 嫁給工程師的好處多?! ^\_^        | 69      | azer         |
| \[公告\] 發文類別新增　\[國防\] 選項                  | 2       | Rooney       |
| \[Tech\_Job\] 看板 選情報導                           | 2       | \[馬路探子\] |
| \[公告\] 投票結果與新板主志工報名                     |         | Rooney       |
| Re: \[公告\] 投票結果與新板主志工報名                 | 3       | Rooney       |
| Re: \[問題\] 科技人的另一半                           | 爆      | Irisyeh      |
| \[心得\] 請大家注意身體健康噢!                        | 28      | chienyu211   |
| \[公告\] 板規修改                                     | 6       | Rooney       |
| Re: \[心得\] 竹朝科技---一個讓我失望+後悔的公司       | XX      | bear3        |
| Re: \[無關\]boylover兄臺                              | 4       | Rooney       |
| \[公告\] 發文限制問題                                 | 5       | Rooney       |
| Re: \[問題\] 為什麼分紅費用化對員工不好呢?            | 80      | LKO          |
| \[公告\] 食衣住行與內幕文問題                         | 5       | Rooney       |
| \[公告\] 常見問題整理                                 | 2       | Rooney       |
| \[閒聊\] 被資遣注意事項!!!                            | 20      | oca          |
| Re: \[問題\] 上夜班如何調整作息?                      | 5       | tatibana31   |
| \[公告\] Tech\_Job板規                                | 4       | DEERETTE     |
| \[公告\] 新的標題分類                                 | 1       | layachang    |
| Re: \[新聞\] 我專利申請量 全球排名第七                | 6       | yaudeh       |
| Re: \[問題\] SSD出來以後,以後主機板會不會內建硬碟     | 10      | shter        |
| Re: \[討論\] 工程師們大多怎麼規劃人生呢               | 22      | deadly       |
| Re: \[新聞\] 索愛慘賠 本土代工廠很剉                  | 40      | shter        |
| \[分享\] 「求去者」所為何事？                         | 3       | VarX         |
| Re: \[問題\] 公司要求加班                             |         | spritecat    |
| Re: \[問題\] 關於研發替代役 錄取的關鍵是?!            | 4       | AixStyle     |
| \[心情\]大家加油不要灰心                              | 24      | mazerlin     |
| Re: \[面試\] 最近面試常被這個問題打敗...              | 2       | smalloc      |
| Re: 忽然覺得 讀書跟賺錢不怎麼成正比                   | 15      | g8330330     |
| Re: 忽然覺得 讀書跟賺錢不怎麼成正比                   | 16      | fbgae        |
| Re: 忽然覺得 讀書跟賺錢不怎麼成正比                   | 44      | hamk5202     |
| Re: \[心得\] offer被取消 沒想到我們也被耍了           | 5       | yuujang      |
| \[面試\] 心得分享                                     | 5       | tojump       |
| \[心得\] 硬體類研發替代役面試心得                     | 3       | blueangel629 |
| \[問題\] 面試自我介紹該講些什麼                       | 7       | ALiGoo       |
| 失業給付的申請 11                                     |         | WRITERT1NA   |
| \[公告\] 感謝sevencolor                               | 11      | layachang    |
| \[心得\] 如何寫份好履歷？從主管的角度看起！           | 8       | autumnbreeze |
| Re: \[問題\] 當找不到工作時，會不會有一種想輕生的 …   | 爆      | Jongny       |
| \[情報\] 台積電受害員工自救會                         |         | layachang    |
| \[公告\] 問卷規範                                     |         | layachang    |
| \[小小分享\] 面試中曾經被問過的問題～                 | 30      | winnie02022  |
| \[公告\] Tech\_Job版版規 0904                         |         | layachang    |
| Re: \[問題\] 請問讀交大電子博班畢業會不會加分呀?      | 5       | whni         |
| 職場求生術與政治學                                    | 23      | karlhsu      |
| \[公告\] 暫停回文                                     |         | layachang    |
| \[公告\] 討論串"台清交博士畢選六萬的工研院還<U+AC20>… | 5       | layachang    |
| \[公告\] 討論串"學歷重要嗎"                           | 3       | layachang    |
| Re: 進入哪家公司 才能夠擁有美好的人生?                | 7       | tyu26        |
| \[公告\] 暫停回覆                                     |         | layachang    |
| \[公告\] 討論串"\[長恨\] 無奈呀 職場如戰場 人生 …     |         | layachang    |
| \[公告\] 請暫停回覆討論串                             | 6       | layachang    |
| \[公告\] 討論串"\[閒聊\] 唸了這麼多書要做什麼??"      | 8       | layachang    |
| \[公告\] 討論串"\[問題\] 有人請教我如何進mtk?"        | 7       | layachang    |
| \[公告\] 誠徵副版主                                   |         | layachang    |
| \[公告\] 懇請熟識板主的板友代為通知                   | 6       | longbow2     |
| \[公告\] 本板暫由小組長接管，徵求新任板主             | 5       | longbow2     |
| \[公告\] 板主選舉投票開始                             | 1       | longbow2     |
| \[公告\] 板主票選提早開票                             |         | longbow2     |
| \[公告\] 解除 fdj 板主職位                            | 2       | longbow2     |
| \[公告\] 徵選本板板主一名                             | 3       | longbow2     |
| Re: \[政見\] illywu(ilsobeit) 競選 Tech\_Job 新版主   | 5       | longbow2     |
| \[公告\] 2009驚夏第一彈 討論串                        | 5       | longbow2     |
| \[政見\] 幫忙一下 若是有機會替大家服務                | 19      | harrygp      |
| \[公告\] achii 警告一次 及板主選舉事項                | 10      | longbow2     |
| Re: \[檢舉\] 鬧板                                     | 9       | longbow2     |
| \[公告\] 物價與薪資 文刪文， SmallJohn 警告一次       | 6       | longbow2     |
| \[公告\] 板主選舉開始                                 | 2       | longbow2     |
| \[公告\] 刪文及水桶（achii）                          | 18      | longbow2     |
| Re: \[討論\] 問一個問題 版主真抱歉                    |         | longbow2     |
| \[公告\] 刪文、水桶、劣退（goosey、dkenvy）           | 4       | longbow2     |
| \[公告\] 投票即將截止，請板友踴躍投票                 | 2       | longbow2     |
| \[公告\] harrygp 就任本板板主                         | 6       | longbow2     |
| \[面試\] 友達光電面試心得                             | 9       | Sunghui      |
| \[討論\] 威盛在臺灣那邊的工資開到多少                 | 7       | qiantangchao |
| Re: \[討論\] 威盛在臺灣那邊的工資開到多少             | 3       | twwo         |
| Re: \[討論\] 威盛在臺灣那邊的工資開到多少             |         | qiantangchao |
| Re: 台積12廠奈米技術整合工程師                        | 49      | powerme      |
| \[面試\] 面試分享                                     | 9       | mythlove     |
| Re: \[討論\] 請教harrygp板主 這樣該給桶嗎?            | 16      | harrygp      |
| Re: \[公告\]徵求另外一位板主共同管理                  | 17      | cloud7515    |
| \[政見\] shaffer 應徵版主                             | 4       | shaffer      |
| Re: \[公告\]徵求另外一位板主共同管理                  | 8       | ShortestPath |
| Re: \[公告\]徵求另外一位板主共同管理                  | 3       | glo6e        |
| \[面試\] 面試心得 凌陽多 宇潤數位 台積 晨星 智源      | 7       | ross999      |
| Re: \[公告\]徵求另外一位板主共同管理                  | 1       | glo6e        |
| \[面試\] 面試心得分享: Google                         | 21      | waitrop      |
| \[公告\]本版有設定發文與推文限制                      | 1       | harrygp      |
| 我天天上班都在玩RPG                                   | 43      | stpippen     |
| \[面試\] Garmin顯示技術面試分享                       | 7       | pinch        |
| \[面試\] 艾克爾面試心得                               | 5       | teanchun     |
| Re: \[討論\] 待業的日子怎麼過                         | 28      | shaffer      |
| \[討論\] 最近來interview的條件都很棒                  | X4      | freeread     |
| \[面試\] 面試後主動與主管會HR連絡會加深印象嗎??       | 9       | freedom70516 |
| \[公告\]邀請ShortestPath就任精華文章面試區及<U+A420>… | 6       | harrygp      |
| Re: Re:工作心得分享(協調會結果)                       | 10      | paleshelter  |
| \[轉錄證明\]\[申請\] Tech\_Job板申請新增板主          |         | harrygp      |
| \[公告\] pangyu 警告一次                              |         | shaffer      |
| \[公告\] wonderfulkid 警告一次                        |         | shaffer      |

``` r
##請將iris取代為上個步驟中產生的爬蟲資料資料框
```

解釋爬蟲結果
------------

``` r
#這是R Code Chunk
str(PttPostsAll)
```

    ## 'data.frame':    100 obs. of  3 variables:
    ##  $ Title  : Factor w/ 94 levels "\n\t\t\t\n\t\t\t\t[Tech_Job] 看板 選情報導\n\t\t\t\n\t\t\t",..: 10 13 20 8 1 3 14 18 11 4 ...
    ##  $ PushNum: Factor w/ 33 levels "","1","2","20",..: 2 8 10 3 3 1 6 13 5 9 ...
    ##  $ Author : Factor w/ 52 levels "[馬路探子]","azer",..: 10 10 2 10 1 10 10 6 4 10 ...

100 obs.代表有100列，也就是有100篇文章標題。

``` r
#這是R Code Chunk
table(PttPostsAll$Author)
```

    ## 
    ##   [馬路探子]         azer        bear3   chienyu211     DEERETTE 
    ##            1            1            1            1            1 
    ##      Irisyeh    layachang          LKO          oca       Rooney 
    ##            1           14            1            1           10 
    ##   tatibana31     AixStyle       ALiGoo autumnbreeze blueangel629 
    ##            1            1            1            1            1 
    ##       deadly        fbgae     g8330330     hamk5202       Jongny 
    ##            1            1            1            1            1 
    ##     mazerlin        shter      smalloc    spritecat       tojump 
    ##            1            2            1            1            1 
    ##         VarX   WRITERT1NA       yaudeh      yuujang      karlhsu 
    ##            1            1            1            1            1 
    ##     longbow2        tyu26         whni  winnie02022      harrygp 
    ##           17            1            1            1            5 
    ##     mythlove      powerme qiantangchao      Sunghui         twwo 
    ##            1            1            2            1            1 
    ##    cloud7515 freedom70516     freeread        glo6e  paleshelter 
    ##            1            1            1            2            1 
    ##        pinch      ross999      shaffer ShortestPath     stpippen 
    ##            1            1            4            1            1 
    ##     teanchun      waitrop 
    ##            1            1

作者longbow2的文章數最多，100篇裡他發了17個文章。

我發現的有趣現象是，裡面有非常多的人詢問和分享面試的心得，但通常這種文章的推文數都很低，反而是一些危言聳聽的標題，例如：\[問題\] 當找不到工作時，會不會有一種想輕生的 …，或是，Re: \[轉錄\]\[就可\] 嫁給工程師的好處多?! ^\_^，之類的標題就會有很多推文，甚至有「爆」的推文數。 然後發現上面說的longbow2的文章標題都會有個\[公告\]，原來他是小組長，他正在舉行版主的投票，所以他的文章數特別多。
