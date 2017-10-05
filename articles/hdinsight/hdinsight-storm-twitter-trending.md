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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="c3477-103">使用 Apache Storm on HDInsight 判斷 Twitter 的趨勢主題</span><span class="sxs-lookup"><span data-stu-id="c3477-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="c3477-104">了解如何使用 Trident 建立 Storm 拓撲，藉此判斷 Twitter 上的趨勢主題 (主題標籤)。</span><span class="sxs-lookup"><span data-stu-id="c3477-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="c3477-105">Trident 是一種高階抽象概念，可提供聯結、彙總、分組、函數和篩選等工具。</span><span class="sxs-lookup"><span data-stu-id="c3477-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="c3477-106">此外，Trident 還會新增原型，以執行可設定狀態的增量處理。</span><span class="sxs-lookup"><span data-stu-id="c3477-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="c3477-107">這份文件中使用的範例是使用自訂 Spout 和函式的 Trident 拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3477-107">The example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="c3477-108">它也用於 Trident 提供的多個內建函式。</span><span class="sxs-lookup"><span data-stu-id="c3477-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="c3477-109">需求</span><span class="sxs-lookup"><span data-stu-id="c3477-109">Requirements</span></span>

* <span data-ttu-id="c3477-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java 和 JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="c3477-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span></span>

* <span data-ttu-id="c3477-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="c3477-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="c3477-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="c3477-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="c3477-113">Twitter 開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="c3477-113">A Twitter developer account</span></span>

## <a name="download-the-project"></a><span data-ttu-id="c3477-114">下載專案</span><span class="sxs-lookup"><span data-stu-id="c3477-114">Download the project</span></span>

<span data-ttu-id="c3477-115">使用以下程式碼在本機上複製專案。</span><span class="sxs-lookup"><span data-stu-id="c3477-115">Use the following code to clone the project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a><span data-ttu-id="c3477-116">了解拓撲</span><span class="sxs-lookup"><span data-stu-id="c3477-116">Understanding the topology</span></span>

<span data-ttu-id="c3477-117">下圖顯示透過此拓撲的資料流︰</span><span class="sxs-lookup"><span data-stu-id="c3477-117">The following diagram shows of how data flows through this topology:</span></span>

