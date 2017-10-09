---
title: "處理使用 aaaScale 媒體 hello Azure 入口網站 |Microsoft 文件"
description: "本教學課程會引導您完成處理使用 hello Azure 入口網站的調整 media hello 步驟。"
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
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a><span data-ttu-id="61fa0-103">變更 hello 保留單位類型</span><span class="sxs-lookup"><span data-stu-id="61fa0-103">Change hello reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="61fa0-104">.NET</span><span class="sxs-lookup"><span data-stu-id="61fa0-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="61fa0-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="61fa0-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="61fa0-106">REST</span><span class="sxs-lookup"><span data-stu-id="61fa0-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="61fa0-107">Java</span><span class="sxs-lookup"><span data-stu-id="61fa0-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="61fa0-108">PHP</span><span class="sxs-lookup"><span data-stu-id="61fa0-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="61fa0-109">概觀</span><span class="sxs-lookup"><span data-stu-id="61fa0-109">Overview</span></span>

<span data-ttu-id="61fa0-110">Media Services 帳戶會決定 hello 速度與媒體處理工作會處理保留單位類型相關聯。</span><span class="sxs-lookup"><span data-stu-id="61fa0-110">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="61fa0-111">您可以挑選之間 hello 下列保留單位類型： **S1**， **S2**，或**S3**。</span><span class="sxs-lookup"><span data-stu-id="61fa0-111">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="61fa0-112">例如，當您使用 hello 相同的編碼工作執行速度的 hello **S2**保留的單位類型比較 toohello **S1**型別。</span><span class="sxs-lookup"><span data-stu-id="61fa0-112">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

<span data-ttu-id="61fa0-113">此外 toospecifying hello 保留單位類型，您可以指定 tooprovision 您帳戶的**保留單位**(RUs)。</span><span class="sxs-lookup"><span data-stu-id="61fa0-113">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="61fa0-114">佈建之俄文的 hello 數目會決定 hello 可以指定帳戶中並行處理的媒體工作數目。</span><span class="sxs-lookup"><span data-stu-id="61fa0-114">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="61fa0-115">RU 用於平行化所有媒體處理，包括使用 Azure 媒體索引器的索引作業。</span><span class="sxs-lookup"><span data-stu-id="61fa0-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="61fa0-116">不過，與編碼不同，索引工作的處理速度不會因為使用較快的保留單元而變快。</span><span class="sxs-lookup"><span data-stu-id="61fa0-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61fa0-117">請確定 tooreview hello[概觀](media-services-scale-media-processing-overview.md)主題 tooget 調整媒體處理主題的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="61fa0-117">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="61fa0-118">調整媒體處理</span><span class="sxs-lookup"><span data-stu-id="61fa0-118">Scale media processing</span></span>
<span data-ttu-id="61fa0-119">toochange hello 保留單位類型和 hello 保留單位數目，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="61fa0-119">toochange hello reserved unit type and hello number of reserved units, do hello following:</span></span>

1. <span data-ttu-id="61fa0-120">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="61fa0-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="61fa0-121">在 hello**設定**視窗中，選取**媒體保留單位**。</span><span class="sxs-lookup"><span data-stu-id="61fa0-121">In hello **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="61fa0-122">hello 的保留單元 toochange hello 數目選取保留的單位類型，請使用 hello**媒體服務單位**滑桿。</span><span class="sxs-lookup"><span data-stu-id="61fa0-122">toochange hello number of reserved units for hello selected reserved unit type, use hello **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="61fa0-123">toochange hello**保留單位類型**，請按 S1、 S2 或 S3。</span><span class="sxs-lookup"><span data-stu-id="61fa0-123">toochange hello **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Processors page](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="61fa0-125">按 hello 儲存按鈕 toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="61fa0-125">Press hello SAVE button toosave your changes.</span></span>
   
    <span data-ttu-id="61fa0-126">當您按下 儲存配置 hello 新保留的單位。</span><span class="sxs-lookup"><span data-stu-id="61fa0-126">hello new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61fa0-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61fa0-127">Next steps</span></span>
<span data-ttu-id="61fa0-128">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="61fa0-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="61fa0-129">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="61fa0-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

