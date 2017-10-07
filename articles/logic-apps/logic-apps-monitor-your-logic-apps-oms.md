---
title: "使用 OMS-Azure 邏輯應用程式執行邏輯應用程式的相關 aaaMonitor 和 get insights |Microsoft 文件"
description: "監視記錄分析和 Operations Management Suite (OMS) tooget insights 與更豐富的偵錯詳細資料，進行疑難排解和診斷程式邏輯應用程式執行"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>透過 Operations Management Suite (OMS) 和 Log Analytics 監視邏輯應用程式執行並取得深入解析

監視和更豐富的偵錯資訊，您可以開啟的記錄分析 hello 在同一時間，當您建立邏輯應用程式。 記錄分析會提供診斷記錄和監視應用程式邏輯會透過 hello Operations Management Suite (OMS) 的入口網站來執行。 當您新增 hello 邏輯應用程式管理解決方案 tooOMS 時，您會取得您的邏輯應用程式執行和特定的詳細資訊，例如狀態、 執行時間、 重新送出狀態，以及相互關聯識別碼的彙總的狀態。

本主題說明如何記錄分析或安裝 tooturn hello 在 OMS 中的邏輯應用程式管理解決方案讓您可以檢視執行階段事件，並執行應用程式邏輯的資料。

 > [!TIP]
 > toomonitor 現有邏輯應用程式，請遵循下列步驟太[開啟診斷記錄，並傳送邏輯應用程式執行階段資料 tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)。

## <a name="requirements"></a>需求

開始之前，您會需要 toohave OMS 工作區。 深入了解[如何 toocreate OMS 工作區](../log-analytics/log-analytics-get-started.md)。 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>建立 Logic Apps 時開啟診斷記錄

1. 在 [Azure 入口網站](https://portal.azure.com)中，建立一個邏輯應用程式。 選擇 [新增] > [企業整合] > [邏輯應用程式] > [建立]。

   ![建立邏輯應用程式](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. 在 hello**建立邏輯應用程式**頁面上，執行這些工作，如所示：

   1. 為您的邏輯應用程式命名並選取您的 Azure 訂用帳戶。 
   2. 建立或選取一個 Azure 資源群組。
   3. 設定**記錄分析**太**上**。 
   您想太傳送應用程式邏輯的資料選取 hello OMS 工作區會執行。 
   4. 當您準備好時，選擇**Pin toodashboard** > **建立**。

      ![建立邏輯應用程式](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      完成此步驟之後，Azure 會建立您的邏輯應用程式，此應用程式現在會與您的 OMS 工作區建立關聯。 
      此外，這個步驟也會自動會 hello 邏輯應用程式管理解決方案安裝在您的 OMS 工作區中。

3. 在 OMS 中，執行邏輯應用程式的 tooview[繼續執行下列步驟](#view-logic-app-runs-oms)。

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>安裝在 OMS 中的 hello 邏輯應用程式管理解決方案

如果您在建立邏輯應用程式時已開啟 Log Analytics，請略過此步驟。 您已經安裝在 OMS 中的 hello 邏輯應用程式管理解決方案。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，選擇**更服務**。 搜尋 "log analytics" 作為您的篩選條件，然後選擇 [Log Analytics]，如下所示：

   ![選擇 [Log Analytics]](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. 在 [Log Analytics] 下，尋找並選取 OMS 工作區。 

   ![選取 OMS 工作區](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. 在 [管理] 下，選擇 [OMS 入口網站]。

   ![選擇 [OMS 入口網站]](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. 在您的 OMS 首頁 hello 升級橫幅顯示時，如果選擇 hello 橫幅，讓您先升級您的 OMS 工作區。 然後選擇 [方案庫]。

   ![選擇 [方案庫]](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. 在下**所有方案**、 尋找並選擇 hello 的 hello 磚**邏輯應用程式管理**方案。

   ![選擇 [Logic Apps Management] \(Logic Apps 管理)](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. 在您的 OMS 工作區中的 tooinstall hello 方案選擇**新增**。

   ![針對 [Logic Apps Management] \(Logic Apps 管理) 選擇 [新增]](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>在 OMS 工作區中檢視邏輯應用程式執行

1. tooview hello 計數和邏輯應用程式的狀態將會為您的 OMS 工作區移 toohello [概觀] 頁面。 檢閱上 hello 的 hello 詳細**邏輯應用程式管理**磚。

   ![顯示邏輯應用程式執行計數和狀態的概觀磚](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > 如果這個升級橫幅顯示而不是 hello 邏輯應用程式管理圖格，請選擇 hello 橫幅，讓您先升級您的 OMS 工作區。
  
   > ![升級「OMS 工作區」](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. 關於您邏輯應用程式執行時，更詳細的資料摘要 tooview 選擇 hello**邏輯應用程式管理**磚。

   在這裡，您的邏輯應用程式執行會依名稱或執行狀態分組。

   ![邏輯應用程式執行的狀態摘要](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. 所有 hello 的 tooview 執行特定邏輯應用程式或狀態、 邏輯應用程式或狀態選取 hello 資料列。

   以下是範例，顯示特定邏輯應用程式的所有 hello 執行：

   ![檢視邏輯應用程式或狀態的執行](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > hello**重新提交**資料行會顯示 [是] 重新提交執行產生的執行。

4. toofilter 這些結果，您可以執行用戶端和伺服器端篩選。

   * 用戶端篩選： 針對每個資料行中，選擇您想要的 hello 篩選器。 
   這裡有一些範例：

     ![資料行篩選範例](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * 伺服器端篩選： toochoose 的出現，請使用 hello 範圍控制 hello 頁面頂端的 hello 的回合的特定時間視窗或 toolimit hello 數。 
   根據預設，一次只能出現 1,000 筆記錄。 
   
     ![變更 hello 時間間隔](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. 所有 tooview 都 hello 動作和特定的執行，選取其詳細資料資料列，這會開啟都 hello 記錄搜尋 頁面。 

   * 這項資訊在資料表中，選擇 tooview**資料表**。
   * toochange hello 查詢中，您可以編輯 hello hello 搜尋列中的查詢字串。 
   若要獲得更佳的體驗，請選擇 [進階分析]。

     ![檢視邏輯應用程式執行的動作和詳細資料](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     這裡在 hello Azure 記錄分析 頁面上，您可以更新查詢和檢視結果 hello 資料表中的 hello。 
     此查詢會使用[Kusto 查詢語言](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html)，如果您想 tooview 不同的結果，您可以編輯。 

     ![Azure Log Analytics - 查詢檢視](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>後續步驟

* [監視 B2B 訊息](../logic-apps/logic-apps-monitor-b2b-message.md)
