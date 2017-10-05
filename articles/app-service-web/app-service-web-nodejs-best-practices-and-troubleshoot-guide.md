---
title: "Azure Web Apps 上節點應用程式的最佳作法和疑難排解指南"
description: "了解 Azure Web Apps 上節點應用程式的最佳作法和疑難排解步驟。"
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: d820ef3438e13332657641b06b57fa277e79f811
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a><span data-ttu-id="c9d70-103">Azure Web Apps 上節點應用程式的最佳作法和疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="c9d70-103">Best practices and troubleshooting guide for node applications on Azure Web Apps</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="c9d70-104">在本文中，您將了解在 Azure Web Apps 上執行之[節點應用程式](app-service-web-get-started-nodejs.md)的最佳作法和疑難排解步驟 (透過 [iisnode](https://github.com/azure/iisnode))。</span><span class="sxs-lookup"><span data-stu-id="c9d70-104">In this article, you will learn the best practices and troubleshooting steps for [node applications](app-service-web-get-started-nodejs.md) running on Azure Webapps (with [iisnode](https://github.com/azure/iisnode)).</span></span>

> [!WARNING]
> <span data-ttu-id="c9d70-105">請小心在您的生產網站上使用疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="c9d70-105">Use caution when using troubleshooting steps on your production site.</span></span> <span data-ttu-id="c9d70-106">建議在非生產安裝 (例如您的預備位置) 上對應用程式進行疑難排解，而當問題修正後，請切換您的預備位置與生產位置。</span><span class="sxs-lookup"><span data-stu-id="c9d70-106">Recommendation is to troubleshoot your app on a non-production setup for example your staging slot and when the issue is fixed, swap your staging slot with your production slot.</span></span>
> 
> 

## <a name="iisnode-configuration"></a><span data-ttu-id="c9d70-107">IISNODE 組態</span><span class="sxs-lookup"><span data-stu-id="c9d70-107">IISNODE configuration</span></span>
<span data-ttu-id="c9d70-108">此 [結構描述檔案](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) 會顯示可針對 iisnode 設定的所有設定。</span><span class="sxs-lookup"><span data-stu-id="c9d70-108">This [schema file](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) shows all the settings that can be configured for iisnode.</span></span> <span data-ttu-id="c9d70-109">適合用於您的應用程式的一些設定如下︰</span><span class="sxs-lookup"><span data-stu-id="c9d70-109">Some of the settings that will be useful for your application are:</span></span>

* <span data-ttu-id="c9d70-110">nodeProcessCountPerApplication</span><span class="sxs-lookup"><span data-stu-id="c9d70-110">nodeProcessCountPerApplication</span></span>
  
    <span data-ttu-id="c9d70-111">此設定會控制每個 IIS 應用程式啟動的節點處理序數目。</span><span class="sxs-lookup"><span data-stu-id="c9d70-111">This setting controls the number of node processes that are launched per IIS application.</span></span> <span data-ttu-id="c9d70-112">預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="c9d70-112">Default value is 1.</span></span> <span data-ttu-id="c9d70-113">您可以將此值設為 0，啟動與您的 VM 核心計數一樣多的 node.exe 。</span><span class="sxs-lookup"><span data-stu-id="c9d70-113">You can launch as many node.exe’s as your VM core count by setting this to 0.</span></span> <span data-ttu-id="c9d70-114">大部分應用程式的建議值為 0，以便您利用電腦上的所有核心。</span><span class="sxs-lookup"><span data-stu-id="c9d70-114">Recommended value is 0 for most application so you can utilize all of the cores on your machine.</span></span> <span data-ttu-id="c9d70-115">Node.exe 為單一執行緒，因此一個 node.exe 最多會耗用 1 個核心，若要讓節點應用程式發揮最大效能，您會可以利用所有的核心。</span><span class="sxs-lookup"><span data-stu-id="c9d70-115">Node.exe is single threaded so one node.exe will consume a maximum of 1 core and to get maximum performance out of your node application you would want to utilize all cores.</span></span>
* <span data-ttu-id="c9d70-116">nodeProcessCommandLine</span><span class="sxs-lookup"><span data-stu-id="c9d70-116">nodeProcessCommandLine</span></span>
  
    <span data-ttu-id="c9d70-117">此設定會控制 node.exe 的路徑。</span><span class="sxs-lookup"><span data-stu-id="c9d70-117">This setting controls the path to the node.exe.</span></span> <span data-ttu-id="c9d70-118">您可以設定此值以指向您的 node.exe 版本。</span><span class="sxs-lookup"><span data-stu-id="c9d70-118">You can set this value to point to your node.exe version.</span></span>
* <span data-ttu-id="c9d70-119">maxConcurrentRequestsPerProcess</span><span class="sxs-lookup"><span data-stu-id="c9d70-119">maxConcurrentRequestsPerProcess</span></span>
  
    <span data-ttu-id="c9d70-120">此設定會控制 iisnode 傳送給每個 node.exe 的並行要求數目上限。</span><span class="sxs-lookup"><span data-stu-id="c9d70-120">This setting controls the maximum number of concurrent requests sent by iisnode to each node.exe.</span></span> <span data-ttu-id="c9d70-121">在 Azure Web Apps 上，此設定的預設值為 [無限]。</span><span class="sxs-lookup"><span data-stu-id="c9d70-121">On azure webapps, the default value for this is Infinite.</span></span> <span data-ttu-id="c9d70-122">您不必擔心這項設定。</span><span class="sxs-lookup"><span data-stu-id="c9d70-122">You will not have to worry about this setting.</span></span> <span data-ttu-id="c9d70-123">在 Azure Web Apps 外部，預設值為 1024。</span><span class="sxs-lookup"><span data-stu-id="c9d70-123">Outside azure webapps, the default value is 1024.</span></span> <span data-ttu-id="c9d70-124">您可以視您的應用程式取得的要求數目以及您的應用程式處理每個要求的速度而定，進行此設定。</span><span class="sxs-lookup"><span data-stu-id="c9d70-124">You might want to configure this depending on how many requests your application gets and how fast your application processes each request.</span></span>
* <span data-ttu-id="c9d70-125">maxNamedPipeConnectionRetry</span><span class="sxs-lookup"><span data-stu-id="c9d70-125">maxNamedPipeConnectionRetry</span></span>
  
    <span data-ttu-id="c9d70-126">此設定會控制 iisnode 將在具名管道上重試連線，以將要求傳送至 node.exe 的次數上限。</span><span class="sxs-lookup"><span data-stu-id="c9d70-126">This setting controls the maximum number of times iisnode will retry making connection on the named pipe to send the request over to node.exe.</span></span> <span data-ttu-id="c9d70-127">此設定結合 namedPipeConnectionRetryDelay 一起使用，可決定 iisnode 內每個要求的總逾時。</span><span class="sxs-lookup"><span data-stu-id="c9d70-127">This setting in combination with namedPipeConnectionRetryDelay determines the total timeout of each request within iisnode.</span></span> <span data-ttu-id="c9d70-128">在 Azure Web Apps 上預設值為 200。</span><span class="sxs-lookup"><span data-stu-id="c9d70-128">Default value is 200 on Azure Webapps.</span></span> <span data-ttu-id="c9d70-129">總逾時 (秒) = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000</span><span class="sxs-lookup"><span data-stu-id="c9d70-129">Total Timeout in seconds = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000</span></span>
* <span data-ttu-id="c9d70-130">namedPipeConnectionRetryDelay</span><span class="sxs-lookup"><span data-stu-id="c9d70-130">namedPipeConnectionRetryDelay</span></span>
  
    <span data-ttu-id="c9d70-131">此設定控制 iisnode 在每次重試透過具名管道將要求傳送到 node.exe 之間所要等待的時間量 (毫秒)。</span><span class="sxs-lookup"><span data-stu-id="c9d70-131">This setting controls the amount of time (in ms) iisnode will wait for between each retry to send request to node.exe over the named pipe.</span></span> <span data-ttu-id="c9d70-132">預設值為 250 毫秒。</span><span class="sxs-lookup"><span data-stu-id="c9d70-132">Default value is 250ms.</span></span>
    <span data-ttu-id="c9d70-133">總逾時 (秒) = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000</span><span class="sxs-lookup"><span data-stu-id="c9d70-133">Total Timeout in seconds = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000</span></span>
  
    <span data-ttu-id="c9d70-134">在 Azure Web Apps 上，iisnode 的總逾時預設為 200 \* 250 毫秒 = 50 秒。</span><span class="sxs-lookup"><span data-stu-id="c9d70-134">By default the total timeout in iisnode on azure webapps is 200 \* 250ms = 50 seconds.</span></span>
* <span data-ttu-id="c9d70-135">logDirectory</span><span class="sxs-lookup"><span data-stu-id="c9d70-135">logDirectory</span></span>
  
    <span data-ttu-id="c9d70-136">此設定會控制 iisnode 記錄 stdout/stderr 的目錄。</span><span class="sxs-lookup"><span data-stu-id="c9d70-136">This setting controls the directory where iisnode will log stdout/stderr.</span></span> <span data-ttu-id="c9d70-137">預設值是相對於主要指令碼目錄 (主要 server.js 所在的目錄) 的 iisnode</span><span class="sxs-lookup"><span data-stu-id="c9d70-137">Default value is iisnode which is relative to the main script directory (directory where main server.js is present)</span></span>
* <span data-ttu-id="c9d70-138">debuggerExtensionDll</span><span class="sxs-lookup"><span data-stu-id="c9d70-138">debuggerExtensionDll</span></span>
  
    <span data-ttu-id="c9d70-139">此設定會控制 iisnode 在進行節點應用程式偵錯時，將使用的節點偵測器版本。</span><span class="sxs-lookup"><span data-stu-id="c9d70-139">This setting controls what version of node-inspector iisnode will use when debugging your node application.</span></span> <span data-ttu-id="c9d70-140">iisnode-inspector-0.7.3.dll 和 iisnode-inspector.dll 目前是此設定僅有的 2 個有效值。</span><span class="sxs-lookup"><span data-stu-id="c9d70-140">Currently iisnode-inspector-0.7.3.dll and iisnode-inspector.dll are the only 2 valid values for this setting.</span></span> <span data-ttu-id="c9d70-141">預設值為 iisnode-inspector-0.7.3.dll。</span><span class="sxs-lookup"><span data-stu-id="c9d70-141">Default value is iisnode-inspector-0.7.3.dll.</span></span> <span data-ttu-id="c9d70-142">iisnode-inspector-0.7.3.dll 版本會使用 node-inspector-0.7.3 並使用 Websocket，所以您必須啟用您的 Azure Web App 上的 Websocket，才能使用這個版本。</span><span class="sxs-lookup"><span data-stu-id="c9d70-142">iisnode-inspector-0.7.3.dll version uses node-inspector-0.7.3 and uses websockets, so you will need to enable websockets on your azure webapp to use this version.</span></span> <span data-ttu-id="c9d70-143">如需有關如何設定 iisnode 以使用新的節點偵測器的詳細資訊，請參閱 <http://www.ranjithr.com/?p=98>。</span><span class="sxs-lookup"><span data-stu-id="c9d70-143">See <http://www.ranjithr.com/?p=98> for more details on how to configure iisnode to use the new node-inspector.</span></span>
* <span data-ttu-id="c9d70-144">flushResponse</span><span class="sxs-lookup"><span data-stu-id="c9d70-144">flushResponse</span></span>
  
    <span data-ttu-id="c9d70-145">IIS 的預設行為是在排清之前或直到回應結束時 (取決於何者較早出現)，將回應資料緩衝至 4MB。</span><span class="sxs-lookup"><span data-stu-id="c9d70-145">The default behavior of IIS is that it buffers response data up to 4MB before flushing, or until the end of the response, whichever comes first.</span></span> <span data-ttu-id="c9d70-146">iisnode 提供組態設定來覆寫這個行為︰若要在 iisnode 從 node.exe 收到回應實體內文的片段時就立刻排清，您需要將 web.config 中的 iisnode/@flushResponse 屬性設定為 'true'︰</span><span class="sxs-lookup"><span data-stu-id="c9d70-146">iisnode offers a configuration setting to override this behavior: to flush a fragment of the response entity body as soon as iisnode receives it from node.exe, you need to set the iisnode/@flushResponse attribute in web.config to 'true':</span></span>
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    <span data-ttu-id="c9d70-147">啟用排清每個回應主體內文片段會增加效能負荷，而降低 ~5% 的系統輸送量 (從 v0.1.13 起)，所以最好讓此設定的範圍僅限於需要回應串流的端點 (例如在 web.config 中使用 <location> 元素)</span><span class="sxs-lookup"><span data-stu-id="c9d70-147">Enabling flushing of every fragment of the response entity body adds performance overhead that reduces the throughput of the system by ~5% (as of v0.1.13), so it is best to scope this setting only to endpoints that require response streaming (e.g. using the <location> element in the web.config)</span></span>
  
    <span data-ttu-id="c9d70-148">除此之外，對於串流應用程式，您也必須將 iisnode 處理常式的 responseBufferLimit 設定為 0。</span><span class="sxs-lookup"><span data-stu-id="c9d70-148">In addition to this, for streaming applications, you will need to also set responseBufferLimit of your iisnode handler to 0.</span></span>
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* <span data-ttu-id="c9d70-149">watchedFiles</span><span class="sxs-lookup"><span data-stu-id="c9d70-149">watchedFiles</span></span>
  
    <span data-ttu-id="c9d70-150">這是以分號分隔的檔案清單，系統將監看其變更。</span><span class="sxs-lookup"><span data-stu-id="c9d70-150">This is a semi-colon separated list of files that will be watched for changes.</span></span> <span data-ttu-id="c9d70-151">檔案變更會導致應用程式回收。</span><span class="sxs-lookup"><span data-stu-id="c9d70-151">A change to a file causes the application to recycle.</span></span> <span data-ttu-id="c9d70-152">每個項目都包含選擇性目錄名稱，再加上相對於主要應用程式進入點所在目錄的必要檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="c9d70-152">Each entry consists of an optional directory name plus required file name which are relative to the directory where the main application entry point is located.</span></span> <span data-ttu-id="c9d70-153">只有檔案名稱部分可以使用萬用字元。</span><span class="sxs-lookup"><span data-stu-id="c9d70-153">Wild cards are allowed in the file name portion only.</span></span> <span data-ttu-id="c9d70-154">預設值為 “\*.js;web.config”</span><span class="sxs-lookup"><span data-stu-id="c9d70-154">Default value is “\*.js;web.config”</span></span>
* <span data-ttu-id="c9d70-155">recycleSignalEnabled</span><span class="sxs-lookup"><span data-stu-id="c9d70-155">recycleSignalEnabled</span></span>
  
    <span data-ttu-id="c9d70-156">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="c9d70-156">Default value is false.</span></span> <span data-ttu-id="c9d70-157">若已啟用，節點應用程式可以連接至具名管道 (環境變數 IISNODE\_CONTROL\_PIPE) 並傳送「回收」訊息。</span><span class="sxs-lookup"><span data-stu-id="c9d70-157">If enabled, your node application can connect to a named pipe (environment variable IISNODE\_CONTROL\_PIPE) and send a “recycle” message.</span></span> <span data-ttu-id="c9d70-158">這會導致正常回收 w3wp。</span><span class="sxs-lookup"><span data-stu-id="c9d70-158">This will cause the w3wp to recycle gracefully.</span></span>
* <span data-ttu-id="c9d70-159">idlePageOutTimePeriod</span><span class="sxs-lookup"><span data-stu-id="c9d70-159">idlePageOutTimePeriod</span></span>
  
    <span data-ttu-id="c9d70-160">預設值為 0，這表示已停用此功能。</span><span class="sxs-lookup"><span data-stu-id="c9d70-160">Default value is 0 which means this feature is disabled.</span></span> <span data-ttu-id="c9d70-161">若設定為大於 0 的值，iisnode 會每隔 'idlePageOutTimePeriod' 毫秒將其所有的子處理序移出分頁。</span><span class="sxs-lookup"><span data-stu-id="c9d70-161">When set to some value greater than 0, iisnode will page out all its child processes every ‘idlePageOutTimePeriod’ milliseconds.</span></span> <span data-ttu-id="c9d70-162">若要了解移出分頁的意思，請參閱此 [文件](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c9d70-162">To understand what page out means, please refer to this [documentation](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx).</span></span> <span data-ttu-id="c9d70-163">對於耗用大量記憶體和偶爾想要將記憶體移出至磁碟以釋放一些 RAM 的應用程式，此設定很有用。</span><span class="sxs-lookup"><span data-stu-id="c9d70-163">This setting will be useful for applications that consume a lot of memory and want to pageout memory to disk occasionally to free up some RAM.</span></span>

> [!WARNING]
> <span data-ttu-id="c9d70-164">在生產應用程式上啟用下列組態設定時，請格外小心。</span><span class="sxs-lookup"><span data-stu-id="c9d70-164">Use caution when enabling the following configuration settings on production applications.</span></span> <span data-ttu-id="c9d70-165">建議不要在實際生產應用程式上啟用它們。</span><span class="sxs-lookup"><span data-stu-id="c9d70-165">Recommendation is to not enable them on live production applications.</span></span>
> 
> 

* <span data-ttu-id="c9d70-166">debugHeaderEnabled</span><span class="sxs-lookup"><span data-stu-id="c9d70-166">debugHeaderEnabled</span></span>
  
    <span data-ttu-id="c9d70-167">預設值為 False。</span><span class="sxs-lookup"><span data-stu-id="c9d70-167">The default value is false.</span></span> <span data-ttu-id="c9d70-168">如果設為 true，iisnode 會將 HTTP 回應標頭 iisnode-debug 加入至它所傳送的每個 HTTP 回應，而 iisnode-debug 標頭值是 URL。</span><span class="sxs-lookup"><span data-stu-id="c9d70-168">If set to true, iisnode will add an HTTP response header iisnode-debug to every HTTP response it sends the iisnode-debug header value is a URL.</span></span> <span data-ttu-id="c9d70-169">查看 URL 片段即可搜集個別的診斷資訊，但在瀏覽器中開啟 URL 可達成更好的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c9d70-169">Individual pieces of diagnostic information can be gleaned by looking at the URL fragment, but a much better visualization is achieved by opening the URL in the browser.</span></span>
* <span data-ttu-id="c9d70-170">loggingEnabled</span><span class="sxs-lookup"><span data-stu-id="c9d70-170">loggingEnabled</span></span>
  
    <span data-ttu-id="c9d70-171">此設定會控制 iisnode 記錄 stdout 和 stderr 的功能。</span><span class="sxs-lookup"><span data-stu-id="c9d70-171">This setting controls the logging of stdout and stderr by iisnode.</span></span> <span data-ttu-id="c9d70-172">Iisnode 將從它所啟動的節點處理序擷取 stdout/stderr，並寫入至 'logDirectory' 設定中指定的目錄。</span><span class="sxs-lookup"><span data-stu-id="c9d70-172">Iisnode will capture stdout/stderr from node processes it launches and write to the directory specified in the ‘logDirectory’ setting.</span></span> <span data-ttu-id="c9d70-173">一旦啟用，您的應用程式會將記錄檔寫入至檔案系統，而視應用程式所完成的記錄量而定，可能會影響效能。</span><span class="sxs-lookup"><span data-stu-id="c9d70-173">Once this is enable, your application will be writing logs to the file system and depending on the amount of logging done by the application, there could be performance implications.</span></span>
* <span data-ttu-id="c9d70-174">devErrorsEnabled</span><span class="sxs-lookup"><span data-stu-id="c9d70-174">devErrorsEnabled</span></span>
  
    <span data-ttu-id="c9d70-175">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="c9d70-175">Default value is false.</span></span> <span data-ttu-id="c9d70-176">若設為 true，iisnode 會在瀏覽器上顯示 HTTP 狀態碼和 Win32 錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="c9d70-176">When set to true, iisnode will display the HTTP status code and Win32 error code on your browser.</span></span> <span data-ttu-id="c9d70-177">在偵錯特定類型的問題時，Win32 程式碼很有幫助。</span><span class="sxs-lookup"><span data-stu-id="c9d70-177">The win32 code will be helpful in debugging certain types of issues.</span></span>
* <span data-ttu-id="c9d70-178">debuggingEnabled (請勿在實際生產網站上啟用)</span><span class="sxs-lookup"><span data-stu-id="c9d70-178">debuggingEnabled (do not enable on live production site)</span></span>
  
    <span data-ttu-id="c9d70-179">此設定會控制偵錯功能。</span><span class="sxs-lookup"><span data-stu-id="c9d70-179">This setting controls debugging feature.</span></span> <span data-ttu-id="c9d70-180">Iisnode 會與節點偵測器整合。</span><span class="sxs-lookup"><span data-stu-id="c9d70-180">Iisnode is integrated with node-inspector.</span></span> <span data-ttu-id="c9d70-181">藉由啟用此設定，即可啟用節點應用程式的偵錯功能。</span><span class="sxs-lookup"><span data-stu-id="c9d70-181">By enabling this setting, you enable debugging of your node application.</span></span> <span data-ttu-id="c9d70-182">啟用此設定後，iisnode 會在對節點應用程式進行第一個偵錯要求時，在 'debuggerVirtualDir' 目錄中配置所需的節點偵測器檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d70-182">Once this setting is enabled, iisnode will layout the necessary node-inspector files in ‘debuggerVirtualDir’ directory on the first debug request to your node application.</span></span> <span data-ttu-id="c9d70-183">您可以將要求傳送至 http://yoursite/server.js/debug，以載入節點偵測器。</span><span class="sxs-lookup"><span data-stu-id="c9d70-183">You can load the node-inspector by sending a request to http://yoursite/server.js/debug.</span></span> <span data-ttu-id="c9d70-184">您可以使用 'debuggerPathSegment' 設定來控制偵錯 URL 區段。</span><span class="sxs-lookup"><span data-stu-id="c9d70-184">You can control the debug URL segment with ‘debuggerPathSegment’ setting.</span></span> <span data-ttu-id="c9d70-185">根據預設，debuggerPathSegment=’debug’。</span><span class="sxs-lookup"><span data-stu-id="c9d70-185">By default debuggerPathSegment=’debug’.</span></span> <span data-ttu-id="c9d70-186">您可以將此值設定為 GUID，所以其他人更難以發現。</span><span class="sxs-lookup"><span data-stu-id="c9d70-186">You can set this to a GUID for example so that it is more difficult to be discovered by others.</span></span>
  
    <span data-ttu-id="c9d70-187">如需偵錯詳細資訊，請查看此 [連結](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) 。</span><span class="sxs-lookup"><span data-stu-id="c9d70-187">Check this [link](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) for more details on debugging.</span></span>

## <a name="scenarios-and-recommendationstroubleshooting"></a><span data-ttu-id="c9d70-188">案例和建議/疑難排解</span><span class="sxs-lookup"><span data-stu-id="c9d70-188">Scenarios and recommendations/troubleshooting</span></span>
### <a name="my-node-application-is-making-too-many-outbound-calls"></a><span data-ttu-id="c9d70-189">我的節點應用程式進行太多的輸出呼叫。</span><span class="sxs-lookup"><span data-stu-id="c9d70-189">My node application is making too many outbound calls.</span></span>
<span data-ttu-id="c9d70-190">許多應用程式想要在其定期作業中進行輸出連線。</span><span class="sxs-lookup"><span data-stu-id="c9d70-190">Many applications would want to make outbound connections as part of their regular operation.</span></span> <span data-ttu-id="c9d70-191">例如，當要求傳入時，節點應用程式會想連絡別處的 REST API，並取得一些資訊來處理要求。</span><span class="sxs-lookup"><span data-stu-id="c9d70-191">For example, when a request comes in, your node app would want to contact a REST API elsewhere and get some information to process the request.</span></span> <span data-ttu-id="c9d70-192">您想要在進行 http 或 https 呼叫時使用保持連線代理程式。</span><span class="sxs-lookup"><span data-stu-id="c9d70-192">You would want to use a keep alive agent when making http or https calls.</span></span> <span data-ttu-id="c9d70-193">例如，您可以在進行這些輸出呼叫時，使用 agentkeepalive 模組做為您的保持連線代理程式。</span><span class="sxs-lookup"><span data-stu-id="c9d70-193">For example, you could use the agentkeepalive module as your keep alive agent when making these outbound calls.</span></span> <span data-ttu-id="c9d70-194">這可確保在您的 Azure Web App VM 上重複使用通訊端，並減少為每個輸出要求建立新通訊端的額外負荷。</span><span class="sxs-lookup"><span data-stu-id="c9d70-194">This makes sure that the sockets are reused on your azure webapp VM and reducing the overhead of creating new sockets for every outbound request.</span></span> <span data-ttu-id="c9d70-195">此外，這可確保您使用較少的通訊端來進行許多輸出要求，因此您不會超過每個 VM 配置的 maxSockets。</span><span class="sxs-lookup"><span data-stu-id="c9d70-195">Also, this makes sure that you are using less number of sockets to make many outbound requests and therefore you don’t exceed the maxSockets that are allocated per VM.</span></span> <span data-ttu-id="c9d70-196">對於 Azure Web Apps 的建議是將 agentKeepAlive maxSockets 值設為每個 VM 總計有 160 個通訊端。</span><span class="sxs-lookup"><span data-stu-id="c9d70-196">Recommendation on Azure Webapps would be to set the agentKeepAlive maxSockets value to a total of 160 sockets per VM.</span></span> <span data-ttu-id="c9d70-197">這表示如果您有 4 個 node.exe 在 VM 上執行，您可以將每個 node.exe 的 agentKeepAlive maxSockets 設定為 40，也就是每個 VM 總計有 160 個。</span><span class="sxs-lookup"><span data-stu-id="c9d70-197">This means that if you have 4 node.exe running on the VM, you would want to set the agentKeepAlive maxSockets to 40 per node.exe which is 160 total per VM.</span></span>

<span data-ttu-id="c9d70-198">範例 [agentKeepALive](https://www.npmjs.com/package/agentkeepalive) 設定：</span><span class="sxs-lookup"><span data-stu-id="c9d70-198">Example [agentKeepALive](https://www.npmjs.com/package/agentkeepalive) configuration:</span></span>

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

<span data-ttu-id="c9d70-199">這個範例假設您有 4 個 node.exe 在 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="c9d70-199">This example assumes you have 4 node.exe running on your VM.</span></span> <span data-ttu-id="c9d70-200">如果您有不同數目的 node.exe 在 VM 上執行，您必須據此修改 maxSockets 設定。</span><span class="sxs-lookup"><span data-stu-id="c9d70-200">If you have a different number of node.exe running on the VM, you will have to modify the maxSockets setting accordingly.</span></span>

### <a name="my-node-application-is-consuming-too-much-cpu"></a><span data-ttu-id="c9d70-201">我的節點應用程式目前耗用太多 CPU。</span><span class="sxs-lookup"><span data-stu-id="c9d70-201">My node application is consuming too much CPU.</span></span>
<span data-ttu-id="c9d70-202">您可能會在您的入口網站上取得 Azure Web Apps 建議的高 cpu 耗用量。</span><span class="sxs-lookup"><span data-stu-id="c9d70-202">You will probably get a recommendation from Azure Webapps on your portal about high cpu consumption.</span></span> <span data-ttu-id="c9d70-203">您也可以設定監視器以監看某些 [度量](web-sites-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="c9d70-203">You can also setup monitors to watch for certain [metrics](web-sites-monitor.md).</span></span> <span data-ttu-id="c9d70-204">在 [Azure 入口網站儀表板](../application-insights/app-insights-web-monitor-performance.md)上檢查 CPU 使用量時，請檢查 CPU 的 MAX 值，您才不會錯過尖峰值。</span><span class="sxs-lookup"><span data-stu-id="c9d70-204">When checking the CPU usage on the [Azure Portal Dashboard](../application-insights/app-insights-web-monitor-performance.md), please check the MAX values for CPU so you don’t miss out the peak values.</span></span>
<span data-ttu-id="c9d70-205">在您認為應用程式耗用太多 CPU，但您無法解釋的情況下，您必須剖析節點應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9d70-205">In cases where you think your application is consuming too much CPU and you cannot explain why, you will need to profile your node application.</span></span>

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a><span data-ttu-id="c9d70-206">在 Azure Web Apps 上使用 V8 分析工具剖析節點應用程式</span><span class="sxs-lookup"><span data-stu-id="c9d70-206">Profiling your node application on azure webapps with V8-Profiler</span></span>
<span data-ttu-id="c9d70-207">例如，假設您擁有想要剖析的 hello world 應用程式，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="c9d70-207">For example, lets say you have a hello world app that you want to profile as shown below:</span></span>

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

<span data-ttu-id="c9d70-208">請移至您的 scm 網站 https://yoursite.scm.azurewebsites.net/DebugConsole</span><span class="sxs-lookup"><span data-stu-id="c9d70-208">Go to your scm site https://yoursite.scm.azurewebsites.net/DebugConsole</span></span>

<span data-ttu-id="c9d70-209">您會看到命令提示字元，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c9d70-209">You will see a command prompt as shown below.</span></span> <span data-ttu-id="c9d70-210">進入 site/wwwroot 目錄</span><span class="sxs-lookup"><span data-stu-id="c9d70-210">Go into your site/wwwroot directory</span></span>

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

<span data-ttu-id="c9d70-211">執行 “npm install v8-profiler” 命令</span><span class="sxs-lookup"><span data-stu-id="c9d70-211">Run the command “npm install v8-profiler”</span></span>

<span data-ttu-id="c9d70-212">這應會在 node\_modules 目錄與其所有的相依項目之下安裝 v8 分析工具。</span><span class="sxs-lookup"><span data-stu-id="c9d70-212">This should install v8-profiler under node\_modules directory and all of its dependencies.</span></span>
<span data-ttu-id="c9d70-213">現在，編輯 server.js 以剖析您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9d70-213">Now, edit your server.js to profile your application.</span></span>

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

<span data-ttu-id="c9d70-214">上述變更將剖析 WriteConsoleLog 函式，然後將設定檔輸出寫入至您的網站 wwwroot 下的 'profile.cpuprofile' 檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d70-214">The above changes will profile the WriteConsoleLog function and then write the profile output to ‘profile.cpuprofile’ file under your site wwwroot.</span></span> <span data-ttu-id="c9d70-215">將要求傳送至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9d70-215">Send a request to your application.</span></span> <span data-ttu-id="c9d70-216">您會在您的網站 wwwroot 下看到所建立的 'profile.cpuprofile' 檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d70-216">You will see a ‘profile.cpuprofile’ file created under your site wwwroot.</span></span>

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

<span data-ttu-id="c9d70-217">下載此檔案，您必須使用 Chrome F12 工具來開啟此檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d70-217">Download this file and you will need to open this file with Chrome F12 Tools.</span></span> <span data-ttu-id="c9d70-218">在 Chrome 上按 F12，然後按一下 [設定檔索引標籤]。</span><span class="sxs-lookup"><span data-stu-id="c9d70-218">Hit F12 on chrome, then click on the “Profiles Tab”.</span></span> <span data-ttu-id="c9d70-219">按一下 [載入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9d70-219">Click on “Load” Button.</span></span> <span data-ttu-id="c9d70-220">選取您剛下載的 profile.cpuprofile 檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d70-220">Select your profile.cpuprofile file that you just downloaded.</span></span> <span data-ttu-id="c9d70-221">按一下您剛下載的設定檔</span><span class="sxs-lookup"><span data-stu-id="c9d70-221">Click on the profile you just loaded.</span></span>

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

<span data-ttu-id="c9d70-222">您會看到 WriteConsoleLog 函式已耗用 95%的時間，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c9d70-222">You will see that 95% of the time was consumed by WriteConsoleLog function as shown below.</span></span> <span data-ttu-id="c9d70-223">這也會顯示造成此問題的確切行號和原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="c9d70-223">This also shows you the exact line numbers and source files that cause the issue.</span></span>

### <a name="my-node-application-is-consuming-too-much-memory"></a><span data-ttu-id="c9d70-224">我的節點應用程式目前耗用太多記憶體。</span><span class="sxs-lookup"><span data-stu-id="c9d70-224">My node application is consuming too much memory.</span></span>
<span data-ttu-id="c9d70-225">您可能會在您的入口網站上取得 Azure Web Apps 建議的高記憶體耗用量。</span><span class="sxs-lookup"><span data-stu-id="c9d70-225">You will probably get a recommendation from Azure Webapps on your portal about high memory consumption.</span></span> <span data-ttu-id="c9d70-226">您也可以設定監視器以監看某些 [度量](web-sites-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="c9d70-226">You can also setup monitors to watch for certain [metrics](web-sites-monitor.md).</span></span> <span data-ttu-id="c9d70-227">在 [Azure 入口網站儀表板](../application-insights/app-insights-web-monitor-performance.md)上檢查記憶體使用量時，請檢查記憶體的 MAX 值，您才不會錯過尖峰值。</span><span class="sxs-lookup"><span data-stu-id="c9d70-227">When checking the memory usage on the [Azure Portal Dashboard](../application-insights/app-insights-web-monitor-performance.md), please check the MAX values for memory so you don’t miss out the peak values.</span></span>

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a><span data-ttu-id="c9d70-228">node.js 的流失偵測和堆積區分</span><span class="sxs-lookup"><span data-stu-id="c9d70-228">Leak detection and Heap Diffing for node.js</span></span>
<span data-ttu-id="c9d70-229">您可以使用 [node-memwatch](https://github.com/lloyd/node-memwatch) 協助找出記憶體流失。</span><span class="sxs-lookup"><span data-stu-id="c9d70-229">You could use [node-memwatch](https://github.com/lloyd/node-memwatch) to help you identify memory leaks.</span></span>
<span data-ttu-id="c9d70-230">如同 v8 分析工具，您可以安裝 memwatch 並編輯您的程式碼來擷取和區分堆積，以找出您應用程式中的記憶體流失。</span><span class="sxs-lookup"><span data-stu-id="c9d70-230">You can install memwatch just like v8-profiler and edit your code to capture and diff heaps to identify the memory leaks in your application.</span></span>

### <a name="my-nodeexes-are-getting-killed-randomly"></a><span data-ttu-id="c9d70-231">我的 node.exe 會隨機終止</span><span class="sxs-lookup"><span data-stu-id="c9d70-231">My node.exe’s are getting killed randomly</span></span>
<span data-ttu-id="c9d70-232">發生這種情況有幾個原因︰</span><span class="sxs-lookup"><span data-stu-id="c9d70-232">There are a few reasons why this could be happening:</span></span>

1. <span data-ttu-id="c9d70-233">您的應用程式擲回未攔截的例外狀況 - 請檢查 d:\\home\\LogFiles\\Application\\logging-errors.txt file 檔案，以取得所擲回例外狀況的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c9d70-233">Your application is throwing uncaught exceptions – Please check d:\\home\\LogFiles\\Application\\logging-errors.txt file for the details on the exception thrown.</span></span> <span data-ttu-id="c9d70-234">這個檔案有堆疊追蹤，所以您可以據此修正您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9d70-234">This file has the stack trace so you can fix your application based on this.</span></span>
2. <span data-ttu-id="c9d70-235">您的應用程式耗用太多記憶體，近而讓其他處理序無法開始執行。</span><span class="sxs-lookup"><span data-stu-id="c9d70-235">Your application is consuming too much memory which is affecting other processes from getting started.</span></span> <span data-ttu-id="c9d70-236">如果 VM 記憶體總數接近 100%，則處理序管理員會終止 node.exe，讓其他處理序有機會執行一些工作。</span><span class="sxs-lookup"><span data-stu-id="c9d70-236">If the total VM memory is close to 100%, your node.exe’s could be killed by the process manager to let other processes get a chance to do some work.</span></span> <span data-ttu-id="c9d70-237">若要修正此問題，請確定您的應用程式並未流失記憶體，或者如果您的應用程式真的需要使用大量記憶體，請相應增加為更多 RAM 的較大 VM。</span><span class="sxs-lookup"><span data-stu-id="c9d70-237">To fix this, either make sure your application is not leaking memory OR if you application really needs to use a lot of memory, please scale up to a larger VM with a lot more RAM.</span></span>

### <a name="my-node-application-does-not-start"></a><span data-ttu-id="c9d70-238">我的節點應用程式並未啟動</span><span class="sxs-lookup"><span data-stu-id="c9d70-238">My node application does not start</span></span>
<span data-ttu-id="c9d70-239">如果您的應用程式在啟動時傳回 500 錯誤，可能有幾個原因︰</span><span class="sxs-lookup"><span data-stu-id="c9d70-239">If your application is returning 500 Errors at startup, there could be a few reasons:</span></span>

1. <span data-ttu-id="c9d70-240">Node.exe 未出現在正確的位置。</span><span class="sxs-lookup"><span data-stu-id="c9d70-240">Node.exe is not present at the correct location.</span></span> <span data-ttu-id="c9d70-241">檢查 nodeProcessCommandLine 設定。</span><span class="sxs-lookup"><span data-stu-id="c9d70-241">Check nodeProcessCommandLine setting.</span></span>
2. <span data-ttu-id="c9d70-242">主要指令碼檔案未出現在正確的位置。</span><span class="sxs-lookup"><span data-stu-id="c9d70-242">Main script file is not present at the correct location.</span></span> <span data-ttu-id="c9d70-243">檢查 web.config，並確定處理常式區段中的主要指令碼檔案名稱符合主要指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d70-243">Check web.config and make sure the name of the main script file in the handlers section matches the main script file.</span></span>
3. <span data-ttu-id="c9d70-244">Web.config 組態不正確 – 檢查設定名稱/值。</span><span class="sxs-lookup"><span data-stu-id="c9d70-244">Web.config configuration is not correct – check the settings names/values.</span></span>
4. <span data-ttu-id="c9d70-245">冷啟動 – 您的應用程式花太長時間啟動。</span><span class="sxs-lookup"><span data-stu-id="c9d70-245">Cold Start – Your application is taking too long to startup.</span></span> <span data-ttu-id="c9d70-246">如果您的應用程式所花的時間大於 (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000 秒，則 iisnode 會傳回 500 錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9d70-246">If your application takes longer than (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000 seconds, iisnode will return 500 error.</span></span> <span data-ttu-id="c9d70-247">增加這些設定的值，以符合您的應用程式開始時間，可防止 iisnode 逾時並傳回 500 錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9d70-247">Increase the values of these settings to match your application start time to prevent iisnode from timing out and returning the 500 error.</span></span>

### <a name="my-node-application-crashed"></a><span data-ttu-id="c9d70-248">我的節點應用程式毀損</span><span class="sxs-lookup"><span data-stu-id="c9d70-248">My node application crashed</span></span>
<span data-ttu-id="c9d70-249">您的應用程式擲回未攔截的例外狀況 - 請檢查 d:\\home\\LogFiles\\Application\\logging-errors.txt file 檔案，以取得所擲回例外狀況的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c9d70-249">Your application is throwing uncaught exceptions – Please check d:\\home\\LogFiles\\Application\\logging-errors.txt file for the details on the exception thrown.</span></span> <span data-ttu-id="c9d70-250">這個檔案有堆疊追蹤，所以您可以據此修正您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9d70-250">This file has the stack trace so you can fix your application based on this.</span></span>

### <a name="my-node-application-takes-too-much-time-to-startup-cold-start"></a><span data-ttu-id="c9d70-251">我的節點應用程式花太多時間啟動 (冷啟動)</span><span class="sxs-lookup"><span data-stu-id="c9d70-251">My node application takes too much time to startup (Cold Start)</span></span>
<span data-ttu-id="c9d70-252">最常見原因的是應用程式在 node\_modules 中有很多檔案，而且應用程式嘗試在啟動期間載入大多數的檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d70-252">Most common reason for this is that the application has a lot of files in the node\_modules and the application tries to load most of these files during startup.</span></span> <span data-ttu-id="c9d70-253">根據預設，因為您的檔案位於 Azure Web Apps 的網路共用上，所以載入太多檔案可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="c9d70-253">By default, since your files reside on the network share on Azure Webapps, loading so many files can take some time.</span></span>
<span data-ttu-id="c9d70-254">讓載入速度變快的解決方式如下︰</span><span class="sxs-lookup"><span data-stu-id="c9d70-254">Some solutions to make this faster are:</span></span>

1. <span data-ttu-id="c9d70-255">使用 npm3 來安裝您的模組，確定您有扁平相依性結構，並沒有重複的相依性。</span><span class="sxs-lookup"><span data-stu-id="c9d70-255">Make sure you have a flat dependency structure and no duplicate dependencies by using npm3 to install your modules.</span></span>
2. <span data-ttu-id="c9d70-256">試著延遲載入您的 node\_modules，而不要在啟動時載入所有的模組。</span><span class="sxs-lookup"><span data-stu-id="c9d70-256">Try to lazy load your node\_modules and not load all of the modules at startup.</span></span> <span data-ttu-id="c9d70-257">這表示對 require('module') 的呼叫應該在嘗試使用模組的函式中有實際需要時進行。</span><span class="sxs-lookup"><span data-stu-id="c9d70-257">This means that the call to require(‘module’) should be done when you actually need it within the function you try to use the module.</span></span>
3. <span data-ttu-id="c9d70-258">Azure Web Apps 會提供稱為本機快取的功能。</span><span class="sxs-lookup"><span data-stu-id="c9d70-258">Azure Webapps offers a feature called local cache.</span></span> <span data-ttu-id="c9d70-259">這項功能會將您的內容從網路共用複製到 VM 上的本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="c9d70-259">This feature copies your content from the network share to the local disk on the VM.</span></span> <span data-ttu-id="c9d70-260">因為這些檔案都在本機，node\_modules 的載入時間快很多。</span><span class="sxs-lookup"><span data-stu-id="c9d70-260">Since the files are local, the load time of node\_modules is much faster.</span></span> <span data-ttu-id="c9d70-261">- 本 [文件](../app-service/app-service-local-cache.md) 詳細說明如何使用本機快取。</span><span class="sxs-lookup"><span data-stu-id="c9d70-261">- This [documentation](../app-service/app-service-local-cache.md) explains how to use Local Cache in more detail.</span></span>

## <a name="iisnode-http-status-and-substatus"></a><span data-ttu-id="c9d70-262">IISNODE http 狀態和子狀態</span><span class="sxs-lookup"><span data-stu-id="c9d70-262">IISNODE http status and substatus</span></span>
<span data-ttu-id="c9d70-263">此 [原始程式檔](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) 會列出 iisnode 可在發生錯誤時傳回的所有可能狀態/子狀態組合。</span><span class="sxs-lookup"><span data-stu-id="c9d70-263">This [source file](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) lists all the possible status/substatus combination iisnode can return in case of error.</span></span>

<span data-ttu-id="c9d70-264">為您的應用程式啟用 FREB 以查看 win32 錯誤碼 (基於效能考量，請確定只在非生產網站上啟用 FREB)。</span><span class="sxs-lookup"><span data-stu-id="c9d70-264">Enable FREB for your application to see the win32 error code (please make sure you enable FREB only on non-production sites for performance reasons).</span></span>

| <span data-ttu-id="c9d70-265">Http 狀態</span><span class="sxs-lookup"><span data-stu-id="c9d70-265">Http Status</span></span> | <span data-ttu-id="c9d70-266">Http 子狀態</span><span class="sxs-lookup"><span data-stu-id="c9d70-266">Http SubStatus</span></span> | <span data-ttu-id="c9d70-267">可能的原因？</span><span class="sxs-lookup"><span data-stu-id="c9d70-267">Possible Reason?</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c9d70-268">500</span><span class="sxs-lookup"><span data-stu-id="c9d70-268">500</span></span> |<span data-ttu-id="c9d70-269">1000</span><span class="sxs-lookup"><span data-stu-id="c9d70-269">1000</span></span> |<span data-ttu-id="c9d70-270">將要求分派至 IISNODE 時發生一些問題 – 檢查 node.exe 是否已啟動。</span><span class="sxs-lookup"><span data-stu-id="c9d70-270">There was some issue dispatching the request to IISNODE – check if node.exe was started up.</span></span> <span data-ttu-id="c9d70-271">Node.exe 可能在啟動時損毀。</span><span class="sxs-lookup"><span data-stu-id="c9d70-271">Node.exe could have crashed on startup.</span></span> <span data-ttu-id="c9d70-272">檢查 web.config 組態是否有錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9d70-272">Check your web.config configuration for errors.</span></span> |
| <span data-ttu-id="c9d70-273">500</span><span class="sxs-lookup"><span data-stu-id="c9d70-273">500</span></span> |<span data-ttu-id="c9d70-274">1001</span><span class="sxs-lookup"><span data-stu-id="c9d70-274">1001</span></span> |<span data-ttu-id="c9d70-275">- Win32Error 0x2 - 應用程式並未回應 URL。</span><span class="sxs-lookup"><span data-stu-id="c9d70-275">- Win32Error 0x2 - App is not responding to the URL.</span></span> <span data-ttu-id="c9d70-276">檢查 URL 重寫規則，或您的快速應用程式是否已定義正確的路由。</span><span class="sxs-lookup"><span data-stu-id="c9d70-276">Check URL rewrite rules or if your express app has the correct routes defined.</span></span> <span data-ttu-id="c9d70-277">- Win32Error 0x6d – 具名管道忙碌中 – Node.exe 不接受要求，因為管道忙碌中。</span><span class="sxs-lookup"><span data-stu-id="c9d70-277">- Win32Error 0x6d – named pipe is busy – Node.exe is not accepting requests because the pipe is busy.</span></span> <span data-ttu-id="c9d70-278">檢查高 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="c9d70-278">Check high cpu usage.</span></span> <span data-ttu-id="c9d70-279">- 其他錯誤 – 檢查 node.exe 是否毀損。</span><span class="sxs-lookup"><span data-stu-id="c9d70-279">- Other errors – check if node.exe crashed.</span></span> |
| <span data-ttu-id="c9d70-280">500</span><span class="sxs-lookup"><span data-stu-id="c9d70-280">500</span></span> |<span data-ttu-id="c9d70-281">1002</span><span class="sxs-lookup"><span data-stu-id="c9d70-281">1002</span></span> |<span data-ttu-id="c9d70-282">Node.exe 損毀 – 檢查 d:\\home\\LogFiles\\logging-errors.txt 中的堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="c9d70-282">Node.exe crashed – check d:\\home\\LogFiles\\logging-errors.txt for stack trace.</span></span> |
| <span data-ttu-id="c9d70-283">500</span><span class="sxs-lookup"><span data-stu-id="c9d70-283">500</span></span> |<span data-ttu-id="c9d70-284">1003</span><span class="sxs-lookup"><span data-stu-id="c9d70-284">1003</span></span> |<span data-ttu-id="c9d70-285">管道組態問題 – 您不應該看見此問題，但如果看見，則表示具名管道組態不正確。</span><span class="sxs-lookup"><span data-stu-id="c9d70-285">Pipe configuration Issue – You should never see this but if you do, the named pipe configuration is incorrect.</span></span> |
| <span data-ttu-id="c9d70-286">500</span><span class="sxs-lookup"><span data-stu-id="c9d70-286">500</span></span> |<span data-ttu-id="c9d70-287">1004-1018</span><span class="sxs-lookup"><span data-stu-id="c9d70-287">1004-1018</span></span> |<span data-ttu-id="c9d70-288">傳送要求或處理 node.exe 的相關回應時發生一些錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9d70-288">There was some error while sending the request or processing the response to/from node.exe.</span></span> <span data-ttu-id="c9d70-289">檢查 node.exe 是否損毀。</span><span class="sxs-lookup"><span data-stu-id="c9d70-289">Check if node.exe crashed.</span></span> <span data-ttu-id="c9d70-290">檢查 d:\\home\\LogFiles\\logging-errors.txt 中的堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="c9d70-290">check d:\\home\\LogFiles\\logging-errors.txt for stack trace.</span></span> |
| <span data-ttu-id="c9d70-291">503</span><span class="sxs-lookup"><span data-stu-id="c9d70-291">503</span></span> |<span data-ttu-id="c9d70-292">1000</span><span class="sxs-lookup"><span data-stu-id="c9d70-292">1000</span></span> |<span data-ttu-id="c9d70-293">記憶體不足，無法配置更多具名管道連線。</span><span class="sxs-lookup"><span data-stu-id="c9d70-293">Not enough memory to allocate more named pipe connections.</span></span> <span data-ttu-id="c9d70-294">檢查您的應用程式為何使用這麼多的記憶體。</span><span class="sxs-lookup"><span data-stu-id="c9d70-294">Check why your app is consuming so much memory.</span></span> <span data-ttu-id="c9d70-295">檢查 maxConcurrentRequestsPerProcess 設定值。</span><span class="sxs-lookup"><span data-stu-id="c9d70-295">Check maxConcurrentRequestsPerProcess setting value.</span></span> <span data-ttu-id="c9d70-296">如果此值並非無限，而且您有許多要求，請增加此值來避免這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9d70-296">If its not infinite and you have a lot of requests, increase this value to prevent this error.</span></span> |
| <span data-ttu-id="c9d70-297">503</span><span class="sxs-lookup"><span data-stu-id="c9d70-297">503</span></span> |<span data-ttu-id="c9d70-298">1001</span><span class="sxs-lookup"><span data-stu-id="c9d70-298">1001</span></span> |<span data-ttu-id="c9d70-299">無法將要求分派至 node.exe，因為應用程式正在回收處理。</span><span class="sxs-lookup"><span data-stu-id="c9d70-299">Request could not be dispatched to node.exe because the application is recycling.</span></span> <span data-ttu-id="c9d70-300">回收應用程式之後，應該會正常提供要求。</span><span class="sxs-lookup"><span data-stu-id="c9d70-300">After the application has recycled, requests should be served normally.</span></span> |
| <span data-ttu-id="c9d70-301">503</span><span class="sxs-lookup"><span data-stu-id="c9d70-301">503</span></span> |<span data-ttu-id="c9d70-302">1002</span><span class="sxs-lookup"><span data-stu-id="c9d70-302">1002</span></span> |<span data-ttu-id="c9d70-303">檢查 win32 錯誤碼的實際原因 – 無法將要求分派至 node.exe。</span><span class="sxs-lookup"><span data-stu-id="c9d70-303">Check win32 error code for actual reason – Request could not be dispatched to a node.exe.</span></span> |
| <span data-ttu-id="c9d70-304">503</span><span class="sxs-lookup"><span data-stu-id="c9d70-304">503</span></span> |<span data-ttu-id="c9d70-305">1003</span><span class="sxs-lookup"><span data-stu-id="c9d70-305">1003</span></span> |<span data-ttu-id="c9d70-306">具名管道太忙 – 檢查節點是否正耗用大量的 CPU</span><span class="sxs-lookup"><span data-stu-id="c9d70-306">Named pipe is too Busy – Check if node is consuming a lot of CPU</span></span> |

<span data-ttu-id="c9d70-307">NODE.exe 內有名為 NODE\_PENDING\_PIPE\_INSTANCES 的設定。</span><span class="sxs-lookup"><span data-stu-id="c9d70-307">There is a setting within NODE.exe called NODE\_PENDING\_PIPE\_INSTANCES.</span></span> <span data-ttu-id="c9d70-308">根據預設，此值在 Azure Web Apps 外部為 4。</span><span class="sxs-lookup"><span data-stu-id="c9d70-308">By default outside of azure webapps this value is 4.</span></span> <span data-ttu-id="c9d70-309">這表示該 node.exe 在具名管道上一次只能接受 4 個要求。</span><span class="sxs-lookup"><span data-stu-id="c9d70-309">This means that node.exe can only accept 4 requests at a time on the named pipe.</span></span> <span data-ttu-id="c9d70-310">在 Azure Web Apps，此值設定為 5000，這個值應足以滿足大部分在 Azure Web Apps 上執行的節點應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9d70-310">On Azure Webapps, this value is set to 5000 and this value should be good enough for most node applications running on azure webapps.</span></span> <span data-ttu-id="c9d70-311">您不應該在 Azure Web Apps 上看見 503.1003，因為我們 NODE\_PENDING\_PIPE\_INSTANCES 的值較高。</span><span class="sxs-lookup"><span data-stu-id="c9d70-311">You should not see 503.1003 on azure webapps because we have a high value for the NODE\_PENDING\_PIPE\_INSTANCES.</span></span>  |

## <a name="more-resources"></a><span data-ttu-id="c9d70-312">其他資源</span><span class="sxs-lookup"><span data-stu-id="c9d70-312">More resources</span></span>
<span data-ttu-id="c9d70-313">請遵循下列連結以深入了解 Azure App Service 上的 node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9d70-313">Follow these links to learn more about node.js applications on Azure App Service.</span></span>

* [<span data-ttu-id="c9d70-314">在 Azure App Service 中開始使用 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c9d70-314">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="c9d70-315">如何在 Azure App Service 中偵錯 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c9d70-315">How to debug a Node.js web app in Azure App Service</span></span>](web-sites-nodejs-debug.md)
* [<span data-ttu-id="c9d70-316">使用 Node.js 模組與 Azure 應用程式搭配</span><span class="sxs-lookup"><span data-stu-id="c9d70-316">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
* [<span data-ttu-id="c9d70-317">Azure App Service Web Apps：Node.js</span><span class="sxs-lookup"><span data-stu-id="c9d70-317">Azure App Service Web Apps: Node.js</span></span>](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [<span data-ttu-id="c9d70-318">Node.js 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="c9d70-318">Node.js Developer Center</span></span>](../nodejs-use-node-modules-azure-apps.md)
* [<span data-ttu-id="c9d70-319">探索神秘無比的 Kudu 偵錯主控台</span><span class="sxs-lookup"><span data-stu-id="c9d70-319">Exploring the Super Secret Kudu Debug Console</span></span>](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

