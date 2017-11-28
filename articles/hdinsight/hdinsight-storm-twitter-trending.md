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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="65fec-103">使用 Apache Storm on HDInsight 判斷 Twitter 的趨勢主題</span><span class="sxs-lookup"><span data-stu-id="65fec-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="65fec-104">了解如何 toouse 戟 toocreate Storm 拓樸，決定趨勢 Twitter 上的主題 （雜湊標記）。</span><span class="sxs-lookup"><span data-stu-id="65fec-104">Learn how toouse Trident toocreate a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="65fec-105">Trident 是一種高階抽象概念，可提供聯結、彙總、分組、函數和篩選等工具。</span><span class="sxs-lookup"><span data-stu-id="65fec-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="65fec-106">此外，Trident 還會新增原型，以執行可設定狀態的增量處理。</span><span class="sxs-lookup"><span data-stu-id="65fec-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="65fec-107">使用這份文件中的 hello 範例是一種戟拓撲的自訂 spout 和函式。</span><span class="sxs-lookup"><span data-stu-id="65fec-107">hello example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="65fec-108">它也用於 Trident 提供的多個內建函式。</span><span class="sxs-lookup"><span data-stu-id="65fec-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="65fec-109">需求</span><span class="sxs-lookup"><span data-stu-id="65fec-109">Requirements</span></span>

* <span data-ttu-id="65fec-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java 和 hello JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="65fec-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and hello JDK 1.8</a></span></span>

* <span data-ttu-id="65fec-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="65fec-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="65fec-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="65fec-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="65fec-113">Twitter 開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="65fec-113">A Twitter developer account</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="65fec-114">下載 hello 專案</span><span class="sxs-lookup"><span data-stu-id="65fec-114">Download hello project</span></span>

<span data-ttu-id="65fec-115">使用下列程式碼 tooclone hello 專案在本機的 hello。</span><span class="sxs-lookup"><span data-stu-id="65fec-115">Use hello following code tooclone hello project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a><span data-ttu-id="65fec-116">了解 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="65fec-116">Understanding hello topology</span></span>

<span data-ttu-id="65fec-117">hello 下列圖表顯示的資料如何流經此拓撲：</span><span class="sxs-lookup"><span data-stu-id="65fec-117">hello following diagram shows of how data flows through this topology:</span></span>

