---
title: "如何使用 REST 取得媒體處理器執行個體 | Microsoft Docs"
description: "了解如何建立媒體處理器元件，為 Azure 媒體服務的媒體內容進行編碼、格式轉換、加密或解密。"
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
ms.openlocfilehash: 4ad90ad979c5bd74fc55155098c88d5c13cb12e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="e1f40-103">如何取得媒體處理器執行個體</span><span class="sxs-lookup"><span data-stu-id="e1f40-103">How to get a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1f40-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e1f40-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="e1f40-105">REST</span><span class="sxs-lookup"><span data-stu-id="e1f40-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e1f40-106">Overview</span><span class="sxs-lookup"><span data-stu-id="e1f40-106">Overview</span></span>
<span data-ttu-id="e1f40-107">在媒體服務中，媒體處理器是可處理特定處理工作的元件，例如編碼、格式轉換、加密或解密媒體內容。</span><span class="sxs-lookup"><span data-stu-id="e1f40-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="e1f40-108">您通常會在建立媒體內容的編碼、加密或格式轉換工作時建立媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="e1f40-108">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="e1f40-109">Azure 媒體處理器</span><span class="sxs-lookup"><span data-stu-id="e1f40-109">Azure media processors</span></span> 

<span data-ttu-id="e1f40-110">下列主題提供媒體處理器的清單：</span><span class="sxs-lookup"><span data-stu-id="e1f40-110">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="e1f40-111">編碼媒體處理器</span><span class="sxs-lookup"><span data-stu-id="e1f40-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="e1f40-112">分析媒體處理器</span><span class="sxs-lookup"><span data-stu-id="e1f40-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="e1f40-113">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="e1f40-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="e1f40-114">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="e1f40-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="e1f40-115">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="e1f40-115">Connect to Media Services</span></span>

<span data-ttu-id="e1f40-116">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="e1f40-116">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="e1f40-117">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="e1f40-117">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="e1f40-118">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="e1f40-118">You must make subsequent calls to the new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="e1f40-119">取得媒體處理器</span><span class="sxs-lookup"><span data-stu-id="e1f40-119">Get a media processor</span></span>

<span data-ttu-id="e1f40-120">下列 REST 呼叫示範如何依名稱取得媒體處理器執行個體 (在此案例中，是**媒體編碼器標準**)。</span><span class="sxs-lookup"><span data-stu-id="e1f40-120">The following REST call shows how to get a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="e1f40-121">要求：</span><span class="sxs-lookup"><span data-stu-id="e1f40-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="e1f40-122">回應：</span><span class="sxs-lookup"><span data-stu-id="e1f40-122">Response:</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="e1f40-123">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="e1f40-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e1f40-124">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e1f40-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e1f40-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1f40-125">Next Steps</span></span>
<span data-ttu-id="e1f40-126">既然您已了解如何取得媒體處理器執行個體，請移至 [如何為資產編碼](media-services-rest-get-started.md) 主題，以了解如何使用媒體編碼器標準將資產編碼。</span><span class="sxs-lookup"><span data-stu-id="e1f40-126">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-rest-get-started.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

