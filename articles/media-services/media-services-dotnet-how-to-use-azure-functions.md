---
title: "aaaDevelop Azure Media services 的函式"
description: "本主題說明如何開發 Azure Media Services 使用的函式的 toostart hello Azure 入口網站。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="afc60-103">開發具有媒體服務的 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="afc60-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="afc60-104">本主題說明如何 tooget 開始建立使用媒體服務的 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="afc60-104">This topic shows you how tooget started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="afc60-105">hello Azure 本主題中所定義的函式監視名為儲存體帳戶容器**輸入**新 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="afc60-105">hello Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="afc60-106">一旦檔案放入 hello 儲存體容器，hello blob 觸發程序會執行 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="afc60-106">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>

<span data-ttu-id="afc60-107">如果您想 tooexplore 和部署使用 Azure Media Services 的現有 Azure 函式時，請參閱[媒體服務的 Azure 功能](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)。</span><span class="sxs-lookup"><span data-stu-id="afc60-107">If you want tooexplore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="afc60-108">這個儲存機制包含使用 Media Services tooshow 工作流程相關的 tooingesting 內容直接從 blob 儲存體，編碼方式，將內容寫入回 tooblob 儲存體的範例。</span><span class="sxs-lookup"><span data-stu-id="afc60-108">This repository contains examples that use Media Services tooshow workflows related tooingesting content directly from blob storage, encoding, and writing content back tooblob storage.</span></span> <span data-ttu-id="afc60-109">它也包含如何 toomonitor 作業透過 Webhook 和 Azure 佇列通知的範例。</span><span class="sxs-lookup"><span data-stu-id="afc60-109">It also includes examples of how toomonitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="afc60-110">您也可以開發根據 hello 中的 hello 範例函式[媒體服務的 Azure 功能](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)儲存機制。</span><span class="sxs-lookup"><span data-stu-id="afc60-110">You can also develop your Functions based on hello examples in hello [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="afc60-111">toodeploy hello 函式，請按 hello**部署 tooAzure** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="afc60-111">toodeploy hello functions, press hello **Deploy tooAzure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afc60-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="afc60-112">Prerequisites</span></span>

- <span data-ttu-id="afc60-113">您可以建立您的第一個函式之前，您會需要 toohave 有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="afc60-113">Before you can create your first function, you need toohave an active Azure account.</span></span> <span data-ttu-id="afc60-114">如果您還沒有 Azure 帳戶， [可以使用免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="afc60-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="afc60-115">如果您正在執行您的 Azure 媒體服務 (AMS) 帳戶或接聽 tooevents 由 Media Services 傳送 toocreate Azure 函式，如所述，您應該建立 AMS 帳戶，[這裡](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="afc60-115">If you are going toocreate Azure Functions that perform actions on your Azure Media Services (AMS) account or listen tooevents sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="afc60-116">了解[如何 toouse Azure 函式](../azure-functions/functions-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="afc60-116">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="afc60-117">此外，請參閱：</span><span class="sxs-lookup"><span data-stu-id="afc60-117">Also, review:</span></span>
    - [<span data-ttu-id="afc60-118">Azure Functions HTTP 和 Webhook 繫結</span><span class="sxs-lookup"><span data-stu-id="afc60-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="afc60-119">如何 tooconfigure Azure 函式應用程式設定</span><span class="sxs-lookup"><span data-stu-id="afc60-119">How tooconfigure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="afc60-120">考量</span><span class="sxs-lookup"><span data-stu-id="afc60-120">Considerations</span></span>

-  <span data-ttu-id="afc60-121">Azure hello 耗用量計劃之下執行的函式具有 5 分鐘逾時限制。</span><span class="sxs-lookup"><span data-stu-id="afc60-121">Azure Functions running under hello Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="afc60-122">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="afc60-122">Create a function app</span></span>

1. <span data-ttu-id="afc60-123">移 toohello [Azure 入口網站](http://portal.azure.com)和使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="afc60-123">Go toohello [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="afc60-124">如[這裡](../azure-functions/functions-create-function-app-portal.md)所述建立函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="afc60-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="afc60-125">您在 hello 中指定的儲存體帳戶**StorageConnection**環境變數 （請參閱 hello 下一個步驟） 應該在 hello 與您的應用程式相同的區域。</span><span class="sxs-lookup"><span data-stu-id="afc60-125">A storage account that you specify in hello **StorageConnection** environment variable (see hello next step) should be in hello same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="afc60-126">設定函式應用程式設定</span><span class="sxs-lookup"><span data-stu-id="afc60-126">Configure function app settings</span></span>

<span data-ttu-id="afc60-127">開發媒體服務函式，很方便 tooadd 將在整個函式的環境變數。</span><span class="sxs-lookup"><span data-stu-id="afc60-127">When developing Media Services functions, it is handy tooadd environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="afc60-128">tooconfigure 應用程式設定，請按一下 hello 設定應用程式設定] 連結。</span><span class="sxs-lookup"><span data-stu-id="afc60-128">tooconfigure app settings, click hello Configure App Settings link.</span></span> <span data-ttu-id="afc60-129">如需詳細資訊，請參閱[如何 tooconfigure Azure 函式應用程式設定](../azure-functions/functions-how-to-use-azure-function-app-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="afc60-129">For more information, see  [How tooconfigure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="afc60-130">例如：</span><span class="sxs-lookup"><span data-stu-id="afc60-130">For example:</span></span>

![設定](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="afc60-132">hello 定義函式，在本文中，假設您擁有 hello 遵循您的應用程式設定中的環境變數：</span><span class="sxs-lookup"><span data-stu-id="afc60-132">hello function, defined in this article, assumes you have hello following environment variables in your app settings:</span></span>

<span data-ttu-id="afc60-133">**AMSAccount**：AMS 帳戶名稱 (例如 testams)</span><span class="sxs-lookup"><span data-stu-id="afc60-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="afc60-134">**AMSKey**：AMS 帳戶金鑰 (例如 IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span><span class="sxs-lookup"><span data-stu-id="afc60-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="afc60-135">**MediaServicesStorageAccountName**：儲存體帳戶名稱 (例如 testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="afc60-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="afc60-136">**MediaServicesStorageAccountKey**：儲存體帳戶金鑰 (例如 xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span><span class="sxs-lookup"><span data-stu-id="afc60-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="afc60-137">**StorageConnection**：儲存體連接 (例如 DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span><span class="sxs-lookup"><span data-stu-id="afc60-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="afc60-138">建立函式</span><span class="sxs-lookup"><span data-stu-id="afc60-138">Create a function</span></span>

<span data-ttu-id="afc60-139">部署函式應用程式之後，您可以在**應用程式服務** Azure Functions 中找到它。</span><span class="sxs-lookup"><span data-stu-id="afc60-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="afc60-140">選取您的函式應用程式，然後按一下 [新增函式]。</span><span class="sxs-lookup"><span data-stu-id="afc60-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="afc60-141">選擇 hello **C#**語言和**資料處理**案例。</span><span class="sxs-lookup"><span data-stu-id="afc60-141">Choose hello **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="afc60-142">選擇 [BlobTrigger] 範本。</span><span class="sxs-lookup"><span data-stu-id="afc60-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="afc60-143">此函式將會觸發，每當 blob 上傳到 hello**輸入**容器。</span><span class="sxs-lookup"><span data-stu-id="afc60-143">This function will be triggered whenever a blob is uploaded into hello **input** container.</span></span> <span data-ttu-id="afc60-144">hello**輸入**名稱指定在 hello**路徑**，hello 下一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="afc60-144">hello **input** name is specified in hello **Path**, in hello next step.</span></span>

    ![檔案](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="afc60-146">一旦您選取**BlobTrigger**，某些更多的控制會出現在 hello] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="afc60-146">Once you select **BlobTrigger**, some more controls will appear on hello page.</span></span>

    ![檔案](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="afc60-148">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="afc60-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="afc60-149">檔案</span><span class="sxs-lookup"><span data-stu-id="afc60-149">Files</span></span>

<span data-ttu-id="afc60-150">您的 Azure 函式會與本節所述的程式碼檔案和其他檔案相關聯。</span><span class="sxs-lookup"><span data-stu-id="afc60-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="afc60-151">根據預設，函式會與 **function.json** 和 **run.csx** (C#) 檔案相關聯。</span><span class="sxs-lookup"><span data-stu-id="afc60-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="afc60-152">您將需要 tooadd **project.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="afc60-152">You will need tooadd a **project.json** file.</span></span> <span data-ttu-id="afc60-153">hello 本節其餘部分會顯示 hello 定義，這些檔案。</span><span class="sxs-lookup"><span data-stu-id="afc60-153">hello rest of this section shows hello definitions for these files.</span></span>

![檔案](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="afc60-155">function.json</span><span class="sxs-lookup"><span data-stu-id="afc60-155">function.json</span></span>

<span data-ttu-id="afc60-156">hello function.json 檔案定義 hello 函式繫結和其他組態設定。</span><span class="sxs-lookup"><span data-stu-id="afc60-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="afc60-157">hello runtime 使用這個檔案 toodetermine hello 事件 toomonitor 和如何 toopass 資料到傳回的資料，從函式執行。</span><span class="sxs-lookup"><span data-stu-id="afc60-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="afc60-158">如需詳細資訊，請參閱 [Azure Functions HTTP 和 Webhook 繫結](../azure-functions/functions-reference.md#function-code)。</span><span class="sxs-lookup"><span data-stu-id="afc60-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="afc60-159">設定 hello**停用**屬性太**true** tooprevent hello 函式不會執行。</span><span class="sxs-lookup"><span data-stu-id="afc60-159">Set hello **disabled** property too**true** tooprevent hello function from being executed.</span></span> 


<span data-ttu-id="afc60-160">以下是 **function.json** 檔案的範例。</span><span class="sxs-lookup"><span data-stu-id="afc60-160">Here is an example of **function.json** file.</span></span>

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a><span data-ttu-id="afc60-161">project.json</span><span class="sxs-lookup"><span data-stu-id="afc60-161">project.json</span></span>

<span data-ttu-id="afc60-162">hello project.json 檔案包含相依性。</span><span class="sxs-lookup"><span data-stu-id="afc60-162">hello project.json file contains dependencies.</span></span> <span data-ttu-id="afc60-163">以下是範例**project.json**從 Nuget 封裝檔案，其中包含所需的 hello.NET Azure Media Services。</span><span class="sxs-lookup"><span data-stu-id="afc60-163">Here is an example of **project.json** file that includes hello required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="afc60-164">請注意，hello 版本號碼會變更與最新的更新 toohello 封裝，因此您應該確認 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="afc60-164">Note that hello version numbers will change with latest updates toohello packages, so you should confirm hello most recent versions.</span></span> 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a><span data-ttu-id="afc60-165">run.csx</span><span class="sxs-lookup"><span data-stu-id="afc60-165">run.csx</span></span>

<span data-ttu-id="afc60-166">這是您的函式的 hello C# 程式碼。</span><span class="sxs-lookup"><span data-stu-id="afc60-166">This is hello C# code for your function.</span></span>  <span data-ttu-id="afc60-167">hello 函式定義監視器下方名為儲存體帳戶容器**輸入**（這是 hello 路徑中指定） 的新 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="afc60-167">hello function defined below monitors a storage account container named **input** (that is what was specified in hello path) for new MP4 files.</span></span> <span data-ttu-id="afc60-168">一旦檔案放入 hello 儲存體容器，hello blob 觸發程序會執行 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="afc60-168">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>
    
<span data-ttu-id="afc60-169">此區段中定義的 hello 範例將示範</span><span class="sxs-lookup"><span data-stu-id="afc60-169">hello example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="afc60-170">tooingest 到 Media Services 資產 （藉由複製 blob 到 AMS 資產） 的帳戶和</span><span class="sxs-lookup"><span data-stu-id="afc60-170">how tooingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="afc60-171">如何 toosubmit 編碼工作使用媒體編碼程式標準的 「 自動調整 Streaming 」 預設。</span><span class="sxs-lookup"><span data-stu-id="afc60-171">how toosubmit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="afc60-172">在 hello 真實生活案例中，您很可能會想 tootrack 工作進度，，然後發行您編碼的資產。</span><span class="sxs-lookup"><span data-stu-id="afc60-172">In hello real life scenario, you most likely want tootrack job progress and then publish your encoded asset.</span></span> <span data-ttu-id="afc60-173">如需詳細資訊，請參閱[使用 Azure Webhook toomonitor Media Services 工作通知](media-services-dotnet-check-job-progress-with-webhooks.md)。</span><span class="sxs-lookup"><span data-stu-id="afc60-173">For more information, see [Use Azure WebHooks toomonitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="afc60-174">如需詳細資訊，請參閱[媒體服務 Azure Functions (英文)](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)。</span><span class="sxs-lookup"><span data-stu-id="afc60-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="afc60-175">當您完成定義之後，按一下 [儲存並執行]。</span><span class="sxs-lookup"><span data-stu-id="afc60-175">Once you are done defining your function click **Save and Run**.</span></span>

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get hello destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of hello destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a><span data-ttu-id="afc60-176">測試您的函式</span><span class="sxs-lookup"><span data-stu-id="afc60-176">Test your function</span></span>

<span data-ttu-id="afc60-177">tootest 您的函式，您需要的 MP4 檔案到 hello tooupload**輸入**hello hello 連接字串中指定的儲存體帳戶的容器。</span><span class="sxs-lookup"><span data-stu-id="afc60-177">tootest your function, you need tooupload an MP4 file into hello **input** container of hello storage account that you specified in hello connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="afc60-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="afc60-178">Next step</span></span>

<span data-ttu-id="afc60-179">此時，您就準備好 toostart 開發媒體服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="afc60-179">At this point, you are ready toostart developing a Media Services application.</span></span> 
 
<span data-ttu-id="afc60-180">如需詳細資料與完整範例/解決方案 Azure Media Services toocreate 自訂內容建立工作流程搭配使用 Azure 函式和邏輯應用程式，請參閱 hello[媒體服務.NET 函式整合 GitHub 上的範例](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="afc60-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services toocreate custom content creation workflows, see hello [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="afc60-181">此外，請參閱[使用 Azure Webhook toomonitor Media Services 工作通知使用.NET](media-services-dotnet-check-job-progress-with-webhooks.md)。</span><span class="sxs-lookup"><span data-stu-id="afc60-181">Also, see [Use Azure WebHooks toomonitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="afc60-182">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="afc60-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="afc60-183">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="afc60-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

