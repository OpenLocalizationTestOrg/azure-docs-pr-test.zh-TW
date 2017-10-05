---
title: "在 Windows 中針對 Azure 微服務進行偵錯 | Microsoft Docs"
description: "了解如何監視和診斷在本機開發電腦上使用 Microsoft Azure Service Fabric 所撰寫的服務。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 08998340afb2f242b9a268331607b0d1ddb9b0c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="f6a46-103">監視和診斷本機開發設定中的服務</span><span class="sxs-lookup"><span data-stu-id="f6a46-103">Monitor and diagnose services in a local machine development setup</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6a46-104">Windows</span><span class="sxs-lookup"><span data-stu-id="f6a46-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="f6a46-105">Linux</span><span class="sxs-lookup"><span data-stu-id="f6a46-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

<span data-ttu-id="f6a46-106">監視、偵測、診斷和疑難排解可讓服務繼續順利執行，盡可能減少服務中斷的使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="f6a46-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="f6a46-107">雖然監視和診斷在實際部署的生產環境中相當重要，但是效率會取決於在服務開發期間採用相似的模型，以確保它們能夠在您移至實際設定時正常運作。</span><span class="sxs-lookup"><span data-stu-id="f6a46-107">While monitoring and diagnostics are critical in an actual deployed production environment, the efficiency will depend on adopting a similar model during development of services to ensure they work when you move to a real-world setup.</span></span> <span data-ttu-id="f6a46-108">Service Fabric 可讓服務開發人員輕鬆實作診斷，可以在單一電腦本機開發設定和實際生產叢集設定上順暢地工作。</span><span class="sxs-lookup"><span data-stu-id="f6a46-108">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>

## <a name="event-tracing-for-windows"></a><span data-ttu-id="f6a46-109">Windows 的事件追蹤</span><span class="sxs-lookup"><span data-stu-id="f6a46-109">Event Tracing for Windows</span></span>
<span data-ttu-id="f6a46-110">[Windows 事件追蹤](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) 是我們建議的技術，可用於追蹤 Service Fabric 中的訊息。</span><span class="sxs-lookup"><span data-stu-id="f6a46-110">[Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) is the recommended technology for tracing messages in Service Fabric.</span></span> <span data-ttu-id="f6a46-111">使用 ETW 的部分優點為：</span><span class="sxs-lookup"><span data-stu-id="f6a46-111">Some benefits of using ETW are:</span></span>

* <span data-ttu-id="f6a46-112">**ETW 相當快速。**</span><span class="sxs-lookup"><span data-stu-id="f6a46-112">**ETW is fast.**</span></span> <span data-ttu-id="f6a46-113">其是以一種追蹤技術建置而成，並對您程式碼執行時間的影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="f6a46-113">It was built as a tracing technology that has minimal impact on code execution times.</span></span>
* <span data-ttu-id="f6a46-114">**ETW 會在本機開發環境以及實際叢集設定順暢地進行追蹤。**</span><span class="sxs-lookup"><span data-stu-id="f6a46-114">**ETW tracing works seamlessly across local development environments and also real-world cluster setups.**</span></span> <span data-ttu-id="f6a46-115">這表示當您準備好將程式碼部署至實際叢集時，您不需要重寫追蹤程式碼。</span><span class="sxs-lookup"><span data-stu-id="f6a46-115">This  means you don't have to rewrite your tracing code when you are ready to deploy your code to a real cluster.</span></span>
* <span data-ttu-id="f6a46-116">**Service Fabric 系統程式碼也會將 ETW 用於內部追蹤。**</span><span class="sxs-lookup"><span data-stu-id="f6a46-116">**Service Fabric system code also uses ETW for internal tracing.**</span></span> <span data-ttu-id="f6a46-117">這可讓您檢視與 Service Fabric 系統追蹤交錯的應用程式追蹤。</span><span class="sxs-lookup"><span data-stu-id="f6a46-117">This allows you to view your application traces interleaved with Service Fabric system traces.</span></span> <span data-ttu-id="f6a46-118">同時協助您更輕鬆了解在基礎系統中應用程式程式碼與事件之間的序列和相互關係。</span><span class="sxs-lookup"><span data-stu-id="f6a46-118">It also helps you to more easily understand the sequences and interrelationships between your application code and events in the underlying system.</span></span>
* <span data-ttu-id="f6a46-119">**內建支援的 Service Fabric Visual Studio 工具可供您檢視 ETW 事件。**</span><span class="sxs-lookup"><span data-stu-id="f6a46-119">**There is built-in support in Service Fabric Visual Studio tools to view ETW events.**</span></span> <span data-ttu-id="f6a46-120">一旦使用 Service Fabric 正確設定 Visual Studio 之後，ETW 事件就會出現在 Visual Studio 的 [診斷事件] 檢視中。</span><span class="sxs-lookup"><span data-stu-id="f6a46-120">ETW events appear in the Diagnostic Events view of Visual Studio once Visual Studio is correctly configured with Service Fabric.</span></span> 

