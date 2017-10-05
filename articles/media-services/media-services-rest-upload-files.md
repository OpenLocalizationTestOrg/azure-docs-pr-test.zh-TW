---
title: "使用 REST 將檔案上傳至媒體服務帳戶 | Microsoft Docs"
description: "了解如何建立並上傳資產，以將媒體內容移至媒體服務中。"
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
ms.openlocfilehash: 955356ffe6fc524c1528364add7e2c2a336137b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="0044e-103">使用 REST 將檔案上傳至媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="0044e-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0044e-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0044e-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="0044e-105">REST</span><span class="sxs-lookup"><span data-stu-id="0044e-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="0044e-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="0044e-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="0044e-107">在媒體服務中，您會將數位檔案上傳到到資產。</span><span class="sxs-lookup"><span data-stu-id="0044e-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="0044e-108">[資產](https://docs.microsoft.com/rest/api/media/operations/asset)實體可以包含視訊、音訊、影像、縮圖集合、文字播放軌及隱藏式輔助字幕檔案 (以及這些檔案的相關中繼資料)。一旦檔案會上傳到資產，您的內容會安全地儲存在雲端，以便進行進一步的處理和串流。</span><span class="sxs-lookup"><span data-stu-id="0044e-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="0044e-109">您必須考量下列事項：</span><span class="sxs-lookup"><span data-stu-id="0044e-109">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="0044e-110">建置串流內容的 URL (例如，http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters) 時，媒體服務會使用 IAssetFile.Name 屬性的值。基於這個理由，不允許 percent-encoding。</span><span class="sxs-lookup"><span data-stu-id="0044e-110">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="0044e-111">**Name** 屬性的值不能有下列任何[百分比編碼保留字元](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters)：!*'();:@&=+$,/?%#[]"。</span><span class="sxs-lookup"><span data-stu-id="0044e-111">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="0044e-112">而且，副檔名只能有一個 '.'。</span><span class="sxs-lookup"><span data-stu-id="0044e-112">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="0044e-113">名稱長度不應超過 260 個字元。</span><span class="sxs-lookup"><span data-stu-id="0044e-113">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="0044e-114">對於在媒體服務處理檔案，支援的檔案大小有上限。</span><span class="sxs-lookup"><span data-stu-id="0044e-114">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="0044e-115">請參閱[此](media-services-quotas-and-limitations.md)主題，以取得有關檔案大小限制的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0044e-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> 

<span data-ttu-id="0044e-116">上傳資產的基本工作流程分成下列各節：</span><span class="sxs-lookup"><span data-stu-id="0044e-116">The basic workflow for uploading Assets is divided into the following sections:</span></span>

* <span data-ttu-id="0044e-117">建立資產</span><span class="sxs-lookup"><span data-stu-id="0044e-117">Create an Asset</span></span>
* <span data-ttu-id="0044e-118">加密資產 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="0044e-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="0044e-119">將檔案上傳至 blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="0044e-119">Upload a file to blob storage</span></span>

