---
title: "aaa 管理速度和並行的編碼方式，透過 Azure Media Services |Microsoft 文件"
description: "本文提供如何使用 Azure 媒體服務管理編碼作業/工作之速度和並行的簡短概觀。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="3d023-103">管理編碼的速度和並行</span><span class="sxs-lookup"><span data-stu-id="3d023-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="3d023-104">本文提供如何管理編碼作業/工作之速度和並行的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="3d023-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="3d023-105">概觀</span><span class="sxs-lookup"><span data-stu-id="3d023-105">Overview</span></span>

<span data-ttu-id="3d023-106">在 Media Services**保留單位類型**決定 hello 與媒體處理工作會處理的速度。</span><span class="sxs-lookup"><span data-stu-id="3d023-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="3d023-107">您可以挑選之間 hello 下列保留單位類型： **S1**， **S2**，或**S3**。</span><span class="sxs-lookup"><span data-stu-id="3d023-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="3d023-108">例如，當您使用 hello 相同的編碼工作執行速度的 hello **S2**保留的單位類型比較 toohello **S1**型別。</span><span class="sxs-lookup"><span data-stu-id="3d023-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="3d023-109">hello[調整編碼單元](media-services-scale-media-processing-overview.md)主題說明可協助您做出決策選擇不同的編碼速度時的資料表。</span><span class="sxs-lookup"><span data-stu-id="3d023-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="3d023-110">此外 toospecifying hello 保留單位類型，您可以指定 tooprovision 您帳戶的**保留單位**。</span><span class="sxs-lookup"><span data-stu-id="3d023-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="3d023-111">hello 佈建的保留單元數目決定 hello 可以指定帳戶中並行處理的媒體工作數目。</span><span class="sxs-lookup"><span data-stu-id="3d023-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="3d023-112">例如，如果您的帳戶有五個媒體工作將會執行同時只要 5 個保留的單位，為有工作 toobe 處理。</span><span class="sxs-lookup"><span data-stu-id="3d023-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="3d023-113">hello 其餘的工作會在 hello 佇列中等候，而且會取得收取正在執行的工作完成時，依序處理。</span><span class="sxs-lookup"><span data-stu-id="3d023-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="3d023-114">如果帳戶未佈建任何保留單元，則會循序地挑選工作。</span><span class="sxs-lookup"><span data-stu-id="3d023-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="3d023-115">在此情況下，hello 之間的等候時間一個工作完成並 hello 一開始會相依於資源的 hello 可用性 hello 系統中。</span><span class="sxs-lookup"><span data-stu-id="3d023-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="3d023-116">詳細的資訊和範例，顯示如何 tooscale 編碼單元，請參閱[這](media-services-scale-media-processing-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="3d023-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="3d023-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d023-117">Next step</span></span>

[<span data-ttu-id="3d023-118">調整編碼單位</span><span class="sxs-lookup"><span data-stu-id="3d023-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="3d023-119">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="3d023-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3d023-120">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="3d023-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

