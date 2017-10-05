---
title: "App Service API 應用程式觸發程序 | Microsoft Docs"
description: "如何在 Azure App Service 的 API 應用程式中實作觸發程序"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="9831a-103">Azure App Service API 應用程式觸發程序</span><span class="sxs-lookup"><span data-stu-id="9831a-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="9831a-104">這一版的文章適用於 API Apps 2014-12-01-preview 結構描述版本。</span><span class="sxs-lookup"><span data-stu-id="9831a-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="9831a-105">Overview</span><span class="sxs-lookup"><span data-stu-id="9831a-105">Overview</span></span>
<span data-ttu-id="9831a-106">本文說明如何實作 API 應用程式觸發程序，並從邏輯應用程式加以使用。</span><span class="sxs-lookup"><span data-stu-id="9831a-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="9831a-107">本主題中所有程式碼片段的複製來源為 [FileWatcher API 應用程式的程式碼範例](http://go.microsoft.com/fwlink/?LinkId=534802)。</span><span class="sxs-lookup"><span data-stu-id="9831a-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="9831a-108">請注意，您將需要下載下列 nuget 封裝，以取得本文中建置與執行所需的程式碼： [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/)。</span><span class="sxs-lookup"><span data-stu-id="9831a-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="9831a-109">何謂 API 應用程式觸發程序？</span><span class="sxs-lookup"><span data-stu-id="9831a-109">What are API app triggers?</span></span>
<span data-ttu-id="9831a-110">API 應用程式常會需要引發事件，以讓 API 應用程式用戶端採取適當的動作來回應事件。</span><span class="sxs-lookup"><span data-stu-id="9831a-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="9831a-111">支援此案例的REST API 型機制稱為 API 應用程式觸發程序。</span><span class="sxs-lookup"><span data-stu-id="9831a-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="9831a-112">例如，假設用戶端程式碼使用 [Twitter 連接器 API 應用程式](../connectors/connectors-create-api-twitter.md) ，且您的程式碼必須根據其中包含特定文字的新推文來執行動作。</span><span class="sxs-lookup"><span data-stu-id="9831a-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="9831a-113">在此情況下，您可以設定輪詢或推入觸發程序來加速處理這項需求。</span><span class="sxs-lookup"><span data-stu-id="9831a-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="9831a-114">輪詢觸發程序與推入觸發程序</span><span class="sxs-lookup"><span data-stu-id="9831a-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="9831a-115">目前支援兩種類型的觸發程序：</span><span class="sxs-lookup"><span data-stu-id="9831a-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="9831a-116">輪詢觸發程序 - 用戶端會輪詢 API 應用程式以取得已引發事件的通知</span><span class="sxs-lookup"><span data-stu-id="9831a-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="9831a-117">推入觸發程序 - 當事件引發時，API 應用程式會通知用戶端</span><span class="sxs-lookup"><span data-stu-id="9831a-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="9831a-118">輪詢觸發程序</span><span class="sxs-lookup"><span data-stu-id="9831a-118">Poll trigger</span></span>
<span data-ttu-id="9831a-119">輪詢觸發程序實作為一般的 REST API，並預期它的用戶端 (例如邏輯應用程式) 輪詢它以取得通知。</span><span class="sxs-lookup"><span data-stu-id="9831a-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="9831a-120">用戶端可能會維持狀態，而輪詢觸發程序本身是無狀態的。</span><span class="sxs-lookup"><span data-stu-id="9831a-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="9831a-121">有關要求和回應封包的下列資訊，說明輪詢觸發程序合約的一些重要層面：</span><span class="sxs-lookup"><span data-stu-id="9831a-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="9831a-122">要求</span><span class="sxs-lookup"><span data-stu-id="9831a-122">Request</span></span>
  * <span data-ttu-id="9831a-123">HTTP 方法：GET</span><span class="sxs-lookup"><span data-stu-id="9831a-123">HTTP method: GET</span></span>
  * <span data-ttu-id="9831a-124">參數</span><span class="sxs-lookup"><span data-stu-id="9831a-124">Parameters</span></span>
    * <span data-ttu-id="9831a-125">triggerState - 此選用參數可讓用戶端指定其狀態，以便輪詢觸發程序可以根據指定的狀態，正確決定是否要傳回通知。</span><span class="sxs-lookup"><span data-stu-id="9831a-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="9831a-126">API 特有的參數</span><span class="sxs-lookup"><span data-stu-id="9831a-126">API-specific parameters</span></span>
