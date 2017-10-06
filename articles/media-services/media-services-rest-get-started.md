---
title: "將內容傳送隨選使用 REST 入門 aaaGet |Microsoft 文件"
description: "本教學課程會引導您實作上的要求內容傳遞應用程式透過 Azure Media Services 使用 REST API 的 hello 步驟。"
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
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="d403b-103">使用 REST 傳遞點播內容入門</span><span class="sxs-lookup"><span data-stu-id="d403b-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="d403b-104">本快速入門將引導您完成 hello 步驟實作 Video-on-Demand (VoD) 傳遞內容的應用程式，使用 Azure 媒體服務 (AMS) REST Api。</span><span class="sxs-lookup"><span data-stu-id="d403b-104">This quickstart walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="d403b-105">hello 教學課程介紹 hello 基本 Media Services 工作流程和 hello 最常見的程式設計物件，以及 Media Services 開發所需的工作。</span><span class="sxs-lookup"><span data-stu-id="d403b-105">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="d403b-106">在 hello 完成 hello 教學課程，您將會是能 toostream 或漸進式下載範例媒體檔案，您可以上傳、 編碼，以及下載。</span><span class="sxs-lookup"><span data-stu-id="d403b-106">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="d403b-107">hello 下圖顯示一些最常用的 hello 物件開發 VoD 針對 hello 媒體服務 OData 模型的應用程式時。</span><span class="sxs-lookup"><span data-stu-id="d403b-107">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="d403b-108">按一下 hello 映像 tooview 它的完整大小。</span><span class="sxs-lookup"><span data-stu-id="d403b-108">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="d403b-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="d403b-109">Prerequisites</span></span>
<span data-ttu-id="d403b-110">hello 下列必要條件是必要的 toostart 使用媒體服務 REST api 進行開發。</span><span class="sxs-lookup"><span data-stu-id="d403b-110">hello following prerequisites are required toostart developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="d403b-111">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d403b-111">An Azure account.</span></span> <span data-ttu-id="d403b-112">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d403b-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d403b-113">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="d403b-113">A Media Services account.</span></span> <span data-ttu-id="d403b-114">toocreate Media Services 帳戶，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="d403b-114">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d403b-115">了解如何使用媒體服務 REST API toodevelop。</span><span class="sxs-lookup"><span data-stu-id="d403b-115">Understanding of how toodevelop with Media Services REST API.</span></span> <span data-ttu-id="d403b-116">如需詳細資訊，請參閱[媒體服務 REST API 概觀](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="d403b-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="d403b-117">由您選擇可以傳送 HTTP 要求和回應的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d403b-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="d403b-118">本教學課程使用 [Fiddler](http://www.telerik.com/download/fiddler)。</span><span class="sxs-lookup"><span data-stu-id="d403b-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="d403b-119">本快速入門中，會顯示 hello 下列工作。</span><span class="sxs-lookup"><span data-stu-id="d403b-119">hello following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="d403b-120">啟動串流端點 （使用 hello Azure 入口網站）。</span><span class="sxs-lookup"><span data-stu-id="d403b-120">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="d403b-121">使用 REST API 連接 toohello Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d403b-121">Connect toohello Media Services account with REST API.</span></span>
3. <span data-ttu-id="d403b-122">使用 REST API 建立新資產並上傳視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="d403b-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="d403b-123">Hello 來源檔案編碼成一組彈性位元速率 MP4 檔案使用 REST API。</span><span class="sxs-lookup"><span data-stu-id="d403b-123">Encode hello source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="d403b-124">發佈 hello 資產和取得資料流及使用 REST API 的漸進式下載 Url。</span><span class="sxs-lookup"><span data-stu-id="d403b-124">Publish hello asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="d403b-125">播放您的內容。</span><span class="sxs-lookup"><span data-stu-id="d403b-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="d403b-126">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="d403b-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d403b-127">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="d403b-127">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d403b-128">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="d403b-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="d403b-129">如需本主題中所用的 AMS REST 實體的詳細資訊，請參閱 [Azure 媒體服務 REST API 參考](/rest/api/media/services/azure-media-services-rest-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="d403b-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="d403b-130">此外，請參閱 [Azure 媒體服務概念](media-services-concepts.md)。</span><span class="sxs-lookup"><span data-stu-id="d403b-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="d403b-131">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="d403b-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d403b-132">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="d403b-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="d403b-133">啟動串流端點使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d403b-133">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="d403b-134">當使用 Azure Media Services hello 最常見的案例的其中一個會將視訊透過串流處理的彈性位元速率。</span><span class="sxs-lookup"><span data-stu-id="d403b-134">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="d403b-135">Media Services 提供的動態封裝，可讓您 toodeliver 您彈性位元速率編碼的 MP4 內容串流處理媒體服務 (MPEG DASH、 HLS、 Smooth Streaming) 在 just-in-time，支援不需要您 toostore 預先封裝格式每種串流處理格式的版本。</span><span class="sxs-lookup"><span data-stu-id="d403b-135">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="d403b-136">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="d403b-136">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d403b-137">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="d403b-137">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="d403b-138">toostart hello 串流端點，請執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-138">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="d403b-139">在 hello 登入[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d403b-139">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d403b-140">在 hello 設定視窗中，按一下 串流端點。</span><span class="sxs-lookup"><span data-stu-id="d403b-140">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="d403b-141">按一下 hello 預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="d403b-141">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="d403b-142">hello 預設串流端點詳細資料 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="d403b-142">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="d403b-143">按一下 hello 入門圖示。</span><span class="sxs-lookup"><span data-stu-id="d403b-143">Click hello Start icon.</span></span>
5. <span data-ttu-id="d403b-144">按一下 hello 儲存按鈕 toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="d403b-144">Click hello Save button toosave your changes.</span></span>

## <span data-ttu-id="d403b-145"><a id="connect"></a>使用 REST API 連接 toohello Media Services 帳戶</span><span class="sxs-lookup"><span data-stu-id="d403b-145"><a id="connect"></a>Connect toohello Media Services account with REST API</span></span>

<span data-ttu-id="d403b-146">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d403b-146">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d403b-147">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="d403b-147">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d403b-148">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="d403b-148">You must make subsequent calls toohello new URI.</span></span>

<span data-ttu-id="d403b-149">比方說，如果在嘗試後 tooconnect，您會取得 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d403b-149">For example, if after trying tooconnect, you got hello following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="d403b-150">您應該張貼您後續的 API 呼叫 toohttps://wamsbayclus001rest-hs.cloudapp.net/api/。</span><span class="sxs-lookup"><span data-stu-id="d403b-150">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="d403b-151"><a id="upload"></a>使用 REST API 建立新資產並上傳視訊檔案</span><span class="sxs-lookup"><span data-stu-id="d403b-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="d403b-152">在媒體服務中，您會將數位檔案上傳到到資產。</span><span class="sxs-lookup"><span data-stu-id="d403b-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="d403b-153">hello**資產**實體可以包含視訊、 音訊、 影像、 縮圖集合、 文字播放軌和隱藏式的字幕檔案 （和 hello 中繼資料，這些檔案的相關。）之後 hello 檔案上傳到 hello 資產時，您的內容會安全地儲存在 hello 用於進一步處理和雲端資料流。</span><span class="sxs-lookup"><span data-stu-id="d403b-153">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="d403b-154">建立資產時，有 tooprovide hello 值的其中一個是資產建立選項。</span><span class="sxs-lookup"><span data-stu-id="d403b-154">One of hello values that you have tooprovide when creating an asset is asset creation options.</span></span> <span data-ttu-id="d403b-155">hello**選項**屬性是描述可以建立資產的 hello 加密選項的列舉值。</span><span class="sxs-lookup"><span data-stu-id="d403b-155">hello **Options** property is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="d403b-156">有效的值是從 hello 清單下，此清單中的值組合的 hello 值的其中一個：</span><span class="sxs-lookup"><span data-stu-id="d403b-156">A valid value is one of hello values from hello list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="d403b-157">**None** = **0** - 不使用加密。</span><span class="sxs-lookup"><span data-stu-id="d403b-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="d403b-158">使用此選項時，您的內容在傳輸或儲存體中靜止時不會受到保護。</span><span class="sxs-lookup"><span data-stu-id="d403b-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="d403b-159">如果您計畫使用漸進式下載 toodeliver MP4，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="d403b-159">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="d403b-160">**StorageEncrypted** = **1** -加密您清除的內容，在本機使用 AES 256 位元加密，並將其上傳 tooAzure 儲存體的方式予以儲存加密在靜止。</span><span class="sxs-lookup"><span data-stu-id="d403b-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="d403b-161">使用儲存體加密保護的資產會自動加密，並在 「 加密的檔案系統先前 tooencoding，及選擇性地重新加密的先前 toouploading 回為新輸出資產。</span><span class="sxs-lookup"><span data-stu-id="d403b-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="d403b-162">儲存體加密的 hello 主要使用案例是當您想 toosecure 強式加密在靜止高品質的輸入的媒體檔案在磁碟上。</span><span class="sxs-lookup"><span data-stu-id="d403b-162">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="d403b-163">**CommonEncryptionProtected** = **2** - 如果您要上傳已經使用一般加密或 PlayReady DRM (例如使用 PlayReady DRM 保護的 Smooth Streaming) 加密及保護的內容，請使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="d403b-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="d403b-164">**EnvelopeEncryptionProtected** = **4** – 如果您要上傳使用 AES 加密的 HLS，請使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="d403b-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="d403b-165">hello 檔案必須已編碼並由 Transform Manager 加密。</span><span class="sxs-lookup"><span data-stu-id="d403b-165">hello files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="d403b-166">建立資產</span><span class="sxs-lookup"><span data-stu-id="d403b-166">Create an asset</span></span>
<span data-ttu-id="d403b-167">資產是媒體服務中多種類型或物件集的容器，包括視訊、音訊、影像、縮圖集合、文字播放軌和隱藏式字幕檔案。</span><span class="sxs-lookup"><span data-stu-id="d403b-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="d403b-168">在 hello REST API，建立資產必須傳送 POST 要求 tooMedia 服務和 hello 要求本文中放置關於您資產的任何屬性資訊。</span><span class="sxs-lookup"><span data-stu-id="d403b-168">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="d403b-169">下列範例會示範如何 hello toocreate 資產。</span><span class="sxs-lookup"><span data-stu-id="d403b-169">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="d403b-170">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-170">**HTTP Request**</span></span>

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


<span data-ttu-id="d403b-171">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-171">**HTTP Response**</span></span>

<span data-ttu-id="d403b-172">如果成功，則會傳回 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d403b-172">If successful, hello following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="d403b-173">建立 AssetFile</span><span class="sxs-lookup"><span data-stu-id="d403b-173">Create an AssetFile</span></span>
<span data-ttu-id="d403b-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile)實體代表儲存在 blob 容器的視訊或音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="d403b-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="d403b-175">資產檔案一律會與資產相關聯，資產可包含一或多個 Assetfile。</span><span class="sxs-lookup"><span data-stu-id="d403b-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="d403b-176">如果資產檔案物件不是 blob 容器中的數位檔案相關聯，hello Media Services 編碼器工作會失敗。</span><span class="sxs-lookup"><span data-stu-id="d403b-176">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="d403b-177">您將數位媒體檔案上傳到 blob 容器之後，您會使用 hello**合併**HTTP 要求 tooupdate hello AssetFile 媒體檔案 （如 hello 主題稍後所示） 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d403b-177">After you upload your digital media file into a blob container, you use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span>

<span data-ttu-id="d403b-178">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-178">**HTTP Request**</span></span>

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


<span data-ttu-id="d403b-179">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-179">**HTTP Response**</span></span>

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


### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="d403b-180">建立具有寫入權限的 AccessPolicy hello</span><span class="sxs-lookup"><span data-stu-id="d403b-180">Creating hello AccessPolicy with write permission</span></span>
<span data-ttu-id="d403b-181">將任何檔案上傳到 blob 儲存體之前, 設定 hello 存取原則撰寫 tooan 資產的權限。</span><span class="sxs-lookup"><span data-stu-id="d403b-181">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="d403b-182">toodo 的 POST HTTP 要求 toohello AccessPolicies 實體集。</span><span class="sxs-lookup"><span data-stu-id="d403b-182">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="d403b-183">請在建立時定義 DurationInMinutes 值，否則您會在回應中收到 500 內部伺服器錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d403b-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="d403b-184">如需 AccessPolicies 的詳細資訊，請參閱 [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)。</span><span class="sxs-lookup"><span data-stu-id="d403b-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="d403b-185">下列範例會示範如何 hello toocreate AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="d403b-185">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="d403b-186">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-186">**HTTP Request**</span></span>

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

<span data-ttu-id="d403b-187">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-187">**HTTP Response**</span></span>

<span data-ttu-id="d403b-188">如果成功，則會傳回下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-188">If successful, hello following response is returned:</span></span>

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="d403b-189">取得上傳 URL hello</span><span class="sxs-lookup"><span data-stu-id="d403b-189">Get hello Upload URL</span></span>

<span data-ttu-id="d403b-190">tooreceive hello 實際的上傳 URL，建立 SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="d403b-190">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="d403b-191">定位器會定義要 tooaccess 檔案資產中的用戶端 hello 開始時間和連線端點的型別。</span><span class="sxs-lookup"><span data-stu-id="d403b-191">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="d403b-192">要求與需求時，您便可以建立給定 AccessPolicy 與 Asset 配對 toohandle 不同的用戶端的多個 Locator 實體。</span><span class="sxs-lookup"><span data-stu-id="d403b-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="d403b-193">這些 locator 都會使用 hello StartTime 值加上的時間可以使用 URL hello AccessPolicy toodetermine hello 長度 hello 和 DurationInMinutes 值。</span><span class="sxs-lookup"><span data-stu-id="d403b-193">Each of these Locators uses hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="d403b-194">如需詳細資訊，請參閱 [定位器](https://docs.microsoft.com/rest/api/media/operations/locator)。</span><span class="sxs-lookup"><span data-stu-id="d403b-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="d403b-195">SAS URL 具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-195">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="d403b-196">適用一些考量事項：</span><span class="sxs-lookup"><span data-stu-id="d403b-196">Some considerations apply:</span></span>

* <span data-ttu-id="d403b-197">您一次不能有超過五個唯一定位器與指定的資產相關聯。</span><span class="sxs-lookup"><span data-stu-id="d403b-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="d403b-198">如需詳細資訊，請參閱＜定位器＞。</span><span class="sxs-lookup"><span data-stu-id="d403b-198">For more information, see Locator.</span></span>
* <span data-ttu-id="d403b-199">如果您需要 tooupload 檔案立即，您應該設定您的 StartTime 值 toofive 分鐘，再 hello 目前的時間。</span><span class="sxs-lookup"><span data-stu-id="d403b-199">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="d403b-200">這是因為用戶端電腦與媒體服務之間可能有時間差。</span><span class="sxs-lookup"><span data-stu-id="d403b-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="d403b-201">此外，您的 StartTime 值必須在下列日期時間格式的 hello: YYYY-MM-DDTHH:mm:ssZ (例如，"2014年-05-23T17:53:50Z")。</span><span class="sxs-lookup"><span data-stu-id="d403b-201">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="d403b-202">可能有 30 到 40 秒延遲定位器建立 toowhen 它是可供使用之後。</span><span class="sxs-lookup"><span data-stu-id="d403b-202">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="d403b-203">此問題適用於 SAS URL tooboth 和原始定位器。</span><span class="sxs-lookup"><span data-stu-id="d403b-203">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="d403b-204">如需 SAS 定位器的詳細資訊，請參閱[這個](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)部落格。</span><span class="sxs-lookup"><span data-stu-id="d403b-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="d403b-205">hello 下列範例顯示如何 toocreate SAS URL 定位器，所定義的 hello (如 SAS 定位器為"1") 和"2"的點播原始定位器 hello 要求主體中的類型屬性。</span><span class="sxs-lookup"><span data-stu-id="d403b-205">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="d403b-206">hello**路徑**屬性傳回包含 hello URL，您必須使用 tooupload 您的檔案。</span><span class="sxs-lookup"><span data-stu-id="d403b-206">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="d403b-207">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-207">**HTTP Request**</span></span>

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


<span data-ttu-id="d403b-208">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-208">**HTTP Response**</span></span>

<span data-ttu-id="d403b-209">如果成功，則會傳回下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-209">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="d403b-210">將檔案上傳至 blob 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="d403b-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="d403b-211">一旦您擁有 hello AccessPolicy 與 Locator 組，hello 實際的檔案是使用 hello Azure Storage REST Api 上傳的 tooan Azure blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="d403b-211">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure blob storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="d403b-212">您必須將 hello 檔案上傳為區塊 blob。</span><span class="sxs-lookup"><span data-stu-id="d403b-212">You must upload hello files as block blobs.</span></span> <span data-ttu-id="d403b-213">「Azure 媒體服務」不支援分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="d403b-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="d403b-214">您必須新增 hello 檔案名稱 hello 檔案中，您想 tooupload toohello 定位器**路徑**收到 hello 前一節中的值。</span><span class="sxs-lookup"><span data-stu-id="d403b-214">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="d403b-215">例如，https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="d403b-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="d403b-216">.</span><span class="sxs-lookup"><span data-stu-id="d403b-216">.</span></span> <span data-ttu-id="d403b-217">.</span><span class="sxs-lookup"><span data-stu-id="d403b-217">.</span></span> <span data-ttu-id="d403b-218">.</span><span class="sxs-lookup"><span data-stu-id="d403b-218">.</span></span>
>
>

<span data-ttu-id="d403b-219">如需使用 Azure 儲存體 blob 的詳細資訊，請參閱 [Blob 服務 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)。</span><span class="sxs-lookup"><span data-stu-id="d403b-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="d403b-220">更新 AssetFile hello</span><span class="sxs-lookup"><span data-stu-id="d403b-220">Update hello AssetFile</span></span>
<span data-ttu-id="d403b-221">既然您已上傳您的檔案，更新 hello FileAsset 大小 （及其他） 資訊。</span><span class="sxs-lookup"><span data-stu-id="d403b-221">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="d403b-222">例如：</span><span class="sxs-lookup"><span data-stu-id="d403b-222">For example:</span></span>

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


<span data-ttu-id="d403b-223">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-223">**HTTP Response**</span></span>

<span data-ttu-id="d403b-224">如果成功，則會傳回 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d403b-224">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="d403b-225">刪除 hello Locator 和 AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="d403b-225">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="d403b-226">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="d403b-227">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-227">**HTTP Response**</span></span>

<span data-ttu-id="d403b-228">如果成功，則會傳回 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d403b-228">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="d403b-229">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="d403b-230">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-230">**HTTP Response**</span></span>

<span data-ttu-id="d403b-231">如果成功，則會傳回 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d403b-231">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="d403b-232"><a id="encode"></a>Hello 原始程式檔編碼一組彈性位元速率 MP4 檔案</span><span class="sxs-lookup"><span data-stu-id="d403b-232"><a id="encode"></a>Encode hello source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="d403b-233">之前之後擷取到 Media Services，媒體資產可以編碼、 轉碼多工處理，浮水印等，它會傳遞 tooclients。</span><span class="sxs-lookup"><span data-stu-id="d403b-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="d403b-234">這些活動均已排程，並針對多種背景角色執行個體 tooensure 高效能、 可用性執行。</span><span class="sxs-lookup"><span data-stu-id="d403b-234">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="d403b-235">這些活動稱為作業和每個工作是不可部分完成的工作，請勿 hello hello 資產檔案上的實際工作所組成 (如需詳細資訊，請參閱[作業](/rest/api/media/services/job)，[工作](/rest/api/media/services/task)描述)。</span><span class="sxs-lookup"><span data-stu-id="d403b-235">These activities are called Jobs and each Job is composed of atomic Tasks that do hello actual work on hello Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="d403b-236">如已稍早所述，當使用 Azure Media Services 一個 hello 最常見的案例提供自動調整位元速率串流 tooyour 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d403b-236">As was mentioned earlier, when working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="d403b-237">Media Services 可以動態封裝成 hello 下列格式的其中一個的一組彈性位元速率 MP4 檔案： HTTP Live Streaming (HLS)，Smooth Streaming、 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="d403b-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="d403b-238">hello 下列區段會顯示如何 toocreate 之作業中包含一種編碼工作。</span><span class="sxs-lookup"><span data-stu-id="d403b-238">hello following section shows how toocreate a job that contains one encoding task.</span></span> <span data-ttu-id="d403b-239">hello 工作指定 tootranscode hello 夾層檔為彈性位元速率 mp4 集使用一組**媒體編碼器標準**。</span><span class="sxs-lookup"><span data-stu-id="d403b-239">hello task specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="d403b-240">hello > 一節也會示範如何 toomonitor hello 工作處理進度。</span><span class="sxs-lookup"><span data-stu-id="d403b-240">hello section also shows how toomonitor hello job processing progress.</span></span> <span data-ttu-id="d403b-241">Hello 工作完成時，您都可以 toocreate 定位器屬於所需的 tooget 存取 tooyour 資產。</span><span class="sxs-lookup"><span data-stu-id="d403b-241">When hello job is complete, you would be able toocreate locators that are needed tooget access tooyour assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="d403b-242">取得媒體處理器</span><span class="sxs-lookup"><span data-stu-id="d403b-242">Get a media processor</span></span>
<span data-ttu-id="d403b-243">在媒體服務中，媒體處理器是可處理特定處理工作的元件，例如編碼、格式轉換、加密或解密媒體內容。</span><span class="sxs-lookup"><span data-stu-id="d403b-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="d403b-244">Hello 編碼工作顯示在本教學課程，我們 toouse hello 媒體編碼器標準。</span><span class="sxs-lookup"><span data-stu-id="d403b-244">For hello encoding task shown in this tutorial, we are going toouse hello Media Encoder Standard.</span></span>

<span data-ttu-id="d403b-245">下列程式碼要求 hello 編碼器的識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="d403b-245">hello following code requests hello encoder's id.</span></span>

<span data-ttu-id="d403b-246">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="d403b-247">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-247">**HTTP Response**</span></span>

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

### <a name="create-a-job"></a><span data-ttu-id="d403b-248">建立工作</span><span class="sxs-lookup"><span data-stu-id="d403b-248">Create a job</span></span>
<span data-ttu-id="d403b-249">每個工作可以有一個或更多的工作，根據 hello 類型處理您想 tooaccomplish。</span><span class="sxs-lookup"><span data-stu-id="d403b-249">Each Job can have one or more Tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="d403b-250">透過 hello REST API，您可以建立工作和其相關的工作中有兩種： 工作可以透過 hello 工作導覽屬性上作業的實體，或透過 OData 批次處理內嵌定義。</span><span class="sxs-lookup"><span data-stu-id="d403b-250">Through hello REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through hello Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="d403b-251">hello Media Services SDK 使用批次處理。</span><span class="sxs-lookup"><span data-stu-id="d403b-251">hello Media Services SDK uses batch processing.</span></span> <span data-ttu-id="d403b-252">不過，本主題中的 hello 程式碼範例的 hello 可讀性，工作是內嵌定義。</span><span class="sxs-lookup"><span data-stu-id="d403b-252">However, for hello readability of hello code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="d403b-253">如需批次處理的資訊，請參閱 [開放式資料通訊協定 (OData) 批次處理](http://www.odata.org/documentation/odata-version-3-0/batch-processing/)。</span><span class="sxs-lookup"><span data-stu-id="d403b-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="d403b-254">hello 下列範例會示範如何 toocreate 和 post 作業的一項工作設定 tooencode 視訊在特定的解析度與品質。</span><span class="sxs-lookup"><span data-stu-id="d403b-254">hello following example shows you how toocreate and post a Job with one Task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="d403b-255">下列文件區段的 hello 包含所有 hello hello 清單[工作預設](http://msdn.microsoft.com/library/mt269960)hello 媒體編碼器標準處理器所支援。</span><span class="sxs-lookup"><span data-stu-id="d403b-255">hello following documentation section contains hello list of all hello [task presets](http://msdn.microsoft.com/library/mt269960) supported by hello Media Encoder Standard processor.</span></span>  

<span data-ttu-id="d403b-256">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-256">**HTTP Request**</span></span>

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

<span data-ttu-id="d403b-257">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-257">**HTTP Response**</span></span>

<span data-ttu-id="d403b-258">如果成功，則會傳回下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-258">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="d403b-259">在任何作業要求中有幾項重點 toonote:</span><span class="sxs-lookup"><span data-stu-id="d403b-259">There are a few important things toonote in any Job request:</span></span>

* <span data-ttu-id="d403b-260">TaskBody 屬性必須使用常值的輸入或輸出資產 hello 工作所使用的 XML toodefine hello 數目。</span><span class="sxs-lookup"><span data-stu-id="d403b-260">TaskBody properties MUST use literal XML toodefine hello number of input, or output assets that are used by hello Task.</span></span> <span data-ttu-id="d403b-261">hello 工作主題包含 XML hello XML 結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="d403b-261">hello Task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="d403b-262">在 hello TaskBody 定義中，每個內部值<inputAsset>和<outputAsset>必須設定為 JobInputAsset(value) 或 JobOutputAsset(value)。</span><span class="sxs-lookup"><span data-stu-id="d403b-262">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="d403b-263">每個工作可以有多個輸出資產。</span><span class="sxs-lookup"><span data-stu-id="d403b-263">A task can have multiple output assets.</span></span> <span data-ttu-id="d403b-264">一個 JobOutputAsset(x) 只能使用一次做為工作中的工作輸出。</span><span class="sxs-lookup"><span data-stu-id="d403b-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="d403b-265">您可以指定 JobInputAsset 或 JobOutputAsset 做為工作的輸入資產。</span><span class="sxs-lookup"><span data-stu-id="d403b-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="d403b-266">工作不能形成循環。</span><span class="sxs-lookup"><span data-stu-id="d403b-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="d403b-267">您傳遞 tooJobInputAsset 或 JobOutputAsset 的 hello value 參數代表資產的 hello 索引值。</span><span class="sxs-lookup"><span data-stu-id="d403b-267">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an Asset.</span></span> <span data-ttu-id="d403b-268">hello 實際資產被定義在 hello 工作實體定義的 hello Inputmediaasset 與 Outputmediaasset 導覽屬性中。</span><span class="sxs-lookup"><span data-stu-id="d403b-268">hello actual Assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="d403b-269">因為 Media Services 內建於 OData v3，hello 個別資產 Inputmediaasset 與 Outputmediaasset 導覽屬性集合會透過參考"__metadata: uri"名稱 / 值組。</span><span class="sxs-lookup"><span data-stu-id="d403b-269">Because Media Services is built on OData v3, hello individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="d403b-270">Inputmediaasset 對應 tooone 或您已建立 Media Services 中的多個資產。</span><span class="sxs-lookup"><span data-stu-id="d403b-270">InputMediaAssets maps tooone or more Assets you have created in Media Services.</span></span> <span data-ttu-id="d403b-271">Outputmediaasset 由 hello 系統建立。</span><span class="sxs-lookup"><span data-stu-id="d403b-271">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="d403b-272">它們不會參考現有的資產。</span><span class="sxs-lookup"><span data-stu-id="d403b-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="d403b-273">Outputmediaasset 可以使用 hello assetName 屬性命名。</span><span class="sxs-lookup"><span data-stu-id="d403b-273">OutputMediaAssets can be named using hello assetName attribute.</span></span> <span data-ttu-id="d403b-274">如果這個屬性不存在，則 hello OutputMediaAsset hello 名稱是 hello 任何 hello 內部文字值<outputAsset>項目是與 hello 作業名稱值或 （在 hello hello Name 屬性不定義所在的情況下） 的 hello 作業識別碼值的尾碼。</span><span class="sxs-lookup"><span data-stu-id="d403b-274">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="d403b-275">例如，如果您設定 assetName 的值太 「 範例 」，則 OutputMediaAsset Name 屬性會設定 hello 太"Sample"。</span><span class="sxs-lookup"><span data-stu-id="d403b-275">For example, if you set a value for assetName too"Sample", then hello OutputMediaAsset Name property would be set too"Sample".</span></span> <span data-ttu-id="d403b-276">不過，如果您未設定 assetName 的值，但未設定 hello 工作名稱太"NewJob"，然後 hello OutputMediaAsset Name 將"JobOutputAsset （值） _NewJob"。</span><span class="sxs-lookup"><span data-stu-id="d403b-276">However, if you did not set a value for assetName, but did set hello job name too"NewJob", then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="d403b-277">hello 下列範例顯示如何 tooset hello assetName 屬性：</span><span class="sxs-lookup"><span data-stu-id="d403b-277">hello following example shows how tooset hello assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="d403b-278">tooenable 鏈結工作：</span><span class="sxs-lookup"><span data-stu-id="d403b-278">tooenable task chaining:</span></span>

  * <span data-ttu-id="d403b-279">工作必須有至少 2 個工作</span><span class="sxs-lookup"><span data-stu-id="d403b-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="d403b-280">必須有至少一個工作的輸入是 hello 作業中的另一個工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="d403b-280">There must be at least one task whose input is output of another task in hello job.</span></span>

<span data-ttu-id="d403b-281">如需詳細資訊，請參閱[使用 hello 媒體服務 REST API 建立編碼工作](media-services-rest-encode-asset.md)。</span><span class="sxs-lookup"><span data-stu-id="d403b-281">For more information see, [Creating an Encoding Job with hello Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="d403b-282">監看處理進度</span><span class="sxs-lookup"><span data-stu-id="d403b-282">Monitor Processing Progress</span></span>
<span data-ttu-id="d403b-283">Hello 下列範例所示，您可以使用 hello State 屬性擷取 hello 作業狀態。</span><span class="sxs-lookup"><span data-stu-id="d403b-283">You can retrieve hello Job status by using hello State property, as shown in hello following example.</span></span>

<span data-ttu-id="d403b-284">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="d403b-285">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-285">**HTTP Response**</span></span>

<span data-ttu-id="d403b-286">如果成功，則會傳回下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-286">If successful, hello following response is returned:</span></span>

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


### <a name="cancel-a-job"></a><span data-ttu-id="d403b-287">取消工作</span><span class="sxs-lookup"><span data-stu-id="d403b-287">Cancel a job</span></span>
<span data-ttu-id="d403b-288">Media Services 可讓您 toocancel 透過 hello 利用 CancelJob 函數執行作業。</span><span class="sxs-lookup"><span data-stu-id="d403b-288">Media Services allows you toocancel running jobs through hello CancelJob function.</span></span> <span data-ttu-id="d403b-289">此呼叫會傳回 400 錯誤碼，如果您嘗試 toocancel 當其狀態為已取消的工作、 取消、 錯誤，或完成。</span><span class="sxs-lookup"><span data-stu-id="d403b-289">This call returns a 400 error code if you try toocancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="d403b-290">下列範例會示範如何 hello toocall CancelJob。</span><span class="sxs-lookup"><span data-stu-id="d403b-290">hello following example shows how toocall CancelJob.</span></span>

<span data-ttu-id="d403b-291">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="d403b-292">如果成功，會傳回 204 回應碼且沒有訊息主體。</span><span class="sxs-lookup"><span data-stu-id="d403b-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="d403b-293">您必須進行 URL 編碼 hello 作業識別碼 (當成： somevalue) 時把它中當做參數 tooCancelJob 傳遞。</span><span class="sxs-lookup"><span data-stu-id="d403b-293">You must URL-encode hello job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter tooCancelJob.</span></span>
>
>

### <a name="get-hello-output-asset"></a><span data-ttu-id="d403b-294">取得 hello 輸出資產</span><span class="sxs-lookup"><span data-stu-id="d403b-294">Get hello output asset</span></span>
<span data-ttu-id="d403b-295">hello 下列程式碼會示範如何 toorequest hello 輸出資產識別碼。</span><span class="sxs-lookup"><span data-stu-id="d403b-295">hello following code shows how toorequest hello output asset Id.</span></span>

<span data-ttu-id="d403b-296">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="d403b-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="d403b-297">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="d403b-297">**HTTP Response**</span></span>

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



## <span data-ttu-id="d403b-298"><a id="publish_get_urls"></a>發佈 hello 資產和取得資料流及使用 REST API 的漸進式下載 Url</span><span class="sxs-lookup"><span data-stu-id="d403b-298"><a id="publish_get_urls"></a>Publish hello asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="d403b-299">toostream 或下載資產，您首先需要太 「 發行 」 它藉由建立定位器。</span><span class="sxs-lookup"><span data-stu-id="d403b-299">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="d403b-300">定位器提供存取 toofiles hello 資產中所包含。</span><span class="sxs-lookup"><span data-stu-id="d403b-300">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="d403b-301">Media Services 支援兩種類型的定位器： OnDemandOrigin 定位器，使用的 toostream 媒體 （例如，MPEG DASH、 HLS 或 Smooth Streaming） 和存取簽章 (SAS) 定位器，使用 toodownload 媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="d403b-301">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files.</span></span> <span data-ttu-id="d403b-302">如需 SAS 定位器的詳細資訊，請參閱[這個](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)部落格。</span><span class="sxs-lookup"><span data-stu-id="d403b-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="d403b-303">一旦您建立 hello 定位器時，您可以建立 hello Url 使用的 toostream 或下載您的檔案。</span><span class="sxs-lookup"><span data-stu-id="d403b-303">Once you create hello locators, you can build hello URLs that are used toostream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="d403b-304">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="d403b-304">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d403b-305">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="d403b-305">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="d403b-306">Smooth Streaming 的串流 URL 具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-306">A streaming URL for Smooth Streaming has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="d403b-307">HLS 的串流 URL 具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-307">A streaming URL for HLS has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="d403b-308">適用於 MPEG DASH 串流 URL 具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-308">A streaming URL for MPEG DASH has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="d403b-309">使用 SAS URL toodownload 檔案具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-309">A SAS URL used toodownload files has hello following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="d403b-310">本節說明影響 tooperform hello 下列工作需要太 「 發行 」 您的資產。</span><span class="sxs-lookup"><span data-stu-id="d403b-310">This section shows how tooperform hello following tasks necessary too"publish" your assets.</span></span>  

* <span data-ttu-id="d403b-311">建立具有讀取權限的 AccessPolicy hello</span><span class="sxs-lookup"><span data-stu-id="d403b-311">Creating hello AccessPolicy with read permission</span></span>
* <span data-ttu-id="d403b-312">建立下載內容用的 SAS URL</span><span class="sxs-lookup"><span data-stu-id="d403b-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="d403b-313">建立串流內容用的原始 URL</span><span class="sxs-lookup"><span data-stu-id="d403b-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-hello-accesspolicy-with-read-permission"></a><span data-ttu-id="d403b-314">建立具有讀取權限的 AccessPolicy hello</span><span class="sxs-lookup"><span data-stu-id="d403b-314">Creating hello AccessPolicy with read permission</span></span>
<span data-ttu-id="d403b-315">然後再下載或串流任何媒體內容，先定義具有讀取權限的 AccessPolicy，並建立 hello 適當的 Locator 實體，指定 hello 類型的傳遞機制想 tooenable 為用戶端。</span><span class="sxs-lookup"><span data-stu-id="d403b-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create hello appropriate Locator entity that specifies hello type of delivery mechanism you want tooenable for your clients.</span></span> <span data-ttu-id="d403b-316">如需有關可用 hello 屬性的詳細資訊，請參閱[AccessPolicy 實體屬性](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties)。</span><span class="sxs-lookup"><span data-stu-id="d403b-316">For more information on hello properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="d403b-317">hello 下列範例顯示如何 toospecify hello 指定之資產的讀取權限的 AccessPolicy。</span><span class="sxs-lookup"><span data-stu-id="d403b-317">hello following example shows how toospecify hello AccessPolicy for read permissions for a given Asset.</span></span>

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

<span data-ttu-id="d403b-318">如果成功，會傳回 201 成功碼，描述您所建立的 hello AccessPolicy 實體。</span><span class="sxs-lookup"><span data-stu-id="d403b-318">If successful, a 201 success code is returned describing hello AccessPolicy entity that you created.</span></span> <span data-ttu-id="d403b-319">然後，您可以使用在 hello AccessPolicy Id 與 hello hello 資產，其中包含您想要 toodeliver （例如輸出資產） toocreate hello Locator 實體的 hello 檔案資產識別碼。</span><span class="sxs-lookup"><span data-stu-id="d403b-319">You then use hello AccessPolicy Id along with hello Asset Id of hello asset that contains hello file you want toodeliver(such as an output asset) toocreate hello Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="d403b-320">此基本工作流程是 hello 與上傳檔案時擷取資產 （如已稍早在本主題中所討論） 相同。</span><span class="sxs-lookup"><span data-stu-id="d403b-320">This basic workflow is hello same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="d403b-321">此外，例如上傳檔案，如果您 （或您的用戶端） 需要 tooaccess 檔案立即，設定您的 StartTime 值 toofive 分鐘，再 hello 目前的時間。</span><span class="sxs-lookup"><span data-stu-id="d403b-321">Also, like uploading files, if you (or your clients) need tooaccess your files immediately, set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="d403b-322">這個動作是必要的因為可能有時鐘誤差 hello 用戶端與 Media Services 之間。</span><span class="sxs-lookup"><span data-stu-id="d403b-322">This action is necessary because there may be clock skew between hello client and Media Services.</span></span> <span data-ttu-id="d403b-323">hello StartTime 值必須在下列日期時間格式的 hello: YYYY-MM-DDTHH:mm:ssZ (例如，"2014年-05-23T17:53:50Z")。</span><span class="sxs-lookup"><span data-stu-id="d403b-323">hello StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="d403b-324">建立下載內容用的 SAS URL</span><span class="sxs-lookup"><span data-stu-id="d403b-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="d403b-325">hello，下列程式碼顯示如何 tooget 可以是使用的 toodownload 媒體檔案的 URL 建立和上傳先前。</span><span class="sxs-lookup"><span data-stu-id="d403b-325">hello following code shows how tooget a URL that can be used toodownload a media file created and uploaded previously.</span></span> <span data-ttu-id="d403b-326">hello AccessPolicy 具有讀取權限集，然後 hello 定位器路徑 tooa SAS 下載 URL。</span><span class="sxs-lookup"><span data-stu-id="d403b-326">hello AccessPolicy has read permissions set and hello Locator path refers tooa SAS download URL.</span></span>

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

<span data-ttu-id="d403b-327">如果成功，則會傳回下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-327">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="d403b-328">傳回的 hello**路徑**屬性包含 hello SAS URL。</span><span class="sxs-lookup"><span data-stu-id="d403b-328">hello returned **Path** property contains hello SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="d403b-329">如果您下載儲存體加密內容，您就必須手動將其解密才能呈現，，或使用的 hello 中處理工作 toooutput Storage Decryption mediaprocessor 安全處理 hello 清除 tooan OutputAsset 中的檔案，然後從該資產下載。</span><span class="sxs-lookup"><span data-stu-id="d403b-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use hello Storage Decryption MediaProcessor in a processing task toooutput processed files in hello clear tooan OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="d403b-330">如需有關處理的詳細資訊，請參閱使用 hello 媒體服務 REST API 建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="d403b-330">For more information on processing, see Creating an Encoding Job with hello Media Services REST API.</span></span> <span data-ttu-id="d403b-331">此外，已建立 SAS URL 定位器之後，無法更新它們。</span><span class="sxs-lookup"><span data-stu-id="d403b-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="d403b-332">例如，您無法重複使用 hello 與更新的 StartTime 值相同的定位器。</span><span class="sxs-lookup"><span data-stu-id="d403b-332">For example, you cannot reuse hello same Locator with an updated StartTime value.</span></span> <span data-ttu-id="d403b-333">這是因為建立 SAS Url 的 hello 方式。</span><span class="sxs-lookup"><span data-stu-id="d403b-333">This is because of hello way SAS URLs are created.</span></span> <span data-ttu-id="d403b-334">如果您想要 tooaccess 資產下載定位器過期之後，您必須建立一個新使用新的 StartTime。</span><span class="sxs-lookup"><span data-stu-id="d403b-334">If you want tooaccess an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="d403b-335">下載檔案</span><span class="sxs-lookup"><span data-stu-id="d403b-335">Download files</span></span>
<span data-ttu-id="d403b-336">一旦您擁有 hello AccessPolicy 與 Locator 集，您可以使用下載檔案 hello Azure Storage REST Api。</span><span class="sxs-lookup"><span data-stu-id="d403b-336">Once you have hello AccessPolicy and Locator set, you can download files using hello Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="d403b-337">您必須新增 hello 檔案名稱 hello 檔案中，您想 toodownload toohello 定位器**路徑**收到 hello 前一節中的值。</span><span class="sxs-lookup"><span data-stu-id="d403b-337">You must add hello file name for hello file you want toodownload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="d403b-338">例如，https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="d403b-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="d403b-339">.</span><span class="sxs-lookup"><span data-stu-id="d403b-339">.</span></span> <span data-ttu-id="d403b-340">.</span><span class="sxs-lookup"><span data-stu-id="d403b-340">.</span></span> <span data-ttu-id="d403b-341">.</span><span class="sxs-lookup"><span data-stu-id="d403b-341">.</span></span>
>
>

<span data-ttu-id="d403b-342">如需使用 Azure 儲存體 blob 的詳細資訊，請參閱 [Blob 服務 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)。</span><span class="sxs-lookup"><span data-stu-id="d403b-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="d403b-343">Hello 編碼您稍早執行的作業 （編碼成自動調整 MP4 組），因為您有多個，您可以漸進式下載 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="d403b-343">As a result of hello encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="d403b-344">例如：</span><span class="sxs-lookup"><span data-stu-id="d403b-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="d403b-345">建立串流內容用的串流 URL</span><span class="sxs-lookup"><span data-stu-id="d403b-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="d403b-346">hello 下列程式碼會示範如何 toocreate 串流的 URL 定位器：</span><span class="sxs-lookup"><span data-stu-id="d403b-346">hello following code shows how toocreate a streaming URL Locator:</span></span>

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

<span data-ttu-id="d403b-347">如果成功，則會傳回下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="d403b-347">If successful, hello following response is returned:</span></span>

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

<span data-ttu-id="d403b-348">toostream Smooth Streaming 原始 URL，在串流媒體播放器，您必須將附加的 hello Smooth Streaming 資訊清單檔案，後面接"/manifest"hello 名稱 hello 路徑屬性。</span><span class="sxs-lookup"><span data-stu-id="d403b-348">toostream a Smooth Streaming origin URL in a streaming media player, you must append hello Path property with hello name of hello Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="d403b-349">toostream HLS，附加 (格式 = m3u8 aapl) hello 後"接 /manifest"。</span><span class="sxs-lookup"><span data-stu-id="d403b-349">toostream HLS, append (format=m3u8-aapl) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="d403b-350">toostream MPEG DASH 附加 (格式 = mpd-時間-csf) hello 後"接 /manifest"。</span><span class="sxs-lookup"><span data-stu-id="d403b-350">toostream MPEG DASH, append (format=mpd-time-csf) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="d403b-351"><a id="play"></a>播放您的內容</span><span class="sxs-lookup"><span data-stu-id="d403b-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="d403b-352">視訊，您使用 toostream [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="d403b-352">toostream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="d403b-353">tootest 漸進式下載，將 URL 貼到瀏覽器 （例如，IE、 Chrome、 Safari）。</span><span class="sxs-lookup"><span data-stu-id="d403b-353">tootest progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="d403b-354">後續步驟：媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="d403b-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d403b-355">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d403b-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
