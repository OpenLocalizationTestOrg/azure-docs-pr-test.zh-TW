---
title: "使用 REST Media Services 帳戶將 aaaUpload 檔案 |Microsoft 文件"
description: "了解如何 tooget 媒體內容至媒體服務建立和上傳資產。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="46d5d-103">使用 REST 將檔案上傳至媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="46d5d-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46d5d-104">.NET</span><span class="sxs-lookup"><span data-stu-id="46d5d-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="46d5d-105">REST</span><span class="sxs-lookup"><span data-stu-id="46d5d-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="46d5d-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="46d5d-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="46d5d-107">在媒體服務中，您會將數位檔案上傳到到資產。</span><span class="sxs-lookup"><span data-stu-id="46d5d-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="46d5d-108">hello[資產](https://docs.microsoft.com/rest/api/media/operations/asset)實體可以包含視訊、 音訊、 影像、 縮圖集合、 文字播放軌和隱藏式的字幕檔案 （和 hello 中繼資料，這些檔案的相關。）之後 hello 檔案上傳到 hello 資產時，您的內容會安全地儲存在 hello 用於進一步處理和雲端資料流。</span><span class="sxs-lookup"><span data-stu-id="46d5d-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="46d5d-109">hello 下列考量適用於：</span><span class="sxs-lookup"><span data-stu-id="46d5d-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="46d5d-110">Media Services 使用 hello hello IAssetFile.Name 屬性值，當建置 Url 的 hello 串流處理內容 (例如，http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters。)基於這個理由，不允許 percent-encoding。</span><span class="sxs-lookup"><span data-stu-id="46d5d-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="46d5d-111">hello hello 值**名稱**屬性不能有 hello 下列任何一項[百分比編碼的保留字元](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ！ *' （);: @& = + $，/？ %# []"。</span><span class="sxs-lookup"><span data-stu-id="46d5d-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="46d5d-112">此外，只能有一個 '。 ' hello 檔案名稱副檔名。</span><span class="sxs-lookup"><span data-stu-id="46d5d-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="46d5d-113">hello hello 名稱長度不能超過 260 個字元。</span><span class="sxs-lookup"><span data-stu-id="46d5d-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="46d5d-114">沒有支援 Media Services 中的處理限制 toohello 最大檔案大小。</span><span class="sxs-lookup"><span data-stu-id="46d5d-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="46d5d-115">請參閱[這](media-services-quotas-and-limitations.md)hello 檔案大小限制的詳細主題。</span><span class="sxs-lookup"><span data-stu-id="46d5d-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="46d5d-116">hello 上傳資產的基本工作流程分成下列各節的 hello:</span><span class="sxs-lookup"><span data-stu-id="46d5d-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="46d5d-117">建立資產</span><span class="sxs-lookup"><span data-stu-id="46d5d-117">Create an Asset</span></span>
* <span data-ttu-id="46d5d-118">加密資產 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="46d5d-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="46d5d-119">上傳檔案 tooblob 存放裝置</span><span class="sxs-lookup"><span data-stu-id="46d5d-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="46d5d-120">AMS 也可讓您大量 tooupload 資產。</span><span class="sxs-lookup"><span data-stu-id="46d5d-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="46d5d-121">如需詳細資訊，請參閱 [本節](media-services-rest-upload-files.md#upload_in_bulk) 。</span><span class="sxs-lookup"><span data-stu-id="46d5d-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="46d5d-122">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="46d5d-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="46d5d-123">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="46d5d-124">TooMedia 服務連接</span><span class="sxs-lookup"><span data-stu-id="46d5d-124">Connect tooMedia Services</span></span>

<span data-ttu-id="46d5d-125">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="46d5d-126">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="46d5d-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="46d5d-127">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="46d5d-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="46d5d-128">上傳資產</span><span class="sxs-lookup"><span data-stu-id="46d5d-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="46d5d-129">建立資產</span><span class="sxs-lookup"><span data-stu-id="46d5d-129">Create an asset</span></span>

<span data-ttu-id="46d5d-130">資產是媒體服務中多種類型或物件集的容器，包括視訊、音訊、影像、縮圖集合、文字播放軌和隱藏式字幕檔案。</span><span class="sxs-lookup"><span data-stu-id="46d5d-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="46d5d-131">在 hello REST API，建立資產必須傳送 POST 要求 tooMedia 服務和 hello 要求本文中放置關於您資產的任何屬性資訊。</span><span class="sxs-lookup"><span data-stu-id="46d5d-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="46d5d-132">您可以指定當建立資產時的 hello 屬性的其中一個**選項**。</span><span class="sxs-lookup"><span data-stu-id="46d5d-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="46d5d-133">**選項**是描述可以建立資產的 hello 加密選項的列舉值。</span><span class="sxs-lookup"><span data-stu-id="46d5d-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="46d5d-134">有效的值是其中一個 hello 值從 hello 下方的清單，不得為值的組合。</span><span class="sxs-lookup"><span data-stu-id="46d5d-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="46d5d-135">**None** = **0**：將不使用加密。</span><span class="sxs-lookup"><span data-stu-id="46d5d-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="46d5d-136">這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="46d5d-136">This is hello default value.</span></span> <span data-ttu-id="46d5d-137">請注意，使用這個選項時您的內容在傳輸中或在儲存體中不受保護。</span><span class="sxs-lookup"><span data-stu-id="46d5d-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="46d5d-138">如果您計畫使用漸進式下載 toodeliver MP4，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="46d5d-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="46d5d-139">**StorageEncrypted** = **1**： 指定是否要為您的檔案 toobe AES 256 位元加密上, 傳和儲存體加密。</span><span class="sxs-lookup"><span data-stu-id="46d5d-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="46d5d-140">如果您的資產是儲存體加密，必須設定資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="46d5d-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="46d5d-141">如需詳細資訊，請參閱 [設定資產傳遞原則](media-services-rest-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="46d5d-142">**CommonEncryptionProtected** = **2**：如果上傳使用一般加密方法 (例如 PlayReady) 保護的檔案，請指定此值。</span><span class="sxs-lookup"><span data-stu-id="46d5d-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="46d5d-143">**EnvelopeEncryptionProtected** = **4**：如果上傳使用 AES 檔案加密的 HLS，請指定此值。</span><span class="sxs-lookup"><span data-stu-id="46d5d-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="46d5d-144">請注意，hello 檔案必須具有已編碼，並由 Transform Manager 加密。</span><span class="sxs-lookup"><span data-stu-id="46d5d-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="46d5d-145">如果您的資產會使用加密，您必須建立**ContentKey**並連結到 tooyour 資產 hello 下列主題中所述：[如何 toocreate ContentKey](media-services-rest-create-contentkey.md)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="46d5d-146">請注意，您上傳到 hello 資產的 hello 檔案之後，您需要 tooupdate hello 加密內容上 hello **AssetFile** hello 值所得期間 hello 實體**資產**加密。</span><span class="sxs-lookup"><span data-stu-id="46d5d-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="46d5d-147">請勿使用 hello**合併**HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="46d5d-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="46d5d-148">下列範例會示範如何 hello toocreate 資產。</span><span class="sxs-lookup"><span data-stu-id="46d5d-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="46d5d-149">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="46d5d-149">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

<span data-ttu-id="46d5d-150">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-150">**HTTP Response**</span></span>

<span data-ttu-id="46d5d-151">如果成功，則會傳回 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="46d5d-151">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="46d5d-152">建立 AssetFile</span><span class="sxs-lookup"><span data-stu-id="46d5d-152">Create an AssetFile</span></span>
<span data-ttu-id="46d5d-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile)實體代表儲存在 blob 容器的視訊或音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="46d5d-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="46d5d-154">資產檔案一律會與資產相關聯，而資產可包含一或多個資產檔案。</span><span class="sxs-lookup"><span data-stu-id="46d5d-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="46d5d-155">如果資產檔案物件不是 blob 容器中的數位檔案相關聯，hello Media Services 編碼器工作會失敗。</span><span class="sxs-lookup"><span data-stu-id="46d5d-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="46d5d-156">請注意該 hello **AssetFile**執行個體與 hello 實際媒體檔案的兩個相異的物件。</span><span class="sxs-lookup"><span data-stu-id="46d5d-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="46d5d-157">hello AssetFile 執行個體包含 hello 媒體檔案的相關中繼資料，而 hello 媒體檔案包含 hello 實際的媒體內容。</span><span class="sxs-lookup"><span data-stu-id="46d5d-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="46d5d-158">您將數位媒體檔案上傳到 blob 容器之後，您將使用 hello**合併**HTTP 要求 tooupdate hello AssetFile 媒體檔案 （如 hello 主題稍後所示） 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="46d5d-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="46d5d-159">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="46d5d-159">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="46d5d-160">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-160">**HTTP Response**</span></span>

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="46d5d-161">建立 hello AccessPolicy 與寫入權限。</span><span class="sxs-lookup"><span data-stu-id="46d5d-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="46d5d-162">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="46d5d-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="46d5d-163">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="46d5d-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="46d5d-164">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="46d5d-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="46d5d-165">將任何檔案上傳到 blob 儲存體之前, 設定 hello 存取原則撰寫 tooan 資產的權限。</span><span class="sxs-lookup"><span data-stu-id="46d5d-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="46d5d-166">toodo 的 POST HTTP 要求 toohello AccessPolicies 實體集。</span><span class="sxs-lookup"><span data-stu-id="46d5d-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="46d5d-167">請在建立時定義 DurationInMinutes 值，否則您會在回應中收到 500 內部伺服器錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="46d5d-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="46d5d-168">如需 AccessPolicies 的詳細資訊，請參閱 [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="46d5d-169">下列範例會示範如何 hello toocreate AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="46d5d-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="46d5d-170">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="46d5d-170">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="46d5d-171">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="46d5d-171">**HTTP Request**</span></span>

    If successful, hello following response is returned:

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="46d5d-172">取得上傳 URL hello</span><span class="sxs-lookup"><span data-stu-id="46d5d-172">Get hello Upload URL</span></span>
<span data-ttu-id="46d5d-173">tooreceive hello 實際的上傳 URL，建立 SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="46d5d-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="46d5d-174">定位器會定義要 tooaccess 檔案資產中的用戶端 hello 開始時間和連線端點的型別。</span><span class="sxs-lookup"><span data-stu-id="46d5d-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="46d5d-175">要求與需求時，您便可以建立給定 AccessPolicy 與 Asset 配對 toohandle 不同的用戶端的多個 Locator 實體。</span><span class="sxs-lookup"><span data-stu-id="46d5d-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="46d5d-176">這些 locator 都會使用 hello StartTime 值加上的時間可以使用 URL hello AccessPolicy toodetermine hello 長度 hello 和 DurationInMinutes 值。</span><span class="sxs-lookup"><span data-stu-id="46d5d-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="46d5d-177">如需詳細資訊，請參閱 [定位器](https://docs.microsoft.com/rest/api/media/operations/locator)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="46d5d-178">SAS URL 具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="46d5d-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="46d5d-179">適用一些考量事項：</span><span class="sxs-lookup"><span data-stu-id="46d5d-179">Some considerations apply:</span></span>

* <span data-ttu-id="46d5d-180">您一次不能有超過五個唯一定位器與指定的資產相關聯。</span><span class="sxs-lookup"><span data-stu-id="46d5d-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="46d5d-181">如需詳細資訊，請參閱＜定位器＞。</span><span class="sxs-lookup"><span data-stu-id="46d5d-181">For more information, see Locator.</span></span>
* <span data-ttu-id="46d5d-182">如果您需要 tooupload 檔案立即，您應該設定您的 StartTime 值 toofive 分鐘，再 hello 目前的時間。</span><span class="sxs-lookup"><span data-stu-id="46d5d-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="46d5d-183">這是因為用戶端電腦與媒體服務之間可能有時間差。</span><span class="sxs-lookup"><span data-stu-id="46d5d-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="46d5d-184">此外，您的 StartTime 值必須在下列日期時間格式的 hello: YYYY-MM-DDTHH:mm:ssZ (例如，"2014年-05-23T17:53:50Z")。</span><span class="sxs-lookup"><span data-stu-id="46d5d-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="46d5d-185">可能有 30 到 40 秒延遲定位器建立 toowhen 它是可供使用之後。</span><span class="sxs-lookup"><span data-stu-id="46d5d-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="46d5d-186">此問題適用於 SAS URL tooboth 和原始定位器。</span><span class="sxs-lookup"><span data-stu-id="46d5d-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="46d5d-187">hello 下列範例顯示如何 toocreate SAS URL 定位器，所定義的 hello (如 SAS 定位器為"1") 和"2"的點播原始定位器 hello 要求主體中的類型屬性。</span><span class="sxs-lookup"><span data-stu-id="46d5d-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="46d5d-188">hello**路徑**屬性傳回包含 hello URL，您必須使用 tooupload 您的檔案。</span><span class="sxs-lookup"><span data-stu-id="46d5d-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="46d5d-189">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="46d5d-189">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

<span data-ttu-id="46d5d-190">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-190">**HTTP Response**</span></span>

<span data-ttu-id="46d5d-191">如果成功，則會傳回下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="46d5d-191">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="46d5d-192">將檔案上傳至 blob 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="46d5d-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="46d5d-193">一旦您擁有 hello AccessPolicy 與 Locator 組，hello 實際的檔案是使用 hello Azure Storage REST Api 上傳的 tooan Azure Blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="46d5d-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="46d5d-194">您必須將 hello 檔案上傳為區塊 blob。</span><span class="sxs-lookup"><span data-stu-id="46d5d-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="46d5d-195">「Azure 媒體服務」不支援分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="46d5d-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="46d5d-196">您必須新增 hello 檔案名稱 hello 檔案中，您想 tooupload toohello 定位器**路徑**收到 hello 前一節中的值。</span><span class="sxs-lookup"><span data-stu-id="46d5d-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="46d5d-197">例如，https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="46d5d-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="46d5d-198">.</span><span class="sxs-lookup"><span data-stu-id="46d5d-198">.</span></span> <span data-ttu-id="46d5d-199">.</span><span class="sxs-lookup"><span data-stu-id="46d5d-199">.</span></span> <span data-ttu-id="46d5d-200">.</span><span class="sxs-lookup"><span data-stu-id="46d5d-200">.</span></span> 
> 
> 

<span data-ttu-id="46d5d-201">如需使用 Azure 儲存體 blob 的詳細資訊，請參閱 [Blob 服務 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="46d5d-202">更新 AssetFile hello</span><span class="sxs-lookup"><span data-stu-id="46d5d-202">Update hello AssetFile</span></span>
<span data-ttu-id="46d5d-203">既然您已上傳您的檔案，更新 hello FileAsset 大小 （及其他） 資訊。</span><span class="sxs-lookup"><span data-stu-id="46d5d-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="46d5d-204">例如：</span><span class="sxs-lookup"><span data-stu-id="46d5d-204">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="46d5d-205">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-205">**HTTP Response**</span></span>

<span data-ttu-id="46d5d-206">如果成功，hello 下列會傳回： HTTP/1.1 204 沒有內容</span><span class="sxs-lookup"><span data-stu-id="46d5d-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="46d5d-207">刪除 hello Locator 和 AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="46d5d-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="46d5d-208">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="46d5d-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="46d5d-209">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-209">**HTTP Response**</span></span>

<span data-ttu-id="46d5d-210">如果成功，則會傳回 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="46d5d-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="46d5d-211">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="46d5d-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="46d5d-212">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-212">**HTTP Response**</span></span>

<span data-ttu-id="46d5d-213">如果成功，則會傳回 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="46d5d-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="46d5d-214"><a id="upload_in_bulk"></a>上傳大量資產</span><span class="sxs-lookup"><span data-stu-id="46d5d-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="46d5d-215">建立 hello IngestManifest</span><span class="sxs-lookup"><span data-stu-id="46d5d-215">Create hello IngestManifest</span></span>
<span data-ttu-id="46d5d-216">hello IngestManifest 是一組資產、 資產檔案，以及統計資料資訊的容器使用的大量擷取 hello 組 toodetermine hello 進度。</span><span class="sxs-lookup"><span data-stu-id="46d5d-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="46d5d-217">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="46d5d-217">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="46d5d-218">建立資產</span><span class="sxs-lookup"><span data-stu-id="46d5d-218">Create assets</span></span>
<span data-ttu-id="46d5d-219">建立 hello IngestManifestAsset 之前，您會需要 toocreate hello 會使用大量擷取完成的資產。</span><span class="sxs-lookup"><span data-stu-id="46d5d-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="46d5d-220">資產是媒體服務中多種類型或物件集的容器，包括視訊、音訊、影像、縮圖集合、文字播放軌和隱藏式字幕檔案。</span><span class="sxs-lookup"><span data-stu-id="46d5d-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="46d5d-221">Hello REST API，在建立資產必須傳送 HTTP POST 要求 tooMicrosoft Azure Media Services 和 hello 要求本文中放置關於您資產的任何屬性資訊。在此範例中，hello 資產是使用隨附於 hello 要求主體的 hello storageencrption （1） 選項來建立。</span><span class="sxs-lookup"><span data-stu-id="46d5d-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="46d5d-222">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-222">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="46d5d-223">建立 hello Ingestmanifestasset</span><span class="sxs-lookup"><span data-stu-id="46d5d-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="46d5d-224">IngestManifestAssets 代表 IngestManifest 中配合大量內嵌使用的資產。</span><span class="sxs-lookup"><span data-stu-id="46d5d-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="46d5d-225">hello 基本上是連結 hello 資產 toohello 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="46d5d-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="46d5d-226">Azure Media Services 在內部監看 hello 檔案上傳 Ingestmanifestfile 相關聯集合 toohello IngestManifestAsset。</span><span class="sxs-lookup"><span data-stu-id="46d5d-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="46d5d-227">上傳這些檔案，一旦 hello 資產便已完成。</span><span class="sxs-lookup"><span data-stu-id="46d5d-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="46d5d-228">您可以使用 HTTP POST 要求來建立新的 IngestManifestAsset。</span><span class="sxs-lookup"><span data-stu-id="46d5d-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="46d5d-229">在 hello 要求主體中，包括 hello IngestManifest 識別碼與 hello 資產識別碼，IngestManifestAsset 應該連結在一起進行大量擷取的 hello。</span><span class="sxs-lookup"><span data-stu-id="46d5d-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="46d5d-230">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-230">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="46d5d-231">為每個資產建立 hello 的 Ingestmanifestfile</span><span class="sxs-lookup"><span data-stu-id="46d5d-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="46d5d-232">IngestManifestFile 代表實際的視訊或音訊 Blob 物件，將針對資產上傳此物件以做為大量內嵌的一部分。</span><span class="sxs-lookup"><span data-stu-id="46d5d-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="46d5d-233">加密的相關屬性並非必要項，除非 hello 資產使用加密選項。</span><span class="sxs-lookup"><span data-stu-id="46d5d-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="46d5d-234">使用本節中的 hello 範例示範建立 IngestManifestFile 使用 StorageEncryption hello 先前建立的資產。</span><span class="sxs-lookup"><span data-stu-id="46d5d-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="46d5d-235">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-235">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="46d5d-236">上傳 hello 檔案 tooBlob 儲存體</span><span class="sxs-lookup"><span data-stu-id="46d5d-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="46d5d-237">您可以使用任何適當的高速用戶端的應用程式能夠將上傳 hello 資產檔案 toohello blob 儲存體容器 hello hello IngestManifest BlobStorageUriForUpload 屬性所提供的 Uri。</span><span class="sxs-lookup"><span data-stu-id="46d5d-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="46d5d-238">一個著名的高速上傳服務是 [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="46d5d-239">監視大量內嵌進度</span><span class="sxs-lookup"><span data-stu-id="46d5d-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="46d5d-240">您可以監視 hello 大量擷取進度的作業 IngestManifest 藉由輪詢 hello 的 hello IngestManifest 的 Statistics 屬性。</span><span class="sxs-lookup"><span data-stu-id="46d5d-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="46d5d-241">該屬性是複雜類型 [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="46d5d-242">toopoll hello 統計資料屬性送出的 HTTP GET 要求傳送嗨 IngestManifest 識別碼。</span><span class="sxs-lookup"><span data-stu-id="46d5d-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="46d5d-243">建立要用於加密的 ContentKey</span><span class="sxs-lookup"><span data-stu-id="46d5d-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="46d5d-244">如果您的資產會使用加密，您必須建立用於加密資產檔案建立 hello 之前 hello ContentKey toobe。</span><span class="sxs-lookup"><span data-stu-id="46d5d-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="46d5d-245">儲存體加密 hello 下列屬性應該包含 hello 要求主體中。</span><span class="sxs-lookup"><span data-stu-id="46d5d-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="46d5d-246">要求本文屬性</span><span class="sxs-lookup"><span data-stu-id="46d5d-246">Request body property</span></span> | <span data-ttu-id="46d5d-247">說明</span><span class="sxs-lookup"><span data-stu-id="46d5d-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="46d5d-248">識別碼</span><span class="sxs-lookup"><span data-stu-id="46d5d-248">Id</span></span> |<span data-ttu-id="46d5d-249">hello 我們所產生的 ContentKey 識別碼自己使用 hello 下列格式，"nb:<NEW GUID>"。</span><span class="sxs-lookup"><span data-stu-id="46d5d-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="46d5d-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="46d5d-250">ContentKeyType</span></span> |<span data-ttu-id="46d5d-251">這是 hello 內容金鑰類型為此內容金鑰的整數。</span><span class="sxs-lookup"><span data-stu-id="46d5d-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="46d5d-252">我們傳遞儲存體加密的 hello 值 1。</span><span class="sxs-lookup"><span data-stu-id="46d5d-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="46d5d-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="46d5d-253">EncryptedContentKey</span></span> |<span data-ttu-id="46d5d-254">我們會建立新的內容金鑰值，其為 256 位元 (32 位元組) 的值。</span><span class="sxs-lookup"><span data-stu-id="46d5d-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="46d5d-255">使用 hello 儲存加密 X.509 憑證執行 hello GetProtectionKeyId 與 GetProtectionKey 方法的 HTTP GET 要求來擷取從 Microsoft Azure Media Services，hello 金鑰進行加密。</span><span class="sxs-lookup"><span data-stu-id="46d5d-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="46d5d-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="46d5d-256">ProtectionKeyId</span></span> |<span data-ttu-id="46d5d-257">這是我們的內容金鑰 hello hello 儲存加密 X.509 憑證的已使用的 tooencrypt 保護金鑰識別碼。</span><span class="sxs-lookup"><span data-stu-id="46d5d-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="46d5d-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="46d5d-258">ProtectionKeyType</span></span> |<span data-ttu-id="46d5d-259">這是 hello hello 已使用的 tooencrypt hello 內容金鑰的保護金鑰的加密類型。</span><span class="sxs-lookup"><span data-stu-id="46d5d-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="46d5d-260">針對本文範例，此值為 StorageEncryption(1)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="46d5d-261">Checksum</span><span class="sxs-lookup"><span data-stu-id="46d5d-261">Checksum</span></span> |<span data-ttu-id="46d5d-262">hello MD5 計算總和檢查碼 hello 內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="46d5d-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="46d5d-263">會透過加密 hello 內容金鑰的 hello 內容識別碼，以執行計算。</span><span class="sxs-lookup"><span data-stu-id="46d5d-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="46d5d-264">hello 範例程式碼會示範如何 toocalculate hello 總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="46d5d-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="46d5d-265">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-265">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="46d5d-266">連結 hello ContentKey toohello 資產</span><span class="sxs-lookup"><span data-stu-id="46d5d-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="46d5d-267">hello ContentKey 是相關聯的 tooone 或多個資產，藉由傳送 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="46d5d-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="46d5d-268">hello 以下要求是範例 toolink hello 範例 ContentKey toohello 範例資產識別碼。</span><span class="sxs-lookup"><span data-stu-id="46d5d-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="46d5d-269">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-269">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="46d5d-270">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="46d5d-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="46d5d-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46d5d-271">Next steps</span></span>

<span data-ttu-id="46d5d-272">您現在可以將上傳的資產編碼。</span><span class="sxs-lookup"><span data-stu-id="46d5d-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="46d5d-273">如需詳細資訊，請參閱 [為資產編碼](media-services-portal-encode.md)。</span><span class="sxs-lookup"><span data-stu-id="46d5d-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="46d5d-274">您也可以使用 Azure 函式 tootrigger 抵達 hello 設定容器中的檔案為基礎的編碼工作。</span><span class="sxs-lookup"><span data-stu-id="46d5d-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="46d5d-275">如需詳細資訊，請參閱[此範例](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )。</span><span class="sxs-lookup"><span data-stu-id="46d5d-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="46d5d-276">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="46d5d-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="46d5d-277">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="46d5d-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

