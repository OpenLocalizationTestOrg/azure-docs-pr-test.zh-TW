---
title: "aaaInvestigate 和共用的使用量資料與 Azure Application Insights 中的互動式活頁簿 |Microsoft 文件"
description: "您 Web 應用程式的使用者人口統計分析。"
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a>調查使用方式資料並且與 Application Insights 中的互動式活頁簿共用

活頁簿將 [Azure Application Insights](app-insights-overview.md) 資料視覺效果、[分析查詢](app-insights-analytics.md) 及文字合併為互動式文件。 活頁簿可以編輯存取 toohello 與其他小組成員相同的 Azure 資源。 這表示 hello 查詢和控制項使用的 toocreate 活頁簿可用 tooother 人讀取 hello 活頁簿，讓您輕鬆 tooexplore、 擴充和檢查錯誤。

活頁簿對於下列案例很有用：

* 瀏覽 hello 應用程式的使用方式，在不事先知道感興趣的 hello 度量： 使用者、 保留率、 轉換比率和其他內容的數字。不同於 Application Insights 中的其他使用方式分析工具，活頁簿可讓您合併多種類型的視覺效果與分析，使其更適合這種自由形式探索。
* 說明 tooyour 小組如何執行新發行的功能，顯示使用者計數索引鍵的互動和其他度量資訊。
* 共用 hello 結果的 A / B 實驗中應用程式與其他小組成員。 您可以解釋 hello 的 hello 目標試驗的文字，則會顯示每個使用量度量及分析查詢使用 tooevaluate hello 試驗，以及清除圖說的每個度量是否上方或下方的目標。
* 報告中斷的 hello 影響 hello 使用方式的結合資料、 文字說明，以及下一個步驟 tooprevent 中斷 hello 未來的討論在您的應用程式。

> [!NOTE]
> Application Insights 資源必須包含頁面檢視或自訂事件 toouse 活頁簿。 [了解如何註冊您的應用程式 toocollect 頁面 tooset 檢視自動以 hello Application Insights JavaScript SDK](app-insights-javascript.md)。
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a>編輯、重新排列、複製和刪除活頁簿區段

活頁簿是由下列區段組成：獨立的可編輯使用方式視覺效果、圖表、資料表、文字或分析查詢結果。

tooedit hello 內容的活頁簿 區段中，按一下 hello**編輯**下面的按鈕和 toohello hello 活頁簿區段的權限。

![Application Insights 活頁簿區段編輯控制項](./media/app-insights-usage-workbooks/editing-controls.png)

1. 當您完成編輯區段，按一下**完成編輯**hello 的左下角 hello > 一節中。

2. toocreate 重複的區段中，按一下 hello**複製本節**圖示。 建立重複的區段是絕佳的 tooway tooiterate 查詢，而不會遺失先前反覆項目。

3. 活頁簿中的區段組成 toomove 按一下 hello**向上移動**或**下移**圖示。

4. tooremove 區段永久，按一下 hello**移除**圖示。

## <a name="adding-usage-data-visualization-sections"></a>新增使用方式資料視覺效果區段

活頁簿提供四種類型的內建使用方式分析視覺效果。 每個回應 hello 使用量的相關應用程式的常見的問題。 tooadd 資料表和圖表以外這些四個區段中，加入分析查詢區段 （如下所示）。

tooadd 使用者、 工作階段、 事件或保留區段 tooyour 活頁簿中，使用 hello**新增使用者**或其他對應按鈕在 hello 底部 hello 活頁簿，或在任何區段的 hello 底部。

![活頁簿中的使用者區段](./media/app-insights-usage-workbooks/users-section.png)

[使用者] 區段會回答「有多少使用者檢視我的網站的某些分頁或使用某些功能？」

[工作階段] 區段會回答「使用者耗費多少工作階段來檢視我的網站的某些分頁或使用某些功能？」

[事件] 區段會回答「使用者檢視我的網站的某些分頁或使用某些功能多少次？」

每個三個區段類型的控制項和視覺效果的相同集合提供 hello:

* [深入了解編輯使用者、工作階段和事件區段](app-insights-usage-segmentation.md)
* 切換 hello 主要圖表、 長條圖方格、 自動的深入資訊和範例使用者視覺效果使用 hello**顯示圖表**，**顯示方格**，**顯示 Insights**，和**這些使用者的範例**在每個區段的 hello 最上方的核取方塊。

