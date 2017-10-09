---
title: "在 Visual Studio 中的 aaaAnalyzing 趨勢 |Microsoft 文件"
description: "在 Visual Studio 中分析、 視覺化及探索您的 Application Insights 遙測的趨勢。"
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 5c623ec040363f05e80ca927dc8855eb016adc99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-trends-in-visual-studio"></a>在 Visual Studio 中分析趨勢 | Microsoft Azure
hello Application Insights Trends 工具視覺化檢視如何 web 應用程式的重要的遙測事件會隨時間變更，可幫助您快速識別出問題與異常狀況。 您可以將您連結 toomore 詳細的診斷資訊，趨勢可協助您改善應用程式效能，追蹤 hello 原因的例外狀況，並展現從您的自訂事件的深入見解。

![範例趨勢視窗](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a>針對 Application Insights 設定您的 Web 應用程式

如果您尚未這麼做，請[針對 Application Insights 設定您的 Web 應用程式](app-insights-overview.md)。 這可讓它 toosend 遙測 toohello Application Insights 入口網站。 hello 趨勢工具會從該處讀取 hello 遙測。

在 Visual Studio 2015 Update 3 及更新版本中可取得 Application Insights 趨勢。

## <a name="open-application-insights-trends"></a>開啟 Application Insights 趨勢
tooopen hello Application Insights Trends 視窗：

* 從 hello Application Insights 工具列按鈕，選擇 **瀏覽遙測趨勢**，或
* Hello 專案內容功能表中選擇**Application Insights > 瀏覽遙測趨勢**，或
* 從 hello Visual Studio 功能表列上選擇 **檢視 > 其他視窗 > Application Insights Trends**。

您可能會看到提示 tooselect 資源。 按一下**選取資源**，請使用 Azure 訂用帳戶，登入，然後從您想其 tooanalyze 遙測趨勢的 hello 清單中選擇的 Application Insights 資源。

## <a name="choose-a-trend-analysis"></a>選擇趨勢分析
![趨勢分析的常見類型功能表](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

開始使用所選擇的其中五個一般趨勢分析，從 hello 過去 24 小時內每個分析資料：

* **調查您伺服器要求的效能問題**-提出的要求 tooyour 服務，依回應時間
* **分析伺服器要求中的錯誤**-提出的要求 tooyour 服務，依 HTTP 回應碼
* **檢查您的應用程式中的 hello 例外狀況**-例外狀況，從您的服務，依例外狀況類型
* **檢查您的應用程式相依性的 hello 效能**-服務您的服務，稱為依回應時間
* **檢查您的自訂事件** - 您為服務設定的自訂事件 (依事件類型分組)。

稍後從 hello 使用預先建立的分析這些項目**檢視遙測分析的一般類型**在 hello hello 趨勢視窗左上角的按鈕。

## <a name="visualize-trends-in-your-application"></a>以視覺化方式呈現您的應用程式的趨勢
Application Insights 趨勢會從您的應用程式的遙測建立時間序列視覺效果。 每一個時間序列視覺效果會顯示某些時間範圍內一種類型的遙測 (依該遙測的其中一個屬性分組)。 例如，您可以依 hello 國家 （地區） 將它們產生，透過 hello 過去 24 小時的 tooview 伺服器要求。 在此範例中，hello 視覺效果上的每個泡泡會在一小時期間代表某些國家/地區的 hello 伺服器要求的計數。

使用 hello 控制項上方的 hello 視窗 tooadjust hello 檢視哪些類型的遙測資料。 首先，選擇您感興趣的 hello 遙測類型：

* **遙測類型** - 伺服器要求、例外狀況、相依性或自訂事件
* **時間範圍**-從過去 30 分鐘 toohello hello 過去 3 天的任何位置
* **分組依據** - 例外狀況類型、問題識別碼、國家/區域等等。

然後，按一下 **分析遙測**toorun hello 查詢。

toonavigate 之間在 hello 視覺效果 （泡泡）：

* 按一下 tooselect 泡泡，就會更新在 hello hello 視窗中，彙總只 hello 事件發生在特定時間週期內的底部 hello 篩選
* 按兩下泡泡 toonavigate toohello 搜尋工具，並查看所有在該時間內發生的 hello 個別遙測事件
* Ctrl 按一下泡泡 toode 選取它 hello 視覺效果中。

> [!TIP]
> hello 趨勢，並搜尋工具一起運作 toohelp 您之間數千個遙測事件服務中找出 hello 的問題的原因。 例如，如果您的客戶在某個下午通知您的應用程式較無回應，請開始使用「趨勢」。 分析提出的要求 tooyour 服務透過 hello 過去幾小時，依回應時間分組。 查看是否有非常大量的慢速要求。 然後按兩下該泡泡 toogo toohello 搜尋工具，篩選的 toothose 要求事件。 從搜尋中，您可以瀏覽 hello 內容的要求，並瀏覽 toohello 程式碼牽涉到 tooresolve hello 問題。
> 
> 

## <a name="filter"></a>Filter
探索更特定的趨勢與 hello 篩選器控制項在 hello hello 視窗的底部。 tooapply 篩選中，按一下其名稱。 您可以快速切換不同的篩選器可能會隱藏您遙測的特定維度中的 toodiscover 趨勢。 如果您套用在一個維度中，例如例外狀況類型篩選其他維度中的篩選器會保留可點選，即使檔案會呈現灰色。tooun-套用篩選，再按一次。 按一下 Ctrl 以 tooselect 中的多個篩選條件 hello 相同的維度。

![趨勢篩選器](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

如果您想 tooapply 多個篩選條件嗎？ 

1. 套用 hello 第一個篩選器。 
2. 按一下 hello**套用選取的篩選並再次查詢**hello 名稱 hello 維度的第一個篩選按鈕。 這會重新查詢您遙測符合 hello 第一個篩選條件的事件。 
3. 套用第二個篩選器。 
4. 重複您遙測的特定子集 hello 程序 toofind 趨勢。 例如，名為 "GET Home/Index"「且」來自德國「且」收到 500 回應碼的伺服器要求。 

tooun-套用這些篩選條件的其中一個，請按一下 hello**移除選取的篩選，並再次查詢**hello 維度 按鈕。

![多個篩選器](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a>尋找異常
hello 趨勢工具可以反白顯示泡泡在 hello 異常比較的 tooother （泡泡） 事件的相同時間序列。 在 hello 檢視類型下拉式清單中，選擇 **時間貯體 （反白顯示異常狀況） 中的計數**或**時間貯體 （反白顯示異常狀況） 中的百分比**。 紅色泡泡為異常。 計數/百分比超過 2.1 時間 hello hello 計數/百分比超過兩個時間週期 （48 小時，如果您正在檢視 hello 最後 24 小時等等）。 hello 中發生的標準差 （泡泡） 所定義的異常狀況。

![彩色的點表示異常](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> 在小型泡泡的時間序列中尋找可能看起來大小相似的離群值時，醒目提示異常特別實用。  
> 
> 

## <a name="next"></a>接續步驟
|  |  |
| --- | --- |
| **[在 Visual Studio 中使用 Application Insights](app-insights-visual-studio.md)**<br/>搜尋遙測、查看 CodeLens 中的資料，以及設定 Application Insights。 盡在 Visual Studio 中。 |![Hello 專案上按一下滑鼠右鍵，然後選擇 Application Insights 搜尋](./media/app-insights-visual-studio-trends/34.png) |
| **[新增更多測試](app-insights-asp-net-more.md)**<br/>監視使用狀況、可用性、相依性、例外狀況。 整合來自記錄架構的追蹤。 撰寫自訂遙測。 |![Visual Studio](./media/app-insights-visual-studio-trends/64.png) |
| **[使用 hello Application Insights 入口網站](app-insights-dashboards.md)**<br/>儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及遙測匯出等功能。 |![Visual Studio](./media/app-insights-visual-studio-trends/62.png) |

