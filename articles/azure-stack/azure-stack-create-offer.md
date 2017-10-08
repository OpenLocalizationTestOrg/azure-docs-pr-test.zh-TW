---
title: "aaaCreate Azure 堆疊中提供項目 |Microsoft 文件"
description: "是雲端系統管理員，瞭解如何 toocreate Azure 堆疊中的租用戶優惠。"
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
ms.openlocfilehash: 924526a0ff1c634b7c127c03a4572057c35b497b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="0c906-103">在 Azure Stack 中建立優惠</span><span class="sxs-lookup"><span data-stu-id="0c906-103">Create an offer in Azure Stack</span></span>
<span data-ttu-id="0c906-104">[提供](azure-stack-key-features.md)是群組的一或多個計劃存在 tootenants toopurchase 該提供者或訂閱。</span><span class="sxs-lookup"><span data-stu-id="0c906-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present tootenants toopurchase or subscribe to.</span></span> <span data-ttu-id="0c906-105">本文件說明如何 toocreate 優惠，其中包含 hello[您所建立的計劃](azure-stack-create-plan.md)hello 最後一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="0c906-105">This document shows you how toocreate an offer that includes hello [plan that you created](azure-stack-create-plan.md) in hello last step.</span></span> <span data-ttu-id="0c906-106">這項優惠提供 hello 能力 tooprovision 虛擬機器的 「 訂閱者 」。</span><span class="sxs-lookup"><span data-stu-id="0c906-106">This offer gives subscribers hello ability tooprovision virtual machines.</span></span>

1. <span data-ttu-id="0c906-107">登入 toohello 堆疊 Azure 管理員入口網站 (https://adminportal.local.azurestack.external) > 按一下**新增** > **租用戶提供 + 計劃** >  **提供**。</span><span class="sxs-lookup"><span data-stu-id="0c906-107">Sign in toohello Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="0c906-108">在 hello**新提供**刀鋒視窗中，填滿**顯示名稱**和**資源名稱**，，然後選取新的或現有**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="0c906-108">In hello **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="0c906-109">hello 顯示名稱是 hello 供應項目的易記名稱，並且 hello 時，使用者會看到訂閱 hello 優惠 hello 唯一資訊。</span><span class="sxs-lookup"><span data-stu-id="0c906-109">hello Display Name is hello offer's friendly name and is hello only information about hello offer that hello users will see when subscribing.</span></span> <span data-ttu-id="0c906-110">因此，請確定 toouse 直覺式的名稱，可協助 hello 使用者了解隨附 hello 優惠的內容。</span><span class="sxs-lookup"><span data-stu-id="0c906-110">Therefore, be sure toouse an intuitive name that helps hello user understand what comes with hello offer.</span></span> <span data-ttu-id="0c906-111">只有 hello 管理員可以看到 hello 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="0c906-111">Only hello admin can see hello Resource Name.</span></span> <span data-ttu-id="0c906-112">它的 hello 名稱，系統管理員 」 搭配 toowork hello 供應項目做為 Azure 資源管理員資源。</span><span class="sxs-lookup"><span data-stu-id="0c906-112">It's hello name that admins use toowork with hello offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="0c906-113">按一下**基底計劃**，而在 hello**規劃**刀鋒視窗中，選取 hello 計劃您想要在 hello 優惠 tooinclude，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="0c906-113">Click **Base plans** and, in hello **Plan** blade, select hello plans you want tooinclude in hello offer, and then click **Select**.</span></span> <span data-ttu-id="0c906-114">按一下**建立**toocreate hello 供應項目。</span><span class="sxs-lookup"><span data-stu-id="0c906-114">Click **Create** toocreate hello offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="0c906-115">按一下**所有資源**、 新的優惠搜尋、 按一下 hello 新的優惠，然後按一下**狀態變更**，然後按一下**公用**。</span><span class="sxs-lookup"><span data-stu-id="0c906-115">Click **All Resources**, search for your new offer, click on hello new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="0c906-116">提供項目必須會公開讓租用戶 tooget hello 完整檢視訂閱時。</span><span class="sxs-lookup"><span data-stu-id="0c906-116">Offers must be made public for tenants tooget hello full view when subscribing.</span></span> <span data-ttu-id="0c906-117">供應項目可以是：</span><span class="sxs-lookup"><span data-stu-id="0c906-117">Offers can be:</span></span>

* <span data-ttu-id="0c906-118">**公用**： 可見 tootenants。</span><span class="sxs-lookup"><span data-stu-id="0c906-118">**Public**: Visible tootenants.</span></span>
* <span data-ttu-id="0c906-119">**私用**： 只顯示 toohello 雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="0c906-119">**Private**: Only visible toohello cloud administrators.</span></span> <span data-ttu-id="0c906-120">有用時草擬階段 hello 計劃或提供的服務，或如果 hello 雲端系統管理員想 tooapprove 每個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c906-120">Useful while drafting hello plan or offer, or if hello cloud administrator wants tooapprove every subscription.</span></span>
* <span data-ttu-id="0c906-121">**解除委任**： 關閉 toonew 「 訂閱者 」。</span><span class="sxs-lookup"><span data-stu-id="0c906-121">**Decommissioned**: Closed toonew subscribers.</span></span> <span data-ttu-id="0c906-122">hello 雲端系統管理員可以使用已解除委任的 tooprevent 未來的訂閱，但保留目前的訂閱者不變。</span><span class="sxs-lookup"><span data-stu-id="0c906-122">hello cloud administrator can use decommissioned tooprevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="0c906-123">變更 toohello 供應項目不會立即看到 toohello 租用戶。</span><span class="sxs-lookup"><span data-stu-id="0c906-123">Changes toohello offer are not immediately visible toohello tenant.</span></span> <span data-ttu-id="0c906-124">toosee hello 變更，您可能必須 toologout/登入 toosee hello 新訂用帳戶中 hello 」 訂用帳戶選擇器 」 時建立資源/資源群組。</span><span class="sxs-lookup"><span data-stu-id="0c906-124">toosee hello changes, you might have toologout/login toosee hello new subscription in hello “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="0c906-125">您也可以使用 PowerShell hello 中所述建立預設優惠、 計劃和配額[Azure 堆疊服務系統管理員讀我檔案](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin)。</span><span class="sxs-lookup"><span data-stu-id="0c906-125">You can also create default offers, plans, and quotas by using PowerShell as explained in hello [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


## <a name="next-steps"></a><span data-ttu-id="0c906-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c906-126">Next steps</span></span>
[<span data-ttu-id="0c906-127">訂閱 tooan 供應項目，然後佈建 VM</span><span class="sxs-lookup"><span data-stu-id="0c906-127">Subscribe tooan offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
