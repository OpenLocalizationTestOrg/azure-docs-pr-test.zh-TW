---
title: "使用 Application Insights aaaSCOM 整合 |Microsoft 文件"
description: "如果您是 SCOM 使用者，請使用 Application Insights 來監視效能和診斷問題。 完整的儀表板、智慧警示、功能強大的診斷工具和分析查詢。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>使用 Application Insights 的 SCOM 應用程式效能監視
如果您使用 System Center Operations Manager (SCOM) toomanage 您的伺服器，您可以監視效能和診斷效能問題的 hello 說明[Azure Application Insights](app-insights-asp-net.md)。 Application Insights 會監視 Web 應用程式的連入要求、REST 和 SQL 傳出呼叫、例外狀況，以及記錄追蹤。 它提供的儀表板具有度量圖表和智慧警示，以及透過此遙測來實現的強大診斷搜尋和分析查詢功能。 

您可以使用 SCOM 管理組件來開啟 Application Insights 監視。

## <a name="before-you-start"></a>開始之前
我們假設︰

* 您已熟悉 SCOM 中，並使用 SCOM 2012 R2 或 2016 toomanage IIS web 伺服器。
* 您已安裝在伺服器上您想要使用 Application Insights toomonitor web 應用程式。
* 應用程式架構版本是 .NET 4.5 或更新版本。
* 您有存取 tooa 訂用帳戶[Microsoft Azure](https://azure.com)可以登入 toohello [Azure 入口網站](https://portal.azure.com)。 您的組織可能有訂用帳戶，並可以加入您的 Microsoft 帳戶 tooit。

(hello 開發小組可以建置 hello [Application Insights SDK](app-insights-asp-net.md)到 hello web 應用程式。 此建置階段檢測可讓他們獲得更大的彈性來撰寫自訂遙測。 不過，它並不重要： 您可以依照 hello 不論 SDK 內建的 hello 此處所述的步驟。)

## <a name="one-time-install-application-insights-management-pack"></a>(一次) 安裝 Application Insights 管理組件
在執行 Operations Manager 的 hello 機器：

1. 解除安裝任何舊版的 hello 管理組件：
   1. 在 Operations Manager 中，開啟 [系統管理] > [管理組件]。 
   2. 刪除 hello 舊版本。
2. 下載並安裝 hello 管理組件從 hello 類別目錄。
3. 重新啟動 Operations Manager。

## <a name="create-a-management-pack"></a>建立管理組件
1. 在 Operations Manager 中，開啟 [撰寫中] > [.NET...(使用 Application Insights)] > [加入監視精靈]，然後再次選擇 [.NET...(使用 Application Insights)]。
   
    ![](./media/app-insights-scom/020.png)
2. Hello 組態之後您的應用程式名稱。 （您需要 tooinstrument 一個應用程式一次）。
   
    ![](./media/app-insights-scom/030.png)
3. 在 hello 相同精靈頁面上，請建立新的管理組件，或選取您稍早建立的 Application Insights 的組件。
   
     (hello Application Insights[管理組件](https://technet.microsoft.com/library/cc974491.aspx)是的範本，您可以從中建立執行個體。 您可以重複使用相同的更新版本執行個體的 hello。）

    ![在 hello [一般] 索引標籤中，輸入 hello hello 應用程式名稱。 按一下 [新增]，然後輸入管理組件的名稱。 按一下 [確定]，然後按 [下一步]。](./media/app-insights-scom/040.png)

1. 選擇一個應用程式，您想 toomonitor。 在您的伺服器上安裝應用程式之間的 hello 搜尋功能搜尋。
   
    ![哪些 tooMonitor 索引標籤上，按一下 [新增]，輸入 hello 應用程式名稱的部分，按一下 [搜尋]，選擇 hello 應用程式，然後按一下 [新增]，[確定]。](./media/app-insights-scom/050.png)
   
    如果您不想 toomonitor hello 應用程式中的所有伺服器，hello 選擇性的監視範圍欄位可以是使用的 toospecify 您伺服器的子集。
2. 在 hello 下一步 精靈頁面上，您必須先提供您的認證 toosign tooMicrosoft Azure 中。
   
    這個頁面上，您可以選擇您想要分析並顯示 hello 遙測資料 toobe hello Application Insights 資源。 
   
   * 如果 hello 應用程式已在開發期間設定為 Application Insights，請選取現有的資源。
   * 否則，建立名為 hello 應用程式的新資源。 如果沒有其他應用程式之元件的 hello 相同的系統，將它們放在 hello 相同的資源群組、 toomake 存取 toohello 遙測更容易 toomanage。
     
     您稍後可以變更這些設定。
     
     ![在 [Application Insights 設定] 索引標籤上按一下 [登入]，並提供適用於 Azure 的 Microsoft 帳戶認證。 然後選擇訂用帳戶、資源群組和資源。](./media/app-insights-scom/060.png)
3. Hello 完成精靈。
   
    ![Click Create](./media/app-insights-scom/070.png)

您想 toomonitor 每個應用程式重複此程序。

如果您稍後需要 toochange 設定，重新開啟 hello 屬性 hello 監視從 hello 撰寫視窗。

![在 [撰寫] 中，選取 [使用 Application Insights 的 .NET 應用程式監視效能]、選取監視器，然後按一下 [屬性]。](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>驗證監視
hello 監視您已經安裝在每一部伺服器上搜尋您的應用程式。 它會尋找 hello 應用程式，它會設定 Application Insights 狀態監視器 toomonitor hello 應用程式。 如有必要，先安裝狀態監視器 hello 伺服器上。

您可以確認它已找到的 hello 應用程式的執行個體：

![在 [監視] 中開啟 Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>在 Application Insights 中檢視遙測
在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽您的應用程式的 toohello 資源。 您會[看到顯示應用程式之遙測的圖表](app-insights-dashboards.md)。 (如果它尚未顯示 hello 主頁面上尚未，按一下 即時度量資料流)。

## <a name="next-steps"></a>後續步驟
* [設定儀表板](app-insights-dashboards.md)toobring 一起 hello 最重要圖表監視這與其他應用程式。
* [深入了解度量](app-insights-metrics-explorer.md)
* [設定警示](app-insights-alerts.md)
* [診斷效能問題](app-insights-detect-triage-diagnose.md)
* [功能強大的分析查詢](app-insights-analytics.md)
* [可用性 Web 測試](app-insights-monitor-web-app-availability.md)