<span data-ttu-id="0044e-120">AMS 也可讓您上傳大量資產。</span><span class="sxs-lookup"><span data-stu-id="0044e-120">AMS also enables you to upload assets in bulk.</span></span> <span data-ttu-id="0044e-121">如需詳細資訊，請參閱 [本節](media-services-rest-upload-files.md#upload_in_bulk) 。</span><span class="sxs-lookup"><span data-stu-id="0044e-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="0044e-122">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="0044e-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="0044e-123">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="0044e-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="0044e-124">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="0044e-124">Connect to Media Services</span></span>

<span data-ttu-id="0044e-125">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="0044e-125">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="0044e-126">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="0044e-126">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0044e-127">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="0044e-127">You must make subsequent calls to the new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="0044e-128">上傳資產</span><span class="sxs-lookup"><span data-stu-id="0044e-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="0044e-129">建立資產</span><span class="sxs-lookup"><span data-stu-id="0044e-129">Create an asset</span></span>

<span data-ttu-id="0044e-130">資產是媒體服務中多種類型或物件集的容器，包括視訊、音訊、影像、縮圖集合、文字播放軌和隱藏式字幕檔案。</span><span class="sxs-lookup"><span data-stu-id="0044e-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="0044e-131">在 REST API 中，建立資產必須傳送 POST 要求給媒體服務，並將關於您資產的任何屬性資訊放在要求主體中。</span><span class="sxs-lookup"><span data-stu-id="0044e-131">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="0044e-132">您可以在建立資產時指定的其中一個屬性是 **Options**。</span><span class="sxs-lookup"><span data-stu-id="0044e-132">One of the properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="0044e-133">**Options** 是列舉值，描述可用來建立資產的加密選項。</span><span class="sxs-lookup"><span data-stu-id="0044e-133">**Options** is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="0044e-134">有效的值是以下清單的其中一個值，而不是值的組合。</span><span class="sxs-lookup"><span data-stu-id="0044e-134">A valid value is one of the values from the list below, not a combination of values.</span></span> 

* <span data-ttu-id="0044e-135">**None** = **0**：將不使用加密。</span><span class="sxs-lookup"><span data-stu-id="0044e-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="0044e-136">這是預設值。</span><span class="sxs-lookup"><span data-stu-id="0044e-136">This is the default value.</span></span> <span data-ttu-id="0044e-137">請注意，使用這個選項時您的內容在傳輸中或在儲存體中不受保護。</span><span class="sxs-lookup"><span data-stu-id="0044e-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="0044e-138">如果您計劃使用漸進式下載傳遞 MP4，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="0044e-138">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="0044e-139">**StorageEncrypted** = **1**：如果要用 AES-256 位元加密來加密您的檔案，以便進行上傳和儲存，請指定此值。</span><span class="sxs-lookup"><span data-stu-id="0044e-139">**StorageEncrypted** = **1**: Specify if you want for your files to be encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="0044e-140">如果您的資產是儲存體加密，必須設定資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="0044e-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="0044e-141">如需詳細資訊，請參閱 [設定資產傳遞原則](media-services-rest-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="0044e-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="0044e-142">**CommonEncryptionProtected** = **2**：如果上傳使用一般加密方法 (例如 PlayReady) 保護的檔案，請指定此值。</span><span class="sxs-lookup"><span data-stu-id="0044e-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="0044e-143">**EnvelopeEncryptionProtected** = **4**：如果上傳使用 AES 檔案加密的 HLS，請指定此值。</span><span class="sxs-lookup"><span data-stu-id="0044e-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="0044e-144">請注意，檔案必須已由 Transform Manager 編碼和加密。</span><span class="sxs-lookup"><span data-stu-id="0044e-144">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="0044e-145">如果您的資產會使用加密，您必須建立 **ContentKey** 並將它連結到您的資產，如下列主題中所述：[如何建立 ContentKey](media-services-rest-create-contentkey.md)。</span><span class="sxs-lookup"><span data-stu-id="0044e-145">If your asset will use encryption, you must create a **ContentKey** and link it to your asset as described in the following topic:[How to create a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="0044e-146">請注意，檔案上傳到資產之後，您必須將 **AssetFile** 實體上的加密屬性更新為在**資產**加密期間得到的值。</span><span class="sxs-lookup"><span data-stu-id="0044e-146">Note that after you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption.</span></span> <span data-ttu-id="0044e-147">請使用 **MERGE** HTTP 要求執行此作業。</span><span class="sxs-lookup"><span data-stu-id="0044e-147">Do it by using the **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="0044e-148">下列範例示範如何建立資產。</span><span class="sxs-lookup"><span data-stu-id="0044e-148">The following example shows how to create an asset.</span></span>

<span data-ttu-id="0044e-149">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="0044e-149">**HTTP Request**</span></span>

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

<span data-ttu-id="0044e-150">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-150">**HTTP Response**</span></span>

<span data-ttu-id="0044e-151">如果成功，則會傳回下列內容：</span><span class="sxs-lookup"><span data-stu-id="0044e-151">If successful, the following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="0044e-152">建立 AssetFile</span><span class="sxs-lookup"><span data-stu-id="0044e-152">Create an AssetFile</span></span>
<span data-ttu-id="0044e-153">[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 實體代表儲存在 blob 容器中的視訊或音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="0044e-153">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="0044e-154">資產檔案一律會與資產相關聯，而資產可包含一或多個資產檔案。</span><span class="sxs-lookup"><span data-stu-id="0044e-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="0044e-155">如果資產檔案物件並未與 blob 容器中的數位檔案相關聯，媒體服務編碼器工作將會失敗。</span><span class="sxs-lookup"><span data-stu-id="0044e-155">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="0044e-156">請注意， **AssetFile** 執行個體和實際的媒體檔案是兩個不同的物件。</span><span class="sxs-lookup"><span data-stu-id="0044e-156">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="0044e-157">AssetFile 執行個體包含媒體檔案的相關中繼資料，而媒體檔案包含實際的媒體內容。</span><span class="sxs-lookup"><span data-stu-id="0044e-157">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="0044e-158">當您將數位媒體檔案上傳至 blob 容器之後，您將使用 **MERGE** HTTP 要求，以媒體檔案的相關資訊來更新 AssetFile (如本主題稍後所示)。</span><span class="sxs-lookup"><span data-stu-id="0044e-158">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span> 

<span data-ttu-id="0044e-159">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="0044e-159">**HTTP Request**</span></span>

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

<span data-ttu-id="0044e-160">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-160">**HTTP Response**</span></span>

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

### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="0044e-161">建立具有寫入權限的 AccessPolicy。</span><span class="sxs-lookup"><span data-stu-id="0044e-161">Creating the AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="0044e-162">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="0044e-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="0044e-163">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="0044e-163">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="0044e-164">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="0044e-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="0044e-165">將任何檔案上傳到 blob 儲存體之前，請設定寫入資產的存取原則權限。</span><span class="sxs-lookup"><span data-stu-id="0044e-165">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="0044e-166">若要這樣做，請 POST HTTP 要求到 AccessPolicies 實體集。</span><span class="sxs-lookup"><span data-stu-id="0044e-166">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="0044e-167">請在建立時定義 DurationInMinutes 值，否則您會在回應中收到 500 內部伺服器錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="0044e-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="0044e-168">如需 AccessPolicies 的詳細資訊，請參閱 [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)。</span><span class="sxs-lookup"><span data-stu-id="0044e-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="0044e-169">下列範例示範如何建立 AccessPolicy：</span><span class="sxs-lookup"><span data-stu-id="0044e-169">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="0044e-170">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="0044e-170">**HTTP Request**</span></span>

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

<span data-ttu-id="0044e-171">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="0044e-171">**HTTP Request**</span></span>

    If successful, the following response is returned:

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

### <a name="get-the-upload-url"></a><span data-ttu-id="0044e-172">取得上傳 URL</span><span class="sxs-lookup"><span data-stu-id="0044e-172">Get the Upload URL</span></span>
<span data-ttu-id="0044e-173">若要接收實際的上傳 URL，請建立 SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="0044e-173">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="0044e-174">定位器為想要存取資產中之檔案的用戶端定義連線端點的開始時間和類型。</span><span class="sxs-lookup"><span data-stu-id="0044e-174">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="0044e-175">您可以為指定的 AccessPolicy 與 Asset 配對建立多個 Locator 實體，以處理不同的用戶端要求與需求。</span><span class="sxs-lookup"><span data-stu-id="0044e-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="0044e-176">這些 Locator 每個都會使用 StartTime 值加上 AccessPolicy 的 DurationInMinutes 值，以判斷可以使用 URL 的時間長度。</span><span class="sxs-lookup"><span data-stu-id="0044e-176">Each of these Locators use the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="0044e-177">如需詳細資訊，請參閱 [定位器](https://docs.microsoft.com/rest/api/media/operations/locator)。</span><span class="sxs-lookup"><span data-stu-id="0044e-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="0044e-178">SAS URL 具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="0044e-178">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="0044e-179">適用一些考量事項：</span><span class="sxs-lookup"><span data-stu-id="0044e-179">Some considerations apply:</span></span>

* <span data-ttu-id="0044e-180">您一次不能有超過五個唯一定位器與指定的資產相關聯。</span><span class="sxs-lookup"><span data-stu-id="0044e-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="0044e-181">如需詳細資訊，請參閱＜定位器＞。</span><span class="sxs-lookup"><span data-stu-id="0044e-181">For more information, see Locator.</span></span>
* <span data-ttu-id="0044e-182">如果您需要立即上傳檔案，您應該將 StartTime 值設為目前時間的五分鐘前。</span><span class="sxs-lookup"><span data-stu-id="0044e-182">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="0044e-183">這是因為用戶端電腦與媒體服務之間可能有時間差。</span><span class="sxs-lookup"><span data-stu-id="0044e-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="0044e-184">此外，您的 StartTime 值必須是以下日期時間格式：YYYY-MM-DDTHH:mm:ssZ (例如，"2014-05-23T17:53:50Z")。</span><span class="sxs-lookup"><span data-stu-id="0044e-184">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="0044e-185">建立 Locator 之後到它可供使用時，中間可能會有 30 到 40 秒的延遲。</span><span class="sxs-lookup"><span data-stu-id="0044e-185">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="0044e-186">此問題同時適用於 SAS URL 與原始定位器。</span><span class="sxs-lookup"><span data-stu-id="0044e-186">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="0044e-187">下列範例會示範如何建立 SAS URL 定位器，如要求主體中的 Type 屬性所定義 ("1" 代表 SAS 定位器，"2" 代表隨選原始定位器)。</span><span class="sxs-lookup"><span data-stu-id="0044e-187">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="0044e-188">傳回的 **Path** 屬性包含上傳檔案必須使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="0044e-188">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="0044e-189">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="0044e-189">**HTTP Request**</span></span>

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

<span data-ttu-id="0044e-190">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-190">**HTTP Response**</span></span>

<span data-ttu-id="0044e-191">如果成功，則會傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="0044e-191">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="0044e-192">將檔案上傳至 blob 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="0044e-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="0044e-193">一旦設定 AccessPolicy 與 Locator，實際檔案會使用 Azure 儲存體 REST API 上傳至 Azure Blob 儲存容器。</span><span class="sxs-lookup"><span data-stu-id="0044e-193">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="0044e-194">您必須將檔案以區塊 Blob 形式上傳。</span><span class="sxs-lookup"><span data-stu-id="0044e-194">You must upload the files as block blobs.</span></span> <span data-ttu-id="0044e-195">「Azure 媒體服務」不支援分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="0044e-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="0044e-196">您必須將要上傳的檔案名稱新增到上一節中所收到的 Locator **Path** 值。</span><span class="sxs-lookup"><span data-stu-id="0044e-196">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="0044e-197">例如，https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="0044e-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="0044e-198">.</span><span class="sxs-lookup"><span data-stu-id="0044e-198">.</span></span> <span data-ttu-id="0044e-199">.</span><span class="sxs-lookup"><span data-stu-id="0044e-199">.</span></span> <span data-ttu-id="0044e-200">.</span><span class="sxs-lookup"><span data-stu-id="0044e-200">.</span></span> 
> 
> 

<span data-ttu-id="0044e-201">如需使用 Azure 儲存體 blob 的詳細資訊，請參閱 [Blob 服務 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)。</span><span class="sxs-lookup"><span data-stu-id="0044e-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="0044e-202">更新 AssetFile</span><span class="sxs-lookup"><span data-stu-id="0044e-202">Update the AssetFile</span></span>
<span data-ttu-id="0044e-203">現在，您已上傳您的檔案，請更新 FileAsset 大小 (及其他) 資訊。</span><span class="sxs-lookup"><span data-stu-id="0044e-203">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="0044e-204">例如：</span><span class="sxs-lookup"><span data-stu-id="0044e-204">For example:</span></span>

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


<span data-ttu-id="0044e-205">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-205">**HTTP Response**</span></span>

<span data-ttu-id="0044e-206">如果成功，會傳回下列訊息：HTTP/1.1 204 沒有內容</span><span class="sxs-lookup"><span data-stu-id="0044e-206">If successful, the following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="0044e-207">刪除 Locator 和 AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="0044e-207">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="0044e-208">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="0044e-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="0044e-209">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-209">**HTTP Response**</span></span>

<span data-ttu-id="0044e-210">如果成功，則會傳回下列內容：</span><span class="sxs-lookup"><span data-stu-id="0044e-210">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="0044e-211">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="0044e-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="0044e-212">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-212">**HTTP Response**</span></span>

<span data-ttu-id="0044e-213">如果成功，則會傳回下列內容：</span><span class="sxs-lookup"><span data-stu-id="0044e-213">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="0044e-214"><a id="upload_in_bulk"></a>上傳大量資產</span><span class="sxs-lookup"><span data-stu-id="0044e-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-the-ingestmanifest"></a><span data-ttu-id="0044e-215">建立 IngestManifest</span><span class="sxs-lookup"><span data-stu-id="0044e-215">Create the IngestManifest</span></span>
<span data-ttu-id="0044e-216">IngestManifest 是適用於一組資產、資產檔案及統計資訊的容器，可用來判斷針對該組合進行大量內嵌的進度。</span><span class="sxs-lookup"><span data-stu-id="0044e-216">The IngestManifest is a container for a set of assets, asset files, and statistic information that can be used to determine the progress of bulk ingesting for the set.</span></span>

<span data-ttu-id="0044e-217">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="0044e-217">**HTTP Request**</span></span>

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

### <a name="create-assets"></a><span data-ttu-id="0044e-218">建立資產</span><span class="sxs-lookup"><span data-stu-id="0044e-218">Create assets</span></span>
<span data-ttu-id="0044e-219">建立 IngestManifestAsset 之前，您必須建立將使用大量內嵌完成的資產。</span><span class="sxs-lookup"><span data-stu-id="0044e-219">Before creating the IngestManifestAsset, you need to create the Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="0044e-220">資產是媒體服務中多種類型或物件集的容器，包括視訊、音訊、影像、縮圖集合、文字播放軌和隱藏式字幕檔案。</span><span class="sxs-lookup"><span data-stu-id="0044e-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="0044e-221">在 REST API 中，建立資產需要將 HTTP POST 要求傳送至 Microsoft Azure 媒體服務，並在要求本文中放置關於資產的任何屬性資訊。在此範例中，資產是使用要求本文包含的 StorageEncrption(1) 選項所建立。</span><span class="sxs-lookup"><span data-stu-id="0044e-221">In the REST API, creating an Asset requires sending a HTTP POST request to Microsoft Azure Media Services and placing any property information about your asset in the request body.In this example, the Asset is created using the StorageEncrption(1) option included with the request body.</span></span>

<span data-ttu-id="0044e-222">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-222">**HTTP Response**</span></span>

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

### <a name="create-the-ingestmanifestassets"></a><span data-ttu-id="0044e-223">建立 IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="0044e-223">Create the IngestManifestAssets</span></span>
<span data-ttu-id="0044e-224">IngestManifestAssets 代表 IngestManifest 中配合大量內嵌使用的資產。</span><span class="sxs-lookup"><span data-stu-id="0044e-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="0044e-225">基本上是將資產連結到資訊清單。</span><span class="sxs-lookup"><span data-stu-id="0044e-225">The basically link the asset to the manifest.</span></span> <span data-ttu-id="0044e-226">Azure 媒體服務會根據與 IngestManifestAsset 相關聯的 Ingestmanifestfile 集合，觀察內部的檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="0044e-226">Azure Media Services watches internally for the file upload based on IngestManifestFiles collection associated to the IngestManifestAsset.</span></span> <span data-ttu-id="0044e-227">將這些檔案上傳之後，資產便已完成。</span><span class="sxs-lookup"><span data-stu-id="0044e-227">Once these files are uploaded, the asset is completed.</span></span> <span data-ttu-id="0044e-228">您可以使用 HTTP POST 要求來建立新的 IngestManifestAsset。</span><span class="sxs-lookup"><span data-stu-id="0044e-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="0044e-229">在要求本文中，包含 IngestManifest 識別碼和資產識別碼，IngestManifestAsset 應該會將它們連結在一起以進行大量內嵌。</span><span class="sxs-lookup"><span data-stu-id="0044e-229">In the request body, include the IngestManifest Id and the Asset Id that the IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="0044e-230">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-230">**HTTP Response**</span></span>

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


### <a name="create-the-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="0044e-231">為每個資產建立 IngestManifestFile</span><span class="sxs-lookup"><span data-stu-id="0044e-231">Create the IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="0044e-232">IngestManifestFile 代表實際的視訊或音訊 Blob 物件，將針對資產上傳此物件以做為大量內嵌的一部分。</span><span class="sxs-lookup"><span data-stu-id="0044e-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="0044e-233">除非資產正在使用加密選項，否則不需與加密相關的屬性。</span><span class="sxs-lookup"><span data-stu-id="0044e-233">Encryption related properties are not required unless the asset is using an encryption option.</span></span> <span data-ttu-id="0044e-234">本節使用的範例示範如何建立 IngestManifestFile，針對先前建立的資產使用 StorageEncryption。</span><span class="sxs-lookup"><span data-stu-id="0044e-234">The example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for the Asset previously created.</span></span>

<span data-ttu-id="0044e-235">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-235">**HTTP Response**</span></span>

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

### <a name="upload-the-files-to-blob-storage"></a><span data-ttu-id="0044e-236">將檔案上傳至 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="0044e-236">Upload the Files to Blob Storage</span></span>
<span data-ttu-id="0044e-237">您可以使用任何高速用戶端應用程式，此應用程式能夠將資產檔案上傳至 IngestManifest 之 BlobStorageUriForUpload 屬性所提供的 Blob 儲存體容器 URI。</span><span class="sxs-lookup"><span data-stu-id="0044e-237">You can use any high speed client application capable of uploading the asset files to the blob storage container Uri provided by the BlobStorageUriForUpload property of the IngestManifest.</span></span> <span data-ttu-id="0044e-238">一個著名的高速上傳服務是 [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001)。</span><span class="sxs-lookup"><span data-stu-id="0044e-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="0044e-239">監視大量內嵌進度</span><span class="sxs-lookup"><span data-stu-id="0044e-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="0044e-240">您可以藉由輪詢 IngestManifest 的 Statistics 屬性，來監視 IngestManifest 的大量內嵌作業進度。</span><span class="sxs-lookup"><span data-stu-id="0044e-240">You can monitor the progress of bulk ingesting operations for an IngestManifest by polling the Statistics property of the IngestManifest.</span></span> <span data-ttu-id="0044e-241">該屬性是複雜類型 [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics)。</span><span class="sxs-lookup"><span data-stu-id="0044e-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="0044e-242">若要輪詢 Statistics 屬性，請送出 HTTP GET 要求以傳遞 IngestManifest 識別碼。</span><span class="sxs-lookup"><span data-stu-id="0044e-242">To poll the Statistics property, submit a HTTP GET request passing the IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="0044e-243">建立要用於加密的 ContentKey</span><span class="sxs-lookup"><span data-stu-id="0044e-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="0044e-244">如果您的資產會使用加密功能，就必須在建立資產檔案前，建立要用於加密的 ContentKey。</span><span class="sxs-lookup"><span data-stu-id="0044e-244">If your asset will use encryption, you must create the ContentKey to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="0044e-245">對於儲存體加密，要求本文中應該包含下列屬性。</span><span class="sxs-lookup"><span data-stu-id="0044e-245">For storage encryption, the following properties should be included in the request body.</span></span>

| <span data-ttu-id="0044e-246">要求本文屬性</span><span class="sxs-lookup"><span data-stu-id="0044e-246">Request body property</span></span> | <span data-ttu-id="0044e-247">說明</span><span class="sxs-lookup"><span data-stu-id="0044e-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0044e-248">識別碼</span><span class="sxs-lookup"><span data-stu-id="0044e-248">Id</span></span> |<span data-ttu-id="0044e-249">我們使用下列格式自行產生的 ContentKey 識別碼："nb:kid:UUID:<NEW GUID>"。</span><span class="sxs-lookup"><span data-stu-id="0044e-249">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="0044e-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="0044e-250">ContentKeyType</span></span> |<span data-ttu-id="0044e-251">這是針對此內容金鑰以整數表示的內容金鑰類型。</span><span class="sxs-lookup"><span data-stu-id="0044e-251">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="0044e-252">我們會傳遞值 1 來進行儲存體加密。</span><span class="sxs-lookup"><span data-stu-id="0044e-252">We pass the value 1 for storage encryption.</span></span> |
| <span data-ttu-id="0044e-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="0044e-253">EncryptedContentKey</span></span> |<span data-ttu-id="0044e-254">我們會建立新的內容金鑰值，其為 256 位元 (32 位元組) 的值。</span><span class="sxs-lookup"><span data-stu-id="0044e-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="0044e-255">此金鑰是藉由針對 GetProtectionKeyId 與 GetProtectionKey 方法執行 HTTP GET 要求，使用我們從 Microsoft Azure 媒體服務擷取的儲存體加密 X.509 憑證來加密的。</span><span class="sxs-lookup"><span data-stu-id="0044e-255">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="0044e-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="0044e-256">ProtectionKeyId</span></span> |<span data-ttu-id="0044e-257">這是適用於儲存體加密 X.509 憑證的保護金鑰識別碼，可用來加密我們的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="0044e-257">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span> |
| <span data-ttu-id="0044e-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="0044e-258">ProtectionKeyType</span></span> |<span data-ttu-id="0044e-259">這是適用於保護金鑰的加密類型，可用來將內容金鑰加密。</span><span class="sxs-lookup"><span data-stu-id="0044e-259">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="0044e-260">針對本文範例，此值為 StorageEncryption(1)。</span><span class="sxs-lookup"><span data-stu-id="0044e-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="0044e-261">Checksum</span><span class="sxs-lookup"><span data-stu-id="0044e-261">Checksum</span></span> |<span data-ttu-id="0044e-262">MD5 會針對內容金鑰計算出總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="0044e-262">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="0044e-263">它是使用內容金鑰來將內容識別碼加密計算而得的。</span><span class="sxs-lookup"><span data-stu-id="0044e-263">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="0044e-264">範例程式碼示範如何計算總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="0044e-264">The example code demonstrates how to calculate the checksum.</span></span> |

<span data-ttu-id="0044e-265">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-265">**HTTP Response**</span></span>

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

### <a name="link-the-contentkey-to-the-asset"></a><span data-ttu-id="0044e-266">將 ContentKey 連結到資產</span><span class="sxs-lookup"><span data-stu-id="0044e-266">Link the ContentKey to the Asset</span></span>
<span data-ttu-id="0044e-267">您可以藉由傳送 HTTP POST 要求，來將 ContentKey 關聯至一或多個資產。</span><span class="sxs-lookup"><span data-stu-id="0044e-267">The ContentKey is associated to one or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="0044e-268">下列要求是依識別碼將範例 ContentKey 連結至範例資產的範例。</span><span class="sxs-lookup"><span data-stu-id="0044e-268">The following request is an example to link the example ContentKey to the example asset by Id.</span></span>

<span data-ttu-id="0044e-269">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-269">**HTTP Response**</span></span>

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

<span data-ttu-id="0044e-270">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="0044e-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="0044e-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0044e-271">Next steps</span></span>

<span data-ttu-id="0044e-272">您現在可以將上傳的資產編碼。</span><span class="sxs-lookup"><span data-stu-id="0044e-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="0044e-273">如需詳細資訊，請參閱 [為資產編碼](media-services-portal-encode.md)。</span><span class="sxs-lookup"><span data-stu-id="0044e-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="0044e-274">您也可以使用 Azure Functions，以根據在所設定容器到達的檔案來觸發編碼作業。</span><span class="sxs-lookup"><span data-stu-id="0044e-274">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="0044e-275">如需詳細資訊，請參閱[此範例](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )。</span><span class="sxs-lookup"><span data-stu-id="0044e-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="0044e-276">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="0044e-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0044e-277">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="0044e-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How to Get a Media Processor]: media-services-get-media-processor.md

