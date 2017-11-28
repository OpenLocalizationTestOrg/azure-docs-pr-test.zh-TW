---
title: "透過 StorSimple 裝置管理員記錄支援票證 | Microsoft Docs"
description: "描述 StorSimple 裝置管理員診斷功能，並說明如何使用它來針對 StorSimple Virtual Array 進行疑難排解。"
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a0c394df-957b-49b3-a283-38824f8847fd
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 658afbc178814389fefd7941e2ca030741bd08e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-log-a-support-request-for-the-storsimple-virtual-array"></a><span data-ttu-id="67a1d-103">使用 StorSimple 裝置管理員服務來登錄 StorSimple Virtual Array 的支援要求</span><span class="sxs-lookup"><span data-stu-id="67a1d-103">Use the StorSimple Device Manager service to log a Support request for the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="67a1d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="67a1d-104">Overview</span></span>

<span data-ttu-id="67a1d-105">StorSimple 裝置管理員可讓您在服務摘要刀鋒視窗中**登錄新的支援要求**。</span><span class="sxs-lookup"><span data-stu-id="67a1d-105">The StorSimple Device Manager provides the capability to **log a new support request** within the service summary blade.</span></span> <span data-ttu-id="67a1d-106">本文說明如何從入口網站登錄新的支援要求並管理其生命週期。</span><span class="sxs-lookup"><span data-stu-id="67a1d-106">This article explains how you can log a new support request and manage its lifecycle from within the portal.</span></span>

## <a name="new-support-request"></a><span data-ttu-id="67a1d-107">新的支援要求</span><span class="sxs-lookup"><span data-stu-id="67a1d-107">New support request</span></span>

<span data-ttu-id="67a1d-108">視您的[支援方案](https://azure.microsoft.com/support/plans/)而定，您可以直接從 StorSimple 裝置管理員服務摘要刀鋒視窗中，針對 StorSimple Virtual Array 的問題建立支援票證。</span><span class="sxs-lookup"><span data-stu-id="67a1d-108">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple Virtual array directly from the StorSimple Device Manager service summary blade.</span></span>

#### <a name="to-log-a-new-request"></a><span data-ttu-id="67a1d-109">若要登錄新的要求</span><span class="sxs-lookup"><span data-stu-id="67a1d-109">To log a new request</span></span>

1. <span data-ttu-id="67a1d-110">移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="67a1d-110">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="67a1d-111">在服務摘要刀鋒視窗的設定中，移至 [支援 + 疑難排解] 區段，然後按一下 [新增支援要求]。</span><span class="sxs-lookup"><span data-stu-id="67a1d-111">In the service summary blade settings, go to **SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
   
    ![新的支援要求](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket1.png)

2. <span data-ttu-id="67a1d-113">在 [基本] 刀鋒視窗上，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="67a1d-113">In the **Basics** blade, do the following:</span></span>

    1. <span data-ttu-id="67a1d-114">從 [問題類型] 下拉式清單中，選取 [技術]。</span><span class="sxs-lookup"><span data-stu-id="67a1d-114">From the **Issue type** dropdown list, select **Technical**.</span></span> 
    
    2. <span data-ttu-id="67a1d-115">自動會選擇目前的 [訂用帳戶]、[服務] 類型和 [資源] \(StorSimple 裝置管理員服務)。</span><span class="sxs-lookup"><span data-stu-id="67a1d-115">The current **Subscription**, **Service** type, and the **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 

    3. <span data-ttu-id="67a1d-116">指定一或多個已向服務註冊的有問題裝置。</span><span class="sxs-lookup"><span data-stu-id="67a1d-116">Specify one or more devices registered to your service that are experiencing issues.</span></span>

    4. <span data-ttu-id="67a1d-117">如果您的訂用帳戶有多個相關聯的方案，請選擇適當的**支援方案**。</span><span class="sxs-lookup"><span data-stu-id="67a1d-117">Choose an appropriate **support plan** if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="67a1d-118">您必須已付費購買支援方案，才能啟用技術支援。</span><span class="sxs-lookup"><span data-stu-id="67a1d-118">You need a paid support plan to enable Technical Support.</span></span>

3. <span data-ttu-id="67a1d-119">在**步驟 2** 中，選擇 [嚴重性]，並指定問題是與陣列還是 StorSimple 裝置管理員服務有關。</span><span class="sxs-lookup"><span data-stu-id="67a1d-119">In **Step 2**, choose the **Severity** and specify if the issue is related to the array or the StorSimple Device Manager service.</span></span> <span data-ttu-id="67a1d-120">同時，選擇這個問題的 [類別]，並提供問題的其他 [詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="67a1d-120">Also, choose a **Category** for this issue and provide more **Details** about the issue.</span></span>
   
    ![新的支援要求](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket2.png)

4. <span data-ttu-id="67a1d-122">在**步驟 3** 中，提供您的連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="67a1d-122">In **Step 3**, provide your contact information.</span></span> <span data-ttu-id="67a1d-123">Microsoft 支援服務會利用此資訊來連絡您，以取得進一步資訊、進行診斷及解決。</span><span class="sxs-lookup"><span data-stu-id="67a1d-123">Microsoft Support will use this information to reach out to you for further information, diagnosis, and resolution.</span></span>
   
    ![新的支援要求](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket3.png)

## <a name="manage-a-support-request"></a><span data-ttu-id="67a1d-125">管理支援要求</span><span class="sxs-lookup"><span data-stu-id="67a1d-125">Manage a support request</span></span>

<span data-ttu-id="67a1d-126">建立支援票證之後，您便可以從入口網站中管理票證的生命週期。</span><span class="sxs-lookup"><span data-stu-id="67a1d-126">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span>

#### <a name="to-manage-your-support-requests"></a><span data-ttu-id="67a1d-127">若要管理支援要求</span><span class="sxs-lookup"><span data-stu-id="67a1d-127">To manage your support requests</span></span>

<span data-ttu-id="67a1d-128">若要移至說明和支援頁面，請瀏覽至 [瀏覽] > [說明 + 支援]。</span><span class="sxs-lookup"><span data-stu-id="67a1d-128">To get to the help and support page, navigate to **Browse > Help + support**.</span></span>

![管理支援要求](./media/storsimple-virtual-array-log-support-ticket/manage-support-tickets.png)

## <a name="next-steps"></a><span data-ttu-id="67a1d-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67a1d-130">Next steps</span></span>

<span data-ttu-id="67a1d-131">了解如何[診斷並解決 StorSimple Virtual Array 的相關問題](storsimple-virtual-array-diagnose-problems.md)</span><span class="sxs-lookup"><span data-stu-id="67a1d-131">Learn how to [diagnose and solve problems related to your StorSimple Virtual array](storsimple-virtual-array-diagnose-problems.md)</span></span>

