---
title: "資料連線：來自事件資料流的資料流輸入 | Microsoft Docs"
description: "深入了解設定資料連接 tooStream 呼叫 '輸入' 的分析。 輸入包括來自事件的資料流，以及參考資料。"
keywords: "資料流, 資料連線, 事件資料流"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 8155823c-9dd8-4a6b-8393-34452d299b68
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/05/2017
ms.author: samacha
ms.openlocfilehash: be2008f159061c5c9be9d0314c27fa67193e3269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-connection-learn-about-data-stream-inputs-from-events-toostream-analytics"></a>資料連接： 了解資料中的事件 tooStream 分析的資料流輸入
hello 資料連接 tooa 資料流分析工作會從資料來源，也就是參考的 tooas hello 作業的事件資料流*輸入*。 串流分析與 Azure 資料流來源的整合性極佳，來源包括 [Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/)、[Azure IoT 中樞](https://azure.microsoft.com/services/iot-hub/)和 [Azure Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)。 這些輸入來源可以是從 hello 相同 Azure 訂用帳戶以分析工作，或從不同的訂用帳戶。

## <a name="data-input-types-data-stream-and-reference-data"></a>資料輸入類型：資料流和參考資料
資料推入 tooa 資料來源，因為它有 hello 資料流分析工作所耗用，而且即時處理。 輸入分為兩種類型：資料流輸入和參考資料輸入。

### <a name="data-stream-inputs"></a>資料流輸入
資料流是一段時間內發生的無限制事件序列。 串流分析作業必須包含至少一個資料流輸入。 支援將事件中樞、IoT 中樞和 Blob 儲存體當成資料流輸入來源。 事件中心是使用的 toocollect 事件資料流，從多個裝置和服務。 這些資料流可能包括社交媒體活動摘要、股票交易資訊或來自感應器的資料。 IoT 中樞是從連接的裝置在物聯網 (IoT) 案例中的最佳化的 toocollect 資料。  Blob 儲存體可作為輸入來源，將大量資料內嵌為資料流，例如記錄檔。  

### <a name="reference-data"></a>參考資料
串流分析也支援稱為「參考資料」的輸入。 這是靜態或緩慢變更的輔助資料。 通常用來執行相互關聯和查閱。 例如，您可能會聯結資料 hello 參考資料中的 hello 資料資料流輸入 toodata 就像您會執行 SQL 聯結 toolook 靜態值。 Azure Blob 儲存體正在 hello 只支援輸入的參考資料來源。 參考資料來源 blob 受到 too100 MB 的大小。

如何 toocreate 參考資料輸入，請參閱的 toolearn[使用參考資料](stream-analytics-use-reference-data.md)。  

## <a name="create-data-stream-input-from-event-hubs"></a>從事件中樞建立資料流輸入

Azure 事件中樞提供高延展性的發佈-訂閱事件擷取器。 事件中心可以收集數百萬個每秒的事件，如此您可以處理及分析 hello 連接的裝置和應用程式所產生的資料量很大。 事件中樞搭配串流分析，一起為您提供端對端解決方案來分析即時資料 -- 事件中樞可讓您即時將事件傳送到 Azure，而 Stream Analytics 作業可以即時處理這些事件。 例如，您可以傳送網頁點選、 感應器讀數或線上記錄事件 tooEvent 集線器。 然後，您可以建立資料流分析工作 toouse 事件中心為 hello 即時篩選、 彙總，以及相互關聯的輸入的資料流。

hello 預設來自事件中心在 Stream Analytics 中的事件時間戳記是 hello hello 事件的時間戳記抵達 hello 事件中心是`EventEnqueuedUtcTime`。 tooprocess hello hello 事件裝載中使用時間戳記資料流的形式的資料，您必須使用 hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx)關鍵字。

### <a name="consumer-groups"></a>用戶群組
您應該設定每個資料流分析事件中樞輸入的 toohave 它自己的取用者群組。 當作業包含自我聯結或有多個輸入時，某些輸入可能由下游的多個讀取器所讀取。 這種情況下會影響單一取用者群組中的讀取器的 hello 數目。 tooavoid 超過 hello 事件中心限制的每個取用者群組，每個資料分割的五個讀取器，它是最佳的作法 toodesignate 取用者群組的每個資料流分析工作。 另外也限制每一個事件中樞最多有 20 個取用者群組。 如需詳細資訊，請參閱[事件中樞程式設計指南](../event-hubs/event-hubs-programming-guide.md)。

### <a name="configure-an-event-hub-as-a-data-stream-input"></a>將事件中樞設定為資料流輸入
hello 下列資料表說明每個屬性在 hello**新輸入**刀鋒視窗中 hello Azure 入口網站，當您設定事件中心做為輸入。

