---
title: "在航太工業中使用 Azure - Cortana Intelligence 解決方案進行預測性維護的技術指南 | Microsoft Docs"
description: "航太、公用事業和運輸中預測性維護的 Microsoft Cortana Intelligence 解決方案範本的技術指南。"
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
ms.openlocfilehash: d878a9b4d2e614070b5e0bf0cee5a2871963d6ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="technical-guide-to-the-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>航太與其他業務中預測性維護的 Cortana Intelligence 解決方案範本的技術指南

## <a name="important"></a>**重要**
此文章已被取代。 其中資訊與目前問題，亦即航太工業中的預測性維護，仍有相關，不過包含最新資訊的最新文章可在[此處](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace)找到。 

## <a name="acknowledgements"></a>**通知**
本文是由 Microsoft 的資料科學家 Yan Zhang、Gauher Shaheen、Fidan Boylu Uz 和軟體工程師 Dan Grecoe 所共同撰寫。

## <a name="overview"></a>**概觀**
解決方案範本的設計是要加速在 Cortana Intelligence 套件之上建置 E2E 示範的程序。 已部署的範本會以所需的 Cortana Intelligence 元件佈建您的訂用帳戶，並建立兩者間的關聯性。 它也會在資料管線內植入由資料產生器應用程式所產生的範例資料，供您在部署解決方案範本之後下載並安裝到本機電腦上。 由產生器產生的資料將會產生資料管線，並開始產生機器學習服務預測，然後您可以在 Power BI 儀表板上將其視覺化。 部署程序將引導您完成數個步驟來設定解決方案的認證。 務必記錄這些認證，例如您在部署期間提供的解決方案名稱、使用者名稱和密碼。  

這份文件的目標是說明參考架構，以及隨著此解決方案範本佈建在您訂用帳戶中的不同元件。 文件也會示範如何使用您自己的實際資料來取代範例資料，以便看到您自己的資料的見解和預測。 此外，文件將說明如果想要以您自己的資料自訂解決方案，您需要修改的解決方案範本部份。 最後會提供如何建置此方案範本的 Power BI 儀表板的指示。

> [!TIP]
> 您可以下載及列印 [這份文件的 PDF 版本](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf)。
> 
> 