* <span data-ttu-id="9831a-127">Response</span><span class="sxs-lookup"><span data-stu-id="9831a-127">Response</span></span>
  * <span data-ttu-id="9831a-128">狀態碼 **200** - 要求有效，而且沒有觸發程序的通知。</span><span class="sxs-lookup"><span data-stu-id="9831a-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="9831a-129">通知的內容成為回應主體。</span><span class="sxs-lookup"><span data-stu-id="9831a-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="9831a-130">回應中的 "Retry-After" 標頭會指出，必須透過後續要求呼叫擷取其他通知資料。</span><span class="sxs-lookup"><span data-stu-id="9831a-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="9831a-131">狀態碼 **202** - 要求有效，但沒有新的觸發程序通知。</span><span class="sxs-lookup"><span data-stu-id="9831a-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="9831a-132">狀態碼 **4xx** - 要求無效。</span><span class="sxs-lookup"><span data-stu-id="9831a-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="9831a-133">用戶端不應該重試要求。</span><span class="sxs-lookup"><span data-stu-id="9831a-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="9831a-134">狀態碼 **5xx** - 要求導致內部伺服器錯誤及/或暫時性問題。</span><span class="sxs-lookup"><span data-stu-id="9831a-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="9831a-135">用戶端應該重試要求。</span><span class="sxs-lookup"><span data-stu-id="9831a-135">The client should retry the request.</span></span>

