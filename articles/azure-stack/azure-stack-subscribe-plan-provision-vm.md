---
title: "訂閱供應項目 | Microsoft Docs"
description: "以使用者身分了解如何訂閱供應項目。"
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
ms.openlocfilehash: f70815b5e89753a4b0083ffbe10d9920062d1ff0
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="subscribe-to-an-offer"></a><span data-ttu-id="abe07-103">訂閱優惠</span><span class="sxs-lookup"><span data-stu-id="abe07-103">Subscribe to an offer</span></span>

<span data-ttu-id="abe07-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="abe07-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="abe07-105">既然您已經[建立供應項目](azure-stack-create-offer.md)，接著應該測試您的使用者是否可以建立訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="abe07-105">Now that you've [created an offer](azure-stack-create-offer.md), test that your users can create a subscription.</span></span>

1. <span data-ttu-id="abe07-106">[登入](azure-stack-connect-azure-stack.md) Azure Stack 使用者入口網站 (https://portal.local.azurestack.external)，然後按一下 [取得訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="abe07-106">[Sign in](azure-stack-connect-azure-stack.md) to the Azure Stack user portal (https://portal.local.azurestack.external) and click **Get a Subscription**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image01.png)
2. <span data-ttu-id="abe07-107">在 顯示名稱 欄位中，輸入您的訂用帳戶名稱、按一下 供應項目、按一下 選擇供應項目 刀鋒視窗中的其中一個供應項目，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="abe07-107">In the **Display Name** field, type a name for your subscription, click **Offer**, click one of the offers in the **Choose an offer** blade, and then click **Create**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image02.png)
3. <span data-ttu-id="abe07-108">若要檢視您建立的訂用帳戶，請按一下 [更多服務]、按一下 [訂用帳戶]，然後按一下您的新訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="abe07-108">To view the subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

<span data-ttu-id="abe07-109">訂閱供應項目之後，請重新整理入口網站以查看哪些服務是新訂用帳戶的一部分。</span><span class="sxs-lookup"><span data-stu-id="abe07-109">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span></span>

## <a name="subscribe-to-an-add-on-plan"></a><span data-ttu-id="abe07-110">訂閱附加方案</span><span class="sxs-lookup"><span data-stu-id="abe07-110">Subscribe to an add-on plan</span></span>
<span data-ttu-id="abe07-111">如果供應項目有附加方案，則使用者可以隨時將附加方案新增至其訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="abe07-111">If the offer has an add-on plan, users can add them to their subscription at any time.</span></span>  

1. <span data-ttu-id="abe07-112">在使用者入口網站中，選取 [更多服務] > [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="abe07-112">In the user portal, select **More services** > **Subscriptions**.</span></span>

2. <span data-ttu-id="abe07-113">按一下訂用帳戶 > [新增方案] 按鈕，然後選取附加方案。</span><span class="sxs-lookup"><span data-stu-id="abe07-113">Click on the subscription > **Add Plan** button, and select the add-on plan.</span></span>



## <a name="next-steps"></a><span data-ttu-id="abe07-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abe07-114">Next steps</span></span>
[<span data-ttu-id="abe07-115">佈建虛擬機器</span><span class="sxs-lookup"><span data-stu-id="abe07-115">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
