---
title: "aaaAdd 資料輸入 tooyour 串流分析工作 |Microsoft 文件"
description: "了解如何設定串流分析資料來源 tooyour toohook 作業為資料流的資料輸入從事件中心或參考的資料，從 Blob 儲存體。"
keywords: "資料輸入, 串流資料"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a>新增資料流資料輸入或參考資料 tooa 資料流分析工作
了解如何設定串流分析資料來源 tooyour toohook 作業為資料流的資料輸入從事件中心或參考的資料，從 Blob 儲存體。

Azure 串流分析工作可以是連線的 tooone 資料輸入或更多，其中每個定義連線 tooan 現有資料來源。 當資料傳送 toothat 資料來源時，它是 hello 資料流分析工作所耗用，而且處理即時串流資料。 資料流分析第一個類別與已經整合[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)和[Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)內部和外部 hello 作業的訂用帳戶。

這篇文章是 hello 的步驟[Stream Analytics 學習路徑](/documentation/learning-paths/stream-analytics/)。

## <a name="data-input-streaming-data-and-reference-data"></a>資料輸入：資料流處理資料及參考資料
串流分析有兩種不同的輸入類型：資料流和參考資料。

* **資料流**： 串流分析工作必須包含至少一個資料資料流輸入的 toobe hello 工作所耗用及轉換。 支援將 Azure Blob 儲存體和 Azure 事件中樞當成資料流輸入來源。 Azure 事件中心是使用的 toocollect 事件資料流，從連接的裝置、 服務和應用程式。 Azure Blob 儲存體可用於擷取大量資料作為資料流的輸入來源。  
* **參考資料**：串流分析會支援稱為參考資料的第二類型輔助輸入。  為移動中的相對於 toodata，此資料是靜態或慢性變更。  它通常用來執行查閱和相互關聯資料流 toocreate 更豐富的資料集。  Azure Blob 儲存體正在 hello 只支援輸入的參考資料來源。  

tooadd tooyour 輸入資料流分析工作：

1. Hello Azure 入口網站中按一下**輸入**，然後按一下**將輸入**Stream Analytics 工作。
   
    ![Azure 傳統入口網站 - 新增輸入。](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    在 hello Azure 入口網站按一下 hello**輸入**磚中的資料流分析工作。  
   
    ![Azure 入口網站 - 新增資料輸入。](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. 指定 hello hello 輸入型別： 任一**資料流**或**參考資料**。
   
    ![新增 hello 正確的資料輸入、 資料流或參考](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![新增 hello 正確的資料輸入、 資料流或參考](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. 如果建立資料流輸入，指定 hello hello 輸入的來源類型。  由於目前僅支援 Blob 儲存體，因此在參考資料建立期間可以省略此步驟。
   
    ![加入資料流資料輸入](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![加入資料流資料輸入](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. 提供此輸入中的 hello 輸入別名 方塊中的易記名稱。  此名稱將用於作業的之後會在 toorefer toohello 輸入的查詢。
   
    填寫 hello rest hello 所需的連接屬性 tooconnect tooyour 資料來源。 這些欄位會因輸入類型和來源類型而有所不同，詳細定義請見 [此處](stream-analytics-create-a-job.md)。  
   
    ![新增事件中樞資料輸入](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. 指定 hello hello 輸入資料的序列化設定：
   
   * 確定您的查詢運作 hello 方式您預期，toomake 指定 hello**事件序列化格式**的內送資料。  支援的序列化格式為 JSON、CSV 及 Avro。
   * 確認 hello**編碼**hello 資料。  Utf-8 是 hello 此時只支援編碼格式。
     
     ![Hello 資料輸入的資料序列化設定](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Hello 資料輸入的資料序列化設定](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. 完成之後 hello 輸入的建立，資料流分析會確認可連線 toohello 輸入的來源。  您可以在 hello 通知中樞的檢視 hello hello 測試連接作業狀態。
   
    ![測試連接的資料流資料輸入 hello](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![測試連接的資料流資料輸入 hello](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a>取得資料流處理資料輸入的協助
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

