---
title: "aaaIntroduction tooStream 分析 |Microsoft 文件"
description: "深入了解 Stream Analytics 中，受管理的服務，可協助您分析 hello 物聯網 (IoT) 從資料流資料即時。"
keywords: "分析服務, 受管理服務, 串流處理, 串流分析, 什麼是串流分析"
services: stream-analytics
documentationcenter: 
author: jenniehubbard
manager: jhubbard
editor: cgronlun
ms.assetid: 613c9b01-d103-46e0-b0ca-0839fee94ca8
ms.service: stream-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/08/2017
ms.author: jhubbard
ms.openlocfilehash: 6dd7ea1d358bcc94e927a3e699a2771a25104d72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-stream-analytics"></a>什麼是串流分析？

Azure 串流分析是可完全管理的事件處理引擎，可讓您設定串流資料的即時分析計算。 hello 資料可以來自裝置、 感應器、 網站、 社交媒體摘要、 應用程式、 基礎結構系統等等。 

## <a name="what-can-i-do-with-stream-analytics"></a>如何使用串流分析？

使用資料流分析 tooexamine 大量資料從裝置或處理程序、 hello 資料流，從擷取的資訊和尋找模式、 趨勢和關聯性。 根據何謂 hello 資料中，您可以再執行應用程式工作。 比方說，您可能會引發警示、 開始進行的自動化工作流程、 摘要資訊 tooa 報告工具，例如 Power BI 中，或儲存資料供日後調查。 

範例：

* 由金融服務公司所提供的個人化即時股票交易分析和警示。
* 透過檢查交易資料即時偵測詐騙行動。 
* 資料與身分識別保護服務。
* 分析實體物件 (物聯網或 IoT) 中裝載的感應器和傳動器所產生的資料。
* Web 點選流分析。
* 客戶關係管理 (CRM) 應用程式，例如當客戶體驗的表現在某段時間內變差時發出警示。

## <a name="how-does-stream-analytics-work"></a>串流分析如何運作？

此圖說明 hello 資料流分析管線，顯示如何資料會內嵌、 分析，然後再傳送簡報或動作。 

![串流分析流程](./media/stream-analytics-introduction/stream_analytics_intro_pipeline.png)

