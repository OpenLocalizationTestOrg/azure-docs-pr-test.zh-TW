---
title: "使用 Azure HDInsight 上的 Spark 資料科學的其中一個 aaaOverview |Microsoft 文件"
description: "hello Spark MLlib toolkit 帶來相當大的機器學習模型化功能 toohello 分散式 HDInsight 環境。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a4e1de99-a554-4240-9647-2c6d669593c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 515705684a46917c2741bf063d439b1cda016abb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-data-science-using-spark-on-azure-hdinsight"></a>在 Azure HDInsight 上使用 Spark 的資料科學概觀
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

此套件的主題示範如何 toouse HDInsight Spark toocomplete 一般資料科學工作例如擷取資料、 特徵設計、 模型和模型評估。 使用 hello 資料是 hello 2013 NYC 計程車行程及價位資料集的範例。 內建的 hello 模型包括羅吉斯和線性迴歸、 隨機樹系和梯度促進式樹狀結構。 hello 主題也顯示如何 toostore 這些模型在 Azure blob 儲存體 (WASB) 以及 tooscore 並評估其預測的效能。 更進階的主題會討論如何使用交叉驗證和超參數掃掠來訓練模型。 這個概觀主題也會參考 hello 主題描述如何設定 tooset hello 需要 toocomplete hello 步驟提供的 hello 逐步解說中的 Spark 叢集。 

