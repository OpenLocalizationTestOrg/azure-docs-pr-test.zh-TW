---
title: "aaaHandle 雲端服務生命週期事件 |Microsoft 文件"
description: "了解如何使用雲端服務角色的 hello 存留週期方法，在.NET 中"
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
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a><span data-ttu-id="5777a-103">自訂 hello.NET 中的 Web 或背景工作角色的生命週期</span><span class="sxs-lookup"><span data-stu-id="5777a-103">Customize hello Lifecycle of a Web or Worker role in .NET</span></span>
<span data-ttu-id="5777a-104">當您建立背景工作角色時，您必須擴充 hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx)類別可提供方法讓您可讓您的 toooverride 回應 toolifecycle 事件。</span><span class="sxs-lookup"><span data-stu-id="5777a-104">When you create a worker role, you extend hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) class which provides methods for you toooverride that let you respond toolifecycle events.</span></span> <span data-ttu-id="5777a-105">Web 角色的這個類別是選擇性的因此您必須使用它 toorespond toolifecycle 事件。</span><span class="sxs-lookup"><span data-stu-id="5777a-105">For web roles this class is optional, so you must use it toorespond toolifecycle events.</span></span>

## <a name="extend-hello-roleentrypoint-class"></a><span data-ttu-id="5777a-106">擴充 hello RoleEntryPoint 類別</span><span class="sxs-lookup"><span data-stu-id="5777a-106">Extend hello RoleEntryPoint class</span></span>
<span data-ttu-id="5777a-107">hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx)類別包括 Azure 所呼叫的方法時它**啟動**，**執行**，或**停止**web 或背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="5777a-107">hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) class includes methods that are called by Azure when it **starts**, **runs**, or **stops** a web or worker role.</span></span> <span data-ttu-id="5777a-108">您選擇可以覆寫這些方法 toomanage 角色初始化、 角色關機順序或 hello hello 角色的執行緒。</span><span class="sxs-lookup"><span data-stu-id="5777a-108">You can optionally override these methods toomanage role initialization, role shutdown sequences, or hello execution thread of hello role.</span></span> 

<span data-ttu-id="5777a-109">在擴充**RoleEntryPoint**，您應留意下列 hello 方法的行為的 hello:</span><span class="sxs-lookup"><span data-stu-id="5777a-109">When extending **RoleEntryPoint**, you should be aware of hello following behaviors of hello methods:</span></span>

* <span data-ttu-id="5777a-110">hello [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx)和[OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)方法會傳回布林值，因此您很可能 tooreturn **false**這些方法。</span><span class="sxs-lookup"><span data-stu-id="5777a-110">hello [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) and [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) methods return a boolean value, so it is possible tooreturn **false** from these methods.</span></span>
  
   <span data-ttu-id="5777a-111">如果您的程式碼傳回**false**hello 角色程序會突然終止，但不執行任何關閉程序中，您可能必須在位置。</span><span class="sxs-lookup"><span data-stu-id="5777a-111">If your code returns **false**, hello role process is abruptly terminated, without running any shutdown sequence you may have in place.</span></span> <span data-ttu-id="5777a-112">一般情況下，您應該避免傳回**false**從 hello **OnStart**方法。</span><span class="sxs-lookup"><span data-stu-id="5777a-112">In general, you should avoid returning **false** from hello **OnStart** method.</span></span>
* <span data-ttu-id="5777a-113">**RoleEntryPoint** 方法多載中未能攔截的任何例外狀況，都會被視為未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5777a-113">Any uncaught exception within an overload of a **RoleEntryPoint** method is treated as an unhandled exception.</span></span>
  
   <span data-ttu-id="5777a-114">其中一個 hello 存留週期方法內發生的例外狀況，Azure 會引發 hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx)事件，然後終止 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="5777a-114">If an exception occurs within one of hello lifecycle methods, Azure will raise hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) event, and then hello process is terminated.</span></span> <span data-ttu-id="5777a-115">您的角色離線之後，Azure 將重新啟動該角色。</span><span class="sxs-lookup"><span data-stu-id="5777a-115">After your role has been taken offline, it will be restarted by Azure.</span></span> <span data-ttu-id="5777a-116">當未處理的例外狀況發生時，hello[停止](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx)事件就不會引發，和 hello **OnStop**不會呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="5777a-116">When an unhandled exception occurs, hello [Stopping](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) event is not raised, and hello **OnStop** method is not called.</span></span>

