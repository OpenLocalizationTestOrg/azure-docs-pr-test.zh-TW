---
title: "aaaStream 分析的版本資訊 |Microsoft 文件"
description: "串流分析版本資訊"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e59f893-cd2c-43fb-9eca-c146ce637203
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/03/2017
ms.author: jeffstok
ms.openlocfilehash: 1426ebc260be19fbde60518b25501fe53d908d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-release-notes"></a>串流分析版本資訊

## <a name="notes-for-06142017-update-of-stream-analytics-tools-for-visual-studio"></a>適用於 Visual Studio 的 Azure 串流分析工具 2017/06/14 更新注意事項
此更新適用於我們的 Visual Studio Tools。 這個版本包含下列新功能的 hello。

| Title | 說明 |
| --- | --- |
| Java 指令碼編輯器支援 |您可以享用 hello 原生 java 指令碼建立您的 java 指令碼函式之後的編輯器體驗。|
| 檢視作業執行階段錯誤訊息 | 如果作業執行期間發生執行階段錯誤，則您可以調整 hello 顯示的時段 hello 錯誤 索引標籤中檢視它們。 依預設它會顯示 hello 錯誤訊息的最近 30 分鐘。 |
| 本機測試輸入的 CSV 和 Avro 支援 | 除了 JSON，現在您還可以使用 CSV 和 Avro 檔案格式作為本機測試輸入。|

## <a name="notes-for-05032017-update-of-stream-analytics"></a>串流分析 05/03/2017 版本的注意事項
此更新是我們的疑難排解文件版本。

hello[疑難排解指南](stream-analytics-troubleshooting-guide.md)和其他文件發行。 請檢閱，並歡迎提供意見反應。

## <a name="notes-for-04242017-update-of-stream-analytics-tools-for-visual-studio"></a>適用於 Visual Studio 的 Azure 串流分析工具 2017/04/24 更新注意事項
此更新適用於我們的 Visual Studio Tools。 這個版本包含下列新功能的 hello。

| Title | 說明 |
| --- | --- |
| 在 Visual Studio 中檢視本機測試結果 | tooview hello 輸出結果 hello 本機測試，只要按下 ENTER hello 輸出主控台視窗中的或關閉它。 hello 結果將會顯示在 Visual Studio 視窗中資料表格式。 |
| 以 JSON 格式輸出本機結果 | 當您執行本機測試時，如 JSON 和 CSV 檔案格式，將會產生 hello 輸出結果。 |
| 預覽 Blob/資料表儲存體輸入/輸出資料 | 用滑鼠右鍵按一下在 blob 或表格儲存體輸入/輸出 hello 工作檢視中，您可以非常輕鬆地預覽 hello 在 Visual Studio 內的資料。 |
| 檢視輸入/輸出的錯誤訊息 | 如果某些執行階段錯誤相關的 tooyou 工作輸入或輸出，它將會顯示在其中您可以在其將滑鼠停留的 hello 工作圖表上 toosee hello 詳細的錯誤訊息。|


