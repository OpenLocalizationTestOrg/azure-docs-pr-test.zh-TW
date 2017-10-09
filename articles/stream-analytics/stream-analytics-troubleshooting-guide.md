---
title: "Azure Stream Analytics 的 aaaTroubleshooting 指南 |Microsoft 文件"
description: "如何 tootroubleshoot 串流分析工作"
keywords: "疑難排解指南"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Azure 串流分析的疑難排解指南

Azure Stream Analytics 疑難排解可能會出現 toobe 複雜工作第一眼看起來。 之後使用許多使用者，我們已建立此指南 toohelp 簡化 hello 程序，並移除 hello 猜測有關輸入、 輸出、 查詢和函式。

## <a name="troubleshoot-your-stream-analytics-job"></a>對您的串流分析作業進行疑難排解

疑難排解資料流分析工作的最佳結果，請使用下列指導方針的 hello:

1.  測試連線：
    - 請確認連線 tooinputs 和輸出使用 hello**測試連接**針對每個輸入及輸出 按鈕。

2.  檢查您的輸入資料：
    - 輸入資料的 tooverify 流入事件中樞，請使用[Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure 事件中心 （如果使用事件中樞輸入）。  
    - 使用 hello [**範例資料**](stream-analytics-sample-data-input.md)按鈕的每個輸入，並下載 hello 輸入的範例資料。
    - 檢查 hello 範例資料 toounderstand hello hello 資料圖形： hello 結構描述和 hello[資料型別](https://msdn.microsoft.com/library/azure/dn835065.aspx)。

3.  測試查詢︰
    - 在 hello**查詢**索引標籤上，使用 hello**測試**按鈕 tootest hello 查詢，並使用下載的 hello 範例資料太[測試 hello 查詢](stream-analytics-test-query.md)。 檢查任何錯誤，並嘗試 toocorrect 它們。
    - 如果您使用[ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx)，請確認 hello 事件有時間戳記大於 hello[工作開始時間](stream-analytics-out-of-order-and-late-events.md)。

4.  對應用程式進行偵錯：
    - 使用步驟重建 hello 逐漸從簡單的 select 陳述式 toomore 複雜的彙總的查詢。 toobuild 向上 hello 查詢邏輯逐步解說，使用[WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx)子句。
    - 使用[SELECT INTO](stream-analytics-select-into.md) toodebug 查詢步驟。

5.  排除常見的錯誤，例如︰
    - A [**其中**](https://msdn.microsoft.com/library/azure/dn835048.aspx) hello 查詢子句篩選掉所有的事件，防止產生任何輸出。
    - 當您使用視窗函式時，等到 hello 整個視窗持續時間 toosee hello 查詢的輸出。
    - hello 事件時間戳記之前 hello 工作開始時間，因此，正在捨棄事件。

6.  使用事件順序︰
    - 如果所有 hello 可以正常運作的上一個步驟，請移至 toohello**設定**刀鋒視窗，然後選取[**事件順序**](stream-analytics-out-of-order-and-late-events.md)。 請確定此原則已設定為適用於您的情況。 hello 原則是*不*時使用 hello 套用**測試**按鈕 tootest hello 查詢。 這個結果會測試在瀏覽器與生產環境中執行 hello 工作之間的差異。

7.  使用計量進行偵錯：
    - 如果 hello 預期的持續時間 （根據 hello 查詢） 之後，您會不取得任何輸出，請嘗試下列 hello:
        - 查看[**監視度量**](stream-analytics-monitoring.md)上 hello**監視器** 索引標籤。Hello 值會彙總，因為 hello 度量會延遲幾分鐘的時間。
            - 如果輸入事件 > 0，hello 作業是無法 tooread 輸入的資料。 如果輸入事件不是 > 0，然後︰
                - toosee hello 資料來源是否為有效的資料，請檢查它使用[Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a)。 如果 hello 作業使用事件中心做為輸入，適用於這項檢查。
                - 檢查 toosee hello 資料序列化格式資料的編碼方式並不會如預期般。
                - 如果 hello 作業使用事件中心，請檢查 toosee hello hello 訊息本文是否*Null*。
            - 如果資料轉換錯誤 > 0，上升 hello 下列條件可能會為 true:
                - hello 作業可能不是能 toode-序列化 hello 事件。
                - hello 事件結構描述可能不符合定義的 hello 或預期的結構描述的 hello hello 查詢中的事件。
                - hello 的一些 hello 事件中的 hello 欄位的資料類型可能不符合預期。
            - 如果執行階段錯誤 > 0，這表示該 hello 工作可以接收 hello 資料，但處理 hello 查詢時產生錯誤。
                - toofind hello 錯誤，請移 toohello[稽核記錄檔](../azure-resource-manager/resource-group-audit.md)和篩選*失敗*狀態。
            - 如果 InputEvents > 0 和 OutputEvents = 0，則表示 hello 下列其中一項成立：
                - 查詢處理產生了零個輸出事件。
                - 事件或其欄位可能格式錯誤，因此在查詢處理後導致零個輸出。
                - hello 工作已無法 toopush 資料 toohello[輸出接收](stream-analytics-select-into.md)連線或驗證的原因。
        - 在所有 hello 先前所述錯誤情況下，作業記錄檔訊息的說明 （包括發生什麼事，） 的其他詳細資料的情況下 hello 查詢邏輯篩除的所有事件除外。 如果多個事件的 hello 處理產生錯誤，記錄資料流分析記錄檔 hello 的 hello 相同的型別 tooOperations 10 分鐘內的前三個錯誤訊息。 接著會隱藏其他完全相同的錯誤並顯示錯誤訊息，內容為「錯誤發生次數太頻繁，因此隱藏這些錯誤」。

8. 使用稽核和診斷記錄進行偵錯：
    - 使用[稽核記錄檔](../azure-resource-manager/resource-group-audit.md)，以及篩選 tooidentify 和偵錯錯誤。
    - 使用[作業診斷記錄](stream-analytics-job-diagnostic-logs.md)tooidentify 和偵錯錯誤。

9. 檢查有 hello 輸出：
    - Hello 工作狀態時*執行*，端視在 hello 查詢中，您可以看到 hello 接收資料來源中的 hello 輸出約定的 hello 持續時間。
    - 如果看不到要 tooa 特定的輸出類型的輸出，將他們重新導向 tooan 較不複雜，例如 Azure Blob 的輸出類型。 藉由使用儲存體總管，檢查 toosee 是否可以看見 hello 輸出。 此外，確認是否在 hello 輸出節流限制防止資料被接收。

10. 搭配使用資料流分析與作業圖表計量︰
    - tooanalyze 資料流動，且找出問題，使用 hello[具有度量的作業圖表](stream-analytics-job-diagram-with-metrics.md)。

11. 建立支援案例：
    - 最後，如果所有解決方案均失敗，請開啟 Microsoft 支援案例使用 hello 訂用帳戶 Id，其中包含您的工作。

## <a name="get-help"></a>取得說明

如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟

* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
