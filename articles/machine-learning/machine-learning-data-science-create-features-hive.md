---
title: "針對使用 Hive 查詢之 Hadoop 叢集中的資料建立特性 | Microsoft Docs"
description: "Hive 查詢的範例，產生儲存在 Azure HDInsight Hadoop 叢集中之資料中的特性。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e027a6ffcb63868be13432870e484c5cbf2eef4b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="1060e-103">針對使用 Hive 查詢之 Hadoop 叢集中的資料建立特性</span><span class="sxs-lookup"><span data-stu-id="1060e-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="1060e-104">本文件說明如何使用 Hive 查詢，針對儲存在 Azure HDInsight Hadoop 叢集中的資料建立特徵。</span><span class="sxs-lookup"><span data-stu-id="1060e-104">This document shows how to create features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="1060e-105">這些 Hive 查詢會使用針對其提供指令碼的內嵌 Hive 使用者定義函式 (UDF)。</span><span class="sxs-lookup"><span data-stu-id="1060e-105">These Hive queries use embedded Hive User Defined Functions (UDFs), the scripts for which are provided.</span></span>

<span data-ttu-id="1060e-106">建立特徵所需的作業可能耗用大量記憶體。</span><span class="sxs-lookup"><span data-stu-id="1060e-106">The operations needed to create features can be memory intensive.</span></span> <span data-ttu-id="1060e-107">在此情況下，Hive 查詢的效能會變得十分重要，可微調某些參數來改善。</span><span class="sxs-lookup"><span data-stu-id="1060e-107">The performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="1060e-108">最後一節討論如何微調這些參數。</span><span class="sxs-lookup"><span data-stu-id="1060e-108">The tuning of these parameters is discussed in the final section.</span></span>

