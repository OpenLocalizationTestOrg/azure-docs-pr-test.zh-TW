---
title: "使用媒體服務 REST API aaaConfiguring 資產傳遞原則 |Microsoft 文件"
description: "本主題說明如何使用媒體服務 REST API tooconfigure 不同資產傳遞原則。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a>設定資產傳遞原則
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

如果您計劃 toodeliver 動態加密資產，hello 其中一個步驟中 hello 媒體服務內容傳遞工作流程設定資產的傳遞原則。 hello 資產傳遞原則會告知 Media Services 方式如您傳遞的資產 toobe： 成哪一個資料流通訊協定應在您的資產動態封裝 （適用於例如 MPEG DASH、 HLS、 Smooth Streaming 或全部），是否要 toodynamically加密您的資產和方式 （信封或一般加密）。

本主題討論原因以及如何 toocreate 及設定資產的傳遞原則。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 
>
>此外，toobe 無法 toouse 動態封裝和動態加密您的資產必須包含一組彈性位元速率 mp4 或彈性位元速率 Smooth Streaming 檔案。

您可以套用不同的原則 toohello 相同資產。 例如，您可以套用 PlayReady 加密 tooSmooth 資料流與 AES 信封加密 tooMPEG DASH 和 HLS。 傳遞原則中未定義任何通訊協定 （例如，新增只能指定 HLS 作為 hello 通訊協定的單一原則），將無法從資料流。 hello 例外狀況 toothis 是如果您有未完全定義的資產傳遞原則。 然後，將允許 hello 清除所有通訊協定。

如果您想 toodeliver 儲存體加密資產時，您必須設定 hello 資產的傳遞原則。 在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則。 比方說，toodeliver 資產加密使用進階加密標準 (AES) 信封加密金鑰，將 hello 原則類型設定太**DynamicEnvelopeEncryption**。 tooremove 存放裝置加密和資料流 hello 資產中 hello 清除，設定 hello 原則類型太**NoDynamicEncryption**。 顯示如何 tooconfigure 這些原則類型的範例。

取決於您如何設定 hello 資產傳遞原則會是能 toodynamically 封裝、 動態加密和 hello 遵循串流通訊協定資料流： Smooth Streaming、 HLS、 MPEG DASH 資料流。

下列清單顯示 hello hello 格式化您使用 toostream Smooth、 HLS、 破折號。

Smooth Streaming：

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest

HLS：

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=mpd-time-csf)


如需有關如何 toopublish 資產和建置串流 URL，請參閱指示[建置串流 URL](media-services-deliver-streaming-content.md)。

## <a name="considerations"></a>考量
* 當資產的 OnDemand (串流) 定位器仍存在時，您無法刪除與該資產關聯的 AssetDeliveryPolicy。 hello 建議是從 hello 資產 tooremove hello 原則之前刪除 hello 原則。
* 未設定資產傳遞原則時，將無法於儲存空間已加密的資產建立串流定位器。  如果 hello 資產不儲存體加密，hello 系統可讓您在 hello 清除未使用的資產傳遞原則中建立定位器和資料流的 hello 資產。
* 您可以有多個單一資產相關聯的資產傳遞原則，但您只能指定其中一種方式 toohandle 給定 AssetDeliveryProtocol。  這表示如果您嘗試 toolink 兩個傳遞指定的原則，因為 hello 系統並不知道哪一個，將會導致錯誤的 hello AssetDeliveryProtocol.SmoothStreaming 通訊協定您希望 tooapply 當用戶端要求 Smooth Streaming。
* 如果您有現有的串流定位器的資產，您無法連結新的原則 toohello 資產、 取消連結現有的原則從 hello 資產，或更新與 hello 資產相關聯的傳遞原則。  第一次有 tooremove hello 串流定位器，調整 hello 原則，然後重新建立 hello 串流定位器。  您可以使用相同的 locatorId，當您重新建立 hello 串流定位器，但是您應該確定因為 hello 原點或下游 CDN 快取內容，將不會造成問題的用戶端 hello。

>[!NOTE]

>在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。 如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。

## <a name="connect-toomedia-services"></a>TooMedia 服務連接

如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。 

>[!NOTE]
>已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。 您必須進行的後續呼叫 toohello 新的 URI。

## <a name="clear-asset-delivery-policy"></a>清除資產傳遞原則
### <a id="create_asset_delivery_policy"></a>建立資產傳遞原則
hello 下列 HTTP 要求建立資產傳遞原則，指定 toonot 套用動態加密和 toodeliver hello 資料流中的 hello 遵循任何通訊協定： MPEG DASH、 HLS 和 Smooth Streaming 通訊協定。 

建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。   

要求：

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

