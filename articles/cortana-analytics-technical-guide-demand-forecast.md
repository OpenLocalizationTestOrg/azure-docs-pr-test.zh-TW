---
title: "aaaDemand 能源技術指南中的預測 |Microsoft 文件"
description: "指定預測中能源技術指南 toohello Intelligence< Cortana 方案範本。"
services: cortana-analytics
documentationcenter: 
author: yijichen
manager: ilanr9
editor: yijichen
ms.assetid: 7f1a866b-79b7-4b97-ae3e-bc6bebe8c756
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: inqiu;yijichen;ilanr9
ms.openlocfilehash: c97b7c19c9e3a317aecc329e61a0692d2f1ec53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-demand-forecast-in-energy"></a>預測中能源需求的技術指南 toohello Cortana 智慧方案範本
## <a name="overview"></a>**概觀**
設計解決方案範本 tooaccelerate hello 建置程序在 Cortana 智慧套件之上 E2E 示範。 範本部署會佈建必要 Cortana 智慧元件與您訂用帳戶，並建置 hello 之間的關聯性。 它也會取得從資料模擬應用程式所產生的範例資料設 hello 資料管線。 從提供的 hello 連結下載 hello 資料模擬器並將它安裝在本機電腦上，請參閱 toohello readme.txt 檔案，以使用 hello 模擬器的相關指示。 Hello 資料管線並產生然後 hello Power BI 儀表板上要視覺化的機器學習預測的開始，將會產生從 hello 模擬器產生的資料。

您可以找到 hello 方案範本[這裡](https://gallery.cortanaintelligence.com/SolutionTemplate/Demand-Forecasting-for-Energy-1)

hello 部署程序將引導您完成幾個步驟 tooset 方案認證。 請確定記錄例如方案名稱、 使用者名稱和密碼 hello 部署時提供這些認證。

這份文件 hello 目標是 tooexplain hello 參考架構和佈建您的訂用帳戶，做為此解決方案範本的一部分中的不同元件。 hello 文件也參 tooreplace hello 範例資料，以自己 toobe 無法 toosee insights/預測您贏了資料的真實資料的方式。 此外，hello 文件討論 hello hello 需要 toobe，如果您想 toocustomize hello 方案要與您自己的資料修改的方案範本的一部分。 Hello 結尾會提供如何 toobuild hello 此解決方案範本的 Power BI 儀表板上的指示。

## <a name="big-picture"></a>**概觀**
![](media/cortana-analytics-technical-guide-demand-forecast/ca-topologies-energy-forecasting.png)

### <a name="architecture-explained"></a>所說明的架構
部署 hello 方案時，會啟動 Cortana Analytics suite 這套內各種 Azure 服務 (*也就是*事件中樞、串流分析、HDInsight、Data Factory、機器學習服務等)。 hello 架構圖上面所示，在高的層級，hello 需求預測能源方案範本從端對端的建構方式。 您將無法 tooinvestigate 這些服務上按一下這些 hello 與 hello hello 方案部署所建立的方案範本圖表。 hello 下列各節說明每個片段。

## <a name="data-source-and-ingestion"></a>**資料來源及擷取**
### <a name="synthetic-data-source"></a>綜合資料來源
此範本 hello 資料使用來源會產生從桌面應用程式，您將會下載並成功部署之後在本機執行。 您會尋找 hello 指示 toodownload 並安裝此應用程式在 hello 屬性列中，當您選取 hello hello 解決方案範本圖表上呼叫能源預測資料模擬器的第一個節點。 此應用程式摘要 hello [Azure 事件中心](#azure-event-hub)服務與資料點或將使用在 hello 方案流程 hello 其餘部分的事件。

只有當它在您的電腦上執行時，才 hello 事件產生應用程式將會填入 hello Azure 事件中心。

### <a name="azure-event-hub"></a>Azure 事件中樞
hello [Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)服務是 hello 收件者的 hello hello 綜合上面所述的資料來源所提供的輸入。

## <a name="data-preparation-and-analysis"></a>**資料準備和分析**
### <a name="azure-stream-analytics"></a>Azure 串流分析
hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)服務已接近即時的分析 hello hello 從輸入資料流上使用的 tooprovide [Azure 事件中心](#azure-event-hub)服務並發行到結果[Power BI](https://powerbi.microsoft.com)儀表板，以及保存所有未經處理的內送事件 toohello [Azure 儲存體](https://azure.microsoft.com/services/storage/)服務以便之後處理 hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)服務。

### <a name="hd-insights-custom-aggregation"></a>HD Insights 自訂彙總
hello Azure HD Insight 服務是使用的 toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) hello 未經處理的事件上使用 hello Azure Stream Analytics 服務已封存的指令碼 （由 Azure Data Factory 協調） tooprovide 彙總。

### <a name="azure-machine-learning"></a>Azure Machine Learning
hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) （由 Azure Data Factory 協調） 來使用服務 toomake 未來的功率耗用量給定收到 hello 輸入特定地區的預測。