![拓撲](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="c3477-119">此圖以簡化的方式呈現拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3477-119">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="c3477-120">元件的多個執行個體會分散到叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="c3477-120">Multiple instances of the components are distributed across the nodes in the cluster.</span></span>


<span data-ttu-id="c3477-121">實作拓撲的 Trident 程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="c3477-121">The Trident code that implements the topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="c3477-122">此程式碼會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c3477-122">This code performs the following actions:</span></span>

1. <span data-ttu-id="c3477-123">從 Spout 建立資料流。</span><span class="sxs-lookup"><span data-stu-id="c3477-123">Creates a stream from the spout.</span></span> <span data-ttu-id="c3477-124">Spout 會擷取 Twitter 中的推文，然後篩選特定關鍵字 (在此範例中，為 love、music 和 coffee)。</span><span class="sxs-lookup"><span data-stu-id="c3477-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="c3477-125">會使用自訂函數 HashtagExtractor 擷取每則推文中的主題標籤。</span><span class="sxs-lookup"><span data-stu-id="c3477-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span></span> <span data-ttu-id="c3477-126">主題標籤會發出至資料流。</span><span class="sxs-lookup"><span data-stu-id="c3477-126">The hash tags are emitted to the stream.</span></span>

3. <span data-ttu-id="c3477-127">資料流接著會依主題標籤進行分組，然後傳遞給彙總工具。</span><span class="sxs-lookup"><span data-stu-id="c3477-127">The stream is grouped by hash tag, and passed to an aggregator.</span></span> <span data-ttu-id="c3477-128">此彙總工具會建立每個主題標籤出現次數的計數。</span><span class="sxs-lookup"><span data-stu-id="c3477-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="c3477-129">計數資料會保存在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="c3477-129">This data is persisted in memory.</span></span> <span data-ttu-id="c3477-130">最後，會發出含有主題標籤和計數的新資料流。</span><span class="sxs-lookup"><span data-stu-id="c3477-130">Finally, a new stream is emitted that contains the hash tag and the count.</span></span>

4. <span data-ttu-id="c3477-131">**FirstN** 組件會被套用來根據計數欄位僅傳回前 10 個值。</span><span class="sxs-lookup"><span data-stu-id="c3477-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span></span>

> [!NOTE]
> <span data-ttu-id="c3477-132">如需使用 Trident 的詳細資訊，請參閱 [Trident API 概觀](http://storm.apache.org/releases/current/Trident-API-Overview.html) 文件。</span><span class="sxs-lookup"><span data-stu-id="c3477-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="the-spout"></a><span data-ttu-id="c3477-133">Spout</span><span class="sxs-lookup"><span data-stu-id="c3477-133">The spout</span></span>

<span data-ttu-id="c3477-134">Spout **TwitterSpout** 會使用 [Twitter4j](http://twitter4j.org/en/) 從 Twitter 擷取推文。</span><span class="sxs-lookup"><span data-stu-id="c3477-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span></span> <span data-ttu-id="c3477-135">接著會對於 __love__、**music** 和 **coffee** 這些字建立篩選條件。</span><span class="sxs-lookup"><span data-stu-id="c3477-135">A filter is created for the words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="c3477-136">符合篩選條件的傳入推文 (status) 將儲存在連結的封鎖佇列中。</span><span class="sxs-lookup"><span data-stu-id="c3477-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="c3477-137">最後，會將項目拉出佇列，然後發出至拓撲。</span><span class="sxs-lookup"><span data-stu-id="c3477-137">Finally, items are pulled off the queue and emitted to the topology.</span></span>

### <a name="the-hashtagextractor"></a><span data-ttu-id="c3477-138">HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="c3477-138">The HashtagExtractor</span></span>

<span data-ttu-id="c3477-139">若要擷取主題標籤，可以使用 [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) 來擷取推文中包含的所有主題標籤。</span><span class="sxs-lookup"><span data-stu-id="c3477-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span></span> <span data-ttu-id="c3477-140">之後，會將這些發出至資料流。</span><span class="sxs-lookup"><span data-stu-id="c3477-140">These are then emitted to the stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="c3477-141">設定 Twitter</span><span class="sxs-lookup"><span data-stu-id="c3477-141">Configure Twitter</span></span>

<span data-ttu-id="c3477-142">使用以下步驟註冊新的 Twitter 應用程式，然後取得讀取 Twitter 內容所需的取用者和存取權杖資訊。</span><span class="sxs-lookup"><span data-stu-id="c3477-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span></span>

1. <span data-ttu-id="c3477-143">前往 [Twitter 應用程式](https://apps.twitter.com)，然後按一下 [建立新應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c3477-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span></span> <span data-ttu-id="c3477-144">填寫表單時，請將 [回呼 URL]  欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="c3477-144">When filling in the form, leave the **Callback URL** field empty.</span></span>

2. <span data-ttu-id="c3477-145">建立應用程式後，按一下 [金鑰和存取權杖]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c3477-145">When the app is created, click the **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="c3477-146">複製 [取用者金鑰] 和 [取用者密碼] 的資訊。</span><span class="sxs-lookup"><span data-stu-id="c3477-146">Copy the **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="c3477-147">如果沒有權杖，請在頁面底部選取 [建立我的存取權杖]  。</span><span class="sxs-lookup"><span data-stu-id="c3477-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="c3477-148">建立權杖後，複製 [存取權杖] 和 [存取權杖密碼] 的資訊。</span><span class="sxs-lookup"><span data-stu-id="c3477-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="c3477-149">在先前複製的 **TwitterSpoutTopology** 專案中，開啟 **resources/twitter4j.properties** 檔案，並新增先前步驟中所收集的資訊，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="c3477-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="c3477-150">建置拓撲</span><span class="sxs-lookup"><span data-stu-id="c3477-150">Build the topology</span></span>

<span data-ttu-id="c3477-151">請使用以下程式碼建置專案：</span><span class="sxs-lookup"><span data-stu-id="c3477-151">Use the following code to build the project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a><span data-ttu-id="c3477-152">測試拓撲</span><span class="sxs-lookup"><span data-stu-id="c3477-152">Test the topology</span></span>

<span data-ttu-id="c3477-153">請使用以下命令在本機上測試拓撲：</span><span class="sxs-lookup"><span data-stu-id="c3477-153">Use the following command to test the topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="c3477-154">拓撲啟動後，您應該會看到含有拓撲所發出之主題標籤和計數的偵錯資訊。</span><span class="sxs-lookup"><span data-stu-id="c3477-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span></span> <span data-ttu-id="c3477-155">輸出應該如下列文字所示：</span><span class="sxs-lookup"><span data-stu-id="c3477-155">The output should appear similar to the following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="c3477-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3477-156">Next steps</span></span>

<span data-ttu-id="c3477-157">現在，您已經在本機上測試拓撲，接著請探索如何部署拓撲： [部署和管理 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="c3477-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="c3477-158">您也可能會對下列 Storm 主題感興趣：</span><span class="sxs-lookup"><span data-stu-id="c3477-158">You may also be interested in the following Storm topics:</span></span>

* [<span data-ttu-id="c3477-159">使用 Maven 開發 Storm on HDInsight 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="c3477-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="c3477-160">使用 Visual Studio 開發 Storm on HDInsight 的 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="c3477-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="c3477-161">如需 HDinsight 的 Storm 範例：</span><span class="sxs-lookup"><span data-stu-id="c3477-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="c3477-162">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="c3477-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

