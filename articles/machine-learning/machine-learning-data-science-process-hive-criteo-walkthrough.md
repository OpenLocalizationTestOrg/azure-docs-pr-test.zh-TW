---
title: "hello 小組資料科學程序中為 1 TB 的資料集上使用 Azure HDInsight Hadoop 叢集動作 |Microsoft 文件"
description: "使用 hello 小組資料科學程序的端對端案例，採用 HDInsight Hadoop 叢集 toobuild 及部署模型，使用大型 (1TB) 公開可用資料集"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a>-1 TB 的資料集上使用 Azure HDInsight Hadoop 叢集動作中的 hello 小組資料科學程序

本逐步解說將示範使用 hello 在端對端案例中使用資料科學的小組流程[Azure HDInsight Hadoop 叢集](https://azure.microsoft.com/services/hdinsight/)toostore，瀏覽、 功能工程師編寫，並公開向下一個 hello 的取樣資料可用[Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/)資料集。 我們在此資料上使用 Azure Machine Learning toobuild 二元分類模型。 我們也將顯示如何 toopublish 下列其中一種模型做為 Web 服務。

它也是可能 toouse IPython 筆記型電腦 tooaccomplish hello 工作本逐步解說。 使用者會像這種方法，應洽詢的 tootry hello [Criteo 逐步解說使用 hive 控制檔的 ODBC 連接](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb)主題。

## <a name="dataset"></a>Criteo 資料集說明
hello Criteo 資料是按預測資料集，大約是 370 GB gzip 壓縮 TSV 檔案 (~1.3TB 未壓縮)，可包含多個 4.3 10 億個資料錄。 它取自 [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/)提供的 24 天點選資料。 為資料科學家的 hello 方便起見，我們已將工具解壓縮資料可用 toous 的 tooexperiment 與。

在此資料集中的每一筆記錄包含 40 個資料行：

* hello 第一個資料行是標籤資料行，指出使用者是否按一下**新增**（值 1） 或不按一下其中一個 （值 0）
* 接下來 13 個資料行是數字，以及
* 最後 26 個資料行是類別資料行

hello 資料行匿名的並使用一連串的列舉名稱:"Col1"（適用於 hello 標籤資料行） 太 ' Col40"（為 hello 最後的類別資料行）。            

以下是 hello 的摘錄，第一次 20 的資料行與此資料集中的兩個觀察 （資料列）：

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

遺漏值中有兩個 hello 數值和分類資料行中此資料集。 我們將描述來處理 hello 遺漏值的簡單方法。 當我們將它們儲存成 Hive 資料表時，會探索 hello 資料的其他詳細資料。

**定義：** *點選率 (CTR):*這是 hello 百分比 hello 資料點選。 在此 Criteo 集中，hello CTR 的大約 3.3%或 0.033。

## <a name="mltasks"></a>預測工作的範例
本逐步解說將討論兩個範例預測問題：

1. **二進位分類**：預測使用者是否按下加入：
   
   * 類別 0：未按一下
   * 類別 1：按一下
2. **迴歸**： 從使用者特徵 ad 按一下 hello 機率的預測。

## <a name="setup"></a>為資料科學設定 HDInsight Hadoop 叢集
**附註：**這通常是**管理**工作。

設定 Azure 資料科學環境，用於使用 HDInsight 叢集以三個步驟建置預測性的分析解決方案：

1. [建立儲存體帳戶](../storage/common/storage-create-storage-account.md)： 這個儲存體帳戶是 Azure Blob 儲存體使用的 toostore 資料。 用於 HDInsight 叢集的 hello 資料儲存在這裡。
2. [自訂適用於資料科學的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)：這個步驟將會建立已在所有節點上安裝 64 位元 Anaconda Python 2.7 的 Azure HDInsight Hadoop 叢集。 自訂 hello HDInsight 叢集時，有兩個重要的步驟 （如本主題所述） toocomplete。
   
   * 您必須連結 hello 時就會建立在與 HDInsight 叢集的步驟 1 中建立的儲存體帳戶。 這個儲存體帳戶用來存取可處理 hello 叢集內的資料。
   * 在建立後，您必須啟用遠端存取 toohello 叢集前端節點 hello。 請記住您在此處指定 （不同於所指定的 hello 在其建立的叢集） hello 遠端存取認證： 需要 toocomplete hello 下列程序。
3. [建立 Azure ML 工作區](machine-learning-create-workspace.md)： 此 Azure 機器學習工作區用來建立機器學習模型之後的初始資料瀏覽和向下 hello HDInsight 叢集上的取樣。

## <a name="getdata"></a>取得並從公用來源取用資料
hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/)資料集可以透過按一下 hello 連結，接受 hello 使用條款，並提供名稱。 其外觀的快照如下所示：

