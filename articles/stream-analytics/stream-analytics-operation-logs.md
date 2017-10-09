---
title: "使用中資料流分析作業及服務記錄檔的 aaaDebug |Microsoft 文件"
description: "如何 toouse 資料流分析作業記錄檔"
keywords: "服務記錄檔"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a>使用服務和作業記錄檔對串流分析工作進行偵錯
所有 Azure 服務供應器的操作記錄訊息 toousers toorecord 詳細資料相關的 toomanagement 作業。 在 Azure Stream Analytics 中，這項資訊可用以進行偵錯，例如一段時間，從開始 tooprocessing toooutput 檢視工作狀態、 工作進度和失敗作業的訊息 tootrack hello 進度。

## <a name="find-operation-logs-in-hello-azure-management-portal"></a>尋找 hello Azure 管理入口網站中的作業記錄檔
作業記錄檔可用兩種方式來存取：  

* Hello 資料流分析工作的儀表板  
* Hello Azure 傳統入口網站中管理服務  

## <a name="dashboard-of-hello-stream-analytics-job"></a>Hello 資料流分析工作的儀表板
連結 toohello 對應的資料流分析工作的記錄檔會顯示 hello 作業儀表板 索引標籤上。如果您按一下該連結時，它會設定 hello 篩選，它會顯示該特定工作的最新記錄檔的方式。

  ![選取管理服務記錄檔](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a>管理服務
toomanually 巡覽 toohello 作業記錄檔資料流分析和 hello Azure 傳統入口網站中的其他服務：

1. 按一下**管理服務**在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 選取**Stream Analytics**如**類型**和 hello hello 作業名稱**服務名稱**。  
   
   ![選取串流分析](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a>找到 hello Azure 入口網站的稽核記錄
按一下 toofind hello Azure 入口網站中的資料流分析工作的操作記錄檔**瀏覽**，然後選取 **稽核記錄檔**。

  ![Azure 入口網站選取串流分析](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

這會開啟刀鋒視窗中顯示來自 hello 事件的所有資源的過去 7 天您訂用帳戶中。  您可以篩選指定類型或時間範圍內的 toosee 事件即可 hello**篩選**命令。

  ![Azure 入口網站選取串流分析](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a>取得記錄檔詳細資料
您可以篩選由時間範圍和狀態 tooview hello 記錄您的工作。

在 hello Azure 管理入口網站中，按一下 hello**詳細資料**底部 hello hello 視窗 tooview 按鈕所選事件的詳細。 

  ![選取詳細資料](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

在 hello Azure 入口網站中，按一下 記錄檔項目 toosee hello 詳細內文中的事件。

  ![Azure 入口網站選取詳細資料](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

您可以從該處，開啟 hello**詳細**刀鋒視窗上 hello 事件即可。

  ![Azure 入口網站選取詳細資料](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a>偵錯失敗的工作
在 hello Azure 管理入口網站中，按一下 hello 搜尋圖示並輸入 '失敗'。 這樣可以找出所有包含失敗項目的記錄檔。 

  ![針對失敗的工作進行偵錯](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

在 hello Azure 入口網站，您可以篩選層級的訊息 tooview**重大**事件。

  ![Azure 入口網站偵錯](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

您可以選取任何一種 hello 失敗，並按一下 hello**詳細資料**hello 錯誤更多資訊。  某些錯誤訊息也會提供有關如何 toomitigate hello 問題的資訊。 

  ![Operation Details](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

萬一您需要 toocontact[支援](https://azure.microsoft.com/support/options/)或提供資訊 toohello 小組透過 hello [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)，請注意 hello 作業的詳細資訊，特別是 hello**相互關聯識別碼**. 

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

