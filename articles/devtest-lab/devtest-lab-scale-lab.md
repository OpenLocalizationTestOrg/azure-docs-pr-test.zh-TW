---
title: "在 Azure DevTest Labs 中調整實驗室的配額和限制 | Microsoft Docs"
description: "了解如何在 Azure DevTest Labs 中調整實驗室"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: f11ed42b474e4f208eac92689bfa33fb188d15a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="8ed23-103">在 DevTest Labs 中調整配額和限制</span><span class="sxs-lookup"><span data-stu-id="8ed23-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="8ed23-104">當您在 DevTest Labs 中工作時，您可能會發現某些 Azure 資源有特定預設限制，會影響 DevTest Labs 服務。</span><span class="sxs-lookup"><span data-stu-id="8ed23-104">As you work in DevTest Labs, you might notice that there are certain default limits to some Azure resources, which can affect the DevTest Labs service.</span></span> <span data-ttu-id="8ed23-105">這些限制稱為**配額**。</span><span class="sxs-lookup"><span data-stu-id="8ed23-105">These limits are referred to as **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed23-106">DevTest Labs 服務不會造成任何配額。</span><span class="sxs-lookup"><span data-stu-id="8ed23-106">The DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="8ed23-107">您可能遇到的任何配額是整體 Azure 訂用帳戶的預設條件約束。</span><span class="sxs-lookup"><span data-stu-id="8ed23-107">Any quotas you might encounter are default constraints of the overall Azure subscription.</span></span>

<span data-ttu-id="8ed23-108">您可以使用每個 Azure 資源直到您達到其配額。</span><span class="sxs-lookup"><span data-stu-id="8ed23-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="8ed23-109">每個訂用帳戶都有個別配額，並且會追蹤每個訂用帳戶的使用量。</span><span class="sxs-lookup"><span data-stu-id="8ed23-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="8ed23-110">例如，每個訂用帳戶都有預設配額 20 個核心。</span><span class="sxs-lookup"><span data-stu-id="8ed23-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="8ed23-111">因此，如果您在具有四個核心的實驗室中建立 VM，則您只能建立五個 VM。</span><span class="sxs-lookup"><span data-stu-id="8ed23-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="8ed23-112">[Azure 訂用帳戶和服務限制](https://docs.microsoft.com/azure/azure-subscription-service-limits)列出一些 Azure 資源最常見的配額。</span><span class="sxs-lookup"><span data-stu-id="8ed23-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of the most common quotas for Azure resources.</span></span> <span data-ttu-id="8ed23-113">在實驗室中最常使用的資源 (且您可能會遇到其配額) 包括 VM 核心、公用 IP 位址、網路介面、受控磁碟、RBAC 角色指派，以及 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="8ed23-113">The resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="8ed23-114">檢視使用量和配額</span><span class="sxs-lookup"><span data-stu-id="8ed23-114">View your usage and quotas</span></span>
<span data-ttu-id="8ed23-115">下列步驟將示範如何檢視訂用帳戶中 Azure 資源的目前配額，以及查看您使用的每個配額百分比。</span><span class="sxs-lookup"><span data-stu-id="8ed23-115">These steps show you how to view the current quotas in your subscription for specific Azure resources, and to see what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="8ed23-116">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="8ed23-116">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="8ed23-117">選取 [更多服務]，然後從清單中選取 [計費]。</span><span class="sxs-lookup"><span data-stu-id="8ed23-117">Select **More Services**, and then select **Billing** from the list.</span></span>
1. <span data-ttu-id="8ed23-118">在 [計費] 刀鋒視窗中選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ed23-118">In the Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="8ed23-119">選取 [使用量 + 配額]。</span><span class="sxs-lookup"><span data-stu-id="8ed23-119">Select **Usage + quotas**.</span></span>

   ![使用量和配額按鈕](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="8ed23-121">[使用量 + 配額] 刀鋒視窗隨即出現，列出該訂用帳戶中可用的不同資源，以及每個資源使用的配額百分比。</span><span class="sxs-lookup"><span data-stu-id="8ed23-121">The Usage + quotas blade appears, listing different resources available in that subscription and the percentage of the quota that is being used per resource.</span></span>

   ![配額和使用量](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="8ed23-123">要求訂用帳戶中的更多資源</span><span class="sxs-lookup"><span data-stu-id="8ed23-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="8ed23-124">如果達到配額上限，訂用帳戶中資源的預設限制可以增加到最大限制，如 [Azure 訂用帳戶和服務限制](https://docs.microsoft.com/azure/azure-subscription-service-limits)中所述。</span><span class="sxs-lookup"><span data-stu-id="8ed23-124">If you reach a quota cap, the default limit of a resource in a subscription can be increased up to a maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="8ed23-125">這些步驟為您示範如何透過 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)要求配額增加。</span><span class="sxs-lookup"><span data-stu-id="8ed23-125">These steps show you how to request a quota increase through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="8ed23-126">選取 [更多服務]，選取 [計費]，然後選取 [使用量 + 配額]。</span><span class="sxs-lookup"><span data-stu-id="8ed23-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="8ed23-127">在 [使用量 + 配額] 刀鋒視窗中，選取 [要求增加] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8ed23-127">In the Usage + quotas blade, select the **Request Increase** button.</span></span>

   ![要求增加按鈕](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="8ed23-129">若要完成要求並且提交，請在 [新增支援要求] 表單的全部三個索引標籤上填寫必要資訊。</span><span class="sxs-lookup"><span data-stu-id="8ed23-129">To complete and submit the request, fill out the required information on all three tabs of the **New support request** form.</span></span>

   ![要求增加表單](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="8ed23-131">[了解 Azure 限制和增加](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/)提供連絡 Azure 支援以要求配額增加的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8ed23-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support to request a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="8ed23-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ed23-132">Next steps</span></span>
* <span data-ttu-id="8ed23-133">瀏覽 [DevTest Labs Azure Resource Manager 快速入門範本資源庫 (英文)](https://github.com/Azure/azure-devtestlab/tree/master/Samples)。</span><span class="sxs-lookup"><span data-stu-id="8ed23-133">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
