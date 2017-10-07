---
title: "與診斷記錄檔的 Azure Stream Analytics aaaTroubleshoot |Microsoft 文件"
description: "了解 tooanalyze 診斷記錄的方式從資料流分析作業在 Microsoft Azure 中。"
keywords: 
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
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a>使用析診斷記錄對 Azure 串流分進行疑難排解

有時候，Azure 串流分析作業會非預期地停止處理。 很重要的 toobe 無法 tootroubleshoot 這種事件。 hello 事件的原因可能是未預期的查詢結果、 連線 toodevices 或發生未預期的服務中斷。 hello 在 Stream Analytics 中診斷記錄檔可協助您找出問題 hello 原因，當發生，而減少復原時間。

## <a name="log-types"></a>記錄類型

串流分析提供開兩種記錄類型： 
* [活動記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (一律開啟)。 活動記錄可讓您對所執行作業有深入的了解。
* [診斷記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (可設定)。 診斷記錄可讓您更深入地了所有與作業相關的發生事件。 診斷記錄建立 hello 作業時，開始和結束時刪除 hello 作業。 它們所涵蓋事件 hello 作業更新時以及它正在執行。

> [!NOTE]
> 您可以使用服務，例如 Azure 儲存體、 Azure 事件中樞和 Azure Log Analytics tooanalyze 不合格資料。 您負責根據 hello 定價模型針對這些服務。
>

## <a name="turn-on-diagnostics-logs"></a>開啟診斷記錄

診斷記錄預設為 [關閉]。 tooturn 診斷記錄檔，完成下列步驟：

1.  登入 toohello Azure 入口網站，並移 toohello 串流處理作業 刀鋒視窗。 在 [監視] 下，選取 [診斷記錄]。

    ![刀鋒視窗中瀏覽 toodiagnostics 記錄檔](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  選取 [開啟診斷]。

    ![開啟診斷記錄](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  在 hello**診斷設定** 頁面上，針對**狀態**，選取**上**。

    ![變更診斷記錄的狀態](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  Hello 封存目標 （儲存體帳戶，事件中心，記錄分析） 您想要的設定。 然後，選取您想 toocollect （執行、 撰寫） 的記錄檔的 hello 類別。 

5.  儲存 hello 新的診斷組態。

hello 診斷組態才會大約 10 分鐘 tootake 生效。 在這之後，hello 記錄開始出現在設定的 hello 保存目標 (您可以看到這些 hello**診斷記錄檔**頁面):

![刀鋒視窗中瀏覽 toodiagnostics 記錄保存的目標](./media/stream-analytics-job-diagnostic-logs/image4.png)

如需有關診斷設定的詳細資訊，請參閱[收集並取用來自 Azure 資源的診斷資料](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)。

## <a name="diagnostics-log-categories"></a>診斷記錄類別

我們目前會擷取兩種診斷記錄︰

* **編寫**。 擷取會記錄事件的撰寫作業的相關的 toojob： 建立工作，加入和刪除輸入和輸出，新增和更新 hello 查詢、 啟動和停止 hello 作業。
* **執行**。 擷取作業執行期間發生的事件︰
    * 連線錯誤
    * 資料處理錯誤，包括：
        * 事件不符合 toohello 查詢定義 （不相符的欄位類型和值，遺漏的欄位，以及等等）
        * 運算式評估錯誤
    * 其他事件和錯誤

## <a name="diagnostics-logs-schema"></a>診斷記錄結構描述

所有記錄會儲存為 JSON 格式。 每個項目具有下列共通的字串欄位的 hello:

名稱 | 說明
------- | -------
分析 | 時間戳記 （UTC) 的 hello 記錄檔。
resourceId | Hello 作業的 hello 資源 ID 已進行，以大寫。 其中包括 hello 訂用帳戶 ID、 hello 資源群組，以及 hello 作業名稱。 例如，**/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**。
category | 記錄類別 (**執行**或**編寫**)。
operationName | Hello 作業所記錄的名稱。 例如，**傳送事件： SQL 輸出寫入失敗 toomysqloutput**。
status | Hello 作業的狀態。 例如，**失敗**或**成功**。
層級 | 記錄層級。 例如，**錯誤**、**警告**或**資訊**。
屬性 | 記錄項目特定詳細資料 (序列化為 JSON 字串)。 如需詳細資訊，請參閱下列各節的 hello。

### <a name="execution-log-properties-schema"></a>執行記錄屬性結構描述

執行記錄包含在執行串流分析作業期間所發生事件的資訊。 hello 結構描述的內容會因 hello 事件類型而有所不同。 目前，我們有下列類型的執行記錄的 hello:

### <a name="data-errors"></a>資料錯誤

這個類別的記錄檔，是 hello 作業正在處理資料時，就會發生任何錯誤。 這些記錄最常於資料讀取、序列化和寫入作業時建立。 這些記錄不包含連線錯誤。 連線錯誤視為一般事件。

名稱 | 說明
------- | -------
來源 | 輸入或輸出發生 hello 錯誤 hello 作業的名稱。
訊息 | 與 hello 錯誤相關聯的訊息。
類型 | 錯誤類型。 例如，**DataConversionError**、**CsvParserError** 或 **ServiceBusPropertyColumnMissingError**。
資料 | 包含有用的資料 tooaccurately 找出 hello hello 錯誤來源。 主旨 tootruncation，視大小而定。

根據 hello **operationName**值，資料錯誤有下列結構描述的 hello:
* **序列化事件**。 序列化事件會在事件讀取作業期間發生。 當 hello hello 輸入的資料不符合 hello 查詢結構描述的其中一個原因而發生：
    * *事件 (de) 期間的類型不符序列化*： 識別造成 hello 錯誤 hello 欄位。
    * *無法讀取事件、 無效的序列化*： 列出發生 hello 錯誤 hello 輸入資料中的 hello 位置的相關資訊。 包含 blob 名稱的 blob 輸入、 位移和 hello 資料的範例。
* **傳送事件**。 傳送事件會發生在寫入作業期間。 它們可識別 hello 造成 hello 錯誤的事件資料流處理。

### <a name="generic-events"></a>一般事件

一般事件涵蓋所有其他事件。

名稱 | 說明
-------- | --------
錯誤 | (選用) 錯誤資訊。 這通常是例外狀況資訊 (如果有的話)。
訊息| 記錄訊息。
類型 | 訊息類型。 將對應 toointernal 分類的錯誤。 例如，**JobValidationError**或 **BlobOutputAdapterInitializationFailure**。
相互關連識別碼 | [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier)可唯一識別 hello 作業執行。 所有的執行記錄項目從 hello 時間 hello 作業啟動，直到 hello 作業停止擁有 hello 相同**相互關聯識別碼**值。

## <a name="next-steps"></a>後續步驟

* [簡介 tooStream 分析](stream-analytics-introduction.md)
* [開始使用串流分析](stream-analytics-real-time-fraud-detection.md)
* [調整串流分析作業](stream-analytics-scale-jobs.md)
* [串流分析查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
