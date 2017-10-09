---
title: "您的 Azure 程式碼在 Visual Studio 中的 aaaOptimizing |Microsoft 文件"
description: "了解 Visual Studio 中的 Azure 程式碼最佳化工具如何協助讓程式碼更穩定且有更好的效能。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="7ea6e-103">最佳化您的 Azure 程式碼</span><span class="sxs-lookup"><span data-stu-id="7ea6e-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="7ea6e-104">您正在設計程式時使用 Microsoft Azure 的應用程式，有一些編碼方式，您應該遵循 toohelp 避免發生問題的應用程式延展性、 行為和雲端環境中的效能。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow toohelp avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="7ea6e-105">Microsoft 有提供 Azure Code Analysis 工具，可辨識並找出許多常見問題，並幫助您解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="7ea6e-106">您可以下載 Visual Studio 中透過 NuGet 中的 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-106">You can download hello tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="7ea6e-107">Azure Code Analysis 規則</span><span class="sxs-lookup"><span data-stu-id="7ea6e-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="7ea6e-108">hello Azure 程式碼分析工具會使用下列規則 tooautomatically 旗標 Azure 程式碼，並且在找到效能影響的已知的問題的 hello。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-108">hello Azure Code Analysis tool uses hello following rules tooautomatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="7ea6e-109">偵測到的問題會顯示為警告或編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="7ea6e-110">通常透過燈泡圖示提供程式碼修正或建議 tooresolve hello 警告或錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-110">Code fixes or suggestions tooresolve hello warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="7ea6e-111">避免使用預設 (同處理序) 工作階段狀態模式</span><span class="sxs-lookup"><span data-stu-id="7ea6e-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-112">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-112">ID</span></span>
<span data-ttu-id="7ea6e-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="7ea6e-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-114">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-114">Description</span></span>
<span data-ttu-id="7ea6e-115">如果您的雲端應用程式使用 hello 預設 （同處理序） 工作階段狀態模式，您可能會遺失工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-115">If you use hello default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="7ea6e-116">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-117">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-117">Reason</span></span>
<span data-ttu-id="7ea6e-118">根據預設，hello hello web.config 檔案中指定的工作階段狀態模式是同處理序。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-118">By default, hello session state mode specified in hello web.config file is in-process.</span></span> <span data-ttu-id="7ea6e-119">此外，如果沒有 hello 組態檔中指定的項目，hello 工作階段狀態模式會預設 tooin 程序。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-119">Also, if no entry specified in hello configuration file, hello Session State mode defaults tooin-process.</span></span> <span data-ttu-id="7ea6e-120">hello 同處理序模式會將工作階段狀態儲存在 hello web 伺服器上的記憶體。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-120">hello in-process mode stores session state in memory on hello web server.</span></span> <span data-ttu-id="7ea6e-121">當重新啟動執行個體或負載平衡或容錯移轉支援使用新的執行個體時，不會儲存 hello 工作階段狀態儲存在 hello web 伺服器上的記憶體。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-121">When an instance is restarted or a new instance is used for load balancing or failover support, hello session state stored in memory on hello web server isn’t saved.</span></span> <span data-ttu-id="7ea6e-122">這種情況下，防止 hello 從 hello 雲端上可擴充的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-122">This situation prevents hello application from being scalable on hello cloud.</span></span>

