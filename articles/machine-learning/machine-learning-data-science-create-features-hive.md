---
title: "使用 Hive 查詢 Hadoop 叢集中的資料 aaaCreate 功能 |Microsoft 文件"
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
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="df4b6-103">針對使用 Hive 查詢之 Hadoop 叢集中的資料建立特性</span><span class="sxs-lookup"><span data-stu-id="df4b6-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="df4b6-104">本文件示範 toocreate 功能資料儲存在 Azure HDInsight Hadoop 叢集中使用 Hive 查詢的方式。</span><span class="sxs-lookup"><span data-stu-id="df4b6-104">This document shows how toocreate features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="df4b6-105">這些 Hive 查詢使用內嵌 hive 控制檔的使用者定義函數 (Udf)，提供其 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="df4b6-105">These Hive queries use embedded Hive User Defined Functions (UDFs), hello scripts for which are provided.</span></span>

<span data-ttu-id="df4b6-106">hello 作業所需 toocreate 功能可以是需要大量的記憶體。</span><span class="sxs-lookup"><span data-stu-id="df4b6-106">hello operations needed toocreate features can be memory intensive.</span></span> <span data-ttu-id="df4b6-107">hello 的 Hive 查詢的效能變得十分重要，在此情況下，來調整特定參數便可改善。</span><span class="sxs-lookup"><span data-stu-id="df4b6-107">hello performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="df4b6-108">hello 微調這些參數的 hello 最後一節中討論。</span><span class="sxs-lookup"><span data-stu-id="df4b6-108">hello tuning of these parameters is discussed in hello final section.</span></span>

