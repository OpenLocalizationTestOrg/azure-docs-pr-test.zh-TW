---
title: "aaaHow tooconfigure 資料輸出資料流分析作業 |Microsoft 文件"
description: "設定串流分析工作的輸出 | 學習路徑區段。"
keywords: "資料輸出, 資料移動"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>Tooconfigure 資料輸出資料流分析工作的方式

Azure 串流分析工作可以是連線的 tooone 或更多的資料輸出，定義連接 tooan 現有資料接收。 串流分析工作處理，並將內送資料轉換，因為資料輸出事件資料流寫入 tooyour 工作的輸出。

使用的 toosource 即時儀表板或警示、 觸發程序的資料移動工作流程或只是供稍後處理批次的封存資料，可以是資料流分析資料輸出。 串流分析與數個 Azure 服務具有第一級的整合，將在此詳述。

tooadd 輸出 tooyour 資料流分析工作：

1. 在 hello [Azure 入口網站](https://portal.azure.com)，開啟您的工作，然後按一下**輸出**，然後按一下**新增**在 hello 輸出刀鋒視窗中出現。
   
    ![加入輸出](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. 提供在 hello 此輸出的易記名稱**輸出別名**方塊。 這個名稱可以用於作業的查詢，之後會在 toorefer toohello 輸出。  
   
    在所需的 hello 連接屬性 tooconnect tooyour 輸出 hello 其餘部分填滿。  這些欄位會因輸出類型而有所不同，其詳細定義在這裡。  
   
    ![選擇資料移動類型](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. 根據 hello 輸出類型，您可能需要的 toospecify hello 資料已序列化或格式化的方式。 記載 hello 特定的序列化設定每個輸出類型。
   
    填寫 hello rest hello 所需的連接屬性 tooconnect tooyour 資料來源。 這些欄位變更類型的輸入和來源的類型，且已定義在 hello 詳細[建立作業的發行項](stream-analytics-create-a-job.md)。  

> [!Note]
>
> 任何輸出項目加入的 toohello 的作業，必須先建立 hello 作業已啟動，而且流動開始事件。 比方說，如果您使用 Blob 儲存體做為輸出時，hello 作業將不會自動建立儲存體帳戶。 它需要 toobe hello ASA 工作啟動之前，由 hello 使用者所建立。
> 
 

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