## <a name="notes-for-02012017-release-of-stream-analytics"></a>串流分析 2017/02/01 版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| 簡介 JavaScript 使用者定義函數 (UDF) |[Java 使用者定義函數](stream-analytics-javascript-user-defined-functions.md)現已可為建立查詢提供額外的彈性。 |
| 簡介 Visual Studio 和串流分析的工具 |[Visual Studio 適用的工具](stream-analytics-tools-for-visual-studio.md)現已可供進行偵錯，並具備更強大的功能。 |
| 簡介診斷記錄 |[診斷記錄](stream-analytics-job-diagnostic-logs.md)現已具有額外的疑難排解選項。 |
| 簡介 GeoSpatial 函數 |[GeoSpatial 函數](http://msdn.microsoft.com/library/mt778980(Azure.100).aspx)現已正式推出。 |

## <a name="notes-for-04152016-release-of-stream-analytics"></a>串流分析 2016 年 4 月 15 日版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| Power BI 輸出的一般可用性 |[Power BI 輸出](stream-analytics-power-bi-dashboard.md)現在已正式運作。 Power BI 的 hello 90 天的授權到期日已移除。 如需授權中需要更新 toobe 案例詳細資訊，請參閱 hello[更新授權](stream-analytics-power-bi-dashboard.md#renew-authorization)區段建立的 Power BI 儀表板。 |

## <a name="notes-for-03032016-release-of-stream-analytics"></a>串流分析 2016/03/03 版的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| 新的串流分析查詢語言項目 |SAQL 現在有 [GetType](https://msdn.microsoft.com/library/azure/mt643890.aspx "GetType MSDN 頁面")、[TRY_CAST](https://msdn.microsoft.com/library/azure/mt643735.aspx "TRY_CAST MSDN 頁面") 以及 [REGEXMATCH](https://msdn.microsoft.com/library/azure/mt643891.aspx "REGEXMATCH MSDN 頁面")。 |

## <a name="notes-for-12102015-release-of-stream-analytics"></a>串流分析 2015 年 12 月 10 日版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| REST API 版本更新 |hello REST API 版本已更新的 too2015-10-01。 您可在[串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)和[在串流分析中整合機器學習服務](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)的 MSDN 中取得詳細資料。 |
| Azure 機器學習的整合 |此版本開始支援 Azure 機器學習的使用者定義函數。 請參閱 hello[教學課程](stream-analytics-machine-learning-integration-tutorial.md)如需詳細資訊，以及 hello[一般部落格通知](http://blogs.technet.com/b/machinelearning/archive/2015/12/10/apply-azure-ml-as-a-function-in-azure-stream-analytics.aspx)。 |

## <a name="notes-for-11122015-release-of-stream-analytics"></a>串流分析 2015/11/12 版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| SELECT 的新行為 |選取在 Stream Analytics 中已擴充的 tooallow * 做為巢狀記錄的屬性存取子。 如需進一步資訊，請參閱 [http://msdn。microsoft。com/library/mt622759。aspx](http://msdn.microsoft.com/library/mt622759.aspx "複雜資料類型")。 |

## <a name="notes-for-10222015-release-of-stream-analytics"></a>串流分析 2015/10/22 版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| 其他查詢語言功能 |資料流分析已擴展 hello 查詢語言包含下列功能的 hello: [ABS](https://msdn.microsoft.com/library/azure/mt574054.aspx)， [CEILING](https://msdn.microsoft.com/library/azure/mt605286.aspx)， [EXP](https://msdn.microsoft.com/library/azure/mt605289.aspx)， [FLOOR](https://msdn.microsoft.com/library/azure/mt605240.aspx)，[電源](https://msdn.microsoft.com/library/azure/mt605287.aspx)，[登](https://msdn.microsoft.com/library/azure/mt605290.aspx)，[方](https://msdn.microsoft.com/library/azure/mt605288.aspx)，和[SQRT](https://msdn.microsoft.com/library/azure/mt605238.aspx)。 |
| 移除了彙總限制 |此版本中移除 15 個彙總的 hello 的限制在查詢中。 現在是每個查詢的彙總無限制 toohello 數目。 |
| 新增了 GROUP BY System.Timestamp 功能 |hello [GROUP BY](https://msdn.microsoft.com/library/azure/dn835023.aspx)函式現在允許任一 items> 或[System.Timestamp](https://msdn.microsoft.com/library/azure/mt598501.aspx)。 |
| 新增了適用於輪轉和跳動視窗的 OFFSET |根據預設，[輪轉](https://msdn.microsoft.com/library/azure/dn835055.aspx)和[跳動](https://msdn.microsoft.com/library/azure/dn835041.aspx)視窗已對準零點時間 (國際標準時間 0001 年 1 月 1 日上午 12:00:00)。 hello 新 （選擇性） 的參數 'offsetsize' 允許指定自訂位移 （或對齊）。 |

## <a name="notes-for-09292015-release-of-stream-analytics"></a>串流分析 2015/09/29 版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| Azure IoT Suite 公用預覽 |資料流分析會包含在 hello 公開預覽版的 Azure IoT 套件 hello。 |
| Azure 入口網站整合 |Hello Azure 管理入口網站中新增 toocontinued 是否存在，請在資料流分析會現在整合 hello [Azure 入口網站](https://azure.microsoft.com/overview/preview-portal/)。 請注意，目前是 hello 預覽入口網站中的資料流分析功能 hello 功能子集提供 hello Azure 管理入口網站中，但不支援瀏覽器中查詢測試，在 Power BI 輸出組態和 tooor 建立新的瀏覽您可以存取的訂用帳戶中的輸入和輸出資源。 |
| 支援 Cosmos DB 輸出 |資料流分析工作可以現在太輸出[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/)。 |
| 支援 IoT 中樞輸入 |串流分析作業現在可以內嵌來自 IoT 中樞的資料。 |
| 異質事件的時間戳記格式 |當單一資料流包含多個具有不同欄位中的時間戳記的事件類型時，您現在可以使用[TIMESTAMP BY](http://msdn.microsoft.com/library/mt573293.aspx)運算式 toospecify 不同的時間戳記欄位，每個案例。 |

## <a name="notes-for-09102015-release-of-stream-analytics"></a>資料流分析 2015/09/10 版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| 支援 PowerBI 群組 |資料與其他 Power BI 使用者共用，串流分析工作現在就可以撰寫太 tooenable[PowerBI 群組](stream-analytics-define-outputs.md#power-bi)Power BI 帳戶內。 |

## <a name="notes-for-08202015-release-of-stream-analytics"></a>串流分析 2015 年 8 月 20 日版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| 加入 LAST 函式 |hello[最後](http://msdn.microsoft.com/library/mt421186.aspx)函式現在已提供使用資料流分析工作，讓您在給定的時間範圍內的事件資料流 tooretrieve hello 最新事件。 |
| 新的陣列函數 |現在已可使用陣列函數 [GetArrayElement](http://msdn.microsoft.com/library/mt270218.aspx)、[GetArrayElements](http://msdn.microsoft.com/library/mt298451.aspx) 及 [GetArrayLength](http://msdn.microsoft.com/library/mt270226.aspx)。 |
| 新的記錄函數 |現在已可使用記錄函數 [GetRecordProperties](http://msdn.microsoft.com/library/mt270221.aspx) 和 [GetRecordPropertyValue](http://msdn.microsoft.com/library/mt270220.aspx)。 |

## <a name="notes-for-07302015-release-of-stream-analytics"></a>串流分析 07/30/2015 版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| 與 Azure 識別碼分離的 Power BI 組織識別碼 |此功能可為任何 Azure 帳戶類型 (Live ID 或組織識別碼) 下的 ASA 工作啟用 [Power BI 輸出](stream-analytics-power-bi-dashboard.md) 。 此外，您可以擁有 Azure 帳戶的組織識別碼，並使用另一個識別碼用於授權 Power BI 輸出。 |
| 支援服務匯流排佇列輸出 |現在您可以在「串流分析」工作中使用[服務匯流排佇列](stream-analytics-define-outputs.md#service-bus-queues)輸出。 |
| 支援服務匯流排主題輸出 |現在您可以在「串流分析」工作中使用[服務匯流排主題](stream-analytics-define-outputs.md#service-bus-topics)輸出。 |

## <a name="notes-for-07092015-release-of-stream-analytics"></a>串流分析 2015/07/09 版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| 自訂 Blob 輸出資料分割 |Blob 儲存體輸出現在可讓寫入輸出 blob 的選項 toospecify hello 頻率和 hello 結構與 hello 格式輸出資料路徑的資料夾結構。 |

## <a name="notes-for-05032015-release-of-stream-analytics"></a>串流分析 2015/05/03 版本的注意事項
這個版本包含下列更新的 hello。

| Title | 說明 |
| --- | --- |
| 增加次序錯誤允許的時間範圍的最大值 |hello hello 次序不對的容錯時間的最大大小現在是 59:59 (mm: ss) |
| JSON 輸出格式：以行分隔或陣列 |現在沒有選擇其中一個陣列的 JSON 物件，或以新行分隔的 JSON 物件當做輸出 tooBlob 存放裝置或事件中心 toooutput 時。 |

## <a name="notes-for-04162015-release-of-stream-analytics"></a>串流分析 2015/04/16 版本的注意事項
| 課程名稱 | 說明 |
| --- | --- |
| Azure 儲存體帳戶組態的延遲 |在 hello 的區域中第一次建立資料流分析工作，當您將會提示的 toocreate 新的儲存體帳戶，或指定監視該區域中的資料流分析工作的現有帳戶。 到期 toolatency 中設定監視，在相同的區域，30 分鐘內就會提示輸入 hello 指定第二個儲存體帳戶而不會顯示 hello hello 中建立另一個資料流分析工作最近曾經設定過 hello 監視儲存體中的其中一個帳戶下拉式清單。 tooavoid 建立不必要的儲存體帳戶、 等待 30 分鐘在 hello 的區域中佈建該區域中的其他工作之前的第一次建立作業之後。 |
| 工作升級 |在這個階段中，資料流分析不支援即時編輯 toohello 定義或執行工作的組態。 在順序 toochange hello 輸入、 輸出、 查詢、 小數位數或執行工作的組態，您必須先停止 hello 作業。 |
| 從輸入來源推斷而來的資料類型 |如果未使用 CREATE TABLE 陳述式，hello 輸入的類型衍生自輸入格式，例如從 CSV 的所有欄位都是字串。 欄位需要 toobe 明確轉換 toohello hello CAST 函數使用順序 tooavoid 類型不符的錯誤中的正確類型。 |
| 遺漏的欄位在輸出後會變成 null 值 |參考不存在於 hello 輸入來源的欄位，將會導致 hello 輸出事件中的 null 值。 |
| WITH 陳述式前面必須是 SELECT 陳述式 |在您的查詢中，SELECT 陳述式後面必須是 WITH 陳述式中定義的下列子查詢。 |
| 記憶體不足問題 |具有大型的容錯的次序不對事件及/或維護大量的狀態可能會造成記憶體不足，請產生作業中的 hello 作業 toorun 複雜查詢的資料流分析工作重新啟動。 hello 開始和停止作業會顯示在 hello 作業的作業記錄檔。 tooavoid 此行為，標尺 hello 查詢逾時是跨多個資料分割。 在未來版本中，將會藉由降低受影響之工作的效能 (而不是加以重新啟動)，來解決這項限制。 |
| 沒有裝載時間戳記的大型 Blob 輸入，可能會造成記憶體不足問題 |使用大型的檔案從 Blob 儲存體可能會造成資料流分析工作 toocrash 如果透過 TIMESTAMP BY 未指定時間戳記欄位。 tooavoid 這個問題，請保持小於 10 MB 的每個 blob 的大小。 |
| SQL Database事件容量限制 |當使用 SQL 資料庫做為輸出目標，非常大量的輸出資料可能會導致 hello 資料流分析工作 tootime 出。tooresolve 這個問題，請使用彙總或篩選運算子來減少 hello 輸出磁碟區，或改為做為輸出目標選擇 Azure Blob 儲存體或事件中心。 |
| PowerBI 資料集只能包含一個資料表 |PowerBI 不允許指定的資料集中存在多個資料表。 |

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
