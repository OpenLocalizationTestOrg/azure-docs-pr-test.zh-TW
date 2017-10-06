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
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a>使用 REST 傳遞點播內容入門
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

本快速入門將引導您完成 hello 步驟實作 Video-on-Demand (VoD) 傳遞內容的應用程式，使用 Azure 媒體服務 (AMS) REST Api。

hello 教學課程介紹 hello 基本 Media Services 工作流程和 hello 最常見的程式設計物件，以及 Media Services 開發所需的工作。 在 hello 完成 hello 教學課程，您將會是能 toostream 或漸進式下載範例媒體檔案，您可以上傳、 編碼，以及下載。

hello 下圖顯示一些最常用的 hello 物件開發 VoD 針對 hello 媒體服務 OData 模型的應用程式時。

按一下 hello 映像 tooview 它的完整大小。  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a>必要條件
hello 下列必要條件是必要的 toostart 使用媒體服務 REST api 進行開發。

* 一個 Azure 帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* 媒體服務帳戶。 toocreate Media Services 帳戶，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。
* 了解如何使用媒體服務 REST API toodevelop。 如需詳細資訊，請參閱[媒體服務 REST API 概觀](media-services-rest-how-to-use.md)。
* 由您選擇可以傳送 HTTP 要求和回應的應用程式。 本教學課程使用 [Fiddler](http://www.telerik.com/download/fiddler)。

本快速入門中，會顯示 hello 下列工作。

1. 啟動串流端點 （使用 hello Azure 入口網站）。
2. 使用 REST API 連接 toohello Media Services 帳戶。
3. 使用 REST API 建立新資產並上傳視訊檔案。
4. Hello 來源檔案編碼成一組彈性位元速率 MP4 檔案使用 REST API。
5. 發佈 hello 資產和取得資料流及使用 REST API 的漸進式下載 Url。
6. 播放您的內容。

>[!NOTE]
>對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。 您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。 如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。

如需本主題中所用的 AMS REST 實體的詳細資訊，請參閱 [Azure 媒體服務 REST API 參考](/rest/api/media/services/azure-media-services-rest-api-reference)。 此外，請參閱 [Azure 媒體服務概念](media-services-concepts.md)。

>[!NOTE]
>在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。 如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>啟動串流端點使用 hello Azure 入口網站

當使用 Azure Media Services hello 最常見的案例的其中一個會將視訊透過串流處理的彈性位元速率。 Media Services 提供的動態封裝，可讓您 toodeliver 您彈性位元速率編碼的 MP4 內容串流處理媒體服務 (MPEG DASH、 HLS、 Smooth Streaming) 在 just-in-time，支援不需要您 toostore 預先封裝格式每種串流處理格式的版本。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。

toostart hello 串流端點，請執行下列 hello:

1. 在 hello 登入[Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 設定視窗中，按一下 串流端點。
3. 按一下 hello 預設串流端點。

    hello 預設串流端點詳細資料 視窗隨即出現。

4. 按一下 hello 入門圖示。
5. 按一下 hello 儲存按鈕 toosave 您的變更。

## <a id="connect"></a>使用 REST API 連接 toohello Media Services 帳戶

如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。 

>[!NOTE]
>已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。 您必須進行的後續呼叫 toohello 新的 URI。

比方說，如果在嘗試後 tooconnect，您會取得 hello 下列：

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

您應該張貼您後續的 API 呼叫 toohttps://wamsbayclus001rest-hs.cloudapp.net/api/。

## <a id="upload"></a>使用 REST API 建立新資產並上傳視訊檔案

在媒體服務中，您會將數位檔案上傳到到資產。 hello**資產**實體可以包含視訊、 音訊、 影像、 縮圖集合、 文字播放軌和隱藏式的字幕檔案 （和 hello 中繼資料，這些檔案的相關。）之後 hello 檔案上傳到 hello 資產時，您的內容會安全地儲存在 hello 用於進一步處理和雲端資料流。

建立資產時，有 tooprovide hello 值的其中一個是資產建立選項。 hello**選項**屬性是描述可以建立資產的 hello 加密選項的列舉值。 有效的值是從 hello 清單下，此清單中的值組合的 hello 值的其中一個：

* **None** = **0** - 不使用加密。 使用此選項時，您的內容在傳輸或儲存體中靜止時不會受到保護。
    如果您計畫使用漸進式下載 toodeliver MP4，請使用此選項。
* **StorageEncrypted** = **1** -加密您清除的內容，在本機使用 AES 256 位元加密，並將其上傳 tooAzure 儲存體的方式予以儲存加密在靜止。 使用儲存體加密保護的資產會自動加密，並在 「 加密的檔案系統先前 tooencoding，及選擇性地重新加密的先前 toouploading 回為新輸出資產。 儲存體加密的 hello 主要使用案例是當您想 toosecure 強式加密在靜止高品質的輸入的媒體檔案在磁碟上。
* **CommonEncryptionProtected** = **2** - 如果您要上傳已經使用一般加密或 PlayReady DRM (例如使用 PlayReady DRM 保護的 Smooth Streaming) 加密及保護的內容，請使用這個選項。
* **EnvelopeEncryptionProtected** = **4** – 如果您要上傳使用 AES 加密的 HLS，請使用這個選項。 hello 檔案必須已編碼並由 Transform Manager 加密。

### <a name="create-an-asset"></a>建立資產
資產是媒體服務中多種類型或物件集的容器，包括視訊、音訊、影像、縮圖集合、文字播放軌和隱藏式字幕檔案。 在 hello REST API，建立資產必須傳送 POST 要求 tooMedia 服務和 hello 要求本文中放置關於您資產的任何屬性資訊。

下列範例會示範如何 hello toocreate 資產。

**HTTP 要求**

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


**HTTP 回應**

如果成功，則會傳回 hello 下列：

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

### <a name="create-an-assetfile"></a>建立 AssetFile
hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile)實體代表儲存在 blob 容器的視訊或音訊檔案。 資產檔案一律會與資產相關聯，資產可包含一或多個 Assetfile。 如果資產檔案物件不是 blob 容器中的數位檔案相關聯，hello Media Services 編碼器工作會失敗。

您將數位媒體檔案上傳到 blob 容器之後，您會使用 hello**合併**HTTP 要求 tooupdate hello AssetFile 媒體檔案 （如 hello 主題稍後所示） 的相關資訊。

**HTTP 要求**

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


**HTTP 回應**

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


### <a name="creating-hello-accesspolicy-with-write-permission"></a>建立具有寫入權限的 AccessPolicy hello
將任何檔案上傳到 blob 儲存體之前, 設定 hello 存取原則撰寫 tooan 資產的權限。 toodo 的 POST HTTP 要求 toohello AccessPolicies 實體集。 請在建立時定義 DurationInMinutes 值，否則您會在回應中收到 500 內部伺服器錯誤訊息。 如需 AccessPolicies 的詳細資訊，請參閱 [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)。

下列範例會示範如何 hello toocreate AccessPolicy:

**HTTP 要求**

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

**HTTP 回應**

如果成功，則會傳回下列回應 hello:

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

### <a name="get-hello-upload-url"></a>取得上傳 URL hello

tooreceive hello 實際的上傳 URL，建立 SAS 定位器。 定位器會定義要 tooaccess 檔案資產中的用戶端 hello 開始時間和連線端點的型別。 要求與需求時，您便可以建立給定 AccessPolicy 與 Asset 配對 toohandle 不同的用戶端的多個 Locator 實體。 這些 locator 都會使用 hello StartTime 值加上的時間可以使用 URL hello AccessPolicy toodetermine hello 長度 hello 和 DurationInMinutes 值。 如需詳細資訊，請參閱 [定位器](https://docs.microsoft.com/rest/api/media/operations/locator)。

SAS URL 具有下列格式的 hello:

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

適用一些考量事項：

* 您一次不能有超過五個唯一定位器與指定的資產相關聯。 如需詳細資訊，請參閱＜定位器＞。
* 如果您需要 tooupload 檔案立即，您應該設定您的 StartTime 值 toofive 分鐘，再 hello 目前的時間。 這是因為用戶端電腦與媒體服務之間可能有時間差。 此外，您的 StartTime 值必須在下列日期時間格式的 hello: YYYY-MM-DDTHH:mm:ssZ (例如，"2014年-05-23T17:53:50Z")。    
* 可能有 30 到 40 秒延遲定位器建立 toowhen 它是可供使用之後。 此問題適用於 SAS URL tooboth 和原始定位器。

如需 SAS 定位器的詳細資訊，請參閱[這個](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)部落格。

hello 下列範例顯示如何 toocreate SAS URL 定位器，所定義的 hello (如 SAS 定位器為"1") 和"2"的點播原始定位器 hello 要求主體中的類型屬性。 hello**路徑**屬性傳回包含 hello URL，您必須使用 tooupload 您的檔案。

**HTTP 要求**

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


**HTTP 回應**

如果成功，則會傳回下列回應 hello:

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

### <a name="upload-a-file-into-a-blob-storage-container"></a>將檔案上傳至 blob 儲存體容器
一旦您擁有 hello AccessPolicy 與 Locator 組，hello 實際的檔案是使用 hello Azure Storage REST Api 上傳的 tooan Azure blob 儲存體容器。 您必須將 hello 檔案上傳為區塊 blob。 「Azure 媒體服務」不支援分頁 Blob。  

> [!NOTE]
> 您必須新增 hello 檔案名稱 hello 檔案中，您想 tooupload toohello 定位器**路徑**收到 hello 前一節中的值。 例如，https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . .
>
>

如需使用 Azure 儲存體 blob 的詳細資訊，請參閱 [Blob 服務 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)。

### <a name="update-hello-assetfile"></a>更新 AssetFile hello
既然您已上傳您的檔案，更新 hello FileAsset 大小 （及其他） 資訊。 例如：

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


**HTTP 回應**

如果成功，則會傳回 hello 下列：

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a>刪除 hello Locator 和 AccessPolicy
**HTTP 要求**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP 回應**

如果成功，則會傳回 hello 下列：

    HTTP/1.1 204 No Content
    ...

**HTTP 要求**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

**HTTP 回應**

如果成功，則會傳回 hello 下列：

    HTTP/1.1 204 No Content
    ...

## <a id="encode"></a>Hello 原始程式檔編碼一組彈性位元速率 MP4 檔案

之前之後擷取到 Media Services，媒體資產可以編碼、 轉碼多工處理，浮水印等，它會傳遞 tooclients。 這些活動均已排程，並針對多種背景角色執行個體 tooensure 高效能、 可用性執行。 這些活動稱為作業和每個工作是不可部分完成的工作，請勿 hello hello 資產檔案上的實際工作所組成 (如需詳細資訊，請參閱[作業](/rest/api/media/services/job)，[工作](/rest/api/media/services/task)描述)。

如已稍早所述，當使用 Azure Media Services 一個 hello 最常見的案例提供自動調整位元速率串流 tooyour 用戶端。 Media Services 可以動態封裝成 hello 下列格式的其中一個的一組彈性位元速率 MP4 檔案： HTTP Live Streaming (HLS)，Smooth Streaming、 MPEG DASH。

hello 下列區段會顯示如何 toocreate 之作業中包含一種編碼工作。 hello 工作指定 tootranscode hello 夾層檔為彈性位元速率 mp4 集使用一組**媒體編碼器標準**。 hello > 一節也會示範如何 toomonitor hello 工作處理進度。 Hello 工作完成時，您都可以 toocreate 定位器屬於所需的 tooget 存取 tooyour 資產。

### <a name="get-a-media-processor"></a>取得媒體處理器
在媒體服務中，媒體處理器是可處理特定處理工作的元件，例如編碼、格式轉換、加密或解密媒體內容。 Hello 編碼工作顯示在本教學課程，我們 toouse hello 媒體編碼器標準。

下列程式碼要求 hello 編碼器的識別碼 hello。

**HTTP 要求**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP 回應**

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

### <a name="create-a-job"></a>建立工作
每個工作可以有一個或更多的工作，根據 hello 類型處理您想 tooaccomplish。 透過 hello REST API，您可以建立工作和其相關的工作中有兩種： 工作可以透過 hello 工作導覽屬性上作業的實體，或透過 OData 批次處理內嵌定義。 hello Media Services SDK 使用批次處理。 不過，本主題中的 hello 程式碼範例的 hello 可讀性，工作是內嵌定義。 如需批次處理的資訊，請參閱 [開放式資料通訊協定 (OData) 批次處理](http://www.odata.org/documentation/odata-version-3-0/batch-processing/)。

hello 下列範例會示範如何 toocreate 和 post 作業的一項工作設定 tooencode 視訊在特定的解析度與品質。 下列文件區段的 hello 包含所有 hello hello 清單[工作預設](http://msdn.microsoft.com/library/mt269960)hello 媒體編碼器標準處理器所支援。  

**HTTP 要求**

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

**HTTP 回應**

如果成功，則會傳回下列回應 hello:

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


在任何作業要求中有幾項重點 toonote:

* TaskBody 屬性必須使用常值的輸入或輸出資產 hello 工作所使用的 XML toodefine hello 數目。 hello 工作主題包含 XML hello XML 結構描述定義。
* 在 hello TaskBody 定義中，每個內部值<inputAsset>和<outputAsset>必須設定為 JobInputAsset(value) 或 JobOutputAsset(value)。
* 每個工作可以有多個輸出資產。 一個 JobOutputAsset(x) 只能使用一次做為工作中的工作輸出。
* 您可以指定 JobInputAsset 或 JobOutputAsset 做為工作的輸入資產。
* 工作不能形成循環。
* 您傳遞 tooJobInputAsset 或 JobOutputAsset 的 hello value 參數代表資產的 hello 索引值。 hello 實際資產被定義在 hello 工作實體定義的 hello Inputmediaasset 與 Outputmediaasset 導覽屬性中。

> [!NOTE]
> 因為 Media Services 內建於 OData v3，hello 個別資產 Inputmediaasset 與 Outputmediaasset 導覽屬性集合會透過參考"__metadata: uri"名稱 / 值組。
>
>

* Inputmediaasset 對應 tooone 或您已建立 Media Services 中的多個資產。 Outputmediaasset 由 hello 系統建立。 它們不會參考現有的資產。
* Outputmediaasset 可以使用 hello assetName 屬性命名。 如果這個屬性不存在，則 hello OutputMediaAsset hello 名稱是 hello 任何 hello 內部文字值<outputAsset>項目是與 hello 作業名稱值或 （在 hello hello Name 屬性不定義所在的情況下） 的 hello 作業識別碼值的尾碼。 例如，如果您設定 assetName 的值太 「 範例 」，則 OutputMediaAsset Name 屬性會設定 hello 太"Sample"。 不過，如果您未設定 assetName 的值，但未設定 hello 工作名稱太"NewJob"，然後 hello OutputMediaAsset Name 將"JobOutputAsset （值） _NewJob"。

    hello 下列範例顯示如何 tooset hello assetName 屬性：

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* tooenable 鏈結工作：

  * 工作必須有至少 2 個工作
  * 必須有至少一個工作的輸入是 hello 作業中的另一個工作的輸出。

如需詳細資訊，請參閱[使用 hello 媒體服務 REST API 建立編碼工作](media-services-rest-encode-asset.md)。

### <a name="monitor-processing-progress"></a>監看處理進度
Hello 下列範例所示，您可以使用 hello State 屬性擷取 hello 作業狀態。

**HTTP 要求**

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


**HTTP 回應**

如果成功，則會傳回下列回應 hello:

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


### <a name="cancel-a-job"></a>取消工作
Media Services 可讓您 toocancel 透過 hello 利用 CancelJob 函數執行作業。 此呼叫會傳回 400 錯誤碼，如果您嘗試 toocancel 當其狀態為已取消的工作、 取消、 錯誤，或完成。

下列範例會示範如何 hello toocall CancelJob。

**HTTP 要求**

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


如果成功，會傳回 204 回應碼且沒有訊息主體。

> [!NOTE]
> 您必須進行 URL 編碼 hello 作業識別碼 (當成： somevalue) 時把它中當做參數 tooCancelJob 傳遞。
>
>

### <a name="get-hello-output-asset"></a>取得 hello 輸出資產
hello 下列程式碼會示範如何 toorequest hello 輸出資產識別碼。

**HTTP 要求**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP 回應**

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



## <a id="publish_get_urls"></a>發佈 hello 資產和取得資料流及使用 REST API 的漸進式下載 Url

toostream 或下載資產，您首先需要太 「 發行 」 它藉由建立定位器。 定位器提供存取 toofiles hello 資產中所包含。 Media Services 支援兩種類型的定位器： OnDemandOrigin 定位器，使用的 toostream 媒體 （例如，MPEG DASH、 HLS 或 Smooth Streaming） 和存取簽章 (SAS) 定位器，使用 toodownload 媒體檔案。 如需 SAS 定位器的詳細資訊，請參閱[這個](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)部落格。

一旦您建立 hello 定位器時，您可以建立 hello Url 使用的 toostream 或下載您的檔案。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。

Smooth Streaming 的串流 URL 具有下列格式的 hello:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

HLS 的串流 URL 具有下列格式的 hello:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

適用於 MPEG DASH 串流 URL 具有下列格式的 hello:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


使用 SAS URL toodownload 檔案具有下列格式的 hello:

    {blob container name}/{asset name}/{file name}/{SAS signature}

本節說明影響 tooperform hello 下列工作需要太 「 發行 」 您的資產。  

* 建立具有讀取權限的 AccessPolicy hello
* 建立下載內容用的 SAS URL
* 建立串流內容用的原始 URL

### <a name="creating-hello-accesspolicy-with-read-permission"></a>建立具有讀取權限的 AccessPolicy hello
然後再下載或串流任何媒體內容，先定義具有讀取權限的 AccessPolicy，並建立 hello 適當的 Locator 實體，指定 hello 類型的傳遞機制想 tooenable 為用戶端。 如需有關可用 hello 屬性的詳細資訊，請參閱[AccessPolicy 實體屬性](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties)。

hello 下列範例顯示如何 toospecify hello 指定之資產的讀取權限的 AccessPolicy。

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

如果成功，會傳回 201 成功碼，描述您所建立的 hello AccessPolicy 實體。 然後，您可以使用在 hello AccessPolicy Id 與 hello hello 資產，其中包含您想要 toodeliver （例如輸出資產） toocreate hello Locator 實體的 hello 檔案資產識別碼。

> [!NOTE]
> 此基本工作流程是 hello 與上傳檔案時擷取資產 （如已稍早在本主題中所討論） 相同。 此外，例如上傳檔案，如果您 （或您的用戶端） 需要 tooaccess 檔案立即，設定您的 StartTime 值 toofive 分鐘，再 hello 目前的時間。 這個動作是必要的因為可能有時鐘誤差 hello 用戶端與 Media Services 之間。 hello StartTime 值必須在下列日期時間格式的 hello: YYYY-MM-DDTHH:mm:ssZ (例如，"2014年-05-23T17:53:50Z")。
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a>建立下載內容用的 SAS URL
hello，下列程式碼顯示如何 tooget 可以是使用的 toodownload 媒體檔案的 URL 建立和上傳先前。 hello AccessPolicy 具有讀取權限集，然後 hello 定位器路徑 tooa SAS 下載 URL。

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

如果成功，則會傳回下列回應 hello:

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


傳回的 hello**路徑**屬性包含 hello SAS URL。

> [!NOTE]
> 如果您下載儲存體加密內容，您就必須手動將其解密才能呈現，，或使用的 hello 中處理工作 toooutput Storage Decryption mediaprocessor 安全處理 hello 清除 tooan OutputAsset 中的檔案，然後從該資產下載。 如需有關處理的詳細資訊，請參閱使用 hello 媒體服務 REST API 建立編碼工作。 此外，已建立 SAS URL 定位器之後，無法更新它們。 例如，您無法重複使用 hello 與更新的 StartTime 值相同的定位器。 這是因為建立 SAS Url 的 hello 方式。 如果您想要 tooaccess 資產下載定位器過期之後，您必須建立一個新使用新的 StartTime。
>
>

### <a name="download-files"></a>下載檔案
一旦您擁有 hello AccessPolicy 與 Locator 集，您可以使用下載檔案 hello Azure Storage REST Api。  

> [!NOTE]
> 您必須新增 hello 檔案名稱 hello 檔案中，您想 toodownload toohello 定位器**路徑**收到 hello 前一節中的值。 例如，https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . .
>
>

如需使用 Azure 儲存體 blob 的詳細資訊，請參閱 [Blob 服務 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)。

Hello 編碼您稍早執行的作業 （編碼成自動調整 MP4 組），因為您有多個，您可以漸進式下載 MP4 檔案。 例如：    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a>建立串流內容用的串流 URL
hello 下列程式碼會示範如何 toocreate 串流的 URL 定位器：

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

如果成功，則會傳回下列回應 hello:

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

toostream Smooth Streaming 原始 URL，在串流媒體播放器，您必須將附加的 hello Smooth Streaming 資訊清單檔案，後面接"/manifest"hello 名稱 hello 路徑屬性。

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

toostream HLS，附加 (格式 = m3u8 aapl) hello 後"接 /manifest"。

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

toostream MPEG DASH 附加 (格式 = mpd-時間-csf) hello 後"接 /manifest"。

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <a id="play"></a>播放您的內容
視訊，您使用 toostream [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。

tootest 漸進式下載，將 URL 貼到瀏覽器 （例如，IE、 Chrome、 Safari）。

## <a name="next-steps-media-services-learning-paths"></a>後續步驟：媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