<span data-ttu-id="7ea6e-123">ASP.NET 工作階段狀態支援數種不同的工作階段狀態資料儲存選項：InProc、StateServer、SQLServer、自訂和關閉。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="7ea6e-124">建議您自訂模式 toohost 資料上使用外部的工作階段狀態存放區，例如[Redis 的 Azure 工作階段狀態提供者](http://go.microsoft.com/fwlink/?LinkId=401521)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-124">It’s recommended that you use Custom mode toohost data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-125">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-125">Solution</span></span>
<span data-ttu-id="7ea6e-126">建議的解決方案之一，是在受管理快取服務 toostore 工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-126">One recommended solution is toostore session state on a managed cache service.</span></span> <span data-ttu-id="7ea6e-127">深入了解如何 toouse [Redis 的 Azure 工作階段狀態提供者](http://go.microsoft.com/fwlink/?LinkId=401521)toostore 工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-127">Learn how toouse [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore your session state.</span></span> <span data-ttu-id="7ea6e-128">您可以也存放區的工作階段狀態中其他地方 tooensure hello 雲端位於可擴充您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-128">You can also store session state in other places tooensure your application is scalable on hello cloud.</span></span> <span data-ttu-id="7ea6e-129">深入了解替代方案，請閱讀 toolearn[工作階段狀態模式](https://msdn.microsoft.com/library/ms178586)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-129">toolearn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="7ea6e-130">執行方法必須同步</span><span class="sxs-lookup"><span data-stu-id="7ea6e-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-131">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-131">ID</span></span>
<span data-ttu-id="7ea6e-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="7ea6e-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-133">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-133">Description</span></span>
<span data-ttu-id="7ea6e-134">建立非同步方法 (例如[await](https://msdn.microsoft.com/library/hh156528.aspx)) 外部 hello [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法，然後呼叫 hello 非同步方法，從[run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call hello async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="7ea6e-135">宣告 hello [ [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法為非同步會導致 hello 背景工作角色 tooenter 重新啟動迴圈。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-135">Declaring hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes hello worker role tooenter a restart loop.</span></span>

<span data-ttu-id="7ea6e-136">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-137">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-137">Reason</span></span>
<span data-ttu-id="7ea6e-138">Hello 內呼叫非同步方法[run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法會導致 hello 雲端服務執行階段 toorecycle hello 背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-138">Calling async methods inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello cloud service runtime toorecycle hello worker role.</span></span> <span data-ttu-id="7ea6e-139">所有程式執行的背景工作角色啟動時，都都在 hello [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-139">When a worker role starts, all program execution takes place inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="7ea6e-140">現有的 hello [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法會導致 hello 背景工作角色 toorestart。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-140">Exiting hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello worker role toorestart.</span></span> <span data-ttu-id="7ea6e-141">當 hello 背景工作角色執行階段叫用 hello 非同步方法時，它會分派 hello 非同步方法之後的所有作業，然後傳回。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-141">When hello worker role runtime hits hello async method, it dispatches all operations after hello async method and then returns.</span></span> <span data-ttu-id="7ea6e-142">這會導致 hello 背景工作角色 tooexit 從 hello [ [ [ [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法並重新啟動。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-142">This causes hello worker role tooexit from hello [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="7ea6e-143">Hello 下一個反覆項目中執行的再次 hello 非同步方法並重新啟動時，造成 hello 背景工作角色 toorecycle 一次也會叫用 hello 背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-143">In hello next iteration of execution, hello worker role hits hello async method again and restarts, causing hello worker role toorecycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-144">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-144">Solution</span></span>
<span data-ttu-id="7ea6e-145">放置 hello 之外的所有非同步作業[run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-145">Place all async operations outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="7ea6e-146">然後，呼叫 hello 重構非同步方法，從內 hello [ [run （)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法，例如 RunAsync （).wait。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-146">Then, call hello refactored async method from inside hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="7ea6e-147">hello Azure 程式碼分析工具可協助您修正此問題。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-147">hello Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="7ea6e-148">下列程式碼片段的 hello 示範 hello 程式碼修正此問題：</span><span class="sxs-lookup"><span data-stu-id="7ea6e-148">hello following code snippet demonstrates hello code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="7ea6e-149">使用服務匯流排共用存取簽章驗證</span><span class="sxs-lookup"><span data-stu-id="7ea6e-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-150">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-150">ID</span></span>
<span data-ttu-id="7ea6e-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="7ea6e-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-152">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-152">Description</span></span>
<span data-ttu-id="7ea6e-153">使用共用存取簽章 (SAS) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="7ea6e-154">存取控制服務 (ACS) 將不可再用於進行服務匯流排驗證。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="7ea6e-155">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-156">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-156">Reason</span></span>
<span data-ttu-id="7ea6e-157">為加強安全性，Azure Active Directory 將以 SAS 驗證取代 ACS 驗證。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="7ea6e-158">請參閱[Azure Active Directory 是 hello ACS 的未來](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx)hello 轉換計畫的資訊。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-158">See [Azure Active Directory is hello future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on hello transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-159">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-159">Solution</span></span>
<span data-ttu-id="7ea6e-160">在應用程式中使用 SAS 驗證。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="7ea6e-161">hello 下列範例顯示如何 toouse 現有 SAS 權杖 tooaccess 服務匯流排命名空間或實體。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-161">hello following example shows how toouse an existing SAS token tooaccess a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="7ea6e-162">請參閱下列主題以取得詳細資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-162">See hello following topics for more information.</span></span>

* <span data-ttu-id="7ea6e-163">如需概觀，請參閱 [使用服務匯流排的共用存取簽章驗證](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="7ea6e-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="7ea6e-164">如何使用服務匯流排的共用存取簽章驗證 toouse</span><span class="sxs-lookup"><span data-stu-id="7ea6e-164">How toouse Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="7ea6e-165">如須專案範例，請參閱 [搭配使用共用存取簽章 (SAS) 驗證與服務匯流排訂用帳戶](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="7ea6e-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a><span data-ttu-id="7ea6e-166">請考慮使用 OnMessage 方法 tooavoid 「 接收迴圈 」</span><span class="sxs-lookup"><span data-stu-id="7ea6e-166">Consider using OnMessage method tooavoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-167">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-167">ID</span></span>
<span data-ttu-id="7ea6e-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="7ea6e-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-169">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-169">Description</span></span>
<span data-ttu-id="7ea6e-170">進入 「 接收迴圈 」 tooavoid 呼叫 hello **OnMessage**方法是更好的解決方案來接收訊息比呼叫 hello**接收**方法。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-170">tooavoid going into a "receive loop," calling hello **OnMessage** method is a better solution for receiving messages than calling hello **Receive** method.</span></span> <span data-ttu-id="7ea6e-171">不過，如果您必須使用 hello**接收**方法之外，指定非預設伺服器等待時間，請確定 hello 伺服器等待時間超過一分鐘。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-171">However, if you must use hello **Receive** method, and you specify a non-default server wait time, make sure hello server wait time is more than one minute.</span></span>

<span data-ttu-id="7ea6e-172">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-173">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-173">Reason</span></span>
<span data-ttu-id="7ea6e-174">當呼叫**OnMessage**，hello 用戶端啟動內部訊息幫浦，持續地輪詢 hello 佇列或訂閱。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-174">When calling **OnMessage**, hello client starts an internal message pump that constantly polls hello queue or subscription.</span></span> <span data-ttu-id="7ea6e-175">此訊息幫浦包含無限迴圈，發出呼叫 tooreceive 訊息。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-175">This message pump contains an infinite loop that issues a call tooreceive messages.</span></span> <span data-ttu-id="7ea6e-176">如果 hello 呼叫逾時，它就會發出新的呼叫。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-176">If hello call times out, it issues a new call.</span></span> <span data-ttu-id="7ea6e-177">hello 逾時間隔由 hello hello 值[OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx)屬性 hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)正在使用。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-177">hello timeout interval is determined by hello value of hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="7ea6e-178">hello 使用優點**OnMessage**太比較**接收**是使用者不需要輪詢訊息、 處理例外狀況、 處理多個訊息，以平行方式，和完成 hello toomanually訊息。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-178">hello advantage of using **OnMessage** compared too**Receive** is that users don’t have toomanually poll for messages, handle exceptions, process multiple messages in parallel, and complete hello messages.</span></span>

<span data-ttu-id="7ea6e-179">如果您呼叫**接收**不使用其預設值，可確定 hello *ServerWaitTime*值是一分鐘以上。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-179">If you call **Receive** without using its default value, be sure hello *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="7ea6e-180">設定*ServerWaitTime*超過一分鐘 toomore 防止 hello 伺服器完全收到 hello 訊息之前逾時。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-180">Setting *ServerWaitTime* toomore than one minute prevents hello server from timing out before hello message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-181">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-181">Solution</span></span>
<span data-ttu-id="7ea6e-182">請 hello 遵循建議的使用方式的程式碼範例，參閱。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-182">Please see hello following code examples for recommended usages.</span></span> <span data-ttu-id="7ea6e-183">如需詳細資訊，請參閱 [QueueClient.OnMessage 方法 (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) 和 [QueueClient.Receive 方法 (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="7ea6e-184">tooimprove hello 效能的 hello Azure 傳訊基礎結構，請參閱 hello 設計模式[非同步傳訊入門](https://msdn.microsoft.com/library/dn589781.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-184">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="7ea6e-185">hello 以下是示範如何使用**OnMessage** tooreceive 訊息。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-185">hello following is an example of using **OnMessage** tooreceive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

<span data-ttu-id="7ea6e-186">hello 以下是示範如何使用**接收**與 hello 預設伺服器等待時間。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-186">hello following is an example of using **Receive** with hello default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="7ea6e-187">hello 以下是示範如何使用**接收**與非預設伺服器等待時間。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-187">hello following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="7ea6e-188">考慮使用非同步服務匯流排方法</span><span class="sxs-lookup"><span data-stu-id="7ea6e-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-189">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-189">ID</span></span>
<span data-ttu-id="7ea6e-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="7ea6e-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-191">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-191">Description</span></span>
<span data-ttu-id="7ea6e-192">使用非同步服務匯流排方法 tooimprove 效能代理傳訊。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-192">Use asynchronous Service Bus methods tooimprove performance with brokered messaging.</span></span>

<span data-ttu-id="7ea6e-193">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-194">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-194">Reason</span></span>
<span data-ttu-id="7ea6e-195">使用非同步方法可讓應用程式並行存取，因為執行每個呼叫不會封鎖 hello 主要執行緒。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block hello main thread.</span></span> <span data-ttu-id="7ea6e-196">使用服務匯流排傳訊方法時，需要花時間執行各項作業 (傳送、接收、刪除等)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="7ea6e-197">此時根據 hello 服務匯流排服務包括 hello 處理 hello 作業的加法 toohello 延遲 hello 要求與 hello 回覆中。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-197">This time includes hello processing of hello operation by hello Service Bus service in addition toohello latency of hello request and hello reply.</span></span> <span data-ttu-id="7ea6e-198">tooincrease hello 數字，每次的作業，必須同時執行作業。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-198">tooincrease hello number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="7ea6e-199">如需詳細資訊，請參閱太[的效能改進使用 Service Bus 代理訊息的最佳作法](https://msdn.microsoft.com/library/azure/hh528527.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-199">For more information please refer too[Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-200">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-200">Solution</span></span>
<span data-ttu-id="7ea6e-201">請參閱[QueueClient 類別 (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx)有關 toouse hello 建議的非同步方法的使用。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how toouse hello recommended asynchronous method.</span></span>

<span data-ttu-id="7ea6e-202">tooimprove hello 效能的 hello Azure 傳訊基礎結構，請參閱 hello 設計模式[非同步傳訊入門](https://msdn.microsoft.com/library/dn589781.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-202">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="7ea6e-203">考慮分割服務匯流排佇列和主題</span><span class="sxs-lookup"><span data-stu-id="7ea6e-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-204">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-204">ID</span></span>
<span data-ttu-id="7ea6e-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="7ea6e-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-206">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-206">Description</span></span>
<span data-ttu-id="7ea6e-207">分割服務匯流排佇列和主題以獲得更好的服務匯流排傳訊效能。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="7ea6e-208">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-209">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-209">Reason</span></span>
<span data-ttu-id="7ea6e-210">資料分割服務匯流排佇列和主題可提升效能的輸送量和服務的可用性，因為 hello 分割的佇列或主題的整體輸送量不會再受限於單一訊息代理程式或訊息存放區的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="7ea6e-211">此外，即使訊息存放區暫時中斷也不會讓分割後的佇列或主題無法使用。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="7ea6e-212">如需詳細資訊，請參閱 [分割訊息實體](https://msdn.microsoft.com/library/azure/dn520246.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-213">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-213">Solution</span></span>
<span data-ttu-id="7ea6e-214">hello 下列程式碼片段會示範如何 toopartition 傳訊實體。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-214">hello following code snippet shows how toopartition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="7ea6e-215">如需詳細資訊，請參閱[分割服務匯流排佇列和主題 |Microsoft Azure 部落格](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/)與簽出 hello [Microsoft Azure 服務匯流排分割的佇列](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f)範例。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out hello [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="7ea6e-216">不要設定 SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="7ea6e-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-217">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-217">ID</span></span>
<span data-ttu-id="7ea6e-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="7ea6e-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-219">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-219">Description</span></span>
<span data-ttu-id="7ea6e-220">您應該避免使用 SharedAccessStartTimeset toohello tooimmediately 啟動 hello 共用存取原則的目前時間。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-220">You should avoid using SharedAccessStartTimeset toohello current time tooimmediately start hello Shared Access policy.</span></span> <span data-ttu-id="7ea6e-221">您只需要 tooset 這個屬性如果您稍後想 toostart hello 共用存取原則。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-221">You only need tooset this property if you want toostart hello Shared Access policy at a later time.</span></span>

<span data-ttu-id="7ea6e-222">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-223">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-223">Reason</span></span>
<span data-ttu-id="7ea6e-224">時鐘同步處理會讓資料中心彼此間產生些微時差。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="7ea6e-225">例如，您會以邏輯方式將儲存體 SAS 原則設定 hello 開始時間視為 hello 目前的時間使用 DateTime.Now 或類似的方法會導致 hello SAS 原則 tootake 效果立即。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-225">For example, you would logically think setting hello start time of a storage SAS policy as hello current time by using DateTime.Now or a similar method will cause hello SAS policy tootake effect immediately.</span></span> <span data-ttu-id="7ea6e-226">不過，資料中心之間的 hello 時間稍微會造成這個問題，因為某些資料中心時間可能稍微晚於 hello 開始時間，而其他則比較早。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-226">However, hello slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than hello start time, while others ahead of it.</span></span> <span data-ttu-id="7ea6e-227">如此一來，hello SAS 原則可能很快過期 （甚至是立即） 如果 hello 原則存留時間設定太短。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-227">As a result, hello SAS policy can expire quickly (or even immediately) if hello policy lifetime is set too short.</span></span>

<span data-ttu-id="7ea6e-228">如需詳細指引 Azure 儲存體上使用共用存取簽章的詳細資訊，請參閱[簡介資料表 SAS （共用存取簽章）、 佇列 SAS 以及更新 tooBlob SAS-Microsoft Azure 儲存體團隊部落格-網站首頁-MSDN 部落格](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-229">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-229">Solution</span></span>
<span data-ttu-id="7ea6e-230">移除設定 hello hello 共用存取原則的開始時間的 hello 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-230">Remove hello statement that sets hello start time of hello shared access policy.</span></span> <span data-ttu-id="7ea6e-231">hello Azure 程式碼分析工具會提供修正此問題。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-231">hello Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="7ea6e-232">如需有關安全性管理的詳細資訊，請參閱 hello 設計模式[附屬金鑰模式](https://msdn.microsoft.com/library/dn568102.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-232">For more information on security management, please see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="7ea6e-233">下列程式碼片段的 hello 示範 hello 程式碼修正此問題。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-233">hello following code snippet demonstrates hello code fix for this issue.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="7ea6e-234">共用存取原則的到期時間必須超過五分鐘</span><span class="sxs-lookup"><span data-stu-id="7ea6e-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-235">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-235">ID</span></span>
<span data-ttu-id="7ea6e-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="7ea6e-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-237">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-237">Description</span></span>
<span data-ttu-id="7ea6e-238">可以是如往常般到期 tooa 所謂 「 時鐘誤差。 」 的不同位置的資料中心之間的時鐘相差五分鐘</span><span class="sxs-lookup"><span data-stu-id="7ea6e-238">There can be as much as a five minute difference in clocks among datacenters at different locations due tooa condition known as "clock skew."</span></span> <span data-ttu-id="7ea6e-239">tooprevent hello SAS 原則權杖過期之前的已規劃、 設定 hello 到期時間 toobe 超過五分鐘。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-239">tooprevent hello SAS policy token from expiring earlier than planned, set hello expiry time toobe more than five minutes.</span></span>

<span data-ttu-id="7ea6e-240">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-241">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-241">Reason</span></span>
<span data-ttu-id="7ea6e-242">時脈訊號而同步化 hello 世界各地的不同位置的資料中心。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-242">Datacenters at different locations around hello world synchronize by a clock signal.</span></span> <span data-ttu-id="7ea6e-243">因為它需要花費一些時間時脈訊號 tootravel toodifferent 位置，可以有不同的地理位置的資料中心之間的時差雖然真地同步處理的所有項目。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-243">Because it takes time for clock signal tootravel toodifferent locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="7ea6e-244">這項時間差異可能會影響 hello 共用存取原則開始時間和到期間隔。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-244">This time difference can affect hello Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="7ea6e-245">因此，tooensure 共用存取原則會立即生效，不會指定 hello 開始時間。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-245">Therefore, tooensure Shared Access policy takes effect immediately, don’t specify hello start time.</span></span> <span data-ttu-id="7ea6e-246">此外，請確定 hello 到期時間超過 5 分鐘 tooprevent 提早逾時。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-246">In addition, make sure hello expiration time is more than 5 minutes tooprevent early timeout.</span></span>

<span data-ttu-id="7ea6e-247">如需 Azure 儲存體上使用共用存取簽章的詳細資訊，請參閱[簡介資料表 SAS （共用存取簽章）、 佇列 SAS 以及更新 tooBlob SAS-Microsoft Azure 儲存體團隊部落格-網站首頁-MSDN 部落格](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-248">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-248">Solution</span></span>
<span data-ttu-id="7ea6e-249">如需有關安全性管理的詳細資訊，請參閱 hello 設計模式[附屬金鑰模式](https://msdn.microsoft.com/library/dn568102.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-249">For more information on security management, see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="7ea6e-250">hello 以下是範例未指定共用存取原則開始時間。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-250">hello following is an example of not specifying a Shared Access policy start time.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="7ea6e-251">hello 以下是範例原則到期持續時間超過五分鐘的指定共用存取原則開始時間。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-251">hello following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="7ea6e-252">如需詳細資訊，請參閱 [建立和使用共用存取簽章](https://msdn.microsoft.com/library/azure/jj721951.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="7ea6e-253">使用 CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="7ea6e-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-254">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-254">ID</span></span>
<span data-ttu-id="7ea6e-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="7ea6e-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-256">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-256">Description</span></span>
<span data-ttu-id="7ea6e-257">使用 hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx)專案的類別，例如 Azure 網站和 Azure 行動服務不會產生執行階段問題。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-257">Using hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="7ea6e-258">最佳做法，不過，它是個不錯的主意 toouse 雲端[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx)做為統一的管理所有 Azure 雲端應用程式的設定方式。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-258">As a best practice, however, it's a good idea toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="7ea6e-259">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-260">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-260">Reason</span></span>
<span data-ttu-id="7ea6e-261">CloudConfigurationManager 讀取 hello 組態檔案適當 toohello 應用程式環境。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-261">CloudConfigurationManager reads hello configuration file appropriate toohello application environment.</span></span>

[<span data-ttu-id="7ea6e-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="7ea6e-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="7ea6e-263">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-263">Solution</span></span>
<span data-ttu-id="7ea6e-264">重構程式碼 toouse hello [CloudConfigurationManager 類別](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-264">Refactor your code toouse hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="7ea6e-265">Hello Azure 程式碼分析工具會提供程式碼修正此問題。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-265">A code fix for this issue is provided by hello Azure Code Analysis tool.</span></span>

<span data-ttu-id="7ea6e-266">下列程式碼片段的 hello 示範 hello 程式碼修正此問題。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-266">hello following code snippet demonstrates hello code fix for this issue.</span></span> <span data-ttu-id="7ea6e-267">Replace</span><span class="sxs-lookup"><span data-stu-id="7ea6e-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="7ea6e-268">取代為</span><span class="sxs-lookup"><span data-stu-id="7ea6e-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="7ea6e-269">以下是如何 toostore hello App.config 或 Web.config 檔案中的組態設定的範例。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-269">Here's an example of how toostore hello configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="7ea6e-270">新增 hello 設定 toohello hello 設定檔的 appSettings 區段。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-270">Add hello settings toohello appSettings section of hello configuration file.</span></span> <span data-ttu-id="7ea6e-271">hello 以下是上述程式碼範例 hello hello Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-271">hello following is hello Web.config file for hello previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="7ea6e-272">避免使用硬式編碼的連接字串</span><span class="sxs-lookup"><span data-stu-id="7ea6e-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-273">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-273">ID</span></span>
<span data-ttu-id="7ea6e-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="7ea6e-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-275">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-275">Description</span></span>
<span data-ttu-id="7ea6e-276">如果您使用硬式編碼的連接字串，您需要 tooupdate 這些更新版本中，您將有 toomake 變更 tooyour 原始程式碼並重新編譯 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-276">If you use hard-coded connection strings and you need tooupdate them later, you’ll have toomake changes tooyour source code and recompile hello application.</span></span> <span data-ttu-id="7ea6e-277">不過，如果您將連接字串儲存在組態檔時，您稍後可以變更它們只要更新 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating hello configuration file.</span></span>

<span data-ttu-id="7ea6e-278">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-279">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-279">Reason</span></span>
<span data-ttu-id="7ea6e-280">硬式編碼的連接字串是不良作法，因為當連接字串需要 toobe 快速變更時，它會導致問題。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need toobe changed quickly.</span></span> <span data-ttu-id="7ea6e-281">此外，如果 hello 專案需要 toobe 簽入 toosource 控制，硬式編碼的連接字串會造成安全性漏洞因為 hello 字串就可以在 hello 原始碼檢視。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-281">In addition, if hello project needs toobe checked in toosource control, hard-coded connection strings introduce security vulnerabilities since hello strings can be viewed in hello source code.</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-282">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-282">Solution</span></span>
<span data-ttu-id="7ea6e-283">連接字串儲存在 hello 設定檔或 Azure 環境。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-283">Store connection strings in hello configuration files or Azure environments.</span></span>

* <span data-ttu-id="7ea6e-284">對於獨立應用程式，使用 app.config toostore 連接字串設定。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-284">For standalone applications, use app.config toostore connection string settings.</span></span>
* <span data-ttu-id="7ea6e-285">對於 IIS 裝載的 web 應用程式，使用 web.config toostore 連接字串。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-285">For IIS-hosted web applications, use web.config toostore connection strings.</span></span>
* <span data-ttu-id="7ea6e-286">對於 ASP.NET vNext 應用程式，使用 configuration.json toostore 連接字串。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-286">For ASP.NET vNext applications, use configuration.json toostore connection strings.</span></span>

<span data-ttu-id="7ea6e-287">如需使用 web.config 或 app.config 等組態檔的相關資訊，請參閱 [ASP.NET Web 組態指導方針](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="7ea6e-288">如需 Azure 環境變數運作方式的相關資訊，請參閱 [Azure 網站：應用程式字串與連接字串的運作方式](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="7ea6e-289">如需在原始檔控制中儲存連接字串的相關資訊，請參閱 [避免將敏感資訊 (例如連接字串) 放在儲存於原始程式碼儲存機制的檔案](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="7ea6e-290">使用診斷組態檔</span><span class="sxs-lookup"><span data-stu-id="7ea6e-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-291">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-291">ID</span></span>
<span data-ttu-id="7ea6e-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="7ea6e-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-293">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-293">Description</span></span>
<span data-ttu-id="7ea6e-294">而不是使用這類程式碼中設定診斷設定 hello Microsoft.WindowsAzure.Diagnostics 程式設計 API，您應該在 hello diagnostics.wadcfg 檔案設定診斷設定。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-294">Instead of configuring diagnostics settings in your code such as by using hello Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in hello diagnostics.wadcfg file.</span></span> <span data-ttu-id="7ea6e-295">(或者，如果您使用 Azure SDK 2.5，則在 diagnostics.wadcfgx 中設定)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="7ea6e-296">這樣做，您可以變更診斷設定，而不需要 toorecompile 您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-296">By doing this, you can change diagnostics settings without having toorecompile your code.</span></span>

<span data-ttu-id="7ea6e-297">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-298">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-298">Reason</span></span>
<span data-ttu-id="7ea6e-299">之前使用數種不同的方法，則無法設定 Azure SDK 2.5 （這會使用 Azure 診斷 1.3），Azure 診斷 (WAD): 將它加入 toohello 組態 blob 儲存體中使用命令式程式碼、 宣告式組態或預設 hello組態設定。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it toohello configuration blob in storage, by using imperative code, declarative configuration, or hello default configuration.</span></span> <span data-ttu-id="7ea6e-300">不過，hello 慣用方式 tooconfigure 診斷是 toouse XML 組態檔 （diagnostics.wadcfg 或 diagnositcs.wadcfgx SDK 2.5 和更新版本） hello 應用程式專案中。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-300">However, hello preferred way tooconfigure diagnostics is toouse an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in hello application project.</span></span> <span data-ttu-id="7ea6e-301">這種方法，hello diagnostics.wadcfg 檔案完整定義 hello 組態及可以更新並重新部署。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-301">In this approach, hello diagnostics.wadcfg file completely defines hello configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="7ea6e-302">混合 hello 用 hello diagnostics.wadcfg 組態檔以 hello 以程式設計方式設定組態使用 hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)或[RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)類別可能會導致 tooconfusion。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-302">Mixing hello use of hello diagnostics.wadcfg configuration file with hello programmatic methods of setting configurations by using hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead tooconfusion.</span></span> <span data-ttu-id="7ea6e-303">如需詳細資訊，請參閱 [初始化或變更 Azure 診斷組態](https://msdn.microsoft.com/library/azure/hh411537.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="7ea6e-304">從 WAD 1.3 （隨附於 Azure SDK 2.5） 開始，就無法再可能 toouse 程式碼 tooconfigure 診斷。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible toouse code tooconfigure diagnostics.</span></span> <span data-ttu-id="7ea6e-305">如此一來，您可以只提供 hello 組態時套用或更新 hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-305">As a result, you can only provide hello configuration when applying or updating hello diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-306">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-306">Solution</span></span>
<span data-ttu-id="7ea6e-307">使用 hello 診斷組態設計工具 toomove 診斷設定 toohello 診斷組態檔 （中的 diagnositcs.wadcfg 或 diagnositcs.wadcfgx SDK 2.5 和更新版本）。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-307">Use hello diagnostics configuration designer toomove diagnostic settings toohello diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="7ea6e-308">也建議您安裝[Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188)使用 hello 最新的診斷功能。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use hello latest diagnostics feature.</span></span>

1. <span data-ttu-id="7ea6e-309">在 hello 想 tooconfigure hello 角色的捷徑功能表，選擇 內容，然後選擇 hello 設定 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-309">On hello shortcut menu for hello role that you want tooconfigure, choose Properties, and then choose hello Configuration tab.</span></span>
2. <span data-ttu-id="7ea6e-310">在 hello**診斷**區段中，請確定該 hello**啟用診斷**選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-310">In hello **Diagnostics** section, make sure that hello **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="7ea6e-311">選擇 hello**設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-311">Choose hello **Configure** button.</span></span>

   ![存取 hello 啟用診斷 選項](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="7ea6e-313">如需詳細資訊，請參閱 [為 Azure 雲端服務和虛擬機器設定診斷功能](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) 。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="7ea6e-314">避免將 DbContext 物件宣告為靜態</span><span class="sxs-lookup"><span data-stu-id="7ea6e-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="7ea6e-315">ID</span><span class="sxs-lookup"><span data-stu-id="7ea6e-315">ID</span></span>
<span data-ttu-id="7ea6e-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="7ea6e-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="7ea6e-317">說明</span><span class="sxs-lookup"><span data-stu-id="7ea6e-317">Description</span></span>
<span data-ttu-id="7ea6e-318">toosave 記憶體，避免將 DBContext 物件做為靜態宣告。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-318">toosave memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="7ea6e-319">請在 [Azure Code Analysis 意見反應](http://go.microsoft.com/fwlink/?LinkId=403771)分享您的想法和意見。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="7ea6e-320">原因</span><span class="sxs-lookup"><span data-stu-id="7ea6e-320">Reason</span></span>
<span data-ttu-id="7ea6e-321">DBContext 物件保存 hello 從每個呼叫的查詢結果。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-321">DBContext objects hold hello query results from each call.</span></span> <span data-ttu-id="7ea6e-322">Hello 應用程式網域卸載之前，不會處置靜態 DBContext 物件。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-322">Static DBContext objects are not disposed until hello application domain is unloaded.</span></span> <span data-ttu-id="7ea6e-323">因此，靜態 DBContext 物件可能會耗用大量記憶體。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="7ea6e-324">方案</span><span class="sxs-lookup"><span data-stu-id="7ea6e-324">Solution</span></span>
<span data-ttu-id="7ea6e-325">將 DBContext 宣告為區域變數或非靜態執行個體欄位、將它用於工作，然後讓它在使用後受到處置。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="7ea6e-326">下列範例 MVC 控制器類別的 hello 顯示 toouse hello DBContext 物件的方式。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-326">hello following example MVC controller class shows how toouse hello DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="7ea6e-327">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ea6e-327">Next steps</span></span>
<span data-ttu-id="7ea6e-328">toolearn 深入了解最佳化和疑難排解 Azure 應用程式，請參閱[疑難排解 web 應用程式中使用 Visual Studio 的 Azure App Service](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="7ea6e-328">toolearn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
