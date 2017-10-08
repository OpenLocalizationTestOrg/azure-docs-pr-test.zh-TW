---
title: "Mobile Engagement Windows 通用 SDK 整合 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="0d8e8-103">適用於 Azure Mobile Engagement 的 Windows 通用 SDK 整合</span><span class="sxs-lookup"><span data-stu-id="0d8e8-103">Windows Universal SDK Integration for Azure Mobile Engagement</span></span>
<span data-ttu-id="0d8e8-104">本文件說明所有 hello 整合和組態選項可供 hello Azure Mobile Engagement Windows 通用 SDK。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-104">This document describes all hello integration and configuration options available for hello Azure Mobile Engagement Windows Universal SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d8e8-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="0d8e8-105">Prerequisites</span></span>
<span data-ttu-id="0d8e8-106">開始本教學課程之前，您必須先完成 [15 分鐘教學課程](mobile-engagement-windows-store-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-106">Before starting this tutorial, you must first complete our [15-minute tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="advanced-features"></a><span data-ttu-id="0d8e8-107">進階功能</span><span class="sxs-lookup"><span data-stu-id="0d8e8-107">Advanced features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="0d8e8-108">報告功能</span><span class="sxs-lookup"><span data-stu-id="0d8e8-108">Reporting features</span></span>
<span data-ttu-id="0d8e8-109">您可以新增這些功能：</span><span class="sxs-lookup"><span data-stu-id="0d8e8-109">You can add these features:</span></span>

1. [<span data-ttu-id="0d8e8-110">進階報告選項</span><span class="sxs-lookup"><span data-stu-id="0d8e8-110">Advanced reporting options</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
2. [<span data-ttu-id="0d8e8-111">進階組態選項</span><span class="sxs-lookup"><span data-stu-id="0d8e8-111">Advanced configuration options</span></span>](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="0d8e8-112">通知</span><span class="sxs-lookup"><span data-stu-id="0d8e8-112">Notifications</span></span>
[<span data-ttu-id="0d8e8-113">如何在 Windows 通用應用程式中的 toointegrate 觸達 （通知）</span><span class="sxs-lookup"><span data-stu-id="0d8e8-113">How toointegrate Reach (Notifications) in your Windows Universal app</span></span>](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a><span data-ttu-id="0d8e8-114">標記計畫實作：</span><span class="sxs-lookup"><span data-stu-id="0d8e8-114">Tag plan implementation:</span></span>
[<span data-ttu-id="0d8e8-115">如何 toouse hello 進階 Mobile Engagement 標記 Windows 通用應用程式中的應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="0d8e8-115">How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app</span></span>](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="0d8e8-116">版本資訊</span><span class="sxs-lookup"><span data-stu-id="0d8e8-116">Release notes</span></span>
### <a name="341-11032016"></a><span data-ttu-id="0d8e8-117">3.4.1 (11/03/2016)</span><span class="sxs-lookup"><span data-stu-id="0d8e8-117">3.4.1 (11/03/2016)</span></span>

* <span data-ttu-id="0d8e8-118">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-118">Stability improvements.</span></span>

<span data-ttu-id="0d8e8-119">如先前的版本，請參閱 hello[完成版本資訊](mobile-engagement-windows-store-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="0d8e8-119">For earlier versions, see hello [complete release notes](mobile-engagement-windows-store-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="0d8e8-120">升級程序</span><span class="sxs-lookup"><span data-stu-id="0d8e8-120">Upgrade procedures</span></span>
<span data-ttu-id="0d8e8-121">如果您已經有整合至您的應用程式較舊版本的參與，則必須升級 hello SDK 時，下列點 tooconsider hello。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-121">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="0d8e8-122">如果您錯過數個版本的 hello SDK，您可能必須 toofollow 數個程序。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-122">If you missed several versions of hello SDK, you may have toofollow several procedures.</span></span> <span data-ttu-id="0d8e8-123">請參閱完整的 hello[升級程序](mobile-engagement-windows-store-upgrade-procedure.md)。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-123">See hello complete [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md).</span></span> <span data-ttu-id="0d8e8-124">例如，如果您從 0.10.1 移轉 too0.11.0 您有遵循 hello toofirst"0.9.0 從 too0.10.1 」 程序然後 hello 」 從 0.10.1 too0.11.0 」 程序。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-124">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

### <a name="from-330-too340"></a><span data-ttu-id="0d8e8-125">從 3.3.0 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="0d8e8-125">From 3.3.0 too3.4.0</span></span>
#### <a name="test-logs"></a><span data-ttu-id="0d8e8-126">測試記錄檔</span><span class="sxs-lookup"><span data-stu-id="0d8e8-126">Test logs</span></span>
<span data-ttu-id="0d8e8-127">主控台記錄檔所產生的 hello SDK 現在可以啟用/停用/篩選。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-127">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="0d8e8-128">toocustomize，更新 hello 屬性`EngagementAgent.Instance.TestLogEnabled`的 hello 值可從 hello tooone`EngagementTestLogLevel`列舉型別，例如：</span><span class="sxs-lookup"><span data-stu-id="0d8e8-128">toocustomize, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello values available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a><span data-ttu-id="0d8e8-129">資源</span><span class="sxs-lookup"><span data-stu-id="0d8e8-129">Resources</span></span>
<span data-ttu-id="0d8e8-130">已改善 hello 觸達重疊。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-130">hello Reach overlay has been improved.</span></span> <span data-ttu-id="0d8e8-131">它是 hello SDK 的 NuGet 封裝資源的一部分。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-131">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="0d8e8-132">升級 toohello hello SDK 新版本，您可以選擇或不 hello 從現有的檔案是否要將 tookeep 覆疊資源的資料夾：</span><span class="sxs-lookup"><span data-stu-id="0d8e8-132">While upgrading toohello new version of hello SDK, you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="0d8e8-133">如果 hello 先前覆疊適合您，或者您要整合 hello`WebView`項目以手動方式，然後您可以決定 tookeep 您結束檔案，它仍可運作。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-133">If hello previous overlay is working for you, or you are integrating hello `WebView` elements manually, then you can decide tookeep your exiting files, it will still work.</span></span>
* <span data-ttu-id="0d8e8-134">tooupdate toohello 新建立的重疊取代 hello 整個`overlay`從您的資源，以從 hello SDK 套件中的 hello 新資料夾 (UWP 應用程式： hello 升級之後，您可以從 %USERPROFILE%取得新重疊資料夾 hello\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources)。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-134">tooupdate toohello new overlay, replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="0d8e8-135">使用 hello 新重疊，就會覆寫 hello 舊版本上所做的任何自訂。</span><span class="sxs-lookup"><span data-stu-id="0d8e8-135">Using hello new overlay overwrites any customizations made on hello previous version.</span></span>
> 
> 

### <a name="upgrade-from-older-versions"></a><span data-ttu-id="0d8e8-136">從舊版升級</span><span class="sxs-lookup"><span data-stu-id="0d8e8-136">Upgrade from older versions</span></span>
<span data-ttu-id="0d8e8-137">請參閱 [升級程序](mobile-engagement-windows-store-upgrade-procedure.md)</span><span class="sxs-lookup"><span data-stu-id="0d8e8-137">See [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)</span></span>