## <a name="spark-and-mllib"></a>Spark 及 MLlib
[Spark](http://spark.apache.org/)開放原始碼的平行處理架構，可支援記憶體中處理 tooboost hello 巨量資料分析的應用程式效能。 hello Spark 處理引擎內建的速度、 容易使用，且複雜的分析。 Spark 的記憶體中分散式的計算功能讓您更好的選擇 hello 反覆演算法用於機器學習及圖形的計算。 [MLlib](http://spark.apache.org/mllib/) Spark 的可調整的機器學習文件庫，讓演算法 hello 模型化功能 toothis 分散式的環境。 

## <a name="hdinsight-spark"></a>HDInsight Spark
[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure 裝載的開放原始碼 Spark 供應項目。 它也包含支援**Jupyter PySpark 筆記本**hello Spark 叢集，可以執行轉換、 篩選和視覺化資料儲存在 Azure Blob (WASB) 的 Spark SQL 互動式查詢。 PySpark 為 hello Spark API Python。 hello 程式碼的程式碼片段提供 hello 解決方案，並顯示 hello 相關繪圖 toovisualize hello 資料這裡 Jupyter 筆記本 hello Spark 叢集上安裝中執行。 這些主題中的 hello 模型步驟包含顯示 tootrain，如何評估、 儲存和取用每種模型類型的程式碼。 

## <a name="setup-spark-clusters-and-jupyter-notebooks"></a>設定：Spark 叢集和 Jupyter Notebook
此逐步解說所提供的設定步驟和程式碼適用於使用 HDInsight Spark 1.6。 不過 Jupyter Notebook 可供 HDInsight Spark 1.6 版和 Spark 2.0 叢集兩者使用。 Hello 中提供的 hello 筆記本與連結 toothem 描述[Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello GitHub 儲存機制包含它們。 此外，hello 程式碼及連結的 hello 筆記本為泛型，應該在任何 Spark 叢集上運作。 如果您未使用 HDInsight Spark，hello 叢集中設定和管理步驟可能稍有不同於這裡所顯示。 為了方便起見，以下是 hello 的 hello 的 hello 連結 toohello Jupyter 筆記本 Spark 1.6 (執行中 Jupyter 筆記本伺服器 hello pySpark 核心 toobe) 和 Spark 2.0 (執行中 Jupyter 筆記本伺服器 hello pySpark3 核心 toobe):

### <a name="spark-16-notebooks"></a>Spark 1.6 Notebook
這些筆記型電腦有 toobe 的 Jupyter 筆記本伺服器 hello pySpark 核心中執行。

- [pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb)： 提供有關如何 tooperform 資料瀏覽、 建立模型及計分具有數個不同的演算法。
- [pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)：包含Notebook #1 中的主題，以及使用超參數微調和交叉驗證的模型開發。
- [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb)： 示範如何 toooperationalize 已儲存的模型使用 Python HDInsight 上的叢集。

### <a name="spark-20-notebooks"></a>Spark 2.0 Notebook
這些筆記型電腦有 toobe 的 Jupyter 筆記本伺服器 hello pySpark3 核心中執行。

- [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)： 這個檔案提供如何 tooperform 資料瀏覽、 建立模型及計分 Spark 2.0 中使用叢集 hello NYC 計程車路線資訊和價位資料集描述[這裡](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data)。 筆記本可能會快速瀏覽我們的 Spark 2.0 所提供的 hello 程式碼很好的起點。 更詳細的筆記本分析 hello NYC 計程車資料時，請參閱這份清單中的 hello 下一步筆記型電腦。 請參閱此清單後面，比較這些筆記本 hello 備註。 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb)： 此檔案會顯示如何 tooperform 資料 wrangling （Spark SQL 和資料框架作業），瀏覽模型及計分使用 hello NYC 計程車行程及價位資料集描述[這裡](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data)。
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb)： 此檔案會顯示如何 tooperform 資料 wrangling （Spark SQL 和資料框架作業），瀏覽模型及計分使用 hello 已知 Airline 準時離開從 2011年和 2012年的資料集。 我們整合 hello airline 資料集與 hello 機場天氣資料 （例如 windspeed、 溫度、 海拔高度等） 之前 toomodeling，因此這些天氣功能可以包含在 hello 模型中。

<!-- -->

> [!NOTE]
> hello airline 資料集加入 toohello Spark 2.0 筆記本 toobetter 說明 hello 使用分類演算法。 請參閱下列連結查看有關 airline 準時出發，資料集和天氣資料集的 hello:

>- 航班準時出發資料：[http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- 機場天氣資料：[https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
在 hello NYC 計程車的 hello Spark 2.0 筆記本與 airline 飛行延遲資料集可能需要 10 分鐘或更多 toorun （取決於 hello HDI 叢集大小）。 hello hello 上述清單中的第一個筆記本會顯示 hello 資料瀏覽的許多層面，視覺效果和 ML 模型定型中採用較少的時間 toorun 下取樣 NYC 資料集中的 hello 計程車行程及價位檔案都已預先已加入的筆記本： [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)筆記本會採用更短時間 toofinish （2-3 分鐘為單位），並可能不錯的起點快速瀏覽 hello 程式碼我們有提供 Spark 2.0。 

<!-- -->

如需 hello 實施 Spark 2.0 模型及計分模型耗用量的指引，請參閱 hello[耗用量的 Spark 1.6 文件](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb)例如大綱 hello 所需的步驟。 toouse 上的 Spark 2.0 中，這會取代 hello Python 程式碼包含檔案[這個檔案](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py)。

### <a name="prerequisites"></a>必要條件
下列程序的 hello 是相關的 tooSpark 1.6。 如需 hello Spark 2.0 版本中，使用 hello 筆記本所述，與連結 toopreviously。 

1. 您必須擁有 Azure 訂用帳戶。 如果還沒有訂用帳戶，請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。

2.您需要 Spark 1.6 叢集 toocomplete 本逐步解說。 toocreate 其中一個，請參閱所提供的 hello 指示[快速入門： 建立 Azure HDInsight 上的 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)。 hello 叢集類型和版本指定從 hello**選取叢集類型**功能表。 

![設定叢集](./media/machine-learning-data-science-spark-overview/spark-cluster-on-portal.png)

<!-- -->

> [!NOTE]
> 顯示 toouse Scala，而不是 Python toocomplete 端對端資料科學處理程序的工作的主題，請參閱 hello [Scala 使用 Azure 上的 Spark 資料科學](machine-learning-data-science-process-scala-walkthrough.md)。
> 
> 

<!-- -->

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

## <a name="hello-nyc-2013-taxi-data"></a>hello NYC 2013 計程車資料
hello NYC 計程車路線資料約 20 GB 的壓縮以逗號分隔值 (CSV) 檔案 (~ 48 GB 未壓縮)，可包含多個 173 百萬個個別的往返和 hello fares 支付每往返作業。 每個往返記錄包含 hello 收取和下車地點和時間、 匿名的 hack (driver) 授權編號和 medallion (計程車的唯一 id) 數目。 hello 資料涵蓋所有往返 hello 年份 2013年中，並提供下列兩個資料集的每個月的 hello:

1. hello 'trip_data' CSV 檔案包含路線的詳細資訊，例如乘客數目、 收取和持續時間和路線長度 dropoff 點、 中斷。 以下是一些範例記錄：
   
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

我們已經建立這些檔案和聯結的 hello 路線 0.1%範例\_資料和路線\_成單一資料集 toouse 再見 CSV 檔案，做為此逐步解說中的 hello 輸入資料集。 hello 唯一索引鍵 toojoin 路線\_資料和路線\_價位組成 hello 欄位： medallion 具 「 可回復\_授權與收取\_日期時間。 Hello 資料集的每一筆記錄會包含下列屬性代表 NYC 計程車路線 hello:

| 欄位 | 簡短描述 |
| --- | --- |
| medallion |匿名的計程車圓形徽章 (唯一的計程車識別碼) |
| hack_license |匿名的 Hackney 歸位字元駕照號碼 |
| vendor_id |計程車廠商識別碼 |
| rate_code |NYC 計程車費率 |
| store_and_fwd_flag |儲存和轉寄旗標 |
| pickup_datetime |上車日期和時間 |
| dropoff_datetime |下車日期和時間 |
| pickup_hour |於幾點上車 |
| pickup_week |挑選 hello 當年第幾週 |
| weekday |工作日 (範圍 1-7) |
| passenger_count |計程車車程的乘客數目 |
| trip_time_in_secs |往返時間 (秒) |
| trip_distance |以英哩計的車程距離 |
| pickup_longitude |上車處經度 |
| pickup_latitude |上車處緯度 |
| dropoff_longitude |下車經度 |
| dropoff_latitude |下車緯度 |
| direct_distance |上車與下車位置之間的直線距離 |
| payment_type |付款類型 (cas、信用卡等) |
| fare_amount |費用金額 |
| surcharge |額外費用 |
| mta_tax |Mta 稅額 |
| tip_amount |小費金額 |
| tolls_amount |收費金額 |
| total_amount |總金額 |
| tipped |已收到小費 (用 0 或 1 表示否或是) |
| tip_class |小費類別 (0：$0、1：$0-5、2：$6-10、3：$11-20、4：> $20) |

## <a name="execute-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>從 Jupyter 筆記本 hello Spark 叢集上執行程式碼
您可以啟動 hello Jupyter 筆記本從 hello Azure 入口網站。 尋找您儀表板上的 Spark 叢集，然後按一下它 tooenter 管理頁面，為您的叢集。 按一下 tooopen hello 筆記本 hello Spark 叢集，相關聯**叢集儀表板** -> **Jupyter 筆記本**。

![叢集儀表板](./media/machine-learning-data-science-spark-overview/spark-jupyter-on-portal.png)

您也可以瀏覽過***https://CLUSTERNAME.azurehdinsight.net/jupyter*** tooaccess hello Jupyter 筆記本。 此 URL 的 hello CLUSTERNAME 一部分取代為您自己的叢集 hello 名稱。 您需要系統管理員帳戶 tooaccess hello 筆記本 hello 密碼。

![瀏覽 Jupyter Notebooks](./media/machine-learning-data-science-spark-overview/spark-jupyter-notebook.png)

選取 PySpark toosee 目錄，其中包含的一些範例使用的 hello PySpark API.hello 筆記本包含此套件的 Spark 主題的 hello 程式碼範例時使用的預先封裝筆記本[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark)

您可以上傳 hello 筆記本，直接從[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark) toohello Jupyter 筆記本伺服器上的 Spark 叢集。 在您 Jupyter 的 hello 首頁上，按一下 hello**上傳**hello 權限屬於囉 」 畫面上的按鈕。 [檔案總管] 隨即開啟。 這裡貼上 hello GitHub （未經處理的內容） URL hello 筆記本，然後按一下**開啟**。 

您看到與您 Jupyter 檔案清單中的 hello 檔案名稱**上傳**按鈕一次。 按一下此 [上傳]  按鈕。 現在您已匯入 hello 筆記型電腦。 本逐步解說中的其他筆記本重複這些步驟 tooupload hello。

> [!TIP]
> 您可以以滑鼠右鍵按一下 hello 連結您的瀏覽器，並選取**複製連結**tooget hello github 未經處理內容的 URL。 您可以將此 URL 貼到 hello Jupyter 上傳檔案總管 對話方塊。
> 
> 

現在您可以：

* 依序按一下 hello 筆記型電腦，請參閱 hello 程式碼。
* 按 **SHIFT-ENTER** 執行每個儲存格。
* 按一下以執行 hello 整個筆記本**儲存格** -> **執行**。
* 使用 hello 自動視覺效果的查詢。

> [!TIP]
> hello PySpark 核心自動視覺化 hello 的 SQL (HiveQL) 查詢的輸出。 您可以在多種不同類型的視覺效果 （資料表、 圓形圖、 線條、 區域或列） 之間的 hello 選項 tooselect 使用 hello**類型**hello 筆記本中的功能表按鈕：
> 
> 

![泛型方法的羅吉斯迴歸 ROC 曲線](./media/machine-learning-data-science-spark-overview/pyspark-jupyter-autovisualization.png)

## <a name="whats-next"></a>後續步驟
現在您使用 HDInsight Spark 叢集設定，並已上傳 hello Jupyter 筆記本，您就準備好 toowork 透過對應 toohello 三個 PySpark 筆記本的 hello 主題。 它們會顯示如何 tooexplore 您的資料，然後如何 toocreate 和取用模型。 進階資料瀏覽以及如何模型化筆記本顯示 hello tooinclude 交叉驗證，超參數牽涉和模型評估。 

**資料探索和模型使用 Spark:**探索 hello 資料集以及建立、 計分，和透過 hello 工作來評估 hello 機器學習模型[以 hello Spark 中建立資料的二元分類和迴歸模型MLlib toolkit](machine-learning-data-science-spark-data-exploration-modeling.md)主題。

**模型耗用量：** toolearn 如何 tooscore hello 分類和迴歸模型建立本主題中，請參閱[分數及評估 Spark 建立機器學習模型](machine-learning-data-science-spark-model-consumption.md)。

**交叉驗證和超參數掃掠**：如需如何使用交叉驗證和超參數掃掠訓練模型的相關資訊，請參閱 [使用 Spark 進階資料探索和模型化](machine-learning-data-science-spark-advanced-data-exploration-modeling.md)

