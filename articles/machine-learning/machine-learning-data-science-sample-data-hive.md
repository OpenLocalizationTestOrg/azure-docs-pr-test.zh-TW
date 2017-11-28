---
title: "Azure HDInsight Hive 資料表中的 aaaSample 資料 |Microsoft 文件"
description: "在 Azure HDInsight (Hadopop) Hive 資料表中進行資料向下取樣"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="a1e64-103">在 Azure HDInsight Hive 資料表中進行資料取樣</span><span class="sxs-lookup"><span data-stu-id="a1e64-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="a1e64-104">在本文中，我們會說明如何 toodown 範例資料儲存在使用 Hive 查詢的 Azure HDInsight Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="a1e64-104">In this article, we describe how toodown-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="a1e64-105">我們將討論三個普遍使用的取樣方法：</span><span class="sxs-lookup"><span data-stu-id="a1e64-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="a1e64-106">統一隨機取樣</span><span class="sxs-lookup"><span data-stu-id="a1e64-106">Uniform random sampling</span></span>
* <span data-ttu-id="a1e64-107">依群組隨機取樣</span><span class="sxs-lookup"><span data-stu-id="a1e64-107">Random sampling by groups</span></span>
* <span data-ttu-id="a1e64-108">分層取樣</span><span class="sxs-lookup"><span data-stu-id="a1e64-108">Stratified sampling</span></span>

<span data-ttu-id="a1e64-109">hello 下列**功能表**連結 tootopics 描述如何從各種不同的儲存體環境 toosample 資料。</span><span class="sxs-lookup"><span data-stu-id="a1e64-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="a1e64-110">**為何要對您的資料進行取樣？**</span><span class="sxs-lookup"><span data-stu-id="a1e64-110">**Why sample your data?**</span></span>
<span data-ttu-id="a1e64-111">如果您計劃 tooanalyze hello 資料集很大，它通常是個不錯的主意 toodown 範例 hello 資料 tooreduce 它 tooa 小型但具代表性且更容易管理的大小。</span><span class="sxs-lookup"><span data-stu-id="a1e64-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="a1e64-112">這有助於資料了解、探索和功能工程。</span><span class="sxs-lookup"><span data-stu-id="a1e64-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="a1e64-113">Hello 小組資料科學程序在其角色將是 tooenable 快速原型化的 hello 資料處理函式和機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="a1e64-113">Its role in hello Team Data Science Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="a1e64-114">此取樣工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。</span><span class="sxs-lookup"><span data-stu-id="a1e64-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-toosubmit-hive-queries"></a><span data-ttu-id="a1e64-115">如何 toosubmit Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="a1e64-115">How toosubmit Hive queries</span></span>
<span data-ttu-id="a1e64-116">您可以從 hello hello hello Hadoop 叢集的前端節點上的 Hadoop 命令列主控台提交 hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="a1e64-116">Hive queries can be submitted from hello Hadoop Command Line console on hello head node of hello Hadoop cluster.</span></span> <span data-ttu-id="a1e64-117">此登入 hello 前端節點的 hello Hadoop 叢集上，開啟 toodo hello Hadoop 命令列主控台中，並送出 hello Hive 查詢從該處。</span><span class="sxs-lookup"><span data-stu-id="a1e64-117">toodo this, log into hello head node of hello Hadoop cluster, open hello Hadoop Command Line console, and submit hello Hive queries from there.</span></span> <span data-ttu-id="a1e64-118">如需提交 Hive 查詢 hello Hadoop 命令列主控台中的指示，請參閱[如何 tooSubmit Hive 查詢](machine-learning-data-science-move-hive-tables.md#submit)。</span><span class="sxs-lookup"><span data-stu-id="a1e64-118">For instructions on submitting Hive queries in hello Hadoop Command Line console, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="a1e64-119"><a name="uniform"></a> 統一隨機取樣</span><span class="sxs-lookup"><span data-stu-id="a1e64-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="a1e64-120">統一的隨機取樣，表示 hello 資料集中的每個資料列的取樣相等的機會。</span><span class="sxs-lookup"><span data-stu-id="a1e64-120">Uniform random sampling means that each row in hello data set has an equal chance of being sampled.</span></span> <span data-ttu-id="a1e64-121">這可以在 hello 內部"select"查詢中，加入額外的欄位 rand （） toohello 資料集來實作，並在 hello 外部 「 選取 」 查詢該隨機欄位條件。</span><span class="sxs-lookup"><span data-stu-id="a1e64-121">This can be implemented by adding an extra field rand() toohello data set in hello inner "select" query, and in hello outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="a1e64-122">查詢範例如下：</span><span class="sxs-lookup"><span data-stu-id="a1e64-122">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

<span data-ttu-id="a1e64-123">在這裡，`<sample rate, 0-1>`指定的記錄 hello 使用者想 toosample hello 比例。</span><span class="sxs-lookup"><span data-stu-id="a1e64-123">Here, `<sample rate, 0-1>` specifies hello proportion of records that hello users want toosample.</span></span>

## <span data-ttu-id="a1e64-124"><a name="group"></a> 依群組隨機取樣</span><span class="sxs-lookup"><span data-stu-id="a1e64-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="a1e64-125">分類資料取樣，您可能想 tooeither 包含或排除所有的類別變數的一些特定值的 hello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a1e64-125">When sampling categorical data, you may want tooeither include or exclude all of hello instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="a1e64-126">這就是「依群組取樣」的意思。</span><span class="sxs-lookup"><span data-stu-id="a1e64-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="a1e64-127">例如，如果您有 「 狀態 」 的類別變數時，具有的值開頭為 NY MA、 CA、 NJ、 PA、 等，您要記錄的 hello 相同狀態會永遠在一起，它們會取樣或不。</span><span class="sxs-lookup"><span data-stu-id="a1e64-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of hello same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="a1e64-128">以下是依群組取樣的查詢範例：</span><span class="sxs-lookup"><span data-stu-id="a1e64-128">Here is an example query that samples by group:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <span data-ttu-id="a1e64-129"><a name="stratified"></a>分層取樣</span><span class="sxs-lookup"><span data-stu-id="a1e64-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="a1e64-130">隨機取樣與尊重 tooa 類別變數時取得的 hello 範例會使用該類別的值中 hello （stratified sampling) 相同的比例，如 hello 父母體擴展所取得的 hello 範例所示。</span><span class="sxs-lookup"><span data-stu-id="a1e64-130">Random sampling is stratified with respect tooa categorical variable when hello samples obtained have values of that categorical that are in hello same ratio as in hello parent population from which hello samples were obtained.</span></span> <span data-ttu-id="a1e64-131">使用 hello 上述相同的範例，假設您的資料有子母體擴展依狀態、 說 NJ 具備 100 觀察、 開頭為 NY 有 60 的觀察值，且 WA 300 的觀察值。</span><span class="sxs-lookup"><span data-stu-id="a1e64-131">Using hello same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="a1e64-132">如果您指定的 hello 速率分層取樣 toobe 0.5，則 hello 範例取得應該有大約 50、 30 和 150 NJ 及開頭為 NY，WA 的觀察分別。</span><span class="sxs-lookup"><span data-stu-id="a1e64-132">If you specify hello rate of stratified sampling toobe 0.5, then hello sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="a1e64-133">查詢範例如下：</span><span class="sxs-lookup"><span data-stu-id="a1e64-133">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


<span data-ttu-id="a1e64-134">如需可在 Hive 中使用的進一步進階取樣方法相關資訊，請參閱 [LanguageManual 取樣](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling)。</span><span class="sxs-lookup"><span data-stu-id="a1e64-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

