---
title: "aaaHow toocreate 資料流分析的資料分析處理作業 |Microsoft 文件"
description: "為串流分析建立資料分析處理工作 | 學習路徑區段。"
keywords: "資料分析處理"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a>如何 toocreate 處理資料分析工作的資料流分析
在 Azure Stream Analytics hello 最上層資源是串流分析工作。  它包含一或多個輸入資料來源、 表達 hello 資料轉換、 查詢和結果會寫入一或多個輸出為目標。 這些一起可讓 hello 使用者 tooperform 資料分析的資料流資料處理實例。

toostart 使用 Stream Analytics 中，開始建立新的資料流分析工作。  請注意這個動作沒有任何的計費方式，直到 hello 工作已啟動。

1. 登入線上 hello [Azure 傳統入口網站](http://manage.windowsazure.com)或 hello [Azure 入口網站](https://portal.azure.com/)。
2. Hello 入口網站中：**按一下 新增**，然後按一下 **Data Services**或**資料分析**根據您的入口網站，然後按一下**Azure Stream Analytics**或**串流分析**然後**快速建立**。
   
   ![資料分析處理工作精靈](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![建立資料分析處理工作](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. 指定 hello hello 資料流分析工作所需的組態。
   
   * 在 hello**工作名稱**方塊中，輸入名稱 tooidentify hello 資料流分析工作。 當 hello**工作名稱**驗證時，綠色的核取記號會出現在 hello 工作名稱 方塊。 hello**工作名稱**可能只包含英數字元和 hello '-' 字元，而且必須介於 3 到 63 個字元之間。
   * 使用**區域**hello Azure 入口網站中或**位置**在 hello Azure 入口網站 toospecify hello toorun hello 作業所在的地理位置。
   * 如果使用 hello Azure 入口網站，請選取或建立 hello 為儲存體帳戶 toouse**區域監視儲存體帳戶**。 這個儲存體帳戶是使用的 toostore 監視在此區域中執行的所有串流分析工作的資料。
   * 如果使用 hello Azure 入口網站，指定新的或現有的**資源群組**toohold 相關聯的應用程式的資源。
4. 一旦設定 hello 新的資料流分析工作選項，按一下**建立串流分析工作**。 可能需要幾分鐘，讓建立 hello 資料流分析工作 toobe。 toocheck hello 狀態，您可以監視 hello 通知中樞中的 hello 進度。
   
   ![資料分析處理作業通知中樞](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure 入口網站中資料分析處理作業的建立作業](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. hello 新作業將會顯示狀態為**Created**。 請注意該 hello**啟動**按鈕已停用。 Hello 作業開始之前，請設定 hello 作業輸入、 查詢和輸出。
   
   ![資料分析處理的作業狀態](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure 入口網站中資料分析處理的作業狀態](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