串流分析會從串流資料的來源開始。 可以 ingested hello 資料至 Azure，Azure 事件中心] 或 [IoT 中樞用裝置。 hello 資料也可以取自資料存放區，例如 Azure Blob 儲存體。 

tooexamine hello 資料流，建立資料流分析*作業*指定 hello 資料來自何處。 hello 作業也會指定*轉換*&mdash;如何 toolook 的資料、 模式或關聯性。 針對這項工作，串流分析支援類似 SQL 的查詢語言，可讓您篩選、排序、彙總和聯結一段時間內的串流資料。

最後，hello 作業指定輸出 toosend hello 轉換的資料。 這可讓您控制哪些 toodo 回應 toohello 資訊在您已經分析。 例如，在回應 tooanalysis，您可能會：

* 傳送命令 toochange 裝置的設定。 
* 傳送資料 tooa 佇列監視的處理序會根據它所找到的動作。 
* 傳送資料 tooa Power BI 儀表板報告。
* 傳送資料 toostorage 像是 Data Lake Store、 SQL Server 資料庫或 Azure Blob 或資料表儲存體。

執行作業時，您可以監視作業和調整其每秒處理的事件數。 您也可以取得作業的產生診斷記錄，以便進行移難排解。

## <a name="key-capabilities-and-benefits"></a>主要功能和優點

Stream Analytics 是設計的 toobe 輕鬆 toouse，彈性、 可擴充 tooany 作業大小及節省資源。

### <a name="connectivity-toomany-inputs-and-outputs"></a>連線 toomany 輸入和輸出

Stream Analytics 連接直接太[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)和[Azure IoT 中樞](https://azure.microsoft.com/services/iot-hub/)資料流擷取和 hello [Azure Blob 儲存體服務](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage-accounts)tooingest 歷程記錄資料。 如果您從事件中樞取得資料，可以結合串流分析與其他資料來源和處理引擎。

作業輸入也可以包含參考資料 (靜態或變更緩慢的資料)。 您可以將資料流資料 toothis 參考資料 tooperform 查閱作業 hello 相同的方式使用資料庫查詢。

以許多方向路由傳送串流分析作業輸出。 您可以撰寫 toostorage，例如 Azure 儲存體 blob 或資料表、 Azure SQL DB、 Azure 資料湖存放區或 Azure Cosmos DB。 從該處，hello 資料可能會透過 Azure HDInsight 移批次分析的。 您可能會傳送 hello 輸出 tooanother 服務取用另一個處理序，例如事件中心、 Azure 服務匯流排主題或佇列。 您可能會傳送 hello 輸出 tooPower BI 視覺效果。

### <a name="ease-of-use"></a>容易使用

使用簡單、 宣告式 toodefine 轉換[Stream Analytics 查詢語言](https://msdn.microsoft.com/library/azure/dn834998.aspx)，可讓您以任何程式設計方式建立複雜的分析。 hello 查詢語言會接受做為輸入資料流處理資料。 接著，您可以篩選及排序 hello 資料彙總值、 執行計算，加入資料 （資料流或 tooreference 資料內），並使用地理空間函數。 您可以編輯查詢 hello 入口網站中的使用 IntelliSense 和語法檢查以及您可以測試使用範例資料，您可以從 hello 即時資料流擷取的查詢。

### <a name="extensible-query-language"></a>可延伸的查詢語言

您可以擴充 hello 功能 hello 查詢語言的定義，並叫用其他函數。 您可以定義函式呼叫 hello Azure 機器學習服務 tootake 利用 Azure 機器學習解決方案中。 您也可以整合順序 tooperform 複雜計算中的 JavaScript 使用者定義函數 (Udf)，做為資料流分析查詢的一部分。

### <a name="scalability"></a>延展性

資料流分析可以處理向上 too1 GB 每秒連入資料。 與整合[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)和[Azure IoT 中樞](https://azure.microsoft.com/services/iot-hub/)一些可讓工作 tooingest 數以百萬計的第二個來自事件從連接的裝置、 整體觀，以及記錄檔，tooname。 使用事件中心 hello 資料分割功能，您可以分割為邏輯步驟的計算，每個都有 hello 能力 toobe 進一步分割 tooincrease 延展性。

### <a name="low-cost"></a>低成本

為雲端服務時，串流分析是最佳化的 toolet 開始極低成本。 您必須支付隨時根據資料流處理單位使用量和 hello 金額 hello 系統所處理的資料。 使用衍生根據 hello 磁碟區處理的事件，而且 hello 數量計算能力的佈建內 hello 叢集 toohandle 串流分析工作。

### <a name="reliability-quick-recovery-and-repeatability"></a>可靠性、快速修復和可重複性

Hello 雲端中受管理的服務，為資料流分析可協助防止資料遺失，並提供業務持續性。 如果發生失敗，hello 服務會提供內建復原功能。 Hello 能力 toointernally 維護狀態，hello 服務提供可重複的結果，確保它很可能 tooarchive 事件，而且重新套用 hello 未來，永遠都會取得相同的結果 hello 中處理。 這可讓您回到過去的 toogo 並調查根本原因分析、 假設狀況分析等方式來執行作業的計算。

## <a name="next-steps"></a>後續步驟

* 先從[嘗試從 IoT 裝置執行匯入和查詢](stream-analytics-get-started-with-azure-stream-analytics-to-process-data-from-iot-devices.md)開始。
* 建置[端對端資料流分析解決方案](stream-analytics-real-time-fraud-detection.md)，會檢查電話中繼資料 toolook 詐騙的呼叫。
* 了解獨特的概念，例如 hello Stream Analytics 中，類似 SQL 的查詢語言以及[視窗函數](stream-analytics-window-functions.md)。
* 了解如何太[調整串流分析工作](stream-analytics-scale-jobs.md)。 
* 了解如何太[整合資料流分析和 Azure Machine Learning](stream-analytics-machine-learning-integration-tutorial.md)。
* Hello 中找到 tooyour 資料流分析問題的答案[Azure 資料流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

