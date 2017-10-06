---
title: "aaaExplore 資料在 Hadoop 叢集，並在 Azure Machine Learning 中建立模型 |Microsoft 文件"
description: "使用 hello 小組資料科學程序的端對端案例，採用 HDInsight Hadoop 叢集 toobuild，並部署模型，使用公開可用的資料集。"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a>在動作中的 hello 小組資料科學程序： 使用 Azure HDInsight Hadoop 叢集
在本逐步解說中，我們使用 hello[小組資料科學程序 (TDSP)](data-science-process-overview.md)端對端實例使用[Azure HDInsight Hadoop 叢集](https://azure.microsoft.com/services/hdinsight/)toostore，探索和公開功能從 hello 的工程資料可用[NYC 計程車往返](http://www.andresmh.com/nyctaxitrips/)資料集和 toodown 範例 hello 資料。 使用 Azure Machine Learning toohandle 二進位和多級分類和迴歸的預測工作所建置的 hello 資料模型。

如需示範如何 toohandle 較大的 (1 tb) 資料集的類似的狀況使用 HDInsight Hadoop 叢集以提供資料處理的逐步解說，請參閱[小組資料科學流程1TB資料集上使用AzureHDInsightHadoop叢集](machine-learning-data-science-process-hive-criteo-walkthrough.md).

它也是可能 toouse IPython 筆記型電腦 tooaccomplish hello 工作呈現的 hello 逐步解說使用 hello 1 TB 的資料集。 使用者會像這種方法，應洽詢的 tootry hello [Criteo 逐步解說使用 hive 控制檔的 ODBC 連接](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb)主題。

## <a name="dataset"></a>NYC 計程車車程資料集說明
hello NYC 計程車路線資料約 20 GB 的壓縮以逗號分隔值 (CSV) 檔案 (~ 48 GB 未壓縮)，可包含多個 173 百萬個個別的往返和 hello fares 支付每往返作業。 每個往返記錄包括 hello 收取和下車位置和時間、 匿名的 hack (driver) 授權編號和 medallion (計程車的唯一 id) 數目。 hello 資料涵蓋所有往返 hello 年份 2013年中，並提供下列兩個資料集的每個月的 hello:

1. hello 'trip_data' CSV 檔案包含路線詳細資料，例如乘客、 收取和 dropoff 點數目、 路線持續時間，以及路線長度。 以下是一些範例記錄：
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. hello 'trip_fare' CSV 檔案包含 hello 價位支付每個路線，例如付款類型、 價位量、 產生額外負荷及稅金、 秘訣和 tolls，以及 hello 總容量付費的詳細資料。 以下是一些範例記錄：
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

hello 唯一索引鍵 toojoin 路線\_資料和路線\_價位組成 hello 欄位： medallion 具 「 可回復\_授權與收取\_日期時間。

tooget 所有 hello 詳細資料相關的 tooa 特定路線，它是具有三個索引鍵的足夠 toojoin: hello"medallion"，"hack\_授權 」 和 「 收取\_datetime"。

當我們將它們儲存成 Hive 資料表稍後我們將描述 hello 資料的其他一些詳細資料。

## <a name="mltasks"></a>預測工作的範例
當處理資料時，判斷 hello 種類的預測，您想要根據其分析的 toomake 有助於釐清您的程序中，您將需要 tooinclude hello 工作。
以下是三個預測的問題，我們解決其編寫根據 hello 這個逐步解說中的範例*提示\_量*:

1. **二元分類**：預測是否已支付某趟車程的小費，例如大於美金 $0 元的 tip\_amount 為正面範例，而等於美金 $0 元的 tip\_amount 為負面範例。
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. **多級分類**: hello 路線支付 toopredict hello 範圍的提示數量。 我們將 hello*提示\_量*到五個紙匣或類別：
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **迴歸工作**: hello 提示 toopredict hello 數量支付路線。  

## <a name="setup"></a>設定進階分析的 HDInsight Hadoop 叢集
> [!NOTE]
> 這通常是 **管理** 工作。
> 
> 

您可以採取三個步驟，為利用 HDInsight 叢集的進階分析設定 Azure 環境：

1. [建立儲存體帳戶](../storage/common/storage-create-storage-account.md)：這個儲存體帳戶是用來將資料儲存在 Azure Blob 儲存體中。 用於 HDInsight 叢集的 hello 資料也位於此處。
2. [自訂 Azure HDInsight Hadoop 叢集以提供 hello 進階分析程序和技術](machine-learning-data-science-customize-hadoop-cluster.md)。 這個步驟會建立已在所有節點上安裝 64 位元 Anaconda Python 2.7 的 Azure HDInsight Hadoop 叢集。 有兩個重要步驟 tooremember 時自訂您的 HDInsight 叢集。
   
   * 請記住 toolink hello 儲存體帳戶建立它時，與您的 HDInsight 叢集的步驟 1 中建立。 這個儲存體帳戶是使用的 tooaccess 處理 hello 叢集內的資料。
   * 建立 hello 叢集之後，啟用 遠端存取 toohello 叢集前端節點 hello。 瀏覽 toohello**組態**索引標籤上，按一下 **啟用遠端**。 此步驟中指定遠端登入所用的 hello 使用者認證。
3. [建立 Azure 機器學習工作區](machine-learning-create-workspace.md)： 此 Azure 機器學習工作區是使用的 toobuild 機器學習模型。 這項工作已獲得解決，完成初始資料探索之後，並向使用 hello HDInsight 叢集的取樣。

## <a name="getdata"></a>從公用的來源取得 hello 資料
> [!NOTE]
> 這通常是 **管理** 工作。
> 
> 

tooget hello [NYC 計程車往返](http://www.andresmh.com/nyctaxitrips/)從公用位置的資料集，您可以使用任何 hello 方法中所述[從 Azure Blob 儲存體移動資料 tooand](machine-learning-data-science-move-azure-blob.md) toocopy hello 資料 tooyour 機器。

這裡我們將描述如何使用 AzCopy tootransfer hello 檔案包含的資料。 toodownload 並安裝 AzCopy 遵循 hello 指示[開始使用 AzCopy 命令列公用程式的 hello](../storage/common/storage-use-azcopy.md)。

1. 命令提示字元 視窗中，發出下列的 AzCopy 命令、 取代 hello *< path_to_data_folder >*與 hello 所需的目的地：

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. Hello 複製完成時，總共 24 zip 檔案會位於 hello 資料資料夾中選擇。 解壓縮下載的 hello 檔案 toohello 本機電腦上相同的目錄。 記下 hello hello 未壓縮檔案所在的資料夾。 這個資料夾將會參考的 tooas hello *< 路徑\_至\_unzipped_data\_檔案\>*是後面。

## <a name="upload"></a>上傳 Azure HDInsight Hadoop 叢集中的 hello 資料 toohello 預設容器
> [!NOTE]
> 這通常是 **管理** 工作。
> 
> 

在 hello 下列的 AzCopy 命令，會取代 hello 遵循 hello 實際值來建立 hello Hadoop 叢集時，您所指定的參數，並解壓縮 hello 資料檔案。

* ***&#60; path_to_data_folder >*** hello 目錄 （以及路徑） 包含 hello 解壓縮資料檔案在電腦上  
* ***&#60; Hadoop 叢集的儲存體帳戶名稱 >*** hello 與您的 HDInsight 叢集相關聯的儲存體帳戶
* ***&#60; Hadoop 叢集的預設容器 >*** hello 叢集所使用的預設容器。 請注意該 hello 名稱的 hello 預設容器通常是相同的名稱，為 hello 叢集本身的 hello。 例如，如果 hello 叢集中稱為 「 abc123.azurehdinsight.net"，hello 預設容器。 abc123
* ***&#60; 儲存體帳戶金鑰 >*** hello 叢集所使用的 hello 儲存體帳戶金鑰

從命令提示字元或在您的電腦中的 Windows PowerShell 視窗中，執行下列兩個的 AzCopy 命令 hello。

此命令會將上傳 hello 路線資料太***nyctaxitripraw***目錄中的 hello Hadoop 叢集的 hello 預設容器。

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

此命令會將上傳 hello 價位資料太***nyctaxifareraw***目錄中的 hello Hadoop 叢集的 hello 預設容器。

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

hello 資料現在應該在 Azure Blob 儲存體和準備 toobe 耗用 hello HDInsight 叢集。

## <a name="#download-hql-files"></a>登入 hello Hadoop 叢集前端節點，並準備資料探勘分析
> [!NOTE]
> 這通常是 **管理** 工作。
> 
> 

tooaccess hello 叢集前端節點 hello 探勘測試的資料分析的時間和停機的 hello 資料取樣，請遵循 「 hello 程序中所述[存取 hello 的 Hadoop 叢集前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)。

在本逐步解說中，我們主要是使用撰寫的查詢[Hive](https://hive.apache.org/)，類似 SQL 的查詢語言、 tooperform 初步資料瀏覽。 hello Hive 查詢會儲存在.hql 檔案。 我們再向下範例此 Azure Machine Learning 中用來建立模型的資料 toobe。

資料探勘分析 tooprepare hello 叢集，我們下載 hello.hql 檔案，其中包含 hello 相關的 Hive 指令碼從[github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa 本機目錄 (C:\temp)，hello 前端節點上的。 toodo，開啟 hello**命令提示字元**從 hello 前端節點的 hello 叢集和問題 hello 下列兩個命令：

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

這兩個命令會下載需要此逐步解說 toohello 本機目錄中的所有.hql 檔案***C:\temp &#92;*** hello 前端節點中。

## <a name="#hive-db-tables"></a>建立依月份分割的 Hive 資料庫和資料表
> [!NOTE]
> 這通常是 **管理** 工作。
> 
> 

我們已經準備好 toocreate Hive 資料表我們 NYC 計程車資料集。
在 hello hello Hadoop 叢集的前端節點，開啟 hello ***Hadoop 命令列***hello 桌面的 hello 前端節點，且輸入 hello 命令輸入 hello Hive 目錄

    cd %hive_home%\bin

> [!NOTE]
> **在此逐步解說中執行所有的登錄區命令，從上述 Hive bin hello / 目錄提示字元。如此可自動處理路徑相關問題。我們使用 hello 詞彙"Hive 目錄 prompt"，"Hive bin / 目錄提示字元 」，和交換在本逐步解說中的 「 Hadoop 命令列 」。**
> 
> 

Hello Hive 目錄提示字元中，輸入下列命令在 hello 前端節點 toosubmit hello Hive 查詢 toocreate Hive 資料庫和資料表的 Hadoop 命令列的 hello:

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

以下是 hello hello 內容***C:\temp\sample\_hive\_建立\_db\_和\_tables.hql***檔案會建立登錄區資料庫***nyctaxidb***和資料表***路線***和***價位***。

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

這個 Hive 指令碼會建立兩個資料表：

* hello 「 往返 」 資料表包含 （驅動程式詳細資料、 收取的時間、 旅行距離和時間） 的每個賽車路線詳細資料
* hello"價位 」 資料表包含價位詳細資料 （價位量、 提示量、 tolls 和 surcharges）。

如果您需要這些程序的任何其他協助，或想 tooinvestigate 替代項目，請參閱 hello 節[提交 Hive 查詢直接從 hello Hadoop 命令列](machine-learning-data-science-move-hive-tables.md#submit)。

## <a name="#load-data"></a>載入資料 tooHive 資料表資料分割
> [!NOTE]
> 這通常是 **管理** 工作。
> 
> 

hello NYC 計程車資料集有自然的資料分割以月，我們使用 tooenable 處理和查詢的速度。 hello 下列 PowerShell 命令 (從 hello Hive 目錄使用 hello 發出**Hadoop 命令列**) 載入 toohello"路線 」 及 「 價位"Hive 資料表，根據月份分割。

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

hello*範例\_hive\_載入\_資料\_由\_partitions.hql*檔案包含下列 hello**載入**命令。

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

請注意一些我們在此使用 hello 瀏覽處理序中的 Hive 查詢包含查詢只是單一分割，或者只使用幾個資料分割。 但是，這些查詢可以執行跨 hello 整個資料。

### <a name="#show-db"></a>顯示資料庫中 hello HDInsight Hadoop 叢集
所建立的 HDInsight Hadoop 叢集內 hello Hadoop 命令列視窗中，執行下列命令 Hadoop 命令列中的 hello tooshow hello 資料庫：

    hive -e "show databases;"

### <a name="#show-tables"></a>顯示 hello nyctaxidb 資料庫中的 hello Hive 資料表
在 hello nyctaxidb 資料庫，請執行下列命令 Hadoop 命令列中的 hello tooshow hello 資料表：

    hive -e "show tables in nyctaxidb;"

我們可以確認 hello 資料表已分割藉由發出下列 hello 命令：

    hive -e "show partitions nyctaxidb.trip;"

hello 預期輸出如下所示：

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

同樣地，我們可以確定該 hello 價位表分割藉由發出下列 hello 命令：

    hive -e "show partitions nyctaxidb.fare;"

hello 預期輸出如下所示：

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a>Hive 中的資料探索和特徵工程
> [!NOTE]
> 這通常是 **資料科學家** 工作。
> 
> 

hello 資料瀏覽和功能的資料載入至 hello Hive 資料表可以使用 Hive 查詢來達成的 hello 工程工作。 以下是我們將在本節中逐步引導您執行的這類工作範例：

* 檢視兩個資料表中的 hello 前 10 筆記錄。
* 在變動的時間範圍中探索數個欄位的資料分佈。
* 調查 hello 經度和緯度欄位的資料品質。
* 產生二進位和多級分類標籤根據 hello**提示\_量**。
* 產生功能，藉由計算 hello 直接的旅行距離。

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a>瀏覽： 檢視資料表旅程中的 hello 前 10 筆記錄
> [!NOTE]
> 這通常是 **資料科學家** 工作。
> 
> 

hello 資料看起來像 toosee，我們會檢查每個資料表中的 10 筆記錄。 執行 hello hello Hadoop 命令列主控台 tooinspect hello 記錄中的 hello Hive 目錄提示字元中的個別下列兩個查詢。

tooget hello 前 10 筆記錄 hello 資料表 」 行程"hello 第一個月中：

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

tooget hello 前 10 個資料表中的記錄 hello"再見"hello 從第一個月：

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

它通常是很有用的 toosave hello 記錄 tooa 檔方便檢視。 上述查詢小幅變更 toohello 完成這項操作：

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a>瀏覽： 檢視每個 hello 12 個資料分割中的 hello 記錄數目
> [!NOTE]
> 這通常是 **資料科學家** 工作。
> 
> 

感興趣的是如何 hello 的往返次數變化期間 hello 日曆年度的 hello。 依月份群組可讓我們 toosee 的行程此分佈是什麼樣子。

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

這會提供 hello 輸出：

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

在這裡，hello 第一個資料行是 hello 的月份，而 hello 該月份的第二種是 hello 的往返次數。

我們也可以藉由發出下列命令，在提示字元中 Hive 目錄 hello hello 我們路線資料集中計數 hello 的總記錄數。

    hive -e "select count(*) from nyctaxidb.trip;"

這會產生：

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

使用命令類似 toothose 所示為 hello 路線的資料集，我們可以發出 Hive 查詢從 hello 價位資料集 toovalidate hello 的記錄數目的 hello Hive 目錄提示字元。

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

這會提供 hello 輸出：

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

請注意，hello 完全相同的往返次數每個月就會傳回兩個資料集。 這會提供 hello 第一個驗證該 hello 正確地載入資料。

計算 hello 的總記錄數 hello 價位資料集中，才可以使用下面的 hello Hive 目錄提示字元中的 hello 命令：

    hive -e "select count(*) from nyctaxidb.fare;"

這會產生：

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

也 hello hello 的總記錄數兩個資料表中相同。 這會提供第二個驗證該 hello 正確地載入資料。

### <a name="exploration-trip-distribution-by-medallion"></a>探索：依據 medallion 的車程分佈
> [!NOTE]
> 這通常是 **資料科學家** 工作。
> 
> 

這個範例會在給定的時間間隔內識別超過 100 個往返 hello medallion （計程車數字）。 從 hello hello 查詢優點分割資料表存取，因為它由 hello 分割變數所**月份**。 hello 查詢結果會以撰寫 tooa 本機檔案 queryoutput.tsv `C:\temp` hello 前端節點上。

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

以下是 hello 內容*範例\_hive\_路線\_計數\_由\_medallion.hql*進行檢查的檔案。

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

hello medallion hello NYC 計程車資料集內識別的唯一封包。 我們可以詢問哪些計程車在特定時段超過特定的車程數目，以識別哪些計程車「忙碌中」。 hello 下列範例會識別在 hello 中前三個月，進行超過一百往返的封包，並儲存 hello 查詢結果 tooa 本機檔案，C:\temp\queryoutput.tsv。

以下是 hello 內容*範例\_hive\_路線\_計數\_由\_medallion.hql*進行檢查的檔案。

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

從 hello hive 控制檔目錄提示字元中，下列的問題 hello 命令：

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>探索：依據 medallion 和 hack_license 的車程分佈
> [!NOTE]
> 這通常是 **資料科學家** 工作。
> 
> 

當瀏覽資料集，我們經常想 tooexamine hello 次數 co-群組的值。 本章節將提供範例，此作業對於擷取 toodo 如何與驅動程式。

hello*範例\_hive\_路線\_計數\_由\_medallion\_license.hql* "medallion"和"hack_license"上設定的 hello 價位資料的檔案群組與每個組合的傳回計數。 以下是其內容。

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

這個查詢會依車程數目的遞減順序，傳回計程車和特定駕駛的組合。

從 hello hive 控制檔目錄提示字元，請執行：

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

hello 查詢結果會寫入 C:\temp\queryoutput.tsv tooa 本機檔案。

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a>探索：藉由檢查無效的經度/緯度記錄來評估資料品質
> [!NOTE]
> 這通常是 **資料科學家** 工作。
> 
> 

資料探勘分析的常見目標是 tooweed 出無效或不正確的記錄。 hello 本節中的範例會決定是否可以是 hello 經度或緯度的欄位包含遠超出 hello NYC 區域的值。 因為這是可能這類記錄都有錯誤的經度-緯度值，我們想要從 toobe 任何資料模型所用的 tooeliminate。

以下是 hello 內容*範例\_hive\_品質\_assessment.hql*進行檢查的檔案。

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


從 hello hive 控制檔目錄提示字元，請執行：

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

hello *-S*包含在此命令的引數會抑制 hello 狀態螢幕列印成品的 hello Hive Map/Reduce 作業。 這非常有用，因為它會讓 hello 螢幕列印 hello 的 Hive 查詢的輸出更容易閱讀。

### <a name="exploration-binary-class-distributions-of-trip-tips"></a>探索：車程小費的二元類別分佈
> [!NOTE]
> 這通常是 **資料科學家** 工作。
> 
> 

Hello 中所述的 hello 二元分類問題[預測工作的範例](machine-learning-data-science-process-hive-walkthrough.md#mltasks) 區段中，很有用的 tooknow 是否或不指定提示。 小費是二元分佈：

* tip given(Class 1, tip\_amount > $0)  
* no tip (Class 0, tip\_amount = $0)

hello*範例\_hive\_傾斜\_frequencies.hql*檔案如下所示的做法。

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

從 hello hive 控制檔目錄提示字元，請執行：

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a>瀏覽： Hello 多級設定中的類別分佈
> [!NOTE]
> 這通常是 **資料科學家** 工作。
> 
> 

Hello 中所述的 hello 多級分類問題[預測工作的範例](machine-learning-data-science-process-hive-walkthrough.md#mltasks)此資料集也借用本身 tooa 自然的分類，其中，我們都希望 toopredict hello 數量指定 hello 提示 > 一節。 我們可以使用分類收納 toodefine 提示範圍 hello 查詢中。 tooget hello hello 類別分配不同提示的範圍，我們使用 hello*範例\_hive\_提示\_範圍\_frequencies.hql*檔案。 以下是其內容。

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

執行下列命令從 Hadoop 命令列主控台 hello:

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a>探索：計算兩個經度-緯度位置之間的直線距離
> [!NOTE]
> 這通常是 **資料科學家** 工作。
> 
> 

擁有 hello 直接距離的量值可讓我們 toofind hello 不一致，它與 hello 之間出實際成為距離。 我們藉由指出，旅客可能會小於激勵這項功能可能工具提示 」 如果它們找出該 hello 驅動程式具有刻意它們所採取的較長的路由。

實際的旅行距離與 hello toosee hello 比較[Haversine 距離](http://en.wikipedia.org/wiki/Haversine_formula)經度-緯度兩點之間 （hello"優越 circle"距離），我們使用可用的 hello 三角函式內登錄區，因此：

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

在上述查詢 hello，R 是 hello 半徑 hello 地球英里，而 pi 是轉換的 tooradians。 請注意，hello 經度-緯度點為遠離 hello NYC 區域的 篩選 」 tooremove 值。

在此情況下，我們會撰寫我們稱為 「 queryoutputdir"的結果 tooa 目錄。 hello 順序如下所示的命令的輸出目錄中，會先建立，並執行 hello Hive 命令。

從 hello hive 控制檔目錄提示字元，請執行：

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


hello 查詢結果會寫入 too9 Azure blob ***queryoutputdir/000000\_0***太***queryoutputdir/000008\_0*** hello hello Hadoop 叢集的預設容器下。

toosee hello 的 hello 個別 blob 的大小，我們要執行 hello hello Hive 目錄提示字元中的下列命令：

    hdfs dfs -ls wasb:///queryoutputdir

指定的檔案，toosee hello 內容說 000000\_0，我們使用 Hadoop 的`copyToLocal`命令，因此。

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> 遇到大型檔案，`copyToLocal` 可能會很慢，因此不建議使用。  
> 
> 

包含此資料位於 Azure blob 的主要優點是，我們可能會瀏覽使用 hello Azure Machine Learning 中的 hello 資料[匯入資料][ import-data]模組。

## <a name="#downsample"></a>在 Azure Machine Learning 中縮小取樣和建置模型
> [!NOTE]
> 這通常是 **資料科學家** 工作。
> 
> 

Hello 探勘測試的資料分析階段之後，我們現在是準備 toodown 範例 hello 資料來建立 Azure Machine Learning 中的模型。 在本節中，我們會示範如何 toouse Hive 查詢 toodown 範例 hello 資料，然後從 hello 存取[匯入資料][ import-data] Azure Machine Learning 中的模組。

### <a name="down-sampling-hello-data"></a>向下取樣 hello 資料
這個程序包含兩個步驟。 我們第一次加入 hello **nyctaxidb.trip**和**nyctaxidb.fare**上會出現在所有記錄中的三個索引鍵的資料表:"medallion"，"hack\_授權 」，和 「 收取\_datetime"。 接著產生二元分類標籤 **tipped** 和多元分類標籤 **tip\_class**。

取樣的資料，直接從 hello 向 toobe 無法 toouse hello[匯入資料][ import-data]模組在 Azure Machine Learning 中，就需要 toostore hello 結果的查詢 tooan 內部的 Hive 資料表上方的 hello。 在以下，我們會建立內部的 Hive 資料表，並聯結 hello 上下取樣的資料填入它的內容。

hello 查詢適用於標準 Hive 函式直接 toogenerate hello 當日小時、 一週的年、 週間日 （1 代表星期一和 7 代表星期日） 從 hello"收取\_日期時間 」 欄位，以及 hello 直接 hello 收取和距離 dropoff位置。 使用者可以參考太[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF)的這類函式的完整清單。

hello 查詢，然後向下範例 hello 資料，以便 hello 查詢結果可以納入 hello Azure Machine Learning Studio。 只有約 1%的 hello 原始資料集匯入 hello Studio。

下面是 hello 內容*範例\_hive\_準備\_如\_aml\_full.hql*建置 Azure Machine Learning 中的模型來準備資料的檔案。

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

此查詢中的，從 hello Hive 目錄提示 toorun:

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

我們現在有內部的資料表使用 hello 可存取的 「 nyctaxidb.nyctaxi_downsampled_dataset"[匯入資料][ import-data]從 Azure 機器學習模組。 此外，我們可能使用這個資料集來建置機器學習服務模型。  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a>Azure Machine Learning tooaccess hello 向取樣資料中使用 hello 資料匯入模組
為發行在 hello 的 Hive 查詢的必要條件[匯入資料][ import-data] Azure 機器學習模組中的，我們需要存取 tooan Azure Machine Learning 工作區，並存取 hello toohello 認證叢集和與其相關聯的儲存體帳戶。

部分詳細資料上 hello[匯入資料][ import-data]模組和 hello 參數 tooinput:

**HCatalog 伺服器 URI**： 如果 hello 叢集名稱 abc123，則這只是： https://abc123.azurehdinsight.net

**Hadoop 使用者帳戶名稱**: hello hello 叢集針對所選的使用者名稱 (**不**hello 遠端存取使用者名稱)

**Hadoop ser 帳戶密碼**: hello 叢集所選擇的 hello 密碼 (**不**hello 遠端存取密碼)

**輸出資料的位置**： 這選擇 toobe Azure。

**Azure 儲存體帳戶名稱**: hello 與 hello 叢集相關聯的預設儲存體帳戶名稱。

**Azure 容器名稱**： 這是 hello hello 叢集的預設容器名稱，通常是相同 hello 與 hello 叢集名稱。 如果叢集為 "abc123"，即為 abc123。

> [!IMPORTANT]
> **我們希望使用 hello tooquery 任何資料表[匯入資料][ import-data] Azure Machine Learning 中的模組必須是內部的資料表。** 以下是判斷資料庫 D.db 中的資料表 T 是否為內部資料表的秘訣。
> 
> 

從 hello hive 控制檔目錄提示字元中，問題 hello 命令：

    hdfs dfs -ls wasb:///D.db/T

如果 hello 資料表為內部的資料表，且它會擴展，其內容必須顯示在這裡。 另一個方式 toodetermine 資料表是否為內部的資料表為 toouse hello Azure 儲存體總管。 使用它的 hello 叢集 toonavigate toohello 預設容器名稱，然後篩選 hello 資料表名稱。 如果 hello 資料表和其內容顯示，這可確認它是內部的資料表。

以下是建立的快照 hello Hive 查詢並 hello[匯入資料][ import-data]模組：

![匯入資料模組的 Hive 查詢](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

請注意，因為我們 hello 預設容器中的取樣的資料所在的清單中，從 Azure Machine Learning hello 產生 Hive 查詢非常簡單只是 「 選取 * 從 nyctaxidb.nyctaxi\_downsampled\_資料 」。

hello 資料集現在做 hello 起點來建立機器學習模型。

### <a name="mlmodel"></a>在 Azure Machine Learning 中建置模型
我們現在是無法 tooproceed toomodel 建置和中的模型部署[Azure Machine Learning](https://studio.azureml.net)。 hello 資料已準備好我們 toouse 解決上述 hello 預測問題：

**1.二元分類**: toopredict 提示是否支付路線。

**已使用學習者：** 二元羅吉斯迴歸

a. 對於這個問題，我們的目標 (或類別) 標籤是 "tipped"。 縮小取樣的原始資料集有幾個資料行會顯示這個分類實驗目標。 特別是： 提示\_類別中，提示\_數量，與總\_金額不是可在測試時間的 hello 目標標籤的顯示資訊。 我們將不考慮使用 hello 移除這些資料行[資料集中選取的資料行][ select-columns]模組。

hello 快照下方會顯示我們實驗 toopredict 提示支付給定的路線。

![實驗快照](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

b.這是另一個 C# 主控台應用程式。 對於這項實驗，我們的目標標籤分佈大約是 1:1。

hello 快照下方顯示 hello 分佈 hello 二元分類問題的秘訣類別標籤。

![類別標籤的分佈](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

如此一來，我們取得 0.987 的 AUC hello 圖所示。

![AUC 值](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

**2.多級分類**: hello 來回傳送時，先前使用 hello 付費的提示數量 toopredict hello 範圍定義的類別。

**已使用學習者：** 多元羅吉斯迴歸

a. 對於這個問題，我們的目標 (或類別) 標籤是 "tip\_class"，可能採用五個值 (0、1、2、3、4) 的其中一個。 如同 hello 二元分類的情況，我們有此實驗目標流失的幾個資料行。 特別是： 傾斜，提示\_總數量\_金額不是可在測試時間的 hello 目標標籤的顯示資訊。 我們會移除這些資料行使用 hello[資料集中選取的資料行][ select-columns]模組。

hello 的快照集所示的紙匣中的秘訣是可能 toofall 我們實驗 toopredict (類別 0： 提示 = $0，1 類別： 提示 > $0 和秘訣 < = $5，類別 2： 提示 > $5 和秘訣 < = $10、 等級 3： 提示 > $10 到提示 < = $20類別 4： 提示 > $20)

![實驗快照](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

現在會顯示實際的測試類別分佈。 我們看到普遍類別 0 和 1 類別時，hello 其他類別少。

![測試類別分佈](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

b. 此實驗中，我們會使用混淆矩陣 toolook 在我們的預測精確度。 如下所示。

![混淆矩陣](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

請注意，雖然 hello 普遍類別上我們類別精確度是很好，hello 模型並不會很好的 「 學習 」 hello 少數類別上。

**3.迴歸工作**: toopredict hello 數量提示支付路線。

**已使用學習者：** 推進式決策樹

a. 對於這個問題，我們的目標 (或類別) 標籤是 "tip\_amount"。 我們的目標流失在此情況下，： 傾斜，提示\_類別細明體，總\_量; 所有這些變數會顯示 hello 通常無法使用，在測試時間的提示數量的相關資訊。 我們會移除這些資料行使用 hello[資料集中選取的資料行][ select-columns]模組。

hello 快照 belows 顯示我們實驗 toopredict hello 的數量 hello 提供提示。

![實驗快照](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

b. 針對迴歸問題，我們可以藉由查看 hello 預測中的 hello 平方錯誤測量 hello 我們預測的精確度，當做、 hello 判斷的係數和 hello 類似。 以下將進行示範。

![預測統計資料](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

我們會看到有關 hello 判斷的係數是 0.709，意味著大約 71 %hello 差異的說明由我們模型的係數。

> [!IMPORTANT]
> 深入了解 Azure Machine Learning toolearn 以及 tooaccess 並使用它，請參閱太[什麼是機器學習？](machine-learning-what-is-machine-learning.md)。 與 Azure Machine Learning 中的機器學習實驗的一大堆矔菛非常實用的資源為 hello [Cortana 智慧組件庫](https://gallery.cortanaintelligence.com/)。 hello 圖庫涵蓋實驗的一系列，並且提供 Azure Machine Learning 的 hello 各種功能的完整介紹。
> 
> 

## <a name="license-information"></a>授權資訊
此範例逐步解說和其隨附的指令碼由共用 Microsoft hello MIT 授權。 請 hello 目錄中的 hello 範例程式碼在 GitHub 上如需詳細資訊，在檢查 hello LICENSE.txt 檔。

## <a name="references"></a>參考
•    [Andrés Monroy NYC 計程車車程下載頁面](http://www.andresmh.com/nyctaxitrips/)  
•    [FOILing NYC 的計程車車程資料 (作者為 Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [NYC 計程車和禮車委託研究和統計資料](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
