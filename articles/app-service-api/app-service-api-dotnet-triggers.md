---
title: "aaaApp 服務 API 的應用程式觸發程序 |Microsoft 文件"
description: "Tooimplement 觸發程序在 Azure App Service API 應用程式中"
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
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="af26d-103">Azure App Service API 應用程式觸發程序</span><span class="sxs-lookup"><span data-stu-id="af26d-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="af26d-104">這個版本的 hello 文件適用於 tooAPI 應用程式 2014年-12-01-預覽結構描述版本。</span><span class="sxs-lookup"><span data-stu-id="af26d-104">This version of hello article applies tooAPI apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="af26d-105">概觀</span><span class="sxs-lookup"><span data-stu-id="af26d-105">Overview</span></span>
<span data-ttu-id="af26d-106">本文說明如何觸發 tooimplement API 應用程式，並從邏輯應用程式中使用它們。</span><span class="sxs-lookup"><span data-stu-id="af26d-106">This article explains how tooimplement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="af26d-107">所有 hello 本主題中的程式碼片段會從 hello 複製[監看員活動 API 應用程式程式碼範例](http://go.microsoft.com/fwlink/?LinkId=534802)。</span><span class="sxs-lookup"><span data-stu-id="af26d-107">All of hello code snippets in this topic are copied from hello [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="af26d-108">請注意，您必須遵循本文章 toobuild 中的 hello 程式碼的 nuget 封裝，並執行 toodownload hello: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/)。</span><span class="sxs-lookup"><span data-stu-id="af26d-108">Note that you'll need toodownload hello following nuget package for hello code in this article toobuild and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="af26d-109">何謂 API 應用程式觸發程序？</span><span class="sxs-lookup"><span data-stu-id="af26d-109">What are API app triggers?</span></span>
<span data-ttu-id="af26d-110">它是 API 應用程式 toofire 事件的常見案例，以便 hello API 應用程式的用戶端可以採取回應 toohello 事件中的 hello 適當的動作。</span><span class="sxs-lookup"><span data-stu-id="af26d-110">It's a common scenario for an API app toofire an event so that clients of hello API app can take hello appropriate action in response toohello event.</span></span> <span data-ttu-id="af26d-111">hello REST API 為基礎的機制，支援這種情況下會呼叫的應用程式開發介面應用程式觸發程序。</span><span class="sxs-lookup"><span data-stu-id="af26d-111">hello REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="af26d-112">例如，假設您的用戶端程式碼會使用 hello [Twitter 連接器 API 應用程式](../connectors/connectors-create-api-twitter.md)和您的程式碼需要的 tooperform 新推文包含特定文字為基礎的動作。</span><span class="sxs-lookup"><span data-stu-id="af26d-112">For example, let's say your client code is using hello [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs tooperform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="af26d-113">在此情況下，您可能設定輪詢或推播的觸發程序 toofacilitate 這項需求。</span><span class="sxs-lookup"><span data-stu-id="af26d-113">In this case, you might set up a poll or push trigger toofacilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="af26d-114">輪詢觸發程序與推入觸發程序</span><span class="sxs-lookup"><span data-stu-id="af26d-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="af26d-115">目前支援兩種類型的觸發程序：</span><span class="sxs-lookup"><span data-stu-id="af26d-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="af26d-116">輪詢觸發程序-用戶端輪詢 hello API 的應用程式的需要被引發的事件通知</span><span class="sxs-lookup"><span data-stu-id="af26d-116">Poll trigger - Client polls hello API app for notification of an event having been fired</span></span>
* <span data-ttu-id="af26d-117">推入觸發程序-用戶端會收到 hello API 應用程式時就會引發事件</span><span class="sxs-lookup"><span data-stu-id="af26d-117">Push trigger - Client is notified by hello API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="af26d-118">輪詢觸發程序</span><span class="sxs-lookup"><span data-stu-id="af26d-118">Poll trigger</span></span>
<span data-ttu-id="af26d-119">輪詢觸發程序實作為一般的 REST API，而且必須要有其用戶端 （例如邏輯應用程式） toopoll 順序 tooget 通知中。</span><span class="sxs-lookup"><span data-stu-id="af26d-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) toopoll it in order tooget notification.</span></span> <span data-ttu-id="af26d-120">Hello 用戶端可能會維護狀態，而 hello 輪詢觸發程序本身是無狀態。</span><span class="sxs-lookup"><span data-stu-id="af26d-120">While hello client may maintain state, hello poll trigger itself is stateless.</span></span>

<span data-ttu-id="af26d-121">hello 遵循 hello 要求和回應封包的相關資訊說明 hello 輪詢觸發程序合約的一些重要的層面：</span><span class="sxs-lookup"><span data-stu-id="af26d-121">hello following information regarding hello request and response packets illustrate some key aspects of hello poll trigger contract:</span></span>

* <span data-ttu-id="af26d-122">要求</span><span class="sxs-lookup"><span data-stu-id="af26d-122">Request</span></span>
  * <span data-ttu-id="af26d-123">HTTP 方法：GET</span><span class="sxs-lookup"><span data-stu-id="af26d-123">HTTP method: GET</span></span>
  * <span data-ttu-id="af26d-124">參數</span><span class="sxs-lookup"><span data-stu-id="af26d-124">Parameters</span></span>
    * <span data-ttu-id="af26d-125">triggerState-此選用參數可讓用戶端 toospecify 其狀態，因此，hello 輪詢觸發程序才能正確地決定 tooreturn 通知或未根據的 hello 特定狀態。</span><span class="sxs-lookup"><span data-stu-id="af26d-125">triggerState - This optional parameter allows clients toospecify their state so that hello poll trigger can properly decide whether tooreturn notification or not based on hello specified state.</span></span>
    * <span data-ttu-id="af26d-126">API 特有的參數</span><span class="sxs-lookup"><span data-stu-id="af26d-126">API-specific parameters</span></span>
* <span data-ttu-id="af26d-127">Response</span><span class="sxs-lookup"><span data-stu-id="af26d-127">Response</span></span>
  * <span data-ttu-id="af26d-128">狀態碼**200** -要求無效，而且沒有從 hello 觸發程序的通知。</span><span class="sxs-lookup"><span data-stu-id="af26d-128">Status code **200** - Request is valid and there is a notification from hello trigger.</span></span> <span data-ttu-id="af26d-129">hello 通知的 hello 內容會 hello 回應主體。</span><span class="sxs-lookup"><span data-stu-id="af26d-129">hello content of hello notification will be hello response body.</span></span> <span data-ttu-id="af26d-130">「 重試-呼叫後 」 標頭 hello 回應中的指出必須擷取的後續要求呼叫的其他通知資料。</span><span class="sxs-lookup"><span data-stu-id="af26d-130">A "Retry-After" header in hello response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="af26d-131">狀態碼**202** -要求有效，但沒有任何新的通知，從 hello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="af26d-131">Status code **202** - Request is valid, but there is no new notification from hello trigger.</span></span>
  * <span data-ttu-id="af26d-132">狀態碼 **4xx** - 要求無效。</span><span class="sxs-lookup"><span data-stu-id="af26d-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="af26d-133">hello 用戶端應該不會重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="af26d-133">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="af26d-134">狀態碼 **5xx** - 要求導致內部伺服器錯誤及/或暫時性問題。</span><span class="sxs-lookup"><span data-stu-id="af26d-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="af26d-135">hello 用戶端應該重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="af26d-135">hello client should retry hello request.</span></span>

<span data-ttu-id="af26d-136">下列程式碼片段的 hello 是如何 tooimplement 輪詢觸發程序的範例。</span><span class="sxs-lookup"><span data-stu-id="af26d-136">hello following code snippet is an example of how tooimplement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="af26d-137">tootest 輪詢此觸發程序，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="af26d-137">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="af26d-138">部署 hello API 應用程式與驗證設定的**匿名公用**。</span><span class="sxs-lookup"><span data-stu-id="af26d-138">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="af26d-139">呼叫 hello**觸控**作業 tootouch 檔案。</span><span class="sxs-lookup"><span data-stu-id="af26d-139">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="af26d-140">hello 下列影像顯示的範例要求透過郵差。</span><span class="sxs-lookup"><span data-stu-id="af26d-140">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="af26d-141">![透過 Postman 呼叫接觸作業](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="af26d-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="af26d-142">呼叫 hello 輪詢觸發程序以 hello **triggerState**參數設定 tooa 時間戳記之前 tooStep #2。</span><span class="sxs-lookup"><span data-stu-id="af26d-142">Call hello poll trigger with hello **triggerState** parameter set tooa time stamp prior tooStep #2.</span></span> <span data-ttu-id="af26d-143">hello 下圖顯示透過郵差 hello 範例要求。</span><span class="sxs-lookup"><span data-stu-id="af26d-143">hello following image shows hello sample request via Postman.</span></span>
   <span data-ttu-id="af26d-144">![透過 Postman 呼叫輪詢觸發程序](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="af26d-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="af26d-145">推入觸發程序</span><span class="sxs-lookup"><span data-stu-id="af26d-145">Push trigger</span></span>
<span data-ttu-id="af26d-146">推入觸發程序會實作為一般的 REST API，將推入通知 tooclients 註冊了 toobe 引發特定事件時收到通知。</span><span class="sxs-lookup"><span data-stu-id="af26d-146">A push trigger is implemented as a regular REST API that pushes notifications tooclients who have registered toobe notified when specific events fire.</span></span>

<span data-ttu-id="af26d-147">hello 遵循 hello 要求和回應封包的相關資訊說明 hello 推入觸發程序合約某些重要的部分。</span><span class="sxs-lookup"><span data-stu-id="af26d-147">hello following information regarding hello request and response packets illustrate some key aspects of hello push trigger contract.</span></span>

* <span data-ttu-id="af26d-148">要求</span><span class="sxs-lookup"><span data-stu-id="af26d-148">Request</span></span>
  * <span data-ttu-id="af26d-149">HTTP 方法：PUT</span><span class="sxs-lookup"><span data-stu-id="af26d-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="af26d-150">參數</span><span class="sxs-lookup"><span data-stu-id="af26d-150">Parameters</span></span>
    * <span data-ttu-id="af26d-151">triggerId： 需要-不透明的字串 （例如 GUID) 代表 hello 註冊推入觸發程序。</span><span class="sxs-lookup"><span data-stu-id="af26d-151">triggerId: required - Opaque string (such as a GUID) that represents hello registration of a push trigger.</span></span>
    * <span data-ttu-id="af26d-152">callbackUrl： 需要-hello 回呼 tooinvoke hello 事件引發時的 URL。</span><span class="sxs-lookup"><span data-stu-id="af26d-152">callbackUrl: required - URL of hello callback tooinvoke when hello event fires.</span></span> <span data-ttu-id="af26d-153">hello 引動過程是簡單的 POST HTTP 呼叫。</span><span class="sxs-lookup"><span data-stu-id="af26d-153">hello invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="af26d-154">API 特有的參數</span><span class="sxs-lookup"><span data-stu-id="af26d-154">API-specific parameters</span></span>
* <span data-ttu-id="af26d-155">Response</span><span class="sxs-lookup"><span data-stu-id="af26d-155">Response</span></span>
  * <span data-ttu-id="af26d-156">狀態碼**200** -成功的要求 tooregister 用戶端。</span><span class="sxs-lookup"><span data-stu-id="af26d-156">Status code **200** - Request tooregister client successful.</span></span>
  * <span data-ttu-id="af26d-157">狀態碼 **4xx** - 要求無效。</span><span class="sxs-lookup"><span data-stu-id="af26d-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="af26d-158">hello 用戶端應該不會重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="af26d-158">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="af26d-159">狀態碼 **5xx** - 要求導致內部伺服器錯誤及/或暫時性問題。</span><span class="sxs-lookup"><span data-stu-id="af26d-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="af26d-160">hello 用戶端應該重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="af26d-160">hello client should retry hello request.</span></span>
* <span data-ttu-id="af26d-161">回呼</span><span class="sxs-lookup"><span data-stu-id="af26d-161">Callback</span></span>
  * <span data-ttu-id="af26d-162">HTTP 方法：POST</span><span class="sxs-lookup"><span data-stu-id="af26d-162">HTTP method: POST</span></span>
  * <span data-ttu-id="af26d-163">要求內文： 通知內容。</span><span class="sxs-lookup"><span data-stu-id="af26d-163">Request body: Notification content.</span></span>

<span data-ttu-id="af26d-164">下列程式碼片段的 hello 是如何 tooimplement 推入觸發程序的範例：</span><span class="sxs-lookup"><span data-stu-id="af26d-164">hello following code snippet is an example of how tooimplement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
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
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="af26d-165">tootest 輪詢此觸發程序，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="af26d-165">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="af26d-166">部署 hello API 應用程式與驗證設定的**匿名公用**。</span><span class="sxs-lookup"><span data-stu-id="af26d-166">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="af26d-167">瀏覽過[http://requestb.in/](http://requestb.in/) toocreate RequestBin 這將做為回呼 URL。</span><span class="sxs-lookup"><span data-stu-id="af26d-167">Browse too[http://requestb.in/](http://requestb.in/) toocreate a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="af26d-168">呼叫 hello 推入觸發程序以做為 GUID **triggerId**和 hello RequestBin URL 做為**callbackUrl**。</span><span class="sxs-lookup"><span data-stu-id="af26d-168">Call hello push trigger with a GUID as **triggerId** and hello RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="af26d-169">![透過 Postman 呼叫推入觸發程序](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="af26d-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="af26d-170">呼叫 hello**觸控**作業 tootouch 檔案。</span><span class="sxs-lookup"><span data-stu-id="af26d-170">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="af26d-171">hello 下列影像顯示的範例要求透過郵差。</span><span class="sxs-lookup"><span data-stu-id="af26d-171">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="af26d-172">![透過 Postman 呼叫接觸作業](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="af26d-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="af26d-173">請檢查 hello 推入觸發程序回呼的 hello RequestBin tooconfirm 用來叫用輸出屬性。</span><span class="sxs-lookup"><span data-stu-id="af26d-173">Check hello RequestBin tooconfirm that hello push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="af26d-174">![透過 Postman 呼叫輪詢觸發程序](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="af26d-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="af26d-175">在 API 定義中描述觸發程序</span><span class="sxs-lookup"><span data-stu-id="af26d-175">Describe triggers in API definition</span></span>
<span data-ttu-id="af26d-176">實作 hello 觸發程序及部署之後您的應用程式開發介面應用程式 tooAzure，瀏覽 toohello **API 定義**刀鋒視窗中 hello Azure preview 入口網站，而且您會看到觸發程序會自動辨識在 UI，由所驅動 hellohello Swagger 2.0 API 中定義的 hello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="af26d-176">After implementing hello triggers and deploying your API app tooAzure, navigate toohello **API Definition** blade in hello Azure preview portal and you'll see that triggers are automatically recognized in hello UI, which is driven by hello Swagger 2.0 API definition of hello API app.</span></span>

![API 定義刀鋒視窗](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="af26d-178">如果您按一下 hello**下載 Swagger**按鈕並開啟 hello JSON 檔案，您會看到下列結果類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="af26d-178">If you click hello **Download Swagger** button and open hello JSON file, you'll see results similar toohello following:</span></span>

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

<span data-ttu-id="af26d-179">hello 延伸模組屬性**x-ms-schedular-觸發程序**是觸發程序的應用程式開發介面定義中所述的方式，而且當您要求透過 hello 閘道 hello API 定義如果 hello 要求的 tooone 會自動加入 hello API 應用程式閘道下列準則的 hello。</span><span class="sxs-lookup"><span data-stu-id="af26d-179">hello extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by hello API app gateway when you request hello API definition via hello gateway if hello request tooone of hello following criteria.</span></span> <span data-ttu-id="af26d-180">(您也可以手動加入這個屬性。)</span><span class="sxs-lookup"><span data-stu-id="af26d-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="af26d-181">輪詢觸發程序</span><span class="sxs-lookup"><span data-stu-id="af26d-181">Poll trigger</span></span>
  * <span data-ttu-id="af26d-182">如果 HTTP 方法 hello**取得**。</span><span class="sxs-lookup"><span data-stu-id="af26d-182">If hello HTTP method is **GET**.</span></span>
  * <span data-ttu-id="af26d-183">如果 hello **operationId**屬性包含字串 hello**觸發程序**。</span><span class="sxs-lookup"><span data-stu-id="af26d-183">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="af26d-184">如果 hello**參數**屬性包含具有參數**名稱**屬性設定太**triggerState**。</span><span class="sxs-lookup"><span data-stu-id="af26d-184">If hello **parameters** property includes a parameter with a **name** property set too**triggerState**.</span></span>
* <span data-ttu-id="af26d-185">推入觸發程序</span><span class="sxs-lookup"><span data-stu-id="af26d-185">Push trigger</span></span>
  * <span data-ttu-id="af26d-186">如果 HTTP 方法 hello**放**。</span><span class="sxs-lookup"><span data-stu-id="af26d-186">If hello HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="af26d-187">如果 hello **operationId**屬性包含字串 hello**觸發程序**。</span><span class="sxs-lookup"><span data-stu-id="af26d-187">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="af26d-188">如果 hello**參數**屬性包含具有參數**名稱**屬性設定太**triggerId**。</span><span class="sxs-lookup"><span data-stu-id="af26d-188">If hello **parameters** property includes a parameter with a **name** property set too**triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="af26d-189">在邏輯應用程式中使用 API 應用程式觸發程序</span><span class="sxs-lookup"><span data-stu-id="af26d-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a><span data-ttu-id="af26d-190">列出及 hello 邏輯應用程式的設計工具中設定應用程式開發介面應用程式觸發程序</span><span class="sxs-lookup"><span data-stu-id="af26d-190">List and configure API app triggers in hello Logic apps designer</span></span>
<span data-ttu-id="af26d-191">如果您在 hello 中建立邏輯應用程式相同的資源群組，做為 hello API 應用程式，您將會無法 tooadd 它 toohello 設計工具的畫布，只要按一下它。</span><span class="sxs-lookup"><span data-stu-id="af26d-191">If you create a Logic app in hello same resource group as hello API app, you will be able tooadd it toohello designer canvas simply by clicking it.</span></span> <span data-ttu-id="af26d-192">下列映像的 hello 來說明這點：</span><span class="sxs-lookup"><span data-stu-id="af26d-192">hello following images illustrate this:</span></span>

![邏輯應用程式設計工具中的觸發程序](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![在邏輯應用程式設計工具中設定輸詢觸發程序](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![在邏輯應用程式設計工具中設定推入觸發程序](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="af26d-196">為邏輯應用程式最佳化 API 應用程式觸發程序</span><span class="sxs-lookup"><span data-stu-id="af26d-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="af26d-197">新增觸發程序 tooan API 應用程式之後，有幾件事，在邏輯應用程式中使用 hello API 應用程式時，您可以執行 tooimprove hello 體驗。</span><span class="sxs-lookup"><span data-stu-id="af26d-197">After you add triggers tooan API app, there are a few things you can do tooimprove hello experience when using hello API app in a Logic app.</span></span>

<span data-ttu-id="af26d-198">比方說，hello **triggerState**輪詢觸發程序的參數應設 toohello 下列 hello 邏輯應用程式中的運算式。</span><span class="sxs-lookup"><span data-stu-id="af26d-198">For instance, hello **triggerState** parameter for poll triggers should be set toohello following expression in hello Logic app.</span></span> <span data-ttu-id="af26d-199">這個運算式應該評估 hello hello 邏輯應用程式，從 hello 觸發程序的最後一個引動過程，傳回的值。</span><span class="sxs-lookup"><span data-stu-id="af26d-199">This expression should evaluate hello last invocation of hello trigger from hello Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="af26d-200">注意： 如需使用在上面的 hello 運算式中的 hello 函式的說明，請參閱 toohello 文件上[邏輯應用程式工作流程定義語言](https://msdn.microsoft.com/library/azure/dn948512.aspx)。</span><span class="sxs-lookup"><span data-stu-id="af26d-200">NOTE: For an explanation of hello functions used in hello expression above, refer toohello documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="af26d-201">邏輯應用程式的使用者將需要 tooprovide hello 運算式上方 hello **triggerState**時使用 hello 觸發程序的參數。</span><span class="sxs-lookup"><span data-stu-id="af26d-201">Logic app users would need tooprovide hello expression above for hello **triggerState** parameter while using hello trigger.</span></span> <span data-ttu-id="af26d-202">它是透過 hello 延伸模組屬性的 hello 邏輯應用程式設計師可能 toohave 此值預設**x ms-排程器建議**。</span><span class="sxs-lookup"><span data-stu-id="af26d-202">It is possible toohave this value preset by hello Logic app designer through hello extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="af26d-203">hello **x ms 可見度**延伸模組屬性可以設定 tooa 值*內部*以便 hello 參數本身不會顯示 hello 設計工具上。</span><span class="sxs-lookup"><span data-stu-id="af26d-203">hello **x-ms-visibility** extension property can be set tooa value of *internal* so that hello parameter itself is not shown on hello designer.</span></span>  <span data-ttu-id="af26d-204">hello，下列程式碼片段將說明。</span><span class="sxs-lookup"><span data-stu-id="af26d-204">hello following snippet illustrates that.</span></span>

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

<span data-ttu-id="af26d-205">推入觸發程序，hello **triggerId**參數必須唯一識別 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="af26d-205">For push triggers, hello **triggerId** parameter must uniquely identify hello Logic app.</span></span> <span data-ttu-id="af26d-206">建議的最佳作法是的 tooset hello 工作流程使用的這個屬性 toohello 名稱 hello 下列運算式：</span><span class="sxs-lookup"><span data-stu-id="af26d-206">A recommended best practice is tooset this property toohello name of hello workflow by using hello following expression:</span></span>

    @workflow().name

<span data-ttu-id="af26d-207">使用 hello **x ms-排程器建議**和**x ms 可見度**其應用程式開發介面的定義，hello API 應用程式中的擴充功能屬性可以傳遞 toohello 邏輯應用程式的設計工具 tooautomatically 設定hello 使用者的運算式。</span><span class="sxs-lookup"><span data-stu-id="af26d-207">Using hello **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, hello API app can convey toohello Logic app designer tooautomatically set this expression for hello user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="af26d-208">在 API 定義中加入延伸模組屬性</span><span class="sxs-lookup"><span data-stu-id="af26d-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="af26d-209">其他中繼資料資訊-例如 hello 延伸模組屬性**x ms-排程器建議**和**x ms 可見度**-可以加入 hello 應用程式開發介面定義中有兩種： 靜態或動態。</span><span class="sxs-lookup"><span data-stu-id="af26d-209">Additional metadata information - such as hello extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in hello API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="af26d-210">對於靜態中繼資料，您可以直接編輯 hello */metadata/apiDefinition.swagger.json*檔案在您的專案，然後手動加入 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="af26d-210">For static metadata, you can directly edit hello */metadata/apiDefinition.swagger.json* file in your project and add hello properties manually.</span></span>

<span data-ttu-id="af26d-211">應用程式開發介面使用的應用程式動態中繼資料，您可以編輯 hello SwaggerConfig.cs 檔案 tooadd 可以加入這些擴充功能作業篩選器。</span><span class="sxs-lookup"><span data-stu-id="af26d-211">For API apps using dynamic metadata, you can edit hello SwaggerConfig.cs file tooadd an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="af26d-212">hello 以下是如何這個類別可以實作的 toofacilitate hello 動態中繼資料案例的範例。</span><span class="sxs-lookup"><span data-stu-id="af26d-212">hello following is an example of how this class can be implemented toofacilitate hello dynamic metadata scenario.</span></span>

    // Add extension properties on hello triggerState parameter
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
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
