---
title: "使用媒體處理器 aaaHow tooCreate hello Azure Media Services SDK for.NET |Microsoft 文件"
description: "了解 toocreate 媒體處理器元件 tooencode 」，將格式轉換、 加密或解密媒體內容，Azure 媒體服務的方式。 程式碼範例會以 C# 所撰寫，並使用 hello Media Services SDK for.NET。"
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
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="be43f-104">如何：取得媒體處理器執行個體</span><span class="sxs-lookup"><span data-stu-id="be43f-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be43f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="be43f-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="be43f-106">REST</span><span class="sxs-lookup"><span data-stu-id="be43f-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="be43f-107">Overview</span><span class="sxs-lookup"><span data-stu-id="be43f-107">Overview</span></span>
<span data-ttu-id="be43f-108">在媒體服務中，媒體處理器是可處理特定處理工作的元件，例如編碼、格式轉換、加密或解密媒體內容。</span><span class="sxs-lookup"><span data-stu-id="be43f-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="be43f-109">通常當您建立工作 tooencode 建立媒體處理器、 加密，或將媒體內容的 hello 格式轉換。</span><span class="sxs-lookup"><span data-stu-id="be43f-109">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="be43f-110">Azure 媒體處理器</span><span class="sxs-lookup"><span data-stu-id="be43f-110">Azure media processors</span></span> 

<span data-ttu-id="be43f-111">hello 下列主題提供媒體處理器的清單：</span><span class="sxs-lookup"><span data-stu-id="be43f-111">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="be43f-112">編碼媒體處理器</span><span class="sxs-lookup"><span data-stu-id="be43f-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="be43f-113">分析媒體處理器</span><span class="sxs-lookup"><span data-stu-id="be43f-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="be43f-114">取得媒體處理器</span><span class="sxs-lookup"><span data-stu-id="be43f-114">Get Media Processor</span></span>

<span data-ttu-id="be43f-115">hello 遵循方法顯示如何 tooget 媒體處理器執行個體。</span><span class="sxs-lookup"><span data-stu-id="be43f-115">hello following method shows how tooget a media processor instance.</span></span> <span data-ttu-id="be43f-116">hello 程式碼範例假設名為的模組層級變數 hello 使用**（_c)** tooreference hello 伺服器內容 hello > 一節中所述[如何： 連接服務以程式設計方式 tooMedia](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="be43f-116">hello code example assumes hello use of a module-level variable named **_context** tooreference hello server context as described in hello section [How to: Connect tooMedia Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="be43f-117">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="be43f-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="be43f-118">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="be43f-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="be43f-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be43f-119">Next Steps</span></span>
<span data-ttu-id="be43f-120">您現在知道如何 tooget 媒體處理器執行個體中，移 toohello[如何 tooEncode 資產](media-services-dotnet-encode-with-media-encoder-standard.md)這會顯示如何 toouse 會 hello 媒體編碼器標準 tooencode 資產的主題。</span><span class="sxs-lookup"><span data-stu-id="be43f-120">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

