---
title: "在與 Azure-Cortana 智慧方案的技術指南太空 aaaPredictive 維護 |Microsoft 文件"
description: "預測中對於維護太空、 公用程式及傳輸技術指南 toohello Intelligence< Cortana 方案範本。"
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2c4d2147-0f05-4705-8748-9527c2c1f033
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: 30ddc1c101007546ae1b303bccebae3ecdacb442
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>預測性維護太空和其他企業中的技術指南 toohello Cortana 智慧方案範本

## <a name="important"></a>**重要**
此文章已被取代。 hello 資訊仍與 toohello 手邊問題，也就是預測性維護中太空，但是可以找到 hello 最新文件以 hello 最總 toodate 資訊[這裡](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace)。 

## <a name="acknowledgements"></a>**通知**
本文是由 Microsoft 的資料科學家 Yan Zhang、Gauher Shaheen、Fidan Boylu Uz 和軟體工程師 Dan Grecoe 所共同撰寫。

## <a name="overview"></a>**概觀**
設計解決方案範本 tooaccelerate hello 建置程序在 Cortana 智慧套件之上 E2E 示範。 已部署的範本將會佈建必要 Cortana 智慧元件是與您訂用帳戶，並建置 hello 兩者間的關聯性。 它也會從您下載及部署 hello 方案範本後更新在本機電腦上的資料產生器應用程式所產生的範例資料設 hello 資料管線。 hello hello 產生器所產生的資料將會產生 hello 資料管線，並產生然後 hello Power BI 儀表板上要視覺化的機器學習預測。 hello 部署程序將引導您完成幾個步驟 tooset 方案認證。 請確定記錄例如方案名稱、 使用者名稱和密碼 hello 部署時提供這些認證。  

這份文件 hello 目標是 tooexplain hello 參考架構和佈建您的訂用帳戶，做為此解決方案範本的一部分中的不同元件。 hello 文件也會示範如何 tooreplace toobe 無法 toosee insights 和從您自己的資料預測的實際資料的範例資料。 此外，hello 文件討論 hello 需要 toobe，如果您想 toocustomize hello 方案與您自己的資料修改的方案範本的組件。 Hello 結尾會提供如何 toobuild hello 此解決方案範本的 Power BI 儀表板上的指示。

> [!TIP]
> 您可以下載及列印 [這份文件的 PDF 版本](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf)。
> 
> 

## <a name="big-picture"></a>**概觀**
![預測性維護架構](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

部署 hello 方案時，會啟動 Cortana Analytics suite 這套內各種 Azure 服務 (*也就是*事件中樞、串流分析、HDInsight、Data Factory、機器學習服務等)。 hello 架構圖上面所示，在高的層級，hello 航太方案範本的預測性維護從端對端的建構方式。 您將這些服務建立的 HDInsight 的 hello 例外，因為這個服務的 hello 部署的 hello 方案 hello 方案範本圖表上按一下這些 hello azure 入口網站中已佈建視 hello 相關時無法 tooinvestigate管線的活動是必要的 toorun，而且之後刪除。
您可以下載[hello 圖表的完整大小版本](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png)。

hello 下列各節說明每個片段。

## <a name="data-source-and-ingestion"></a>**資料來源及擷取**
### <a name="synthetic-data-source"></a>綜合資料來源
此範本 hello 資料使用來源會產生從桌面應用程式，您將會下載並成功部署之後在本機執行。 您會尋找 hello 指示 toodownload 並安裝此應用程式在 hello 屬性列中，當您選取 hello hello 解決方案範本圖表上呼叫預測維護資料產生器的第一個節點。 此應用程式摘要 hello [Azure 事件中心](#azure-event-hub)服務與資料點或將使用在 hello 方案流程 hello 其餘部分的事件。 此資料來源是組成或衍生自公開可用的資料，從[NASA 資料儲存機制](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/)使用 hello [Turbofan 引擎降低模擬資料集](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan)。

只有當它在您的電腦上執行時，才 hello 事件產生應用程式將會填入 hello Azure 事件中心。

### <a name="azure-event-hub"></a>Azure 事件中樞
hello [Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)服務是 hello 收件者的 hello hello 綜合上面所述的資料來源所提供的輸入。

## <a name="data-preparation-and-analysis"></a>**資料準備和分析**
### <a name="azure-stream-analytics"></a>Azure 串流分析
hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)服務已接近即時的分析 hello hello 從輸入資料流上使用的 tooprovide [Azure 事件中心](#azure-event-hub)服務並發行到結果[Power BI](https://powerbi.microsoft.com)儀表板，以及保存所有未經處理的內送事件 toohello [Azure 儲存體](https://azure.microsoft.com/services/storage/)服務以便之後處理 hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)服務。

### <a name="hd-insights-custom-aggregation"></a>HD Insights 自訂彙總
hello Azure HD Insight 服務是使用的 toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) hello 未經處理的事件上使用 hello Azure Stream Analytics 服務已封存的指令碼 （由 Azure Data Factory 協調） tooprovide 彙總。

### <a name="azure-machine-learning"></a>Azure Machine Learning
hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) （由 Azure Data Factory 協調） 來使用服務上剩餘的生命週期 (RUL) 提供收到 hello 輸入特定飛機引擎 hello toomake 預測。

