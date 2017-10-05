---
title: "Twitter 的趨勢主題與 Apache Storm on HDInsight | Microsoft Docs"
description: "了解如何使用 Trident 建立 Apache Storm 拓撲，藉此根據主題標籤判斷 Twitter 上的趨勢主題。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: d588221586f151319436525c5098b0bb2694e5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>使用 Apache Storm on HDInsight 判斷 Twitter 的趨勢主題

了解如何使用 Trident 建立 Storm 拓撲，藉此判斷 Twitter 上的趨勢主題 (主題標籤)。

Trident 是一種高階抽象概念，可提供聯結、彙總、分組、函數和篩選等工具。 此外，Trident 還會新增原型，以執行可設定狀態的增量處理。 這份文件中使用的範例是使用自訂 Spout 和函式的 Trident 拓撲。 它也用於 Trident 提供的多個內建函式。

## <a name="requirements"></a>需求

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java 和 JDK 1.8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Twitter 開發人員帳戶

## <a name="download-the-project"></a>下載專案

使用以下程式碼在本機上複製專案。

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a>了解拓撲

下圖顯示透過此拓撲的資料流︰

![拓撲](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> 此圖以簡化的方式呈現拓撲。 元件的多個執行個體會分散到叢集中的節點。


實作拓撲的 Trident 程式碼如下：

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

此程式碼會執行下列動作：

1. 從 Spout 建立資料流。 Spout 會擷取 Twitter 中的推文，然後篩選特定關鍵字 (在此範例中，為 love、music 和 coffee)。

2. 會使用自訂函數 HashtagExtractor 擷取每則推文中的主題標籤。 主題標籤會發出至資料流。

3. 資料流接著會依主題標籤進行分組，然後傳遞給彙總工具。 此彙總工具會建立每個主題標籤出現次數的計數。 計數資料會保存在記憶體中。 最後，會發出含有主題標籤和計數的新資料流。

4. **FirstN** 組件會被套用來根據計數欄位僅傳回前 10 個值。

> [!NOTE]
> 如需使用 Trident 的詳細資訊，請參閱 [Trident API 概觀](http://storm.apache.org/releases/current/Trident-API-Overview.html) 文件。

### <a name="the-spout"></a>Spout

Spout **TwitterSpout** 會使用 [Twitter4j](http://twitter4j.org/en/) 從 Twitter 擷取推文。 接著會對於 __love__、**music** 和 **coffee** 這些字建立篩選條件。 符合篩選條件的傳入推文 (status) 將儲存在連結的封鎖佇列中。 最後，會將項目拉出佇列，然後發出至拓撲。

### <a name="the-hashtagextractor"></a>HashtagExtractor

若要擷取主題標籤，可以使用 [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) 來擷取推文中包含的所有主題標籤。 之後，會將這些發出至資料流。

## <a name="configure-twitter"></a>設定 Twitter

使用以下步驟註冊新的 Twitter 應用程式，然後取得讀取 Twitter 內容所需的取用者和存取權杖資訊。

1. 前往 [Twitter 應用程式](https://apps.twitter.com)，然後按一下 [建立新應用程式] 按鈕。 填寫表單時，請將 [回呼 URL]  欄位保留空白。

2. 建立應用程式後，按一下 [金鑰和存取權杖]  索引標籤。

3. 複製 [取用者金鑰] 和 [取用者密碼] 的資訊。

4. 如果沒有權杖，請在頁面底部選取 [建立我的存取權杖]  。 建立權杖後，複製 [存取權杖] 和 [存取權杖密碼] 的資訊。

5. 在先前複製的 **TwitterSpoutTopology** 專案中，開啟 **resources/twitter4j.properties** 檔案，並新增先前步驟中所收集的資訊，然後儲存檔案。

## <a name="build-the-topology"></a>建置拓撲

請使用以下程式碼建置專案：

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a>測試拓撲

請使用以下命令在本機上測試拓撲：

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

拓撲啟動後，您應該會看到含有拓撲所發出之主題標籤和計數的偵錯資訊。 輸出應該如下列文字所示：

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a>後續步驟

現在，您已經在本機上測試拓撲，接著請探索如何部署拓撲： [部署和管理 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology.md)。

您也可能會對下列 Storm 主題感興趣：

* [使用 Maven 開發 Storm on HDInsight 的 Java 拓撲](hdinsight-storm-develop-java-topology.md)
* [使用 Visual Studio 開發 Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)

如需 HDinsight 的 Storm 範例：

* [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)

