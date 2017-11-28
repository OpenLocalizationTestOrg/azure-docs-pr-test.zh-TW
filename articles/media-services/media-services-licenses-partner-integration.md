---
title: "aaaUsing 夥伴 toodeliver Widevine 授權 tooAzure Media Services |Microsoft 文件"
description: "本文說明如何使用 Azure 媒體服務 (AMS) toodeliver 以 PlayReady 和 Widevine DRMs AMS 動態加密的資料流。 hello PlayReady 授權來自 Media Services PlayReady 授權伺服器，並 Widevine 授權傳遞 castLabs 授權伺服器。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5bcad5a4-c0bb-4871-9cce-808a913c53e6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 3c18a8a22ced239931dea5385020194bd6d83f28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-partners-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="4dbd8-104">使用協力廠商 toodeliver Widevine 授權 tooAzure 媒體服務</span><span class="sxs-lookup"><span data-stu-id="4dbd8-104">Using partners toodeliver Widevine licenses tooAzure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="4dbd8-105">概觀</span><span class="sxs-lookup"><span data-stu-id="4dbd8-105">Overview</span></span>
<span data-ttu-id="4dbd8-106">Microsoft Azure Media Services 可讓您 toodeliver 受到 Widevine DRM，會根據 hello Common Encryption (CENC) 規格加密的 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="4dbd8-106">Microsoft Azure Media Services enables you toodeliver MPEG-DASH protected with Widevine DRM, which is encrypted per hello Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="4dbd8-107">從開始 hello Media Services.NET SDK 版本 3.5.2，Media Services 可讓您 tooconfigure Widevine 授權範本，並取得 Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="4dbd8-107">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="4dbd8-108">您也可以使用下列 AMS 夥伴 toohelp 傳遞 Widevine 授權 hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/)， [EZDRM](http://ezdrm.com/)， [castLabs](http://castlabs.com/company/partners/azure/)。</span><span class="sxs-lookup"><span data-stu-id="4dbd8-108">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="4dbd8-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="4dbd8-109">castLabs</span></span>
<span data-ttu-id="4dbd8-110">您可以使用[castLabs](http://castlabs.com/company/partners/azure/) toodeliver Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="4dbd8-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) toodeliver Widevine licenses.</span></span> <span data-ttu-id="4dbd8-111">如需詳細資訊，請參閱[使用 castLabs toodeliver DRM 授權 tooAzure 媒體服務](media-services-castlabs-integration.md)</span><span class="sxs-lookup"><span data-stu-id="4dbd8-111">For more information, see [Using castLabs toodeliver DRM licenses tooAzure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="4dbd8-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="4dbd8-112">Axinom</span></span>
<span data-ttu-id="4dbd8-113">您可以使用[Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) toodeliver Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="4dbd8-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) toodeliver Widevine licenses.</span></span> <span data-ttu-id="4dbd8-114">如需詳細資訊，請參閱[使用 Axinom toodeliver DRM 授權 tooAzure 媒體服務](media-services-axinom-integration.md)</span><span class="sxs-lookup"><span data-stu-id="4dbd8-114">For more information, see [Using Axinom toodeliver DRM licenses tooAzure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="4dbd8-115">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="4dbd8-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4dbd8-116">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="4dbd8-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="4dbd8-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4dbd8-117">See also</span></span>
[<span data-ttu-id="4dbd8-118">使用 PlayReady 和/或 Widevine 動態一般加密</span><span class="sxs-lookup"><span data-stu-id="4dbd8-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="4dbd8-119">Mingfei 的部落格</span><span class="sxs-lookup"><span data-stu-id="4dbd8-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

