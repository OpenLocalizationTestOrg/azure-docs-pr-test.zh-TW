---
title: "檢視 Azure DevTest Labs 中的每月估計實驗室成本趨勢 | Microsoft Docs"
description: "了解 Azure DevTest Labs 每月估計成本趨勢圖表。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: b3ad1ead522908d4b41b7cca98d20ac91664998e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="5d517-103">檢視 Azure DevTest Labs 中的每月估計實驗室成本趨勢</span><span class="sxs-lookup"><span data-stu-id="5d517-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="5d517-104">研測實驗室的成本管理功能可協助您追蹤實驗室成本。</span><span class="sxs-lookup"><span data-stu-id="5d517-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="5d517-105">本文會示範如何使用「每月估計成本趨勢」  圖表，來檢視目前日曆月份的到目前為止的估計成本，以及目前日曆月份的預計月底成本。</span><span class="sxs-lookup"><span data-stu-id="5d517-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="5d517-106">在本文中，您將學習如何在 Azure 入口網站中檢視每月估計成本趨勢圖表。</span><span class="sxs-lookup"><span data-stu-id="5d517-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="5d517-107">檢視每月估計成本趨勢圖表</span><span class="sxs-lookup"><span data-stu-id="5d517-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="5d517-108">若要檢視「每月估計成本趨勢」圖表，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="5d517-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="5d517-109">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="5d517-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="5d517-110">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="5d517-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="5d517-111">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="5d517-111">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="5d517-112">在實驗室的刀鋒視窗上，選取 [成本設定] 。</span><span class="sxs-lookup"><span data-stu-id="5d517-112">On the lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="5d517-113">在實驗室的 [成本設定] 刀鋒視窗中，選取 [實驗室成本趨勢]。</span><span class="sxs-lookup"><span data-stu-id="5d517-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="5d517-114">下列螢幕擷取畫面顯示成本圖表範例。</span><span class="sxs-lookup"><span data-stu-id="5d517-114">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![成本圖表](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="5d517-116">**估計成本** 值是到目前行事曆月份為止累計的預估成本。</span><span class="sxs-lookup"><span data-stu-id="5d517-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="5d517-117">**預計成本** 是目前行事曆月份整個月的估計成本，是以前五天的實驗室成本來計算。</span><span class="sxs-lookup"><span data-stu-id="5d517-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="5d517-118">成本金額會無條件進位到下一個整數。</span><span class="sxs-lookup"><span data-stu-id="5d517-118">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="5d517-119">例如：</span><span class="sxs-lookup"><span data-stu-id="5d517-119">For example:</span></span> 

* <span data-ttu-id="5d517-120">5.01 會無條件進位到 6</span><span class="sxs-lookup"><span data-stu-id="5d517-120">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="5d517-121">5.50 會無條件進位到 6</span><span class="sxs-lookup"><span data-stu-id="5d517-121">5.50 rounds up to 6</span></span>
* <span data-ttu-id="5d517-122">5.99 會無條件進位到 6</span><span class="sxs-lookup"><span data-stu-id="5d517-122">5.99 rounds up to 6</span></span>

<span data-ttu-id="5d517-123">如圖表上方所述，您在圖表中看到的成本是使用[隨用隨付](https://azure.microsoft.com/offers/ms-azr-0003p/)優惠費率的*估計*成本。</span><span class="sxs-lookup"><span data-stu-id="5d517-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="5d517-124">此外，以下「未」  併入成本計算︰</span><span class="sxs-lookup"><span data-stu-id="5d517-124">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="5d517-125">目前不支援 CSP 和 Dreamspark 訂用帳戶，因為 Azure DevTest Labs 使用 [Azure 計費 API](../billing/billing-usage-rate-card-overview.md) 來計算實驗室成本，而 Azure 計費 API 並不支援 CSP 或 Dreamspark 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d517-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="5d517-126">您的優惠費率。</span><span class="sxs-lookup"><span data-stu-id="5d517-126">Your offer rates.</span></span> <span data-ttu-id="5d517-127">目前，我們無法使用您與 Microsoft 或 Microsoft 合作夥伴協議的優惠費率 (顯示於您的訂用帳戶下方)。</span><span class="sxs-lookup"><span data-stu-id="5d517-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="5d517-128">我們將使用隨用隨付費率。</span><span class="sxs-lookup"><span data-stu-id="5d517-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="5d517-129">您的稅率</span><span class="sxs-lookup"><span data-stu-id="5d517-129">Your taxes</span></span>
* <span data-ttu-id="5d517-130">您的折扣</span><span class="sxs-lookup"><span data-stu-id="5d517-130">Your discounts</span></span>
* <span data-ttu-id="5d517-131">您的帳單貨幣。</span><span class="sxs-lookup"><span data-stu-id="5d517-131">Your billing currency.</span></span> <span data-ttu-id="5d517-132">目前，實驗室成本只會以美元貨幣顯示。</span><span class="sxs-lookup"><span data-stu-id="5d517-132">Currently, the lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="5d517-133">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="5d517-133">Related blog posts</span></span>
* [<span data-ttu-id="5d517-134">讓 DevTest Labs 成本不失控的另外兩項須知</span><span class="sxs-lookup"><span data-stu-id="5d517-134">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="5d517-135">為何要設定成本臨界值？</span><span class="sxs-lookup"><span data-stu-id="5d517-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="5d517-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d517-136">Next steps</span></span>
<span data-ttu-id="5d517-137">以下是接下來要嘗試的一些事項：</span><span class="sxs-lookup"><span data-stu-id="5d517-137">Here are some things to try next:</span></span>

* <span data-ttu-id="5d517-138">[定義實驗室原則](devtest-lab-set-lab-policy.md) - 了解如何設定用來管理您實驗室及其 VM 使用方式的各種原則。</span><span class="sxs-lookup"><span data-stu-id="5d517-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="5d517-139">[建立自訂映像](devtest-lab-create-template.md) - 當您建立 VM 時，您要指定一個基本映像，它可以是自訂映像或 Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="5d517-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="5d517-140">本文會示範如何從 VHD 檔案建立自訂的映像。</span><span class="sxs-lookup"><span data-stu-id="5d517-140">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="5d517-141">[設定 Marketplace 映像](devtest-lab-configure-marketplace-images.md) - DevTest Labs 支援根據 Azure Marketplace 映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="5d517-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="5d517-142">本文會示範在實驗室中建立 VM 時，如何指定可以使用哪些 Azure Marketplace 映像 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="5d517-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="5d517-143">[在實驗室中建立 VM](devtest-lab-add-vm-with-artifacts.md) - 示範如何從基本映像 (自訂或 Marketplace) 建立 VM，以及如何使用 VM 中的構件。</span><span class="sxs-lookup"><span data-stu-id="5d517-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