| 屬性 | 說明 |
| --- | --- |
| **輸入別名** |這個輸入您在 hello 工作查詢 tooreference 中使用的易記名稱。 |
| **服務匯流排命名空間** |Azure 服務匯流排命名空間，是一組訊息實體的容器。 建立新的事件中樞時，也會建立服務匯流排命名空間。 |
| **事件中樞名稱** |hello 的 hello 事件中樞 toouse 做為輸入的名稱。 |
| **事件中樞原則名稱** |提供存取 toohello 事件中樞的 hello 共用存取原則。 每一個共用存取原則都會有名稱、權限 (由您設定) 和存取金鑰。 |
| **事件中樞取用者群組** (選用) |hello 取用者群組 toouse tooingest 資料從 hello 事件中樞。 如果取用者未不指定任何群組，hello 資料流分析工作會使用 hello 預設取用者群組。 建議讓每一個串流分析作業使用不同的取用者群組。 |
| **事件序列化格式** |hello 序列化格式 （JSON、 CSV 或 Avro） hello 內送資料流。 |
| **編碼** | Utf-8 是目前只支援 hello 編碼格式。 |

當您的資料來自於事件中樞時，您會有存取 toohello 下列中繼資料資料流分析查詢中的欄位：

| 屬性 | 說明 |
| --- | --- |
| **EventProcessedUtcTime** |hello 日期和時間 hello 事件已處理的資料流分析。 |
| **EventEnqueuedUtcTime** |hello 日期和時間 hello 事件已收到事件中心。 |
| **PartitionId** |hello hello 輸入配接器的以零為起始的資料分割識別碼。 |

例如，使用這些欄位，您就可以撰寫類似下列範例中的 hello 的查詢：

````
SELECT
    EventProcessedUtcTime,
    EventEnqueuedUtcTime,
    PartitionId
FROM Input
````

## <a name="create-data-stream-input-from-iot-hub"></a>從 IoT 中樞建立資料流輸入
Azure IoT 中樞是已針對 IoT 案例最佳化的高延展性發佈/訂閱事件擷取器。

hello 預設時間戳記的事件來自 IoT 中心在 Stream Analytics 是 hello hello 事件的時間戳記到達在 hello IoT 中樞是`EventEnqueuedUtcTime`。 tooprocess hello hello 事件裝載中使用時間戳記資料流的形式的資料，您必須使用 hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx)關鍵字。

> [!NOTE]
> 傳送的訊息必須附上 `DeviceClient` 屬性才能處理。
> 
> 

### <a name="consumer-groups"></a>用戶群組
您應該設定每個資料流分析 IoT 中樞輸入的 toohave 它自己的取用者群組。 當作業包含自我聯結或有多個輸入時，某些輸入可能由下游的多個讀取器所讀取。 這種情況下會影響單一取用者群組中的讀取器的 hello 數目。 tooavoid 超過 hello Azure IoT 中樞限制的每個取用者群組，每個資料分割的五個讀取器，它是最佳的作法 toodesignate 取用者群組的每個資料流分析工作。

### <a name="configure-an-iot-hub-as-a-data-stream-input"></a>將 IoT 中樞設定為資料流輸入
hello 下列資料表說明每個屬性在 hello**新輸入**hello IoT 中樞設定做為輸入時，Azure 入口網站中的刀鋒視窗。

| 屬性 | 說明 |
| --- | --- |
| **輸入別名** |這個輸入您在 hello 工作查詢 tooreference 中使用的易記名稱。|
| **IoT 中樞** |hello 的 hello IoT 中樞 toouse 做為輸入的名稱。 |
| **端點** |hello hello IoT 中樞端點。|
| **共用存取原則名稱** |提供存取 toohello IoT 中樞的 hello 共用存取原則。 每一個共用存取原則都會有名稱、權限 (由您設定) 和存取金鑰。 |
| **共用存取原則金鑰** |使用 tooauthorize 存取 toohello IoT 中樞的 hello 共用的存取金鑰。 |
| **取用者群組** (選用) |hello 取用者群組 toouse tooingest 資料 hello IoT 中樞。 如果取用者未不指定任何群組，資料流分析工作會使用 hello 預設取用者群組。 建議讓每一個串流分析作業使用不同的取用者群組。 |
| **事件序列化格式** |hello 序列化格式 （JSON、 CSV 或 Avro） hello 內送資料流。 |
| **編碼** |Utf-8 是目前只支援 hello 編碼格式。 |

當您的資料來自 IoT 中樞時，您會有存取 toohello 下列中繼資料資料流分析查詢中的欄位：

| 屬性 | 說明 |
| --- | --- |
| **EventProcessedUtcTime** |hello 事件處理的 hello 日期和時間。 |
| **EventEnqueuedUtcTime** |hello 日期和時間 hello 事件已收到 hello IoT 中樞。 |
| **PartitionId** |hello hello 輸入配接器的以零為起始的資料分割識別碼。 |
| **IoTHub.MessageId** | 識別碼中使用過 toocorrelate 雙向通訊 IoT 中樞。 |
| **IoTHub.CorrelationId** |IoT 中樞內用於訊息回應和回饋的識別碼。 |
| **IoTHub.ConnectionDeviceId** |hello 驗證識別碼使用 toosend 這則訊息。 這個值是由 hello IoT 中樞，加上戳記 servicebound 訊息上。 |
| **IoTHub.ConnectionDeviceGenerationId** |hello 產生識別碼 hello 進行驗證裝置所使用的 toosend 這則訊息。 這個值是由 hello IoT 中樞，加上戳記 servicebound 訊息上。 |
| **IoTHub.EnqueuedTime** |收到 hello 訊息 hello IoT 中樞的 hello 時間。 |
| **IoTHub.StreamId** |自訂事件屬性，新增的 hello 寄件者裝置。 |