## <a name="data-publishing"></a>**資料發佈**
### <a name="azure-sql-database-service"></a>Azure SQL Database 服務
hello [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)服務已收到 hello Azure 機器學習服務將會用在 hello （由 Azure Data Factory） 使用的 toostore hello 預測[Power BI](https://powerbi.microsoft.com)儀表板。

## <a name="data-consumption"></a>**資料耗用量**
### <a name="power-bi"></a>Power BI
hello [Power BI](https://powerbi.microsoft.com)服務是使用的 tooshow hello 所提供的彙總的儀表板[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)服務，以及視需要預測結果儲存在[Azure SQL資料庫](https://azure.microsoft.com/services/sql-database/)，產生使用 hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)服務。 如需有關如何 toobuild hello Power BI 儀表板此解決方案範本的指示，請參閱 toohello 一節。

## <a name="how-toobring-in-your-own-data"></a>**如何在您自己的資料 toobring**
本章節描述如何 toobring 您自己的資料 tooAzure，和區域會需要變更 hello 資料帶入這個架構。

也不太可能，您將任何資料集符合使用此解決方案範本的 hello 資料集。 了解您的資料和需求將會是非常重要的是您如何修改此範本 toowork 與您自己的資料。 如果這是您第一次的曝光 toohello Azure 機器學習服務，您可以藉由使用中的 hello 範例取得簡介 tooit[如何 toocreate 第一個實驗](machine-learning/machine-learning-create-experiment.md)。

hello 下列各節將討論 hello 區段 hello 範本時，將需要修改引進新的資料集。

### <a name="azure-event-hub"></a>Azure 事件中樞
hello [Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)服務，非常一般化，這類資料發佈 toohello 中樞 CSV 或 JSON 格式。 進行任何特殊處理，就會發生在 hello Azure 事件中心，但請務必瞭解會送入的 hello 資料。

本文件並未說明如何 tooingest 您的資料，但有一位可以輕鬆地傳送事件或資料 tooan Azure 事件中心，使用 hello[事件中心 API](event-hubs/event-hubs-programming-guide.md)。

### <a name="azure-stream-analytics"></a>Azure 串流分析
hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)服務是使用的 tooprovide 接近即時的分析資料流讀取和輸出的來源資料 tooany 數目。

Hello Azure Stream Analytics 查詢 hello 需求預測能源解決方案範本，包含兩個的子查詢，每個耗用 hello Azure 事件中心服務做為輸入的事件，以及取得輸出 tootwo 不同位置。 這些輸出包含一個 Power BI 資料集和一個 Azure 儲存體位置。

hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)查詢即可找到：