## <a name="view-service-fabric-system-events-in-visual-studio"></a><span data-ttu-id="f6a46-121">在 Visual Studio 中檢視 Service Fabric 系統事件</span><span class="sxs-lookup"><span data-stu-id="f6a46-121">View Service Fabric system events in Visual Studio</span></span>
<span data-ttu-id="f6a46-122">Service Fabric 會發出 ETW 事件，以協助應用程式開發人員了解平台中發生的事情。</span><span class="sxs-lookup"><span data-stu-id="f6a46-122">Service Fabric emits ETW events to help application developers understand what's happening in the platform.</span></span> <span data-ttu-id="f6a46-123">如果您還沒有這麼做，請繼續遵循 [在 Visual Studio 中建立第一個應用程式](service-fabric-create-your-first-application-in-visual-studio.md)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="f6a46-123">If you haven't already done so, go ahead and follow the steps in [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span> <span data-ttu-id="f6a46-124">此資訊將協助您啟動應用程式，並執行可顯示追蹤訊息的 [診斷事件檢視器]。</span><span class="sxs-lookup"><span data-stu-id="f6a46-124">This information will help you get an application up and running with the Diagnostics Events Viewer showing the trace messages.</span></span>

1. <span data-ttu-id="f6a46-125">若 [診斷事件] 視窗不會自動顯示，請移至 Visual Studio 中的 [檢視] 索引標籤，選擇 [其他視窗]，然後選擇 [診斷事件檢視器]。</span><span class="sxs-lookup"><span data-stu-id="f6a46-125">If the diagnostics events window does not automatically show, Go to the **View** tab in Visual Studio, choose **Other Windows** and then **Diagnostic Events Viewer**.</span></span>
2. <span data-ttu-id="f6a46-126">每個事件皆有標準的中繼資料資訊，可告訴您事件所來自的節點、應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="f6a46-126">Each event has standard metadata information that tells you the node, application and service the event is coming from.</span></span> <span data-ttu-id="f6a46-127">您也可以使用事件視窗頂端的 [篩選事件] 方塊來篩選事件清單。</span><span class="sxs-lookup"><span data-stu-id="f6a46-127">You can also filter the list of events by using the **Filter events** box at the top of the events window.</span></span> <span data-ttu-id="f6a46-128">例如，您可以依 [節點名稱] 或 [服務名稱] 進行篩選。</span><span class="sxs-lookup"><span data-stu-id="f6a46-128">For example, you can filter on **Node Name** or **Service Name.**</span></span> <span data-ttu-id="f6a46-129">而當您查看事件詳細資料時，您也可以使用事件視窗頂端的 [暫停] 按鈕來暫停並於稍後繼續，而不會遺失任何事件。</span><span class="sxs-lookup"><span data-stu-id="f6a46-129">And when you're looking at event details, you can also pause by using the **Pause** button at the top of the events window and resume later without any loss of events.</span></span>
   
   ![Visual Studio 診斷事件檢視器](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-to-the-application-code"></a><span data-ttu-id="f6a46-131">將您自己自訂的追蹤新增至應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="f6a46-131">Add your own custom traces to the application code</span></span>
<span data-ttu-id="f6a46-132">Service Fabric Visual Studio 專案範本包含範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="f6a46-132">The Service Fabric Visual Studio project templates contain sample code.</span></span> <span data-ttu-id="f6a46-133">程式碼示範如何新增自訂的應用程式程式碼 ETW 追蹤，其會與來自 Service Fabric 的系統追蹤一併顯示在 Visual Studio ETW 檢視器中。</span><span class="sxs-lookup"><span data-stu-id="f6a46-133">The code shows how to add custom application code ETW traces that show up in the Visual Studio ETW viewer alongside system traces from Service Fabric.</span></span> <span data-ttu-id="f6a46-134">這個方法的優點是中繼資料會自動新增至追蹤，且 Visual Studio 診斷事件檢視器已設定為顯示追蹤。</span><span class="sxs-lookup"><span data-stu-id="f6a46-134">The advantage of this method is that metadata is automatically added to traces, and the Visual Studio Diagnostic Events Viewer is already configured to display them.</span></span>

<span data-ttu-id="f6a46-135">針對從「服務範本」(無狀態或可設定狀態) 建立的專案，只要搜尋 `RunAsync` 實作即可：</span><span class="sxs-lookup"><span data-stu-id="f6a46-135">For projects created from the **service templates** (stateless or stateful) just search for the `RunAsync` implementation:</span></span>

1. <span data-ttu-id="f6a46-136">使用 `ServiceEventSource.Current.ServiceMessage` in the `RunAsync` 時會顯示來自應用程式程式碼的自訂 ETW 追蹤範例。</span><span class="sxs-lookup"><span data-stu-id="f6a46-136">The call to `ServiceEventSource.Current.ServiceMessage` in the `RunAsync` method shows an example of a custom ETW trace from the application code.</span></span>
2. <span data-ttu-id="f6a46-137">在 **ServiceEventSource.cs** 檔案中，您會找到 `ServiceEventSource.ServiceMessage` 方法的多載，出於效能因素，應該將其用於高頻率事件。</span><span class="sxs-lookup"><span data-stu-id="f6a46-137">In the **ServiceEventSource.cs** file, you will find an overload for the `ServiceEventSource.ServiceMessage` method that should be used for high-frequency events due to performance reasons.</span></span>

<span data-ttu-id="f6a46-138">針對從 **動作項目範本** (無狀態或可設定狀態) 所建立專案：</span><span class="sxs-lookup"><span data-stu-id="f6a46-138">For projects created from the **actor templates** (stateless or stateful):</span></span>

1. <span data-ttu-id="f6a46-139">開啟 **"ProjectName".cs** 檔案，其中 *ProjectName* 是您針對 Visual Studio 專案所選擇的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a46-139">Open the **"ProjectName".cs** file where *ProjectName* is the name you chose for your Visual Studio project.</span></span>  
2. <span data-ttu-id="f6a46-140">在 *DoWorkAsync* 方法中找出程式碼 `ActorEventSource.Current.ActorMessage(this, "Doing Work");`。</span><span class="sxs-lookup"><span data-stu-id="f6a46-140">Find the code `ActorEventSource.Current.ActorMessage(this, "Doing Work");` in the *DoWorkAsync* method.</span></span>  <span data-ttu-id="f6a46-141">這是來自應用程式程式碼撰寫的自訂 ETW 追蹤範例。</span><span class="sxs-lookup"><span data-stu-id="f6a46-141">This is an example of a custom ETW trace written from application code.</span></span>  
3. <span data-ttu-id="f6a46-142">在 **ActorEventSource.cs** 中，您會找到 `ActorEventSource.ActorMessage` 方法的多載，出於效能因素，應該將其用於高頻率事件。</span><span class="sxs-lookup"><span data-stu-id="f6a46-142">In file **ActorEventSource.cs**, you will find an overload for the `ActorEventSource.ActorMessage` method that should be used for high-frequency events due to performance reasons.</span></span>

<span data-ttu-id="f6a46-143">將自訂 ETW 追蹤新增至服務程式碼之後，您可以再次建置、部署，以及執行應用程式以查看診斷事件檢視器中的事件。</span><span class="sxs-lookup"><span data-stu-id="f6a46-143">After adding custom ETW tracing to your service code, you can build, deploy, and run the application again to see your event(s) in the Diagnostic Events Viewer.</span></span> <span data-ttu-id="f6a46-144">如果您使用 **F5**來偵錯應用程式，診斷事件檢視器將會自動開啟。</span><span class="sxs-lookup"><span data-stu-id="f6a46-144">If you debug the application with **F5**, the Diagnostic Events Viewer will open automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6a46-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6a46-145">Next steps</span></span>
<span data-ttu-id="f6a46-146">在 Azure 叢集上執行應用程式時，您針對本機診斷在上方應用程式所新增的相同追蹤程式碼，將會使用可以用來檢視這些事件的工具。</span><span class="sxs-lookup"><span data-stu-id="f6a46-146">The same tracing code that you added to your application above for local diagnostics will work with tools that you can use to view these events when running your application on an Azure cluster.</span></span> <span data-ttu-id="f6a46-147">請參閱下列文章，其中討論各種適用於工具的選項，並說明如何設定它們。</span><span class="sxs-lookup"><span data-stu-id="f6a46-147">Check out these articles that discuss the different options for the tools and describe how you can set them up.</span></span>

* [<span data-ttu-id="f6a46-148">如何利用 Azure 診斷收集記錄檔</span><span class="sxs-lookup"><span data-stu-id="f6a46-148">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
* [<span data-ttu-id="f6a46-149">使用 EventFlow 的事件彙總與集合</span><span class="sxs-lookup"><span data-stu-id="f6a46-149">Event aggregation and collection using EventFlow</span></span>](service-fabric-diagnostics-event-aggregation-eventflow.md)

