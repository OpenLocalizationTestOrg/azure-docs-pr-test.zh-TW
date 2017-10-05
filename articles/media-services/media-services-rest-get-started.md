---
title: "使用 REST 傳遞點播內容入門 | Microsoft Docs"
description: "本教學課程會帶您逐步完成使用 REST API 實作含 Azure 媒體服務的點播內容傳遞應用程式。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f304f7671465862123f64c8b0f9af95a7c828cc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="de601-103">使用 REST 傳遞點播內容入門</span><span class="sxs-lookup"><span data-stu-id="de601-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="de601-104">本快速入門將逐步引導您使用 REST API 完成利用 Azure 媒體服務 (AMS) 來實作點播視訊 (VoD) 內容傳遞應用程式。</span><span class="sxs-lookup"><span data-stu-id="de601-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="de601-105">教學課程中介紹基本的媒體服務工作流程，以及媒體服務開發最常用的程式設計物件和必要工作。</span><span class="sxs-lookup"><span data-stu-id="de601-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="de601-106">完成本教學課程時，您將能夠串流或漸進式下載您已上傳、編碼和下載的範例媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="de601-106">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="de601-107">下列影像顯示針對媒體服務 OData 模型開發 VoD 應用程式時一些最常用的物件。</span><span class="sxs-lookup"><span data-stu-id="de601-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="de601-108">按一下影像可以完整大小檢視。</span><span class="sxs-lookup"><span data-stu-id="de601-108">Click the image to view it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="de601-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="de601-109">Prerequisites</span></span>
<span data-ttu-id="de601-110">需要下列必要條件，才能開始使用 REST API 用媒體服務進行開發。</span><span class="sxs-lookup"><span data-stu-id="de601-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="de601-111">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="de601-111">An Azure account.</span></span> <span data-ttu-id="de601-112">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="de601-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="de601-113">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="de601-113">A Media Services account.</span></span> <span data-ttu-id="de601-114">若要建立媒體服務帳戶，請參閱[如何建立媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="de601-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="de601-115">了解如何使用媒體服務 REST API 進行開發。</span><span class="sxs-lookup"><span data-stu-id="de601-115">Understanding of how to develop with Media Services REST API.</span></span> <span data-ttu-id="de601-116">如需詳細資訊，請參閱[媒體服務 REST API 概觀](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="de601-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="de601-117">由您選擇可以傳送 HTTP 要求和回應的應用程式。</span><span class="sxs-lookup"><span data-stu-id="de601-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="de601-118">本教學課程使用 [Fiddler](http://www.telerik.com/download/fiddler)。</span><span class="sxs-lookup"><span data-stu-id="de601-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="de601-119">本快速入門會顯示下列工作。</span><span class="sxs-lookup"><span data-stu-id="de601-119">The following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="de601-120">啟動串流端點 (使用 Azure 入口網站)。</span><span class="sxs-lookup"><span data-stu-id="de601-120">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="de601-121">使用 REST API 連接到媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="de601-121">Connect to the Media Services account with REST API.</span></span>
3. <span data-ttu-id="de601-122">使用 REST API 建立新資產並上傳視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="de601-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="de601-123">使用 REST API 將來源檔案編碼為一組調適性位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="de601-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="de601-124">使用 REST API 發行資產及取得串流和漸進式下載 URL。</span><span class="sxs-lookup"><span data-stu-id="de601-124">Publish the asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="de601-125">播放您的內容。</span><span class="sxs-lookup"><span data-stu-id="de601-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="de601-126">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="de601-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="de601-127">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="de601-127">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="de601-128">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="de601-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="de601-129">如需本主題中所用的 AMS REST 實體的詳細資訊，請參閱 [Azure 媒體服務 REST API 參考](/rest/api/media/services/azure-media-services-rest-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="de601-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="de601-130">此外，請參閱 [Azure 媒體服務概念](media-services-concepts.md)。</span><span class="sxs-lookup"><span data-stu-id="de601-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="de601-131">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="de601-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="de601-132">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="de601-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="de601-133">使用 Azure 入口網站開始串流端點</span><span class="sxs-lookup"><span data-stu-id="de601-133">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="de601-134">使用 Azure 媒體服務時，其中一個最常見的案例是透過自適性串流提供影片。</span><span class="sxs-lookup"><span data-stu-id="de601-134">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="de601-135">媒體服務提供動態封裝，這讓您以媒體服務即時支援的串流格式 (MPEG DASH、HLS、Smooth Streaming) 提供自適性 MP4 編碼內容，而不必儲存這些串流格式個別的預先封裝版本。</span><span class="sxs-lookup"><span data-stu-id="de601-135">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="de601-136">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="de601-136">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="de601-137">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="de601-137">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="de601-138">若要啟動串流端點，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="de601-138">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="de601-139">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="de601-139">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="de601-140">在 [設定] 視窗中，按一下 [串流端點]。</span><span class="sxs-lookup"><span data-stu-id="de601-140">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="de601-141">按一下預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="de601-141">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="de601-142">[預設串流端點詳細資料] 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="de601-142">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="de601-143">按一下 [啟動] 圖示。</span><span class="sxs-lookup"><span data-stu-id="de601-143">Click the Start icon.</span></span>
5. <span data-ttu-id="de601-144">按一下 [儲存] 按鈕以儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="de601-144">Click the Save button to save your changes.</span></span>

## <span data-ttu-id="de601-145"><a id="connect"></a>使用 REST API 連接到媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="de601-145"><a id="connect"></a>Connect to the Media Services account with REST API</span></span>

<span data-ttu-id="de601-146">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="de601-146">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="de601-147">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="de601-147">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="de601-148">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="de601-148">You must make subsequent calls to the new URI.</span></span>

<span data-ttu-id="de601-149">例如，如果您在嘗試進行連接之後得到下列結果：</span><span class="sxs-lookup"><span data-stu-id="de601-149">For example, if after trying to connect, you got the following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="de601-150">您應該將後續的 API 呼叫張貼到 https://wamsbayclus001rest-hs.cloudapp.net/api/。</span><span class="sxs-lookup"><span data-stu-id="de601-150">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="de601-151"><a id="upload"></a>使用 REST API 建立新資產並上傳視訊檔案</span><span class="sxs-lookup"><span data-stu-id="de601-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="de601-152">在媒體服務中，您會將數位檔案上傳到到資產。</span><span class="sxs-lookup"><span data-stu-id="de601-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="de601-153">**資產**實體可以包含視訊、音訊、影像、縮圖集合、文字播放軌及隱藏式輔助字幕檔案 (以及這些檔案的相關中繼資料)。一旦檔案會上傳到資產，您的內容會安全地儲存在雲端，以便進行進一步的處理和串流。</span><span class="sxs-lookup"><span data-stu-id="de601-153">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="de601-154">您必須建立資產時提供的值是資產建立選項。</span><span class="sxs-lookup"><span data-stu-id="de601-154">One of the values that you have to provide when creating an asset is asset creation options.</span></span> <span data-ttu-id="de601-155">**Options** 屬性是描述可以使用建立資產之加密選項的列舉值。</span><span class="sxs-lookup"><span data-stu-id="de601-155">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="de601-156">有效的值是以下清單的其中一個值，而不是值的組合。</span><span class="sxs-lookup"><span data-stu-id="de601-156">A valid value is one of the values from the list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="de601-157">**None** = **0** - 不使用加密。</span><span class="sxs-lookup"><span data-stu-id="de601-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="de601-158">使用此選項時，您的內容在傳輸或儲存體中靜止時不會受到保護。</span><span class="sxs-lookup"><span data-stu-id="de601-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="de601-159">如果您計劃使用漸進式下載傳遞 MP4，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="de601-159">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="de601-160">**StorageEncrypted** = **1** - 使用 AES-256 位元加密對您的內容進行本機加密，接著上傳到已靜止加密儲存的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="de601-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="de601-161">以儲存體加密保護的資產會自動解除加密並在編碼前放置在加密的檔案系統中，並且會在上傳為新輸出資產之前選擇性地重新編碼。</span><span class="sxs-lookup"><span data-stu-id="de601-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="de601-162">儲存體加密的主要使用案例是讓您可以使用強式加密來保護磁碟中靜止的高品質輸入媒體檔。</span><span class="sxs-lookup"><span data-stu-id="de601-162">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="de601-163">**CommonEncryptionProtected** = **2** - 如果您要上傳已經使用一般加密或 PlayReady DRM (例如使用 PlayReady DRM 保護的 Smooth Streaming) 加密及保護的內容，請使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="de601-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="de601-164">**EnvelopeEncryptionProtected** = **4** – 如果您要上傳使用 AES 加密的 HLS，請使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="de601-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="de601-165">檔案必須已由 Transform Manager 編碼和加密。</span><span class="sxs-lookup"><span data-stu-id="de601-165">The files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="de601-166">建立資產</span><span class="sxs-lookup"><span data-stu-id="de601-166">Create an asset</span></span>
<span data-ttu-id="de601-167">資產是媒體服務中多種類型或物件集的容器，包括視訊、音訊、影像、縮圖集合、文字播放軌和隱藏式字幕檔案。</span><span class="sxs-lookup"><span data-stu-id="de601-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="de601-168">在 REST API 中，建立資產必須傳送 POST 要求給媒體服務，並將關於您資產的任何屬性資訊放在要求主體中。</span><span class="sxs-lookup"><span data-stu-id="de601-168">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="de601-169">下列範例示範如何建立資產。</span><span class="sxs-lookup"><span data-stu-id="de601-169">The following example shows how to create an asset.</span></span>

<span data-ttu-id="de601-170">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-170">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="de601-171">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-171">**HTTP Response**</span></span>

<span data-ttu-id="de601-172">如果成功，則會傳回下列內容：</span><span class="sxs-lookup"><span data-stu-id="de601-172">If successful, the following is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="de601-173">建立 AssetFile</span><span class="sxs-lookup"><span data-stu-id="de601-173">Create an AssetFile</span></span>
<span data-ttu-id="de601-174">[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 實體代表儲存在 blob 容器中的視訊或音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="de601-174">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="de601-175">資產檔案一律會與資產相關聯，資產可包含一或多個 Assetfile。</span><span class="sxs-lookup"><span data-stu-id="de601-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="de601-176">如果資產檔案物件並未與 blob 容器中的數位檔案相關聯，媒體服務編碼器工作將會失敗。</span><span class="sxs-lookup"><span data-stu-id="de601-176">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="de601-177">您將數位媒體檔案上傳至 blob 容器之後，您將使用 **MERGE** HTTP 要求，以媒體檔案的相關資訊來更新 AssetFile (如本主題稍後所示)。</span><span class="sxs-lookup"><span data-stu-id="de601-177">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span>

<span data-ttu-id="de601-178">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-178">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="de601-179">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-179">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="de601-180">建立具有寫入權限的 AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="de601-180">Creating the AccessPolicy with write permission</span></span>
<span data-ttu-id="de601-181">將任何檔案上傳到 blob 儲存體之前，請設定寫入資產的存取原則權限。</span><span class="sxs-lookup"><span data-stu-id="de601-181">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="de601-182">若要這樣做，請 POST HTTP 要求到 AccessPolicies 實體集。</span><span class="sxs-lookup"><span data-stu-id="de601-182">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="de601-183">請在建立時定義 DurationInMinutes 值，否則您會在回應中收到 500 內部伺服器錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="de601-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="de601-184">如需 AccessPolicies 的詳細資訊，請參閱 [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)。</span><span class="sxs-lookup"><span data-stu-id="de601-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="de601-185">下列範例示範如何建立 AccessPolicy：</span><span class="sxs-lookup"><span data-stu-id="de601-185">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="de601-186">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-186">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="de601-187">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-187">**HTTP Response**</span></span>

<span data-ttu-id="de601-188">如果成功，則會傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="de601-188">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-the-upload-url"></a><span data-ttu-id="de601-189">取得上傳 URL</span><span class="sxs-lookup"><span data-stu-id="de601-189">Get the Upload URL</span></span>

<span data-ttu-id="de601-190">若要接收實際的上傳 URL，請建立 SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="de601-190">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="de601-191">定位器為想要存取資產中之檔案的用戶端定義連線端點的開始時間和類型。</span><span class="sxs-lookup"><span data-stu-id="de601-191">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="de601-192">您可以為指定的 AccessPolicy 與 Asset 配對建立多個 Locator 實體，以處理不同的用戶端要求與需求。</span><span class="sxs-lookup"><span data-stu-id="de601-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="de601-193">這些 Locator 每個都會使用 StartTime 值加上 AccessPolicy 的 DurationInMinutes 值，以判斷可以使用 URL 的時間長度。</span><span class="sxs-lookup"><span data-stu-id="de601-193">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="de601-194">如需詳細資訊，請參閱 [定位器](https://docs.microsoft.com/rest/api/media/operations/locator)。</span><span class="sxs-lookup"><span data-stu-id="de601-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="de601-195">SAS URL 具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="de601-195">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="de601-196">適用一些考量事項：</span><span class="sxs-lookup"><span data-stu-id="de601-196">Some considerations apply:</span></span>

* <span data-ttu-id="de601-197">您一次不能有超過五個唯一定位器與指定的資產相關聯。</span><span class="sxs-lookup"><span data-stu-id="de601-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="de601-198">如需詳細資訊，請參閱＜定位器＞。</span><span class="sxs-lookup"><span data-stu-id="de601-198">For more information, see Locator.</span></span>
* <span data-ttu-id="de601-199">如果您需要立即上傳檔案，您應該將 StartTime 值設為目前時間的五分鐘前。</span><span class="sxs-lookup"><span data-stu-id="de601-199">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="de601-200">這是因為用戶端電腦與媒體服務之間可能有時間差。</span><span class="sxs-lookup"><span data-stu-id="de601-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="de601-201">此外，您的 StartTime 值必須是以下日期時間格式：YYYY-MM-DDTHH:mm:ssZ (例如，"2014-05-23T17:53:50Z")。</span><span class="sxs-lookup"><span data-stu-id="de601-201">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="de601-202">建立 Locator 之後到它可供使用時，中間可能會有 30 到 40 秒的延遲。</span><span class="sxs-lookup"><span data-stu-id="de601-202">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="de601-203">此問題同時適用於 SAS URL 與原始定位器。</span><span class="sxs-lookup"><span data-stu-id="de601-203">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="de601-204">如需 SAS 定位器的詳細資訊，請參閱[這個](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)部落格。</span><span class="sxs-lookup"><span data-stu-id="de601-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="de601-205">下列範例會示範如何建立 SAS URL 定位器，如要求主體中的 Type 屬性所定義 ("1" 代表 SAS 定位器，"2" 代表隨選原始定位器)。</span><span class="sxs-lookup"><span data-stu-id="de601-205">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="de601-206">傳回的 **Path** 屬性包含上傳檔案必須使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="de601-206">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="de601-207">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-207">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="de601-208">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-208">**HTTP Response**</span></span>

<span data-ttu-id="de601-209">如果成功，則會傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="de601-209">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="de601-210">將檔案上傳至 blob 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="de601-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="de601-211">一旦設定 AccessPolicy 與 Locator，就會使用「Azure 儲存體 REST API」將實際檔案上傳到 Azure Blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="de601-211">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="de601-212">您必須將檔案以區塊 Blob 形式上傳。</span><span class="sxs-lookup"><span data-stu-id="de601-212">You must upload the files as block blobs.</span></span> <span data-ttu-id="de601-213">「Azure 媒體服務」不支援分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="de601-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="de601-214">您必須將要上傳的檔案名稱新增到上一節中所收到的 Locator **Path** 值。</span><span class="sxs-lookup"><span data-stu-id="de601-214">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="de601-215">例如，https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="de601-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="de601-216">.</span><span class="sxs-lookup"><span data-stu-id="de601-216">.</span></span> <span data-ttu-id="de601-217">.</span><span class="sxs-lookup"><span data-stu-id="de601-217">.</span></span> <span data-ttu-id="de601-218">.</span><span class="sxs-lookup"><span data-stu-id="de601-218">.</span></span>
>
>

<span data-ttu-id="de601-219">如需使用 Azure 儲存體 blob 的詳細資訊，請參閱 [Blob 服務 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)。</span><span class="sxs-lookup"><span data-stu-id="de601-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="de601-220">更新 AssetFile</span><span class="sxs-lookup"><span data-stu-id="de601-220">Update the AssetFile</span></span>
<span data-ttu-id="de601-221">現在，您已上傳您的檔案，請更新 FileAsset 大小 (及其他) 資訊。</span><span class="sxs-lookup"><span data-stu-id="de601-221">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="de601-222">例如：</span><span class="sxs-lookup"><span data-stu-id="de601-222">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="de601-223">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-223">**HTTP Response**</span></span>

<span data-ttu-id="de601-224">如果成功，則會傳回下列內容：</span><span class="sxs-lookup"><span data-stu-id="de601-224">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="de601-225">刪除 Locator 和 AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="de601-225">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="de601-226">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="de601-227">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-227">**HTTP Response**</span></span>

<span data-ttu-id="de601-228">如果成功，則會傳回下列內容：</span><span class="sxs-lookup"><span data-stu-id="de601-228">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="de601-229">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="de601-230">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-230">**HTTP Response**</span></span>

<span data-ttu-id="de601-231">如果成功，則會傳回下列內容：</span><span class="sxs-lookup"><span data-stu-id="de601-231">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="de601-232"><a id="encode"></a>將來源檔案編碼為一組調適性位元速率 MP4 檔案</span><span class="sxs-lookup"><span data-stu-id="de601-232"><a id="encode"></a>Encode the source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="de601-233">將資產內嵌到媒體服務之後，可以先將媒體編碼、轉碼多工處理、加上浮水印等，再傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="de601-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="de601-234">這些活動會針對多個背景角色執行個體排定和執行，以確保高效能與可用性。</span><span class="sxs-lookup"><span data-stu-id="de601-234">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="de601-235">這些活動稱為作業，每個作業包含對資產檔案執行實際工作的不可部分完成的工作 (如需詳細資訊，請參閱[作業](/rest/api/media/services/job)、[工作](/rest/api/media/services/task)說明)。</span><span class="sxs-lookup"><span data-stu-id="de601-235">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="de601-236">如稍早所提及，使用 Azure 媒體服務時，其中一個最常見的案例是將調適性位元速率串流傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="de601-236">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="de601-237">媒體服務可以以下列其中一種格式動態封裝一組自適性 MP4 檔案：HTTP 即時串流 (HLS)、Smooth Streaming 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="de601-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="de601-238">下一節示範如何建立包含一個編碼工作的工作。</span><span class="sxs-lookup"><span data-stu-id="de601-238">The following section shows how to create a job that contains one encoding task.</span></span> <span data-ttu-id="de601-239">此工作指定使用 **媒體編碼器標準**，將夾層檔案轉換為一組調適性位元速率 MP4。</span><span class="sxs-lookup"><span data-stu-id="de601-239">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="de601-240">此節也會示範如何監視工作處理進度。</span><span class="sxs-lookup"><span data-stu-id="de601-240">The section also shows how to monitor the job processing progress.</span></span> <span data-ttu-id="de601-241">工作完成時，您將能夠建立存取資產所需的定位器。</span><span class="sxs-lookup"><span data-stu-id="de601-241">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="de601-242">取得媒體處理器</span><span class="sxs-lookup"><span data-stu-id="de601-242">Get a media processor</span></span>
<span data-ttu-id="de601-243">在媒體服務中，媒體處理器是可處理特定處理工作的元件，例如編碼、格式轉換、加密或解密媒體內容。</span><span class="sxs-lookup"><span data-stu-id="de601-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="de601-244">此教學課程中所示的編碼工作，我們將使用媒體編碼器標準。</span><span class="sxs-lookup"><span data-stu-id="de601-244">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span></span>

<span data-ttu-id="de601-245">下列程式碼要求編碼器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="de601-245">The following code requests the encoder's id.</span></span>

<span data-ttu-id="de601-246">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="de601-247">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-247">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="de601-248">建立工作</span><span class="sxs-lookup"><span data-stu-id="de601-248">Create a job</span></span>
<span data-ttu-id="de601-249">每個工作可以有一或多個工作，視您想要完成的處理類型而定。</span><span class="sxs-lookup"><span data-stu-id="de601-249">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="de601-250">您可以透過 REST API 以兩種方式的其中之一建立工作和其相關工作：工作可以透過 Job 實體上的 Tasks 導覽屬性，或透過 OData 批次處理進行內嵌定義。</span><span class="sxs-lookup"><span data-stu-id="de601-250">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="de601-251">媒體服務 SDK 使用批次處理。</span><span class="sxs-lookup"><span data-stu-id="de601-251">The Media Services SDK uses batch processing.</span></span> <span data-ttu-id="de601-252">不過，為了本主題中的程式碼範例可讀性，工作都是內嵌定義。</span><span class="sxs-lookup"><span data-stu-id="de601-252">However, for the readability of the code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="de601-253">如需批次處理的資訊，請參閱 [開放式資料通訊協定 (OData) 批次處理](http://www.odata.org/documentation/odata-version-3-0/batch-processing/)。</span><span class="sxs-lookup"><span data-stu-id="de601-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="de601-254">下列範例會示範如何建立和張貼工作，並將一個工作設為在特定的解析度與品質將視訊編碼。</span><span class="sxs-lookup"><span data-stu-id="de601-254">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="de601-255">下列文件區段包含媒體編碼器標準處理器支援的所有 [工作預設](http://msdn.microsoft.com/library/mt269960) 清單。</span><span class="sxs-lookup"><span data-stu-id="de601-255">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span></span>  

<span data-ttu-id="de601-256">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-256">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="de601-257">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-257">**HTTP Response**</span></span>

<span data-ttu-id="de601-258">如果成功，則會傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="de601-258">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="de601-259">有任何工作要求中有一些重要事項要注意：</span><span class="sxs-lookup"><span data-stu-id="de601-259">There are a few important things to note in any Job request:</span></span>

* <span data-ttu-id="de601-260">TaskBody 屬性必須使用 XML 常值來定義工作所使用的輸入或輸出資產數目。</span><span class="sxs-lookup"><span data-stu-id="de601-260">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span></span> <span data-ttu-id="de601-261">工作主題包含 XML 的 XML 結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="de601-261">The Task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="de601-262">在 TaskBody 定義中，<inputAsset> 和 <outputAsset> 的每一個內部值必須設定為 JobInputAsset(value) 或 JobOutputAsset(value)。</span><span class="sxs-lookup"><span data-stu-id="de601-262">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="de601-263">每個工作可以有多個輸出資產。</span><span class="sxs-lookup"><span data-stu-id="de601-263">A task can have multiple output assets.</span></span> <span data-ttu-id="de601-264">一個 JobOutputAsset(x) 只能使用一次做為工作中的工作輸出。</span><span class="sxs-lookup"><span data-stu-id="de601-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="de601-265">您可以指定 JobInputAsset 或 JobOutputAsset 做為工作的輸入資產。</span><span class="sxs-lookup"><span data-stu-id="de601-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="de601-266">工作不能形成循環。</span><span class="sxs-lookup"><span data-stu-id="de601-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="de601-267">您傳遞至 JobInputAsset 或 JobOutputAsset 的 value 參數代表資產的索引值。</span><span class="sxs-lookup"><span data-stu-id="de601-267">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span></span> <span data-ttu-id="de601-268">實際資產定義在作業實體定義上的 InputMediaAsset 與 OutputMediaAsset 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="de601-268">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="de601-269">由於媒體服務建置在 OData v3 之上，因此 InputMediaAsset 與 OutputMediaAsset 導覽屬性集合中的個別資產會透過 "__metadata : uri" 名稱 / 值組參考。</span><span class="sxs-lookup"><span data-stu-id="de601-269">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="de601-270">InputMediaAsset 對應至您在媒體服務中建立的一個或多個資產。</span><span class="sxs-lookup"><span data-stu-id="de601-270">InputMediaAssets maps to one or more Assets you have created in Media Services.</span></span> <span data-ttu-id="de601-271">OutputMediaAsset 由系統建立。</span><span class="sxs-lookup"><span data-stu-id="de601-271">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="de601-272">它們不會參考現有的資產。</span><span class="sxs-lookup"><span data-stu-id="de601-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="de601-273">OutputMediaAsset 可以使用 assetName 屬性命名。</span><span class="sxs-lookup"><span data-stu-id="de601-273">OutputMediaAssets can be named using the assetName attribute.</span></span> <span data-ttu-id="de601-274">如果這個屬性不存在，則 OutputMediaAsset 的名稱是 <outputAsset> 元素的任何內部文字值，並且尾碼為工作名稱值或工作識別碼值 (在未定義 Name 屬性的情況下)。</span><span class="sxs-lookup"><span data-stu-id="de601-274">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="de601-275">例如，如果您將 assetName 的值設為 "Sample"，則 OutputMediaAsset Name 屬性會設為 "Sample"。</span><span class="sxs-lookup"><span data-stu-id="de601-275">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span></span> <span data-ttu-id="de601-276">不過，如果您未設定 assetName 的值，但已將工作名稱設為 "NewJob"，則 OutputMediaAsset Name 會是 "JobOutputAsset(value)_NewJob"。</span><span class="sxs-lookup"><span data-stu-id="de601-276">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="de601-277">下列範例示範如何設定 assetName 屬性：</span><span class="sxs-lookup"><span data-stu-id="de601-277">The following example shows how to set the assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="de601-278">啟用工作鏈結：</span><span class="sxs-lookup"><span data-stu-id="de601-278">To enable task chaining:</span></span>

  * <span data-ttu-id="de601-279">工作必須有至少 2 個工作</span><span class="sxs-lookup"><span data-stu-id="de601-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="de601-280">必須有至少一個工作的輸入是工作中另一項工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="de601-280">There must be at least one task whose input is output of another task in the job.</span></span>

<span data-ttu-id="de601-281">如需詳細資訊，請參閱 [使用媒體服務 REST API 建立編碼工作](media-services-rest-encode-asset.md)。</span><span class="sxs-lookup"><span data-stu-id="de601-281">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="de601-282">監看處理進度</span><span class="sxs-lookup"><span data-stu-id="de601-282">Monitor Processing Progress</span></span>
<span data-ttu-id="de601-283">您可以使用 State 屬性擷取工作狀態，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="de601-283">You can retrieve the Job status by using the State property, as shown in the following example.</span></span>

<span data-ttu-id="de601-284">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="de601-285">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-285">**HTTP Response**</span></span>

<span data-ttu-id="de601-286">如果成功，則會傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="de601-286">If successful, the following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="de601-287">取消工作</span><span class="sxs-lookup"><span data-stu-id="de601-287">Cancel a job</span></span>
<span data-ttu-id="de601-288">媒體服務可讓您透過 CancelJob 函式取消正在執行的工作。</span><span class="sxs-lookup"><span data-stu-id="de601-288">Media Services allows you to cancel running jobs through the CancelJob function.</span></span> <span data-ttu-id="de601-289">如果您嘗試取消的工作狀態為已取消、取消中、錯誤或已完成，這項呼叫將傳回 400 錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="de601-289">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="de601-290">下列範例示範如何呼叫 CancelJob。</span><span class="sxs-lookup"><span data-stu-id="de601-290">The following example shows how to call CancelJob.</span></span>

<span data-ttu-id="de601-291">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="de601-292">如果成功，會傳回 204 回應碼且沒有訊息主體。</span><span class="sxs-lookup"><span data-stu-id="de601-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="de601-293">將工作識別碼做為參數傳遞到 CancelJob 時，您必須將工作識別碼進行 URL 編碼 (通常是 nb:jid:UUID: somevalue)。</span><span class="sxs-lookup"><span data-stu-id="de601-293">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span></span>
>
>

### <a name="get-the-output-asset"></a><span data-ttu-id="de601-294">取得輸出資產</span><span class="sxs-lookup"><span data-stu-id="de601-294">Get the output asset</span></span>
<span data-ttu-id="de601-295">下列程式碼示範如何要求輸出資產識別碼。</span><span class="sxs-lookup"><span data-stu-id="de601-295">The following code shows how to request the output asset Id.</span></span>

<span data-ttu-id="de601-296">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="de601-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="de601-297">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="de601-297">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <span data-ttu-id="de601-298"><a id="publish_get_urls"></a>使用 REST API 發行資產及取得串流和漸進式下載 URL</span><span class="sxs-lookup"><span data-stu-id="de601-298"><a id="publish_get_urls"></a>Publish the asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="de601-299">若要串流處理或下載資產，您必須先建立定位器來「發佈」它。</span><span class="sxs-lookup"><span data-stu-id="de601-299">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="de601-300">定位器提供對於資產中包含之檔案的存取。</span><span class="sxs-lookup"><span data-stu-id="de601-300">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="de601-301">媒體服務支援兩種類型的定位器：OnDemandOrigin 定位器，用於串流媒體 (例如，MPEG DASH、HLS 或 Smooth Streaming) 和存取簽章 (SAS) 定位器，用來下載媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="de601-301">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span> <span data-ttu-id="de601-302">如需 SAS 定位器的詳細資訊，請參閱[這個](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)部落格。</span><span class="sxs-lookup"><span data-stu-id="de601-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="de601-303">建立定位器之後，您便可以建立用來串流或下載檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="de601-303">Once you create the locators, you can build the URLs that are used to stream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="de601-304">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="de601-304">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="de601-305">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="de601-305">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="de601-306">Smooth Streaming 的串流 URL 具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="de601-306">A streaming URL for Smooth Streaming has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="de601-307">HLS 的串流 URL 具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="de601-307">A streaming URL for HLS has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="de601-308">MPEG DASH 的串流 URL 具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="de601-308">A streaming URL for MPEG DASH has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="de601-309">用來下載檔案的 SAS URL 具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="de601-309">A SAS URL used to download files has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="de601-310">本節示範如何執行「發佈」您的資產所需的下列工作。</span><span class="sxs-lookup"><span data-stu-id="de601-310">This section shows how to perform the following tasks necessary to "publish" your assets.</span></span>  

* <span data-ttu-id="de601-311">建立具有讀取權限的 AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="de601-311">Creating the AccessPolicy with read permission</span></span>
* <span data-ttu-id="de601-312">建立下載內容用的 SAS URL</span><span class="sxs-lookup"><span data-stu-id="de601-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="de601-313">建立串流內容用的原始 URL</span><span class="sxs-lookup"><span data-stu-id="de601-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-the-accesspolicy-with-read-permission"></a><span data-ttu-id="de601-314">建立具有讀取權限的 AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="de601-314">Creating the AccessPolicy with read permission</span></span>
<span data-ttu-id="de601-315">下載或串流任何媒體內容之前，請先定義具有讀取權限的 AccessPolicy，並建立適當的 Locator 實體，指定您想要為用戶端啟用的傳遞機制類型。</span><span class="sxs-lookup"><span data-stu-id="de601-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span></span> <span data-ttu-id="de601-316">如需可用屬性的詳細資訊，請參閱 [AccessPolicy 實體屬性](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties)。</span><span class="sxs-lookup"><span data-stu-id="de601-316">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="de601-317">下列範例示範如何針對指定資產指定讀取權限的 AccessPolicy。</span><span class="sxs-lookup"><span data-stu-id="de601-317">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="de601-318">如果成功，會傳回 201 成功碼，描述您所建立的 AccessPolicy 實體。</span><span class="sxs-lookup"><span data-stu-id="de601-318">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span></span> <span data-ttu-id="de601-319">然後，您將使用 AccessPolicy 識別碼以及資產的資產識別碼，其中此資產包含您要傳遞 (例如做為輸出資產) 以建立 Locator 實體的檔案。</span><span class="sxs-lookup"><span data-stu-id="de601-319">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="de601-320">這個基本工作流程在擷取資產 時 (如本主題前面所討論) 與上傳檔案相同。</span><span class="sxs-lookup"><span data-stu-id="de601-320">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="de601-321">此外，就像上傳檔案，如果您 (或您的用戶端) 需要立即存取檔案，請將 StartTime 值設定為目前時間之前五分鐘。</span><span class="sxs-lookup"><span data-stu-id="de601-321">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="de601-322">需要進行此動作是因為用戶端電腦與媒體服務之間可能有時間差。</span><span class="sxs-lookup"><span data-stu-id="de601-322">This action is necessary because there may be clock skew between the client and Media Services.</span></span> <span data-ttu-id="de601-323">StartTime 值必須是以下日期時間格式：YYYY-MM-DDTHH:mm:ssZ (例如，"2014-05-23T17:53:50Z")。</span><span class="sxs-lookup"><span data-stu-id="de601-323">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="de601-324">建立下載內容用的 SAS URL</span><span class="sxs-lookup"><span data-stu-id="de601-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="de601-325">下列程式碼示範如何取得可以用來下載先前建立及上傳之媒體檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="de601-325">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span></span> <span data-ttu-id="de601-326">AccessPolicy 具有讀取權限集，而定位器路徑指向 SAS 下載 URL。</span><span class="sxs-lookup"><span data-stu-id="de601-326">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="de601-327">如果成功，則會傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="de601-327">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="de601-328">傳回的 **Path** 屬性包含 SAS URL。</span><span class="sxs-lookup"><span data-stu-id="de601-328">The returned **Path** property contains the SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="de601-329">如果您下載儲存體加密內容，則必須手動將其解密才能呈現，或是在處理工作中使用儲存體解密 MediaProcessor，以純文字將處理的檔案輸出到 OutputAsset，然後從該資產下載。</span><span class="sxs-lookup"><span data-stu-id="de601-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="de601-330">如需有關處理的詳細資訊，請參閱＜使用媒體服務 REST API 建立編碼工作＞。</span><span class="sxs-lookup"><span data-stu-id="de601-330">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span></span> <span data-ttu-id="de601-331">此外，已建立 SAS URL 定位器之後，無法更新它們。</span><span class="sxs-lookup"><span data-stu-id="de601-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="de601-332">例如，您無法以更新的 StartTime 值重複使用相同的定位器。</span><span class="sxs-lookup"><span data-stu-id="de601-332">For example, you cannot reuse the same Locator with an updated StartTime value.</span></span> <span data-ttu-id="de601-333">這是因為建立 SAS URL 的方式。</span><span class="sxs-lookup"><span data-stu-id="de601-333">This is because of the way SAS URLs are created.</span></span> <span data-ttu-id="de601-334">如果您想要在定位器過期之後存取資產以便下載，您必須用新的 StartTime 建立一個新的定位器。</span><span class="sxs-lookup"><span data-stu-id="de601-334">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="de601-335">下載檔案</span><span class="sxs-lookup"><span data-stu-id="de601-335">Download files</span></span>
<span data-ttu-id="de601-336">設定 AccessPolicy 與 Locator 之後，您可以使用 Azure 儲存體 REST API 下載檔案。</span><span class="sxs-lookup"><span data-stu-id="de601-336">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="de601-337">您必須將要下載的檔案名稱新增到前一節中所收到的 Locator **Path** 值。</span><span class="sxs-lookup"><span data-stu-id="de601-337">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="de601-338">例如，https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="de601-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="de601-339">.</span><span class="sxs-lookup"><span data-stu-id="de601-339">.</span></span> <span data-ttu-id="de601-340">.</span><span class="sxs-lookup"><span data-stu-id="de601-340">.</span></span> <span data-ttu-id="de601-341">.</span><span class="sxs-lookup"><span data-stu-id="de601-341">.</span></span>
>
>

<span data-ttu-id="de601-342">如需使用 Azure 儲存體 blob 的詳細資訊，請參閱 [Blob 服務 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)。</span><span class="sxs-lookup"><span data-stu-id="de601-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="de601-343">由於您先前執行的編碼工作 (編碼成自調適性 MP4 集)，您有多個可以漸進式下載的 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="de601-343">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="de601-344">例如：</span><span class="sxs-lookup"><span data-stu-id="de601-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="de601-345">建立串流內容用的串流 URL</span><span class="sxs-lookup"><span data-stu-id="de601-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="de601-346">下列程式碼示範如何建立串流 URL 定位器：</span><span class="sxs-lookup"><span data-stu-id="de601-346">The following code shows how to create a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="de601-347">如果成功，則會傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="de601-347">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="de601-348">若要在串流媒體播放器中串流 Smooth Streaming 原始 URL，您必須在 Path 屬性後附加 Smooth Streaming 資訊清單檔案的名稱，後面再接 "/manifest"。</span><span class="sxs-lookup"><span data-stu-id="de601-348">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="de601-349">若要串流 HLS，請在 "/manifest" 之後附加 (format=m3u8-aapl) 。</span><span class="sxs-lookup"><span data-stu-id="de601-349">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="de601-350">若要串流 MPEG DASH，請在 "/manifest" 之後附加 (format=mpd-time-csf) 。</span><span class="sxs-lookup"><span data-stu-id="de601-350">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="de601-351"><a id="play"></a>播放您的內容</span><span class="sxs-lookup"><span data-stu-id="de601-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="de601-352">若要串流您的視訊，請使用 [Azure 媒體服務播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="de601-352">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="de601-353">若要測試漸進式下載，請將 URL 貼入瀏覽器 (例如，IE、Chrome、Safari)。</span><span class="sxs-lookup"><span data-stu-id="de601-353">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="de601-354">後續步驟：媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="de601-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="de601-355">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="de601-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
