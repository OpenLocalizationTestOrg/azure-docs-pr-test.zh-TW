---
title: "aaaEncode hello Azure 入口網站使用的媒體編碼器標準資產 |Microsoft 文件"
description: "本教學課程會引導您編碼資產 hello Azure 入口網站使用的媒體編碼器標準 hello 步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="31cc6-103">編碼資產 hello Azure 入口網站使用標準的媒體編碼器</span><span class="sxs-lookup"><span data-stu-id="31cc6-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="31cc6-104">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="31cc6-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="31cc6-105">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="31cc6-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="31cc6-106">當使用 Azure Media Services hello 最常見的案例之一傳遞彈性位元速率串流 tooyour 用戶端。</span><span class="sxs-lookup"><span data-stu-id="31cc6-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="31cc6-107">Media Services 支援下列彈性位元速率串流技術的 hello: HTTP Live Streaming (HLS)，Smooth Streaming、 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="31cc6-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="31cc6-108">tooprepare 視訊彈性位元速率串流，您需要 tooencode 您的來源視訊多位元速率檔案。</span><span class="sxs-lookup"><span data-stu-id="31cc6-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="31cc6-109">您應該使用 hello**媒體編碼器標準**編碼器 tooencode 視訊。</span><span class="sxs-lookup"><span data-stu-id="31cc6-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="31cc6-110">Media Services 也提供可讓您 toodeliver 動態封裝中遵循的串流格式 hello 您多位元速率 mp4 集： MPEG DASH、 HLS、 Smooth Streaming，不需要您 toore 封裝到這些資料流的格式。</span><span class="sxs-lookup"><span data-stu-id="31cc6-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="31cc6-111">使用動態封裝您只需要 toostore 及支付一種儲存格式，以及 Media Services 中的 hello 檔案將會建立及傳遞 hello 適當的回應，根據用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="31cc6-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="31cc6-112">tootake 利用動態封裝，您需要 tooencode 原始程式檔成一組多位元速率 MP4 檔案 （hello 編碼步驟會示範稍後這一節）。</span><span class="sxs-lookup"><span data-stu-id="31cc6-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="31cc6-113">tooscale 媒體處理，請參閱[這](media-services-portal-scale-media-processing.md)主題。</span><span class="sxs-lookup"><span data-stu-id="31cc6-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="31cc6-114">編碼以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="31cc6-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="31cc6-115">本章節描述 hello 步驟可讓您 tooencode 媒體編碼器標準內容。</span><span class="sxs-lookup"><span data-stu-id="31cc6-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="31cc6-116">在 [hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="31cc6-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="31cc6-117">在 [hello**設定**視窗中，選取**資產**。</span><span class="sxs-lookup"><span data-stu-id="31cc6-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="31cc6-118">在 [hello**資產**視窗中，您想要 tooencode 選取 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="31cc6-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="31cc6-119">按 hello**編碼**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31cc6-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="31cc6-120">在 [hello**編碼資產**視窗中選取 hello 「 媒體編碼器標準 」 的處理器，並預先設定。</span><span class="sxs-lookup"><span data-stu-id="31cc6-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="31cc6-121">如需預設值的相關資訊，請參閱[自動產生的位元速率排行榜](media-services-autogen-bitrate-ladder-with-mes.md)和 [MES 的工作預設值](media-services-mes-presets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="31cc6-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="31cc6-122">如果您打算使用的編碼預設 toocontrol，記住這： 請務必 tooselect hello 預先設定的最適合您輸入的視訊。</span><span class="sxs-lookup"><span data-stu-id="31cc6-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="31cc6-123">比方說，如果您知道輸入的視訊具有 1920 x 1080 像素的解析度，然後您可以使用 hello"H264 多重位元速率 1080p 」 預設。</span><span class="sxs-lookup"><span data-stu-id="31cc6-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="31cc6-124">如果您有低解析度 (640x360) 視訊，則不應該使用 [H264 多重位元速率 1080p] 預設值。</span><span class="sxs-lookup"><span data-stu-id="31cc6-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="31cc6-125">為了方便管理，您必須編輯 hello 名稱 hello 輸出資產，以及 hello hello 作業名稱的選項。</span><span class="sxs-lookup"><span data-stu-id="31cc6-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![為資產編碼](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="31cc6-127">按下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="31cc6-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="31cc6-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31cc6-128">Next step</span></span>
<span data-ttu-id="31cc6-129">中所述，您可以監視以 hello Azure 入口網站的編碼工作進度[這](media-services-portal-check-job-progress.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="31cc6-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="31cc6-130">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="31cc6-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="31cc6-131">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="31cc6-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