## <a name="big-picture"></a>**概觀**
![預測性維護架構](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

部署解決方案時，會啟動 Cortana Analytics 套件中的各種 Azure 服務 (也就是事件中樞、串流分析、HDInsight、Data Factory、機器學習服務等)。 架構圖顯示在高層從端對端為航太解決方案範本建構預測性維護的方式。 您將可以在 Azure 入口網站調查這些服務，方法是對部署解決方案時所建立的解決方案範本圖表上的服務按一下，但 HDInsight 除外，因為當需要相關的管線活動才能執行時才會隨選佈建此服務，並且會於隨後刪除。
您可以下載 [完整大小版本的圖表](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png)。

下列章節說明每個片段。

## <a name="data-source-and-ingestion"></a>**資料來源及擷取**
### <a name="synthetic-data-source"></a>綜合資料來源
針對此範本，使用的資料來源是從桌面應用程式產生，您將會下載應用程式並於部署成功後在本機執行。 當您在解決方案範本圖表上選取稱為「預測性維護資料產生器」的第一個節點時，可以在屬性列中找到下載及安裝此應用程式的指示。 此應用程式會將在解決方案流程的其餘部分使用的資料點或事件送入 [Azure 事件中樞](#azure-event-hub) 服務。 此資料來源的組成為或衍生自[使用 Turbofan 引擎降低模擬資料集](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan)從 [NASA 資料儲存機制](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/)公開取得的資料。

只有當它在您的電腦上執行時，事件產生應用程式才會填入 Azure 事件中樞。

### <a name="azure-event-hub"></a>Azure 事件中樞
[Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/) 服務是上述的綜合資料來源所提供的輸入收件者。

## <a name="data-preparation-and-analysis"></a>**資料準備和分析**
### <a name="azure-stream-analytics"></a>Azure 串流分析
[Azure 串流分析](https://azure.microsoft.com/services/stream-analytics/)服務用來為來自 [Azure 事件中樞](#azure-event-hub)服務的輸入串流提供近乎即時的分析，並將結果發佈到 [Power BI](https://powerbi.microsoft.com) 儀表板，以及將所有未經處理的內送事件保存至 [Azure 儲存體](https://azure.microsoft.com/services/storage/)服務，供 [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) 服務後續處理。

### <a name="hd-insights-custom-aggregation"></a>HD Insights 自訂彙總
Azure HD Insight 服務用來執行 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 指令碼 (由 Azure Data Factory 協調)，以提供使用 Azure 串流分析服務封存的原始事件的彙總。

### <a name="azure-machine-learning"></a>Azure Machine Learning
使用 [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) 服務 (由 Azure Data Factory 協調) 對特定飛機引擎 (提供所收到輸入資料) 的剩餘使用年限 (RUL) 進行預測。

## <a name="data-publishing"></a>**資料發佈**
### <a name="azure-sql-database-service"></a>Azure SQL Database 服務
[Azure SQL Database](https://azure.microsoft.com/services/sql-database/) 服務用來儲存 (由 Azure Data Factory 管理) Azure Machine Learning 服務收到的預測，供 [Power BI](https://powerbi.microsoft.com) 儀表板中取用。

## <a name="data-consumption"></a>**資料耗用量**
### <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com) 服務用來顯示儀表板，其中包含 [Azure 串流分析](https://azure.microsoft.com/services/stream-analytics/)服務提供的彙總與警示，以及儲存在使用 [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) 服務產生的 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) 的 RUL 預測。 如需如何建置此方案範本的 Power BI 儀表板的指示，請參閱下一節。

## <a name="how-to-bring-in-your-own-data"></a>**如何帶入您自己的資料**
本節說明如何將您自己的資料帶入 Azure，以及對於您放入這個架構的資料，需要變更哪些區域。

您放入的任何資料集不太可能會符合用於這個解決方案範本的 [Turbofan 引擎降低模擬資料集](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) 所用的資料集。 了解您的資料與需求對於您如何修改此範本以搭配您自己的資料非常重要。 如果這是您第一次使用 Azure Machine Learning 服務，您可以使用 [如何建立您的第一個實驗](machine-learning-create-experiment.md)中的範例來取得簡介。

下列各節將討論推出新資料集將需要修改的範本區段。

### <a name="azure-event-hub"></a>Azure 事件中樞
Azure 事件中樞服務非常廣泛，因而資料可以以 CSV 或 JSON 格式張貼至中樞。 Azure 事件中樞中未發生任何特殊處理，但務必了解提供給它的資料。

這份文件不會描述如何擷取您的資料，但您可以使用事件中樞 API，輕鬆地傳送事件或資料到 Azure 事件中樞。

### <a name="azure-stream-analytics"></a>Azure 串流分析
Azure 串流分析服務用來提供近乎即時分析，方法是從資料串流讀取並輸出資料至任意數目的來源。

針對航太解決方案的預測性維護範本，Azure 串流分析查詢方案範本包含四個子查詢，每個均從 Azure 事件中樞服務取用事件，並且輸出至四個不同的位置。 這些輸出包含三個 Power BI 資料集和一個 Azure 儲存體位置。

可以透過以下方式找到 Azure 串流分析查詢：

* 登入 Azure 入口網站
* 找出部署解決方案時產生的串流分析作業 ![串流分析圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) (例如，預測性維護解決方案的 **maintenancesa02asapbi** 和 **maintenancesa02asablob**)
* 選取
  
  * [輸入] 以檢視查詢輸入
  * [查詢] 以檢視查詢本身
  * [輸出] 以檢視不同的輸出

Azure 串流分析查詢建構的相關資訊可在 MSDN 上的 [串流分析查詢參考](https://msdn.microsoft.com/library/azure/dn834998.aspx) 中找到。

在此解決方案中，查詢會將三個資料集及內送資料串流近乎即時的分析資訊輸出到隨著這個解決方案範本提供的 Power BI 儀表板。 因為對於內送資料格式具有隱含知識，必須根據您的資料格式變更這些查詢。

第二個串流分析作業 **maintenancesa02asablob** 中的查詢只是將所有[事件中樞](https://azure.microsoft.com/services/event-hubs/)事件輸出至 [Azure 儲存體](https://azure.microsoft.com/services/storage/)，不論資料格式為何，都不需進行修改，因為完整的事件資訊會串流至儲存體。

### <a name="azure-data-factory"></a>Azure Data Factory
[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) 服務會協調資料的移動和處理。 在航太解決方案的預測性維護範本中，Data Factory 包含三個 [管線](../data-factory/data-factory-create-pipelines.md) ，會使用各種技術移動和處理資料。  您可以開啟隨著解決方案部署建立的解決方案範本圖表底端的 Data Factory 節點，以存取您的 Data Factory。 這樣會帶您前往 Azure 入口網站上的 Data Factory。 如果您在您的資料集下看到錯誤，您可以忽略這些，錯誤是因為在啟動資料產生器之前即已部署 Data Factory。 這些錯誤不會防止您的 Data Factory 運作。

![Data Factory 資料集錯誤](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

本節將討論 [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) 中包含的必要[管線](../data-factory/data-factory-create-pipelines.md)和[活動](../data-factory/data-factory-create-pipelines.md)。 以下是解決方案的圖表檢視。

![Azure Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

此 Factory 的兩個管線包含 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 指令碼，用來分割及彙總資料。 如上述，指令碼將會位在安裝期間建立的 [Azure 儲存體](https://azure.microsoft.com/services/storage/) 帳戶中。 其位置會是：maintenancesascript\\\\script\\\\hive\\\\ (或 https://[您的解決方案名稱].blob.core.windows.net/maintenancesascript)。

類似於 [Azure 串流分析](#azure-stream-analytics-1)查詢，[Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 指令碼對於內送資料格式具有隱含知識，必須根據您的資料格式和[特徵工程設計](machine-learning-feature-selection-and-engineering.md)需求來變更這些查詢。

#### <a name="aggregateflightinfopipeline"></a><bpt id="p1">*</bpt>AggregateFlightInfoPipeline<ept id="p1">*</ept>
這個[管線](../data-factory/data-factory-create-pipelines.md)包含單一活動 - 使用 [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) 的 [HDInsightHive](../data-factory/data-factory-hive-activity.md) 活動，會在 [Azure 串流分析](https://azure.microsoft.com/services/stream-analytics/)作業期間，執行 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 指令碼來分割放在 [Azure 儲存體](https://azure.microsoft.com/services/storage/)中的資料。

此資料分割工作的 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 指令碼為 ***AggregateFlightInfo.hql***

#### <a name="mlscoringpipeline"></a><bpt id="p1">*</bpt>MLScoringPipeline<ept id="p1">*</ept>
這個[管線](../data-factory/data-factory-create-pipelines.md)包含數個活動，而其最終結果為來自與這個解決方案範本相關聯的 [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) 實驗評分的預測。

包含在此的活動為：

* 使用 [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) 的 [HDInsightHive](../data-factory/data-factory-hive-activity.md) 活動會執行 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 指令碼來執行 [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) 實驗所需的彙總及特徵工程設計。
  此資料分割工作的 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 指令碼是 ***PrepareMLInput.hql***。
* [複製](https://msdn.microsoft.com/library/azure/dn835035.aspx)活動，它會將來自 [HDInsightHive](../data-factory/data-factory-hive-activity.md) 活動的結果移至可供 [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) 活動存取的單一 [Azure 儲存體](https://azure.microsoft.com/services/storage/) Blob。
* 呼叫 [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) 實驗的 [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) 活動，會導致將結果放入單一 [Azure 儲存體](https://azure.microsoft.com/services/storage/) Blob。

#### <a name="copyscoredresultpipeline"></a><bpt id="p1">*</bpt>CopyScoredResultPipeline<ept id="p1">*</ept>
這個[管線](../data-factory/data-factory-create-pipelines.md)包含單一活動 - [複製](https://msdn.microsoft.com/library/azure/dn835035.aspx)活動，會將 [Azure Machine Learning](#azure-machine-learning) 實驗的結果從 ***MLScoringPipeline*** 移至隨著解決方案範本安裝佈建的 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。

### <a name="azure-machine-learning"></a>Azure Machine Learning
用於此解決方案範本的 [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) 實驗會提供飛機引擎的剩餘使用年限 (RUL)。 實驗因取用的資料集而不同，因而需要特別針對帶入的資料進行修改或取代。

如需如何建立 Azure Machine Learning 實驗的詳細資訊，請參閱 [預測性維護：步驟 3 之 1，資料準備和特徵設計](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2)。

## <a name="monitor-progress"></a>**監視進度**
 一旦資料產生器啟動，管線會開始合成，解決方案的不同元件會遵循 Data Factory 發出的命令開始動作。 您有兩種方式可以監視管線。

1. 其中一個串流分析作業會將原始內送資料寫入 blob 儲存體。 如果您從成功部署解決方案的畫面按一下解決方案的 Blob 儲存體元件，然後在右窗格中按一下 [開啟]，系統就會帶您前往[管理入口網站](https://portal.azure.com/)。 一旦在該網站中，按一下 Blobs。 在接下來的面板中，您會看到容器的清單。 按一下 [maintenancesadata]。 在接下來的面板中，您會看到 **rawdata** 資料夾。 在 rawdata 資料夾內，您會看到具有如 hour=17、hour=18 等等名稱的資料夾。如果您看到這些資料夾，則表示原始資料已經成功在您的電腦上產生並儲存在 blob 儲存體。 您應該會在這些資料夾中看到具有有限大小 (MB) 的 csv 檔案。
2. 管線的最後一個步驟是將資料 (例如從機器學習的預測) 寫入至 SQL Database。 您可能必須等候最多三個小時，資料才會出現在 SQL Database。 監視 SQL Database 中有多少資料的其中一種方法是透過 [Azure 入口網站](https://manage.windowsazure.com/)。在左側面板中找出並按一下 SQL DATABASES ![SQL 圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png)。 接著找到您的資料庫 **pmaintenancedb** 並按一下它。 在下一個頁面的底部，按一下 [管理]
   
    ![管理圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png)。
   
    您可以在這裡按一下 [新增查詢]，並且查詢資料列的數目 (例如，從 PMResult 選取 count(*))。 隨著您的資料庫成長，資料表中的資料列數目應該會增加。

## <a name="power-bi-dashboard"></a>**Power BI 儀表板**
### <a name="overview"></a>概觀
本節說明如何設定 Power BI 儀表板，以呈現來自 Azure 串流分析 (熱路徑) 的即時資料，以及來自 Azure 機器學習服務 (冷路徑) 的 Batch 預測結果。

### <a name="setup-cold-path-dashboard"></a>安裝程式冷路徑儀表板
在冷路徑資料管線中，不可或缺的目標是在飛機完成航程 (循環) 後取得每個飛機引擎的預測 RUL (剩餘使用年限)。 預測結果會每 3 個小時更新，用於預測在過去 3 小時內完成航班的飛機引擎。

Power BI 會連接到 Azure SQL Database 做為其資料來源，即預測結果的儲存位置。 附註：1) 在部署您的解決方案時，會在資料庫中顯示過去 3 小時內的實際預測。
產生器下載隨附的 pbix 檔案包含一些種子資料，因此您可以立即建立 Power BI 儀表板。 2) 在此步驟中，必要條件就是下載並安裝免費版軟體 [Power BI 桌面版](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)。

下列步驟將引導您如何將 pbix 檔案連接到 SQL Database，該資料庫針對視覺效果在解決方案部署包含資料 (例如 預測結果) 時加快運轉。

1. 取得資料庫認證。
   
   在移至後續步驟之前，您將需要 **資料庫伺服器名稱、資料庫名稱、使用者名稱和密碼** 。 以下是引導您如何尋找的步驟。
   
   * 一旦您的解決方案範本圖表上的 [Azure SQL Database] 變成綠色之後，請按一下它，然後按一下 [開啟]。
   * 您會看到新的瀏覽器索引標籤/視窗，其中顯示 Azure 入口網站頁面。 按一下左側面板上的 [資源群組]  。
   * 選取您用於部署解決方案的訂用帳戶，然後選取 [YourSolutionName\_ResourceGroup]。
   * 在新的快顯面板中，按一下 ![SQL 圖示](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png)圖示來存取您的資料庫。 您的資料庫名稱會在這個圖示旁邊 (例如，**'pmaintenancedb'**)，而**資料庫伺服器名稱**列在伺服器名稱屬性下方，看起來應該類似 **YourSoutionName.database.windows.net**。
   * 您的資料庫**使用者名稱**和**密碼**使用解決方案部署期間記錄的相同使用者名稱和密碼。
2. 使用 Power BI 桌面版來更新冷路徑報告檔案的資料來源。
   
   * 在您下載並解壓縮產生器檔案之電腦上的資料夾中，按兩下 **PowerBI\\PredictiveMaintenanceAerospace.pbix** 檔案。 如果您開啟檔案時看到任何警告訊息，請忽略它們。 在檔案的頂端按一下 [編輯查詢] 。
     
     ![編輯查詢](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * 您會看到兩個資料表，**RemainingUsefulLife** 和 **PMResult**。 選取第一個資料表，然後在右側 [查詢設定] 面板的 [套用的步驟] 下，按一下 [來源]旁的 ![Query settings icon](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png)。 略過任何出現的警告訊息。
   * 在快顯視窗中，將 [伺服器] 和 [資料庫] 取代為您自己的伺服器和資料庫名稱，然後按一下 [確定]。 針對伺服器名稱，請確定您指定連接埠 1433 (**YourSoutionName.database.windows.net, 1433**)。 讓 [資料庫] 欄位保持為 [pmaintenancedb]。 忽略畫面上出現的警告訊息。
   * 在下一個快顯視窗中，您會在左側窗格上看到兩個選項 ([Windows] 和 [資料庫])。 按一下 [資料庫]，填入您的 [使用者名稱] 和 [密碼] \(這是當您首次部署解決方案並建立 Azure SQL Database 時輸入的使用者名稱和密碼)。 在 [選取要套用這些設定的層級] 中，請勾選資料庫層級選項。 然後按一下 [連接]。
   * 按一下第二個資料表 **PMResult**，然後在右側 [查詢設定] 面板的 [套用的步驟] 下，按一下 [來源] 旁的 ![Navigation icon](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png)，依上述步驟所示更新伺服器和資料庫名稱，然後按一下 [確定]。
   * 一旦引導您回到上一頁，請關閉視窗。 訊息將會蹦現 - 按一下 [套用] 。 最後，按一下 [儲存]  按鈕以儲存變更。 您的 Power BI 檔案現在已建立與伺服器的連線。 如果視覺效果是空的，請確定將視覺效果上的選取範圍都清除，以將所有資料視覺化，成法是按一下圖例右上角的橡皮擦圖示。 使用重新整理按鈕在視覺效果上反映新的資料。 最初，您只會在視覺效果上看到種子資料，因為 Data Factory 排定為每 3 個小時重新整理。 3 小時後，當您重新整理資料時，您會看到新的預測反映在視覺效果中。
3. (選擇性) 將冷路徑儀表板發佈至 [Power BI 線上版](http://www.powerbi.com/)。 請注意，這個步驟需要 Power BI 帳戶 (或 Office 365 帳戶)。
   
   * 按一下 [發佈]，幾秒鐘後會出現一個視窗顯示「發佈至 Power BI 成功!」， 並帶有綠色核取記號。 按一下 [在 Power BI 中開啟 PredictiveMaintenanceAerospace.pbix] 下方的連結。 若要尋找詳細的指示，請參閱[從 Power BI Desktop 發佈](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop)。
   * 若要建立新儀表板：在左側窗格中按一下 [儀表板] 區段旁的 **+** 號。 為這個新儀表板輸入名稱「預測性維護示範」。
   * 開啟報告後，按一下 ![PIN icon](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png)，將所有視覺效果釘選至儀表板。 若要尋找詳細的指示，請參閱 [從報告將磚釘選至 Power BI 儀表板](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report)。
     前往儀表板頁面並調整視覺效果的大小和位置，以及編輯其標題。 若要尋找如何編輯您的磚的詳細說明，請參閱 [編輯磚 -- 調整大小、移動、重新命名、釘選、刪除、加入超連結](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename)。 以下是具有釘選了一些冷路徑視覺效果的範例儀表板。  根據執行資料產生器的時間長度，在視覺效果上的數字可能會不同。
     <br/>
     ![最終檢視](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * 若要排定重新整理資料，請將滑鼠移至 **PredictiveMaintenanceAerospace** 資料集上，按一下 ![Elipsis icon](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png)，然後選擇 [排程重新整理]。
     <br/>
     **附註：**如果您看到警告訊息，請按一下 **編輯認證**，並確定您的資料庫認證與步驟 1 中所述相同。
     <br/>
     ![排程重新整理](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * 展開 **排程重新整理** 一節。 開啟「將您的資料保持最新」。
     <br/>
   * 根據您的需求排程重新整理。 若要尋找詳細資訊，請參閱 [Power BI 中的資料重新整理](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi)。

### <a name="setup-hot-path-dashboard"></a>安裝程式最忙碌路徑儀表板
下列步驟將引導您如何以視覺化方式檢視解決方案部署時所產生串流分析作業的即時資料輸出。 需要 [Power BI 線上版](http://www.powerbi.com/) 帳戶，才能執行下列步驟。 如果您沒有帳戶，您可以 [建立一個](https://powerbi.microsoft.com/pricing)。

1. 在 Azure 串流分析 (ASA) 中加入 Power BI 輸出。
   
   * 您必須依照 [Azure 串流分析及 Power BI：適用於串流資料即時可見度的即時分析儀表板](../stream-analytics/stream-analytics-power-bi-dashboard.md)中的指示，將 Azure 串流分析作業的輸出設定為 Power BI 儀表板。
   * ASA 查詢有三個輸出，分別是 **aircraftmonitor**、**aircraftalert** 和 **flightsbyhour**。 按一下 [查詢] 索引標籤，就可以檢視查詢。 對應至每一個資料表，您必須將輸出新增到 ASA。 當您新增第一個輸出 (例如 **aircraftmonitor**) 時，請確定**輸出別名**、**資料集名稱**和**資料表名稱**皆相同 (**aircraftmonitor**)。 重複這些步驟來新增 **aircraftalert** 和 **flightsbyhour** 的輸出。 新增所有三個輸出資料表並啟動 ASA 作業後，應該會出現確認訊息 (例如，「啟動串流分析作業 maintenancesa02asapbi 成功」)。
2. 登入 [Power BI 線上版](http://www.powerbi.com)
   
   * 在 [我的工作區] 的左側面板 [資料集] 區段中，應該會出現 ***DATASET*** 名稱 **aircraftmonitor**、**aircraftalert** 和 **flightsbyhour**。這是您在上一個步驟中從 Azure 串流分析推送的串流資料。由於其背後的 SQL 查詢本質使然，資料集 **flightsbyhour** 可能不會和其他兩個資料集同時顯示。 不過，它應該會在一個小時之後出現。
   * 請確定 [視覺效果]  窗格開啟，並顯示在螢幕的右邊。
3. 將資料傳送到 Power BI 之後，您就可以開始視覺化串流資料。 以下是具有釘選了一些最忙碌路徑視覺效果的範例儀表板。 您可以根據適當的資料集建立其他儀表板磚。 根據執行資料產生器的時間長度，在視覺效果上的數字可能會不同。

    ![儀表板檢視](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. 以下是一些用來建立上述其中一個圖格的步驟 -「感應器 11 與閾值 48.26 的機隊檢視」磚：
   
   * 在左側面板 [資料集] 區段中按一下資料集 **aircraftmonitor** 。
   * 按一下 [折線圖]  圖示。
   * 按一下 [欄位] 窗格中的 [已處理]，使其顯示於 [視覺效果] 窗格中的「軸」下方。
   * 按一下 "s11" 和 "s11\_alert"，使它們都出現在「值」下方。 按一下 **s11** 和 **s11\_alert** 旁邊的小箭頭，將「總和」變更為「平均」。
   * 按一下上方的 [儲存]  並將報告命名為 "aircraftmonitor"。 名為 "aircraftmonitor" 的報告會顯示在左側 [導覽] 窗格的 [報告] 區段中。
   * 按一下此折線圖右上角的 [釘選視覺]  圖示。 可能出現「釘選至儀表板」視窗供您選擇儀表板。 選取 [預測性維護示範]，然後按一下 [釘選]。
   * 在儀表板上將滑鼠停留在此磚中，按一下右上角的 [編輯] 圖示可將其標題變更為「感應器 11 與閾值 48.26 的機隊檢視」和副標題變更為「機隊經過一段時間的平均值」。

## <a name="how-to-delete-your-solution"></a>**如何刪除解決方案**
請確定您在未積極使用解決方案時有停止資料產生器，因為執行資料產生器將會產生較高的成本。 如果不使用解決方案，請將其刪除。 刪除解決方案時，將會刪除您在部署解決方案時於訂用帳戶中佈建的所有元件。 如果要刪除解決方案，請在解決方案範本左側面板中按一下該解決方案的名稱，然後按一下 [刪除]。

## <a name="cost-estimation-tools"></a>**成本估計工具**
下列兩項工具可協助您進一步了解在您的訂用帳戶中執行航太解決方案範本的預測性維護所牽涉的總成本：

* [Microsoft Azure Cost Estimator Tool (線上版)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure Cost Estimator Tool (桌面版)](http://www.microsoft.com/download/details.aspx?id=43376)