## <a name="data-publishing"></a>**資料發佈**
### <a name="azure-sql-database-service"></a>Azure SQL Database 服務
hello [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)服務已收到 hello Azure 機器學習服務將會用在 hello （由 Azure Data Factory） 使用的 toostore hello 預測[Power BI](https://powerbi.microsoft.com)儀表板。

## <a name="data-consumption"></a>**資料耗用量**
### <a name="power-bi"></a>Power BI
hello [Power BI](https://powerbi.microsoft.com)服務是使用的 tooshow 包含彙總與警示 hello 所提供的儀表板[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)服務以及儲存在 RUL 預測[Azure SQL資料庫](https://azure.microsoft.com/services/sql-database/)，產生使用 hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)服務。 如需有關如何 toobuild hello Power BI 儀表板此解決方案範本的指示，請參閱 toohello 一節。

## <a name="how-toobring-in-your-own-data"></a>**如何在您自己的資料 toobring**
本章節描述如何 toobring 您自己的資料 tooAzure，和區域會需要變更 hello 資料帶入這個架構。

也不太可能，您將任何資料集符合使用 hello hello 資料集[Turbofan 引擎降低模擬資料集](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan)用於此解決方案範本。 了解您的資料和需求將會是非常重要的是您如何修改此範本 toowork 與您自己的資料。 如果這是您第一次的曝光 toohello Azure 機器學習服務，您可以藉由使用中的 hello 範例取得簡介 tooit[如何 toocreate 第一個實驗](machine-learning-create-experiment.md)。

hello 下列各節將討論 hello 區段 hello 範本時，將需要修改引進新的資料集。

### <a name="azure-event-hub"></a>Azure 事件中樞
hello Azure 事件中心服務，非常一般化，這類資料發佈 toohello 中樞 CSV 或 JSON 格式。 Hello Azure 事件中心，但請務必了解會送入的 hello 資料中不發生任何特殊處理。

本文件並未說明如何 tooingest 您的資料，但是您可以輕鬆地傳送事件，或使用 Azure 事件中心資料 tooan hello 事件中心 API 的。

### <a name="azure-stream-analytics"></a>Azure 串流分析
hello Azure Stream Analytics 服務是使用的 tooprovide 接近即時的分析資料流讀取和輸出的來源資料 tooany 數目。

Azure Stream Analytics 查詢 hello 預測性維護航太解決方案範本，包含四個子查詢，每個取用事件 hello Azure 事件中心服務和輸出不必四個不同的位置。 這些輸出包含三個 Power BI 資料集和一個 Azure 儲存體位置。

可以找到 hello Azure Stream Analytics 查詢：

* 登入 hello Azure 入口網站
* 找出 hello 串流分析工作![Stream Analytics 圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png)hello 解決方案部署時，產生 (*例如*， **maintenancesa02asapbi**和**maintenancesa02asablob**預測性維護方案)
* 選取
  
  * ***輸入***tooview hello 查詢輸入
  * ***查詢***tooview hello 查詢本身
  * ***輸出***tooview hello 不同的輸出

Azure Stream Analytics 查詢建構的相關資訊位於 hello[串流分析查詢參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)MSDN 上。

在此解決方案中，hello 查詢輸出三個的資料集以接近即時的分析資訊 hello 內送資料流 tooa Power BI 儀表板提供做為此解決方案範本的一部分。 因為沒有隱含 hello 連入的資料格式的相關知識，這些查詢可能必須改變 toobe 根據您的資料格式。

hello 第二個資料流分析作業中的 hello 查詢**maintenancesa02asablob**只會輸出所有[事件中心](https://azure.microsoft.com/services/event-hubs/)事件[Azure 儲存體](https://azure.microsoft.com/services/storage/)，因此需要無改變不論您的資料格式為 hello 串流 toostorage 完整事件資訊。

### <a name="azure-data-factory"></a>Azure Data Factory
hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)服務所協調 hello 移動和處理的資料。 在預測航太方案範本 hello 資料維護處理站由三個[管線](../data-factory/data-factory-create-pipelines.md)移動，而且處理 hello 資料使用各種技術。  您可以開啟在 hello 解決方案範本圖表建立與 hello hello 方案部署的 hello 底部 hello hello Data Factory 的節點，以存取您的 data factory。 這需要您 toohello 資料處理站在 Azure 入口網站。 如果您看到錯誤在您的資料集下，您可以忽略這些，因為這是因為 toodata factory hello 資料產生器啟動之前部署。 這些錯誤不會防止您的 Data Factory 運作。

![Data Factory 資料集錯誤](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

本章節將討論 hello 必要[管線](../data-factory/data-factory-create-pipelines.md)和[活動](../data-factory/data-factory-create-pipelines.md)包含在 hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)。 以下是 hello 解決方案的 hello 圖表檢視。

![Azure Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

此處理站的 hello 管線的兩個包含[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)使用的 toopartition 和彙總的 hello 資料的指令碼。 Hello 指令碼時所註明，將會位於 hello [Azure 儲存體](https://azure.microsoft.com/services/storage/)在安裝期間建立的帳戶。 其位置會是：maintenancesascript\\\\script\\\\hive\\\\ (或 https://[您的解決方案名稱].blob.core.windows.net/maintenancesascript)。

類似 toohello [Azure Stream Analytics](#azure-stream-analytics-1)查詢[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)指令碼有隱含 hello 連入的資料格式的相關知識，這些查詢將會需要更改 toobe 根據您的資料格式和[功能工程](machine-learning-feature-selection-and-engineering.md)需求。

#### <a name="aggregateflightinfopipeline"></a><bpt id="p1">*</bpt>AggregateFlightInfoPipeline<ept id="p1">*</ept>
這[管線](../data-factory/data-factory-create-pipelines.md)包含單一活動- [HDInsightHive](../data-factory/data-factory-hive-activity.md)活動使用[HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx)執行[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)指令碼 toopartition hello 資料放入[Azure 儲存體](https://azure.microsoft.com/services/storage/)期間[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)作業。

此資料分割工作的 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 指令碼為 ***AggregateFlightInfo.hql***

#### <a name="mlscoringpipeline"></a><bpt id="p1">*</bpt>MLScoringPipeline<ept id="p1">*</ept>
這[管線](../data-factory/data-factory-create-pipelines.md)包含數個活動和其最終結果是從 hello hello 計分預測[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)實驗此解決方案範本相關聯。

是包含在這個 hello 活動：

* [HDInsightHive](../data-factory/data-factory-hive-activity.md)活動使用[HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx)執行[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) tooperform 彙總的指令碼和功能所需的 hello 工程[Azure機器學習](https://azure.microsoft.com/services/machine-learning/)實驗。
  此資料分割工作的 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 指令碼是 ***PrepareMLInput.hql***。
* [複製](https://msdn.microsoft.com/library/azure/dn835035.aspx)移動 hello 結果的活動[HDInsightHive](../data-factory/data-factory-hive-activity.md)單一活動 tooa [Azure 儲存體](https://azure.microsoft.com/services/storage/)可以存取的 blob [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx)活動。
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx)活動呼叫 hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)實驗會導致 hello 結果放入單一[Azure 儲存體](https://azure.microsoft.com/services/storage/)blob。

#### <a name="copyscoredresultpipeline"></a><bpt id="p1">*</bpt>CopyScoredResultPipeline<ept id="p1">*</ept>
這[管線](../data-factory/data-factory-create-pipelines.md)包含單一活動-[複製](https://msdn.microsoft.com/library/azure/dn835035.aspx)移動 hello hello 結果的活動[Azure Machine Learning](#azure-machine-learning)實驗從***MLScoringPipeline*** toohello [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) ，佈建的方案範本安裝的一部分。

### <a name="azure-machine-learning"></a>Azure Machine Learning
hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)項實驗中使用此解決方案範本提供 hello 剩餘有用生命 (RUL) 的飛機引擎。 hello 實驗是特定 toohello 資料集取用，因而需要修改或取代在資料庫處於特定 toohello 資料。

Hello Azure 機器學習實驗的建立方式的相關資訊，請參閱[預測性維護： 步驟 1，3，資料準備和特徵設計的](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2)。

## <a name="monitor-progress"></a>**監視進度**
 一旦啟動 hello 資料產生器時，hello 管線開始 tooget hydrated 並 hello 不同方案的元件開始試用看成下列 hello 命令發出 hello Data Factory 的動作。 有兩種方式，您可以監視 hello 管線。

1. Hello 資料流分析工作的其中一個寫入 hello 原始內送資料 tooblob 儲存體。 如果您按一下 Blob 儲存體元件，您的方案從囉 」 畫面上。 您已成功部署的 hello 方案並 hello 右面板中，然後按一下開啟時，它會帶您 toohello[管理入口網站](https://portal.azure.com/)。 一旦在該網站中，按一下 Blobs。 在 [hello 下一步] 面板中，您會看到容器的清單。 按一下 [maintenancesadata]。 在 hello 下一步 面板中，您會看見 hello **rawdata**資料夾。 在 hello rawdata 資料夾中，您會看到資料夾名稱，例如小時 = 17，小時 = 18 等等。如果您看到這些資料夾時，就表示 hello 未經處理資料成功正在電腦上產生並儲存在 blob 儲存體。 您應該會在這些資料夾中看到具有有限大小 (MB) 的 csv 檔案。
2. hello 的 hello 管線的最後一個步驟是將 SQL Database 的 toowrite 資料 （例如從機器學習的預測）。 您可能必須 toowait hello 資料 tooappear 三個小時的最大值，SQL 資料庫中。 其中一種方式 toomonitor 多少資料均可在您的 SQL 資料庫是透過[azure 入口網站](https://manage.windowsazure.com/)。Hello 左面板上尋找 SQL 資料庫![SQL 圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png)，然後按一下它。 接著找到您的資料庫 **pmaintenancedb** 並按一下它。 Hello hello 底部的下一個頁面，按一下 管理
   
    ![管理圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png).
   
    在這裡，您可以按一下新的查詢和查詢之資料列 (例如從 PMResult 選取 count(*)) hello 數目。 隨著您的資料庫時，應增加 hello hello 資料表中資料列數目。

## <a name="power-bi-dashboard"></a>**Power BI 儀表板**
### <a name="overview"></a>概觀
本節說明如何註冊 Power BI 儀表板 toovisualize tooset 即時資料從 Azure Stream Analytics （最忙碌路徑），以及批次預測結果從 Azure 機器學習 （冷路徑）。

### <a name="setup-cold-path-dashboard"></a>安裝程式冷路徑儀表板
在 hello 冷路徑資料管線，hello 基本目標是 tooget 每一個飛機引擎預測 RUL （剩餘有用的生命週期） 之後完成的班機 （循環）。 hello 預測結果更新的預測 hello 飛機引擎已完成的班機期間 hello 過去 3 小時內每 3 個小時。

Power BI 可連接 tooan Azure SQL database 當做其資料來源，會儲存預測結果的位置。 注意： 1） 在部署您的方案，實際的預測會顯示在 hello 資料庫 3 小時內。
hello 產生器下載隨附 hello pbix 檔案包含某些種子資料，因此您可以立即建立 hello Power BI 儀表板。 2） 請在此步驟中，hello 先決條件是 toodownload 並安裝 hello 免費軟體[Power BI desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)。

hello 下列步驟將引導您在 tooconnect hello pbix 檔案 hello 開始時包含資料的方案部署的 hello 的 SQL Database (*例如*。 預測結果) 時加快運轉。

1. 收到 hello 資料庫認證。
   
   您將需要**資料庫伺服器名稱、 資料庫名稱、 使用者名稱和密碼**日前 toonext 步驟。 以下是 hello 步驟 tooguide 您如何 toofind 它們。
   
   * 一旦您的解決方案範本圖表上的 Azure SQL Database 變成綠色之後，請按一下它，然後按一下開啟。
   * 您會看到新的瀏覽器索引標籤/視窗，其中會顯示 hello Azure 入口網站頁面。 按一下**'資源群組'** hello 左面板上。
   * 選取您所使用的 hello 方案部署的 hello 訂用帳戶，然後選取**' YourSolutionName\_ResourceGroup'**。
   * 在 hello 新快顯面板，按一下 hello ![SQL 圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png)圖示 tooaccess 您的資料庫。 您的資料庫名稱是 [下一步 toohello 這個圖示 (*例如*， **'pmaintenancedb'**)，和 hello**資料庫伺服器名稱**列在 hello 伺服器名稱] 屬性，看起來應該類似太**YourSoutionName.database.windows.net**。
   * 您的資料庫**username**和**密碼**hello 相同 hello 使用者名稱和密碼先前記錄的期間 hello 方案的部署。
2. 使用 Power BI Desktop 更新 hello hello 冷路徑報表檔案資料來源。
   
   * 在您的電腦下載並解壓縮的產生器檔案的位置上 hello 資料夾中，按兩下**PowerBI\\PredictiveMaintenanceAerospace.pbix**檔案。 如果您開啟 hello 檔案時，您會看到警告訊息，請忽略這些訊息。 在 hello hello 檔案頂端，按一下 **編輯查詢**。
     
     ![編輯查詢](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * 您會看到兩個資料表，**RemainingUsefulLife** 和 **PMResult**。 選取 hello 第一個資料表，然後按一下![查詢設定 圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png)下一步太**'Source'**下**套用步驟**上 hello 右**[查詢設定]**面板。 略過任何出現的警告訊息。
   * 在 hello 快顯視窗，以取代**'Server'**和**'Database'**與您自己的伺服器和資料庫名稱，然後按一下**「 確定 」**。 伺服器名稱，請確定您指定 hello 通訊埠 1433年 (**YourSoutionName.database.windows.net，1433年**)。 保留為 hello 資料庫欄位**pmaintenancedb**。 忽略 hello 囉 」 畫面出現的警告訊息。
   * 在 hello 下一步 快顯視窗，您會看見 hello 左窗格中的兩個選項 (**Windows**和**資料庫**)。 按一下**'Database'**，填寫您**'Username'**和**'Password'** (這是 hello 使用者名稱和您初次部署 hello 方案，並建立時，您輸入的密碼Azure SQL database)。 在***選取的層級 tooapply 這些設定***，請檢查資料庫層級的選項。 然後按一下 [連接]。
   * 按一下 hello 第二個資料表**PMResult**然後按一下 ![瀏覽圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png)下一步太**'Source'**下**套用步驟**hello 右上**[查詢設定]**面板，並更新 hello 伺服器和資料庫名稱，例如 hello 上述步驟，然後按一下 [確定]。
   * 一旦您引導式回復 toohello 前一個頁面上，關閉 hello 視窗。 訊息將會蹦現 - 按一下 [套用] 。 最後，按一下 hello**儲存**按鈕 toosave hello 變更。 您的 Power BI 檔案現在已建立連線 toohello 伺服器。 如果視覺效果都是空的請確定清除 hello hello 視覺效果 toovisualize 的選取範圍 hello 的所有資料，即可在 hello 右上角的 hello 圖例 hello 橡皮擦圖示。 在 hello 視覺效果上使用 hello 重新整理按鈕 tooreflect 新資料。 一開始，您只會看到 hello 種子資料視覺效果上為 hello data factory 是排程的 toorefresh 每 3 個小時。 3 小時後，您會看到新的預測，當您重新整理 hello 資料視覺效果中反映。
3. （選擇性）發行 hello 冷路徑儀表板太[線上 Power BI](http://www.powerbi.com/)。 請注意，這個步驟需要 Power BI 帳戶 (或 Office 365 帳戶)。
   
   * 按一下**'發行'**和幾秒鐘後一個視窗隨即出現，顯示的 < 發行 tooPower BI 成功 ！ 」 並帶有綠色核取記號。 按一下下方"開啟 PredictiveMaintenanceAerospace.pbix 在 Power BI"的 hello 連結。 toofind 詳細指示，請參閱[從 Power BI Desktop 發佈](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop)。
   * toocreate 新儀表板： 按一下 hello  **+** 登入 下一步 toothe**儀表板**hello 左窗格上的一節。 輸入此新的儀表板的 hello 名稱"預測維護 Demo"。
   * 一旦您開啟 hello 報表，請按一下![釘選圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png)toopin 所有視覺效果 tooyour 儀表板。 toofind 詳細指示，請參閱[釘選的磚 tooa Power BI 儀表板報表](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report)。
     移至 toohello 儀表板頁面和調整 hello 大小和位置的視覺效果，然後編輯其標題。 toofind 詳細指示如何 tooedit 您的磚，請參閱[編輯圖格： 調整大小、 移動、 重新命名、 釘選、 刪除、 加入超連結](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename)。 以下是一些冷路徑的視覺效果釘選 tooit 範例儀表板。  根據時間長度，您會執行您的資料產生器，您在 hello 視覺效果上的數字可能會不同。
     <br/>
     ![最終檢視](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * tooschedule 資料重新整理的 hello，將滑鼠停留 hello **PredictiveMaintenanceAerospace**資料集，按一下 ![省略符號圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png)，然後選擇 **排程重新整理**。
     <br/>
     **注意：**如果您看到警告操作，按一下 **編輯認證**，並確定您的資料庫認證是 hello 相同的步驟 1 中所述。
     <br/>
     ![排程重新整理](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * 展開 hello**排程重新整理**> 一節。 開啟「將您的資料保持最新」。
     <br/>
   * 根據您的需求排程 hello 重新整理。 toofind 的詳細資訊，請參閱[Power BI 的資料重新整理](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi)。

### <a name="setup-hot-path-dashboard"></a>安裝程式最忙碌路徑儀表板
hello 下列步驟將引導您如何 toovisualize 即時資料從輸出資料流分析工作所產生的方案部署的 hello 時間。 A[線上 Power BI](http://www.powerbi.com/)帳戶是必要的 tooperform hello 下列步驟。 如果您沒有帳戶，您可以 [建立一個](https://powerbi.microsoft.com/pricing)。

1. 在 Azure 串流分析 (ASA) 中加入 Power BI 輸出。
   
   * 您必須在 toofollow hello 指示[Azure Stream Analytics 與 Power BI： 即時串流資料的可見性的即時分析儀表板](../stream-analytics/stream-analytics-power-bi-dashboard.md)tooset 向上 hello 做為您的 Power Azure 串流分析工作輸出BI 的儀表板。
   * hello ASA 查詢有三種輸出，也就是**aircraftmonitor**， **aircraftalert**，和**flightsbyhour**。 您可以按一下 [查詢] 索引標籤上檢視 hello 查詢。對應 tooeach 的這些資料表中，則需要 tooadd 輸出 tooASA。 當您將加入 hello 第一個輸出 (*例如* **aircraftmonitor**) 請確定 hello**輸出別名**，**資料集名稱**和**資料表名稱**hello 相同 (**aircraftmonitor**)。 重複的 hello 步驟 tooadd 輸出**aircraftalert**，和**flightsbyhour**。 一旦加入所有三個輸出資料表並啟動 hello ASA 工作，您應該會收到確認訊息 (*例如*，「 正在開始串流分析工作 maintenancesa02asapbi 成功 」)。
2. 登入太[線上 Power BI](http://www.powerbi.com)
   
   * 在左面板資料集在我的工作區中的 hello***資料集***名稱**aircraftmonitor**， **aircraftalert**，和**flightsbyhour**應該會出現。這是資料流處理的資料集中 hello 先前 step.hello 推入從 Azure Stream Analytics hello **flightsbyhour**可能不會顯示 hello 在相同的時間 hello toohello 性質背後的 hello SQL 查詢因為其他兩個資料集它。 不過，它應該會在一個小時之後出現。
   * 請確定 hello***視覺效果***窗格開啟並顯示 hello 螢幕的右側。
3. 一旦您擁有 hello 資料傳輸到 Power BI，您可以啟動視覺化 hello 串流資料。 以下是一些最忙碌路徑視覺效果的範例儀表板釘選 tooit。 您可以根據適當的資料集建立其他儀表板磚。 根據時間長度，您會執行您的資料產生器，您在 hello 視覺效果上的數字可能會不同。

    ![儀表板檢視](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. 以下是一些步驟 toocreate 上述 – hello 磚的其中一個 hello 」 船隊感應器 11 vs 的檢視。閾值 48.26 的機隊檢視」磚：
   
   * 按一下 資料集**aircraftmonitor** hello 左面板資料集上。
   * 按一下 hello**折線圖**圖示。
   * 按一下**處理**在 hello**欄位**hello 中，就會顯示"座標軸 」 底下的窗格**視覺效果**窗格。
   * 按一下 "s11" 和 "s11\_alert"，使它們都出現在「值」下方。 按一下 hello 的小箭號旁太**s11**和**s11\_警示**，變更 「 總和 」 太 「 平均數的 」。
   * 按一下**儲存**hello 頂端且命名為"aircraftmonitor"hello 報表。 名為"aircraftmonitor 」 報表會顯示 hello**報表**> 一節中 hello**導覽**hello 左側窗格。
   * 按一下 hello**釘選視覺**hello 右上角的這個折線圖上的圖示。 為您選擇儀表板可能會顯示"Pin tooDashboard 」 視窗。 選取 [預測性維護示範]，然後按一下 [釘選]。
   * Hello 滑鼠停留在 hello 儀表板磚中，按一下 太 hello"edit"hello 右上角 toochange 圖示標題 < 的感應器 11 以及檢視與比較。閾值 48.26 」 和副標題太 「 平均數跨以及經過一段時間 」。

## <a name="how-toodelete-your-solution"></a>**如何 toodelete 方案**
請確定未主動使用 hello 方案，因為執行 hello 資料產生器將會造成較高的成本時，停止 hello 資料產生器。 請如果您不使用它，刪除 hello 方案。 刪除您的方案將會刪除所有部署 hello 方案時，您的訂用帳戶中佈建的 hello 元件。 toodelete hello 方案 hello 的 hello 解決方案範本的左窗格中您方案的名稱上按一下，然後按一下 刪除。

## <a name="cost-estimation-tools"></a>**成本估計工具**
hello 下列兩個工具是可用 toohelp 深入了解所涉及執行 hello 預測性維護航太解決方案範本，您的訂用帳戶中的總成本：

* [Microsoft Azure Cost Estimator Tool (線上版)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure Cost Estimator Tool (桌面版)](http://www.microsoft.com/download/details.aspx?id=43376)

