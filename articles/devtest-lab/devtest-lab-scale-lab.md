---
title: "aaaScale 配額和限制您的實驗室中 Azure DevTest Labs |Microsoft 文件"
description: "深入了解如何 tooscale 的實驗室中 Azure DevTest Labs"
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
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="acadc-103">在 DevTest Labs 中調整配額和限制</span><span class="sxs-lookup"><span data-stu-id="acadc-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="acadc-104">DevTest 實驗室中工作時，您可能會注意到有特定的預設限制 toosome Azure 資源，這可能會影響 hello DevTest Labs 服務。</span><span class="sxs-lookup"><span data-stu-id="acadc-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="acadc-105">這些限制會參照的 tooas**配額**。</span><span class="sxs-lookup"><span data-stu-id="acadc-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="acadc-106">hello DevTest Labs 服務不會強制執行任何的配額。</span><span class="sxs-lookup"><span data-stu-id="acadc-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="acadc-107">您可能會遇到任何配額是 hello 整體 Azure 訂用帳戶的預設條件約束。</span><span class="sxs-lookup"><span data-stu-id="acadc-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="acadc-108">您可以使用每個 Azure 資源直到您達到其配額。</span><span class="sxs-lookup"><span data-stu-id="acadc-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="acadc-109">每個訂用帳戶都有個別配額，並且會追蹤每個訂用帳戶的使用量。</span><span class="sxs-lookup"><span data-stu-id="acadc-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="acadc-110">例如，每個訂用帳戶都有預設配額 20 個核心。</span><span class="sxs-lookup"><span data-stu-id="acadc-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="acadc-111">因此，如果您在具有四個核心的實驗室中建立 VM，則您只能建立五個 VM。</span><span class="sxs-lookup"><span data-stu-id="acadc-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="acadc-112">[Azure 訂用帳戶和服務限制](https://docs.microsoft.com/azure/azure-subscription-service-limits)列出一些 hello Azure 資源的最常見的配額。</span><span class="sxs-lookup"><span data-stu-id="acadc-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="acadc-113">hello 在實驗室中，最常使用的資源，並為您可能會遇到配額，加入 VM 核心、 公用 IP 位址、 網路介面、 受管理的磁碟、 RBAC 角色指派和 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="acadc-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="acadc-114">檢視使用量和配額</span><span class="sxs-lookup"><span data-stu-id="acadc-114">View your usage and quotas</span></span>
<span data-ttu-id="acadc-115">這些步驟顯示如何 tooview 會 hello 目前配額的訂用帳戶特定的 Azure 資源，與 toosee 中您已使用的每個配額百分比。</span><span class="sxs-lookup"><span data-stu-id="acadc-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="acadc-116">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="acadc-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="acadc-117">選取**更服務**，然後選取**計費**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="acadc-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="acadc-118">在 hello 帳單 刀鋒視窗中，選取 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="acadc-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="acadc-119">選取 [使用量 + 配額]。</span><span class="sxs-lookup"><span data-stu-id="acadc-119">Select **Usage + quotas**.</span></span>

   ![使用量和配額按鈕](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="acadc-121">hello 使用量 + 配額刀鋒視窗中隨即顯示，列出該訂用帳戶與 hello 的百分比表示每個資源正在使用的 hello 配額不同的資源。</span><span class="sxs-lookup"><span data-stu-id="acadc-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![配額和使用量](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="acadc-123">要求訂用帳戶中的更多資源</span><span class="sxs-lookup"><span data-stu-id="acadc-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="acadc-124">如果達到配額上限，增加 tooa 最大限制，向上的 hello 預設限制的訂用帳戶中的資源中所述[Azure 訂用帳戶和服務限制](https://docs.microsoft.com/azure/azure-subscription-service-limits)。</span><span class="sxs-lookup"><span data-stu-id="acadc-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="acadc-125">這些步驟會告訴您如何 toorequest 配額增加透過 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="acadc-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="acadc-126">選取 [更多服務]，選取 [計費]，然後選取 [使用量 + 配額]。</span><span class="sxs-lookup"><span data-stu-id="acadc-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="acadc-127">在 hello 使用量 + 配額刀鋒視窗中，選取 hello**要求增加** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="acadc-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![要求增加按鈕](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="acadc-129">toocomplete 和提交 hello 要求，請填寫所有的三個索引標籤上的 hello 所需資訊的 hello**新增支援要求**表單。</span><span class="sxs-lookup"><span data-stu-id="acadc-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![要求增加表單](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="acadc-131">[了解 Azure 限制並增加](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/)提供詳細資訊連絡 Azure 支援 toorequest 配額增加。</span><span class="sxs-lookup"><span data-stu-id="acadc-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="acadc-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="acadc-132">Next steps</span></span>
* <span data-ttu-id="acadc-133">瀏覽 hello [DevTest Labs Azure 資源管理員的快速入門範本庫](https://github.com/Azure/azure-devtestlab/tree/master/Samples)。</span><span class="sxs-lookup"><span data-stu-id="acadc-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
