---
title: "如何使用適用於 .NET 的 Azure 媒體服務 SDK 建立媒體處理器 | Microsoft Docs"
description: "了解如何建立媒體處理器元件，為 Azure 媒體服務的媒體內容進行編碼、格式轉換、加密或解密。 程式碼範例以 C# 撰寫，並使用 Media Services SDK for .NET。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: c2cbe41b71afa8acc184f9d7f4cfe94686de783e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="28c9a-104">如何：取得媒體處理器執行個體</span><span class="sxs-lookup"><span data-stu-id="28c9a-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="28c9a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="28c9a-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="28c9a-106">REST</span><span class="sxs-lookup"><span data-stu-id="28c9a-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="28c9a-107">Overview</span><span class="sxs-lookup"><span data-stu-id="28c9a-107">Overview</span></span>
<span data-ttu-id="28c9a-108">在媒體服務中，媒體處理器是可處理特定處理工作的元件，例如編碼、格式轉換、加密或解密媒體內容。</span><span class="sxs-lookup"><span data-stu-id="28c9a-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="28c9a-109">您通常會在建立媒體內容的編碼、加密或格式轉換工作時建立媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="28c9a-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="28c9a-110">Azure 媒體處理器</span><span class="sxs-lookup"><span data-stu-id="28c9a-110">Azure media processors</span></span> 

<span data-ttu-id="28c9a-111">下列主題提供媒體處理器的清單：</span><span class="sxs-lookup"><span data-stu-id="28c9a-111">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="28c9a-112">編碼媒體處理器</span><span class="sxs-lookup"><span data-stu-id="28c9a-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="28c9a-113">分析媒體處理器</span><span class="sxs-lookup"><span data-stu-id="28c9a-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="28c9a-114">取得媒體處理器</span><span class="sxs-lookup"><span data-stu-id="28c9a-114">Get Media Processor</span></span>

<span data-ttu-id="28c9a-115">下列方法將說明如何取得媒體處理器執行個體。</span><span class="sxs-lookup"><span data-stu-id="28c9a-115">The following method shows how to get a media processor instance.</span></span> <span data-ttu-id="28c9a-116">此程式碼範例假設會使用名為 **_context** 的模組層級變數來參考伺服器內容，如[做法：以程式設計方式連接到媒體服務](media-services-use-aad-auth-to-access-ams-api.md)一節所述。</span><span class="sxs-lookup"><span data-stu-id="28c9a-116">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="28c9a-117">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="28c9a-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="28c9a-118">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="28c9a-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="28c9a-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28c9a-119">Next Steps</span></span>
<span data-ttu-id="28c9a-120">既然您已了解如何取得媒體處理器執行個體，請移至 [如何為資產編碼](media-services-dotnet-encode-with-media-encoder-standard.md) 主題，以了解如何使用媒體編碼器標準將資產編碼。</span><span class="sxs-lookup"><span data-stu-id="28c9a-120">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