<span data-ttu-id="1060e-109">[GitHub 存放庫](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)中也會提供 [NYC 計程車車程資料](http://chriswhong.com/open-data/foil_nyc_taxi/)案例特定的查詢範例。</span><span class="sxs-lookup"><span data-stu-id="1060e-109">Examples of the queries that are presented are specific to the [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="1060e-110">這些查詢已經具備指定的資料結構描述，且準備好進行提交來執行。</span><span class="sxs-lookup"><span data-stu-id="1060e-110">These queries already have data schema specified and are ready to be submitted to run.</span></span> <span data-ttu-id="1060e-111">最後一節也會討論使用者可以微調的參數，以改善 Hive 查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="1060e-111">In the final section, parameters that users can tune so that the performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="1060e-112">這個 **功能表** 所連結的主題會說明如何在各種環境中建立資料的特徵。</span><span class="sxs-lookup"><span data-stu-id="1060e-112">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="1060e-113">此工作是 [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="1060e-113">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1060e-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="1060e-114">Prerequisites</span></span>
<span data-ttu-id="1060e-115">本文假設您已經：</span><span class="sxs-lookup"><span data-stu-id="1060e-115">This article assumes that you have:</span></span>

* <span data-ttu-id="1060e-116">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1060e-116">Created an Azure storage account.</span></span> <span data-ttu-id="1060e-117">如需指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="1060e-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="1060e-118">佈建含有 HDInsight 服務的自訂 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="1060e-118">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="1060e-119">如需指示，請參閱 [自訂適用於進階分析的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="1060e-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="1060e-120">已將資料上傳至 Azure HDInsight Hadoop 叢集中的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="1060e-120">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="1060e-121">如果沒有，請遵循 [建立資料並載入 Hive 資料表](machine-learning-data-science-move-hive-tables.md) ，先將資料上傳至 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="1060e-121">If it has not, please follow [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="1060e-122">啟用叢集的遠端存取。</span><span class="sxs-lookup"><span data-stu-id="1060e-122">Enabled remote access to the cluster.</span></span> <span data-ttu-id="1060e-123">如需指示，請參閱 [存取 Hadoop 叢集的前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)。</span><span class="sxs-lookup"><span data-stu-id="1060e-123">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="1060e-124"><a name="hive-featureengineering"></a>功能產生</span><span class="sxs-lookup"><span data-stu-id="1060e-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="1060e-125">在本節中，說明可以使用 Hive 查詢特性之數個方式的範例。</span><span class="sxs-lookup"><span data-stu-id="1060e-125">In this section, several examples of the ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="1060e-126">一旦產生額外功能之後，就可以將它們當成資料行新增至現有的資料表，或是建立具有其他功能和主索引鍵的新資料表 (然後與原始資料表聯結)。</span><span class="sxs-lookup"><span data-stu-id="1060e-126">Once you have generated additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, which can then be joined with the original table.</span></span> <span data-ttu-id="1060e-127">以下是顯示的範例：</span><span class="sxs-lookup"><span data-stu-id="1060e-127">Here are the examples presented:</span></span>

1. [<span data-ttu-id="1060e-128">以頻率為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="1060e-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="1060e-129">二進位分類中類別變數的風險</span><span class="sxs-lookup"><span data-stu-id="1060e-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="1060e-130">從日期時間欄位擷取功能</span><span class="sxs-lookup"><span data-stu-id="1060e-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="1060e-131">從文字欄位擷取功能</span><span class="sxs-lookup"><span data-stu-id="1060e-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="1060e-132">計算 GPS 座標間的距離</span><span class="sxs-lookup"><span data-stu-id="1060e-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="1060e-133"><a name="hive-frequencyfeature"></a>以頻率為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="1060e-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="1060e-134">計算類別變數層級的頻率，或是來自多個類別變數之特定層級組合的頻率，通常很實用。</span><span class="sxs-lookup"><span data-stu-id="1060e-134">It is often useful to calculate the frequencies of the levels of a categorical variable, or the frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="1060e-135">使用者可以使用下列指令碼來計算這些頻率：</span><span class="sxs-lookup"><span data-stu-id="1060e-135">Users can use the following script to calculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="1060e-136"><a name="hive-riskfeature"></a>二進位分類中類別變數的風險</span><span class="sxs-lookup"><span data-stu-id="1060e-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="1060e-137">在二進位分類中，若使用的模型只會採用數值功能，我們就需要將非數值類別變數轉換成數值功能。</span><span class="sxs-lookup"><span data-stu-id="1060e-137">In binary classification, we need to convert non-numeric categorical variables into numeric features when the models being used only take numeric features.</span></span> <span data-ttu-id="1060e-138">您可以使用數值風險來取代每個非數值層級，藉以完成這個動作。</span><span class="sxs-lookup"><span data-stu-id="1060e-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="1060e-139">在本節中，我們將說明一些計算類別變數風險值 (記錄機率) 的泛型 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="1060e-139">In this section, we show some generic Hive queries that calculate the risk values (log odds) of a categorical variable.</span></span>

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

<span data-ttu-id="1060e-140">這個範例會設定變數 `smooth_param1` 和 `smooth_param2`，以減緩從資料計算得來的風險值。</span><span class="sxs-lookup"><span data-stu-id="1060e-140">In this example, variables `smooth_param1` and `smooth_param2` are set to smooth the risk values calculated from the data.</span></span> <span data-ttu-id="1060e-141">風險範圍介於-Inf 和 Inf 之間。</span><span class="sxs-lookup"><span data-stu-id="1060e-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="1060e-142">風險 > 0 表示目標等於 1 的機率大於 0.5。</span><span class="sxs-lookup"><span data-stu-id="1060e-142">A risks > 0 indicates that the probability that the target is equal to 1 is greater than 0.5.</span></span>

<span data-ttu-id="1060e-143">計算出風險資料表之後，使用者就可以藉由將資料表聯結至風險資料表，來將風險值指派給該資料表。</span><span class="sxs-lookup"><span data-stu-id="1060e-143">After the risk table is calculated, users can assign risk values to a table by joining it with the risk table.</span></span> <span data-ttu-id="1060e-144">Hive 聯結查詢已在上一節中提供。</span><span class="sxs-lookup"><span data-stu-id="1060e-144">The Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="1060e-145"><a name="hive-datefeatures"></a>從日期時間欄位擷取功能</span><span class="sxs-lookup"><span data-stu-id="1060e-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="1060e-146">Hive 會和一組 UDF 一起出現，用來處理日期時間欄位。</span><span class="sxs-lookup"><span data-stu-id="1060e-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="1060e-147">在 Hive 中，預設的日期時間格式是 'yyyy-MM-dd 00:00:00' (例如 '1970-01-01 12:21:32')。</span><span class="sxs-lookup"><span data-stu-id="1060e-147">In Hive, the default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="1060e-148">本節會顯示擷取月份日期和來自日期時間欄位的月份範例，以及其他可將預設格式以外格式的日期時間字串轉換為預設格式的日期時間字串範例。</span><span class="sxs-lookup"><span data-stu-id="1060e-148">In this section, we show examples that extract the day of a month, the month from a datetime field, and other examples that convert a datetime string in a format other than the default format to a datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="1060e-149">這個 Hive 查詢假設 *&#60;datetime field>* 是預設的日期時間格式。</span><span class="sxs-lookup"><span data-stu-id="1060e-149">This Hive query assumes that the *&#60;datetime field>* is in the default datetime format.</span></span>

<span data-ttu-id="1060e-150">如果日期時間欄位不是預設格式，您需要先將日期時間欄位轉換為 Unix 時間戳記，然後將 Unix 時間戳記轉換為預設格式的日期時間字串。</span><span class="sxs-lookup"><span data-stu-id="1060e-150">If a datetime field is not in the default format, you need to convert the datetime field into Unix time stamp first, and then convert the Unix time stamp to a datetime string that is in the default format.</span></span> <span data-ttu-id="1060e-151">將日期時間為預設格式之後，使用者就可以套用內嵌的日期時間 UDF 來擷取功能。</span><span class="sxs-lookup"><span data-stu-id="1060e-151">When the datetime is in default format, users can apply the embedded datetime UDFs to extract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of the datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="1060e-152">在這個查詢中，如果 *&#60;datetime field>* 具有類似 *03/26/2015 12:04:39* 的模式，則 *'&#60;pattern of the datetime field>'* 應該是 `'MM/dd/yyyy HH:mm:ss'`。</span><span class="sxs-lookup"><span data-stu-id="1060e-152">In this query, if the *&#60;datetime field>* has the pattern like *03/26/2015 12:04:39*, the *'&#60;pattern of the datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="1060e-153">若要進行測試，使用者可以執行</span><span class="sxs-lookup"><span data-stu-id="1060e-153">To test it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="1060e-154">佈建叢集時，這個查詢中的 *hivesampletable* 預設會預先安裝於所有 Azure HDInsight Hadoop 叢集中。</span><span class="sxs-lookup"><span data-stu-id="1060e-154">The *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when the clusters are provisioned.</span></span>

### <span data-ttu-id="1060e-155"><a name="hive-textfeatures"></a>從文字欄位擷取功能</span><span class="sxs-lookup"><span data-stu-id="1060e-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="1060e-156">當 Hive 資料表具有一個文字欄位且其中包含以空格分隔的文字字串時，下列查詢便會擷取字串長度，以及字串中的字數。</span><span class="sxs-lookup"><span data-stu-id="1060e-156">When the Hive table has a text field that contains a string of words that are delimited by spaces, the following query extracts the length of the string, and the number of words in the string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="1060e-157"><a name="hive-gpsdistance"></a>計算 GPS 座標組之間的距離</span><span class="sxs-lookup"><span data-stu-id="1060e-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="1060e-158">本節中提供的查詢可直接套用至「NYC 計程車車程資料」。</span><span class="sxs-lookup"><span data-stu-id="1060e-158">The query given in this section can be directly applied to the NYC Taxi Trip Data.</span></span> <span data-ttu-id="1060e-159">此查詢的目的是示範如何在 Hive 中套用內嵌的數學函式來產生功能。</span><span class="sxs-lookup"><span data-stu-id="1060e-159">The purpose of this query is to show how to apply an embedded mathematical functions in Hive to generate features.</span></span>

<span data-ttu-id="1060e-160">這個查詢中所使用的欄位是上車與下車位置的 GPS 座標，其名稱為 *pickup\_longitude*、*pickup\_latitude*、*dropoff\_longitude* 和 *dropoff\_latitude*。</span><span class="sxs-lookup"><span data-stu-id="1060e-160">The fields that are used in this query are the GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="1060e-161">計算上車與下車座標間直線距離的查詢如下：</span><span class="sxs-lookup"><span data-stu-id="1060e-161">The queries that calculate the direct distance between the pickup and dropoff coordinates are:</span></span>

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

<span data-ttu-id="1060e-162">您可以在<a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">可移動的類型指令碼</a>網站 (作者為 Peter Lapisu) 上找到計算兩個 GPS 座標間之距離的數學方程式。</span><span class="sxs-lookup"><span data-stu-id="1060e-162">The mathematical equations that calculate the distance between two GPS coordinates can be found on the <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="1060e-163">在他的 Javascript 中，函式 `toRad()` 只是 *lat_or_lon*pi/180*，可將角度轉換為弧度。</span><span class="sxs-lookup"><span data-stu-id="1060e-163">In his Javascript, the function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees to radians.</span></span> <span data-ttu-id="1060e-164">此處的 *lat_or_lon* 為緯度或經度。</span><span class="sxs-lookup"><span data-stu-id="1060e-164">Here, *lat_or_lon* is the latitude or longitude.</span></span> <span data-ttu-id="1060e-165">由於 Hive 不提供函式 `atan2`，但提供函式 `atan`，因此 `atan2` 函式是由上述 Hive 查詢中的 `atan` 函式以 <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a> 中提供的定義來實作。</span><span class="sxs-lookup"><span data-stu-id="1060e-165">Since Hive does not provide the function `atan2`, but provides the function `atan`, the `atan2` function is implemented by `atan` function in the above Hive query using the definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![建立工作區](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="1060e-167">您可以在 <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a> 上的**內建函式**一節中找到 Hive 內嵌 UDF 的完整清單。</span><span class="sxs-lookup"><span data-stu-id="1060e-167">A full list of Hive embedded UDFs can be found in the **Built-in Functions** section on the <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="1060e-168"><a name="tuning"></a> 進階主題：微調 Hive 參數以提升查詢速度</span><span class="sxs-lookup"><span data-stu-id="1060e-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters to Improve Query Speed</span></span>
<span data-ttu-id="1060e-169">Hive 叢集的預設參數設定可能不適合 Hive 查詢以及查詢正在處理的資料。</span><span class="sxs-lookup"><span data-stu-id="1060e-169">The default parameter settings of Hive cluster might not be suitable for the Hive queries and the data that the queries are processing.</span></span> <span data-ttu-id="1060e-170">本節將討論一些使用者可以微調的參數，來提升 Hive 查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="1060e-170">In this section, we discuss some parameters that users can tune that improve the performance of Hive queries.</span></span> <span data-ttu-id="1060e-171">使用者需要在處理資料的查詢之前新增參數微調查詢。</span><span class="sxs-lookup"><span data-stu-id="1060e-171">Users need to add the parameter tuning queries before the queries of processing data.</span></span>

1. <span data-ttu-id="1060e-172">**Java 堆積空間**：對於涉及聯結大型資料集或處理長記錄的查詢，常見的一項錯誤是**堆積空間不足**。</span><span class="sxs-lookup"><span data-stu-id="1060e-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of the common error.</span></span> <span data-ttu-id="1060e-173">這可藉由將參數 *mapreduce.map.java.opts* 和 *mapreduce.task.io.sort.mb* 設定為所需的值來進行微調。</span><span class="sxs-lookup"><span data-stu-id="1060e-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* to desired values.</span></span> <span data-ttu-id="1060e-174">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="1060e-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="1060e-175">這個參數會配置 4 GB 記憶體給 Java 堆積空間，也會藉由配置更多記憶體來使排序更有效率。</span><span class="sxs-lookup"><span data-stu-id="1060e-175">This parameter allocates 4GB memory to Java heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="1060e-176">如果發生任何與堆積空間相關的工作失敗錯誤，那麼使用這些配置會是個好主意。</span><span class="sxs-lookup"><span data-stu-id="1060e-176">It is a good idea to play with these allocations if there are any job failure errors related to heap space.</span></span>

1. <span data-ttu-id="1060e-177">**DFS 區塊大小** ：這個參數會設定檔案系統所儲存的最小資料單位。</span><span class="sxs-lookup"><span data-stu-id="1060e-177">**DFS block size** : This parameter sets the smallest unit of data that the file system stores.</span></span> <span data-ttu-id="1060e-178">例如，如果 DFS 區塊大小為 128 MB，則任何大小小於等於 128 MB 的資料都會儲存於單一區塊中，而大於 128 MB 的資料則會配置額外的區塊。</span><span class="sxs-lookup"><span data-stu-id="1060e-178">As an example, if the DFS block size is 128MB, then any data of size less than and up to 128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="1060e-179">選擇非常小的區塊大小會在 Hadoop 中造成極大的負荷，因為名稱節點必須處理更多要求，以尋找與檔案有關的相關區塊。</span><span class="sxs-lookup"><span data-stu-id="1060e-179">Choosing a very small block size causes large overheads in Hadoop since the name node has to process many more requests to find the relevant block pertaining to the file.</span></span> <span data-ttu-id="1060e-180">在處理 GB (或更大型) 資料時，建議的設定如下：</span><span class="sxs-lookup"><span data-stu-id="1060e-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="1060e-181">**將 Hive 中的聯結作業最佳化** ：儘管 Map/Reduce 架構中的聯結作業通常是在縮減階段執行，但有時可藉由在對應階段中排程聯結 (亦稱為 "mapjoin") 來得到大量的收穫。</span><span class="sxs-lookup"><span data-stu-id="1060e-181">**Optimizing join operation in Hive** : While join operations in the map/reduce framework typically take place in the reduce phase, sometimes, enormous gains can be achieved by scheduling joins in the map phase (also called "mapjoins").</span></span> <span data-ttu-id="1060e-182">若要在適當時機引導 Hive 執行這個動作，我們可以設定：</span><span class="sxs-lookup"><span data-stu-id="1060e-182">To direct Hive to do this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="1060e-183">**指定 Hive 的對應程式數目** ：儘管 Hadoop 允許使用者設定縮減程式的數目，但使用者通常不會設定對應程式的數目。</span><span class="sxs-lookup"><span data-stu-id="1060e-183">**Specifying the number of mappers to Hive** : While Hadoop allows the user to set the number of reducers, the number of mappers is typically not be set by the user.</span></span> <span data-ttu-id="1060e-184">允許對這個數目進行某種程度控制的技巧是選擇 Hadoop 變數 *mapred.min.split.size* 和*mapred.max.split.size*，因為每個對應工作的大小由下列決定：</span><span class="sxs-lookup"><span data-stu-id="1060e-184">A trick that allows some degree of control on this number is to choose the Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as the size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="1060e-185">一般而言，*mapred.min.split.size* 的預設值為 0，*mapred.max.split.size* 的預設值是 **Long.MAX**，而 *dfs.block.size* 的預設值則是 64 MB。</span><span class="sxs-lookup"><span data-stu-id="1060e-185">Typically, the default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="1060e-186">誠如所見，若指定了資料大小，則藉由「設定」這些參數來微調它們，讓我們能夠微調所使用的對應程式數目。</span><span class="sxs-lookup"><span data-stu-id="1060e-186">As we can see, given the data size, tuning these parameters by "setting" them allows us to tune the number of mappers used.</span></span>
4. <span data-ttu-id="1060e-187">以下將提及最佳化 Hive 效能的其他數個更 **進階選項** 。</span><span class="sxs-lookup"><span data-stu-id="1060e-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="1060e-188">這些選項讓您能夠設定配置的記憶體來對應和縮減工作，而且在調整效能時非常實用。</span><span class="sxs-lookup"><span data-stu-id="1060e-188">These allow you to set the memory allocated to map and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="1060e-189">請記住， *mapreduce.reduce.memory.mb* 不能大於 Hadoop 叢集中每個背景工作角色節點的實際記憶體大小。</span><span class="sxs-lookup"><span data-stu-id="1060e-189">Please keep in mind that the *mapreduce.reduce.memory.mb* cannot be greater than the physical memory size of each worker node in the Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