<span data-ttu-id="df4b6-109">顯示 hello 查詢的範例包括特定 toohello [NYC 計程車路線資料](http://chriswhong.com/open-data/foil_nyc_taxi/)案例也會提供在[GitHub 儲存機制](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)。</span><span class="sxs-lookup"><span data-stu-id="df4b6-109">Examples of hello queries that are presented are specific toohello [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="df4b6-110">這些查詢已經有指定的資料結構描述，而且準備好 toobe 提交 toorun。</span><span class="sxs-lookup"><span data-stu-id="df4b6-110">These queries already have data schema specified and are ready toobe submitted toorun.</span></span> <span data-ttu-id="df4b6-111">在 hello 最後一節中也會討論參數，可讓使用者可以調整，以便可以改善 hello 的 Hive 查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="df4b6-111">In hello final section, parameters that users can tune so that hello performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="df4b6-112">這**功能表**連結 tootopics 描述 toocreate 各種環境中的資料的功能。</span><span class="sxs-lookup"><span data-stu-id="df4b6-112">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="df4b6-113">這項工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。</span><span class="sxs-lookup"><span data-stu-id="df4b6-113">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df4b6-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="df4b6-114">Prerequisites</span></span>
<span data-ttu-id="df4b6-115">本文假設您已經：</span><span class="sxs-lookup"><span data-stu-id="df4b6-115">This article assumes that you have:</span></span>

* <span data-ttu-id="df4b6-116">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="df4b6-116">Created an Azure storage account.</span></span> <span data-ttu-id="df4b6-117">如需指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="df4b6-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="df4b6-118">自訂的 Hadoop 叢集以 hello HDInsight 服務使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="df4b6-118">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="df4b6-119">如需指示，請參閱 [自訂適用於進階分析的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="df4b6-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="df4b6-120">hello 資料已上傳的 tooHive Azure HDInsight Hadoop 叢集中的資料表。</span><span class="sxs-lookup"><span data-stu-id="df4b6-120">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="df4b6-121">如果沒有，請依照[建立和載入資料 tooHive 資料表](machine-learning-data-science-move-hive-tables.md)tooupload 資料 tooHive 資料表第一次。</span><span class="sxs-lookup"><span data-stu-id="df4b6-121">If it has not, please follow [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="df4b6-122">啟用遠端存取 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="df4b6-122">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="df4b6-123">如果您需要的指示，請參閱[存取 hello 的 Hadoop 叢集前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)。</span><span class="sxs-lookup"><span data-stu-id="df4b6-123">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="df4b6-124"><a name="hive-featureengineering"></a>功能產生</span><span class="sxs-lookup"><span data-stu-id="df4b6-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="df4b6-125">在本節中描述的 hello 方法中的功能可以會產生使用 Hive 查詢的數個範例。</span><span class="sxs-lookup"><span data-stu-id="df4b6-125">In this section, several examples of hello ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="df4b6-126">一旦您已經產生額外的功能，您可以將活動當做資料行 toohello 現有的資料表加入或建立新的資料表與 hello 額外的功能和主索引鍵，然後可以與 hello 原始資料表聯結。</span><span class="sxs-lookup"><span data-stu-id="df4b6-126">Once you have generated additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, which can then be joined with hello original table.</span></span> <span data-ttu-id="df4b6-127">以下是顯示 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="df4b6-127">Here are hello examples presented:</span></span>

1. [<span data-ttu-id="df4b6-128">以頻率為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="df4b6-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="df4b6-129">二進位分類中類別變數的風險</span><span class="sxs-lookup"><span data-stu-id="df4b6-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="df4b6-130">從日期時間欄位擷取功能</span><span class="sxs-lookup"><span data-stu-id="df4b6-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="df4b6-131">從文字欄位擷取功能</span><span class="sxs-lookup"><span data-stu-id="df4b6-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="df4b6-132">計算 GPS 座標間的距離</span><span class="sxs-lookup"><span data-stu-id="df4b6-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="df4b6-133"><a name="hive-frequencyfeature"></a>以頻率為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="df4b6-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="df4b6-134">通常會很有用的 toocalculate hello 頻率的 hello 層級的類別變數或從多個類別變數的層級的特定組合 hello 頻率。</span><span class="sxs-lookup"><span data-stu-id="df4b6-134">It is often useful toocalculate hello frequencies of hello levels of a categorical variable, or hello frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="df4b6-135">使用者可以使用下列指令碼 toocalculate hello 這些頻率：</span><span class="sxs-lookup"><span data-stu-id="df4b6-135">Users can use hello following script toocalculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="df4b6-136"><a name="hive-riskfeature"></a>二進位分類中類別變數的風險</span><span class="sxs-lookup"><span data-stu-id="df4b6-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="df4b6-137">在二進位分類中，我們需要類別變數則 tooconvert 非數值成數值特徵時只使用 hello 模型需要數值特徵。</span><span class="sxs-lookup"><span data-stu-id="df4b6-137">In binary classification, we need tooconvert non-numeric categorical variables into numeric features when hello models being used only take numeric features.</span></span> <span data-ttu-id="df4b6-138">您可以使用數值風險來取代每個非數值層級，藉以完成這個動作。</span><span class="sxs-lookup"><span data-stu-id="df4b6-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="df4b6-139">在本節中，我們會示範計算的類別變數的 hello 風險值 （對數勝算的特徵） 某些泛型 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="df4b6-139">In this section, we show some generic Hive queries that calculate hello risk values (log odds) of a categorical variable.</span></span>

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

<span data-ttu-id="df4b6-140">在此範例中，變數`smooth_param1`和`smooth_param2`設定 toosmooth hello 風險值計算從 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="df4b6-140">In this example, variables `smooth_param1` and `smooth_param2` are set toosmooth hello risk values calculated from hello data.</span></span> <span data-ttu-id="df4b6-141">風險範圍介於-Inf 和 Inf 之間。</span><span class="sxs-lookup"><span data-stu-id="df4b6-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="df4b6-142">風險 > 0 表示該 hello 目標是相等的 too1 hello 機率大於 0.5。</span><span class="sxs-lookup"><span data-stu-id="df4b6-142">A risks > 0 indicates that hello probability that hello target is equal too1 is greater than 0.5.</span></span>

<span data-ttu-id="df4b6-143">計算 hello 風險資料表之後，使用者可以指派風險值 tooa 資料表聯結與 hello 風險資料表。</span><span class="sxs-lookup"><span data-stu-id="df4b6-143">After hello risk table is calculated, users can assign risk values tooa table by joining it with hello risk table.</span></span> <span data-ttu-id="df4b6-144">上一節中提供 hello Hive 聯結查詢。</span><span class="sxs-lookup"><span data-stu-id="df4b6-144">hello Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="df4b6-145"><a name="hive-datefeatures"></a>從日期時間欄位擷取功能</span><span class="sxs-lookup"><span data-stu-id="df4b6-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="df4b6-146">Hive 會和一組 UDF 一起出現，用來處理日期時間欄位。</span><span class="sxs-lookup"><span data-stu-id="df4b6-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="df4b6-147">在 Hive hello 預設日期時間格式是 'yyyy MM dd 00:00:00' (' 1970年-01-01 12:21:32 ' 例如)。</span><span class="sxs-lookup"><span data-stu-id="df4b6-147">In Hive, hello default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="df4b6-148">在本節中，我們會示範擷取 hello 月份、 日期時間欄位中，從 hello 月份天數的範例和以外 hello 預設格式 tooa datetime 字串的預設格式轉換的日期時間格式字串的其他範例。</span><span class="sxs-lookup"><span data-stu-id="df4b6-148">In this section, we show examples that extract hello day of a month, hello month from a datetime field, and other examples that convert a datetime string in a format other than hello default format tooa datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="df4b6-149">此登錄區查詢假設該 hello *&#60; 日期時間欄位 >* hello 預設日期時間格式。</span><span class="sxs-lookup"><span data-stu-id="df4b6-149">This Hive query assumes that hello *&#60;datetime field>* is in hello default datetime format.</span></span>

<span data-ttu-id="df4b6-150">如果 datetime 欄位不是 hello 預設格式，您需要 tooconvert hello datetime 欄位 Unix 時間戳記至第一次，而且轉換 hello 的 Unix 時間戳記 tooa datetime 的字串，則是位在 hello 預設格式。</span><span class="sxs-lookup"><span data-stu-id="df4b6-150">If a datetime field is not in hello default format, you need tooconvert hello datetime field into Unix time stamp first, and then convert hello Unix time stamp tooa datetime string that is in hello default format.</span></span> <span data-ttu-id="df4b6-151">當 hello datetime 的預設格式，使用者可以套用 hello 內嵌 datetime Udf tooextract 功能。</span><span class="sxs-lookup"><span data-stu-id="df4b6-151">When hello datetime is in default format, users can apply hello embedded datetime UDFs tooextract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="df4b6-152">在此查詢中，如果 hello *（& s) #60; 日期時間欄位 >*具有類似的 hello 模式*03/26/2015年 12:04:39*，hello *' （& s) #60; hello 日期時間欄位的模式 >'*應該是`'MM/dd/yyyy HH:mm:ss'`.</span><span class="sxs-lookup"><span data-stu-id="df4b6-152">In this query, if hello *&#60;datetime field>* has hello pattern like *03/26/2015 12:04:39*, hello *'&#60;pattern of hello datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="df4b6-153">tootest 使用者可以執行它，</span><span class="sxs-lookup"><span data-stu-id="df4b6-153">tootest it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="df4b6-154">hello *hivesampletable*這個查詢中都是在預先安裝在所有 Azure HDInsight Hadoop 叢集上預設時 hello 叢集佈建。</span><span class="sxs-lookup"><span data-stu-id="df4b6-154">hello *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when hello clusters are provisioned.</span></span>

### <span data-ttu-id="df4b6-155"><a name="hive-textfeatures"></a>從文字欄位擷取功能</span><span class="sxs-lookup"><span data-stu-id="df4b6-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="df4b6-156">當 hello Hive 資料表具有包含的以空格分隔的文字字串的文字欄位時，hello 下列查詢會擷取 hello hello 字串和文字在 hello 字串中的 hello 數目的長度。</span><span class="sxs-lookup"><span data-stu-id="df4b6-156">When hello Hive table has a text field that contains a string of words that are delimited by spaces, hello following query extracts hello length of hello string, and hello number of words in hello string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="df4b6-157"><a name="hive-gpsdistance"></a>計算 GPS 座標組之間的距離</span><span class="sxs-lookup"><span data-stu-id="df4b6-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="df4b6-158">本節中的 hello 查詢可以是直接套用的 toohello NYC 計程車路線資料。</span><span class="sxs-lookup"><span data-stu-id="df4b6-158">hello query given in this section can be directly applied toohello NYC Taxi Trip Data.</span></span> <span data-ttu-id="df4b6-159">hello 用途，此查詢的方式是 tooshow tooapply 內嵌的 Hive toogenerate 功能中的數學函式。</span><span class="sxs-lookup"><span data-stu-id="df4b6-159">hello purpose of this query is tooshow how tooapply an embedded mathematical functions in Hive toogenerate features.</span></span>

<span data-ttu-id="df4b6-160">hello 這個查詢中使用的欄位會收取和 dropoff 位置，名為 hello GPS 座標*收取\_經度*，*收取\_緯度*， *dropoff\_經度*，和*dropoff\_緯度*。</span><span class="sxs-lookup"><span data-stu-id="df4b6-160">hello fields that are used in this query are hello GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="df4b6-161">計算 hello hello 收取和 dropoff 座標之間的直接距離的 hello 查詢是：</span><span class="sxs-lookup"><span data-stu-id="df4b6-161">hello queries that calculate hello direct distance between hello pickup and dropoff coordinates are:</span></span>

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

<span data-ttu-id="df4b6-162">計算兩個 GPS 座標之間的 hello 距離 hello 數學方程式可以找到上 hello<a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">可移動類型指令碼</a>Peter Lapisu 所撰寫的網站。</span><span class="sxs-lookup"><span data-stu-id="df4b6-162">hello mathematical equations that calculate hello distance between two GPS coordinates can be found on hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="df4b6-163">在 Javascript 中，hello 函式`toRad()`只是*lat_or_lon*pi/180 *，可將轉換度 tooradians。</span><span class="sxs-lookup"><span data-stu-id="df4b6-163">In his Javascript, hello function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees tooradians.</span></span> <span data-ttu-id="df4b6-164">在這裡， *lat_or_lon* hello 經度或緯度。</span><span class="sxs-lookup"><span data-stu-id="df4b6-164">Here, *lat_or_lon* is hello latitude or longitude.</span></span> <span data-ttu-id="df4b6-165">因為登錄區不提供 hello 函式`atan2`，但提供 hello 函式`atan`，hello`atan2`函式由實作`atan`函式中使用 hello 定義中所提供的 Hive 查詢上述 hello <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">維基百科</a>。</span><span class="sxs-lookup"><span data-stu-id="df4b6-165">Since Hive does not provide hello function `atan2`, but provides hello function `atan`, hello `atan2` function is implemented by `atan` function in hello above Hive query using hello definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![建立工作區](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="df4b6-167">內嵌的 Udf 可以在 hello 的登錄區的完整清單**內建函數**區段 hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>)。</span><span class="sxs-lookup"><span data-stu-id="df4b6-167">A full list of Hive embedded UDFs can be found in hello **Built-in Functions** section on hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="df4b6-168"><a name="tuning"></a>進階主題： 微調 Hive 參數 tooImprove 查詢速度</span><span class="sxs-lookup"><span data-stu-id="df4b6-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters tooImprove Query Speed</span></span>
<span data-ttu-id="df4b6-169">hello Hive 叢集設定可能不適合 hello Hive 查詢和處理 hello 查詢 hello 資料的預設參數。</span><span class="sxs-lookup"><span data-stu-id="df4b6-169">hello default parameter settings of Hive cluster might not be suitable for hello Hive queries and hello data that hello queries are processing.</span></span> <span data-ttu-id="df4b6-170">在本節中，我們會討論一些參數，可讓使用者可以調整改善 hello 的 Hive 查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="df4b6-170">In this section, we discuss some parameters that users can tune that improve hello performance of Hive queries.</span></span> <span data-ttu-id="df4b6-171">使用者需要 tooadd hello 參數微調之前 hello 查詢的處理資料的查詢。</span><span class="sxs-lookup"><span data-stu-id="df4b6-171">Users need tooadd hello parameter tuning queries before hello queries of processing data.</span></span>

1. <span data-ttu-id="df4b6-172">**Java 堆積空間**： 查詢包含聯結大型資料集，或處理長的記錄，**堆積空間用盡**是其中一個 hello 常見的錯誤。</span><span class="sxs-lookup"><span data-stu-id="df4b6-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of hello common error.</span></span> <span data-ttu-id="df4b6-173">這可以藉由設定參數微調*mapreduce.map.java.opts*和*mapreduce.task.io.sort.mb* toodesired 值。</span><span class="sxs-lookup"><span data-stu-id="df4b6-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* toodesired values.</span></span> <span data-ttu-id="df4b6-174">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="df4b6-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="df4b6-175">配置 4 GB 記憶體 tooJava 堆積空間，也可讓排序更有效率地配置更多的記憶體，這個參數。</span><span class="sxs-lookup"><span data-stu-id="df4b6-175">This parameter allocates 4GB memory tooJava heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="df4b6-176">如果有任何作業失敗錯誤的相關的 tooheap 空間，它是個不錯的主意 tooplay 與這些配置。</span><span class="sxs-lookup"><span data-stu-id="df4b6-176">It is a good idea tooplay with these allocations if there are any job failure errors related tooheap space.</span></span>

1. <span data-ttu-id="df4b6-177">**DFS 區塊大小**： 這個參數會設定 hello 最小單位 hello 檔案系統存放區的資料。</span><span class="sxs-lookup"><span data-stu-id="df4b6-177">**DFS block size** : This parameter sets hello smallest unit of data that hello file system stores.</span></span> <span data-ttu-id="df4b6-178">為例，如果 hello DFS 區塊大小為 128 MB，然後大小的任何資料小於和向上 too128MB 儲存在單一區塊中，大於 128 MB 所配置額外的區塊的資料時。</span><span class="sxs-lookup"><span data-stu-id="df4b6-178">As an example, if hello DFS block size is 128MB, then any data of size less than and up too128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="df4b6-179">選擇非常小的區塊的大小上限會導致大型負擔 Hadoop 因為 hello 名稱節點有 tooprocess 許多更多要求 toofind hello 相關區塊相關 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="df4b6-179">Choosing a very small block size causes large overheads in Hadoop since hello name node has tooprocess many more requests toofind hello relevant block pertaining toohello file.</span></span> <span data-ttu-id="df4b6-180">在處理 GB (或更大型) 資料時，建議的設定如下：</span><span class="sxs-lookup"><span data-stu-id="df4b6-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="df4b6-181">**最佳化登錄區中的聯結作業**: hello 對應/減少 framework 中的聯結作業通常發生在 hello 減少階段中，有時候，龐大提升可藉由排程聯結在 hello 對應階段中 （也稱為 「 mapjoins"）。</span><span class="sxs-lookup"><span data-stu-id="df4b6-181">**Optimizing join operation in Hive** : While join operations in hello map/reduce framework typically take place in hello reduce phase, sometimes, enormous gains can be achieved by scheduling joins in hello map phase (also called "mapjoins").</span></span> <span data-ttu-id="df4b6-182">toodirect Hive toodo 這可能的話，我們可以設定：</span><span class="sxs-lookup"><span data-stu-id="df4b6-182">toodirect Hive toodo this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="df4b6-183">**指定 hello 數目自行 tooHive** ： 時 Hadoop 允許 hello 使用者 tooset hello 次數 reducers，對應工具中的 hello 數目通常是由 hello 使用者設定。</span><span class="sxs-lookup"><span data-stu-id="df4b6-183">**Specifying hello number of mappers tooHive** : While Hadoop allows hello user tooset hello number of reducers, hello number of mappers is typically not be set by hello user.</span></span> <span data-ttu-id="df4b6-184">可讓某種程度的控制這個數字的那一墩是 toochoose hello Hadoop 變數， *mapred.min.split.size*和*mapred.max.split.size*與 hello 大小，每個對應的工作取決於：</span><span class="sxs-lookup"><span data-stu-id="df4b6-184">A trick that allows some degree of control on this number is toochoose hello Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as hello size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="df4b6-185">一般而言，hello 預設值是*mapred.min.split.size*為 0，屬於*mapred.max.split.size*是**Long.MAX**與*dfs.block.size*是 64 MB。</span><span class="sxs-lookup"><span data-stu-id="df4b6-185">Typically, hello default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="df4b6-186">我們可以看到，給定的 hello 資料大小，調整這些參數的 「 設定 」 它們可讓我們 tootune hello 數目對應工具中使用。</span><span class="sxs-lookup"><span data-stu-id="df4b6-186">As we can see, given hello data size, tuning these parameters by "setting" them allows us tootune hello number of mappers used.</span></span>
4. <span data-ttu-id="df4b6-187">以下將提及最佳化 Hive 效能的其他數個更 **進階選項** 。</span><span class="sxs-lookup"><span data-stu-id="df4b6-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="df4b6-188">這些 tooset hello 配置記憶體 toomap 可讓您和減少工作，並可用於微調效能。</span><span class="sxs-lookup"><span data-stu-id="df4b6-188">These allow you tooset hello memory allocated toomap and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="df4b6-189">請記住該 hello *mapreduce.reduce.memory.mb*不能大於 hello 的 hello Hadoop 叢集中的每個背景工作節點的實體記憶體大小。</span><span class="sxs-lookup"><span data-stu-id="df4b6-189">Please keep in mind that hello *mapreduce.reduce.memory.mb* cannot be greater than hello physical memory size of each worker node in hello Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

