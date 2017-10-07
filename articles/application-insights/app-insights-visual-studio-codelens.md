---
title: "在 Visual Studio CodeLens Insights 遙測 aaaApplication |Microsoft 文件"
description: "使用 Visual Studio 中的 CodeLens 快速存取 Application Insights 要求和例外狀況遙測。"
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Visual Studio CodeLens 中的 Application Insights 遙測
Hello web 應用程式的程式碼中的方法可以標註具有執行階段例外狀況的遙測，並要求回應時間。 如果您安裝[Azure Application Insights](app-insights-overview.md)應用程式中 hello 遙測會出現在 Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -hello hello 頂端，您的使用位置的每個函式的備忘稿 tooseeing 有用資訊，例如 hello 數目上的芳鄰 hello 函式參考，或 hello 上次編輯它的人員。

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> CodeLens 中的 application Insights 是用於 Visual Studio 2015 Update 3 及更新版本，或是與 hello 最新版本[開發人員分析工具延伸模組](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a)。 CodeLens 提供了 hello 企業版和專業版的 Visual Studio 版本。
> 
> 

## <a name="where-toofind-application-insights-data"></a>其中 toofind Application Insights 資料
尋找在 hello CodeLens 指標 hello 公用要求方法的 web 應用程式中的 Application Insights 遙測。 CodeLens 指標會顯示於 C# 和 Visual Basic 程式碼中的方法和其他宣告上方。 如果 Application Insights 資料可用於某個方法，您將會看到要求和例外狀況的指標，例如「100 個要求，%1 個失敗」或「10 個例外狀況」。 如需詳細資料，按一下 CodeLens 指標。 

> [!TIP]
> Application Insights 要求和例外狀況指標可能需要一些額外的秒鐘 tooload 之後會出現其他 CodeLens 的指標。
> 
> 

## <a name="exceptions-in-codelens"></a>CodeLens 中的例外狀況
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

hello 例外狀況的 CodeLens 指標會顯示 hello hello 15 多數經常發生例外狀況，您的應用程式，在該期間內，處理 hello 要求時由 hello 方法從 hello 在過去 24 小時內發生的例外狀況數目。

toosee 更多詳細資訊，按一下 hello 例外狀況的 CodeLens 指標：

* 例外狀況的 hello 最近 24 小時相對 toohello 先前從次數 24 小時 hello 百分比變更
* 選擇**移 toocode** toonavigate toohello 原始程式碼 hello 函式擲回 hello 例外狀況
* 選擇**搜尋**tooquery 中發生此例外狀況的所有執行個體 hello 過去 24 小時
* 選擇**趨勢**tooview 這個例外狀況在 hello 過去 24 小時內的項目趨勢視覺效果
* 選擇**檢視此應用程式中的所有例外狀況**tooquery 中所發生的所有例外狀況 hello 過去 24 小時
* 選擇**探索例外狀況的趨勢**tooview 趨勢視覺效果中發生的 hello 過去 24 小時內的所有例外狀況。 

> [!TIP]
> 如果您看到 [0 例外狀況] CodeLens 中，但您知道應該例外狀況，請檢查 toomake 確定 CodeLens 已選取 hello 右 Application Insights 資源。 tooselect 另一個資源，hello 方案總管] 中的專案上按一下滑鼠右鍵，然後選擇 [ **Application Insights > 選擇遙測來源**。 CodeLens 僅會顯示 hello 15 多數經常發生例外狀況，應用程式中 hello 過去 24 小時，因此，如果例外狀況經常 hello 大部分 16 或更少，您會看到 [0 例外狀況]。 例外狀況，從 ASP.NET 檢視可能不會出現在產生這些檢視表的 hello 控制器方法。
> 
> [!TIP]
> 如果您在 CodeLens 中看到「？ 例外狀況 > CodeLens，您需要的 tooassociate Visual Studio 或您的 Azure 帳戶的認證與您的 Azure 帳戶可能已過期。 在任一種情況下，按一下「？ 例外狀況]，然後選擇 [**新增帳戶...** tooenter 您的認證。
> 
> 

## <a name="requests-in-codelens"></a>CodeLens 中的要求
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

hello CodeLens 指標顯示 hello 數目的 HTTP 要求會要求已由 hello 過去 24 小時，再加上 hello 百分比，這些失敗的要求中的方法提供服務。

詳細資訊，請按一下 toosee hello 要求 CodeLens 指標：

* 過去 24 小時比較 toohello 先前 hello 透過 24 小時 hello 中要求、 失敗的要求和平均回應時間的數字的絕對值和百分比變更
* hello 方法，計算為未通過 hello 在過去 24 小時內的要求 hello 百分比的 hello 可靠性
* 選擇**搜尋**個要求或所有 hello （失敗） 的要求中所發生 hello 過去 24 小時內失敗的要求 tooquery
* 選擇**趨勢**tooview 趨勢視覺效果的要求、 失敗的要求或平均回應時間在 hello 過去 24 小時。
* Hello 左上角的 hello CodeLens 詳細資料檢視 toochange 哪些資源是 hello CodeLens 資料來源選擇 hello hello Application Insights 資源名稱。

## <a name="next"></a>接續步驟
|  |  |
| --- | --- |
| **[在 Visual Studio 中使用 Application Insights](app-insights-visual-studio.md)**<br/>搜尋遙測、查看 CodeLens 中的資料，以及設定 Application Insights。 盡在 Visual Studio 中。 |![Hello 專案上按一下滑鼠右鍵，然後選擇 Application Insights 搜尋](./media/app-insights-visual-studio-codelens/34.png) |
| **[新增更多測試](app-insights-asp-net-more.md)**<br/>監視使用狀況、可用性、相依性、例外狀況。 整合來自記錄架構的追蹤。 撰寫自訂遙測。 |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[使用 hello Application Insights 入口網站](app-insights-dashboards.md)**<br/>儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及遙測匯出等功能。 |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |

