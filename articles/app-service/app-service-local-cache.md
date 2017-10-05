---
title: "Azure App Service 本機快取概觀 | Microsoft Docs"
description: "本文說明如何啟用、調整大小並查詢 Azure App Service 本機快取功能的狀態"
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: e00d453e9ae34cafb5ce753f63c253e954d6b09a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-local-cache-overview"></a><span data-ttu-id="d3f6a-103">Azure App Service 本機快取概觀</span><span class="sxs-lookup"><span data-stu-id="d3f6a-103">Azure App Service Local Cache overview</span></span>
<span data-ttu-id="d3f6a-104">Azure Web 應用程式的內容儲存在 Azure 儲存體中，並且會持久顯示為內容共用。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-104">Azure web app content is stored on Azure Storage and is surfaced up in a durable manner as a content share.</span></span> <span data-ttu-id="d3f6a-105">這項設計的目的是為了要與各種應用程式搭配使用，而且其具有下列特性︰</span><span class="sxs-lookup"><span data-stu-id="d3f6a-105">This design is intended to work with a variety of apps and has the following attributes:</span></span>  

* <span data-ttu-id="d3f6a-106">內容會由 Web 應用程式的多個虛擬機器 (VM) 執行個體共用。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-106">The content is shared across multiple virtual machine (VM) instances of the web app.</span></span>
* <span data-ttu-id="d3f6a-107">內容具有持久性，且可透過執行 Web 應用程式來修改。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-107">The content is durable and can be modified by running web apps.</span></span>
* <span data-ttu-id="d3f6a-108">記錄檔和診斷資料檔案會在相同的共用內容資料夾底下提供使用。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-108">Log files and diagnostic data files are available under the same shared content folder.</span></span>
* <span data-ttu-id="d3f6a-109">發佈新內容時會直接更新內容資料夾。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-109">Publishing new content directly updates the content folder.</span></span> <span data-ttu-id="d3f6a-110">透過 SCM 網站和執行 Web 應用程式即可立即檢視相同的內容 (通常來說，ASP.NET 之類的某些技術確實會在某些檔案變更時讓 Web 應用程式重新啟動以取得最新內容)。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-110">You can immediately view the same content through the SCM website and the running web app (typically some technologies such as ASP.NET do initiate a web app restart on some file changes to get the latest content).</span></span>

<span data-ttu-id="d3f6a-111">雖然許多 Web 應用程式會使用上述其中一項功能或所有功能，但某些 Web 應用程式只需要可從中執行的內容存放區，而且此存放區具備高效能、唯讀和高可用性。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-111">While many web apps use one or all of these features, some web apps just need a high-performance, read-only content store that they can run from with high availability.</span></span> <span data-ttu-id="d3f6a-112">這些應用程式可以受益於特定本機快取的 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-112">These apps can benefit from a VM instance of a specific local cache.</span></span>

<span data-ttu-id="d3f6a-113">Azure App Service 本機快取功能可讓您以 Web 角色檢視您的內容。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-113">The Azure App Service Local Cache feature provides a web role view of your content.</span></span> <span data-ttu-id="d3f6a-114">這個內容是在網站啟動時，以非同步方式建立之儲存體內容的 write-but-discard 快取。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-114">This content is a write-but-discard cache of your storage content that is created asynchronously on site startup.</span></span> <span data-ttu-id="d3f6a-115">當快取已準備就緒時，網站會切換為執行快取的內容。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-115">When the cache is ready, the site is switched to run against the cached content.</span></span> <span data-ttu-id="d3f6a-116">在本機快取執行的 Web 應用程式具有下列優點︰</span><span class="sxs-lookup"><span data-stu-id="d3f6a-116">Web apps that run on Local Cache have the following benefits:</span></span>

* <span data-ttu-id="d3f6a-117">它們不受存取 Azure 儲存體上的內容時所發生的延遲影響。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-117">They are immune to latencies that occur when they access content on Azure Storage.</span></span>
* <span data-ttu-id="d3f6a-118">它們不受提供內容共用之伺服器所進行的計劃性升級或非計劃性停機，以及 Azure 儲存體的任何其他中斷所影響。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-118">They are immune to the planned upgrades or unplanned downtimes and any other disruptions with Azure Storage that occur on servers that serve the content share.</span></span>
* <span data-ttu-id="d3f6a-119">應用程式比較不會因為儲存體共用變更而重新啟動。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-119">They have fewer app restarts due to storage share changes.</span></span>

