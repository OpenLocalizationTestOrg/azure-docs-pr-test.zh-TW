---
title: "透過 Azure 入口網站調整串流端點 | Microsoft Docs"
description: "本教學課程將逐步引導您完成使用 Azure 入口網站調整串流端點的步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 4bb891371e3fc802fa667688a88878db18e32422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="862e0-103">透過 Azure 入口網站調整串流端點</span><span class="sxs-lookup"><span data-stu-id="862e0-103">Scale streaming endpoints with the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="862e0-104">概觀</span><span class="sxs-lookup"><span data-stu-id="862e0-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="862e0-105">若要完成此教學課程，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="862e0-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="862e0-106">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="862e0-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="862e0-107">**進階**串流端點適合進階工作，提供專用並能靈活調整的頻寬容量。</span><span class="sxs-lookup"><span data-stu-id="862e0-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="862e0-108">擁有**進階**串流端點的客戶預設會取得一個串流單位 (SU)。</span><span class="sxs-lookup"><span data-stu-id="862e0-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="862e0-109">藉由新增 SU 可以調整串流端點。</span><span class="sxs-lookup"><span data-stu-id="862e0-109">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="862e0-110">每個 SU 可為應用程式提供額外的頻寬容量。</span><span class="sxs-lookup"><span data-stu-id="862e0-110">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="862e0-111">如需有關串流端點類型和 CDN 組態的詳細資訊，請參閱[串流端點概觀](media-services-portal-manage-streaming-endpoints.md)主題。</span><span class="sxs-lookup"><span data-stu-id="862e0-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="862e0-112">本主題說明如何調整串流端點。</span><span class="sxs-lookup"><span data-stu-id="862e0-112">This topic shows how to scale a streaming endpoint.</span></span>

<span data-ttu-id="862e0-113">如需定價詳細資料的相關資訊，請參閱＜ [媒體服務定價詳細資料](http://go.microsoft.com/fwlink/?LinkId=275107)＞。</span><span class="sxs-lookup"><span data-stu-id="862e0-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="862e0-114">調整串流端點</span><span class="sxs-lookup"><span data-stu-id="862e0-114">Scale streaming endpoints</span></span>

<span data-ttu-id="862e0-115">若要變更串流端點的數目，請執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="862e0-115">To change the number of streaming units, do the following:</span></span>

1. <span data-ttu-id="862e0-116">在 [Azure 入口網站](https://portal.azure.com/)中，選取您的 Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="862e0-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="862e0-117">在 [設定] 視窗中，選取 [串流端點]。</span><span class="sxs-lookup"><span data-stu-id="862e0-117">In the **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="862e0-118">按一下您要調整的串流端點。</span><span class="sxs-lookup"><span data-stu-id="862e0-118">Click on the streaming endpoint that you want to scale.</span></span> 

    [!NOTE] <span data-ttu-id="862e0-119">您只能調整 [Premium] \(進階\) 串流端點。</span><span class="sxs-lookup"><span data-stu-id="862e0-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="862e0-120">移動滑桿以指定資料流處理單位的數目。</span><span class="sxs-lookup"><span data-stu-id="862e0-120">Move the slider to specify the number of streaming units.</span></span>

    ![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="862e0-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="862e0-122">Next steps</span></span>
<span data-ttu-id="862e0-123">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="862e0-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="862e0-124">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="862e0-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

