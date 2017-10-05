---
title: "透過 Azure 入口網站使用媒體編碼器標準為資產編碼 | Microsoft Docs"
description: "本教學課程將逐步引導您完成透過 Azure 入口網站使用 Media Encoder Standard 為資產編碼的步驟。"
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
ms.openlocfilehash: a299245e285c4caa68988b184799cd6f4d13e080
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a><span data-ttu-id="5f7ce-103">透過 Azure 入口網站使用 Media Encoder Standard 為資產編碼</span><span class="sxs-lookup"><span data-stu-id="5f7ce-103">Encode an asset using Media Encoder Standard with the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="5f7ce-104">若要完成此教學課程，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5f7ce-105">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="5f7ce-106">使用 Azure 媒體服務時，其中一個最常見案例是提供自適性串流給您的用戶端。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-106">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="5f7ce-107">媒體服務支援下列自適性串流技術：HTTP 即時串流 (HLS)、Smooth Streaming、MPEG DAS。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-107">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="5f7ce-108">若要針對自適性串流準備您的視訊，您必須將來源視訊編碼為多位元速率檔案。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-108">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="5f7ce-109">您應該使用 [媒體編碼器標準]  編碼器來為您的視訊編碼。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-109">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="5f7ce-110">媒體服務提供動態封裝，這讓您以下列串流格式 (MPEG DASH、HLS、Smooth Streaming) 提供多位元速率 MP4，而不必重新封裝成這些串流格式。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-110">Media Services also provides dynamic packaging which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to re-package into these streaming formats.</span></span> <span data-ttu-id="5f7ce-111">使用動態封裝，您只需要以單一儲存格式儲存及播放檔案，媒體服務會根據來自用戶端的要求建置及傳遞適當的回應。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-111">With dynamic packaging you only need to store and pay for the files in single storage format and Media Services will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="5f7ce-112">若要利用動態封裝功能，將您的來源檔編碼為一組多位元速率 MP4 檔案 (編碼步驟稍後示範於本節中)。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-112">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="5f7ce-113">若要調整媒體處理，請參閱 [這個](media-services-portal-scale-media-processing.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-113">To scale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-the-azure-portal"></a><span data-ttu-id="5f7ce-114">使用 Azure 入口網站進行編碼</span><span class="sxs-lookup"><span data-stu-id="5f7ce-114">Encode with the Azure portal</span></span>
<span data-ttu-id="5f7ce-115">本節說明當您利用媒體編碼器標準為您的內容編碼時，可以採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-115">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="5f7ce-116">在 [Azure 入口網站](https://portal.azure.com/)中，選取您的 Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="5f7ce-117">在 [設定] 視窗中，選取 [資產]。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-117">In the **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="5f7ce-118">在 [資產]  視窗中，選取您想要編碼的資產。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-118">In the **Assets** window, select the asset that you would like to encode.</span></span>
4. <span data-ttu-id="5f7ce-119">按 [編碼]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-119">Press the **Encode** button.</span></span>
5. <span data-ttu-id="5f7ce-120">在 [為資產編碼]  視窗中，選取 [媒體編碼器標準] 處理器和預設值。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-120">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="5f7ce-121">如需預設值的相關資訊，請參閱[自動產生的位元速率排行榜](media-services-autogen-bitrate-ladder-with-mes.md)和 [MES 的工作預設值](media-services-mes-presets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="5f7ce-122">如果您打算控制所要使用的編碼預設值，請記住：務必選取最適合您輸入視訊的預設值。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-122">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="5f7ce-123">例如，如果您知道您的輸入視訊的解析度為 1920x1080 像素，您則可使用 [H264 多位元速率 1080p] 預設值。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="5f7ce-124">如果您有低解析度 (640x360) 視訊，則不應該使用 [H264 多重位元速率 1080p] 預設值。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="5f7ce-125">為了方便管理，您可以選擇編輯輸出資產的名稱和作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-125">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![為資產編碼](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="5f7ce-127">按下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="5f7ce-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f7ce-128">Next step</span></span>
<span data-ttu-id="5f7ce-129">您可以透過 Azure 入口網站監視編碼作業進度，如 [這篇](media-services-portal-check-job-progress.md) 文章所述。</span><span class="sxs-lookup"><span data-stu-id="5f7ce-129">You can monitor encoding job progress with the Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="5f7ce-130">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="5f7ce-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5f7ce-131">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="5f7ce-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

