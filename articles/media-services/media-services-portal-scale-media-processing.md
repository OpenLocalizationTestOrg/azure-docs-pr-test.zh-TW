---
title: "使用 Azure 入口網站調整媒體處理 | Microsoft Docs"
description: "本教學課程將逐步引導您完成使用 Azure 入口網站調整媒體處理的步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 46ca29d3e66701f2abcb185791089e94761984e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="change-the-reserved-unit-type"></a><span data-ttu-id="416a6-103">變更保留單元類型</span><span class="sxs-lookup"><span data-stu-id="416a6-103">Change the reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="416a6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="416a6-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="416a6-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="416a6-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="416a6-106">REST</span><span class="sxs-lookup"><span data-stu-id="416a6-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="416a6-107">Java</span><span class="sxs-lookup"><span data-stu-id="416a6-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="416a6-108">PHP</span><span class="sxs-lookup"><span data-stu-id="416a6-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="416a6-109">Overview</span><span class="sxs-lookup"><span data-stu-id="416a6-109">Overview</span></span>

<span data-ttu-id="416a6-110">媒體服務帳戶是與保留單元類型相關聯，後者決定媒體處理工作的速度。</span><span class="sxs-lookup"><span data-stu-id="416a6-110">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="416a6-111">您可以選擇下列的保留單元類型：**S1**、**S2** 或 **S3**。</span><span class="sxs-lookup"><span data-stu-id="416a6-111">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="416a6-112">例如，在執行相同編碼作業的前提下，使用 **S2** 保留單元類型的速度會比 **S1** 類型快。</span><span class="sxs-lookup"><span data-stu-id="416a6-112">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span>

<span data-ttu-id="416a6-113">除了指定保留單元類型之外，您還可以指定使用**保留單元** (RU) 來佈建帳戶。</span><span class="sxs-lookup"><span data-stu-id="416a6-113">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="416a6-114">佈建的 RU 數目可決定指定帳戶中可同時處理的媒體工作數目。</span><span class="sxs-lookup"><span data-stu-id="416a6-114">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="416a6-115">RU 用於平行化所有媒體處理，包括使用 Azure 媒體索引器的索引作業。</span><span class="sxs-lookup"><span data-stu-id="416a6-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="416a6-116">不過，與編碼不同，索引工作的處理速度不會因為使用較快的保留單元而變快。</span><span class="sxs-lookup"><span data-stu-id="416a6-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="416a6-117">請務必檢閱 [概觀](media-services-scale-media-processing-overview.md) 主題，以取得調整媒體處理主題的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="416a6-117">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="416a6-118">調整媒體處理</span><span class="sxs-lookup"><span data-stu-id="416a6-118">Scale media processing</span></span>
<span data-ttu-id="416a6-119">若要變更保留單元類型以及保留單元數目，請執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="416a6-119">To change the reserved unit type and the number of reserved units, do the following:</span></span>

1. <span data-ttu-id="416a6-120">在 [Azure 入口網站](https://portal.azure.com/)中，選取您的 Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="416a6-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="416a6-121">在 [設定] 視窗中，選取 [媒體保留單元]。</span><span class="sxs-lookup"><span data-stu-id="416a6-121">In the **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="416a6-122">若要變更所選取保留單元類型的保留單元數目，請使用 [媒體保留單元]  滑桿。</span><span class="sxs-lookup"><span data-stu-id="416a6-122">To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="416a6-123">若要變更 **保留單元類型**，請按 [S1]、[S2] 或 [S3]。</span><span class="sxs-lookup"><span data-stu-id="416a6-123">To change the **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Processors page](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="416a6-125">按 [儲存] 以儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="416a6-125">Press the SAVE button to save your changes.</span></span>
   
    <span data-ttu-id="416a6-126">新的保留單元會在您按 [儲存] 後配置。</span><span class="sxs-lookup"><span data-stu-id="416a6-126">The new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="416a6-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="416a6-127">Next steps</span></span>
<span data-ttu-id="416a6-128">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="416a6-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="416a6-129">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="416a6-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

