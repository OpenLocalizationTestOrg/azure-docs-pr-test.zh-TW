---
title: "在 Azure Stack 中建立供應項目 | Microsoft Docs"
description: "身為雲端系統管理員，您應該了解如何在 Azure Stack 中為您的租用戶建立供應項目。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 96b080a4-a9a5-407c-ba54-111de2413d59
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 3d7360a1fb1c0cf42d77b3f39bf92c30438c2e01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="802ad-103">在 Azure Stack 中建立優惠</span><span class="sxs-lookup"><span data-stu-id="802ad-103">Create an offer in Azure Stack</span></span>
<span data-ttu-id="802ad-104">[供應項目](azure-stack-key-features.md)是提供者提供給租用戶購買或訂閱的一或多個方案群組。</span><span class="sxs-lookup"><span data-stu-id="802ad-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to tenants to purchase or subscribe to.</span></span> <span data-ttu-id="802ad-105">此文件將說明如何建立一個包含您在上一個步驟中[所建立方案](azure-stack-create-plan.md)的供應項目。</span><span class="sxs-lookup"><span data-stu-id="802ad-105">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md) in the last step.</span></span> <span data-ttu-id="802ad-106">此供應項目可讓訂閱者佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="802ad-106">This offer gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="802ad-107">登入 Azure Stack 系統管理員入口網站 (https://adminportal.local.azurestack.external) > 按一下 [新增] > [租用戶供應項目 + 方案] > [供應項目]。</span><span class="sxs-lookup"><span data-stu-id="802ad-107">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="802ad-108">在 [新增供應項目] 刀鋒視窗中，填寫 [顯示名稱] 與 [資源名稱]，然後選取新的或現有的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="802ad-108">In the **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="802ad-109">「顯示名稱」是供應項目的易記名稱，而且是使用者訂閱供應項目時唯一會看到的資訊。</span><span class="sxs-lookup"><span data-stu-id="802ad-109">The Display Name is the offer's friendly name and is the only information about the offer that the users will see when subscribing.</span></span> <span data-ttu-id="802ad-110">因此，請務必使用可協助使用者了解該供應項目附帶內容的直覺式名稱。</span><span class="sxs-lookup"><span data-stu-id="802ad-110">Therefore, be sure to use an intuitive name that helps the user understand what comes with the offer.</span></span> <span data-ttu-id="802ad-111">只有系統管理員可以看到「資源名稱」。</span><span class="sxs-lookup"><span data-stu-id="802ad-111">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="802ad-112">它是系統管理員用來處理其他供應項目 (以 Azure Resource Manager 資源方式) 的名稱。</span><span class="sxs-lookup"><span data-stu-id="802ad-112">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="802ad-113">按一下 [基本方案]，在 [方案] 刀鋒視窗中選取要包含在供應項目中的方案，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="802ad-113">Click **Base plans** and, in the **Plan** blade, select the plans you want to include in the offer, and then click **Select**.</span></span> <span data-ttu-id="802ad-114">按一下 [建立]  來建立優惠。</span><span class="sxs-lookup"><span data-stu-id="802ad-114">Click **Create** to create the offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="802ad-115">按一下 [所有資源]，搜尋您的新供應項目，按一下該新供應項目、按一下 [變更狀態]，然後按一下 [公用]。</span><span class="sxs-lookup"><span data-stu-id="802ad-115">Click **All Resources**, search for your new offer, click on the new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="802ad-116">供應項目必須設定為公用，租用戶才能在訂閱時取得完整的檢視。</span><span class="sxs-lookup"><span data-stu-id="802ad-116">Offers must be made public for tenants to get the full view when subscribing.</span></span> <span data-ttu-id="802ad-117">供應項目可以是：</span><span class="sxs-lookup"><span data-stu-id="802ad-117">Offers can be:</span></span>

* <span data-ttu-id="802ad-118">**公用**：租用戶可以看到。</span><span class="sxs-lookup"><span data-stu-id="802ad-118">**Public**: Visible to tenants.</span></span>
* <span data-ttu-id="802ad-119">**私用**：只有雲端系統管理員可以看到。</span><span class="sxs-lookup"><span data-stu-id="802ad-119">**Private**: Only visible to the cloud administrators.</span></span> <span data-ttu-id="802ad-120">在草擬方案或供應項目時，或雲端系統管理員想要核准每個訂用帳戶時，會相當實用。</span><span class="sxs-lookup"><span data-stu-id="802ad-120">Useful while drafting the plan or offer, or if the cloud administrator wants to approve every subscription.</span></span>
* <span data-ttu-id="802ad-121">**已解除**：不開放給新的訂閱者。</span><span class="sxs-lookup"><span data-stu-id="802ad-121">**Decommissioned**: Closed to new subscribers.</span></span> <span data-ttu-id="802ad-122">雲端系統管理員可以使用「已解除」來避免之後的訂用帳戶使用，但不會影響目前的訂閱者。</span><span class="sxs-lookup"><span data-stu-id="802ad-122">The cloud administrator can use decommissioned to prevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="802ad-123">對供應項目所做的變更不會立即對租用戶顯示。</span><span class="sxs-lookup"><span data-stu-id="802ad-123">Changes to the offer are not immediately visible to the tenant.</span></span> <span data-ttu-id="802ad-124">建立資源/資源群組時，若要查看變更，您可能必須登出/登入，才能在「訂用帳戶選擇器」中看到新的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="802ad-124">To see the changes, you might have to logout/login to see the new subscription in the “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="802ad-125">您也可以如 [Azure Stack 服務管理員讀我檔案](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin) \(英文\) 所述，使用 PowerShell 來建立預設的供應項目、方案及配額。</span><span class="sxs-lookup"><span data-stu-id="802ad-125">You can also create default offers, plans, and quotas by using PowerShell as explained in the [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


## <a name="next-steps"></a><span data-ttu-id="802ad-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="802ad-126">Next steps</span></span>
[<span data-ttu-id="802ad-127">訂閱優惠然後佈建 VM</span><span class="sxs-lookup"><span data-stu-id="802ad-127">Subscribe to an offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
