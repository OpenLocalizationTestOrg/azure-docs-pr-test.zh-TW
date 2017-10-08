---
title: "更多 Azure Application Insights aaaGet |Microsoft 文件"
description: "之後開始使用 Application Insights，以下是您可以瀏覽 hello 功能的摘要。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 7ec10a2d-c669-448d-8d45-b486ee32c8db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: bwren
ms.openlocfilehash: 2023728afcf5aa5ecab8b957c8517d4872668765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="more-telemetry-from-application-insights"></a>更多來自 Application Insights 的遙測
之後[加入 Application Insights tooyour ASP.NET 程式碼](app-insights-asp-net.md)，有幾件事，您可以執行 tooget 甚至更多的遙測。 

| 動作 | 得到什麼結果|
|---|---|
|(IIS 伺服器) 在每一部伺服器電腦上[安裝狀態監視器](http://go.microsoft.com/fwlink/?LinkId=506648)。<br/>（azure web 應用程式）在 hello Azure 控制台 hello web 應用程式開啟 hello Application Insights 刀鋒視窗。| [**效能計數器**](app-insights-performance-counters.md)<br/>[**例外狀況**](app-insights-asp-net-exceptions.md) - 包括堆疊追蹤<br/>[**相依項目**](app-insights-asp-net-dependencies.md)|
|[將 hello JavaScript 程式碼片段 tooyour web 網頁](app-insights-javascript.md)|[頁面效能](app-insights-web-track-usage.md)、瀏覽器例外狀況、AJAX 效能。 自訂用戶端遙測。|
|[建立可用性 Web 測試](app-insights-monitor-web-app-availability.md)|如果網站無法使用，將收到警示|
|[確定 buildinfo.config](https://msdn.microsoft.com/library/dn449058.aspx) 由 MSBuild 產生|[建置度量圖表中的註解](https://blogs.msdn.microsoft.com/visualstudioalm/2013/11/14/implementing-deployment-markers-in-application-insights/)
|[寫入自訂事件和度量](app-insights-api-custom-events-metrics.md)|計算商務事件和度量、追蹤詳細使用方式等等。|
|[剖析您的即時網站](https://aka.ms/AIProfilerPreview)|從作用中的 Web 應用程式取得詳細的函式計時|






