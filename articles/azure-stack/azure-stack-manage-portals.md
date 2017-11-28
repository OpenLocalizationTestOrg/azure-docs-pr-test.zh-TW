---
title: "aaaUsing hello 系統管理員和使用者入口網站在 Azure 堆疊 |Microsoft 文件"
description: "了解 hello Azure 堆疊中 hello 系統管理員和使用者入口網站之間的差異。"
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 02c7ff03-874e-4951-b591-28166b7a7a79
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: twooley
ms.openlocfilehash: 5e940749917e4aade26483a79bcc238346bf94f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-administrator-and-user-portals-in-azure-stack"></a><span data-ttu-id="6a862-103">使用 Azure 堆疊中的 hello 系統管理員和使用者入口網站</span><span class="sxs-lookup"><span data-stu-id="6a862-103">Using hello administrator and user portals in Azure Stack</span></span>

<span data-ttu-id="6a862-104">Azure 堆疊; 中有兩個入口網站hello 管理員入口網站和 hello 使用者入口網站 (也稱為 tooas hello*租用戶*入口網站)。</span><span class="sxs-lookup"><span data-stu-id="6a862-104">There are two portals in Azure Stack; hello administrator portal and hello user portal (also referred tooas hello *tenant* portal).</span></span> <span data-ttu-id="6a862-105">hello 入口網站是由個別執行個體的 Azure 資源管理員支援。</span><span class="sxs-lookup"><span data-stu-id="6a862-105">hello portals are backed by separate instances of Azure Resource Manager.</span></span>

<span data-ttu-id="6a862-106">hello 下表顯示如何 tooconnect toohello 入口網站和 Azure 堆疊開發套件環境中的 tooResource 管理員端點。</span><span class="sxs-lookup"><span data-stu-id="6a862-106">hello following table shows how tooconnect toohello portals and tooResource Manager endpoints in an Azure Stack Development Kit environment.</span></span>

|  <span data-ttu-id="6a862-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="6a862-107">Portal</span></span> | <span data-ttu-id="6a862-108">入口網站 URL</span><span class="sxs-lookup"><span data-stu-id="6a862-108">Portal URL</span></span> | <span data-ttu-id="6a862-109">Resource Manager 端點 URL</span><span class="sxs-lookup"><span data-stu-id="6a862-109">Resource Manager endpoint URL</span></span> |   
| -------- | ------------- | ------- |  
| <span data-ttu-id="6a862-110">系統管理員</span><span class="sxs-lookup"><span data-stu-id="6a862-110">Administrator</span></span> | <span data-ttu-id="6a862-111">https://adminportal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="6a862-111">https://adminportal.local.azurestack.external</span></span>  | <span data-ttu-id="6a862-112">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="6a862-112">https://adminmanagement.local.azurestack.external</span></span>  |  
| <span data-ttu-id="6a862-113">User</span><span class="sxs-lookup"><span data-stu-id="6a862-113">User</span></span> | <span data-ttu-id="6a862-114">https://portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="6a862-114">https://portal.local.azurestack.external</span></span> | <span data-ttu-id="6a862-115">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="6a862-115">https://management.local.azurestack.external</span></span>  |
| | |

## <a name="hello-administrator-portal"></a><span data-ttu-id="6a862-116">hello 管理員入口網站</span><span class="sxs-lookup"><span data-stu-id="6a862-116">hello administrator portal</span></span>

<span data-ttu-id="6a862-117">hello 管理員入口網站可讓雲端操作員 tooperform 系統管理和操作工作。</span><span class="sxs-lookup"><span data-stu-id="6a862-117">hello administrator portal enables a cloud operator tooperform administrative and operational tasks.</span></span> <span data-ttu-id="6a862-118">雲端操作員可執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="6a862-118">A cloud operator can do things such as:</span></span>
* <span data-ttu-id="6a862-119">監視健康情況和警示</span><span class="sxs-lookup"><span data-stu-id="6a862-119">monitor health and alerts</span></span>
* <span data-ttu-id="6a862-120">管理容量</span><span class="sxs-lookup"><span data-stu-id="6a862-120">manage capacity</span></span>
* <span data-ttu-id="6a862-121">填入 hello marketplace</span><span class="sxs-lookup"><span data-stu-id="6a862-121">populate hello marketplace</span></span>
* <span data-ttu-id="6a862-122">建立方案和產品</span><span class="sxs-lookup"><span data-stu-id="6a862-122">create plans and offers</span></span>
* <span data-ttu-id="6a862-123">為租用戶建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6a862-123">create subscriptions for tenants</span></span>

