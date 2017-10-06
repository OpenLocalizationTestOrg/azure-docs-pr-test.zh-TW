---
title: "Application Insights for ASP.NET Core aaaAzure |Microsoft 文件"
description: "監視 Web 應用程式的可用性、效能和使用方式。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a>ASP.NET Core 的 Application Insights
[Application Insights](app-insights-overview.md) 可讓您監視 Web 應用程式的可用性、效能和使用情況。 Hello 您善加 hello 效能和效率 hello 中的應用程式的相關意見反應，可以讓謹慎的選擇 hello 方向 hello 設計的每個開發週期中。

![範例](./media/app-insights-asp-net-core/sample.png)

您需要 [Microsoft Azure](http://azure.com)的訂用帳戶。 使用 Microsoft 帳戶登入，可能是針對 Windows、XBox Live 或其他 Microsoft 雲端服務具備的帳戶。 您的小組可能會有組織的訂用帳戶 tooAzure： 詢問 hello 擁有者 tooadd 您 tooit 使用您的 Microsoft 帳戶。

## <a name="getting-started"></a>開始使用

* 在 Visual Studio [方案總管] 中以滑鼠右鍵按一下專案，然後選取 [設定 Application Insights]，或 [新增] > [Application Insights]。 [深入了解](app-insights-asp-net.md)。
* 如果您沒有看到這些功能表命令，請遵循 hello[手動使用者入門指南](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started)。 您可能需要 toodo 這如果使用您的專案建立 2017年之前的 Visual Studio 版本。

## <a name="using-application-insights"></a>使用 Application Insights
登入 hello [Microsoft Azure 入口網站](https://portal.azure.com)，選取**所有資源**或**Application Insights**，然後選取您的應用程式建立 toomonitor hello 資源。

在另一個瀏覽器視窗中，使用您的應用程式一段時間。 您會看到顯示 hello Application Insights 圖表中的資料。 （您可能需要重新整理 tooclick）。在您的開發過程只會有少量的資料，但是當您發行應用程式並有許多使用者時，這些圖表就會真正活躍起來。 

hello 概觀 頁面上顯示關鍵效能圖表： 伺服器回應時間、 頁面載入時間和失敗要求的計數。 多個圖表和資料，請按一下任何圖 toosee。

Hello 入口網站中的檢視可分成三大類：

* [計量瀏覽器](app-insights-metrics-explorer.md)顯示圖表及資料表的度量和計數，例如回應時間、 失敗率或度量您自行建立以 hello [API](app-insights-api-custom-events-metrics.md)。 篩選器和區段 hello 資料屬性值 tooget 進一步了解您的應用程式和它的使用者。
* [搜尋總管](app-insights-diagnostic-search.md)個別事件，例如特定要求、 例外狀況、 記錄追蹤或以 hello 自己建立的事件會列出[API](app-insights-api-custom-events-metrics.md)。 篩選和搜尋 hello 事件中，瀏覽不同的相關的事件 tooinvestigate 問題。
* [分析](app-insights-analytics.md) 可讓您在遙測上執行類似 SQL 的查詢，而且這是一個功能強大的分析與診斷工具。

## <a name="alerts"></a>Alerts
* 自動取得[主動診斷警示](app-insights-proactive-diagnostics.md)，告訴您相關的失敗率和其他度量異常的變更。
* 設定[可用性測試](app-insights-monitor-web-app-availability.md)tootest 任何測試失敗時以電子郵件傳送您的網站持續全球性、 位置和 get。
* 設定[度量的警示](app-insights-monitor-web-app-availability.md)tooknow 如果度量資訊，例如回應時間或例外狀況率超出可接受的限制。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>開放原始碼
[閱讀及張貼 toohello 程式碼](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>後續步驟
* [將遙測 tooyour web 網頁](app-insights-javascript.md)toomonitor 頁面使用方式和效能。
* [監視的相依性](app-insights-asp-net-dependencies.md)toosee 如果 REST、 SQL 或其他外部資源會減緩您。
* [使用 hello API](app-insights-api-custom-events-metrics.md) toosend 您自己的事件和度量的應用程式的效能和使用方式的更詳細檢視。
* [可用性測試](app-insights-monitor-web-app-availability.md)檢查 hello 世界各地不斷地從應用程式。 

