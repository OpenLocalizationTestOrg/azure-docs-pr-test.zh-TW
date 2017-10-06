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
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="4e722-103">在 Application Insights 中探索 HockeyApp 資料</span><span class="sxs-lookup"><span data-stu-id="4e722-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="4e722-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello 建議監視即時桌上型電腦和行動應用程式的平台。</span><span class="sxs-lookup"><span data-stu-id="4e722-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is hello recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="4e722-105">來自 HockeyApp，您可以傳送自訂和追蹤遙測 toomonitor 使用量，並且協助診斷 （在加法 toogetting 損毀的資料）。</span><span class="sxs-lookup"><span data-stu-id="4e722-105">From HockeyApp, you can send custom and trace telemetry toomonitor usage and assist in diagnosis (in addition toogetting crash data).</span></span> <span data-ttu-id="4e722-106">可以查詢這個資料流的遙測資料，使用功能強大的 hello[分析](app-insights-analytics.md)功能[Azure Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4e722-106">This stream of telemetry can be queried using hello powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="4e722-107">此外，您可以[匯出自訂的 hello 和追蹤遙測](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="4e722-107">In addition, you can [export hello custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="4e722-108">tooenable 這些功能，您將設定轉送 HockeyApp 自訂資料 tooApplication Insights 的橋接器。</span><span class="sxs-lookup"><span data-stu-id="4e722-108">tooenable these features, you set up a bridge that relays HockeyApp custom data tooApplication Insights.</span></span>

## <a name="hello-hockeyapp-bridge-app"></a><span data-ttu-id="4e722-109">hello HockeyApp 橋接器應用程式</span><span class="sxs-lookup"><span data-stu-id="4e722-109">hello HockeyApp Bridge app</span></span>
<span data-ttu-id="4e722-110">hello HockeyApp 橋接器應用程式是 hello 核心功能，可讓您 tooaccess 您自訂的 HockeyApp 和透過 hello 分析，在 Application Insights 追蹤遙測及連續匯出功能。</span><span class="sxs-lookup"><span data-stu-id="4e722-110">hello HockeyApp Bridge App is hello core feature that enables you tooaccess your HockeyApp custom and trace telemetry in Application Insights through hello Analytics and Continuous Export features.</span></span> <span data-ttu-id="4e722-111">自訂和追蹤事件收集 HockeyApp hello hello HockeyApp 橋接器應用程式建立之後仍可從這些功能。</span><span class="sxs-lookup"><span data-stu-id="4e722-111">Custom and trace events collected by HockeyApp after hello creation of hello HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="4e722-112">我們來看看如何 tooset 個橋接器應用程式的其中一個。</span><span class="sxs-lookup"><span data-stu-id="4e722-112">Let’s see how tooset up one of these Bridge Apps.</span></span>

<span data-ttu-id="4e722-113">在 HockeyApp 中，開啟 [帳戶設定]、 [API 權杖](https://rink.hockeyapp.net/manage/auth_tokens)。</span><span class="sxs-lookup"><span data-stu-id="4e722-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="4e722-114">建立新的權杖，或重複使用現有的權杖。</span><span class="sxs-lookup"><span data-stu-id="4e722-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="4e722-115">為 「 唯讀 」 所需的 hello 最小權限。</span><span class="sxs-lookup"><span data-stu-id="4e722-115">hello minimum rights required are "read only".</span></span> <span data-ttu-id="4e722-116">需要一份 hello API 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="4e722-116">Take a copy of hello API token.</span></span>

![取得 HockeyApp API 權杖](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="4e722-118">開啟 hello Microsoft Azure 入口網站和[建立 Application Insights 資源](app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="4e722-118">Open hello Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="4e722-119">設定應用程式類型得 「 HockeyApp 橋接器應用程式 」:</span><span class="sxs-lookup"><span data-stu-id="4e722-119">Set Application Type too“HockeyApp bridge application”:</span></span>

![新增 Application Insights 資源](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="4e722-121">您不需要 tooset 名稱-這將會自動設定從 hello HockeyApp 名稱。</span><span class="sxs-lookup"><span data-stu-id="4e722-121">You don't need tooset a name - this will automatically be set from hello HockeyApp name.</span></span>

<span data-ttu-id="4e722-122">hello HockeyApp 橋接器欄位會出現。</span><span class="sxs-lookup"><span data-stu-id="4e722-122">hello HockeyApp bridge fields appear.</span></span> 

![輸入橋接器欄位](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="4e722-124">輸入您先前記下的 hello HockeyApp 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="4e722-124">Enter hello HockeyApp token you noted earlier.</span></span> <span data-ttu-id="4e722-125">此動作會填入 hello 「 HockeyApp 應用程式 」 下拉式功能表中的所有 HockeyApp 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e722-125">This action populates hello “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="4e722-126">選取 hello 其中一個要 toouse，以及完成 hello 其餘部分的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="4e722-126">Select hello one you want toouse, and complete hello remainder of hello fields.</span></span> 

<span data-ttu-id="4e722-127">開啟 hello 新資源。</span><span class="sxs-lookup"><span data-stu-id="4e722-127">Open hello new resource.</span></span> 

<span data-ttu-id="4e722-128">請注意 hello 資料需要一些時間 toostart 流動。</span><span class="sxs-lookup"><span data-stu-id="4e722-128">Note that hello data takes a while toostart flowing.</span></span>

![等候資料的 Application Insights 資源](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="4e722-130">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="4e722-130">That’s it!</span></span> <span data-ttu-id="4e722-131">從這一點開始收集 HockeyApp 檢測應用程式中自訂和追蹤資料現在也是在 hello 分析可用 tooyou 和 Application Insights 連續匯出功能。</span><span class="sxs-lookup"><span data-stu-id="4e722-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available tooyou in hello Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="4e722-132">讓我們簡短回顧每個這些功能現在可供使用 tooyou。</span><span class="sxs-lookup"><span data-stu-id="4e722-132">Let’s briefly review each of these features now available tooyou.</span></span>

## <a name="analytics"></a><span data-ttu-id="4e722-133">Analytics</span><span class="sxs-lookup"><span data-stu-id="4e722-133">Analytics</span></span>
<span data-ttu-id="4e722-134">分析是特定資料的查詢，可讓您 toodiagnose 強大的工具和分析您的遙測和快速找出根本原因和模式。</span><span class="sxs-lookup"><span data-stu-id="4e722-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you toodiagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Analytics](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="4e722-136">深入了解分析</span><span class="sxs-lookup"><span data-stu-id="4e722-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="4e722-137">連續匯出</span><span class="sxs-lookup"><span data-stu-id="4e722-137">Continuous export</span></span>
<span data-ttu-id="4e722-138">連續匯出可讓您 tooexport 資料至 Azure Blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="4e722-138">Continuous Export allows you tooexport your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="4e722-139">這是非常有用，如果您需要 tookeep 資料長度超過目前提供的 Application Insights hello 保留期限。</span><span class="sxs-lookup"><span data-stu-id="4e722-139">This is very useful if you need tookeep your data for longer than hello retention period currently offered by Application Insights.</span></span> <span data-ttu-id="4e722-140">您可以將 hello 資料保存在 blob 儲存體、 處理它成為 SQL 資料庫中或您慣用的資料倉儲解決方案。</span><span class="sxs-lookup"><span data-stu-id="4e722-140">You can keep hello data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="4e722-141">深入了解連續匯出</span><span class="sxs-lookup"><span data-stu-id="4e722-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="4e722-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e722-142">Next steps</span></span>
* [<span data-ttu-id="4e722-143">適用於分析 tooyour 資料</span><span class="sxs-lookup"><span data-stu-id="4e722-143">Apply Analytics tooyour data</span></span>](app-insights-analytics-tour.md)

