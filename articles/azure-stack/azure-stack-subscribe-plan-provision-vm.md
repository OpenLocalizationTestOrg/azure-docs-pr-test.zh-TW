---
title: "訂閱供應項目 | Microsoft Docs"
description: "以租用戶身分了解如何訂閱供應項目。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 7f3f8683-ef09-4838-92ed-41f2fddbbbed
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/03/2017
ms.author: erikje
ms.openlocfilehash: 3cd87ebe9827249d32f15b5de0ad8521d0282c47
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="subscribe-to-an-offer"></a><span data-ttu-id="dbd18-103">訂閱優惠</span><span class="sxs-lookup"><span data-stu-id="dbd18-103">Subscribe to an offer</span></span>
<span data-ttu-id="dbd18-104">既然您已經[建立供應項目](azure-stack-create-offer.md)，接著應測試您的租用戶是否可以建立訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dbd18-104">Now that you've [created an offer](azure-stack-create-offer.md), test that your tenants can create a subscription.</span></span>

1. <span data-ttu-id="dbd18-105">[登入](azure-stack-connect-azure-stack.md) Azure Stack 租用戶入口網站 (https://portal.local.azurestack.external)，然後按一下 [取得訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="dbd18-105">[Sign in](azure-stack-connect-azure-stack.md) to the Azure Stack tenant portal (https://portal.local.azurestack.external) and click **Get a Subscription**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image01.png)
2. <span data-ttu-id="dbd18-106">在 [顯示名稱] 欄位中，輸入您的訂用帳戶名稱、按一下 [供應項目]、按一下 [選擇供應項目] 刀鋒視窗中的其中一個供應項目，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="dbd18-106">In the **Display Name** field, type a name for your subscription, click **Offer**, click one of the offers in the **Choose an offer** blade, and then click **Create**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image02.png)
3. <span data-ttu-id="dbd18-107">若要檢視您建立的訂用帳戶，請按一下 [更多服務]、按一下 [訂用帳戶]，然後按一下您的新訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dbd18-107">To view the subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

<span data-ttu-id="dbd18-108">訂閱供應項目之後，請重新整理入口網站以查看哪些服務是新訂用帳戶的一部分。</span><span class="sxs-lookup"><span data-stu-id="dbd18-108">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span></span>

## <a name="subscribe-to-an-add-on-plan"></a><span data-ttu-id="dbd18-109">訂閱附加方案</span><span class="sxs-lookup"><span data-stu-id="dbd18-109">Subscribe to an add-on plan</span></span>
<span data-ttu-id="dbd18-110">如果供應項目有附加方案，租用戶可以隨時將附加方案加入至其訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dbd18-110">If the offer has an add-on plan, tenants can add them to their subscription at any time.</span></span>  

1. <span data-ttu-id="dbd18-111">在租用戶入口網站中，選取 [更多服務] > [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="dbd18-111">In the tenant portal, select **More services** > **Subscriptions**.</span></span>

2. <span data-ttu-id="dbd18-112">按一下訂用帳戶 > [新增方案] 按鈕，然後選取附加方案。</span><span class="sxs-lookup"><span data-stu-id="dbd18-112">Click on the subscription > **Add Plan** button, and select the add-on plan.</span></span>



## <a name="next-steps"></a><span data-ttu-id="dbd18-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dbd18-113">Next steps</span></span>
[<span data-ttu-id="dbd18-114">佈建虛擬機器</span><span class="sxs-lookup"><span data-stu-id="dbd18-114">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
