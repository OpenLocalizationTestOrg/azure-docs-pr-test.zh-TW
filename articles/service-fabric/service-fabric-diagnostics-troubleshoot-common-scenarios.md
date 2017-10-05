---
title: "針對事件追蹤進行疑難排解| Microsoft Docs"
description: "在 Microsoft Azure Service Fabric 上部署服務時最常遇到的問題。"
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
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="6730d-103">針對您在 Azure Service Fabric 上部署服務時的常見問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="6730d-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="6730d-104">當您在開發人員電腦上執行服務時，很方便就能使用 [Visual Studio 的偵錯工具](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。</span><span class="sxs-lookup"><span data-stu-id="6730d-104">When you're running services on your developer computer, it is easy to use [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="6730d-105">對於遠端叢集而言，建議一律從 [健康情況報表](service-fabric-view-entities-aggregated-health.md) 開始。</span><span class="sxs-lookup"><span data-stu-id="6730d-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place to start.</span></span> <span data-ttu-id="6730d-106">存取這些報表最簡單的方式，是透過 PowerShell 或 [SFX](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="6730d-106">The easiest ways to access these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="6730d-107">本文假設您要對遠端叢集執行偵錯，而且對於如何使用這些工具已有基本的認識。</span><span class="sxs-lookup"><span data-stu-id="6730d-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how to use either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="6730d-108">應用程式損毀</span><span class="sxs-lookup"><span data-stu-id="6730d-108">Application crash</span></span>
<span data-ttu-id="6730d-109">「分割低於目標複本或執行個體數目」報告是指出您服務將要損毀的最佳指標。</span><span class="sxs-lookup"><span data-stu-id="6730d-109">The "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="6730d-110">若要找出您服務發生損毀的位置，需要進行深入一點的調查。</span><span class="sxs-lookup"><span data-stu-id="6730d-110">To find out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="6730d-111">當大規模執行服務時，最好有一套詳實的追蹤資料。</span><span class="sxs-lookup"><span data-stu-id="6730d-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="6730d-112">建議您嘗試使用 [Azure 診斷](service-fabric-diagnostics-how-to-setup-wad.md)來收集這些追蹤，並使用 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 之類的解決方案來檢視和搜尋追蹤。</span><span class="sxs-lookup"><span data-stu-id="6730d-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching the traces.</span></span>

![SFX 資料分割健康情況](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="6730d-114">在服務或動作項目初始化期間</span><span class="sxs-lookup"><span data-stu-id="6730d-114">During service or actor initialization</span></span>
<span data-ttu-id="6730d-115">在服務類型初始化之前發生的任何例外狀況都將導致程序損毀。</span><span class="sxs-lookup"><span data-stu-id="6730d-115">Any exceptions before the service type is initialized will cause the process to crash.</span></span> <span data-ttu-id="6730d-116">對於這些類型的損毀，應用程式事件記錄檔會顯示您服務中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="6730d-116">For these types of crashes, the application event log will show the error from your service.</span></span>
<span data-ttu-id="6730d-117">這些是服務初始化之前，最常見的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6730d-117">These are the most common exceptions to see before the service is initialized.</span></span>

<span data-ttu-id="6730d-118">System.IO.FileNotFoundException</span><span class="sxs-lookup"><span data-stu-id="6730d-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="6730d-119">這些通常是因為缺少組件相依性所致。</span><span class="sxs-lookup"><span data-stu-id="6730d-119">This error is often due to missing assembly dependencies.</span></span> <span data-ttu-id="6730d-120">請檢查 Visual Studio 中的 CopyLocal 屬性，或節點的全域組件快取。</span><span class="sxs-lookup"><span data-stu-id="6730d-120">Check the CopyLocal property in Visual Studio or the global assembly cache for the node.</span></span>

<span data-ttu-id="6730d-121">***System.Runtime.InteropServices.COMException*** *在 System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory （IntPtr、 IFabricStatefulServiceFactory）*</span><span class="sxs-lookup"><span data-stu-id="6730d-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="6730d-122">這表示註冊的服務類型名稱，與服務資訊清單不符。</span><span class="sxs-lookup"><span data-stu-id="6730d-122">This indicates that the registered service type name does not match the service manifest.</span></span>

<span data-ttu-id="6730d-123">[Azure 診斷](service-fabric-diagnostics-how-to-setup-wad.md) 可以設定成自動上傳您所有節點的應用程式事件記錄。</span><span class="sxs-lookup"><span data-stu-id="6730d-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured to upload the application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="6730d-124">RunAsync() 或 OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="6730d-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="6730d-125">若損毀發生在已註冊之服務類型或動作項目的初始化或執行期間，Azure Service Fabric 將會捕捉到該例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6730d-125">If the crash happens during the initialization or running of your registered service type or actor, the exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="6730d-126">您可以在＜後續步驟＞一節所述的 EventSource 提供者中，檢視這些例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6730d-126">You can view these from the EventSource providers detailed in the "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6730d-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6730d-127">Next steps</span></span>
<span data-ttu-id="6730d-128">深入了解 Service Fabric 所提供的現有診斷：</span><span class="sxs-lookup"><span data-stu-id="6730d-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="6730d-129">Reliable Actors 項目診斷</span><span class="sxs-lookup"><span data-stu-id="6730d-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="6730d-130">Reliable Services 診斷</span><span class="sxs-lookup"><span data-stu-id="6730d-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

