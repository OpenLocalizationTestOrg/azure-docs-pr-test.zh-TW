---
title: "使用 Azure 媒體服務管理編碼的速度和並行 | Microsoft Docs"
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
ms.openlocfilehash: 0463904fd9bf1138587d0d214e572ddd38cc2184
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="aaa60-103">管理編碼的速度和並行</span><span class="sxs-lookup"><span data-stu-id="aaa60-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="aaa60-104">本文提供如何管理編碼作業/工作之速度和並行的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="aaa60-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="aaa60-105">概觀</span><span class="sxs-lookup"><span data-stu-id="aaa60-105">Overview</span></span>

<span data-ttu-id="aaa60-106">在媒體服務中，**保留單元類型**會決定媒體處理工作的處理速度。</span><span class="sxs-lookup"><span data-stu-id="aaa60-106">In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="aaa60-107">您可以選擇下列的保留單元類型：**S1**、**S2** 或 **S3**。</span><span class="sxs-lookup"><span data-stu-id="aaa60-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="aaa60-108">例如，在執行相同編碼作業的前提下，使用 **S2** 保留單元類型的速度會比 **S1** 類型快。</span><span class="sxs-lookup"><span data-stu-id="aaa60-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span> <span data-ttu-id="aaa60-109">[調整編碼單位](media-services-scale-media-processing-overview.md)主題所顯示的資料表可協助您在不同的編碼速度之間做出決定。</span><span class="sxs-lookup"><span data-stu-id="aaa60-109">The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="aaa60-110">除了指定保留單元類型之外，您還可以指定使用**保留單元**來佈建帳戶。</span><span class="sxs-lookup"><span data-stu-id="aaa60-110">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**.</span></span> <span data-ttu-id="aaa60-111">佈建的保留單元數目可決定指定帳戶中可同時處理的媒體工作數目。</span><span class="sxs-lookup"><span data-stu-id="aaa60-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="aaa60-112">例如，如果帳戶有五個保留單元，則只要有工作需要處理，就會同時執行五個媒體工作。</span><span class="sxs-lookup"><span data-stu-id="aaa60-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span></span> <span data-ttu-id="aaa60-113">剩餘的工作會在佇列中等待，當執行中的工作完成時，就循序地挑選來處理。</span><span class="sxs-lookup"><span data-stu-id="aaa60-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="aaa60-114">如果帳戶未佈建任何保留單元，則會循序地挑選工作。</span><span class="sxs-lookup"><span data-stu-id="aaa60-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="aaa60-115">在此情況下，一件工作完成與下一件工作開始之間的等待時間，視系統中的資源可用性而定。</span><span class="sxs-lookup"><span data-stu-id="aaa60-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span></span>

<span data-ttu-id="aaa60-116">如需說明如何調整編碼單位的詳細資訊及範例，請參閱[這個](media-services-scale-media-processing-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="aaa60-116">For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="aaa60-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aaa60-117">Next step</span></span>

[<span data-ttu-id="aaa60-118">調整編碼單位</span><span class="sxs-lookup"><span data-stu-id="aaa60-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="aaa60-119">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="aaa60-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="aaa60-120">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="aaa60-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

