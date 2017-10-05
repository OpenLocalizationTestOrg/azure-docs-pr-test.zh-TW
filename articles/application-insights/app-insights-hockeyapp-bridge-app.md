---
title: "在 Azure Application Insights 中探索 HockeyApp 資料 | Microsoft Docs"
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
ms.openlocfilehash: 450ca10613d137393090578619f3766734d1d493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="fdb8d-103">在 Application Insights 中探索 HockeyApp 資料</span><span class="sxs-lookup"><span data-stu-id="fdb8d-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="fdb8d-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) 是監視即時桌面和行動應用程式的建議平台。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is the recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="fdb8d-105">您可以從 HockeyApp 傳送自訂和追蹤遙測，以便監視使用情況和協助診斷 (除了取得損毀資料以外)。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-105">From HockeyApp, you can send custom and trace telemetry to monitor usage and assist in diagnosis (in addition to getting crash data).</span></span> <span data-ttu-id="fdb8d-106">使用 [Azure Application Insights](app-insights-overview.md) 的強大[分析](app-insights-analytics.md)功能，即可查詢此遙測資料流。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-106">This stream of telemetry can be queried using the powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="fdb8d-107">此外，您可以 [匯出自訂和追蹤遙測](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-107">In addition, you can [export the custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="fdb8d-108">若要啟用這些功能，您可設定橋接器，以將 HockeyApp 自訂資料轉送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-108">To enable these features, you set up a bridge that relays HockeyApp custom data to Application Insights.</span></span>

## <a name="the-hockeyapp-bridge-app"></a><span data-ttu-id="fdb8d-109">HockeyApp 橋接器應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb8d-109">The HockeyApp Bridge app</span></span>
<span data-ttu-id="fdb8d-110">HockeyApp 橋接器應用程式是一項核心功能，可讓您透過分析和連續匯出功能來存取 Application Insights 中的 HockeyApp 自訂和追蹤遙測。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-110">The HockeyApp Bridge App is the core feature that enables you to access your HockeyApp custom and trace telemetry in Application Insights through the Analytics and Continuous Export features.</span></span> <span data-ttu-id="fdb8d-111">經由上述這些功能，可以存取 HockeyApp 在 HockeyApp 橋接器應用程式建立後所收集的自訂和追蹤事件。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-111">Custom and trace events collected by HockeyApp after the creation of the HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="fdb8d-112">我們一起看看如何設定其中一個橋接器應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-112">Let’s see how to set up one of these Bridge Apps.</span></span>

<span data-ttu-id="fdb8d-113">在 HockeyApp 中，開啟 [帳戶設定]、 [API 權杖](https://rink.hockeyapp.net/manage/auth_tokens)。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="fdb8d-114">建立新的權杖，或重複使用現有的權杖。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="fdb8d-115">所需的最小權限是「唯讀」。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-115">The minimum rights required are "read only".</span></span> <span data-ttu-id="fdb8d-116">取得 API 權杖的複本。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-116">Take a copy of the API token.</span></span>

![取得 HockeyApp API 權杖](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="fdb8d-118">開啟 Microsoft Azure 入口網站並 [建立 Application Insights 資源](app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-118">Open the Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="fdb8d-119">將應用程式類型設定為「HockeyApp 橋接器應用程式」：</span><span class="sxs-lookup"><span data-stu-id="fdb8d-119">Set Application Type to “HockeyApp bridge application”:</span></span>

![新增 Application Insights 資源](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="fdb8d-121">您不需要設定名稱 - 將會自動從 HockeyApp 名稱設定。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-121">You don't need to set a name - this will automatically be set from the HockeyApp name.</span></span>

<span data-ttu-id="fdb8d-122">HockeyApp 橋接器欄位隨即出現。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-122">The HockeyApp bridge fields appear.</span></span> 

![輸入橋接器欄位](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="fdb8d-124">輸入您先前記下的 HockeyApp 權杖。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-124">Enter the HockeyApp token you noted earlier.</span></span> <span data-ttu-id="fdb8d-125">此動作會以您所有的 HockeyApp 應用程式填入 [HockeyApp 應用程式] 下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-125">This action populates the “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="fdb8d-126">選取您想要使用的應用程式，並完成其餘的欄位。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-126">Select the one you want to use, and complete the remainder of the fields.</span></span> 

<span data-ttu-id="fdb8d-127">開啟新的資源。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-127">Open the new resource.</span></span> 

<span data-ttu-id="fdb8d-128">請注意，資料需要一些時間才會開始流動。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-128">Note that the data takes a while to start flowing.</span></span>

![等候資料的 Application Insights 資源](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="fdb8d-130">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="fdb8d-130">That’s it!</span></span> <span data-ttu-id="fdb8d-131">從現在開始在 HockeyApp 檢測的應用程式中收集的自訂和追蹤資料，也可供您在 Application Insights 的分析和連續匯出功能中使用。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available to you in the Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="fdb8d-132">讓我們簡短地回顧一下您現在可以使用的功能。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-132">Let’s briefly review each of these features now available to you.</span></span>

## <a name="analytics"></a><span data-ttu-id="fdb8d-133">分析</span><span class="sxs-lookup"><span data-stu-id="fdb8d-133">Analytics</span></span>
<span data-ttu-id="fdb8d-134">「分析」是強大的資料特定查詢工具，可讓您診斷和分析您的遙測，並快速找出根本原因和模式。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you to diagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![分析](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="fdb8d-136">深入了解分析</span><span class="sxs-lookup"><span data-stu-id="fdb8d-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="fdb8d-137">連續匯出</span><span class="sxs-lookup"><span data-stu-id="fdb8d-137">Continuous export</span></span>
<span data-ttu-id="fdb8d-138">連續匯出可讓您將資料匯出至 Azure Blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-138">Continuous Export allows you to export your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="fdb8d-139">如果您的資料所需的保留時間超過 Application Insights 目前提供的保留期間，這就非常有用。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-139">This is very useful if you need to keep your data for longer than the retention period currently offered by Application Insights.</span></span> <span data-ttu-id="fdb8d-140">您可以將資料保留在 Blob 儲存體中，將它處理到 SQL Database 或您慣用的資料倉儲解決方案中。</span><span class="sxs-lookup"><span data-stu-id="fdb8d-140">You can keep the data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="fdb8d-141">深入了解連續匯出</span><span class="sxs-lookup"><span data-stu-id="fdb8d-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="fdb8d-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fdb8d-142">Next steps</span></span>
* [<span data-ttu-id="fdb8d-143">將分析套用到資料</span><span class="sxs-lookup"><span data-stu-id="fdb8d-143">Apply Analytics to your data</span></span>](app-insights-analytics-tour.md)