<span data-ttu-id="5777a-117">如果您的角色未啟動，或 hello 初始化、 忙碌和停止狀態之間循環您的程式碼可能會擲回未處理的例外狀況，其中每個時間 hello 角色重新啟動的 hello 生命週期事件內。</span><span class="sxs-lookup"><span data-stu-id="5777a-117">If your role does not start, or is recycling between hello initializing, busy, and stopping states, your code may be throwing an unhandled exception within one of hello lifecycle events each time hello role restarts.</span></span> <span data-ttu-id="5777a-118">在此情況下，使用 hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx)事件 toodetermine hello hello 例外狀況的原因並加以適當地處理。</span><span class="sxs-lookup"><span data-stu-id="5777a-118">In this case, use hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) event toodetermine hello cause of hello exception and handle it appropriately.</span></span> <span data-ttu-id="5777a-119">您的角色也可能會傳回從 hello[執行](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法，導致 hello 角色 toorestart。</span><span class="sxs-lookup"><span data-stu-id="5777a-119">Your role may also be returning from hello [Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, which causes hello role toorestart.</span></span> <span data-ttu-id="5777a-120">如需部署狀態的詳細資訊，請參閱[一般問題的原因角色 tooRecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)。</span><span class="sxs-lookup"><span data-stu-id="5777a-120">For more information about deployment states, see [Common Issues Which Cause Roles tooRecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5777a-121">如果您使用 hello **Azure Tools for Microsoft Visual Studio** toodevelop 應用程式 hello 角色專案範本會自動擴充 hello **RoleEntryPoint**類別，在 hello *WebRole.cs*和*WorkerRole.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="5777a-121">If you are using hello **Azure Tools for Microsoft Visual Studio** toodevelop your application, hello role project templates automatically extend hello **RoleEntryPoint** class for you, in hello *WebRole.cs* and *WorkerRole.cs* files.</span></span>
> 
> 

## <a name="onstart-method"></a><span data-ttu-id="5777a-122">OnStart 方法</span><span class="sxs-lookup"><span data-stu-id="5777a-122">OnStart method</span></span>
<span data-ttu-id="5777a-123">hello **OnStart**角色執行個體在 Azure 中有不同的回到線上時，呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="5777a-123">hello **OnStart** method is called when your role instance is brought online by Azure.</span></span> <span data-ttu-id="5777a-124">Hello 角色執行個體 hello OnStart 程式碼執行時，會標示為**忙碌**任何外部流量將會導向的 tooit hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5777a-124">While hello OnStart code is executing, hello role instance is marked as **Busy** and no external traffic will be directed tooit by hello load balancer.</span></span> <span data-ttu-id="5777a-125">您可以覆寫此方法 tooperform 初始化工作，例如實作事件處理常式及啟動[Azure 診斷](cloud-services-how-to-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="5777a-125">You can override this method tooperform initialization work, such as implementing event handlers and starting [Azure Diagnostics](cloud-services-how-to-monitor.md).</span></span>

<span data-ttu-id="5777a-126">如果**OnStart**傳回**true**、 hello 執行個體已成功初始化，且 Azure 會呼叫 hello **RoleEntryPoint.Run**方法。</span><span class="sxs-lookup"><span data-stu-id="5777a-126">If **OnStart** returns **true**, hello instance is successfully initialized and Azure calls hello **RoleEntryPoint.Run** method.</span></span> <span data-ttu-id="5777a-127">如果**OnStart**傳回**false**，hello 角色，立即結束，而不執行任何計劃的關機順序。</span><span class="sxs-lookup"><span data-stu-id="5777a-127">If **OnStart** returns **false**, hello role terminates immediately, without executing any planned shutdown sequences.</span></span>

<span data-ttu-id="5777a-128">hello 下列程式碼範例顯示如何 toooverride hello **OnStart**方法。</span><span class="sxs-lookup"><span data-stu-id="5777a-128">hello following code example shows how toooverride hello **OnStart** method.</span></span> <span data-ttu-id="5777a-129">這個方法會設定並啟動診斷監視器時 hello 角色執行個體啟動，並且設定傳輸記錄資料 tooa 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="5777a-129">This method configures and starts a diagnostic monitor when hello role instance starts and sets up a transfer of logging data tooa storage account:</span></span>

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

## <a name="onstop-method"></a><span data-ttu-id="5777a-130">OnStop 方法</span><span class="sxs-lookup"><span data-stu-id="5777a-130">OnStop method</span></span>
<span data-ttu-id="5777a-131">hello **OnStop**離線之後，角色執行個體已由 Azure 和 hello 處理序結束之前，呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="5777a-131">hello **OnStop** method is called after a role instance has been taken offline by Azure and before hello process exits.</span></span> <span data-ttu-id="5777a-132">您可以覆寫此方法的 toocall 程式碼所需的關閉您角色執行個體 toocleanly。</span><span class="sxs-lookup"><span data-stu-id="5777a-132">You can override this method toocall code required for your role instance toocleanly shut down.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5777a-133">在 hello 中執行的程式碼**OnStop**方法具有有限的時間 toofinish 以外的使用者起始關機的原因而呼叫時。</span><span class="sxs-lookup"><span data-stu-id="5777a-133">Code running in hello **OnStop** method has a limited time toofinish when it is called for reasons other than a user-initiated shutdown.</span></span> <span data-ttu-id="5777a-134">這段時間之後，hello 程序即會終止，因此您必須確定該程式碼中 hello **OnStop**方法可快速地執行或容許中斷 toocompletion 未執行。</span><span class="sxs-lookup"><span data-stu-id="5777a-134">After this time elapses, hello process is terminated, so you must make sure that code in hello **OnStop** method can run quickly or tolerates not running toocompletion.</span></span> <span data-ttu-id="5777a-135">hello **OnStop**方法呼叫之後 hello**停止**就會引發事件。</span><span class="sxs-lookup"><span data-stu-id="5777a-135">hello **OnStop** method is called after hello **Stopping** event is raised.</span></span>
> 
> 

## <a name="run-method"></a><span data-ttu-id="5777a-136">Run 方法</span><span class="sxs-lookup"><span data-stu-id="5777a-136">Run method</span></span>
<span data-ttu-id="5777a-137">您可以覆寫 hello**執行**方法 tooimplement 角色執行個體長時間執行的執行緒。</span><span class="sxs-lookup"><span data-stu-id="5777a-137">You can override hello **Run** method tooimplement a long-running thread for your role instance.</span></span>

<span data-ttu-id="5777a-138">覆寫 hello**執行**方法並非必要; hello 的預設實作會啟動永久處於睡眠狀態的執行緒。</span><span class="sxs-lookup"><span data-stu-id="5777a-138">Overriding hello **Run** method is not required; hello default implementation starts a thread that sleeps forever.</span></span> <span data-ttu-id="5777a-139">如果您不要覆寫 hello**執行**方法，您的程式碼應無限期地封鎖。</span><span class="sxs-lookup"><span data-stu-id="5777a-139">If you do override hello **Run** method, your code should block indefinitely.</span></span> <span data-ttu-id="5777a-140">如果 hello**執行**方法傳回時，會自動地正常回收 hello 角色; 換句話說，Azure 會引發 hello**停止**事件並呼叫 hello **OnStop**方法讓hello 角色離線之前，會先執行關機順序。</span><span class="sxs-lookup"><span data-stu-id="5777a-140">If hello **Run** method returns, hello role is automatically gracefully recycled; in other words, Azure raises hello **Stopping** event and calls hello **OnStop** method so that your shutdown sequences may be executed before hello role is taken offline.</span></span>

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a><span data-ttu-id="5777a-141">Web 角色的實作 hello ASP.NET 存留週期方法</span><span class="sxs-lookup"><span data-stu-id="5777a-141">Implementing hello ASP.NET lifecycle methods for a web role</span></span>
<span data-ttu-id="5777a-142">您可以使用 hello ASP.NET 存留週期方法，除了 toothose 提供 hello **RoleEntryPoint**類別，為 web 角色的 toomanage 初始化及關機順序。</span><span class="sxs-lookup"><span data-stu-id="5777a-142">You can use hello ASP.NET lifecycle methods, in addition toothose provided by hello **RoleEntryPoint** class, toomanage initialization and shutdown sequences for a web role.</span></span> <span data-ttu-id="5777a-143">如果您要移植現有的 ASP.NET 應用程式 tooAzure，這可能是適用於相容性用途。</span><span class="sxs-lookup"><span data-stu-id="5777a-143">This may be useful for compatibility purposes if you are porting an existing ASP.NET application tooAzure.</span></span> <span data-ttu-id="5777a-144">hello ASP.NET 存留週期方法從呼叫 hello 內**RoleEntryPoint**方法。</span><span class="sxs-lookup"><span data-stu-id="5777a-144">hello ASP.NET lifecycle methods are called from within hello **RoleEntryPoint** methods.</span></span> <span data-ttu-id="5777a-145">hello**應用程式\_啟動**方法呼叫之後 hello **RoleEntryPoint.OnStart**方法完成。</span><span class="sxs-lookup"><span data-stu-id="5777a-145">hello **Application\_Start** method is called after hello **RoleEntryPoint.OnStart** method finishes.</span></span> <span data-ttu-id="5777a-146">hello**應用程式\_結束**方法 hello 之前呼叫**Application_end**方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="5777a-146">hello **Application\_End** method is called before hello **RoleEntryPoint.OnStop** method is called.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5777a-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5777a-147">Next steps</span></span>
<span data-ttu-id="5777a-148">了解如何太[建立雲端服務封裝](cloud-services-model-and-package.md)。</span><span class="sxs-lookup"><span data-stu-id="5777a-148">Learn how too[create a cloud service package](cloud-services-model-and-package.md).</span></span>