<span data-ttu-id="9831a-136">下列程式碼片段是如何實作輪詢觸發程序的範例。</span><span class="sxs-lookup"><span data-stu-id="9831a-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="9831a-137">若要測試此輪詢觸發程序，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9831a-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="9831a-138">部署驗證設定為 **匿名公用**的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9831a-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="9831a-139">呼叫 **接觸** 作業以接觸檔案。</span><span class="sxs-lookup"><span data-stu-id="9831a-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="9831a-140">下圖顯示透過 Postman 的範例要求。</span><span class="sxs-lookup"><span data-stu-id="9831a-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="9831a-141">![透過 Postman 呼叫接觸作業](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="9831a-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="9831a-142">以在步驟 2 之前設定為時間戳記的 **triggerState** 參數，呼叫輪詢觸發程序。</span><span class="sxs-lookup"><span data-stu-id="9831a-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="9831a-143">下圖顯示透過 Postman 的範例要求。</span><span class="sxs-lookup"><span data-stu-id="9831a-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="9831a-144">![透過 Postman 呼叫輪詢觸發程序](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="9831a-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="9831a-145">推入觸發程序</span><span class="sxs-lookup"><span data-stu-id="9831a-145">Push trigger</span></span>
<span data-ttu-id="9831a-146">推入觸發程序會實作為一般的 REST API，將通知推入已註冊為希望在引發特定事件時收到通知的用戶端。</span><span class="sxs-lookup"><span data-stu-id="9831a-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="9831a-147">下列資訊關於要求和回應封包，說明推入觸發程序合約的一些重要層面。</span><span class="sxs-lookup"><span data-stu-id="9831a-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="9831a-148">要求</span><span class="sxs-lookup"><span data-stu-id="9831a-148">Request</span></span>
  * <span data-ttu-id="9831a-149">HTTP 方法：PUT</span><span class="sxs-lookup"><span data-stu-id="9831a-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="9831a-150">參數</span><span class="sxs-lookup"><span data-stu-id="9831a-150">Parameters</span></span>
    * <span data-ttu-id="9831a-151">觸發程式識別碼：必要項 - 不透明字串 (例如 GUID)，表示推入觸發程序的註冊。</span><span class="sxs-lookup"><span data-stu-id="9831a-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="9831a-152">callbackUrl：必要項 - 當事件引發時所叫用回呼的 URL。</span><span class="sxs-lookup"><span data-stu-id="9831a-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="9831a-153">叫用是一個簡單的 POST HTTP 呼叫。</span><span class="sxs-lookup"><span data-stu-id="9831a-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="9831a-154">API 特有的參數</span><span class="sxs-lookup"><span data-stu-id="9831a-154">API-specific parameters</span></span>
* <span data-ttu-id="9831a-155">Response</span><span class="sxs-lookup"><span data-stu-id="9831a-155">Response</span></span>
  * <span data-ttu-id="9831a-156">狀態碼 **200** - 註冊用戶端的要求成功。</span><span class="sxs-lookup"><span data-stu-id="9831a-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="9831a-157">狀態碼 **4xx** - 要求無效。</span><span class="sxs-lookup"><span data-stu-id="9831a-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="9831a-158">用戶端不應該重試要求。</span><span class="sxs-lookup"><span data-stu-id="9831a-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="9831a-159">狀態碼 **5xx** - 要求導致內部伺服器錯誤及/或暫時性問題。</span><span class="sxs-lookup"><span data-stu-id="9831a-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="9831a-160">用戶端應該重試要求。</span><span class="sxs-lookup"><span data-stu-id="9831a-160">The client should retry the request.</span></span>
* <span data-ttu-id="9831a-161">回呼</span><span class="sxs-lookup"><span data-stu-id="9831a-161">Callback</span></span>
  * <span data-ttu-id="9831a-162">HTTP 方法：POST</span><span class="sxs-lookup"><span data-stu-id="9831a-162">HTTP method: POST</span></span>
  * <span data-ttu-id="9831a-163">要求內文： 通知內容。</span><span class="sxs-lookup"><span data-stu-id="9831a-163">Request body: Notification content.</span></span>

<span data-ttu-id="9831a-164">下列程式碼片段是如何實作推入觸發程序的範例：</span><span class="sxs-lookup"><span data-stu-id="9831a-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="9831a-165">若要測試此輪詢觸發程序，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9831a-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="9831a-166">部署驗證設定為 **匿名公用**的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9831a-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="9831a-167">瀏覽至 [http://requestb.in/](http://requestb.in/) 建立 RequestBin 作為回呼 URL。</span><span class="sxs-lookup"><span data-stu-id="9831a-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="9831a-168">以 GUID 為 **triggerId** 和 RequestBin URL 為 **callbackUrl** 來呼叫推送觸發程序。</span><span class="sxs-lookup"><span data-stu-id="9831a-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="9831a-169">![透過 Postman 呼叫推入觸發程序](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="9831a-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="9831a-170">呼叫 **接觸** 作業以接觸檔案。</span><span class="sxs-lookup"><span data-stu-id="9831a-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="9831a-171">下圖顯示透過 Postman 的範例要求。</span><span class="sxs-lookup"><span data-stu-id="9831a-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="9831a-172">![透過 Postman 呼叫接觸作業](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="9831a-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="9831a-173">請檢查 RequestBin，以確認屬性輸出會叫用推入觸發程序回呼。</span><span class="sxs-lookup"><span data-stu-id="9831a-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="9831a-174">![透過 Postman 呼叫輪詢觸發程序](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="9831a-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="9831a-175">在 API 定義中描述觸發程序</span><span class="sxs-lookup"><span data-stu-id="9831a-175">Describe triggers in API definition</span></span>
<span data-ttu-id="9831a-176">實作觸發程序，並將您的 API 應用程式部署至 Azure 之後，瀏覽至 Azure Preview 入口網站中的 [ **API 定義** ] 刀鋒視窗，然後您會看到 UI 已自動辨識觸發程序 (這是由 API 應用程式的 Swagger 2.0 API 定義所驅動)。</span><span class="sxs-lookup"><span data-stu-id="9831a-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![API 定義刀鋒視窗](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="9831a-178">如果您按一下 [ **下載 Swagger** ] 按鈕並開啟 JSON 檔案，您會看到類似下列的結果：</span><span class="sxs-lookup"><span data-stu-id="9831a-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="9831a-179">擴充屬性 **x-ms-schedular-trigger** 是 API 定義中所描述的觸發程序，而且當您要求透過閘道器要求 API 定義時，若要求符合以下其中一個準則時，API 應用程式閘道會自動加入它。</span><span class="sxs-lookup"><span data-stu-id="9831a-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="9831a-180">(您也可以手動加入這個屬性。)</span><span class="sxs-lookup"><span data-stu-id="9831a-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="9831a-181">輪詢觸發程序</span><span class="sxs-lookup"><span data-stu-id="9831a-181">Poll trigger</span></span>
  * <span data-ttu-id="9831a-182">如果 HTTP 方法為 **GET**。</span><span class="sxs-lookup"><span data-stu-id="9831a-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="9831a-183">如果 **operationId** 屬性包含字串 **trigger**。</span><span class="sxs-lookup"><span data-stu-id="9831a-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="9831a-184">如果 **parameters** 屬性所包含參數的 **name** 屬性設定為 **triggerState**。</span><span class="sxs-lookup"><span data-stu-id="9831a-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="9831a-185">推入觸發程序</span><span class="sxs-lookup"><span data-stu-id="9831a-185">Push trigger</span></span>
  * <span data-ttu-id="9831a-186">如果 HTTP 方法為 **PUT**。</span><span class="sxs-lookup"><span data-stu-id="9831a-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="9831a-187">如果 **operationId** 屬性包含字串 **trigger**。</span><span class="sxs-lookup"><span data-stu-id="9831a-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="9831a-188">如果 **parameters** 屬性所包含參數的 **name** 屬性設定為 **triggerId**。</span><span class="sxs-lookup"><span data-stu-id="9831a-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="9831a-189">在邏輯應用程式中使用 API 應用程式觸發程序</span><span class="sxs-lookup"><span data-stu-id="9831a-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="9831a-190">在邏輯應用程式設計工具中，列出與設定 API 應用程式觸發程序</span><span class="sxs-lookup"><span data-stu-id="9831a-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="9831a-191">如果您在 API 應用程式的相同資源群組中建立邏輯應用程式，您只要按一下它，即可將它加入至設計工具的畫布中。</span><span class="sxs-lookup"><span data-stu-id="9831a-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="9831a-192">請見下圖說明：</span><span class="sxs-lookup"><span data-stu-id="9831a-192">The following images illustrate this:</span></span>

![邏輯應用程式設計工具中的觸發程序](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![在邏輯應用程式設計工具中設定輸詢觸發程序](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![在邏輯應用程式設計工具中設定推入觸發程序](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="9831a-196">為邏輯應用程式最佳化 API 應用程式觸發程序</span><span class="sxs-lookup"><span data-stu-id="9831a-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="9831a-197">將觸發程序加入至 API 應用程式之後，您可以透過幾種方式來改善在邏輯應用程式中使用 API 應用程式的體驗。</span><span class="sxs-lookup"><span data-stu-id="9831a-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="9831a-198">比方說，輪詢觸發程序的 **triggerState** 參數應該在邏輯應用程式中設定為下列運算式。</span><span class="sxs-lookup"><span data-stu-id="9831a-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="9831a-199">此運算式應該評估邏輯應用程式之觸發程序的最後一個叫用，並傳回該值。</span><span class="sxs-lookup"><span data-stu-id="9831a-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="9831a-200">注意：如需上述運算式中所使用函式的說明，請參閱 [邏輯應用程式工作流程定義語言](https://msdn.microsoft.com/library/azure/dn948512.aspx)的文件。</span><span class="sxs-lookup"><span data-stu-id="9831a-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="9831a-201">使用觸發程序時，邏輯應用程式使用者需要為 **triggerState** 參數提供上述運算式。</span><span class="sxs-lookup"><span data-stu-id="9831a-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="9831a-202">邏輯應用程式設計工具可能透過延伸模組屬性 **x-ms-scheduler-recommendation**預先設定此值。</span><span class="sxs-lookup"><span data-stu-id="9831a-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="9831a-203">**x-ms-visibility** 延伸模組屬性的值可以設定為 *internal* ，如此參數本身不會顯示在設計工具上。</span><span class="sxs-lookup"><span data-stu-id="9831a-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="9831a-204">請見下列程式碼片段說明。</span><span class="sxs-lookup"><span data-stu-id="9831a-204">The following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="9831a-205">推入觸發程序的 **triggerId** 參數必須為邏輯應用程式的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="9831a-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="9831a-206">建議的最佳作法是使用下列運算式，將此屬性設定為工作流程的名稱：</span><span class="sxs-lookup"><span data-stu-id="9831a-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="9831a-207">在其 API 定義中使用 **x-ms-scheduler-recommendation** 和 **x-ms-visibility** 擴充屬性，API 應用程式可以傳達給邏輯應用程式設計工具，來自動為使用者設定此運算式。</span><span class="sxs-lookup"><span data-stu-id="9831a-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="9831a-208">在 API 定義中加入延伸模組屬性</span><span class="sxs-lookup"><span data-stu-id="9831a-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="9831a-209">其他中繼資料資訊 (例如擴充屬性 **x-ms-scheduler-recommendation** 和 **x-ms-visibility**) 可以透過以下兩種方式加入 API 定義：靜態或動態。</span><span class="sxs-lookup"><span data-stu-id="9831a-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="9831a-210">對於靜態的中繼資料，您可以直接編輯專案中的 */metadata/apiDefinition.swagger.json* 檔案，並手動加入屬性。</span><span class="sxs-lookup"><span data-stu-id="9831a-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="9831a-211">針對使用動態中繼資料的 API 應用程式，您可以編輯 SwaggerConfig.cs 檔案來加入作業篩選條件，以加入這些延伸模組。</span><span class="sxs-lookup"><span data-stu-id="9831a-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="9831a-212">以下是如何實作這個類別，以協助處理動態中繼資料案例的範例。</span><span class="sxs-lookup"><span data-stu-id="9831a-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
