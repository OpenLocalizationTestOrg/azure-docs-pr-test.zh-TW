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
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>針對使用 Hive 查詢之 Hadoop 叢集中的資料建立特性
本文件示範 toocreate 功能資料儲存在 Azure HDInsight Hadoop 叢集中使用 Hive 查詢的方式。 這些 Hive 查詢使用內嵌 hive 控制檔的使用者定義函數 (Udf)，提供其 hello 指令碼。

hello 作業所需 toocreate 功能可以是需要大量的記憶體。 hello 的 Hive 查詢的效能變得十分重要，在此情況下，來調整特定參數便可改善。 hello 微調這些參數的 hello 最後一節中討論。

顯示 hello 查詢的範例包括特定 toohello [NYC 計程車路線資料](http://chriswhong.com/open-data/foil_nyc_taxi/)案例也會提供在[GitHub 儲存機制](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)。 這些查詢已經有指定的資料結構描述，而且準備好 toobe 提交 toorun。 在 hello 最後一節中也會討論參數，可讓使用者可以調整，以便可以改善 hello 的 Hive 查詢的效能。

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

這**功能表**連結 tootopics 描述 toocreate 各種環境中的資料的功能。 這項工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。

## <a name="prerequisites"></a>必要條件
本文假設您已經：

* 建立 Azure 儲存體帳戶。 如需指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* 自訂的 Hadoop 叢集以 hello HDInsight 服務使用者佈建。  如需指示，請參閱 [自訂適用於進階分析的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)。
* hello 資料已上傳的 tooHive Azure HDInsight Hadoop 叢集中的資料表。 如果沒有，請依照[建立和載入資料 tooHive 資料表](machine-learning-data-science-move-hive-tables.md)tooupload 資料 tooHive 資料表第一次。
* 啟用遠端存取 toohello 叢集。 如果您需要的指示，請參閱[存取 hello 的 Hadoop 叢集前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)。

## <a name="hive-featureengineering"></a>功能產生
在本節中描述的 hello 方法中的功能可以會產生使用 Hive 查詢的數個範例。 一旦您已經產生額外的功能，您可以將活動當做資料行 toohello 現有的資料表加入或建立新的資料表與 hello 額外的功能和主索引鍵，然後可以與 hello 原始資料表聯結。 以下是顯示 hello 範例：

1. [以頻率為基礎的功能產生](#hive-frequencyfeature)
2. [二進位分類中類別變數的風險](#hive-riskfeature)
3. [從日期時間欄位擷取功能](#hive-datefeatures)
4. [從文字欄位擷取功能](#hive-textfeatures)
5. [計算 GPS 座標間的距離](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>以頻率為基礎的功能產生
通常會很有用的 toocalculate hello 頻率的 hello 層級的類別變數或從多個類別變數的層級的特定組合 hello 頻率。 使用者可以使用下列指令碼 toocalculate hello 這些頻率：

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>二進位分類中類別變數的風險
在二進位分類中，我們需要類別變數則 tooconvert 非數值成數值特徵時只使用 hello 模型需要數值特徵。 您可以使用數值風險來取代每個非數值層級，藉以完成這個動作。 在本節中，我們會示範計算的類別變數的 hello 風險值 （對數勝算的特徵） 某些泛型 Hive 查詢。

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

在此範例中，變數`smooth_param1`和`smooth_param2`設定 toosmooth hello 風險值計算從 hello 資料。 風險範圍介於-Inf 和 Inf 之間。 風險 > 0 表示該 hello 目標是相等的 too1 hello 機率大於 0.5。

計算 hello 風險資料表之後，使用者可以指派風險值 tooa 資料表聯結與 hello 風險資料表。 上一節中提供 hello Hive 聯結查詢。

### <a name="hive-datefeatures"></a>從日期時間欄位擷取功能
Hive 會和一組 UDF 一起出現，用來處理日期時間欄位。 在 Hive hello 預設日期時間格式是 'yyyy MM dd 00:00:00' (' 1970年-01-01 12:21:32 ' 例如)。 在本節中，我們會示範擷取 hello 月份、 日期時間欄位中，從 hello 月份天數的範例和以外 hello 預設格式 tooa datetime 字串的預設格式轉換的日期時間格式字串的其他範例。

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

此登錄區查詢假設該 hello *&#60; 日期時間欄位 >* hello 預設日期時間格式。

如果 datetime 欄位不是 hello 預設格式，您需要 tooconvert hello datetime 欄位 Unix 時間戳記至第一次，而且轉換 hello 的 Unix 時間戳記 tooa datetime 的字串，則是位在 hello 預設格式。 當 hello datetime 的預設格式，使用者可以套用 hello 內嵌 datetime Udf tooextract 功能。

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

在此查詢中，如果 hello *（& s) #60; 日期時間欄位 >*具有類似的 hello 模式*03/26/2015年 12:04:39*，hello *' （& s) #60; hello 日期時間欄位的模式 >'*應該是`'MM/dd/yyyy HH:mm:ss'`. tootest 使用者可以執行它，

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

hello *hivesampletable*這個查詢中都是在預先安裝在所有 Azure HDInsight Hadoop 叢集上預設時 hello 叢集佈建。

### <a name="hive-textfeatures"></a>從文字欄位擷取功能
當 hello Hive 資料表具有包含的以空格分隔的文字字串的文字欄位時，hello 下列查詢會擷取 hello hello 字串和文字在 hello 字串中的 hello 數目的長度。

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>計算 GPS 座標組之間的距離
本節中的 hello 查詢可以是直接套用的 toohello NYC 計程車路線資料。 hello 用途，此查詢的方式是 tooshow tooapply 內嵌的 Hive toogenerate 功能中的數學函式。

hello 這個查詢中使用的欄位會收取和 dropoff 位置，名為 hello GPS 座標*收取\_經度*，*收取\_緯度*， *dropoff\_經度*，和*dropoff\_緯度*。 計算 hello hello 收取和 dropoff 座標之間的直接距離的 hello 查詢是：

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

計算兩個 GPS 座標之間的 hello 距離 hello 數學方程式可以找到上 hello<a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">可移動類型指令碼</a>Peter Lapisu 所撰寫的網站。 在 Javascript 中，hello 函式`toRad()`只是*lat_or_lon*pi/180 *，可將轉換度 tooradians。 在這裡， *lat_or_lon* hello 經度或緯度。 因為登錄區不提供 hello 函式`atan2`，但提供 hello 函式`atan`，hello`atan2`函式由實作`atan`函式中使用 hello 定義中所提供的 Hive 查詢上述 hello <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">維基百科</a>。

![建立工作區](./media/machine-learning-data-science-create-features-hive/atan2new.png)

內嵌的 Udf 可以在 hello 的登錄區的完整清單**內建函數**區段 hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>)。  

## <a name="tuning"></a>進階主題： 微調 Hive 參數 tooImprove 查詢速度
hello Hive 叢集設定可能不適合 hello Hive 查詢和處理 hello 查詢 hello 資料的預設參數。 在本節中，我們會討論一些參數，可讓使用者可以調整改善 hello 的 Hive 查詢的效能。 使用者需要 tooadd hello 參數微調之前 hello 查詢的處理資料的查詢。

1. **Java 堆積空間**： 查詢包含聯結大型資料集，或處理長的記錄，**堆積空間用盡**是其中一個 hello 常見的錯誤。 這可以藉由設定參數微調*mapreduce.map.java.opts*和*mapreduce.task.io.sort.mb* toodesired 值。 下列是一個範例：
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    配置 4 GB 記憶體 tooJava 堆積空間，也可讓排序更有效率地配置更多的記憶體，這個參數。 如果有任何作業失敗錯誤的相關的 tooheap 空間，它是個不錯的主意 tooplay 與這些配置。

1. **DFS 區塊大小**： 這個參數會設定 hello 最小單位 hello 檔案系統存放區的資料。 為例，如果 hello DFS 區塊大小為 128 MB，然後大小的任何資料小於和向上 too128MB 儲存在單一區塊中，大於 128 MB 所配置額外的區塊的資料時。 選擇非常小的區塊的大小上限會導致大型負擔 Hadoop 因為 hello 名稱節點有 tooprocess 許多更多要求 toofind hello 相關區塊相關 toohello 檔案。 在處理 GB (或更大型) 資料時，建議的設定如下：
   
        set dfs.block.size=128m;
2. **最佳化登錄區中的聯結作業**: hello 對應/減少 framework 中的聯結作業通常發生在 hello 減少階段中，有時候，龐大提升可藉由排程聯結在 hello 對應階段中 （也稱為 「 mapjoins"）。 toodirect Hive toodo 這可能的話，我們可以設定：
   
        set hive.auto.convert.join=true;
3. **指定 hello 數目自行 tooHive** ： 時 Hadoop 允許 hello 使用者 tooset hello 次數 reducers，對應工具中的 hello 數目通常是由 hello 使用者設定。 可讓某種程度的控制這個數字的那一墩是 toochoose hello Hadoop 變數， *mapred.min.split.size*和*mapred.max.split.size*與 hello 大小，每個對應的工作取決於：
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    一般而言，hello 預設值是*mapred.min.split.size*為 0，屬於*mapred.max.split.size*是**Long.MAX**與*dfs.block.size*是 64 MB。 我們可以看到，給定的 hello 資料大小，調整這些參數的 「 設定 」 它們可讓我們 tootune hello 數目對應工具中使用。
4. 以下將提及最佳化 Hive 效能的其他數個更 **進階選項** 。 這些 tooset hello 配置記憶體 toomap 可讓您和減少工作，並可用於微調效能。 請記住該 hello *mapreduce.reduce.memory.mb*不能大於 hello 的 hello Hadoop 叢集中的每個背景工作節點的實體記憶體大小。
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