<span data-ttu-id="6a862-124">雲端操作員也可以建立資源，例如虛擬機器、虛擬網路和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a862-124">A cloud operator can also create resources such as virtual machines, virtual networks, and storage accounts.</span></span>

 ![hello 管理員入口網站](media/azure-stack-manage-portals/image1.png)

 ## <a name="hello-user-portal"></a><span data-ttu-id="6a862-126">hello 使用者入口網站</span><span class="sxs-lookup"><span data-stu-id="6a862-126">hello user portal</span></span>

 <span data-ttu-id="6a862-127">hello 使用者入口網站不提供存取 tooany hello 管理或操作功能的 hello 管理員入口網站。</span><span class="sxs-lookup"><span data-stu-id="6a862-127">hello user portal does not provide access tooany of hello administrative or operational capabilities of hello administrator portal.</span></span> <span data-ttu-id="6a862-128">在 hello 使用者入口網站，使用者可以訂閱 toopublic 優惠，並使用都可透過這些服務的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="6a862-128">In hello user portal, a user can subscribe toopublic offers, and use hello services that are made available through those offers.</span></span>

  ![hello 使用者入口網站](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a><span data-ttu-id="6a862-130">訂用帳戶行為</span><span class="sxs-lookup"><span data-stu-id="6a862-130">Subscription behavior</span></span>
 
 <span data-ttu-id="6a862-131">請確定您了解 hello 遵循 hello 兩個入口網站中的訂用帳戶行為之間的差異。</span><span class="sxs-lookup"><span data-stu-id="6a862-131">Make sure that you understand hello following differences between subscription behavior in hello two portals.</span></span>

 <span data-ttu-id="6a862-132">系統管理員入口網站：</span><span class="sxs-lookup"><span data-stu-id="6a862-132">Administrator portal:</span></span>
* <span data-ttu-id="6a862-133">沒有可用 hello 管理員入口網站中只有一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a862-133">There is only one subscription that is available in hello administrator portal.</span></span> <span data-ttu-id="6a862-134">此訂用帳戶為 hello*預設提供者訂閱*。</span><span class="sxs-lookup"><span data-stu-id="6a862-134">This subscription is hello *Default Provider Subscription*.</span></span> <span data-ttu-id="6a862-135">您無法加入 hello 管理員入口網站使用任何其他訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a862-135">You can't add any other subscriptions for use in hello administrator portal.</span></span>
* <span data-ttu-id="6a862-136">雲端操作員，您可以從 hello 管理員入口網站訂用帳戶加入為您的使用者 （包括您自己）。</span><span class="sxs-lookup"><span data-stu-id="6a862-136">As a cloud operator, you can add subscriptions for your users (including yourself) from hello administrator portal.</span></span> <span data-ttu-id="6a862-137">（包括您自己） 的使用者可以存取和使用這些訂用帳戶，從 hello 使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="6a862-137">Users (including yourself) can access and use these subscriptions from hello user portal.</span></span>

  >[!NOTE]
  <span data-ttu-id="6a862-138">Hello Azure 資源管理員分離，因為訂用帳戶不會跨越入口網站。</span><span class="sxs-lookup"><span data-stu-id="6a862-138">Because of hello Azure Resource Manager separation, subscriptions do not cross portals.</span></span> <span data-ttu-id="6a862-139">例如，如果您為雲端操作員登入 toohello 使用者入口網站，您無法存取 hello 預設提供者訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a862-139">For example, if you as a cloud operator signs in toohello user portal, you can't access hello Default Provider Subscription.</span></span> <span data-ttu-id="6a862-140">因此，您不需要存取 tooany 管理功能。</span><span class="sxs-lookup"><span data-stu-id="6a862-140">Therefore, you don't have access tooany administrative functions.</span></span> <span data-ttu-id="6a862-141">您可從公用產品為自己建立訂用帳戶，但系統仍會將您視為租用戶使用者。</span><span class="sxs-lookup"><span data-stu-id="6a862-141">You can create subscriptions for yourself from public offers, but you are considered a tenant user.</span></span>

<span data-ttu-id="6a862-142">使用者入口網站：</span><span class="sxs-lookup"><span data-stu-id="6a862-142">User portal:</span></span>
* <span data-ttu-id="6a862-143">在 hello 使用者入口網站的帳戶可以有多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a862-143">In hello user portal, an account can have multiple subscriptions.</span></span>

  >[!NOTE]
  <span data-ttu-id="6a862-144">Hello 套件在開發環境中，如果租用戶使用者所屬 toohello 相同的目錄 hello 雲端操作員，它們不會封鎖在 toohello 管理員入口網站登入。</span><span class="sxs-lookup"><span data-stu-id="6a862-144">In hello development kit environment, if a tenant user belongs toohello same directory as hello cloud operator, they are not blocked from signing in toohello administrator portal.</span></span> <span data-ttu-id="6a862-145">不過，就無法存取任何 hello 管理功能。</span><span class="sxs-lookup"><span data-stu-id="6a862-145">However, they can't access any of hello administrative functions.</span></span> <span data-ttu-id="6a862-146">此外，它們無法加入訂用帳戶或存取提供可用 toothem 源自 hello 使用者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="6a862-146">Also, they can't add subscriptions or access offers that are made available toothem in hello user portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a862-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a862-147">Next steps</span></span>

[<span data-ttu-id="6a862-148">連接 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="6a862-148">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

[<span data-ttu-id="6a862-149">Azure Stack 中的區域管理</span><span class="sxs-lookup"><span data-stu-id="6a862-149">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
