---
title: "處理雲端服務生命週期事件 | Microsoft Docs"
description: "了解如何在 .NET 中使用雲端服務角色的生命週期方法"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: eb78c05df3b3cdf3887334c11bdabd5cebb74747
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="customize-the-lifecycle-of-a-web-or-worker-role-in-net"></a><span data-ttu-id="d7046-103">在 .NET 中自訂 Web 或背景工作角色的生命週期</span><span class="sxs-lookup"><span data-stu-id="d7046-103">Customize the Lifecycle of a Web or Worker role in .NET</span></span>
<span data-ttu-id="d7046-104">當您建立背景工作角色時，擴充可為您提供覆寫方法並讓您回應生命週期事件的 [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) 類別。</span><span class="sxs-lookup"><span data-stu-id="d7046-104">When you create a worker role, you extend the [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) class which provides methods for you to override that let you respond to lifecycle events.</span></span> <span data-ttu-id="d7046-105">若是 Web 角色，此類別是選擇性的，因此您必須使用它來回應生命週期事件。</span><span class="sxs-lookup"><span data-stu-id="d7046-105">For web roles this class is optional, so you must use it to respond to lifecycle events.</span></span>

## <a name="extend-the-roleentrypoint-class"></a><span data-ttu-id="d7046-106">擴充 RoleEntryPoint 類別</span><span class="sxs-lookup"><span data-stu-id="d7046-106">Extend the RoleEntryPoint class</span></span>
<span data-ttu-id="d7046-107">[RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) 類別包含 Azure 在**啟動**、**執行**或**停止** Web 或背景工作角色時所呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="d7046-107">The [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) class includes methods that are called by Azure when it **starts**, **runs**, or **stops** a web or worker role.</span></span> <span data-ttu-id="d7046-108">您可以選擇性地覆寫這些方法來管理角色初始化、角色關機順序或角色的執行緒。</span><span class="sxs-lookup"><span data-stu-id="d7046-108">You can optionally override these methods to manage role initialization, role shutdown sequences, or the execution thread of the role.</span></span> 

<span data-ttu-id="d7046-109">擴充 **RoleEntryPoint**時，您應該注意下列方法的行為：</span><span class="sxs-lookup"><span data-stu-id="d7046-109">When extending **RoleEntryPoint**, you should be aware of the following behaviors of the methods:</span></span>