![接受 Criteo 條款](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

按一下**繼續 tooDownload** tooread 更多關於 hello 資料集和其可用性。

hello 資料常駐於公用中[Azure blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)位置： wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/。 hello"wasb 」 是指 tooAzure Blob 儲存體位置。 

1. 這個公用 blob 儲存體中的 hello 資料所組成的解壓縮資料的三個子資料夾。
   
   1. hello 子資料夾*原始/count/*包含 hello 第一次的 21 天的資料-從天\_00 tooday\_20
   2. hello 子資料夾*原始/定型/*組成的資料，某一天一天\_21
   3. hello 子資料夾*原始/測試/*兩天的資料，包含日\_22 和日\_23
2. 人員想 toostart hello 原始 gzip 資料，這些是也可用在 hello 的主要資料夾*原始 /*為 day_NN.gz，從 00 too23 NN 的地方。

替代方法 tooaccess，瀏覽及此不需要任何本機下載說明在此逐步解說稍後當我們建立 Hive 資料表的資料模型。

## <a name="login"></a>登入 toohello 叢集前端節點
中的 hello 叢集中，使用 hello toohello 前端節點 toolog [Azure 入口網站](https://ms.portal.azure.com)toolocate hello 叢集。 按一下上剩餘的 hello hello HDInsight elephant 圖示，然後按兩下 hello 叢集的名稱。 瀏覽 toohello**組態**索引標籤，按兩下 hello hello 頁面底部 hello 連接 圖示，然後輸入您的遠端存取認證出現提示時。 這會帶您 toohello 的 hello 叢集的前端節點。

以下是典型的第一個記錄檔中 toohello 叢集前端節點看起來像：

![登入 toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

左側 hello，我們會看到 「 Hadoop 命令列 」，這是進行 hello 資料瀏覽我們 workhorse hello。 我們也會看到兩個實用的 URL - "Hadoop Yarn Status" 和 "Hadoop Name Node"。 hello yarn 狀態 URL 會顯示工作進度和 hello 名稱節點 URL 在 hello 叢集設定中提供詳細資料。

現在我們已設定，並準備 toobegin 第一部分 hello 逐步解說： 使用 Hive 和 Azure 機器學習準備資料的資料瀏覽。

## <a name="hive-db-tables"></a> 建立 Hive 資料庫和資料表
toocreate Hive 資料表我們 Criteo 資料集，開啟 hello ***Hadoop 命令列***hello 桌面的 hello 前端節點，且輸入 hello 命令輸入 hello Hive 目錄

    cd %hive_home%\bin

> [!NOTE]
> 在此逐步解說中執行所有的登錄區命令，從 hello Hive bin / 目錄提示字元。 如此可自動處理路徑相關問題。 我們使用 hello 詞彙"Hive 目錄 prompt"，"Hive bin / 目錄提示字元 」，和 「 Hadoop 命令列 」 交換使用。
> 
> [!NOTE]
> tooexecute 任何 Hive 查詢，其中一個永遠都可以使用下列命令的 hello:
> 
> 

        cd %hive_home%\bin
        hive

Hello Hive REPL 就會出現與 「 hive > 」 登入，只需剪下和貼上 hello 查詢 tooexecute 它。

hello 下列程式碼建立資料庫 「 criteo 」，並接著會產生 4 資料表：

* *資料表來產生計數*天天內建\_00 tooday\_20，
* *hello 定型資料集資料表用於*建置當天\_21，和
* 兩個*資料表 hello 做測試資料集*建置當天\_22 和日\_23 分別。

因為其中一個 hello 天為假日中，而且我們想 toodetermine 如果 hello 模型可以偵測到差異假日和非假日 hello 點選連結速度，我們可以分割成兩個不同資料表的我們的測試資料集。

hello 指令碼[範例 &#95; hive &#95; 建立 （& s) #95; criteo &#95; 資料庫 &#95; 和 &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)此處會顯示為方便起見：

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

我們請注意，所有這些資料表是我們只要點 tooAzure Blob 儲存體 (wasb) 的位置做為外部。

**有兩種方式 tooexecute ANY Hive 查詢現在提到。**

1. **使用 hello Hive REPL 命令列**: hello 第一次是 tooissue"hive"命令並複製和貼上在 hello Hive REPL 命令列的查詢。 toodo 此，請執行：
   
        cd %hive_home%\bin
        hive
   
     現在 hello REPL 命令列，在剪下和貼上 hello 查詢會執行它。
2. **儲存查詢 tooa 檔案以及執行 hello 命令**: hello 第二種是 toosave hello 查詢 tooa.hql 檔案 ([範例 &#95; hive &#95; 建立 （& s) #95; criteo &#95; 資料庫 &#95; 和 &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) 和問題 hello 下列然後命令 tooexecute hello 查詢：
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a>確認資料庫和資料表的建立
接下來，我們以 hello hello Hive 紙匣中的下列命令確認 hello 建立 hello 資料庫 / 目錄提示：

        hive -e "show databases;"

這會提供：

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

這可確認 hello 建立 hello 新資料庫，"criteo"。

toosee 資料表建立，我們只是發出 hello 命令這裡 hello Hive 紙匣 / 目錄提示：

        hive -e "show tables in criteo;"

然後，我們會看到 hello 下列輸出：

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a> 在 Hive 中的資料瀏覽
現在我們已備妥 toodo 登錄區中的一些基本的資料瀏覽。 我們透過計算 hello 數目 hello 定型中的範例開頭，而且測試資料的資料表。

### <a name="number-of-train-examples"></a>訓練範例的數目
hello 內容[範例 &#95; hive #95 計數 &#95; 定型 &#95; 資料表 &; #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql)如下所示：

        SELECT COUNT(*) FROM criteo.criteo_train;

這會產生：

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

或者，其中也可能會發出 hello hello Hive 紙匣中的下列命令 / 目錄提示：

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a>測試中的範例數目 hello 兩個測試資料集
我們現在計數 hello 的 hello 兩個測試資料集的範例。 hello 內容[範例 &#95; hive &#95; 計數 &#95; criteo &#95; 測試 &#95; 天 &#95; 22 &#95; 資料表 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql)這裡：

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

這會產生：

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

像往常一樣，我們也可呼叫 hello 指令碼從 hello Hive bin / 目錄發出 hello 命令提示字元：

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

最後，我們檢驗 hello 測試中的範例數目依據一天的 hello 測試資料集\_23。

hello 命令 toodo 這是只顯示一個類似 toohello (請參閱太[範例 &#95; hive #95 計數 &#95; criteo &#95; 測試 &#95; 天 &#95; 23 &; #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

這會提供：

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a>Hello 定型資料集內的標籤發佈
hello 定型資料集中的 hello 標籤分佈是感興趣。 toosee，我們顯示的內容[範例 &#95; hive #95 criteo &#95; 標籤 &#95; 散發 &#95; 定型 &; #95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

這會產生 hello 標籤發佈：

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

請注意 hello 正面標籤的百分比，大約是 3.3%（與 hello 原始資料集一致）。

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a>長條圖分佈在 hello 部分數值變數的定型資料集
我們可以使用 Hive 的原生 「 長條圖\_數值"toofind 出 hello 數值變數哪些 hello 分佈看起來像函式。 以下是 hello 內容[範例 &#95; hive #95 criteo &#95; 長條圖 &; #95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

這會產生下列 hello:

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

hello 側檢視-分裂 Hive 做 tooproduce 是類似 SQL 的輸出，而不是 hello 一般清單中的組合。 請注意，在 hello 這個資料表，hello 第一個資料行對應 toohello bin 置中與 hello 第二個 toohello bin 頻率。

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a>大約百分位數 hello 中部分數值變數的定型資料集
也與數值變數的感興趣的是 hello 計算的近似百分比也一樣。 Hive 的原生 "percentile\_approx" 會為我們執行此動作。 hello 內容[範例 &#95; hive &#95; criteo &#95; 相近 &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql)是：

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

這會產生：

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

我們在每 hello 依百分位數分佈通常是密切相關的 toohello 長條圖任何的散發數值變數。         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a>尋找 hello 定型資料集中的某些類別資料行的唯一值數目
延續 hello 資料瀏覽，我們現在發現某些類別的資料行，則會接受的唯一值的 hello 數目。 toodo，我們顯示的內容[範例 &#95; hive &#95; criteo &#95; 唯一 &#95; 值 &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

這會產生：

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

我們注意到 Col15 有 1900 萬個唯一值！ 使用貝氏技術，如 「 一個熱編碼 」 tooencode 這類高維度的類別變數並不可行。 特別是，我們將說明並示範稱為 [以計數學習](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) 功能強大又穩健的技術，以有效率地解決此問題。

我們來結束此子區段查看 hello 的一些其他的類別資料行以及唯一值數目。 hello 內容[範例 &#95; hive &#95; criteo &#95; 唯一 &#95; 值 &#95; 多個 （& s) #95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql)會：

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

這會產生：

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

同樣地我們看到，除了第 20 欄，所有 hello 其他資料行有多個唯一值。

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a>成對的 hello 定型資料集中的類別變數的共同的發生次數

hello 共同的發生次數的類別變數配對也是感興趣。 這可以使用中的 hello 程式碼來決定[範例 &#95; hive &#95; criteo &#95; 配對 &#95; 類別 （& s) #95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

我們反向順序 hello 計數所發生的情形，並在此情況下查看 hello 前 15。 這會提供：

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a>向 Azure 機器學習範例 hello 資料集
擁有已探索的 hello 資料集，並示範如何我們可能會執行這種類型的任何變數 （包括組合），我們現在關閉取樣 hello 資料集探索，讓我們可以建立 Azure Machine Learning 中的模型。 請記住，我們著重在該 hello 問題是： 提供一組範例屬性 （從 Col2-Col40 功能值），我們的預測是否 Col1 是 0 （沒有按一下） 或 1 （按一下）。

toodown 範例我們定型和測試資料集 too1 %hello 原始大小，我們使用 Hive 的原生 rand （） 函式。 hello 下一個指令碼，[範例 &#95; hive &#95; criteo & #95，可以 #95 定型 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql)做法 hello 定型資料集：

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

這會產生：

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

hello 指令碼[範例 &#95; hive &#95; criteo & #95，可以 #95 測試 &#95; 天 &#95; 22 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql)會測試資料，為一天\_22:

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

這會產生：

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


最後，hello 指令碼[範例 &#95; hive &#95; criteo & #95，可以 #95 測試 &#95; 天 &#95; 23 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql)會測試資料，為一天\_23:

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

這會產生：

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

與這個項目，我們會準備 toouse 我們向下取樣定型和測試資料集來建立 Azure Machine Learning 中的模型。

我們將在 tooAzure Machine Learning 中，也就是考量 hello 計數資料表之前，會最後的重要元件。 在 hello 下一步 子區段中，我們將在討論一些詳細資料。

## <a name="count"></a>Hello 計數資料表上的簡短討論
如我們所見，數個類別變數有極高的維度性。 在我們的逐步解說中，我們提供功能強大的技術稱為[學習與計算](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx)tooencode 這些變數，以有效率、 強固的方式。 在這項技術的詳細資訊是中提供的 hello 連結。

[!NOTE]
>在此逐步解說中，我們會著重在使用的高維度的類別特徵的計數資料表 tooproduce compact 表示。 這不是 hello 方式 tooencode 類別的功能。如需其他技術的詳細資訊，想要的使用者可以簽出[一個熱-編碼](http://en.wikipedia.org/wiki/One-hot)和[特徵雜湊](http://en.wikipedia.org/wiki/Feature_hashing)。
>

toobuild hello 計數的資料計數資料表，我們會使用 hello 資料 hello 資料夾原始/計數中。 在模型化 區段中，我們對使用者顯示 hello 如何 toobuild 這些函數會計算資料表從從頭開始或者 toouse 類別特徵其瀏覽的預先建置的計數資料表。 在如下所示，當我們太 「 預先建置計數資料表 」，是指使用 hello 我們提供的計數資料表。 取得如何 tooaccess 這些資料表提供 hello 下一節中的詳細的指示。

## <a name="aml"></a> 使用 Azure Machine Learning 建置模型
在 Azure Machine Learning 建置模型的程序遵循下列步驟：

1. [Hive 資料表中的 hello 資料送入 Azure Machine Learning](#step1)
2. [建立 hello 實驗： 清除 hello 資料和特徵化的計數資料表](#step2)
3. [建置、 火車和分數 hello 模型](#step3)
4. [評估 hello 模型](#step4)
5. [Hello 模型發佈為 web 服務](#step5)

現在我們已經準備好 toobuild Azure Machine Learning studio 中的模型。 我們向下取樣的資料會儲存為 hello 叢集中的 Hive 資料表。 我們使用 Azure Machine Learning hello**匯入資料**模組 tooread 這項資料。 hello 認證 tooaccess hello 儲存體帳戶的此叢集提供哪些如下所示。

### <a name="step1"></a>步驟 1： 從 Hive 資料表取得資料，放入 Azure 機器學習使用 hello 資料匯入模組，並選取的機器學習實驗
藉由選取 [+ 新增] -> [實驗] -> [空白實驗] 開始。 然後，從 hello**搜尋**hello 左上方，「 匯入資料 」 的搜尋 方塊。 拖放 hello**匯入資料**toohello 實驗畫布 （hello 中間部分囉 」 畫面） toouse hello 模組上存取資料的模組。

這是什麼 hello**匯入資料**從 hello Hive 資料表取得資料時看起來像：

![「匯入資料」取得資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

Hello**匯入資料**模組，提供在 hello 圖形都只是範例的 hello 排序值的 hello 參數 hello 值需要 tooprovide。 以下是一些一般指導方針 hello toofill out hello 參數的設定方式**匯入資料**模組。

1. 對 **資料來源**
2. 在 hello **Hive 資料庫查詢**方塊中，簡單的 SELECT * FROM < 您\_資料庫\_name.your\_資料表\_名稱 >-即已足夠。
3. **Hcatalog 伺服器 URI**：如果您的叢集是 "abc"，那麼這就是：https://abc.azurehdinsight.net
4. **Hadoop 使用者帳戶名稱**: hello 的 commissioning hello 叢集 hello 次選擇的使用者名稱。 （非 hello 遠端存取使用者名稱 ！）
5. **Hadoop 使用者帳戶密碼**: hello 選擇時的 commissioning hello 叢集 hello hello 使用者名稱密碼。 （不 hello 遠端存取密碼 ！）
6. **輸出資料的位置**：選擇 "Azure"
7. **Azure 儲存體帳戶名稱**: hello 與 hello 叢集相關聯的儲存體帳戶
8. **Azure 儲存體帳戶金鑰**: hello 與 hello 叢集相關聯的 hello 儲存體帳戶金鑰。
9. **Azure 容器名稱**： 如果 hello 叢集名稱為"abc"，則這通常是只是"abc，"。

一次 hello**匯入資料**完成取得的資料 （您將看到在 hello 模組 hello 綠色勾號），將此資料儲存為資料集 （與您選擇的名稱）。 看起來像這樣：

![「匯入資料」儲存資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

以滑鼠右鍵按一下 hello 輸出連接埠的 hello**匯入資料**模組。 這會顯示 [另存為資料集] 選項和 [視覺化] 選項。 hello**視覺化**選項，如果按下，會顯示 hello 的資料，以及適用於某些摘要統計資料的右方面板的 100 個資料列。 toosave 資料，只需選取**將儲存為資料集**並遵循指示。

tooselect hello 儲存的資料集以用於機器學習實驗中，找出 hello 資料集使用 hello**搜尋**hello 遵循圖所示的方塊。 然後只輸入出 hello 名稱指定給 hello 資料集部分並拖曳 hello 資料集拖曳至 tooaccess hello 主面板。 拖曳 hello 主要面板選取用於機器學習模型。

![拖曳到 hello 主要面板的資料集](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> Hello 定型和 hello 測試資料集執行這項操作。 此外，請記得 toouse hello 資料庫名稱和您針對此目的所提供的資料表名稱。 hello 圖中所使用的 hello 值是僅供圖 purposes.* *
> 
> 

### <a name="step2"></a>步驟 2： 建立簡易實驗 Azure Machine Learning toopredict 按 / 沒有按下
我們的 Azure ML 實驗看起來如下所示：

![Machine Learning 實驗](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

現在，我們會檢查此實驗 hello 重要元件。 提醒您，我們需要的 toodrag 我們已儲存的定型和測試資料集 tooour 實驗畫布上的第一次。

#### <a name="clean-missing-data"></a>清除遺漏的資料
hello**清除遺漏資料**模組沒有其名所示： 它會清除遺漏資料可以是使用者指定的方式。 查看此模組，我們看到這個：

![清除遺漏的資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

在這裡，我們選擇 tooreplace 完全為遺漏值，以 0。 還有其他選項，可以藉由查看 hello 模組中的 hello 下拉式清單中看到。

#### <a name="feature-engineering-on-hello-data"></a>Hello 資料特徵設計
大型資料集的部分類別功能可以有數百萬的唯一值。 使用像是一個有效編碼的單純方法來表示高維度類別功能是完全不可行的。 在本逐步解說中，我們將示範如何使用內建的 Azure 機器學習模組 toogenerate toouse 計數功能壓縮這些高維度的類別變數的表示法。 hello 最終結果是較小的模型、 更快的定型時間及和效能度量資訊會相當類似 toousing 其他技術。

##### <a name="building-counting-transforms"></a>建置計數轉換
toobuild 計數功能，我們使用 hello**建置計數轉換**Azure Machine Learning 中使用的模組。 hello 模組看起來像這樣：

![建置計數轉換模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![建置計數轉換模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)

> [!IMPORTANT] 
> 在 [hello**計算資料行**] 方塊中，我們輸入資料行，我們希望 tooperform 次數。 一般來說，這些是 (如上所述) 高維度類別資料行。 我們曾提及 hello 開頭的 hello Criteo 資料集有 26 類別資料行： 從第 15 欄 tooCol40。 在這裡，倚賴它們全部，並提供其索引也 （從 15 too40 所示，以逗號分隔)。
> 

中的 toouse hello 模組 hello MapReduce 模式 （適用於大型資料集），我們需要存取 tooan HDInsight Hadoop 叢集中 (一個用於進行探索功能，可重複使用針對此用途以及 hello) 和它的認證。 hello 之前的圖表說明哪些 hello 填滿的值外觀 （取代提供您自己使用案例的相關與 hello 值）。

![模組參數](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

在 hello 圖中，我們會示範如何 tooenter hello 輸入 blob 的位置。 此位置已 hello 保留用來建立計數資料表的資料。

此模組執行之後，我們可以儲存 hello 轉換稍後 hello 模組上按一下滑鼠右鍵，然後選取 hello**存轉換**選項：

![「另存為轉換」選項](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

在我們實驗架構中如上所示，hello 資料集 」 ytransform2 」 對應精確 tooa 儲存計數轉換。 這項實驗中的 hello 其餘部分，我們假設使用該 hello 讀取器**建置計數轉換**模組上某些資料 toogenerate 計數，然後可以使用這些計數 toogenerate 計數功能上 hello 定型和測試資料集。

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a>選擇項目計數功能 tooinclude 一部分 hello 定型和測試資料集
一旦準備好轉換計數，hello 使用者可以選擇哪些功能 tooinclude 中其定型和測試資料集使用 hello**修改計數資料表參數**模組。 為了完整性，我們會在此顯示這個模組，但為了簡單起見，請不要真的在實驗中使用它。

![修改計數資料表參數](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

在此情況下，可以看出我們已選擇 toouse 只 hello 對數勝算和 tooignore hello back off 資料行。 我們也可以設定參數，例如 hello 記憶體回收筒臨界值，多少虛擬先前範例 tooadd 變平滑，及是否 toouse 任何拉普拉斯 noise 與否。 所有這些都進階功能，而且很 toobe 註明 hello 預設值是很好的起點是新的功能產生 toothis 類型使用者。

##### <a name="data-transformation-before-generating-hello-count-features"></a>資料轉換之前產生 hello 計數功能
現在我們著重於很重要的一點需轉換我們定型和測試資料的先前 tooactually 產生計數功能。 請注意，有兩個**執行 R 指令碼**我們套用 hello 計數轉換 tooour 資料之前使用的模組。

![執行 R 指令碼模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

以下是第一個 R 指令碼 hello:

![第一個 R 指令碼](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

在此 R 指令碼中，我們重新命名我們的資料行 toonames"Col1"太"Col40"。 這是因為 hello 計數轉換必須要有這種格式的名稱。

在 hello 第二個 R 指令碼中，我們平衡 hello 正數和負數類別之間的通訊群組 （類別 1 和 0 分別） 由 downsampling hello 負類別。 hello R 指令碼以下顯示如何 toodo 這樣：

![第二個 R 指令碼](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

在這個簡單的 R 指令碼，我們使用 「 pos\_協商\_比率"tooset hello 數量正數 hello 與 hello 負類別之間取得平衡。 這是很重要，因為通常改善類別不平衡有分類問題中的效能優勢 hello 類別發佈所在 toodo 有所偏差 （請記得，在本例中，我們有 3.3%正類別和 96.7%負類別）。

##### <a name="applying-hello-count-transformation-on-our-data"></a>在我們的資料上套用 hello 計數轉換
最後，我們可以使用 hello**套用轉換**模組 tooapply hello 計數轉換在我們的定型和測試資料集。 此模組會將儲存的 hello 計數轉換，當做一個輸入和 hello 定型或測試資料集，如 hello 其他輸入，並傳回的資料計數功能。 如下所示：

![套用轉換模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a>摘錄，hello 計數功能的外觀
很多好處 toosee hello 計數功能看起來像在我們的案例。 以下示範該摘錄：

![計數功能](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

在這段摘錄中，我們顯示 hello 我們上計算的資料行，我們得到 hello 計數，且在加法 tooany 相關 backoffs 記錄勝算的特徵。

現在，我們已準備好 toobuild 使用這些已轉換的資料集的 Azure 機器學習模型。 Hello 下一節，我們會示範如何完成。

### <a name="step3"></a>步驟 3： 建立、 定型和計分 hello 模型

#### <a name="choice-of-learner"></a>選擇學習者
首先，我們需要 toochoose 學習模組。 我們會持續 toouse 兩個類別，促進式決策樹為我們的學習因子。 以下是此學習模組的 hello 預設選項：

![二元促進式決策樹參數](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

我們實驗中，我們會持續 toochoose hello 預設值。 記下該 hello 預設都通常有意義，且對效能的好方法 tooget 快速基準。 您可以清除參數如果您選擇您有的 tooonce 基準，就可改善效能。

#### <a name="train-hello-model"></a>定型 hello 模型
對於訓練，我們只需叫用 **訓練模型** 模組。 兩個輸入 tooit hello 為 hello 二級促進式決策樹的學習因子和我們的定型資料集。 其如下所示：

![訓練模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a>計分 hello 模型
一旦已定型的模型，我們已準備資料集 tooevaluate tooscore hello 上的測試其效能。 要執行此作業使用 hello**計分模型**hello 遵循圖中，連同所示的模組**評估模型**模組：

![Score Model module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a>步驟 4： 評估 hello 模型
最後，我們希望 tooanalyze 模型效能。 通常，針對兩個類別 （二進位） 的分類問題，良好的量值為 hello AUC。 toovisualize，我們連接 hello**計分模型**模組 tooan**評估模型**這個模組。 按一下**視覺化**上 hello**評估模型**模組會產生類似下列其中一個 hello 圖形：

![評估模組 BDT 模型](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

二進位檔 （或兩個類別） 中分類問題，良好的預測精確度量值為 hello 下曲線區域 (AUC)。 接下來，我們會顯示在我們的測試資料集上使用此模型的結果。 tooget hello，以滑鼠右鍵按一下 hello 輸出連接埠**評估模型**模組然後**視覺化**。

![視覺化評估模型模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a>步驟 5: Hello 模型發行為 Web 服務
hello 能力 toopublish 為 web 服務，並至少加裝製作出 Azure 機器學習模型會進行廣泛使用的重要功能。 完成之後，任何人都可以製作呼叫 toohello web 服務所需的預測，，和 hello web 服務使用 hello 模型 tooreturn 這些預測的輸入資料。

toodo，我們先儲存我們已定型的模型中當做已定型的模型物件。 這是以滑鼠右鍵按一下 hello**定型模型**模組，使用 hello**儲存為定型的模型**選項。

接下來，我們需要 toocreate 輸入和輸出的 web 服務連接埠：

* 輸入的連接埠 hello 相同形成所需的預測 hello 資料以取得資料
* 輸出連接埠傳回 hello 計分標籤和 hello 相關聯的機率。

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a>選取幾個資料列之資料的 hello 輸入連接埠
它是方便 toouse**套用 SQL 轉換**模組 tooselect 只是 10 的資料列 tooserve hello 為輸入連接埠資料。 選取這些資料列的資料，我們使用如下所示的 hello SQL 查詢的輸入連接埠：

![輸入連接埠資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a>Web 服務
現在我們已備妥 toorun 小型的實驗可能是使用的 toopublish web 服務。

#### <a name="generate-input-data-for-webservice"></a>產生 Web 服務的輸入資料
第零個步驟，hello 計數資料表很大，因為我們便會採取的測試資料的幾行並從其中產生輸出的資料計數功能。 這可做為我們的 web 服務的 hello 輸入的資料格式。 其如下所示：

![建立 BDT 輸入資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> Hello 輸入的資料格式，我們現在使用 hello 的 hello 輸出**Count Featurizer**模組。 此實驗執行完成時，一旦儲存 hello 輸出從 hello **Count Featurizer**模組做為資料集。 此資料集用於 hello hello web 服務中的輸入資料。
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a>發佈 Web 服務的評分實驗
首先，我們顯示其外觀。 hello 基本結構是**計分模型**模組接受我們定型的模型物件和我們在使用 hello hello 先前步驟中產生的輸入資料的幾行**Count Featurizer**模組。 我們使用 「 選取資料行中資料集 」 tooproject 出 hello 計分標籤與 hello 分數機率。

![選取資料集中的資料行](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

請注意如何 hello**資料集中選取的資料行**模組可用於 '過濾' 的資料從資料集。 我們會顯示以下 hello 內容：

![使用資料集的模組中的 hello 選取資料行篩選](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

tooget hello 藍色輸入和輸出連接埠，您只是按一下**準備 webservice**在 hello 右下方。 執行這項實驗也可讓我們 toopublish hello web 服務： 按一下 hello**發佈 WEB 服務**在 hello 下方所示，這裡的圖示：

![發佈 Web 服務](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

Hello webservice 發行之後，我們會取得重新導向的 tooa 頁面，因此看起來：

![Web 服務儀表板](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

我們可以看到兩個 web 服務連結左邊為 hello:

* hello**要求/回應**服務 （或 RR） 僅供單一預測，而且我們利用此 workshop 中。
* hello**批次執行**服務 (BES) 用於批次預測，而且需要 hello 使用的輸入的資料 toomake 預測位於 Azure Blob 儲存體。

按一下 hello 連結**要求/回應**會帶我們 tooa 頁面，提供預先定義程式碼在 C#、 python 和。進行呼叫 toohello webservice 可以輕鬆地使用這個代碼。 請注意該 hello 這個頁面上的 API 金鑰需要 toobe 用來進行驗證。

它是方便 toocopy 此 python 程式碼 hello IPython 筆記型電腦 tooa 新儲存格上方時。

這裡我們顯示 hello 正確的 API 金鑰的 python 程式碼區段。

![Python 程式碼](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

請注意，我們取代 hello 預設 API 金鑰我們 webservices API 金鑰。 按一下**執行**IPython 中此資料格筆記本會產生下列回應 hello:

![IPython 回應](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

我們會了解 hello 兩個測試我們詢問 （hello JSON framework hello python 指令碼) 中的範例，我們得到解答 hello 表單"計分標籤，計分機率 」。 請注意，在此情況下，我們選擇 hello 預設值的 hello 預先定義的程式碼提供 (0 的所有數值資料行和 hello 字串的所有類別資料行的 「 值 」)。

這會結束我們的端對端逐步解說顯示如何使用 Azure Machine Learning toohandle 大型資料集。 我們入門 tb 資料、 建構預測模型並將它部署為 web 服務 hello 雲端中。

