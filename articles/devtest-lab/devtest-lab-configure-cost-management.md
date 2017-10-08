---
title: "aaaView hello 每月實驗室估計的成本趨勢 Azure DevTest Labs |Microsoft 文件"
description: "深入了解 hello Azure DevTest Labs 每月估計的成本趨勢圖。"
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
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="7f226-103">檢視 hello 每月實驗室估計的成本趨勢 Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="7f226-103">View hello monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="7f226-104">DevTest Labs hello 成本管理功能可協助您追蹤您的實驗室 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="7f226-104">hello Cost Management feature of DevTest Labs helps you track hello cost of your lab.</span></span> <span data-ttu-id="7f226-105">本文將說明如何 toouse hello**每月估計成本趨勢**圖表 tooview hello 行事曆月份的預估的成本與日期和月份 hello hello 規劃的結束月份的成本。</span><span class="sxs-lookup"><span data-stu-id="7f226-105">This article illustrates how toouse hello **Monthly Estimated Cost Trend** chart tooview hello current calendar month's estimated cost-to-date and hello projected end-of-month cost for hello current calendar month.</span></span> <span data-ttu-id="7f226-106">在本文中，您學會如何 tooview hello hello Azure 入口網站中的每月估計的成本趨勢圖。</span><span class="sxs-lookup"><span data-stu-id="7f226-106">In this article, you learn how tooview hello monthly estimated cost trend chart in hello Azure portal.</span></span>

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="7f226-107">檢視 hello 每月估計成本趨勢圖表</span><span class="sxs-lookup"><span data-stu-id="7f226-107">Viewing hello Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="7f226-108">tooview hello 每月估計成本趨勢圖表，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7f226-108">tooview hello Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="7f226-109">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="7f226-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="7f226-110">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="7f226-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="7f226-111">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="7f226-111">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="7f226-112">在 hello 實驗室刀鋒視窗中，選取 **成本設定**。</span><span class="sxs-lookup"><span data-stu-id="7f226-112">On hello lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="7f226-113">在 hello 實驗室**成本設定**刀鋒視窗中，選取**實驗室成本趨勢**。</span><span class="sxs-lookup"><span data-stu-id="7f226-113">On hello lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="7f226-114">hello 下列螢幕擷取畫面顯示成本圖表的範例。</span><span class="sxs-lookup"><span data-stu-id="7f226-114">hello following screen shot shows an example of a cost chart.</span></span> 
   
    ![成本圖表](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="7f226-116">hello**估計成本**值為 hello 行事曆月份的預估的成本與日期。</span><span class="sxs-lookup"><span data-stu-id="7f226-116">hello **Estimated cost** value is hello current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="7f226-117">hello**預計成本**hello 估計的成本 hello 整個目前的日曆月份中，使用計算 hello 實驗室成本 hello 前五天。</span><span class="sxs-lookup"><span data-stu-id="7f226-117">hello **Projected cost** is hello estimated cost for hello entire current calendar month, calculated using hello lab cost for hello previous five days.</span></span>

<span data-ttu-id="7f226-118">hello 成本金額會無條件進位 toohello 下一個整數。</span><span class="sxs-lookup"><span data-stu-id="7f226-118">hello cost amounts are rounded up toohello next whole number.</span></span> <span data-ttu-id="7f226-119">例如：</span><span class="sxs-lookup"><span data-stu-id="7f226-119">For example:</span></span> 

* <span data-ttu-id="7f226-120">5.01 會無條件進位 too6</span><span class="sxs-lookup"><span data-stu-id="7f226-120">5.01 rounds up too6</span></span> 
* <span data-ttu-id="7f226-121">5.50 too6 向上四捨五入</span><span class="sxs-lookup"><span data-stu-id="7f226-121">5.50 rounds up too6</span></span>
* <span data-ttu-id="7f226-122">5.99 會無條件進位 too6</span><span class="sxs-lookup"><span data-stu-id="7f226-122">5.99 rounds up too6</span></span>

<span data-ttu-id="7f226-123">指出 hello 圖表之上，即在 hello 圖表中的 hello 成本是*估計*成本使用[隨用隨付](https://azure.microsoft.com/offers/ms-azr-0003p/)提供率。</span><span class="sxs-lookup"><span data-stu-id="7f226-123">As it states above hello chart, hello costs you see in hello chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="7f226-124">此外，hello 如下*不*納入成本計算 hello:</span><span class="sxs-lookup"><span data-stu-id="7f226-124">Additionally, hello following are *not* included in hello cost calculation:</span></span>

* <span data-ttu-id="7f226-125">CSP 和 Dreamspark 訂用帳戶目前不支援使用作為 Azure DevTest Labs 使用 hello [Azure 計費 Api](../billing/billing-usage-rate-card-overview.md) toocalculate hello 實驗室成本，不支援的 CSP 或 Dreamspark 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f226-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses hello [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) toocalculate hello lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="7f226-126">您的優惠費率。</span><span class="sxs-lookup"><span data-stu-id="7f226-126">Your offer rates.</span></span> <span data-ttu-id="7f226-127">目前，我們不能 toouse （您的訂用帳戶底下顯示），您有與交涉 Microsoft 或 Microsoft 合作夥伴您服務費率。</span><span class="sxs-lookup"><span data-stu-id="7f226-127">Currently, we are not able toouse your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="7f226-128">我們將使用隨用隨付費率。</span><span class="sxs-lookup"><span data-stu-id="7f226-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="7f226-129">您的稅率</span><span class="sxs-lookup"><span data-stu-id="7f226-129">Your taxes</span></span>
* <span data-ttu-id="7f226-130">您的折扣</span><span class="sxs-lookup"><span data-stu-id="7f226-130">Your discounts</span></span>
* <span data-ttu-id="7f226-131">您的帳單貨幣。</span><span class="sxs-lookup"><span data-stu-id="7f226-131">Your billing currency.</span></span> <span data-ttu-id="7f226-132">目前，hello 實驗室成本只會顯示在美金貨幣。</span><span class="sxs-lookup"><span data-stu-id="7f226-132">Currently, hello lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="7f226-133">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="7f226-133">Related blog posts</span></span>
* [<span data-ttu-id="7f226-134">兩個的多個項目 tookeep 上處於 DevTest Labs 追蹤成本</span><span class="sxs-lookup"><span data-stu-id="7f226-134">Two more things tookeep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="7f226-135">為何要設定成本臨界值？</span><span class="sxs-lookup"><span data-stu-id="7f226-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="7f226-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7f226-136">Next steps</span></span>
<span data-ttu-id="7f226-137">以下是一些事情 tootry 下一步：</span><span class="sxs-lookup"><span data-stu-id="7f226-137">Here are some things tootry next:</span></span>

* <span data-ttu-id="7f226-138">[定義 lab 原則](devtest-lab-set-lab-policy.md)-了解如何 tooset hello 所使用的各種原則如何使用您的實驗室和其 Vm toogovern。</span><span class="sxs-lookup"><span data-stu-id="7f226-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how tooset hello various policies used toogovern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="7f226-139">[建立自訂映像](devtest-lab-create-template.md) - 當您建立 VM 時，您要指定一個基本映像，它可以是自訂映像或 Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="7f226-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="7f226-140">本文說明如何 toocreate 自訂映像從 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="7f226-140">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="7f226-141">[設定 Marketplace 映像](devtest-lab-configure-marketplace-images.md) - DevTest Labs 支援根據 Azure Marketplace 映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="7f226-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="7f226-142">本文將說明如何 toospecify 它，如果有的話，可以是 Azure Marketplace 映像在實驗室中建立 Vm 時使用。</span><span class="sxs-lookup"><span data-stu-id="7f226-142">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="7f226-143">[在實驗室中建立的 VM](devtest-lab-add-vm-with-artifacts.md) -說明如何 toocreate 將 VM 的基本映像從 (可能是自訂或 Marketplace)，以及如何 toowork 連同成品放在 VM 中。</span><span class="sxs-lookup"><span data-stu-id="7f226-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

