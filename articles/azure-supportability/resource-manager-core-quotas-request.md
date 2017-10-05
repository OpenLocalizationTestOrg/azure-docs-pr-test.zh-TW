---
title: "Azure Resource Manager 核心配額增加要求 | Microsoft Docs"
description: "Azure Resource Manager 核心配額增加要求"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="e7c5d-103">Resource Manager 核心配額增加要求</span><span class="sxs-lookup"><span data-stu-id="e7c5d-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="e7c5d-104">區域層級和 SKU 系列層級強制執行 Resource Manager 核心配額。</span><span class="sxs-lookup"><span data-stu-id="e7c5d-104">Resource Manager core quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="e7c5d-105">您可以在 [Azure 訂用帳戶和服務限制](http://aka.ms/quotalimits)頁面深入了解如何強制執行配額。</span><span class="sxs-lookup"><span data-stu-id="e7c5d-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="e7c5d-106">若要深入了解 SKU 系列，您可以在[虛擬機器價格](http://aka.ms/pricingcompute)頁面上比較成本和效能。</span><span class="sxs-lookup"><span data-stu-id="e7c5d-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="e7c5d-107">若要要求增加，請在 Azure 入口網站 [https://portal.azure.com](https://portal.azure.com) 中建立核心的配額支援案例。</span><span class="sxs-lookup"><span data-stu-id="e7c5d-107">To request an increase, create a Quota support case for Cores in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="e7c5d-108">了解如何在 Azure 入口網站中[建立支援要求](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request)</span><span class="sxs-lookup"><span data-stu-id="e7c5d-108">Learn how to [create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in the Azure portal</span></span>

1. <span data-ttu-id="e7c5d-109">在新的支援要求頁面上，在 [問題類型] 選取 [配額]，在 [配額類型] 選取 [核心]。</span><span class="sxs-lookup"><span data-stu-id="e7c5d-109">On the new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![配額基本概念刀鋒視窗](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="e7c5d-111">在 [部署模型] 選取 [Resource Manager]，並選取位置。</span><span class="sxs-lookup"><span data-stu-id="e7c5d-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![配額問題刀鋒視窗](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="e7c5d-113">選取需要增加的 SKU 系列。</span><span class="sxs-lookup"><span data-stu-id="e7c5d-113">Select the SKU Families that require an increase.</span></span>

    ![選取的 SKU 系列](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="e7c5d-115">輸入您想要對訂用帳戶採取的新限制。</span><span class="sxs-lookup"><span data-stu-id="e7c5d-115">Enter the new limits you would like on the subscription.</span></span>

    ![SKU 新配額要求](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="e7c5d-117">若要移除一行，請從 SKU 系列下拉式清單中取消核取 SKU，或按一下捨棄 [x] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e7c5d-117">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="e7c5d-118">輸入每個 SKU 系列所需的配額後，請在 [問題步驟] 頁面上按 [下一步] 繼續建立支援要求。</span><span class="sxs-lookup"><span data-stu-id="e7c5d-118">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>
