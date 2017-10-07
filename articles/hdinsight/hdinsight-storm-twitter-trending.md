---
title: "HDInsight 上的 Apache Storm 的 aaaTwitter 趨勢主題 |Microsoft 文件"
description: "了解如何 toouse 戟 toocreate Apache Storm 拓撲會決定在 Twitter 上的趨勢主題根據雜湊標記。"
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
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>使用 Apache Storm on HDInsight 判斷 Twitter 的趨勢主題

了解如何 toouse 戟 toocreate Storm 拓樸，決定趨勢 Twitter 上的主題 （雜湊標記）。

Trident 是一種高階抽象概念，可提供聯結、彙總、分組、函數和篩選等工具。 此外，Trident 還會新增原型，以執行可設定狀態的增量處理。 使用這份文件中的 hello 範例是一種戟拓撲的自訂 spout 和函式。 它也用於 Trident 提供的多個內建函式。

## <a name="requirements"></a>需求

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java 和 hello JDK 1.8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Twitter 開發人員帳戶

## <a name="download-hello-project"></a>下載 hello 專案

使用下列程式碼 tooclone hello 專案在本機的 hello。

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a>了解 hello 拓樸

hello 下列圖表顯示的資料如何流經此拓撲：

![拓撲](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> 此圖表是 hello 拓撲的簡化的檢視。 Hello 元件的多個執行個體分散於 hello hello 叢集中的節點。


hello 作 hello 拓撲戟程式碼如下所示：

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

此程式碼執行下列動作的 hello:

1. 從 hello spout 建立資料流。 hello spout 從 Twitter 擷取推文和特定的關鍵字 （愛、 音樂以及在此範例中的咖啡） 會篩選它們。

2. HashtagExtractor，自訂函式，是從每個推文中使用的 tooextract 雜湊標記。 hello 雜湊標記是發出的 toohello 資料流。

3. hello 資料流是雜湊標記分組，並傳遞 tooan 彙總工具。 此彙總工具會建立每個主題標籤出現次數的計數。 計數資料會保存在記憶體中。 最後，新的資料流，就會發出包含 hello 雜湊標記和 hello 計數。

4. hello **FirstN**組件是套用的 tooreturn 只 hello 前 10 個值，根據 hello 計數欄位。

> [!NOTE]
> 如需使用戟的詳細資訊，請參閱 hello[戟 API 概觀](http://storm.apache.org/releases/current/Trident-API-Overview.html)文件。

### <a name="hello-spout"></a>hello spout

hello spout **TwitterSpout**，會使用[Twitter4j](http://twitter4j.org/en/)從 Twitter tooretrieve 推文。 建立篩選器的 hello 文字__喜愛__，**音樂**，和**咖啡**。 內送推文 （狀態） 符合 hello 篩選條件會儲存在連結的封鎖佇列中。 最後，項目關閉 hello 佇列提取，且發出 toohello 拓撲。

### <a name="hello-hashtagextractor"></a>hello HashtagExtractor

tooextract 雜湊標記， [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--)是使用的 tooretrieve hello 推文中所包含的所有雜湊標記。 這些就發出的 toohello 資料流。

## <a name="configure-twitter"></a>設定 Twitter

使用下列步驟 tooregister 新 Twitter 應用程式的 hello，並從 Twitter 取得 hello 消費者和存取權杖所需的資訊 tooread:

1. 跳過[Twitter 應用程式](https://apps.twitter.com)按一下 hello**建立新的應用程式** 按鈕。 當填滿 hello 表單中，將保留在 hello**回呼 URL**欄位空白。

2. 建立 hello 應用程式時，按一下 hello**機碼和存取權杖** 索引標籤。

3. 複製 hello**取用者索引鍵**和**取用者秘密**資訊。

4. 在 hello hello 頁面底部，選取**建立我的存取權杖**有沒有 token。 Hello 語彙基元時已建立、 複製 hello**存取權杖**和**存取語彙基元秘**資訊。

5. 在 hello **TwitterSpoutTopology**專案您先前複製，請開啟 hello **resources/twitter4j.properties**檔案，在 hello 先前步驟中，新增您所蒐集的 hello 資訊並儲存 hello 檔案.

## <a name="build-hello-topology"></a>建置 hello 拓撲

使用下列程式碼 toobuild hello 專案 hello:

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a>測試 hello 拓撲

使用下列命令 tootest hello 拓撲在本機的 hello:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Hello 拓撲啟動之後，您應該會看到偵錯資訊包含 hello 雜湊標記，並將計算發出的 hello 拓撲。 hello 輸出應該看起來類似 toohello 下列文字：

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

既然您已經測試過本機 hello 拓樸，探索如何 toodeploy hello 拓樸：[部署和管理 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology.md)。

您也可能會想要遵循 Storm 主題 hello:

* [使用 Maven 開發 Storm on HDInsight 的 Java 拓撲](hdinsight-storm-develop-java-topology.md)
* [使用 Visual Studio 開發 Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)

如需 HDinsight 的 Storm 範例：

* [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)