## <a name="how-local-cache-changes-the-behavior-of-app-service"></a><span data-ttu-id="d3f6a-120">本機快取對 App Service 的行為所造成的影響</span><span class="sxs-lookup"><span data-stu-id="d3f6a-120">How Local Cache changes the behavior of App Service</span></span>
* <span data-ttu-id="d3f6a-121">本機快取是 Web 應用程式之 /site 和 /siteextensions 資料夾的複本。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-121">The local cache is a copy of the /site and /siteextensions folders of the web app.</span></span> <span data-ttu-id="d3f6a-122">當 Web 應用程式啟動時，便會在本機 VM 執行個體上建立本機快取。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-122">It is created on the local VM instance on web app startup.</span></span> <span data-ttu-id="d3f6a-123">每個 Web 應用程式的本機快取大小，預設是限制為 300 MB，但最多可以增加至 2 GB。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-123">The size of the local cache per web app is limited to 300 MB by default, but you can increase it up to 2 GB.</span></span>
* <span data-ttu-id="d3f6a-124">本機快取具有讀寫屬性。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-124">The local cache is read-write.</span></span> <span data-ttu-id="d3f6a-125">不過在 Web 應用程式移動虛擬機器或重新啟動時，將會捨棄任何修改。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-125">However, any modifications will be discarded when the web app moves virtual machines or gets restarted.</span></span> <span data-ttu-id="d3f6a-126">因此，請勿針對會在內容存放區中儲存關鍵任務資料的應用程式使用本機快取。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-126">You should not use Local Cache for apps that store mission-critical data in the content store.</span></span>
* <span data-ttu-id="d3f6a-127">Web 應用程式可以像目前一樣，繼續寫入記錄檔和診斷資料。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-127">Web apps can continue to write log files and diagnostic data as they do currently.</span></span> <span data-ttu-id="d3f6a-128">不過，記錄檔和資料會儲存在 VM 本機上。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-128">Log files and data, however, are stored locally on the VM.</span></span> <span data-ttu-id="d3f6a-129">然後再定期將它們複製到共用內容存放區。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-129">Then they are copied over periodically to the shared content store.</span></span> <span data-ttu-id="d3f6a-130">複製到共用內容存放區是最好的狀況；回寫可能會因為 VM 執行個體突然當機而遺失。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-130">The copy to the shared content store is a best-case effort--write backs could be lost due to a sudden crash of a VM instance.</span></span>
* <span data-ttu-id="d3f6a-131">使用「本機快取」之 Web 應用程式的「記錄檔」和「資料」資料夾的資料夾結構有所變更。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-131">There is a change in the folder structure of the LogFiles and Data folders for web apps that use Local Cache.</span></span> <span data-ttu-id="d3f6a-132">儲存體的「記錄檔」和「資料」資料夾中現在有子資料夾，且這些子資料夾會遵循「唯一識別碼」+ 時間戳記的命名模式。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-132">There are now subfolders in the storage LogFiles and Data folders that follow the naming pattern of "unique identifier" + time stamp.</span></span> <span data-ttu-id="d3f6a-133">每個子資料夾都對應到將要用來執行或已用來執行 Web 應用程式的 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-133">Each of the subfolders corresponds to a VM instance where the web app is running or has run.</span></span>  
* <span data-ttu-id="d3f6a-134">透過任何發佈機制將變更發佈至 Web 應用程式時，將會發佈到共用內容存放區。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-134">Publishing changes to the web app through any of the publishing mechanisms will publish to the shared content store.</span></span> <span data-ttu-id="d3f6a-135">這是預設行為，因為我們希望發佈的內容具有持久性。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-135">This is by design because we want the published content to be durable.</span></span> <span data-ttu-id="d3f6a-136">為了重新整理 Web 應用程式的本機快取，就必須重新啟動 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-136">To refresh the local cache of the web app, it needs to be restarted.</span></span> <span data-ttu-id="d3f6a-137">這個步驟看起來是多餘的，不是嗎？</span><span class="sxs-lookup"><span data-stu-id="d3f6a-137">Does this seem like an excessive step?</span></span> <span data-ttu-id="d3f6a-138">為了讓整個生命週期順暢前進，請參閱本文稍後的資訊。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-138">To make the lifecycle seamless, see the information later in this article.</span></span>
* <span data-ttu-id="d3f6a-139">D:\Home 會指向本機快取。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-139">D:\Home will point to the local cache.</span></span> <span data-ttu-id="d3f6a-140">D:\local 將繼續指向暫存 VM 的特定儲存體。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-140">D:\local will continue pointing to the temporary VM specific storage.</span></span>
* <span data-ttu-id="d3f6a-141">SCM 網站的預設內容檢視將仍是共用內容存放區。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-141">The default content view of the SCM site will continue to be that of the shared content store.</span></span>

