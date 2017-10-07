---
title: "aaa tooget 媒體處理器執行個體使用 REST 的方式 |Microsoft 文件"
description: "了解 toocreate 媒體處理器元件 tooencode 」，將格式轉換、 加密或解密媒體內容，Azure 媒體服務的方式。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a><span data-ttu-id="39f7a-103">如何 tooget 媒體處理器執行個體</span><span class="sxs-lookup"><span data-stu-id="39f7a-103">How tooget a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39f7a-104">.NET</span><span class="sxs-lookup"><span data-stu-id="39f7a-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="39f7a-105">REST</span><span class="sxs-lookup"><span data-stu-id="39f7a-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="39f7a-106">Overview</span><span class="sxs-lookup"><span data-stu-id="39f7a-106">Overview</span></span>
<span data-ttu-id="39f7a-107">在媒體服務中，媒體處理器是可處理特定處理工作的元件，例如編碼、格式轉換、加密或解密媒體內容。</span><span class="sxs-lookup"><span data-stu-id="39f7a-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="39f7a-108">通常當您建立工作 tooencode 建立媒體處理器、 加密，或將媒體內容的 hello 格式轉換。</span><span class="sxs-lookup"><span data-stu-id="39f7a-108">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="39f7a-109">Azure 媒體處理器</span><span class="sxs-lookup"><span data-stu-id="39f7a-109">Azure media processors</span></span> 

<span data-ttu-id="39f7a-110">hello 下列主題提供媒體處理器的清單：</span><span class="sxs-lookup"><span data-stu-id="39f7a-110">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="39f7a-111">編碼媒體處理器</span><span class="sxs-lookup"><span data-stu-id="39f7a-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="39f7a-112">分析媒體處理器</span><span class="sxs-lookup"><span data-stu-id="39f7a-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="39f7a-113">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="39f7a-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="39f7a-114">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="39f7a-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="39f7a-115">TooMedia 服務連接</span><span class="sxs-lookup"><span data-stu-id="39f7a-115">Connect tooMedia Services</span></span>

<span data-ttu-id="39f7a-116">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="39f7a-116">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="39f7a-117">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="39f7a-117">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="39f7a-118">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="39f7a-118">You must make subsequent calls toohello new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="39f7a-119">取得媒體處理器</span><span class="sxs-lookup"><span data-stu-id="39f7a-119">Get a media processor</span></span>

<span data-ttu-id="39f7a-120">下列 REST 呼叫的 hello 顯示 tooget 媒體處理器執行個體之名稱的方式 (在此情況下，**媒體編碼器標準**)。</span><span class="sxs-lookup"><span data-stu-id="39f7a-120">hello following REST call shows how tooget a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="39f7a-121">要求：</span><span class="sxs-lookup"><span data-stu-id="39f7a-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="39f7a-122">回應：</span><span class="sxs-lookup"><span data-stu-id="39f7a-122">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
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


## <a name="media-services-learning-paths"></a><span data-ttu-id="39f7a-123">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="39f7a-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="39f7a-124">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="39f7a-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="39f7a-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39f7a-125">Next Steps</span></span>
<span data-ttu-id="39f7a-126">您現在知道如何 tooget 媒體處理器執行個體中，移 toohello[如何 tooEncode 資產](media-services-rest-get-started.md)這會顯示如何 toouse 會 hello 媒體編碼器標準 tooencode 資產的主題。</span><span class="sxs-lookup"><span data-stu-id="39f7a-126">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-rest-get-started.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

