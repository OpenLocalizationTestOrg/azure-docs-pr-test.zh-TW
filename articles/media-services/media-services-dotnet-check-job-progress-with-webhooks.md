---
title: "使用 Azure WebHook 監視 .NET 的媒體服務作業通知 | Microsoft Docs"
description: "了解如何使用 Azure WebHook 來監視媒體服務作業通知。 程式碼範例是以 C# 撰寫，並使用 Media Services SDK for .NET。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a61fe157-81b1-45c1-89f2-224b7ef55869
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/06/2017
ms.author: juliako
ms.openlocfilehash: eaa875a7c78de0b69c81514ea023f9b8bceb2656
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-webhooks-to-monitor-media-services-job-notifications-with-net"></a><span data-ttu-id="5f096-104">使用 Azure WebHook 監視 .NET 的媒體服務作業通知</span><span class="sxs-lookup"><span data-stu-id="5f096-104">Use Azure WebHooks to monitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="5f096-105">執行作業時，您通常需要設法追蹤作業進度。</span><span class="sxs-lookup"><span data-stu-id="5f096-105">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="5f096-106">您可以使用 Azure Webhook 或 [Azure 佇列儲存體](media-services-dotnet-check-job-progress-with-queues.md)來監視媒體服務作業通知。</span><span class="sxs-lookup"><span data-stu-id="5f096-106">You can monitor Media Services job notifications by using Azure Webhooks or [Azure Queue storage](media-services-dotnet-check-job-progress-with-queues.md).</span></span> <span data-ttu-id="5f096-107">本主題說明如何使用 Webhook。</span><span class="sxs-lookup"><span data-stu-id="5f096-107">This topic shows how to work with Webhooks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f096-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="5f096-108">Prerequisites</span></span>

