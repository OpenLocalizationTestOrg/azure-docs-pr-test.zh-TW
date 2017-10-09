---
title: "aaaUpgrading Azure Log Analytics toonew 記錄搜尋 |Microsoft 文件"
description: "hello 新的記錄分析查詢語言幾乎，，您可以參與 hello 公開預覽狀態。  本文說明 hello hello 新語言的優點以及如何 tooconvert 您的工作區。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7659c9d1467cab79d3a16e73b52b507ed281b002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-azure-log-analytics-workspace-toonew-log-search"></a>升級 Azure 記錄分析工作區 toonew 記錄搜尋

> [!NOTE]
> 升級 toohello 新的記錄分析查詢語言是目前選擇性讓您有時間太[掌握 hello 新語言](https://go.microsoft.com/fwlink/?linkid=856078)。  

hello 新的記錄分析查詢語言，而且您需要 tooupgrade 您工作區 tootake 利用到它。  本文說明 hello hello 新語言的優點以及如何 tooconvert 您的工作區。  如果您沒有選擇 tooupgrade 現在，則您的工作區也會持續 toooperate 就像永遠相同，但將在日後自動轉換。  設定該日期時，您會有足夠的時間和通知。

這篇文章提供 hello 新語言和 hello 升級程序的詳細資料。

## <a name="why-hello-new-language"></a>為什麼 hello 新語言？
我們了解的窗格中有任何轉換，並且我們不只變更它的 hello 有趣的 hello 查詢語言。  有多種原因所造成這項變更將會提供重大價值 tooour 記錄分析的客戶。

- **簡單但功能強大。** hello 新語言是更容易 toounderstand 和更多建構類似 tooSQL 喜歡 hello 舊版語言的自然語言。
- **完整的管線語言。**  hello 新語言具有比 hello 舊版語言更廣泛的管線功能。  幾乎任何輸出可以傳送的 tooanother 命令 toocreate 比先前可能更複雜的查詢。
- **搜尋時間欄位擷取。**  hello 新語言可支援比 hello 舊版語言更進階的執行階段導出欄位。  您可以使用複雜的計算擴充欄位，並再使用的 hello 導出欄位的其他命令，包括聯結和彙總。
- **進階聯結。**  hello 新語言，提供更進階比 hello 傳統的語言，包括多個欄位上的 hello 能力 toojoin 資料表聯結，使用內部和外部聯結，並聯結擴充欄位。
- **日期/時間函式。**  hello 新的語言比 hello 舊版語言，提供更多進階日期/時間函數。
- **智慧分析。**  hello 新語言提供進階演算法 tooevaluate 模式中的資料集並比較不同的資料集。
- **進階分析入口網站。**  hello 進階分析入口網站提供的分析功能不適用於 hello 記錄分析入口網站，包括多行編輯的查詢、 其他視覺效果，以及進階的診斷。
- **與其他應用程式的一致性。**  hello 新語言和 hello 進階的分析入口網站已用於 Application Insights 中的分析。  針對 Log Analytics 實作它，在 Azure 服務之間提供一致性。
- **與 Power BI 的更佳整合。** Hello 新語言中的查詢可能會匯出的 tooPower BI Desktop，因此您可以利用其豐富的資料轉換功能。
- **更多功能。** 請參閱 toohello [Azure 記錄分析查詢語言](https://docs.loganalytics.io)完整的詳細資訊及教學課程 hello 新語言的站台。


## <a name="when-can-i-upgrade"></a>何時可以升級？
因此，可能會使用之前其他某些區域中 hello 升級將會在所有的 Azure 地區推出。  您會知道您的工作區時可用的 toobe 升級時您邀請您 tooupgrade 工作區的 hello 頂端看到 hello 紫色橫幅。

![升級 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>升級時會發生什麼事？
當您轉換您的工作區時，任何儲存的搜尋、 警示規則，而且您已建立以 hello 檢視表設計工具的檢視會自動轉換的 toohello 新語言。  包含在方案中的搜尋不會自動轉換，但您開啟程式時，它們改為在 hello 立即轉換。  這是完全透明 tooyou。

## <a name="can-i-go-back-after-i-upgrade"></a>升級之後可以回復嗎？
當您升級時，會進行工作區的完整備份，包含所有已儲存搜尋、警示規則和檢視的快照集。  這可讓您 toorestore 如果您應該稍後想要您舊的工作區。

toorestore 舊版工作區中，跳過**設定**工作區中，然後**升級摘要**。  然後，您可以選取 hello 選項太**還原舊版的工作區**。  

![還原舊版](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-hello-upgrade"></a>如何執行 hello 升級？
當您看見 hello 紫色橫幅頂端 hello hello 入口網站時，您可以升級您的工作區。  

1.  指出 hello 紫色橫幅上的 啟動 hello 升級程序**進一步了解及升級**。<br>![升級 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  閱讀 hello 其他 hello 升級資訊 hello 升級的資訊 頁面上。<br>![升級 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  按一下**立即升級**toostart hello 升級。<br>![升級 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>Hello 右上角的 [通知] 方塊會顯示 hello 狀態。<br>![升級 5](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  這樣就大功告成了！  介紹 toohello 記錄搜尋頁面 toohave 看看您的升級工作區。<br>![升級 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

如果您遇到問題，導致 hello 升級 toofail，您可以移 toohello[討論區論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights)並張貼您的問題或[建立支援要求](../azure-supportability/how-to-create-azure-support-request.md)從 hello Azure 入口網站。

## <a name="how-do-i-learn-hello-new-language"></a>如何了解 hello 新語言？
因為它由多個服務，所以我們建立了[外部網站 toohost hello 文件](https://docs.loganalytics.io/)hello 新語言。  這包括教學課程、 範例和您創造的成果 toospeed 完整參考 toohelp。 您可以逐步進行教學課程中的 hello 在新的語言[入門查詢](https://go.microsoft.com/fwlink/?linkid=856078)以及存取位於 hello 語言參考[記錄分析查詢語言](https://go.microsoft.com/fwlink/?linkid=856079)。  

如果您已經熟悉以 hello 舊版記錄分析查詢語言，，然後您可以使用 hello 語言轉換器 tooyour 工作區加入 hello 升級的一部分。

只在舊版的查詢中輸入，然後按一下**轉換**toosee hello 翻譯版本。  接著，您可以按一下 hello 搜尋按鈕 toorun hello 搜尋或複製並貼上查詢轉換的 hello toouse，例如警示規則的任何其他地方。

![語言轉換器](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>後續步驟
- 簽出[hello 新語言上的教學課程](https://go.microsoft.com/fwlink/?linkid=856078)。
- 逐步解說[使用 hello 記錄搜尋網站上的教學課程](log-analytics-log-search-log-search-portal.md)與 hello 新的查詢語言。
- 取得新簡介 toohello [Advanced Analytics 入口網站](https://go.microsoft.com/fwlink/?linkid=856587)。
