---
title: "使用合作夥伴將 Widevine 授權傳遞到 Azure 媒體服務 | Microsoft Docs"
description: "本文說明如何使用 Azure 媒體服務 (AMS) 來傳遞 AMS 使用 PlayReady 與 Widevine DRM 動態加密的資料流。 PlayReady 授權來自媒體服務 PlayReady 授權伺服器，Widevine 授權由 castLabs 授權伺服器傳遞。"
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
ms.openlocfilehash: 6867e4f910970121df3858516c6bab3114c3c6f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-partners-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="e11ce-104">使用合作夥伴將 Widevine 授權傳遞到 Azure 媒體服務</span><span class="sxs-lookup"><span data-stu-id="e11ce-104">Using partners to deliver Widevine licenses to Azure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="e11ce-105">Overview</span><span class="sxs-lookup"><span data-stu-id="e11ce-105">Overview</span></span>
<span data-ttu-id="e11ce-106">Microsoft Azure 媒體服務可讓您提供受 Widevine DRM 保護的 MPEG-DASH，其會依據「一般加密 (Common Encryption，CENC)」規格進行加密。</span><span class="sxs-lookup"><span data-stu-id="e11ce-106">Microsoft Azure Media Services enables you to deliver MPEG-DASH protected with Widevine DRM, which is encrypted per the Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="e11ce-107">從媒體服務 .NET SDK 版本 3.5.2 開始，媒體服務讓您可設定 Widevine 授權範本並取得 Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="e11ce-107">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="e11ce-108">您也可以使用下列 AMS 合作夥伴來協助您傳遞 Widevine 授權：[Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/)、[EZDRM](http://ezdrm.com/)、[castLabs](http://castlabs.com/company/partners/azure/)。</span><span class="sxs-lookup"><span data-stu-id="e11ce-108">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="e11ce-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="e11ce-109">castLabs</span></span>
<span data-ttu-id="e11ce-110">您可以使用 [castLabs](http://castlabs.com/company/partners/azure/) 傳遞 Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="e11ce-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) to deliver Widevine licenses.</span></span> <span data-ttu-id="e11ce-111">如需詳細資訊，請參閱 [使用 castLabs 將 DRM 授權傳遞到 Azure 媒體服務](media-services-castlabs-integration.md)</span><span class="sxs-lookup"><span data-stu-id="e11ce-111">For more information, see [Using castLabs to deliver DRM licenses to Azure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="e11ce-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="e11ce-112">Axinom</span></span>
<span data-ttu-id="e11ce-113">您可以使用 [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) 傳遞 Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="e11ce-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) to deliver Widevine licenses.</span></span> <span data-ttu-id="e11ce-114">如需詳細資訊，請參閱 [使用 Axinom 將 DRM 授權傳遞到 Azure 媒體服務](media-services-axinom-integration.md)</span><span class="sxs-lookup"><span data-stu-id="e11ce-114">For more information, see [Using Axinom to deliver DRM licenses to Azure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e11ce-115">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="e11ce-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e11ce-116">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e11ce-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="e11ce-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e11ce-117">See also</span></span>
[<span data-ttu-id="e11ce-118">使用 PlayReady 和/或 Widevine 動態一般加密</span><span class="sxs-lookup"><span data-stu-id="e11ce-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="e11ce-119">Mingfei 的部落格</span><span class="sxs-lookup"><span data-stu-id="e11ce-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