* 登入 hello [Azure 管理入口網站](https://manage.windowsazure.com/)
* 找出 hello 資料流分析工作![](media/cortana-analytics-technical-guide-demand-forecast/icon-stream-analytics.png)hello 解決方案部署時所產生。 其中一個是將發送資料 tooblob 儲存體 (例如 mytest1streaming432822asablob)，及 hello 另一個是將發送資料 tooPower BI (例如 mytest1streaming432822asapbi)。
* 選取

  * ***輸入***tooview hello 查詢輸入
  * ***查詢***tooview hello 查詢本身
  * ***輸出***tooview hello 不同的輸出

Azure Stream Analytics 查詢建構的相關資訊位於 hello[串流分析查詢參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)MSDN 上。

在此解決方案中，hello Azure 串流分析工作輸出以接近即時的分析資訊 hello 內送資料流 tooa Power BI 儀表板的資料集提供做為此解決方案範本的一部分。 因為沒有隱含 hello 連入的資料格式的相關知識，這些查詢可能必須改變 toobe 根據您的資料格式。

hello 其他 Azure Stream Analytics 工作輸出所有[事件中心](https://azure.microsoft.com/services/event-hubs/)事件[Azure 儲存體](https://azure.microsoft.com/services/storage/)hello 完整事件資訊是串流，因此要求沒有改變，不論您的資料格式toostorage。

### <a name="azure-data-factory"></a>Azure Data Factory
hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)服務所協調 hello 移動和處理的資料。 在 hello 需求預測能源方案範本 hello 資料 factory 組成十二個[管線](data-factory/data-factory-create-pipelines.md)移動，而且處理 hello 資料使用各種技術。

  您可以開啟在 hello 解決方案範本圖表建立與 hello hello 方案部署的 hello 底部 hello Data Factory 節點，以存取您的 data factory。 這需要您 toohello 資料 factory 在 Azure 管理入口網站上。 如果您看到錯誤在您的資料集下，您可以忽略這些，因為這是因為 toodata factory hello 資料產生器啟動之前部署。 這些錯誤不會防止您的 Data Factory 運作。

本章節將討論 hello 必要[管線](data-factory/data-factory-create-pipelines.md)和[活動](data-factory/data-factory-create-pipelines.md)包含在 hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)。 以下是 hello 解決方案的 hello 圖表檢視。

![](media/cortana-analytics-technical-guide-demand-forecast/ADF2.png)