![活頁簿中的保留期區段](./media/app-insights-usage-workbooks/retention-section.png)

[保留期] 區段會回答「在某天或某週檢視某些分頁或使用某些功能的人員中，有多少人員在後續一天或一週回來？」

* [深入了解編輯保留期區段](app-insights-usage-retention.md)
* 切換 hello 選擇性整體保留使用圖表 hello**顯示整體保留圖表**在 hello hello 區段頂端的核取方塊。

## <a name="adding-application-insights-analytics-sections"></a>新增 Application Insights 分析區段

![活頁簿中的分析區段](./media/app-insights-usage-workbooks/analytics-section.png)

tooadd 應用程式 Insights 分析查詢區段 tooyour 活頁簿中，使用 hello**加入分析查詢**底部 hello hello 活頁簿，或在任何區段的 hello 底部的按鈕。

分析查詢區段可讓您將 Application Insights 資料的任意查詢新增至活頁簿。 這種彈性表示分析查詢區段應該是您移至 toofor 回答關於以外 hello 四個以上所列的使用者、 工作階段、 事件和保留，像是您網站的任何問題：

* 例外狀況數量未 hello 期間您站台的擲回相同時間週期內的使用方式下降？
* Hello 散發的使用者檢視某些頁面的頁面載入時間是什麼？
* 有多少使用者檢視您的網站上的某些分頁集合，但是未檢視其他分頁集合？ 如果您有使用者使用不同的站台的功能子集的叢集，這可能會很有用的 toounderstand (使用 hello`join`運算子以 hello `kind=leftanti` hello 記錄分析查詢語言中的修飾詞)。

使用 hello[記錄分析查詢語言參考](https://docs.loganalytics.io/)toolearn 深入了解撰寫查詢。

## <a name="adding-text-and-markdown-sections"></a>新增文字和 Markdown 區段

新增標題、 說明、 和實況報導 tooyour 活頁簿，可協助變成旁白的一組資料表和圖表。 活頁簿中的文字區段支援 hello [Markdown 語法](https://daringfireball.net/projects/markdown/)文字格式設定，例如標題、 粗體、 斜體和項目符號清單。

tooadd 文字區段 tooyour 活頁簿使用 hello**加入文字**底部 hello hello 活頁簿，或在任何區段的 hello 底部的按鈕。

## <a name="saving-and-sharing-workbooks-with-your-team"></a>儲存活頁簿並且與小組共用

活頁簿都儲存在 Application Insights 資源，有兩種 hello**我的報表**私人 tooyou 區段或 hello**共用報表**具有存取權可存取 tooeveryone 區段toohello Application Insights 資源。 tooview hello 資源中的所有 hello 活頁簿都按一下 hello**開啟**hello 動作列中的按鈕。

為目前的活頁簿 tooshare**我的報表**:

1. 按一下**開啟**hello 動作列中
2. 按一下 hello"..."按鈕旁邊 hello 活頁簿中，您想 tooshare
3. 按一下**移動 tooShared 報表**。

tooshare 活頁簿的連結，或透過電子郵件，按一下**共用**hello 動作列中。 請記住 hello 連結的收件者需要存取 toothis hello Azure 入口網站 tooview hello 活頁簿中的資源。 toomake 編輯收件者需要至少 hello 資源的參與者權限。

toopin 連結 tooa 活頁簿 tooan Azure 儀表板：

1. 按一下**開啟**hello 動作列中
2. 按一下 hello"..."按鈕旁邊 hello 活頁簿中，您想 toopin
3. 按一下**Pin toodashboard**。

## <a name="next-steps"></a>後續步驟

## <a name="next-steps"></a>後續步驟
- tooenable 使用狀況發生時，開始傳送[自訂事件](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或[頁面檢視](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。
- 如果您已傳送自訂事件或網頁 檢視中瀏覽 hello 使用量工具 toolearn 如何使用者使用您的服務。
    - [使用者、工作階段、事件](app-insights-usage-segmentation.md)
    - [漏斗圖](usage-funnels.md)
    - [保留](app-insights-usage-retention.md)
    - [使用者流程](app-insights-usage-flows.md)
    - [新增使用者內容](app-insights-usage-send-user-context.md)
    
