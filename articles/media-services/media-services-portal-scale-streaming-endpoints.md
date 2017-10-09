---
title: "aaaScale 串流端點，其中包含 hello Azure 入口網站 |Microsoft 文件"
description: "本教學課程會引導您 hello 步驟調整串流端點，其中包含 hello Azure 入口網站。"
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
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="0c73d-103">調整串流端點，其中包含 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0c73d-103">Scale streaming endpoints with hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="0c73d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0c73d-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="0c73d-105">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c73d-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="0c73d-106">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="0c73d-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="0c73d-107">**進階**串流端點適合進階工作，提供專用並能靈活調整的頻寬容量。</span><span class="sxs-lookup"><span data-stu-id="0c73d-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="0c73d-108">擁有**進階**串流端點的客戶預設會取得一個串流單位 (SU)。</span><span class="sxs-lookup"><span data-stu-id="0c73d-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="0c73d-109">可以藉由新增 SUs 調整串流端點的 hello。</span><span class="sxs-lookup"><span data-stu-id="0c73d-109">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="0c73d-110">每個 SU 提供額外的頻寬容量 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c73d-110">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="0c73d-111">如需有關資料流端點類型及 CDN 組態的詳細資訊，請參閱 hello[串流端點概觀](media-services-portal-manage-streaming-endpoints.md)主題。</span><span class="sxs-lookup"><span data-stu-id="0c73d-111">For more information about streaming endpoint types and CDN configuration, see hello [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="0c73d-112">本主題說明如何 tooscale 串流端點。</span><span class="sxs-lookup"><span data-stu-id="0c73d-112">This topic shows how tooscale a streaming endpoint.</span></span>

<span data-ttu-id="0c73d-113">如需定價詳細資料的相關資訊，請參閱＜ [媒體服務定價詳細資料](http://go.microsoft.com/fwlink/?LinkId=275107)＞。</span><span class="sxs-lookup"><span data-stu-id="0c73d-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="0c73d-114">調整串流端點</span><span class="sxs-lookup"><span data-stu-id="0c73d-114">Scale streaming endpoints</span></span>

<span data-ttu-id="0c73d-115">資料流處理單位，toochange hello 數目不要 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="0c73d-115">toochange hello number of streaming units, do hello following:</span></span>

1. <span data-ttu-id="0c73d-116">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c73d-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="0c73d-117">在 hello**設定**視窗中，選取**串流端點**。</span><span class="sxs-lookup"><span data-stu-id="0c73d-117">In hello **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="0c73d-118">按一下您想 tooscale hello 串流端點。</span><span class="sxs-lookup"><span data-stu-id="0c73d-118">Click on hello streaming endpoint that you want tooscale.</span></span> 

    [!NOTE] <span data-ttu-id="0c73d-119">您只能調整 [Premium] \(進階\) 串流端點。</span><span class="sxs-lookup"><span data-stu-id="0c73d-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="0c73d-120">移動 hello 滑桿 toospecify hello 資料流單位數目。</span><span class="sxs-lookup"><span data-stu-id="0c73d-120">Move hello slider toospecify hello number of streaming units.</span></span>

    ![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="0c73d-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c73d-122">Next steps</span></span>
<span data-ttu-id="0c73d-123">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="0c73d-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0c73d-124">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="0c73d-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