回應：

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <a id="link_asset_with_asset_delivery_policy"></a>連結資產與資產傳遞原則
下列 HTTP 要求的連結 hello hello 指定資產 toohello 資產傳遞原則。

要求：

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

回應：

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>DynamicEnvelopeEncryption 資產傳遞原則
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a>建立 hello EnvelopeEncryption 類型內容金鑰，並將它連結 toohello 資產
當指定 DynamicEnvelopeEncryption 傳遞原則，您需要 toomake 確定 toolink hello EnvelopeEncryption 類型將資產 tooa 內容金鑰。 如需詳細資訊，請參閱 [建立內容金鑰](media-services-rest-create-contentkey.md)。

### <a id="get_delivery_url"></a>取得傳遞 URL
指定傳遞方法的 hello hello 先前步驟中建立的內容金鑰的 hello get hello 傳遞 URL。 用戶端會使用傳回 URL toorequest hello AES 金鑰或 PlayReady 授權順序 tooplayback hello 中的受保護的內容。

指定 hello hello HTTP 要求主體中的 hello URL tooget hello 類型。 如果您要保護使用 PlayReady，要求媒體服務 PlayReady 授權取得 URL，使用 1 hello keyDeliveryType: {"keyDeliveryType": 1}。 如果您要保護您的內容與 hello 信封加密，來要求金鑰取得 URL 指定 keyDeliveryType 的 2: {"keyDeliveryType": 2}。

要求：

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

回應：

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a>建立資產傳遞原則
hello 下列 HTTP 要求建立 hello **AssetDeliveryPolicy**也就是設定的 tooapply 動態信封加密 (**DynamicEnvelopeEncryption**) toohello **HLS**通訊協定 （在此範例中，其他通訊協定將會遭到封鎖而無法串流處理）。 

建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。   

要求：

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


回應：

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a>連結資產與資產傳遞原則
請參閱 [連結資產與資產傳遞原則](#link_asset_with_asset_delivery_policy)

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>DynamicCommonEncryption 資產傳遞原則
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a>建立 hello CommonEncryption 類型內容金鑰，並將它連結 toohello 資產
當指定 DynamicCommonEncryption 傳遞原則，您需要 toomake 確定 toolink hello CommonEncryption 類型將資產 tooa 內容金鑰。 如需詳細資訊，請參閱 [建立內容金鑰](media-services-rest-create-contentkey.md)。

### <a name="get-delivery-url"></a>取得傳遞 URL
取得 hello PlayReady 傳遞方法的 hello hello 先前步驟中建立的內容金鑰 hello 傳遞 URL。 用戶端會使用 hello 傳回 URL toorequest PlayReady 授權順序 tooplayback hello 中的受保護的內容。 如需詳細資訊，請參閱 [取得傳遞 URL](#get_delivery_url)。

### <a name="create-asset-delivery-policy"></a>建立資產傳遞原則
hello 下列 HTTP 要求建立 hello **AssetDeliveryPolicy**也就是設定的 tooapply 動態一般加密 (**DynamicCommonEncryption**) toohello **Smooth Streaming**通訊協定 （在此範例中，其他通訊協定將會遭到封鎖而無法串流處理）。 

建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。   

要求：

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


如果您想 tooprotect 您使用 Widevine DRM 的內容時，更新 hello AssetDeliveryConfiguration 值 toouse WidevineLicenseAcquisitionUrl （其 hello 值為 7），並指定 hello 授權傳遞服務 URL。 您可以使用下列 AMS 夥伴 toohelp 傳遞 Widevine 授權 hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/)， [EZDRM](http://ezdrm.com/)， [castLabs](http://castlabs.com/company/partners/azure/)。

例如： 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> 當 Widevine 使用加密，才會使用虛線無法 toodeliver。 請確定 toospecify 虛線 (2) 中的 hello 資產傳遞通訊協定。
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a>連結資產與資產傳遞原則
請參閱 [連結資產與資產傳遞原則](#link_asset_with_asset_delivery_policy)

## <a id="types"></a>定義 AssetDeliveryPolicy 時使用的類型

### <a name="assetdeliveryprotocol"></a>AssetDeliveryProtocol

hello 下列列舉描述您可以針對 hello 資產傳遞通訊協定設定的值。

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a>AssetDeliveryPolicyType

hello 下列列舉描述您可以設定 hello 資產傳遞原則類型的值。  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a>ContentKeyDeliveryType

hello 下列列舉描述您可以使用 hello 內容金鑰 toohello 用戶端 tooconfigure hello 傳遞方法的值。
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a>AssetDeliveryPolicyConfigurationKey

下列列舉 hello 描述您可以設定資產傳遞原則的 tooconfigure 用金鑰 tooget 特定組態的值。

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