<span data-ttu-id="5f096-109">需要有下列項目，才能完成教學課程：</span><span class="sxs-lookup"><span data-stu-id="5f096-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="5f096-110">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f096-110">An Azure account.</span></span> <span data-ttu-id="5f096-111">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="5f096-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5f096-112">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f096-112">A Media Services account.</span></span> <span data-ttu-id="5f096-113">若要建立媒體服務帳戶，請參閱[如何建立媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="5f096-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="5f096-114">了解[如何使用 Azure Functions](../azure-functions/functions-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5f096-114">Understanding of [how to use Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="5f096-115">另請檢閱 [Azure Functions HTTP 和 Webhook 繫結](../azure-functions/functions-bindings-http-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="5f096-115">Also, review [Azure functions HTTP and webhook bindings](../azure-functions/functions-bindings-http-webhook.md).</span></span>

<span data-ttu-id="5f096-116">本主題說明如何</span><span class="sxs-lookup"><span data-stu-id="5f096-116">This topic shows how to</span></span>

*  <span data-ttu-id="5f096-117">定義自訂來回應 Webhook 的 Azure Function。</span><span class="sxs-lookup"><span data-stu-id="5f096-117">Define an Azure Function that is customized to respond to webhooks.</span></span> 
    
    <span data-ttu-id="5f096-118">在此情況下，當您的編碼作業變更狀態時，媒體服務會觸發 Webhook。</span><span class="sxs-lookup"><span data-stu-id="5f096-118">In this case, the webhook is triggered by Media Services when your encoding job changes status.</span></span> <span data-ttu-id="5f096-119">此函式會接聽來自媒體服務通知的 Webhook 回呼，並在作業完成之後發佈輸出資產。</span><span class="sxs-lookup"><span data-stu-id="5f096-119">The function listens for the webhook call back from Media Services notifications and publishes the output asset once the job finishes.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="5f096-120">繼續之前，請確定您了解 [Azure Functions HTTP 和 Webhook 繫結](../azure-functions/functions-bindings-http-webhook.md)的運作方式。</span><span class="sxs-lookup"><span data-stu-id="5f096-120">Before continuing, make sure you understand how [Azure Functions HTTP and webhook bindings](../azure-functions/functions-bindings-http-webhook.md) work.</span></span>
    >
    
* <span data-ttu-id="5f096-121">將 Webhook 新增至您的編碼工作，並指定這個 Webhook 所回應的 Webhook URL 和秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f096-121">Add a webhook to your encoding task and specify the webhook URL and secret key that this webhook responds to.</span></span> <span data-ttu-id="5f096-122">在如下所示的範例中，建立編碼工作的程式碼是主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f096-122">In the example shown here, the code that creates the encoding task is a console app.</span></span>

## <a name="setting-up-webhook-notification-azure-functions"></a><span data-ttu-id="5f096-123">設定「webhook 通知」Azure 函式</span><span class="sxs-lookup"><span data-stu-id="5f096-123">Setting up "webhook notification" Azure functions</span></span>

<span data-ttu-id="5f096-124">本節的程式碼示範如何實作做為 Webhook 的 Azure Function。</span><span class="sxs-lookup"><span data-stu-id="5f096-124">The code in this section shows an implementation of an Azure function that is a webhook.</span></span> <span data-ttu-id="5f096-125">在此範例中，此函式會接聽來自媒體服務通知的 Webhook 回呼，並在作業完成之後發佈輸出資產。</span><span class="sxs-lookup"><span data-stu-id="5f096-125">In this sample, the function listens for the webhook call back from Media Services notifications and publishes the output asset once the job finishes.</span></span>

<span data-ttu-id="5f096-126">Webhook 預期簽署金鑰 (認證) 會符合您在設定通知端點時所傳遞的金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f096-126">The webhook expects a signing key (credential) to match the one you pass when you configure the notification endpoint.</span></span> <span data-ttu-id="5f096-127">簽署金鑰是 64 位元組的 Base64 編碼值，可用來保護來自 Azure 媒體服務之 WebHook 回呼的安全。</span><span class="sxs-lookup"><span data-stu-id="5f096-127">The signing key is the 64-byte Base64 encoded value that is used to protect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

<span data-ttu-id="5f096-128">在下列程式碼中，**VerifyWebHookRequestSignature** 方法會進行通知訊息的驗證。</span><span class="sxs-lookup"><span data-stu-id="5f096-128">In the following code, the **VerifyWebHookRequestSignature** method does the verification on the notification message.</span></span> <span data-ttu-id="5f096-129">此驗證的目的是確定訊息是由 Azure 媒體服務所傳送，並且未遭到竄改。</span><span class="sxs-lookup"><span data-stu-id="5f096-129">The purpose of this validation is to ensure that the message was sent by Azure Media Services and hasn’t been tampered with.</span></span> <span data-ttu-id="5f096-130">簽章是 Azure Functions 的選擇性選項，因為它具有**程式碼**值，可透過傳輸層安全性 (TLS) 做為查詢參數。</span><span class="sxs-lookup"><span data-stu-id="5f096-130">The signature is optional for Azure functions as it has the **Code** value as a query parameter over Transport Layer Security (TLS).</span></span> 

<span data-ttu-id="5f096-131">您可以在[這裡](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)找到各種媒體服務 .NET Azure 函式的定義 (包括本主題所示的函式)。</span><span class="sxs-lookup"><span data-stu-id="5f096-131">You can find the definition of various Media Services .NET Azure functions (including the one shown in this topic) [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>

<span data-ttu-id="5f096-132">下列程式碼清單會顯示 Azure 函式參數的定義以及與 Azure 函式相關聯的三個檔案︰function.json、project.json 和 run.csx。</span><span class="sxs-lookup"><span data-stu-id="5f096-132">The following code listing shows the definitions of Azure function parameters and three files that are associated with the Azure function: function.json, project.json, and run.csx.</span></span>

### <a name="application-settings"></a><span data-ttu-id="5f096-133">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="5f096-133">Application settings</span></span> 

<span data-ttu-id="5f096-134">下表顯示本節所定義的 Azure 函式所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="5f096-134">The following table shows the parameters that are used by the Azure function defined in this section.</span></span> 

|<span data-ttu-id="5f096-135">名稱</span><span class="sxs-lookup"><span data-stu-id="5f096-135">Name</span></span>|<span data-ttu-id="5f096-136">定義</span><span class="sxs-lookup"><span data-stu-id="5f096-136">Definition</span></span>|<span data-ttu-id="5f096-137">範例</span><span class="sxs-lookup"><span data-stu-id="5f096-137">Example</span></span>| 
|---|---|---|
|<span data-ttu-id="5f096-138">AMSAccount</span><span class="sxs-lookup"><span data-stu-id="5f096-138">AMSAccount</span></span>|<span data-ttu-id="5f096-139">AMS 帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="5f096-139">Your AMS account name.</span></span> |<span data-ttu-id="5f096-140">juliakomediaservices</span><span class="sxs-lookup"><span data-stu-id="5f096-140">juliakomediaservices</span></span>|
|<span data-ttu-id="5f096-141">AMSKey</span><span class="sxs-lookup"><span data-stu-id="5f096-141">AMSKey</span></span> |<span data-ttu-id="5f096-142">AMS 帳戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f096-142">Your AMS account key.</span></span> | <span data-ttu-id="5f096-143">JUWJdDaOHQQqsZeiXZuE76eDt2SO+YMJk25Lghgy2nY=</span><span class="sxs-lookup"><span data-stu-id="5f096-143">JUWJdDaOHQQqsZeiXZuE76eDt2SO+YMJk25Lghgy2nY=</span></span>|
|<span data-ttu-id="5f096-144">MediaServicesStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="5f096-144">MediaServicesStorageAccountName</span></span> |<span data-ttu-id="5f096-145">與 AMS 帳戶相關聯的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="5f096-145">A name of the storage account that is associated with your AMS account.</span></span>| <span data-ttu-id="5f096-146">storagepkeewmg5c3peq</span><span class="sxs-lookup"><span data-stu-id="5f096-146">storagepkeewmg5c3peq</span></span>|
|<span data-ttu-id="5f096-147">MediaServicesStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="5f096-147">MediaServicesStorageAccountKey</span></span> |<span data-ttu-id="5f096-148">與 AMS 帳戶相關聯的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f096-148">A key of the storage account that is associated with your AMS account.</span></span>|
|<span data-ttu-id="5f096-149">SigningKey</span><span class="sxs-lookup"><span data-stu-id="5f096-149">SigningKey</span></span> |<span data-ttu-id="5f096-150">簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f096-150">A signing key.</span></span>| <span data-ttu-id="5f096-151">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span><span class="sxs-lookup"><span data-stu-id="5f096-151">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span></span>|
|<span data-ttu-id="5f096-152">WebHookEndpoint</span><span class="sxs-lookup"><span data-stu-id="5f096-152">WebHookEndpoint</span></span> | <span data-ttu-id="5f096-153">一個 webhook 端點位址。</span><span class="sxs-lookup"><span data-stu-id="5f096-153">A webhook endpoint address.</span></span> | <span data-ttu-id="5f096-154">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==。</span><span class="sxs-lookup"><span data-stu-id="5f096-154">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span></span>|

### <a name="functionjson"></a><span data-ttu-id="5f096-155">function.json</span><span class="sxs-lookup"><span data-stu-id="5f096-155">function.json</span></span>

<span data-ttu-id="5f096-156">function.json 檔案會定義函式繫結和其他組態設定。</span><span class="sxs-lookup"><span data-stu-id="5f096-156">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="5f096-157">執行階段使用此檔案來判斷要監視的事件，以及如何傳入資料並從函式執行傳回資料。</span><span class="sxs-lookup"><span data-stu-id="5f096-157">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> 

    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [
        "post",
        "get",
        "put",
        "update",
        "patch"
          ]
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
    
### <a name="projectjson"></a><span data-ttu-id="5f096-158">project.json</span><span class="sxs-lookup"><span data-stu-id="5f096-158">project.json</span></span>

<span data-ttu-id="5f096-159">project.json 檔案包含相依性。</span><span class="sxs-lookup"><span data-stu-id="5f096-159">The project.json file contains dependencies.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="5f096-160">run.csx</span><span class="sxs-lookup"><span data-stu-id="5f096-160">run.csx</span></span>

<span data-ttu-id="5f096-161">下列 C# 程式碼會顯示做為 Webhook 的 Azure Function 定義。</span><span class="sxs-lookup"><span data-stu-id="5f096-161">The following C# code shows a definition of an Azure function that is a webhook.</span></span> <span data-ttu-id="5f096-162">此函式會接聽來自媒體服務通知的 Webhook 回呼，並在作業完成之後發佈輸出資產。</span><span class="sxs-lookup"><span data-stu-id="5f096-162">The function listens for the webhook call back from Media Services notifications and publishes the output asset once the job finishes.</span></span> 


>[!NOTE]
><span data-ttu-id="5f096-163">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="5f096-163">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="5f096-164">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="5f096-164">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="5f096-165">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="5f096-165">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    ///////////////////////////////////////////////////
    #r "Newtonsoft.Json"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using System.Globalization;
    using Newtonsoft.Json;
    using Microsoft.Azure;
    using System.Net;
    using System.Security.Cryptography;

    internal const string SignatureHeaderKey = "sha256";
    internal const string SignatureHeaderValueTemplate = SignatureHeaderKey + "={0}";
    static string _webHookEndpoint = Environment.GetEnvironmentVariable("WebHookEndpoint");
    static string _signingKey = Environment.GetEnvironmentVariable("SigningKey");
    static string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    static string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static CloudMediaContext _context = null;

    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

        Task<byte[]> taskForRequestBody = req.Content.ReadAsByteArrayAsync();
        byte[] requestBody = await taskForRequestBody;

        string jsonContent = await req.Content.ReadAsStringAsync();
        log.Info($"Request Body = {jsonContent}");

        IEnumerable<string> values = null;
        if (req.Headers.TryGetValues("ms-signature", out values))
        {
        byte[] signingKey = Convert.FromBase64String(_signingKey);
        string signatureFromHeader = values.FirstOrDefault();

        if (VerifyWebHookRequestSignature(requestBody, signatureFromHeader, signingKey))
        {
            string requestMessageContents = Encoding.UTF8.GetString(requestBody);

            NotificationMessage msg = JsonConvert.DeserializeObject<NotificationMessage>(requestMessageContents);

            if (VerifyHeaders(req, msg, log))
            { 
            string newJobStateStr = (string)msg.Properties.Where(j => j.Key == "NewState").FirstOrDefault().Value;
            if (newJobStateStr == "Finished")
            {
                _context = new CloudMediaContext(new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey));

                if(_context!=null)   
                {                        
                string urlForClientStreaming = PublishAndBuildStreamingURLs(msg.Properties["JobId"]);
                log.Info($"URL to the manifest for client streaming using HLS protocol: {urlForClientStreaming}");
                }
            }

            return req.CreateResponse(HttpStatusCode.OK, string.Empty);
            }
            else
            {
            log.Info($"VerifyHeaders failed.");
            return req.CreateResponse(HttpStatusCode.BadRequest, "VerifyHeaders failed.");
            }
        }
        else
        {
            log.Info($"VerifyWebHookRequestSignature failed.");
            return req.CreateResponse(HttpStatusCode.BadRequest, "VerifyWebHookRequestSignature failed.");
        }
        }

        return req.CreateResponse(HttpStatusCode.BadRequest, "Generic Error.");
    }

    private static string PublishAndBuildStreamingURLs(String jobID)
    {
        IJob job = _context.Jobs.Where(j => j.Id == jobID).FirstOrDefault();
        IAsset asset = job.OutputMediaAssets.FirstOrDefault();

        // Create a 30-day readonly access policy. 
        // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
        TimeSpan.FromDays(30),
        AccessPermissions.Read);

        // Create a locator to the streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy,
        DateTime.UtcNow.AddMinutes(-5));


        // Get a reference to the streaming manifest file from the  
        // collection of files in the asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                    EndsWith(".ism")).
                    FirstOrDefault();

        // Create a full URL to the manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest" +  "(format=m3u8-aapl)";
        return urlForClientStreaming;

    }

    private static bool VerifyWebHookRequestSignature(byte[] data, string actualValue, byte[] verificationKey)
    {
        using (var hasher = new HMACSHA256(verificationKey))
        {
        byte[] sha256 = hasher.ComputeHash(data);
        string expectedValue = string.Format(CultureInfo.InvariantCulture, SignatureHeaderValueTemplate, ToHex(sha256));

        return (0 == String.Compare(actualValue, expectedValue, System.StringComparison.Ordinal));
        }
    }

    private static bool VerifyHeaders(HttpRequestMessage req, NotificationMessage msg, TraceWriter log)
    {
        bool headersVerified = false;

        try
        {
        IEnumerable<string> values = null;
        if (req.Headers.TryGetValues("ms-mediaservices-accountid", out values))
        {
            string accountIdHeader = values.FirstOrDefault();
            string accountIdFromMessage = msg.Properties["AccountId"];

            if (0 == string.Compare(accountIdHeader, accountIdFromMessage, StringComparison.OrdinalIgnoreCase))
            {
            headersVerified = true;
            }
            else
            {
            log.Info($"accountIdHeader={accountIdHeader} does not match accountIdFromMessage={accountIdFromMessage}");
            }
        }
        else
        {
            log.Info($"Header ms-mediaservices-accountid not found.");
        }
        }
        catch (Exception e)
        {
        log.Info($"VerifyHeaders hit exception {e}");
        headersVerified = false;
        }

        return headersVerified;
    }

    private static readonly char[] HexLookup = new char[] { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F' };

    /// <summary>
    /// Converts a <see cref="T:byte[]"/> to a hex-encoded string.
    /// </summary>
    private static string ToHex(byte[] data)
    {
        if (data == null)
        {
        return string.Empty;
        }

        char[] content = new char[data.Length * 2];
        int output = 0;
        byte d;
        for (int input = 0; input < data.Length; input++)
        {
        d = data[input];
        content[output++] = HexLookup[d / 0x10];
        content[output++] = HexLookup[d % 0x10];
        }
        return new string(content);
    }

    internal enum NotificationEventType
    {
        None = 0,
        JobStateChange = 1,
        NotificationEndPointRegistration = 2,
        NotificationEndPointUnregistration = 3,
        TaskStateChange = 4,
        TaskProgress = 5
    }
    
    internal sealed class NotificationMessage
    {
        public string MessageVersion { get; set; }
        public string ETag { get; set; }
        public NotificationEventType EventType { get; set; }
        public DateTime TimeStamp { get; set; }
        public IDictionary<string, string> Properties { get; set; }
    }

### <a name="function-output"></a><span data-ttu-id="5f096-166">函式輸出</span><span class="sxs-lookup"><span data-stu-id="5f096-166">Function output</span></span>

<span data-ttu-id="5f096-167">上述範例會產生下列輸出，而您的值可能會不同。</span><span class="sxs-lookup"><span data-stu-id="5f096-167">The example above produced the following output, your values will vary.</span></span>

    C# HTTP trigger function processed a request. RequestUri=https://juliako001-functions.azurewebsites.net/api/Notification_Webhook_Function?code=9376d69kygoy49oft81nel8frty5cme8hb9xsjslxjhalwhfrqd79awz8ic4ieku74dvkdfgvi
    Request Body = {
      "MessageVersion": "1.1",
      "ETag": "b8977308f48858a8f224708bc963e1a09ff917ce730316b4e7ae9137f78f3b20",
      "EventType": 4,
      "TimeStamp": "2017-02-16T03:59:53.3041122Z",
      "Properties": {
        "JobId": "nb:jid:UUID:badd996c-8d7c-4ae0-9bc1-bd7f1902dbdd",
        "TaskId": "nb:tid:UUID:80e26fb9-ee04-4739-abd8-2555dc24639f",
        "NewState": "Finished",
        "OldState": "Processing",
        "AccountName": "mediapkeewmg5c3peq",
        "AccountId": "301912b0-659e-47e0-9bc4-6973f2be3424",
        "NotificationEndPointId": "nb:nepid:UUID:cb5d707b-4db8-45fe-a558-19f8d3306093"
      }
    }
    
    URL to the manifest for client streaming using HLS protocol: http://mediapkeewmg5c3peq.streaming.mediaservices.windows.net/0ac98077-2b58-4db7-a8da-789a13ac6167/BigBuckBunny.ism/manifest(format=m3u8-aapl)

## <a name="adding-webhook-to-your-encoding-task"></a><span data-ttu-id="5f096-168">將 Webhook 新增至您的編碼工作</span><span class="sxs-lookup"><span data-stu-id="5f096-168">Adding Webhook to your encoding task</span></span>

<span data-ttu-id="5f096-169">本節會顯示將 Webhook 通知新增至工作的程式碼。</span><span class="sxs-lookup"><span data-stu-id="5f096-169">In this section, the code that adds a webhook notification to a Task is shown.</span></span> <span data-ttu-id="5f096-170">您也可以新增作業層級通知，這更適用於具有鏈結工作的作業。</span><span class="sxs-lookup"><span data-stu-id="5f096-170">You can also add a job level notification, which would be more useful for a job with chained tasks.</span></span>  

1. <span data-ttu-id="5f096-171">在 Visual Studio 中，建立新的 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f096-171">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="5f096-172">依序輸入 [名稱]、[位置] 和 [方案名稱]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5f096-172">Enter the Name, Location, and Solution name, and then click OK.</span></span>
2. <span data-ttu-id="5f096-173">使用 [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) 來安裝 Azure 媒體服務。</span><span class="sxs-lookup"><span data-stu-id="5f096-173">Use [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) to install Azure Media Services.</span></span>
3. <span data-ttu-id="5f096-174">使用適當的值來更新 App.config 檔案：</span><span class="sxs-lookup"><span data-stu-id="5f096-174">Update App.config file with appropriate values:</span></span> 
    
    * <span data-ttu-id="5f096-175">將用來傳送通知的 Azure 媒體服務名稱和金鑰，</span><span class="sxs-lookup"><span data-stu-id="5f096-175">Azure Media Services name and key that will be sending notifications,</span></span> 
    * <span data-ttu-id="5f096-176">預期會收到通知的 Webhook URL，</span><span class="sxs-lookup"><span data-stu-id="5f096-176">webhook URL that expects to get the notifications,</span></span> 
    * <span data-ttu-id="5f096-177">符合您 Webhook 所預期金鑰的簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f096-177">the signing key that matches the key that your webhook expects.</span></span> <span data-ttu-id="5f096-178">簽署金鑰是 64 位元組的 Base64 編碼值，可用來保護來自 Azure 媒體服務之 WebHook 回呼的安全。</span><span class="sxs-lookup"><span data-stu-id="5f096-178">The signing key is the 64-byte Base64 encoded value that is used to protect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

            <appSettings>
              <add key="MediaServicesAccountName" value="AMSAcctName" />
              <add key="MediaServicesAccountKey" value="AMSAcctKey" />
              <add key="WebhookURL" value="https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>" />
              <add key="WebhookSigningKey" value="j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt" />
            </appSettings>
            
4. <span data-ttu-id="5f096-179">使用下列程式碼來更新 Program.cs 檔案：</span><span class="sxs-lookup"><span data-stu-id="5f096-179">Update your Program.cs file with the following code:</span></span>

        using System;
        using System.Configuration;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace NotificationWebHook
        {
            class Program
            {
            // Read values from the App.config file.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServicesAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServicesAccountKey"];
            private static readonly string _webHookEndpoint =
                ConfigurationManager.AppSettings["WebhookURL"];
            private static readonly string _signingKey =
                 ConfigurationManager.AppSettings["WebhookSigningKey"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {

                // Used the cached credentials to create CloudMediaContext.
                _context = new CloudMediaContext(new MediaServicesCredentials(
                        _mediaServicesAccountName,
                        _mediaServicesAccountKey));

                byte[] keyBytes = Convert.FromBase64String(_signingKey);

                IAsset newAsset = _context.Assets.FirstOrDefault();

                // Check for existing Notification Endpoint with the name "FunctionWebHook"

                var existingEndpoint = _context.NotificationEndPoints.Where(e => e.Name == "FunctionWebHook").FirstOrDefault();
                INotificationEndPoint endpoint = null;

                if (existingEndpoint != null)
                {
                Console.WriteLine("webhook endpoint already exists");
                endpoint = (INotificationEndPoint)existingEndpoint;
                }
                else
                {
                endpoint = _context.NotificationEndPoints.Create("FunctionWebHook",
                    NotificationEndPointType.WebHook, _webHookEndpoint, keyBytes);
                Console.WriteLine("Notification Endpoint Created with Key : {0}", keyBytes.ToString());
                }

                // Declare a new encoding job with the Standard encoder
                IJob job = _context.Jobs.Create("MES Job");

                // Get a media processor reference, and pass to it the name of the 
                // processor to use for the specific task.
                IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.None);

                // Specify the input asset to be encoded.
                task.InputAssets.Add(newAsset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means the output asset is not encrypted. 
                task.OutputAssets.AddNew(newAsset.Name, AssetCreationOptions.None);

                // Add the WebHook notification to this Task and request all notification state changes.
                // Note that you can also add a job level notification
                // which would be more useful for a job with chained tasks.  
                if (endpoint != null)
                {
                task.TaskNotificationSubscriptions.AddNew(NotificationJobState.All, endpoint, true);
                Console.WriteLine("Created Notification Subscription for endpoint: {0}", _webHookEndpoint);
                }
                else
                {
                Console.WriteLine("No Notification Endpoint is being used");
                }

                job.Submit();

                Console.WriteLine("Expect WebHook to be triggered for the Job ID: {0}", job.Id);
                Console.WriteLine("Expect WebHook to be triggered for the Task ID: {0}", task.Id);

                Console.WriteLine("Job Submitted");

            }
            private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                return processor;
            }

            }
        }

## <a name="next-step"></a><span data-ttu-id="5f096-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f096-180">Next step</span></span>
<span data-ttu-id="5f096-181">檢閱媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="5f096-181">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5f096-182">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="5f096-182">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
