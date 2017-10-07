---
title: "使用 Azure Application Insights 中的使用者傳送 aaaAnalyze 使用者瀏覽模式 |Microsoft 文件"
description: "分析使用者 hello 網頁和 web 應用程式的功能之間的瀏覽。"
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a>在 Application Insights 中使用使用者流程分析使用者瀏覽模式

![Application Insights 使用者流程工具](./media/app-insights-usage-flows/flows.png)

hello 使用者流動工具以視覺化方式檢視使用者 hello 網頁和您的站台的功能之間的瀏覽。 適合用來回答問題，例如：
* 使用者如何離開網站上的分頁？
* 使用者在網站上的分頁按了什麼？
* Hello 會將使用者變換從您的網站的大部分？
* 有其中使用者重複 hello 相同的動作重複的位置嗎？

hello 使用者流動工具將會啟動從初始頁面檢視或您指定的事件。 顯示指定此頁面檢視或自訂的事件，請使用者傳送 hello 頁面檢視和自訂之後在工作階段中，兩個步驟之後，依此類推，立即傳送使用者的事件。 不同粗細的線條顯示每個路徑被使用者追蹤的次數。 特殊的 「 結束工作階段 」 節點顯示的使用者人數任何頁面檢視或自訂的事件之後傳送 hello 前面節點中，反白顯示的使用者可能保留您的網站。



> [!NOTE]
> Application Insights 資源必須包含頁面檢視或自訂事件 toouse hello 使用者流動工具。 [了解如何註冊您的應用程式 toocollect 頁面 tooset 檢視自動以 hello Application Insights JavaScript SDK](app-insights-javascript.md)。
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a>從選擇初始分頁檢視或自訂事件開始

![為使用者流程選擇初始事件](./media/app-insights-usage-flows/flows-initial-event.png)

tooget 啟動回答問題與 hello 使用者流動工具選擇的初始頁面檢視或自訂事件 tooserve 做為起點 hello 視覺效果的 hello:
1. 按一下 hello 中的 hello 連結 」 使用者要怎麼做後...？ 」 標題，或按一下 hello [編輯] 按鈕。 
2. 從 hello 「 初始事件 」 的下拉式清單中選取的頁面檢視或自訂的事件。
3. 按一下 [建立圖形]。

hello hello 視覺效果的 「 步驟 1 」 欄會顯示哪些使用者未最常後方 hello 初始事件，排序上到下從最 tooleast 常。 「 步驟 2 「 hello 和後續的資料行顯示哪些使用者之後，未建立 hello 方法的所有使用者的瀏覽您的網站。

根據預設，hello 使用者流動工具會隨機取樣只 hello 過去的 24 小時內的頁面檢視和自訂的事件，從您的網站。 您可以增加 hello 時間範圍，並變更 hello hello [編輯] 功能表中的隨機取樣的效能和精確度達成平衡。

如果某些 hello 頁面檢視和自訂事件不相關的 tooyou，請按一下 hello"X"想 toohide hello 節點上。 一旦您已選取您想要 toohide hello 節點，按一下下方 hello 視覺效果的 hello"建立圖形 」 按鈕。 toosee 所有 hello 節點已經隱藏，請按一下 hello [編輯] 按鈕，然後查看 hello"排除事件 」 一節。

如果頁面檢視或自訂事件遺失，您會預期 toosee hello 視覺效果：
* 請檢查 hello [編輯] 功能表中的 hello"排除事件 」 一節。
* Hello 「 詳細資料層級 」 中使用控制項 hello 編輯功能表 tooinclude 較不頻繁事件 hello 視覺效果中。
* 如果 hello 頁面檢視或自訂您預期的事件，則由使用者不常傳送，請嘗試增加 hello 時間範圍 hello [編輯] 功能表中的 hello 視覺效果。
* 請確定 hello 頁面檢視或自訂您預期設定 toobe hello 原始程式碼，您的網站中的 hello Application Insights SDK 所收集的事件。 [深入了解收集自訂事件。](app-insights-api-custom-events-metrics.md)

如果您想的 toosee hello 視覺效果中，使用在 hello hello 」 的步驟的數目 滑桿中的多個步驟 編輯 功能表。

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a>造訪分頁或功能之後，使用者的去向以及他們按了什麼？

