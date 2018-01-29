---
title: "將資料輸入新增至串流分析工作中 | Microsoft Docs"
description: "了解如何從事件中樞或 Blog 儲存體的參考資料，將資料來源連接至串流分析工作，以做為資料流處理資料輸入。"
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
ms.openlocfilehash: 7a4eb8642a0496e126b79724b4048bae7cc15a68
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-to-a-stream-analytics-job"></a>將資料流處理資料輸入或參考資料新增至串流分析工作
了解如何從事件中樞或 Blob 儲存體的參考資料，將資料來源連接至串流分析工作，以做為資料流處理資料輸入。

Azure 串流分析工作可以連線至一或多個資料輸入，且每個資料輸入都定義了一個與現有資料來源之間的連線。 當資料傳送到該資料來源時，串流分析工作會即時取用該資料，並把它當做串流資料來處理。 「串流分析」與 [Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/)及 [Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)整合性極佳，不論它們是在工作訂用帳戶內還是工作訂用帳戶外。

本文章是 [串流分析學習路徑](/documentation/learning-paths/stream-analytics/)中的一個步驟。

## <a name="data-input-streaming-data-and-reference-data"></a>資料輸入：資料流處理資料及參考資料
串流分析有兩種不同的輸入類型：資料流和參考資料。

* **資料流**：串流分析工作必須至少包含一個由工作取用和轉換的資料流輸入。 支援將 Azure Blob 儲存體和 Azure 事件中樞當成資料流輸入來源。 Azure 事件中樞是用於從多個連接的裝置和服務收集事件資料流。 Azure Blob 儲存體可用於擷取大量資料作為資料流的輸入來源。  
* **參考資料**：串流分析會支援稱為參考資料的第二類型輔助輸入。  與動態資料相反，這種資料是靜態或變化緩慢的。  其通常與資料流搭配使用來執行查閱和關聯，以建立更豐富的資料集。  在預覽版本中，Azure Blob 儲存體是目前唯一支援當成參考資料的輸入來源。  

若要將輸入加入串流分析工作中：

1. 在 Azure 入口網站中按一下 [輸入]，然後按一下串流分析工作的 [新增輸入]。
   
    ![Azure 入口網站-將輸入。](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    在 Azure 入口網站中，按一下串流分析工作的 [輸入]  磚。  
   
    ![Azure 入口網站 - 新增資料輸入。](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. 指定輸入類型：**資料流**或**參考資料**。
   
    ![新增正確的資料輸入, 串流或參考](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![新增正確的資料輸入, 串流或參考](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. 如果要建立資料流輸入，請指定輸入的來源類型。  由於目前僅支援 Blob 儲存體，因此在參考資料建立期間可以省略此步驟。
   
    ![加入資料流資料輸入](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![加入資料流資料輸入](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. 在 [輸入別名] 方塊中，替這個輸出取一個易記的名稱。  此名稱稍後將在作業查詢中用作指稱輸入。
   
    填寫其餘必要的連接屬性，以連接到資料來源。 這些欄位會因輸入類型和來源類型而有所不同，詳細定義請見 [此處](stream-analytics-create-a-job.md)。  
   
    ![新增事件中樞資料輸入](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. 指定輸入資料的序列化設定：
   
   * 若要確定查詢會依照您所預期的方式處理，請指定傳入資料的 **事件序列化格式** 。  支援的序列化格式為 JSON、CSV 及 Avro。
   * 確認資料的 **編碼** 。  UTF-8 是目前唯一支援的編碼格式。
     
     ![資料輸入的資料序列化設定](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![資料輸入的資料序列化設定](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. 完成建立輸入之後，串流分析會確認其是否可以連接到輸入來源。  您可以在 [通知中樞] 中檢視測試連接作業的狀態。
   
    ![測試串流資料輸入的連線](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![測試串流資料輸入的連線](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a>取得資料流處理資料輸入的協助
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [Azure Stream Analytics 介紹](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

