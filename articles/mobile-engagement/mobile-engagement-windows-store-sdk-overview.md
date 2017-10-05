---
title: "Azure Mobile Engagement Windows 通用 app SDK 整合 | Microsoft Docs"
description: "適用於 Azure Mobile Engagement 的 Windows 通用 SDK 整合"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: d616ad58156a19e89b3e106639a38df67cbd0abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="8c0f7-103">適用於 Azure Mobile Engagement 的 Windows 通用 SDK 整合</span><span class="sxs-lookup"><span data-stu-id="8c0f7-103">Windows Universal SDK Integration for Azure Mobile Engagement</span></span>
<span data-ttu-id="8c0f7-104">此文件說明適用於 Azure Mobile Engagement Windows 通用 SDK 的所有整合及組態選項。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-104">This document describes all the integration and configuration options available for the Azure Mobile Engagement Windows Universal SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c0f7-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="8c0f7-105">Prerequisites</span></span>
<span data-ttu-id="8c0f7-106">開始本教學課程之前，您必須先完成 [15 分鐘教學課程](mobile-engagement-windows-store-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-106">Before starting this tutorial, you must first complete our [15-minute tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="advanced-features"></a><span data-ttu-id="8c0f7-107">進階功能</span><span class="sxs-lookup"><span data-stu-id="8c0f7-107">Advanced features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="8c0f7-108">報告功能</span><span class="sxs-lookup"><span data-stu-id="8c0f7-108">Reporting features</span></span>
<span data-ttu-id="8c0f7-109">您可以新增這些功能：</span><span class="sxs-lookup"><span data-stu-id="8c0f7-109">You can add these features:</span></span>

1. [<span data-ttu-id="8c0f7-110">進階報告選項</span><span class="sxs-lookup"><span data-stu-id="8c0f7-110">Advanced reporting options</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
2. [<span data-ttu-id="8c0f7-111">進階組態選項</span><span class="sxs-lookup"><span data-stu-id="8c0f7-111">Advanced configuration options</span></span>](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="8c0f7-112">通知</span><span class="sxs-lookup"><span data-stu-id="8c0f7-112">Notifications</span></span>
[<span data-ttu-id="8c0f7-113">如何在您的 Windows 通用 App 整合 Reach (通知)</span><span class="sxs-lookup"><span data-stu-id="8c0f7-113">How to integrate Reach (Notifications) in your Windows Universal app</span></span>](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a><span data-ttu-id="8c0f7-114">標記計畫實作：</span><span class="sxs-lookup"><span data-stu-id="8c0f7-114">Tag plan implementation:</span></span>
[<span data-ttu-id="8c0f7-115">如何在您的 Windows 通用 App 使用進階的 Mobile Engagement 標記 API</span><span class="sxs-lookup"><span data-stu-id="8c0f7-115">How to use the advanced Mobile Engagement tagging API in your Windows Universal app</span></span>](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="8c0f7-116">版本資訊</span><span class="sxs-lookup"><span data-stu-id="8c0f7-116">Release notes</span></span>
### <a name="341-11032016"></a><span data-ttu-id="8c0f7-117">3.4.1 (11/03/2016)</span><span class="sxs-lookup"><span data-stu-id="8c0f7-117">3.4.1 (11/03/2016)</span></span>

* <span data-ttu-id="8c0f7-118">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-118">Stability improvements.</span></span>

<span data-ttu-id="8c0f7-119">如需較早版本，請參閱 [完整版本資訊](mobile-engagement-windows-store-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="8c0f7-119">For earlier versions, see the [complete release notes](mobile-engagement-windows-store-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="8c0f7-120">升級程序</span><span class="sxs-lookup"><span data-stu-id="8c0f7-120">Upgrade procedures</span></span>
<span data-ttu-id="8c0f7-121">如果您已經整合舊版 Engagement 到您的應用程式，在升級 SDK 時您必須考慮以下幾點。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-121">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="8c0f7-122">如果您錯過了幾個版本的 SDK，您必須遵循幾個程序。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-122">If you missed several versions of the SDK, you may have to follow several procedures.</span></span> <span data-ttu-id="8c0f7-123">請參閱完整的 [升級程序](mobile-engagement-windows-store-upgrade-procedure.md)。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-123">See the complete [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md).</span></span> <span data-ttu-id="8c0f7-124">例如，如果您要從 0.10.1 移轉到 0.11.0，必須先遵循「從 0.9.0 到 0.10.1」的程序，然後「從 0.10.1 到 0.11.0」的程序。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-124">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

### <a name="from-330-to-340"></a><span data-ttu-id="8c0f7-125">從 3.3.0 到 3.4.0</span><span class="sxs-lookup"><span data-stu-id="8c0f7-125">From 3.3.0 to 3.4.0</span></span>
#### <a name="test-logs"></a><span data-ttu-id="8c0f7-126">測試記錄檔</span><span class="sxs-lookup"><span data-stu-id="8c0f7-126">Test logs</span></span>
<span data-ttu-id="8c0f7-127">SDK 所產生的主控台記錄檔現在可以啟用/停用/篩選。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-127">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="8c0f7-128">若要自訂，請將屬性 `EngagementAgent.Instance.TestLogEnabled` 更新為 `EngagementTestLogLevel` 列舉的其中一個可用值，例如︰</span><span class="sxs-lookup"><span data-stu-id="8c0f7-128">To customize, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the values available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a><span data-ttu-id="8c0f7-129">資源</span><span class="sxs-lookup"><span data-stu-id="8c0f7-129">Resources</span></span>
<span data-ttu-id="8c0f7-130">已改善 Reach 重疊。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-130">The Reach overlay has been improved.</span></span> <span data-ttu-id="8c0f7-131">它是 SDK NuGet 封裝資源的一部分。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-131">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="8c0f7-132">當您升級到新版的 SDK，可以選擇是否要保留資源之重疊資料夾中的現有檔案︰</span><span class="sxs-lookup"><span data-stu-id="8c0f7-132">While upgrading to the new version of the SDK, you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="8c0f7-133">如果先前的重疊對您而言可以運作，或是您要手動整合 `WebView` 元素，則您可以決定保留現有檔案，這樣仍然可以運作。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-133">If the previous overlay is working for you, or you are integrating the `WebView` elements manually, then you can decide to keep your exiting files, it will still work.</span></span>
* <span data-ttu-id="8c0f7-134">若要更新為新的重疊，請將資源的整個 `overlay` 資料夾取代為來自 SDK 封裝的新資料夾 (UWP 應用程式︰升級後，您可以從 %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources 取得新的重疊資料夾)。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-134">To update to the new overlay, replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="8c0f7-135">使用新的重疊會覆寫先前版本上所做的任何自訂。</span><span class="sxs-lookup"><span data-stu-id="8c0f7-135">Using the new overlay overwrites any customizations made on the previous version.</span></span>
> 
> 

### <a name="upgrade-from-older-versions"></a><span data-ttu-id="8c0f7-136">從舊版升級</span><span class="sxs-lookup"><span data-stu-id="8c0f7-136">Upgrade from older versions</span></span>
<span data-ttu-id="8c0f7-137">請參閱 [升級程序](mobile-engagement-windows-store-upgrade-procedure.md)</span><span class="sxs-lookup"><span data-stu-id="8c0f7-137">See [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)</span></span>

