---
title: "aaaGet 入門可藉由在 Azure 中的自訂度量來自動調整規模 |Microsoft 文件"
description: "深入了解如何 tooscale 您依在 Azure 中的自訂度量的資源。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>開始在 Azure 中依自訂計量自動調整規模
本文說明如何 tooscale 您透過 Azure 入口網站中的自訂度量的資源。

只有 tooVirtual 機器規模集 (VMSS)、 雲端服務、 應用程式服務方案和應用程式服務環境，適用於 azure 監視的自動調整規模。 

# <a name="lets-get-started"></a>開始使用
本文假設您的 Web 應用程式已設定 Application Insights。 如果您還沒有，則可[設定 ASP.NET 網站的 Application Insights][1]

- 開啟 [Azure 入口網站][2]
- 按一下 Azure 監視器 hello 左側的導覽窗格中的圖示。
  ![啟動 Azure 監視器][3]
- 按一下 自動調整規模設定 tooview 自動標尺會針對適用的以及其目前的自動調整狀態的所有 hello 資源![探索 Azure 監視的自動調整規模][4]
- 開啟 Azure 監視器中的 '自動調整規模 刀鋒視窗，然後選取您想要 tooscale 的資源
> 注意： hello 執行下列步驟使用已設定的 app insights web 應用程式相關聯的應用程式服務計劃。
- 在 hello hello 資源的小數位數設定刀鋒視窗，請注意 hello 目前執行個體計數為 1。 按一下 [啟用自動調整規模]。
  ![適用於新 Web 應用程式的調整規模設定][5]
- 提供名稱的 hello 縮放設定及 hello 請按一下 [新增規則]。 請注意 hello 小數位數的規則選項，為 hello 右手邊的內容窗格隨即開啟。 根據預設，它會設定您的執行個體計數 1，如果 hello 資源的 hello CPU percetage 超過 70%的 hello 選項 tooscale。 變更 hello 度量來源 hello 頂端太選取"Application Insights"hello 在 hello 'Resource' 下拉式清單中，然後選取 hello 自訂度量以基礎的應用程式 insights 資源想 tooscale。
  ![依自訂計量調整規模][6]
- 上述的類似 toohello 步驟會將調整規模規則將在縮放及 hello 擴充計數減 1，如果 hello 自訂公制低於臨界值。
  ![根據 CPU 調整規模][7]
- 設定執行個體限制的 hello。 比方說，如果您想 tooscale 2-5 根據 hello 自訂度量波動的執行個體之間，設定 [最低] 太 '2'，'最大值' 得 '5' 和 'default' 太 '2 的'
> 附註： 讀取 hello 資源度量的問題，而且 hello 目前容量低於 hello 預設容量，然後 tooensure hello 可用性 hello 資源的自動調整規模將會向外延展 toohello 預設值。 如果已經大於預設容量 hello 目前的容量，並不會將自動調整縮放中。
- 按一下 [儲存]

恭喜！ 您現在已成功建立您的自訂公制為基礎的 web 應用程式設定 tooauto 標尺的標尺。

> 注意： hello 相同的步驟都適用 tooget 入門 VMSS 或雲端服務角色。

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
