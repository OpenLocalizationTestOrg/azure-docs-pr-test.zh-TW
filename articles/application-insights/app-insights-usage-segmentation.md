---
title: "在 Azure Application Insights aaaUser、 session 和事件分析 |Microsoft 文件"
description: "您 Web 應用程式的使用者人口統計分析。"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Application Insights 中的使用者、工作階段和事件分析

了解人們在使用您的 Web 應用程式時，他們最感興趣的網頁、使用者的所在位置，以及他們使用何種瀏覽器與作業系統。 使用 [Azure Application Insights](app-insights-overview.md) 來分析商務和使用量遙測。

## <a name="get-started"></a>開始使用

如果您還沒有看到 hello 使用者、 工作階段或在 hello Application Insights 入口網站事件刀鋒視窗中的資料[學習 tooget hello 使用量工具的啟動方式](app-insights-usage-overview.md)。

## <a name="hello-users-sessions-and-events-segmentation-tool"></a>hello 使用者、 工作階段和事件分割工具

Hello 使用量使用刀鋒視窗中的三種 hello 相同工具 tooslice 和擲骰遙測從您的 web 應用程式，從三個檢視方塊。 藉由篩選，並將 hello 資料分割，您能夠發現深入了解不同的頁面和功能的 hello 相對的使用方式。

* **使用者工具**︰使用您應用程式的使用者數目和應用程式的功能。  會使用儲存在瀏覽器 Cookie 中的匿名識別碼來計算使用者。 使用不同瀏覽器或電腦的單一使用者將會計算為多個使用者。
* **工作階段工具**︰已包含應用程式的特定頁面和功能之使用者活動的工作階段數目。 在使用者閒置半小時或連續使用 24 小時之後，就會計算工作階段。
* **事件工具**︰您應用程式的特定頁面與功能之使用頻率。 當瀏覽器從您的應用程式載入頁面時 (假如您已[將它進行檢測](app-insights-javascript.md)) 就會計算頁面檢視。 

    自訂事件表示一個出現項目內容中您的應用程式，通常使用者互動例如按一下按鈕，或 hello 的部分工作完成的情況。 您將程式碼插入您的應用程式太[產生自訂的事件](app-insights-api-custom-events-metrics.md#trackevent)。

![使用量工具](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>查詢特定使用者 

瀏覽不同的使用者群組，藉由調整 hello 頂端 hello hello 使用者工具的查詢選項： 

* 已使用者︰選擇自訂事件和頁面檢視。 
* 期間︰選擇時間範圍。 
* 藉由： 選擇如何 toobucket hello 資料一段時間或另一個屬性，例如瀏覽器或縣 （市）。 
* 依分割： Toosplit 或區段 hello 資料所選擇的屬性。 
* 加入篩選： 限制 hello 查詢 toocertain 使用者、 工作階段或其屬性，例如瀏覽器或縣 （市） 為基礎的事件。 
 
## <a name="saving-and-sharing-reports"></a>儲存和共用報告 
您可以儲存的報表使用者，可能是私用的只是 tooyou hello 我的報表區段中，或與存取 toothis Application Insights 資源與其他人共用在 hello 共用的報表 區段中。  
 
當儲存報表，或編輯其屬性，請選擇 「 目前相對時間範圍 」 toosave 報表將會持續重新整理資料，返回固定一段時間。  
 
選擇 「 目前絕對時間範圍 」 toosave 報表以一組固定的資料。 請記住 90 天，因此如果超過 90 天內有過具有絕對時間範圍的報表已儲存只會儲存在 Application Insights 中的資料，hello 報表將會顯示為空白。 
 
## <a name="example-instances"></a>範例執行個體

hello 範例執行個體 > 一節顯示少數幾個個別的使用者、 工作階段或 hello 目前的查詢會比對事件的相關資訊。 考量和瀏覽的個人，在加法 tooaggregates hello 行為可深入了解如何實際使用您的應用程式。 
 
## <a name="insights"></a>深入解析 

hello Insights [資訊看板] 會顯示大型叢集的共用通用屬性的使用者。 這些叢集中會發現一些您應用程式使用方式的意外趨勢。 例如，如果 40%的所有應用程式的 hello 使用量來自人使用單一的功能。  


## <a name="next-steps"></a>後續步驟
- tooenable 使用狀況發生時，開始傳送[自訂事件](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或[頁面檢視](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。
- 如果您已傳送自訂事件或網頁 檢視中瀏覽 hello 使用量工具 toolearn 如何使用者使用您的服務。
    - [漏斗圖](usage-funnels.md)
    - [保留](app-insights-usage-retention.md)
    - [使用者流程](app-insights-usage-flows.md)
    - [活頁簿](app-insights-usage-workbooks.md)
    - [新增使用者內容](app-insights-usage-send-user-context.md)