![拓撲](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="65fec-119">此圖表是 hello 拓撲的簡化的檢視。</span><span class="sxs-lookup"><span data-stu-id="65fec-119">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="65fec-120">Hello 元件的多個執行個體分散於 hello hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="65fec-120">Multiple instances of hello components are distributed across hello nodes in hello cluster.</span></span>


<span data-ttu-id="65fec-121">hello 作 hello 拓撲戟程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="65fec-121">hello Trident code that implements hello topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="65fec-122">此程式碼執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="65fec-122">This code performs hello following actions:</span></span>

1. <span data-ttu-id="65fec-123">從 hello spout 建立資料流。</span><span class="sxs-lookup"><span data-stu-id="65fec-123">Creates a stream from hello spout.</span></span> <span data-ttu-id="65fec-124">hello spout 從 Twitter 擷取推文和特定的關鍵字 （愛、 音樂以及在此範例中的咖啡） 會篩選它們。</span><span class="sxs-lookup"><span data-stu-id="65fec-124">hello spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="65fec-125">HashtagExtractor，自訂函式，是從每個推文中使用的 tooextract 雜湊標記。</span><span class="sxs-lookup"><span data-stu-id="65fec-125">HashtagExtractor, a custom function, is used tooextract hash tags from each tweet.</span></span> <span data-ttu-id="65fec-126">hello 雜湊標記是發出的 toohello 資料流。</span><span class="sxs-lookup"><span data-stu-id="65fec-126">hello hash tags are emitted toohello stream.</span></span>

3. <span data-ttu-id="65fec-127">hello 資料流是雜湊標記分組，並傳遞 tooan 彙總工具。</span><span class="sxs-lookup"><span data-stu-id="65fec-127">hello stream is grouped by hash tag, and passed tooan aggregator.</span></span> <span data-ttu-id="65fec-128">此彙總工具會建立每個主題標籤出現次數的計數。</span><span class="sxs-lookup"><span data-stu-id="65fec-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="65fec-129">計數資料會保存在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="65fec-129">This data is persisted in memory.</span></span> <span data-ttu-id="65fec-130">最後，新的資料流，就會發出包含 hello 雜湊標記和 hello 計數。</span><span class="sxs-lookup"><span data-stu-id="65fec-130">Finally, a new stream is emitted that contains hello hash tag and hello count.</span></span>

4. <span data-ttu-id="65fec-131">hello **FirstN**組件是套用的 tooreturn 只 hello 前 10 個值，根據 hello 計數欄位。</span><span class="sxs-lookup"><span data-stu-id="65fec-131">hello **FirstN** assembly is applied tooreturn only hello top 10 values, based on hello count field.</span></span>

> [!NOTE]
> <span data-ttu-id="65fec-132">如需使用戟的詳細資訊，請參閱 hello[戟 API 概觀](http://storm.apache.org/releases/current/Trident-API-Overview.html)文件。</span><span class="sxs-lookup"><span data-stu-id="65fec-132">For more information on working with Trident, see hello [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="hello-spout"></a><span data-ttu-id="65fec-133">hello spout</span><span class="sxs-lookup"><span data-stu-id="65fec-133">hello spout</span></span>

<span data-ttu-id="65fec-134">hello spout **TwitterSpout**，會使用[Twitter4j](http://twitter4j.org/en/)從 Twitter tooretrieve 推文。</span><span class="sxs-lookup"><span data-stu-id="65fec-134">hello spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets from Twitter.</span></span> <span data-ttu-id="65fec-135">建立篩選器的 hello 文字__喜愛__，**音樂**，和**咖啡**。</span><span class="sxs-lookup"><span data-stu-id="65fec-135">A filter is created for hello words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="65fec-136">內送推文 （狀態） 符合 hello 篩選條件會儲存在連結的封鎖佇列中。</span><span class="sxs-lookup"><span data-stu-id="65fec-136">Incoming tweets (status) that match hello filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="65fec-137">最後，項目關閉 hello 佇列提取，且發出 toohello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="65fec-137">Finally, items are pulled off hello queue and emitted toohello topology.</span></span>

### <a name="hello-hashtagextractor"></a><span data-ttu-id="65fec-138">hello HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="65fec-138">hello HashtagExtractor</span></span>

<span data-ttu-id="65fec-139">tooextract 雜湊標記， [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--)是使用的 tooretrieve hello 推文中所包含的所有雜湊標記。</span><span class="sxs-lookup"><span data-stu-id="65fec-139">tooextract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used tooretrieve all hash tags that are contained in hello tweet.</span></span> <span data-ttu-id="65fec-140">這些就發出的 toohello 資料流。</span><span class="sxs-lookup"><span data-stu-id="65fec-140">These are then emitted toohello stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="65fec-141">設定 Twitter</span><span class="sxs-lookup"><span data-stu-id="65fec-141">Configure Twitter</span></span>

<span data-ttu-id="65fec-142">使用下列步驟 tooregister 新 Twitter 應用程式的 hello，並從 Twitter 取得 hello 消費者和存取權杖所需的資訊 tooread:</span><span class="sxs-lookup"><span data-stu-id="65fec-142">Use hello following steps tooregister a new Twitter application and obtain hello consumer and access token information needed tooread from Twitter:</span></span>

1. <span data-ttu-id="65fec-143">跳過[Twitter 應用程式](https://apps.twitter.com)按一下 hello**建立新的應用程式** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65fec-143">Go too[Twitter Apps](https://apps.twitter.com) and click hello **Create new app** button.</span></span> <span data-ttu-id="65fec-144">當填滿 hello 表單中，將保留在 hello**回呼 URL**欄位空白。</span><span class="sxs-lookup"><span data-stu-id="65fec-144">When filling in hello form, leave hello **Callback URL** field empty.</span></span>

2. <span data-ttu-id="65fec-145">建立 hello 應用程式時，按一下 hello**機碼和存取權杖** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="65fec-145">When hello app is created, click hello **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="65fec-146">複製 hello**取用者索引鍵**和**取用者秘密**資訊。</span><span class="sxs-lookup"><span data-stu-id="65fec-146">Copy hello **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="65fec-147">在 hello hello 頁面底部，選取**建立我的存取權杖**有沒有 token。</span><span class="sxs-lookup"><span data-stu-id="65fec-147">At hello bottom of hello page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="65fec-148">Hello 語彙基元時已建立、 複製 hello**存取權杖**和**存取語彙基元秘**資訊。</span><span class="sxs-lookup"><span data-stu-id="65fec-148">When hello tokens have been created, copy hello **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="65fec-149">在 hello **TwitterSpoutTopology**專案您先前複製，請開啟 hello **resources/twitter4j.properties**檔案，在 hello 先前步驟中，新增您所蒐集的 hello 資訊並儲存 hello 檔案.</span><span class="sxs-lookup"><span data-stu-id="65fec-149">In hello **TwitterSpoutTopology** project you previously cloned, open hello **resources/twitter4j.properties** file, add hello information you gathered in hello previous steps, and then save hello file.</span></span>

## <a name="build-hello-topology"></a><span data-ttu-id="65fec-150">建置 hello 拓撲</span><span class="sxs-lookup"><span data-stu-id="65fec-150">Build hello topology</span></span>

<span data-ttu-id="65fec-151">使用下列程式碼 toobuild hello 專案 hello:</span><span class="sxs-lookup"><span data-stu-id="65fec-151">Use hello following code toobuild hello project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a><span data-ttu-id="65fec-152">測試 hello 拓撲</span><span class="sxs-lookup"><span data-stu-id="65fec-152">Test hello topology</span></span>

<span data-ttu-id="65fec-153">使用下列命令 tootest hello 拓撲在本機的 hello:</span><span class="sxs-lookup"><span data-stu-id="65fec-153">Use hello following command tootest hello topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="65fec-154">Hello 拓撲啟動之後，您應該會看到偵錯資訊包含 hello 雜湊標記，並將計算發出的 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="65fec-154">After hello topology starts, you should see debug information that contains hello hash tags and counts emitted by hello topology.</span></span> <span data-ttu-id="65fec-155">hello 輸出應該看起來類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="65fec-155">hello output should appear similar toohello following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="65fec-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65fec-156">Next steps</span></span>

<span data-ttu-id="65fec-157">既然您已經測試過本機 hello 拓樸，探索如何 toodeploy hello 拓樸：[部署和管理 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="65fec-157">Now that you have tested hello topology locally, discover how toodeploy hello topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="65fec-158">您也可能會想要遵循 Storm 主題 hello:</span><span class="sxs-lookup"><span data-stu-id="65fec-158">You may also be interested in hello following Storm topics:</span></span>

* [<span data-ttu-id="65fec-159">使用 Maven 開發 Storm on HDInsight 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="65fec-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="65fec-160">使用 Visual Studio 開發 Storm on HDInsight 的 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="65fec-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="65fec-161">如需 HDinsight 的 Storm 範例：</span><span class="sxs-lookup"><span data-stu-id="65fec-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="65fec-162">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="65fec-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

