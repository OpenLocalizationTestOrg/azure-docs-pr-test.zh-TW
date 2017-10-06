---
title: "aaaExploring Azure Application Insights 中的 HockeyApp 資料 |Microsoft 文件"
description: "使用 Application Insights 分析 Azure 應用程式的使用量和效能。"
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a>在 Application Insights 中探索 HockeyApp 資料
[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello 建議監視即時桌上型電腦和行動應用程式的平台。 來自 HockeyApp，您可以傳送自訂和追蹤遙測 toomonitor 使用量，並且協助診斷 （在加法 toogetting 損毀的資料）。 可以查詢這個資料流的遙測資料，使用功能強大的 hello[分析](app-insights-analytics.md)功能[Azure Application Insights](app-insights-overview.md)。 此外，您可以[匯出自訂的 hello 和追蹤遙測](app-insights-export-telemetry.md)。 tooenable 這些功能，您將設定轉送 HockeyApp 自訂資料 tooApplication Insights 的橋接器。

## <a name="hello-hockeyapp-bridge-app"></a>hello HockeyApp 橋接器應用程式
hello HockeyApp 橋接器應用程式是 hello 核心功能，可讓您 tooaccess 您自訂的 HockeyApp 和透過 hello 分析，在 Application Insights 追蹤遙測及連續匯出功能。 自訂和追蹤事件收集 HockeyApp hello hello HockeyApp 橋接器應用程式建立之後仍可從這些功能。 我們來看看如何 tooset 個橋接器應用程式的其中一個。

在 HockeyApp 中，開啟 [帳戶設定]、 [API 權杖](https://rink.hockeyapp.net/manage/auth_tokens)。 建立新的權杖，或重複使用現有的權杖。 為 「 唯讀 」 所需的 hello 最小權限。 需要一份 hello API 語彙基元。

![取得 HockeyApp API 權杖](./media/app-insights-hockeyapp-bridge-app/01.png)

開啟 hello Microsoft Azure 入口網站和[建立 Application Insights 資源](app-insights-create-new-resource.md)。 設定應用程式類型得 「 HockeyApp 橋接器應用程式 」:

![新增 Application Insights 資源](./media/app-insights-hockeyapp-bridge-app/02.png)

您不需要 tooset 名稱-這將會自動設定從 hello HockeyApp 名稱。

hello HockeyApp 橋接器欄位會出現。 

![輸入橋接器欄位](./media/app-insights-hockeyapp-bridge-app/03.png)

輸入您先前記下的 hello HockeyApp 語彙基元。 此動作會填入 hello 「 HockeyApp 應用程式 」 下拉式功能表中的所有 HockeyApp 應用程式。 選取 hello 其中一個要 toouse，以及完成 hello 其餘部分的 hello 欄位。 

開啟 hello 新資源。 

請注意 hello 資料需要一些時間 toostart 流動。

![等候資料的 Application Insights 資源](./media/app-insights-hockeyapp-bridge-app/04.png)

這樣就大功告成了！ 從這一點開始收集 HockeyApp 檢測應用程式中自訂和追蹤資料現在也是在 hello 分析可用 tooyou 和 Application Insights 連續匯出功能。

讓我們簡短回顧每個這些功能現在可供使用 tooyou。

## <a name="analytics"></a>Analytics
分析是特定資料的查詢，可讓您 toodiagnose 強大的工具和分析您的遙測和快速找出根本原因和模式。

![Analytics](./media/app-insights-hockeyapp-bridge-app/05.png)

* [深入了解分析](app-insights-analytics-tour.md)

## <a name="continuous-export"></a>連續匯出
連續匯出可讓您 tooexport 資料至 Azure Blob 儲存體容器。 這是非常有用，如果您需要 tookeep 資料長度超過目前提供的 Application Insights hello 保留期限。 您可以將 hello 資料保存在 blob 儲存體、 處理它成為 SQL 資料庫中或您慣用的資料倉儲解決方案。

[深入了解連續匯出](app-insights-export-telemetry.md)

## <a name="next-steps"></a>後續步驟
* [適用於分析 tooyour 資料](app-insights-analytics-tour.md)

