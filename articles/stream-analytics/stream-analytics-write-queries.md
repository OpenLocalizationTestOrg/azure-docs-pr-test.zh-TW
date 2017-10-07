---
title: "在 Stream Analytics aaaHow toowrite 查詢 |Microsoft 文件"
description: "在串流分析中編寫查詢及查詢資料 | 學習路徑區段。"
keywords: "toowrite 查詢、 查詢的資料、 如何撰寫查詢時，撰寫查詢"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a>Toowrite 在 Stream Analytics 中查詢的方式
撰寫資料流處理邏輯，在 Azure Stream Analytics 查詢會實作為 「 常設查詢 」 工作開始的資料到達 hello 作業執行之前所定義。 hello 資料轉換是類似 SQL 的查詢語言表達，這是大部分 T-SQL 某些子集新增語言擴充功能，例如[Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx)用 tooexpress 時態語意。

## <a name="writing-queries"></a>編寫查詢：
1. 在資料流分析工作 hello Azure 管理入口網站中，按一下**查詢**。
   
    ![選取查詢](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    在 hello Azure 入口網站，按一下 **查詢**。
   
    ![選取查詢預覽](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. 新的作業會讓您開始使用查詢範本 toohelp。 hello 查詢範本會執行 「 通過 」 查詢 hello 輸出至該專案中輸入事件的所有欄位。  
   
   * 如果您已經定義至少一個輸入和輸出工作，您可以取代 hello 預留位置"[YourOutputAlias]"和"[YourInputAlias]"欄位的輸入和輸出 [您希望使用先 hello hello 別名。 此外，您仍然可以撰寫，並在 hello Azure 傳統入口網站中測試您的查詢，而不需 hello 工作定義輸入和輸出。
   * 如果您想 tooperform 更多的處理，比簡單的傳遞，您可以編輯 hello 查詢定義。 撰寫查詢，開始 tooget 看看一些常用的查詢擷取模式[這裡](stream-analytics-stream-analytics-query-patterns.md)。  
   
   ![查詢資料視窗](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a>正在 toovalidate 查詢資料：
您可以測試您的查詢行為如預期般 hello 瀏覽器中執行一或多個本機 JSON 檔案包含測試資料。 這不會啟動 hello 作業，或是有任何的計費影響。

> [!NOTE]
> 目前瀏覽器中查詢不支援測試 hello Azure 入口網站中。  
> 
> 

1. 請確定 hello （否則 hello [測試] 按鈕將會停用） 的查詢中沒有任何錯誤，然後按一下hello [測試] 按鈕。  
   
   ![查詢資料測試](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. 您將會針對每個 hello 輸入 hello 查詢中參考的提示的 toospecify 檔案。 在此範例中，hello 範本查詢就會維持為是，因此 hello 對話方塊會提示輸入名為"yourinputalias"。  
   
   ![輪詢資料查詢](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. 瀏覽 tooa 測試檔案。 會提供數個範例檔案[github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) ，您也可以從您自己的資料資料流輸入 hello hello 輸入 索引標籤上的範例資料函式透過擷取資料範例。  
   
   ![查詢輸入](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. 在關閉之後 hello 對話方塊，您的查詢將會執行 hello 測試資料，您會看到在 hello hello [查詢] 頁面底部的 hello 結果。  
   
   ![查詢摘要](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

