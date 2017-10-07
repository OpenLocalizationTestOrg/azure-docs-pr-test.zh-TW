---
title: "aaaApplication Azure Application Insights 中的對應 |Microsoft 文件"
description: "Hello 應用程式元件之間的相依性的視覺化呈現方式標示 Kpi 和警示。"
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a>Application Insights 的應用程式對應
在[Azure Application Insights](app-insights-overview.md)，應用程式對應為 visual hello 相依性關聯性的應用程式元件的版面配置。 每個元件顯示 Kpi toohelp 負載、 效能、 失敗和警示，例如您找出任何造成效能問題或失敗的元件。 您可以按一下任何元件 toomore 從詳細的診斷，例如 Application Insights 事件。 如果您的應用程式使用 Azure 服務，您也可以按一下透過 tooAzure 診斷，例如 SQL Database Advisor 的建議。

類似其他圖表中，您可以釘選的應用程式對應 toohello Azure 儀表板，可完整運作。 

## <a name="open-hello-application-map"></a>開啟 hello 應用程式對應
從您的應用程式的 hello 概觀刀鋒視窗開啟 hello 對應：

![開啟應用程式對應](./media/app-insights-app-map/01.png)

![應用程式對應](./media/app-insights-app-map/02.png)

hello 對應可顯示：

* 可用性集合
* 用戶端元件 （使用 JavaScript SDK hello 監視）
* 伺服器端元件
* Hello 用戶端和伺服器元件的相依性

您可以展開與摺疊相依性連結群組︰

![摺疊](./media/app-insights-app-map/03.png)

如果您有某種類型 (SQL、HTTP 等) 的許多相依性，它們可能會以群組方式出現。 

![群組的相依性](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a>找出問題
每個節點都有相關的效能指標，例如 hello 負載、 效能和失敗率，該元件。 

警告圖示會點出可能的問題。 橘色的警告表示要求、頁面檢視或相依性呼叫發生失敗。 紅色表示失敗率大於 5 %。 如果您想 tooadjust 這些閾值，請開啟 [選項]。

![失敗圖示](./media/app-insights-app-map/04.png)

也會出現作用中警示︰ 

![作用中警示](./media/app-insights-app-map/05.png)

如果您使用 SQL Azure，當系統有如何改善效能的建議時，便會出現圖示。 

![Azure 建議](./media/app-insights-app-map/06.png)

按一下任何圖示 tooget 更多詳細資料：

![Azure 建議](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a>診斷點選連結
每一個 hello 節點 hello 地圖上提供目標的點選連結，以診斷資訊。 hello 選項 hello hello 節點類型而有所不同。

![伺服器選項](./media/app-insights-app-map/09.png)

Azure 中主控的元件，hello 選項包括 toothem 直接連結。

## <a name="filters-and-time-range"></a>篩選和時間範圍
根據預設，hello 對應摘要說明可用的 hello 選擇時間範圍內的所有 hello 資料。 但是，可以先篩選 tooinclude 只在特定作業名稱或相依性。

* 作業名稱︰這包括頁面檢視和伺服器端要求類型。 使用此選項，hello 地圖顯示 hello hello 只 hello 選取作業的伺服器/用戶端節點上的 KPI。 它會顯示在這些特定作業的 hello 內容中呼叫 hello 相依性。
* 相依性的主檔名： 這包括 hello AJAX 瀏覽器的相依性和伺服器端的相依性。 如果您要報告自訂相依性遙測，以 hello TrackDependency API，它們也出現在這裡。 您可以選取 hello 相依性 tooshow hello 地圖上。 目前這個選項不會篩選 hello 伺服器端要求或 hello 用戶端的分頁檢視。

![設定篩選](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a>儲存篩選
toosave hello 篩選已套用，針 hello 篩選過的檢視拖曳至[儀表板](app-insights-dashboards.md)。

![Pin toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a>錯誤窗格
當您按一下 hello map 中的節點時，錯誤窗格會顯示在 hello 彙總失敗，該節點的右側。 失敗會先依作業識別碼群組，然後再依問題識別碼群組。

![錯誤窗格](./media/app-insights-app-map/error-pane.png)

按一下 上失敗，會在 toohello 發生失敗的最新執行個體。

## <a name="resource-health"></a>資源健康情況
對於某些資源類型，資源健全狀況會顯示在 hello hello 錯誤窗格頂端。 例如，按一下 [SQL] 節點會顯示 hello 資料庫健康狀態與任何已引發的警示。

![資源健康情況](./media/app-insights-app-map/resource-health.png)

您可以按一下 hello 資源名稱 tooview 標準概觀度量該資源。

## <a name="end-to-end-system-app-maps"></a>端對端系統應用程式對應

*需要 SDK 2.3 版或更新版本*

如果您的應用程式具有數個元件-例如後, 端服務此外 toohello web 應用程式層，則您可以顯示所有在一個整合式應用程式對應。

![設定篩選](./media/app-insights-app-map/multi-component-app-map.png)

hello 應用程式對應尋找遵循以 hello Application Insights SDK 安裝的伺服器之間進行的任何 HTTP 相依性呼叫的伺服器節點。 每個 Application Insights 資源會假設 toocontain 一部伺服器。

### <a name="multi-role-app-map-preview"></a>多角色應用程式對應 (預覽)

hello 預覽多角色應用程式對應功能可讓您 toouse hello 應用程式對應具有多個伺服器傳送資料 toohello 相同的 Application Insights 資源 / 檢測金鑰。 Hello 對應中的伺服器分散 hello cloud_RoleName 屬性遙測項目上。 設定*多角色應用程式對應*太*上*從 hello 預覽刀鋒視窗 tooenable 這項設定。

在微服務應用程式，或在其他案例中，您 toocorrelate 事件在單一的 Application Insights 資源內的多部伺服器，可能需要這種方法。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a>意見反應
請透過提供意見反應 hello 入口網站的意見反應 選項。

![MapLink-1 影像](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a>後續步驟

* [Azure 入口網站](https://portal.azure.com)