* <span data-ttu-id="d7046-110">[OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) 和 [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 方法會傳回布林值，因此可能會從這些方法傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="d7046-110">The [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) and [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) methods return a boolean value, so it is possible to return **false** from these methods.</span></span>
  
   <span data-ttu-id="d7046-111">如果您的程式碼傳回 **false**，會突然終止角色處理序，而不會執行您既有的任何關機順序。</span><span class="sxs-lookup"><span data-stu-id="d7046-111">If your code returns **false**, the role process is abruptly terminated, without running any shutdown sequence you may have in place.</span></span> <span data-ttu-id="d7046-112">一般而言，您應該避免從 **OnStart** 方法傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="d7046-112">In general, you should avoid returning **false** from the **OnStart** method.</span></span>
* <span data-ttu-id="d7046-113">**RoleEntryPoint** 方法多載中未能攔截的任何例外狀況，都會被視為未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d7046-113">Any uncaught exception within an overload of a **RoleEntryPoint** method is treated as an unhandled exception.</span></span>
  
   <span data-ttu-id="d7046-114">如果在其中一個生命週期方法內發生例外狀況，Azure 將會引發 [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) 事件，然後處理序便會終止。</span><span class="sxs-lookup"><span data-stu-id="d7046-114">If an exception occurs within one of the lifecycle methods, Azure will raise the [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) event, and then the process is terminated.</span></span> <span data-ttu-id="d7046-115">您的角色離線之後，Azure 將重新啟動該角色。</span><span class="sxs-lookup"><span data-stu-id="d7046-115">After your role has been taken offline, it will be restarted by Azure.</span></span> <span data-ttu-id="d7046-116">當未處理的例外狀況發生時，不會引發 [Stopping](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) 事件，也不會呼叫 **OnStop** 方法。</span><span class="sxs-lookup"><span data-stu-id="d7046-116">When an unhandled exception occurs, the [Stopping](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) event is not raised, and the **OnStop** method is not called.</span></span>

<span data-ttu-id="d7046-117">如果您的角色無法啟動，或在初始化、忙碌和停止狀態之間循環，每次角色重新啟動時，您的程式碼可能會在其中一個生命週期事件內擲回未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d7046-117">If your role does not start, or is recycling between the initializing, busy, and stopping states, your code may be throwing an unhandled exception within one of the lifecycle events each time the role restarts.</span></span> <span data-ttu-id="d7046-118">在此情況下，使用 [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) 事件判斷造成此例外狀況的原因，並適當地處理。</span><span class="sxs-lookup"><span data-stu-id="d7046-118">In this case, use the [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) event to determine the cause of the exception and handle it appropriately.</span></span> <span data-ttu-id="d7046-119">您的角色可能也會從 [Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 方法傳回，而導致該角色重新啟動。</span><span class="sxs-lookup"><span data-stu-id="d7046-119">Your role may also be returning from the [Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, which causes the role to restart.</span></span> <span data-ttu-id="d7046-120">如需有關部署狀態的詳細資訊，請參閱 [導致角色循環的常見問題](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)。</span><span class="sxs-lookup"><span data-stu-id="d7046-120">For more information about deployment states, see [Common Issues Which Cause Roles to Recycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d7046-121">如果您使用 **Azure Tools for Microsoft Visual Studio** 開發您的應用程式，角色專案範本會在 WebRole.cs 及 WorkerRole.cs 檔案中，自動為您擴充 **RoleEntryPoint** 類別。</span><span class="sxs-lookup"><span data-stu-id="d7046-121">If you are using the **Azure Tools for Microsoft Visual Studio** to develop your application, the role project templates automatically extend the **RoleEntryPoint** class for you, in the *WebRole.cs* and *WorkerRole.cs* files.</span></span>
> 
> 

## <a name="onstart-method"></a><span data-ttu-id="d7046-122">OnStart 方法</span><span class="sxs-lookup"><span data-stu-id="d7046-122">OnStart method</span></span>
<span data-ttu-id="d7046-123">當 Azure 將您的角色執行個體連線時，會呼叫 **OnStart** 方法。</span><span class="sxs-lookup"><span data-stu-id="d7046-123">The **OnStart** method is called when your role instance is brought online by Azure.</span></span> <span data-ttu-id="d7046-124">OnStart 程式碼執行時，角色執行個體會標示為 **Busy** ，而且負載平衡器不會將任何外部流量導向至該執行個體。</span><span class="sxs-lookup"><span data-stu-id="d7046-124">While the OnStart code is executing, the role instance is marked as **Busy** and no external traffic will be directed to it by the load balancer.</span></span> <span data-ttu-id="d7046-125">您可以覆寫此方法以執行初始化工作，例如實作事件處理常式及啟動 [Azure 診斷](cloud-services-how-to-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="d7046-125">You can override this method to perform initialization work, such as implementing event handlers and starting [Azure Diagnostics](cloud-services-how-to-monitor.md).</span></span>

<span data-ttu-id="d7046-126">如果 **OnStart** 傳回 **true**，表示成功地初始化執行個體，而且 Azure 會呼叫 **RoleEntryPoint.Run** 方法。</span><span class="sxs-lookup"><span data-stu-id="d7046-126">If **OnStart** returns **true**, the instance is successfully initialized and Azure calls the **RoleEntryPoint.Run** method.</span></span> <span data-ttu-id="d7046-127">如果 **OnStart** 傳回 **false**，角色會立即終止，而不執行任何計劃的關機順序。</span><span class="sxs-lookup"><span data-stu-id="d7046-127">If **OnStart** returns **false**, the role terminates immediately, without executing any planned shutdown sequences.</span></span>

<span data-ttu-id="d7046-128">下列程式碼範例示範如何覆寫 **OnStart** 方法。</span><span class="sxs-lookup"><span data-stu-id="d7046-128">The following code example shows how to override the **OnStart** method.</span></span> <span data-ttu-id="d7046-129">當角色執行個體啟動，並設定將記錄資料傳輸至儲存體帳戶時，此方法會設定並啟動診斷監視器：</span><span class="sxs-lookup"><span data-stu-id="d7046-129">This method configures and starts a diagnostic monitor when the role instance starts and sets up a transfer of logging data to a storage account:</span></span>

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a><span data-ttu-id="d7046-130">OnStop 方法</span><span class="sxs-lookup"><span data-stu-id="d7046-130">OnStop method</span></span>
<span data-ttu-id="d7046-131">在 Azure 將角色執行個體離線之後，以及處理序結束之前，會呼叫 **OnStop** 方法。</span><span class="sxs-lookup"><span data-stu-id="d7046-131">The **OnStop** method is called after a role instance has been taken offline by Azure and before the process exits.</span></span> <span data-ttu-id="d7046-132">您可以覆寫此方法以呼叫讓您的角色執行個體正常關機所需的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d7046-132">You can override this method to call code required for your role instance to cleanly shut down.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7046-133">因為使用者起始關機以外的原因呼叫使用 **OnStop** 方法執行的程式碼時，其完成時間有限。</span><span class="sxs-lookup"><span data-stu-id="d7046-133">Code running in the **OnStop** method has a limited time to finish when it is called for reasons other than a user-initiated shutdown.</span></span> <span data-ttu-id="d7046-134">經過這個時間之後，處理序便會終止，因此您必須確定 **OnStop** 方法中的該程式碼可以快速執行，或容許完成之前不執行。</span><span class="sxs-lookup"><span data-stu-id="d7046-134">After this time elapses, the process is terminated, so you must make sure that code in the **OnStop** method can run quickly or tolerates not running to completion.</span></span> <span data-ttu-id="d7046-135">系統會在引發 **Stopping** 事件之後呼叫 **OnStop** 方法。</span><span class="sxs-lookup"><span data-stu-id="d7046-135">The **OnStop** method is called after the **Stopping** event is raised.</span></span>
> 
> 

## <a name="run-method"></a><span data-ttu-id="d7046-136">Run 方法</span><span class="sxs-lookup"><span data-stu-id="d7046-136">Run method</span></span>
<span data-ttu-id="d7046-137">您可以覆寫 **Run** 方法，針對您的角色執行個體實作長時間執行的執行緒。</span><span class="sxs-lookup"><span data-stu-id="d7046-137">You can override the **Run** method to implement a long-running thread for your role instance.</span></span>

<span data-ttu-id="d7046-138">不需要覆寫 **Run** 方法；預設實作會啟動永久處於睡眠狀態的執行緒。</span><span class="sxs-lookup"><span data-stu-id="d7046-138">Overriding the **Run** method is not required; the default implementation starts a thread that sleeps forever.</span></span> <span data-ttu-id="d7046-139">如果您覆寫 **Run** 方法，您的程式碼應該會無限期地封鎖。</span><span class="sxs-lookup"><span data-stu-id="d7046-139">If you do override the **Run** method, your code should block indefinitely.</span></span> <span data-ttu-id="d7046-140">如果 **Run** 方法返回，就會自動正常回收角色；換句話說，Azure 會引發 **Stopping** 事件並呼叫 **OnStop** 方法，讓您的關機順序可以在角色離線之前執行。</span><span class="sxs-lookup"><span data-stu-id="d7046-140">If the **Run** method returns, the role is automatically gracefully recycled; in other words, Azure raises the **Stopping** event and calls the **OnStop** method so that your shutdown sequences may be executed before the role is taken offline.</span></span>

### <a name="implementing-the-aspnet-lifecycle-methods-for-a-web-role"></a><span data-ttu-id="d7046-141">實作 Web 角色的 ASP.NET 生命週期方法</span><span class="sxs-lookup"><span data-stu-id="d7046-141">Implementing the ASP.NET lifecycle methods for a web role</span></span>
<span data-ttu-id="d7046-142">除了提供 **RoleEntryPoint** 類別提供的方法之外，您還可以使用 ASP.NET 生命週期方法管理 Web 角色的初始化及關機順序。</span><span class="sxs-lookup"><span data-stu-id="d7046-142">You can use the ASP.NET lifecycle methods, in addition to those provided by the **RoleEntryPoint** class, to manage initialization and shutdown sequences for a web role.</span></span> <span data-ttu-id="d7046-143">如果您要將現有的 ASP.NET 應用程式移植至 Azure，這對於相容性可能很有幫助。</span><span class="sxs-lookup"><span data-stu-id="d7046-143">This may be useful for compatibility purposes if you are porting an existing ASP.NET application to Azure.</span></span> <span data-ttu-id="d7046-144">系統會從 **RoleEntryPoint** 方法內呼叫 ASP.NET 生命週期方法。</span><span class="sxs-lookup"><span data-stu-id="d7046-144">The ASP.NET lifecycle methods are called from within the **RoleEntryPoint** methods.</span></span> <span data-ttu-id="d7046-145">系統會在 **RoleEntryPoint.OnStart** 方法完成之後，呼叫 **Application\_Start** 方法。</span><span class="sxs-lookup"><span data-stu-id="d7046-145">The **Application\_Start** method is called after the **RoleEntryPoint.OnStart** method finishes.</span></span> <span data-ttu-id="d7046-146">系統會在呼叫 **RoleEntryPoint.OnStop** 方法之前，呼叫 **Application\_End** 方法。</span><span class="sxs-lookup"><span data-stu-id="d7046-146">The **Application\_End** method is called before the **RoleEntryPoint.OnStop** method is called.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7046-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d7046-147">Next steps</span></span>
<span data-ttu-id="d7046-148">了解如何 [建立雲端服務封裝](cloud-services-model-and-package.md)。</span><span class="sxs-lookup"><span data-stu-id="d7046-148">Learn how to [create a cloud service package](cloud-services-model-and-package.md).</span></span>