## <a name="create-data-stream-input-from-blob-storage"></a>從 Blob 儲存體建立資料流輸入
含有大量非結構化的資料 toostore hello 雲端中的情況下，Azure Blob 儲存體提供符合成本效益且可擴充的方案。 Blob 儲存體中的資料通常被視為待用資料。 但可以由串流分析當作資料流來處理。 記錄處理是透過串流分析來處理 Blob 儲存體輸入的常見情節。 在此案例中，已從系統擷取遙測資料，需要 toobe 剖析和處理 tooextract 有意義的資料。

hello 預設 Blob 存放區中的事件資料流分析的時間戳記是上次修改 hello blob 的 hello 時間戳記，也就是`BlobLastModifiedUtcTime`。 tooprocess hello hello 事件裝載中使用時間戳記資料流的形式的資料，您必須使用 hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx)關鍵字。

CSV 格式輸入*需要*標頭資料列 toodefine hello 資料集欄位。 此外，所有標題列欄位都必須是唯一的。

> [!NOTE]
> Stream Analytics 不支援加入內容 tooan 現有的 blob。 Stream Analytics 檢視 blob 的一次，並不會處理 hello 作業具有讀取 hello 資料之後進行 hello blob 中的任何變更。 最佳作法是為 tooupload hello 的所有資料一次，而不加入事件 toothat blob 存放區。
> 

### <a name="configure-blob-storage-as-a-data-stream-input"></a>將 Blob 儲存體設定為資料流輸入

hello 下列資料表說明每個屬性在 hello**新輸入**hello Azure 入口網站，當您設定做為輸入的 Blob 儲存體中的刀鋒視窗。

| 屬性 | 說明 |
| --- | --- |
| **輸入別名** | 這個輸入您在 hello 工作查詢 tooreference 中使用的易記名稱。 |
| **儲存體帳戶** | hello hello hello blob 檔案的所在位置的儲存體帳戶名稱。 |
| **儲存體帳戶金鑰** | hello 秘密金鑰與 hello 儲存體帳戶相關聯。 |
| **容器** | hello blob 輸入 hello 容器。 容器提供 blob 儲存在 hello Microsoft Azure Blob 服務中的邏輯分組。 當您上傳 blob toohello Azure Blob 儲存體服務時，您必須指定該 blob 的容器。 |
| **路徑模式** (選用) | toolocate hello blob hello 指定容器內使用 hello 檔案路徑。 Hello 路徑內，您可以指定一或多個執行個體的下列三個變數的 hello: `{date}`， `{time}`，或`{partition}`<br/><br/>範例 1：`cluster1/logs/{date}/{time}/{partition}`<br/><br/>範例 2：`cluster1/logs/{date}`<br/><br/>hello`*`字元不是允許的值為 hello 路徑前置詞。 僅允許有效的 <a HREF="https://msdn.microsoft.com/library/azure/dd135715.aspx">Azure blob 字元</a>。 |
| **日期格式** (選用) | 如果您使用 hello 路徑中的 hello 日期變數，hello 檔會組織中的 hello 的日期格式。 範例： `YYYY/MM/DD` |
| **時間格式** (選用) |  如果您使用 hello 時間變數 hello 路徑中，hello 檔會組織中的 hello 的時間格式。 目前僅支援 hello 的值是`HH`。 |
| **事件序列化格式** | hello 序列化格式 （JSON、 CSV 或 Avro） 為傳入的資料流。 |
| **編碼** | 如需 CSV 和 JSON，utf-8 目前是 hello 才支援編碼格式。 |

當您的資料來自 Blob 儲存體來源時，您會有存取 toohello 下列中繼資料資料流分析查詢中的欄位：

| 屬性 | 說明 |
| --- | --- |
| **BlobName** |來自 hello hello hello 事件的輸入 blob 名稱。 |
| **EventProcessedUtcTime** |hello 日期和時間 hello 事件已處理的資料流分析。 |
| **BlobLastModifiedUtcTime** |上次修改該 hello blob hello 日期和時間。 |
| **PartitionId** |hello hello 輸入配接器的以零為起始的資料分割識別碼。 |

例如，使用這些欄位，您就可以撰寫類似下列範例中的 hello 的查詢：

````
SELECT
    BlobName,
    EventProcessedUtcTime,
    BlobLastModifiedUtcTime
FROM Input
````

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
您已經了解自己串流分析工作的資料連線選項。 toolearn 有關資料流分析的詳細資訊，請參閱：

* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