![使用使用者流動 toounderstand，使用者按一下](./media/app-insights-usage-flows/flows-one-step.png)

如果頁面檢視您初始的事件，hello 第一個資料行 (「 步驟 1 」) 的 hello 視覺效果是哪些使用者沒有瀏覽 hello 頁面之後，立即快速 toounderstand。 請嘗試在視窗下一步 toohello 使用者流動的視覺效果中開啟您的網站。 比較您的預期使用者與 hello 頁面 toohello 清單 hello 」 步驟 1 」 資料行中的事件之間的互動方式。 通常，看起來不顯著 tooyour 小組的 hello 頁面上的 UI 項目可以是之間 hello hello 頁面上最常使用。 它可以是設計改良 tooyour 站台的最佳起始點。

如果您的初始事件的自訂事件，hello 第一欄會顯示使用者未執行該動作之後，只要。 如同網頁檢視，請考慮是否 hello 觀察到的使用者行為符合您的小組目標和期望。 如果您選取的初始事件 「 加入項目 tooShopping 購物車 」，例如，請查看 toosee 如果"Go tooCheckout 」 和 「 已完成採購 」 會出現在不久之後 hello 視覺效果。 如果使用者行為與您的預期不同，請使用 hello 視覺效果 toounderstand 如何使用者會取得 「 受困於連結 」 您的站台目前的設計。

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a>Hello 會將使用者變換從您的網站的大部分？

監看式 」 工作階段結束 」 節點中出現高總 hello 視覺效果，特別是早期流程中的資料行中。 也就是說，許多使用者下列 hello 上述路徑的網頁和 UI 互動之後，可能變換從您的網站。 有時候變換是預期的 - 例如，在電子商務網站上完成購買之後 - 但是變換通常是設計問題、效能不佳，或您的網站可以改善之其他問題的徵兆。

請注意，「工作階段已結束」節點只會根據這個 Application Insights 資源所收集的遙測。 如果 Application Insights 未收到某些使用者互動的遙測，使用者可能仍然有互動網站在這些方法中 hello 使用者流動工具顯示 hello 工作階段結束之後。

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a>有其中使用者重複 hello 相同的動作重複的位置嗎？

尋找頁面檢視或自訂的事件是由許多使用者重複跨 hello 視覺效果中的後續步驟。 這通常表示使用者會在您的網站上執行重複的動作。 如果您發現重複，請思考變更 hello 設計您的網站，或加入新的功能 tooreduce 重複。 例如，如果您發現使用者在資料表元素的每個資料列上執行重複動作，則新增大量編輯功能。

## <a name="common-questions"></a>常見問題

### <a name="why-do-steps-appear-disconnected"></a>為什麼步驟顯示中斷連線？

![具有已中斷連線步驟的使用者流程](./media/app-insights-usage-flows/flows-disconnected.png)

如果已中斷連線的使用者傳送的視覺效果中的步驟 （資料行），則表示 hello hello 步驟之間的使用者所採取的路徑沒有夠頻繁且足以 toobe 所示。 因此 hello 步驟會顯示已連線，調整 hello [編輯] 功能表中的 hello 「 詳細資料層級 」 滑桿，tooshow 小於 hello 視覺效果上常見的事件。

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a>沒有 hello 初始事件代表 hello 第一個時間 hello 事件出現在工作階段，或出現在工作階段中任何時間？

hello 初始事件 hello 視覺效果只代表 hello 使用者傳送該頁面檢視或自訂的事件工作階段期間的第一次。 如果使用者可以在工作階段中，多次傳送 hello 初始事件則 hello 」 步驟 1 」 資料行只會顯示使用者 hello 之後的行為方式*第一個*初始事件的執行個體，並非所有的執行個體。

## <a name="next-steps"></a>後續步驟

* [使用量概觀](app-insights-usage-overview.md)
* [使用者、工作階段和事件](app-insights-usage-segmentation.md)
* [保留](app-insights-usage-retention.md)
* [加入自訂事件 tooyour 應用程式](app-insights-api-custom-events-metrics.md)