## <a name="enable-local-cache-in-app-service"></a><span data-ttu-id="d3f6a-142">在 App Service 中啟用本機快取</span><span class="sxs-lookup"><span data-stu-id="d3f6a-142">Enable Local Cache in App Service</span></span>
<span data-ttu-id="d3f6a-143">您可以使用保留的應用程式設定的組合，以設定本機快取。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-143">You configure Local Cache by using a combination of reserved app settings.</span></span> <span data-ttu-id="d3f6a-144">這些應用程式設定可以使用下列方法來設定：</span><span class="sxs-lookup"><span data-stu-id="d3f6a-144">You can configure these app settings by using the following methods:</span></span>

* [<span data-ttu-id="d3f6a-145">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d3f6a-145">Azure portal</span></span>](#Configure-Local-Cache-Portal)
* [<span data-ttu-id="d3f6a-146">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d3f6a-146">Azure Resource Manager</span></span>](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-the-azure-portal"></a><span data-ttu-id="d3f6a-147">使用 Azure 入口網站設定本機快取</span><span class="sxs-lookup"><span data-stu-id="d3f6a-147">Configure Local Cache by using the Azure portal</span></span>
<a name="Configure-Local-Cache-Portal"></a>

<span data-ttu-id="d3f6a-148">您可以使用下列應用程式設定來針對每個 Web 應用程式啟用本機快取︰ `WEBSITE_LOCAL_CACHE_OPTION` = `Always`</span><span class="sxs-lookup"><span data-stu-id="d3f6a-148">You enable Local Cache on a per-web-app basis by using this app setting: `WEBSITE_LOCAL_CACHE_OPTION` = `Always`</span></span>  

![Azure 入口網站應用程式設定︰本機快取](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a><span data-ttu-id="d3f6a-150">使用 Azure Resource Manager 設定本機快取</span><span class="sxs-lookup"><span data-stu-id="d3f6a-150">Configure Local Cache by using Azure Resource Manager</span></span>
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-the-size-setting-in-local-cache"></a><span data-ttu-id="d3f6a-151">變更本機快取中的大小設定</span><span class="sxs-lookup"><span data-stu-id="d3f6a-151">Change the size setting in Local Cache</span></span>
<span data-ttu-id="d3f6a-152">根據預設，本機快取大小是 **300 MB**。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-152">By default, the local cache size is **300 MB**.</span></span> <span data-ttu-id="d3f6a-153">此大小包括複製自內容存放區的 /site 和 /siteextensions 資料夾，以及任何在本機建立之記錄檔和資料的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-153">This includes the /site and /siteextensions folders that are copied from the content store, as well as any locally created logs and data folders.</span></span> <span data-ttu-id="d3f6a-154">若要增加此限制，請使用應用程式設定 `WEBSITE_LOCAL_CACHE_SIZEINMB`。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-154">To increase this limit, use the app setting `WEBSITE_LOCAL_CACHE_SIZEINMB`.</span></span> <span data-ttu-id="d3f6a-155">每個 Web 應用程式的大小最多可以增加為 **2 GB** (2000 MB)。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-155">You can increase the size up to **2 GB** (2000 MB) per web app.</span></span>

## <a name="best-practices-for-using-app-service-local-cache"></a><span data-ttu-id="d3f6a-156">使用 App Service 本機快取的最佳作法</span><span class="sxs-lookup"><span data-stu-id="d3f6a-156">Best practices for using App Service Local Cache</span></span>
<span data-ttu-id="d3f6a-157">建議您搭配 [預備環境](../app-service-web/web-sites-staged-publishing.md) 功能使用本機快取。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-157">We recommend that you use Local Cache in conjunction with the [Staging Environments](../app-service-web/web-sites-staged-publishing.md) feature.</span></span>

* <span data-ttu-id="d3f6a-158">將「黏性」應用程式設定 `WEBSITE_LOCAL_CACHE_OPTION` 與值 `Always` 新增至您的**生產環境**位置。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-158">Add the *sticky* app setting `WEBSITE_LOCAL_CACHE_OPTION` with the value `Always` to your **Production** slot.</span></span> <span data-ttu-id="d3f6a-159">如果您要使用 `WEBSITE_LOCAL_CACHE_SIZEINMB`，也將它做為黏性設定新增至您的生產環境位置。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-159">If you're using `WEBSITE_LOCAL_CACHE_SIZEINMB`, also add it as a sticky setting to your Production slot.</span></span>
* <span data-ttu-id="d3f6a-160">建立 **預備環境** 位置，並發佈至您的預備環境位置。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-160">Create a **Staging** slot and publish to your Staging slot.</span></span> <span data-ttu-id="d3f6a-161">如果您獲得生產環境位置之「本機快取」提供的好處，便通常不會將預備環境位置設定為使用本機快取以在預備環境獲得順暢的「建置、部署、測試」生命週期。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-161">You typically don't set the staging slot to use Local Cache to enable a seamless build-deploy-test lifecycle for staging if you get the benefits of Local Cache for the production slot.</span></span>
* <span data-ttu-id="d3f6a-162">針對預備位置測試您的網站。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-162">Test your site against your Staging slot.</span></span>  
* <span data-ttu-id="d3f6a-163">準備好後，請在您的「預備環境」和「生產環境」位置之間發出 [交換作業](../app-service-web/web-sites-staged-publishing.md#Swap) 。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-163">When you are ready, issue a [swap operation](../app-service-web/web-sites-staged-publishing.md#Swap) between your Staging and Production slots.</span></span>  
* <span data-ttu-id="d3f6a-164">黏性設定包含位置的名稱和黏性。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-164">Sticky settings include name and sticky to a slot.</span></span> <span data-ttu-id="d3f6a-165">因此當預備環境位置交換到生產環境時，它會繼承本機快取應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-165">So when the Staging slot gets swapped into Production, it will inherit the Local Cache app settings.</span></span> <span data-ttu-id="d3f6a-166">新交換的生產環境位置會在幾分鐘後針對「本機快取」執行，並會在交換後的位置準備就緒時一併就緒。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-166">The newly swapped Production slot will run against the local cache after a few minutes and will be warmed up as part of slot warmup after swap.</span></span> <span data-ttu-id="d3f6a-167">因此完成位置交換時，將會針對「本機快取」執行您的生產環境位置。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-167">So when the slot swap is complete, your Production slot will be running against the local cache.</span></span>

## <a name="frequently-asked-questions-faq"></a><span data-ttu-id="d3f6a-168">常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="d3f6a-168">Frequently asked questions (FAQ)</span></span>
### <a name="how-can-i-tell-if-local-cache-applies-to-my-web-app"></a><span data-ttu-id="d3f6a-169">如何知道「本機快取」是否適用於我的 Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="d3f6a-169">How can I tell if Local Cache applies to my web app?</span></span>
<span data-ttu-id="d3f6a-170">如果您的 Web 應用程式需要高效能、可靠的內容存放區，且不使用內容存放區在執行階段時寫入重要資料並且大小總計小於 2 GB，那麼答案就是肯定的！</span><span class="sxs-lookup"><span data-stu-id="d3f6a-170">If your web app needs a high-performance, reliable content store, does not use the content store to write critical data at runtime, and is less than 2 GB in total size, then the answer is "yes"!</span></span> <span data-ttu-id="d3f6a-171">若要取得您 /site 和 /siteextensions 資料夾的大小總計，您可以使用網站擴充功能「Azure Web Apps 磁碟使用量」。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-171">To get the total size of your /site and /siteextensions folders, you can use the site extension "Azure Web Apps Disk Usage".</span></span>  

### <a name="how-can-i-tell-if-my-site-has-switched-to-using-local-cache"></a><span data-ttu-id="d3f6a-172">如何知道我的網站是否已切換成使用本機快取？</span><span class="sxs-lookup"><span data-stu-id="d3f6a-172">How can I tell if my site has switched to using Local Cache?</span></span>
<span data-ttu-id="d3f6a-173">如果搭配預備環境使用「本機快取」，在本機快取準備就緒之前將無法完成交換作業。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-173">If you're using the Local Cache feature with Staging Environments, the swap operation will not complete until Local Cache is warmed up.</span></span> <span data-ttu-id="d3f6a-174">若要檢查您的網站是否正在執行本機快取，您可以檢查工作者處理序環境變數 `WEBSITE_LOCALCACHE_READY`。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-174">To check if your site is running against Local Cache, you can check the worker process environment variable `WEBSITE_LOCALCACHE_READY`.</span></span> <span data-ttu-id="d3f6a-175">使用 [背景工作角色處理序環境變數](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) 頁面中的指示，存取多個執行個體上的工作者處理序環境變數。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-175">Use the instructions on the [worker process environment variable](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) page to access the worker process environment variable on multiple instances.</span></span>  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-to-have-them-why"></a><span data-ttu-id="d3f6a-176">我剛剛發佈了新的變更，但我的 Web 應用程式似乎沒有變更。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-176">I just published new changes, but my web app does not seem to have them.</span></span> <span data-ttu-id="d3f6a-177">原因為何？</span><span class="sxs-lookup"><span data-stu-id="d3f6a-177">Why?</span></span>
<span data-ttu-id="d3f6a-178">如果您的 Web 應用程式使用「本機快取」，則您需要重新啟動您的網站，以取得最新的變更。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-178">If your web app uses Local Cache, then you need to restart your site to get the latest changes.</span></span> <span data-ttu-id="d3f6a-179">不想對生產網站發佈變更嗎？</span><span class="sxs-lookup"><span data-stu-id="d3f6a-179">Don’t want to publish changes to a production site?</span></span> <span data-ttu-id="d3f6a-180">請參閱前面的最佳作法一節中的位置選項。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-180">See the slot options in the previous best practices section.</span></span>

### <a name="where-are-my-logs"></a><span data-ttu-id="d3f6a-181">我的記錄檔在哪裡？</span><span class="sxs-lookup"><span data-stu-id="d3f6a-181">Where are my logs?</span></span>
<span data-ttu-id="d3f6a-182">使用本機快取，您的記錄檔和資料的資料夾看起來會有點不同。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-182">With Local Cache, your logs and data folders do look a little different.</span></span> <span data-ttu-id="d3f6a-183">不過，子資料夾的結構會保持相同，不同之處在於這些子資料夾會位在格式為「唯一 VM 識別碼」+ 時間戳記的子資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-183">However, the structure of your subfolders remains the same, except that the subfolders are nestled under a subfolder with the format "unique VM identifier" + time stamp.</span></span>

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a><span data-ttu-id="d3f6a-184">我已啟用「本機快取」，但我的 Web 應用程式仍然重新啟動。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-184">I have Local Cache enabled, but my web app still gets restarted.</span></span> <span data-ttu-id="d3f6a-185">這是為什麼？</span><span class="sxs-lookup"><span data-stu-id="d3f6a-185">Why is that?</span></span> <span data-ttu-id="d3f6a-186">我以為「本機快取」有助於頻繁的應用程式重新啟動。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-186">I thought Local Cache helped with frequent app restarts.</span></span>
<span data-ttu-id="d3f6a-187">「本機快取」確實有助於防止儲存體相關 Web 應用程式重新啟動。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-187">Local Cache does help prevent storage-related web app restarts.</span></span> <span data-ttu-id="d3f6a-188">不過，您的 Web 應用程式仍有可能在計劃性 VM 基礎結構升級期間重新啟動。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-188">However, your web app could still undergo restarts during planned infrastructure upgrades of the VM.</span></span> <span data-ttu-id="d3f6a-189">整體而言，啟用「本機快取」後應該比較不會發生應用程式重新啟動。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-189">The overall app restarts that you experience with Local Cache enabled should be fewer.</span></span>

### <a name="does-local-cache-exclude-any-directories-from-being-copied-to-the-faster-local-drive"></a><span data-ttu-id="d3f6a-190">「本機快取」會排除所有目錄而不會複製到更快的本機磁碟機嗎？</span><span class="sxs-lookup"><span data-stu-id="d3f6a-190">Does Local Cache exclude any directories from being copied to the faster local drive?</span></span>
<span data-ttu-id="d3f6a-191">在複製儲存體內容的步驟中，將會排除名為儲存機制的任何資料夾。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-191">As part of the step that copies the storage content any folder that is named repository will be excluded.</span></span> <span data-ttu-id="d3f6a-192">當您的網站內容可能包含 Web 應用程式的日常作業不需要的原始檔控制儲存機制時，這會有幫助。</span><span class="sxs-lookup"><span data-stu-id="d3f6a-192">This helps with scenarios where your site content may contain a source control repository that may not be needed in day to day operation of the web app.</span></span> 