此處理站的 hello 管線的五個包含[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)使用的 toopartition 和彙總的 hello 資料的指令碼。 Hello 指令碼時所註明，將會位於 hello [Azure 儲存體](https://azure.microsoft.com/services/storage/)在安裝期間建立的帳戶。 其位置會是：demandforecasting\\\\script\\\\hive\\\\ (或 https://[解決方案名稱].blob.core.windows.net/demandforecasting)。

類似 toohello [Azure Stream Analytics](#azure-stream-analytics-1)查詢[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)指令碼有隱含 hello 連入的資料格式的相關知識，這些查詢將會需要更改 toobe 根據您的資料格式和[功能工程](machine-learning/machine-learning-feature-selection-and-engineering.md)需求。

#### <a name="aggregatedemanddatato1hrpipeline"></a>*AggregateDemandDataTo1HrPipeline*
這[管線](data-factory/data-factory-create-pipelines.md)管線包含單一活動- [HDInsightHive](data-factory/data-factory-hive-activity.md)活動使用[HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx)執行[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)指令碼 tooaggregate hello 每隔 10 秒鐘分站層級 toohourly 區域層級中的指定資料以資料流處理，並放入[Azure 儲存體](https://azure.microsoft.com/services/storage/)透過 hello Azure 串流分析工作。

此資料分割工作的 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 指令碼為 AggregateDemandRegion1Hr.hql

#### <a name="loadhistorydemanddatapipeline"></a>*LoadHistoryDemandDataPipeline*
這個[管線](data-factory/data-factory-create-pipelines.md)包含兩個活動︰

* [HDInsightHive](data-factory/data-factory-hive-activity.md)活動使用[HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx)執行 Hive 指令碼 tooaggregate hello 每小時歷程記錄需求分站層級 toohourly 區域層級中的資料和 hello Azure 期間放在 Azure 儲存體串流分析工作
* [複製](https://msdn.microsoft.com/library/azure/dn835035.aspx)從 Azure 儲存體 blob toohello hello 方案範本安裝過程所佈建的 Azure SQL Database 移 hello 的活動彙總的資料。

hello [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)編寫指令碼，這項工作是***AggregateDemandHistoryRegion.hql***。

#### <a name="mlscoringregionxpipeline"></a>*MLScoringRegionXPipeline*
這些[管線](data-factory/data-factory-create-pipelines.md)包含數個活動和其最終結果 hello 計分 hello Azure 機器學習實驗此解決方案範本相關聯的預測。 它們是幾乎完全相同，但它們只會處理 hello 不同區域而傳遞 hello ADF 管線和 hello hive 指令碼中的每個區域的不同 RegionID 正在進行。  
是包含在這個 hello 活動：

* [HDInsightHive](data-factory/data-factory-hive-activity.md)活動使用[HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx)執行 Hive 指令碼 tooperform 彙總，而功能所需的 hello Azure 機器學習實驗的工程團隊。 hello Hive 指令碼，這項工作是個別***PrepareMLInputRegionX.hql***。
* [複製](https://msdn.microsoft.com/library/azure/dn835035.aspx)從 hello 移動 hello 結果的活動[HDInsightHive](data-factory/data-factory-hive-activity.md)活動 tooa 單一 Azure 儲存體 blob 可存取的 hello [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx)活動。
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx)呼叫會導致 hello hello Azure 機器學習實驗的活動結果放入單一 Azure 儲存體 blob。

#### <a name="copyscoredresultregionxpipeline"></a>*CopyScoredResultRegionXPipeline*
這些[管線](data-factory/data-factory-create-pipelines.md)包含單一活動-[複製](https://msdn.microsoft.com/library/azure/dn835035.aspx)從各自的 hello 移動的 hello Azure 機器學習實驗的 hello 結果的活動***MLScoringRegionXPipeline*** toohello hello 方案範本安裝過程所佈建的 Azure SQL Database。

#### <a name="copyaggdemandpipeline"></a>*CopyAggDemandPipeline*
這[管線](data-factory/data-factory-create-pipelines.md)包含單一活動-[複製](https://msdn.microsoft.com/library/azure/dn835035.aspx)移動 hello 的活動彙總從進行中的指定資料***LoadHistoryDemandDataPipeline*** toohello Azure已佈建為 hello 方案範本安裝一部分的 SQL 資料庫。

#### <a name="copyregiondatapipeline-copysubstationdatapipeline-copytopologydatapipeline"></a>*CopyRegionDataPipeline、CopySubstationDataPipeline、CopyTopologyDataPipeline*
這些[管線](data-factory/data-factory-create-pipelines.md)包含單一活動-[複製](https://msdn.microsoft.com/library/azure/dn835035.aspx)活動會移動的區域/分站/Topologygeo hello 參考資料，會在上傳 tooAzure 儲存體 blob 的 hello 方案範本安裝 toohello hello 方案範本安裝過程所佈建的 Azure SQL Database。

### <a name="azure-machine-learning"></a>Azure Machine Learning
hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)嘗試使用此解決方案範本提供 hello 預測的區域的需求。 hello 實驗是特定 toohello 資料集取用，因而需要修改或取代在資料庫處於特定 toohello 資料。

## <a name="monitor-progress"></a>**監視進度**
一旦啟動 hello 資料產生器時，hello 管線開始 tooget hydrated 並 hello 不同方案的元件開始試用看成下列 hello 命令發出 hello Data Factory 的動作。 有兩種方式，您可以監視 hello 管線。

1. 請檢查 hello 資料從 Azure Blob 儲存體。

    Hello 資料流分析工作的其中一個寫入 hello 原始內送資料 tooblob 儲存體。 如果您按一下**Azure Blob 儲存體**hello 方案元件畫面上您已成功部署的 hello 方案，然後按一下**開啟**在 hello 右面板中，它會帶您 toohello [Azure 管理入口網站](https://portal.azure.com)。 到達那裡之後，按一下 [Blob]。 在 [hello 下一步] 面板中，您會看到容器的清單。 按一下 [energysadata]。 在 hello 下一步 面板中，您會看見 hello **"demandongoing"**資料夾。 在 hello rawdata 資料夾中，您會看到資料夾名稱，例如日期 = 2016年-01-28 等等。如果您看到這些資料夾時，就表示 hello 未經處理資料成功正在電腦上產生並儲存在 blob 儲存體。 您應該會在這些資料夾中看到具有有限大小 (MB) 的檔案。
2. 請檢查 hello 資料從 Azure SQL Database。

    hello 的 hello 管線的最後一個步驟是將 SQL Database 的 toowrite 資料 （例如從機器學習的預測）。 您可能 toowait 最多 2 小時的 hello 資料 tooappear SQL 資料庫中。 其中一種方式 toomonitor 多少資料均可在您的 SQL 資料庫是透過[Azure 管理入口網站](https://manage.windowsazure.com/)。 Hello 左面板上尋找 SQL 資料庫![](media/cortana-analytics-technical-guide-demand-forecast/SQLicon2.png)，然後按一下它。 然後找到您的資料庫 (亦即 demo123456db) 並且按一下它。 Hello 底下的下一個頁面**「 連線 tooyour 資料庫 」**區段中，按一下**"對 SQL database 執行 TRANSACT-SQL 查詢"**。

    在這裡，您可以按一下新的查詢和查詢之資料列 (例如"select count(*) 從 DemandRealHourly) hello 數目 」 您的資料庫成長時，hello hello 資料表中資料列數目應增加。）
3. 請檢查 hello 資料從 Power BI 儀表板。

    您可以設定 Power BI 最忙碌路徑 儀表板 toomonitor hello 未經處理內送資料。 請遵循 hello"Power BI 儀表板 」 一節中的 hello 指令。

## <a name="power-bi-dashboard"></a>**Power BI 儀表板**
### <a name="overview"></a>概觀
本節說明如何註冊 Power BI 儀表板 toovisualize tooset 即時資料從 Azure 串流分析 (hot path)，也為預測結果從 Azure 機器學習 （冷路徑）。

### <a name="setup-hot-path-dashboard"></a>設定最忙碌路徑儀表板
hello 下列步驟將引導您如何 toovisualize 即時資料從輸出資料流分析工作所產生的方案部署的 hello 時間。 A[線上 Power BI](http://www.powerbi.com/)帳戶是必要的 tooperform hello 下列步驟。 如果您沒有帳戶，您可以 [建立一個](https://powerbi.microsoft.com/pricing)。

1. 在 Azure 串流分析 (ASA) 中加入 Power BI 輸出。

   * 您必須在 toofollow hello 指示[Azure Stream Analytics 與 Power BI： 即時串流資料的可見性的即時分析儀表板](stream-analytics/stream-analytics-power-bi-dashboard.md)tooset 向上 hello 做為您的 Power Azure 串流分析工作輸出BI 的儀表板。
   * 找出 hello 串流分析工作，在您[Azure 管理入口網站](https://manage.windowsazure.com)。 hello hello 作業名稱應該是： YourSolutionName +"streamingjob"+ 隨機數字 +"asapbi 」 (也就是 demostreamingjob123456asapbi)。
   * 新增 hello ASA 工作之 power Bi 輸出。 設定 hello**輸出別名**為**'PBIoutput'**。 將 [資料集名稱] 和 [資料表名稱] 命名為 **‘EnergyStreamData’**。 一旦您加入 hello 輸出，按一下**"Start"**底部 hello hello 頁面 toostart hello 資料流分析工作。 您應該會收到確認訊息 (例如，「串流分析作業 myteststreamingjob12345asablob 啟動成功」)。
2. 登入太[線上 Power BI](http://www.powerbi.com)

   * 在左面板資料集在我的工作區中的 hello，您應該能夠 toosee 新的資料集顯示 hello 的 Power BI 的左面板上。 這是資料流處理的資料，您從 Azure Stream Analytics 推入 hello 上一個步驟中的 hello。
   * 請確定 hello***視覺效果***窗格開啟並顯示 hello 螢幕的右側。
3. 建立的 hello 」 要求的時間戳記 」 磚：

   * 按一下 資料集**'EnergyStreamData'** hello 左面板資料集上。
   * 按一下 [折線圖] 圖示 ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic8.png)。
   * 按一下 [欄位]  面板中的 ’EnergyStreamData’。
   * 按一下 [時間戳記]  ，並確定它顯示在 [座標軸] 底下。 按一下 [載入]  ，並確定它顯示在 [值] 底下。
   * 按一下**儲存**hello 頂端且名稱為"EnergyStreamDataReport"hello 報表。 名為"EnergyStreamDataReport"hello 報表會顯示 hello 左側導覽窗格中的 [報表] 區段中。
   * 按一下**"釘選視覺"** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png)上這個折線圖右上角的圖示，"Pin tooDashboard 」 視窗可能會顯示您 toochoose 的儀表板。 請選取 [EnergyStreamDataReport]，然後按一下 [釘選]。
   * 將滑鼠停留在這個 hello 儀表板上的磚，按一下 [編輯] 圖示上右上角 toochange 」 要求的時間戳記 」 為標題的 hello 滑鼠
4. 根據適當的資料集建立其他儀表板圖格。 hello 最終儀表板檢視顯示如下。
     ![](media/cortana-analytics-technical-guide-demand-forecast/PBIFullScreen.png)

### <a name="setup-cold-path-dashboard"></a>設定冷路徑儀表板
在原始路徑資料管線中，hello 重要目標是 tooget hello 指定預測的每個區域。 Power BI 可連接 tooan Azure SQL database 當做其資料來源，hello 預測結果的儲存位置。

> [!NOTE]
> 1) 它會採用幾小時 toocollect hello 儀表板的足夠預測的結果。 我們建議您在開始此程序 2-3 個小時之後午餐 hello 資料產生器。 2） 請在此步驟中，hello 先決條件是 toodownload 並安裝 hello 免費軟體[Power BI desktop](https://powerbi.microsoft.com/desktop)。
>
>

1. 收到 hello 資料庫認證。

   您將需要**資料庫伺服器名稱、 資料庫名稱、 使用者名稱和密碼**日前 toonext 步驟。 以下是 hello 步驟 tooguide 您如何 toofind 它們。

   * 一旦您的解決方案範本圖表上的 Azure SQL Database 變成綠色，請按一下它，然後按一下開啟。 您將會引導式的 tooAzure 管理入口網站，也將會開啟您的資料庫資訊 頁面。
   * 在 [hello] 頁面上，您可以找到 「 資料庫 」 一節。 它會列出出 hello 您已建立的資料庫。 hello 您資料庫的名稱應該是**"您的方案名稱 + 隨機數字 + 'db'"** (例如"mytest12345db")。
   * 按一下您的資料庫，在新顯面板，您可以找到您的資料庫伺服器名稱 hello 最上層顯示 hello。 您的資料庫伺服器名稱應該是**「您的解決方案名稱 + 隨機數字 + 'database.windows.net,1433'」** (例如 "mytest12345.database.windows.net,1433")。
   * 您的資料庫**username**和**密碼**hello 相同 hello 使用者名稱和密碼先前記錄的期間 hello 方案的部署。
2. 更新 hello 資料來源的 hello 冷路徑的 Power BI 檔案

   * 請確定您已安裝新版的 hello [Power BI desktop](https://powerbi.microsoft.com/desktop)。
   * 在 hello **"DemandForecastingDataGeneratorv1.0"**下載資料夾中，按兩下 hello **' Power BI Template\DemandForecastPowerBI.pbix'**檔案。 hello 初始視覺效果根據虛擬資料。 **注意：**如果您看到錯誤處理，請確定您已安裝的 Power BI Desktop 的 hello 最新版本。

     一旦您開啟時，在 hello hello 檔案的頂端，按一下 **編輯查詢**。 在 hello 顯視窗中，按兩下**'Source'** hello 右面板上。
     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic1.png)
   * 在 hello 快顯視窗，以取代**"Server"**和**「 資料庫 」**與您自己的伺服器和資料庫名稱，然後按一下**確定**。 伺服器名稱，請確定您指定 hello 通訊埠 1433年 (**YourSolutionName.database.windows.net，1433年**)。 忽略 hello 囉 」 畫面出現的警告訊息。
   * 在 hello 下一步 快顯視窗，您會看見 hello 左窗格中的兩個選項 (**Windows**和**資料庫**)。 按一下**「 資料庫 」**，填寫您**"Username"**和**「 密碼 」** (這是 hello 使用者名稱和您初次部署 hello 方案，並建立時，您輸入的密碼Azure SQL database)。 在***選取的層級 tooapply 這些設定***，請檢查資料庫層級的選項。 然後按一下 [連接] 。
   * 一旦您引導式回復 toohello 前一個頁面上，關閉 hello 視窗。 訊息將會蹦現 - 按一下 [套用] 。 最後，按一下 hello**儲存**按鈕 toosave hello 變更。 您的 Power BI 檔案現在已建立連線 toohello 伺服器。 如果視覺效果都是空的請確定清除 hello hello 視覺效果 toovisualize 的選取範圍 hello 的所有資料，即可在 hello 右上角的 hello 圖例 hello 橡皮擦圖示。 在 hello 視覺效果上使用 hello 重新整理按鈕 tooreflect 新資料。 一開始，您只會看到 hello 種子資料視覺效果上為 hello data factory 是排程的 toorefresh 每 3 個小時。 3 小時後，您會看到新的預測，當您重新整理 hello 資料視覺效果中反映。
3. （選擇性）發行 hello 冷路徑儀表板太[線上 Power BI](http://www.powerbi.com/)。 請注意，這個步驟需要 Power BI 帳戶 (或 Office 365 帳戶)。

   * 按一下**[發佈]**和幾秒鐘後一個視窗隨即出現，顯示的 < 發行 tooPower BI 成功 ！ 」 並帶有綠色核取記號。 按一下 「 Power BI 中開啟 demoprediction.pbix"下方的 hello 連結。 toofind 詳細指示，請參閱[從 Power BI Desktop 發佈](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop)。
   * toocreate 新儀表板： 按一下 hello  **+** 登入 下一步 toothe**儀表板**hello 左窗格上的一節。 輸入此新的儀表板的 hello 名稱"要求預測 Demo"。
   * 一旦您開啟 hello 報表，請按一下![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png)toopin 所有視覺效果 tooyour 儀表板。 toofind 詳細指示，請參閱[釘選的磚 tooa Power BI 儀表板報表](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report)。
     移至 toohello 儀表板頁面和調整 hello 大小和位置的視覺效果，然後編輯其標題。 toofind 詳細指示如何 tooedit 您的磚，請參閱[編輯圖格： 調整大小、 移動、 重新命名、 釘選、 刪除、 加入超連結](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename)。 以下是一些冷路徑的視覺效果釘選 tooit 範例儀表板。

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic7.png)
4. （選擇性）Hello 資料來源的排程重新整理。

   * tooschedule 資料重新整理的 hello，將滑鼠停留 hello **EnergyBPI 最終**資料集，按一下  ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic3.png) ，然後選擇 **排程重新整理**。
     **注意：**如果您看到警告操作，按一下 **編輯認證**，並確定您的資料庫認證是 hello 相同的步驟 1 中所述。

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic4.png)
   * 展開 hello**排程重新整理**> 一節。 開啟「將您的資料保持最新」。
   * 根據您的需求排程 hello 重新整理。 toofind 的詳細資訊，請參閱[Power BI 的資料重新整理](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)。

## <a name="how-toodelete-your-solution"></a>**如何 toodelete 方案**
請確定未主動使用 hello 方案，因為執行 hello 資料產生器將會造成較高的成本時，停止 hello 資料產生器。 請如果您不使用它，刪除 hello 方案。 刪除您的方案將會刪除所有部署 hello 方案時，您的訂用帳戶中佈建的 hello 元件。 toodelete hello 方案 hello 的 hello 解決方案範本的左窗格中您方案的名稱上按一下，然後按一下 刪除。

## <a name="cost-estimation-tools"></a>**成本估計工具**
hello 下列兩個工具是可用 toohelp 深入了解所涉及執行 hello 需求預測能源解決方案範本，您的訂用帳戶中的總成本：

* [Microsoft Azure Cost Estimator Tool (線上版)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure Cost Estimator Tool (桌面版)](http://www.microsoft.com/download/details.aspx?id=43376)

## <a name="acknowledgements"></a>**通知**
本文是 Microsoft 的資料科學家 Yijing Chen 與軟體工程師 Qiu Min 所撰寫。
