---
title: "在 Azure Stack 中建立供應項目 | Microsoft Docs"
description: "身為雲端系統管理員，您應該了解如何在 Azure Stack 中為使用者建立供應項目。"
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
ms.openlocfilehash: 269a6106f657536ba74be366f842b2f9cd86c5dc
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="7af5b-103">在 Azure Stack 中建立優惠</span><span class="sxs-lookup"><span data-stu-id="7af5b-103">Create an offer in Azure Stack</span></span>

<span data-ttu-id="7af5b-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="7af5b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="7af5b-105">[供應項目](azure-stack-key-features.md)是一組提供者供使用者購買或訂閱的一或多個方案。</span><span class="sxs-lookup"><span data-stu-id="7af5b-105">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to users to purchase or subscribe to.</span></span> <span data-ttu-id="7af5b-106">此文件將說明如何建立一個包含您在上一個步驟中[所建立方案](azure-stack-create-plan.md)的供應項目。</span><span class="sxs-lookup"><span data-stu-id="7af5b-106">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md) in the last step.</span></span> <span data-ttu-id="7af5b-107">此供應項目可讓訂閱者佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7af5b-107">This offer gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="7af5b-108">登入 Azure Stack 系統管理員入口網站 (https://adminportal.local.azurestack.external) > 按一下 [新增] > [租用戶供應項目 + 方案] > [供應項目]。</span><span class="sxs-lookup"><span data-stu-id="7af5b-108">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="7af5b-109">在 [新增供應項目] 刀鋒視窗中，填寫 [顯示名稱] 與 [資源名稱]，然後選取新的或現有的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="7af5b-109">In the **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="7af5b-110">「顯示名稱」是供應項目的易記名稱，而且是使用者訂閱供應項目時唯一會看到的資訊。</span><span class="sxs-lookup"><span data-stu-id="7af5b-110">The Display Name is the offer's friendly name and is the only information about the offer that the users will see when subscribing.</span></span> <span data-ttu-id="7af5b-111">因此，請務必使用可協助使用者了解該供應項目附帶內容的直覺式名稱。</span><span class="sxs-lookup"><span data-stu-id="7af5b-111">Therefore, be sure to use an intuitive name that helps the user understand what comes with the offer.</span></span> <span data-ttu-id="7af5b-112">只有系統管理員可以看到「資源名稱」。</span><span class="sxs-lookup"><span data-stu-id="7af5b-112">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="7af5b-113">它是系統管理員用來處理其他供應項目 (以 Azure Resource Manager 資源方式) 的名稱。</span><span class="sxs-lookup"><span data-stu-id="7af5b-113">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="7af5b-114">按一下 基本方案，在 方案 刀鋒視窗中選取要包含在供應項目中的方案，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="7af5b-114">Click **Base plans** and, in the **Plan** blade, select the plans you want to include in the offer, and then click **Select**.</span></span> <span data-ttu-id="7af5b-115">按一下 [建立]  來建立優惠。</span><span class="sxs-lookup"><span data-stu-id="7af5b-115">Click **Create** to create the offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="7af5b-116">按一下 所有資源，搜尋您的新供應項目，按一下該新供應項目、按一下 變更狀態，然後按一下公用。</span><span class="sxs-lookup"><span data-stu-id="7af5b-116">Click **All Resources**, search for your new offer, click on the new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="7af5b-117">供應項目必須設定為公用，使用者才能在訂閱時取得完整的檢視。</span><span class="sxs-lookup"><span data-stu-id="7af5b-117">Offers must be made public for users to get the full view when subscribing.</span></span> <span data-ttu-id="7af5b-118">供應項目可以是：</span><span class="sxs-lookup"><span data-stu-id="7af5b-118">Offers can be:</span></span>

* <span data-ttu-id="7af5b-119">**公用**：使用者可以看到。</span><span class="sxs-lookup"><span data-stu-id="7af5b-119">**Public**: Visible to users.</span></span>
* <span data-ttu-id="7af5b-120">**私用**：只有雲端系統管理員可以看到。</span><span class="sxs-lookup"><span data-stu-id="7af5b-120">**Private**: Only visible to the cloud administrators.</span></span> <span data-ttu-id="7af5b-121">在草擬方案或供應項目時，或雲端系統管理員想要核准每個訂用帳戶時，會相當實用。</span><span class="sxs-lookup"><span data-stu-id="7af5b-121">Useful while drafting the plan or offer, or if the cloud administrator wants to approve every subscription.</span></span>
* <span data-ttu-id="7af5b-122">**已解除**：不開放給新的訂閱者。</span><span class="sxs-lookup"><span data-stu-id="7af5b-122">**Decommissioned**: Closed to new subscribers.</span></span> <span data-ttu-id="7af5b-123">雲端系統管理員可以使用「已解除」來避免之後的訂用帳戶使用，但不會影響目前的訂閱者。</span><span class="sxs-lookup"><span data-stu-id="7af5b-123">The cloud administrator can use decommissioned to prevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="7af5b-124">對供應項目所做的變更不會立即對使用者顯示。</span><span class="sxs-lookup"><span data-stu-id="7af5b-124">Changes to the offer are not immediately visible to the user.</span></span> <span data-ttu-id="7af5b-125">建立資源/資源群組時，若要查看變更，您可能必須登出/登入，才能在「訂用帳戶選擇器」中看到新的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7af5b-125">To see the changes, you might have to logout/login to see the new subscription in the “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="7af5b-126">您也可以如 [Azure Stack 服務管理員讀我檔案](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin) \(英文\) 所述，使用 PowerShell 來建立預設的供應項目、方案及配額。</span><span class="sxs-lookup"><span data-stu-id="7af5b-126">You can also create default offers, plans, and quotas by using PowerShell as explained in the [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="7af5b-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7af5b-127">Next steps</span></span>
[<span data-ttu-id="7af5b-128">訂閱優惠然後佈建 VM</span><span class="sxs-lookup"><span data-stu-id="7af5b-128">Subscribe to an offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
