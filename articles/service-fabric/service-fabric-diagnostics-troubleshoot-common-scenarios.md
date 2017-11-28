---
title: "與事件追蹤 aaaTroubleshooting |Microsoft 文件"
description: "hello 在 Microsoft Azure Service Fabric 上部署服務時遇到最常見的問題。"
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="f5caa-103">針對您在 Azure Service Fabric 上部署服務時的常見問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f5caa-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="f5caa-104">如果您開發人員電腦上執行服務，它是簡單 toouse [Visual Studio 的偵錯工具](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。</span><span class="sxs-lookup"><span data-stu-id="f5caa-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="f5caa-105">對於遠端叢集，[健康情況報告](service-fabric-view-entities-aggregated-health.md)永遠是很好的起點 toostart。</span><span class="sxs-lookup"><span data-stu-id="f5caa-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="f5caa-106">hello 這些報表是透過 PowerShell 的最簡單方式 tooaccess 或[SFX](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="f5caa-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="f5caa-107">本文假設您正在偵錯遠端叢集，且有基本的了解如何 toouse 任一種工具。</span><span class="sxs-lookup"><span data-stu-id="f5caa-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="f5caa-108">應用程式損毀</span><span class="sxs-lookup"><span data-stu-id="f5caa-108">Application crash</span></span>
<span data-ttu-id="f5caa-109">hello"分割低於目標複本或執行個體計數 」 報表會清楚指出您的服務所引起。</span><span class="sxs-lookup"><span data-stu-id="f5caa-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="f5caa-110">toofind 出在損毀您的服務會進行一些更多調查。</span><span class="sxs-lookup"><span data-stu-id="f5caa-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="f5caa-111">當大規模執行服務時，最好有一套詳實的追蹤資料。</span><span class="sxs-lookup"><span data-stu-id="f5caa-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="f5caa-112">我們建議您嘗試[Azure 診斷](service-fabric-diagnostics-how-to-setup-wad.md)來收集這些追蹤，並使用像是方案[Azure Application Insights](https://azure.microsoft.com/services/application-insights/)來檢視和搜尋 hello 追蹤。</span><span class="sxs-lookup"><span data-stu-id="f5caa-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![SFX 資料分割健康情況](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="f5caa-114">在服務或動作項目初始化期間</span><span class="sxs-lookup"><span data-stu-id="f5caa-114">During service or actor initialization</span></span>
<span data-ttu-id="f5caa-115">初始化 hello 服務類型之前的任何例外狀況會導致 hello 程序 toocrash。</span><span class="sxs-lookup"><span data-stu-id="f5caa-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="f5caa-116">這些類型的損毀，hello 應用程式事件記錄檔會顯示 hello 錯誤從您的服務。</span><span class="sxs-lookup"><span data-stu-id="f5caa-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="f5caa-117">初始化 hello 服務之前，這些是最常見的例外狀況 toosee hello。</span><span class="sxs-lookup"><span data-stu-id="f5caa-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="f5caa-118">System.IO.FileNotFoundException</span><span class="sxs-lookup"><span data-stu-id="f5caa-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="f5caa-119">此錯誤通常是因為 toomissing 組件相依性。</span><span class="sxs-lookup"><span data-stu-id="f5caa-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="f5caa-120">請檢查 hello CopyLocal 屬性在 Visual Studio 或 hello 全域組件快取中的 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="f5caa-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="f5caa-121">***System.Runtime.InteropServices.COMException*** *在 System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory （IntPtr、 IFabricStatefulServiceFactory）*</span><span class="sxs-lookup"><span data-stu-id="f5caa-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="f5caa-122">這表示該 hello 註冊的服務型別名稱與 hello 服務資訊清單不相符。</span><span class="sxs-lookup"><span data-stu-id="f5caa-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="f5caa-123">[Azure 診斷](service-fabric-diagnostics-how-to-setup-wad.md)可以自動為您的所有節點設定的 tooupload hello 應用程式事件日誌。</span><span class="sxs-lookup"><span data-stu-id="f5caa-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="f5caa-124">RunAsync() 或 OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="f5caa-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="f5caa-125">如果在 hello 初始化期間發生 hello 當機或執行您已註冊的服務型別或動作項目，hello 攔截的例外狀況將被 Azure Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="f5caa-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="f5caa-126">您可以檢視這些提供者 hello EventSource hello 「 後續步驟 」 一節所述。</span><span class="sxs-lookup"><span data-stu-id="f5caa-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5caa-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5caa-127">Next steps</span></span>
<span data-ttu-id="f5caa-128">深入了解 Service Fabric 所提供的現有診斷：</span><span class="sxs-lookup"><span data-stu-id="f5caa-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="f5caa-129">Reliable Actors 項目診斷</span><span class="sxs-lookup"><span data-stu-id="f5caa-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="f5caa-130">Reliable Services 診斷</span><span class="sxs-lookup"><span data-stu-id="f5caa-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

