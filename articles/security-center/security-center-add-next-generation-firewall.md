---
title: "下一個層代防火牆 Azure 資訊安全中心 aaaAdd |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議 * * 加入 下一步產生防火牆 * * 和 * * 路由流量透過 NGFW 只 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="30300-103">在 Azure 資訊安全中心新增新一代防火牆</span><span class="sxs-lookup"><span data-stu-id="30300-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="30300-104">Azure 資訊安全中心可能會建議您新增的下一個層代防火牆 (NGFW) 從 Microsoft 夥伴 tooincrease 安全性保護。</span><span class="sxs-lookup"><span data-stu-id="30300-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> <span data-ttu-id="30300-105">本文件將逐步引導您透過如何的範例 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="30300-105">This document walks you through an example of how toodo this.</span></span>

> [!NOTE]
> <span data-ttu-id="30300-106">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="30300-106">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="30300-107">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="30300-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="30300-108">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="30300-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="30300-109">在 hello**建議**刀鋒視窗中，選取**加入下一個層代防火牆**。</span><span class="sxs-lookup"><span data-stu-id="30300-109">In hello **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="30300-110">![新增新一代防火牆][1]</span><span class="sxs-lookup"><span data-stu-id="30300-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="30300-111">在 hello**加入下一個層代防火牆**刀鋒視窗中，選取一個端點。</span><span class="sxs-lookup"><span data-stu-id="30300-111">In hello **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="30300-112">![選取端點][2]</span><span class="sxs-lookup"><span data-stu-id="30300-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="30300-113">第二個 [新增新一代防火牆]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="30300-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="30300-114">如果您可以選擇 toouse 現有的方案使用，或您可以建立一個新。</span><span class="sxs-lookup"><span data-stu-id="30300-114">You can choose toouse an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="30300-115">此範例中沒有任何可用的現有解決方案，因此我們將建立一個 NGFW。</span><span class="sxs-lookup"><span data-stu-id="30300-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="30300-116">![新建新一代防火牆][3]</span><span class="sxs-lookup"><span data-stu-id="30300-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="30300-117">toocreate NGFW 中，選取方案，從 hello 整合協力電腦清單。</span><span class="sxs-lookup"><span data-stu-id="30300-117">toocreate an NGFW, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="30300-118">在此範例中，我們會選取 [檢查點]。</span><span class="sxs-lookup"><span data-stu-id="30300-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="30300-119">![選取新一代防火牆解決方案][4]</span><span class="sxs-lookup"><span data-stu-id="30300-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="30300-120">hello**檢查點**刀鋒視窗會開啟提供您 hello 夥伴方案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="30300-120">hello **Check Point** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="30300-121">選取**建立**hello 資訊刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="30300-121">Select **Create** in hello information blade.</span></span>
   <span data-ttu-id="30300-122">![防火牆資訊刀鋒視窗][5]</span><span class="sxs-lookup"><span data-stu-id="30300-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="30300-123">hello**建立虛擬機器**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="30300-123">hello **Create virtual machine** blade opens.</span></span> <span data-ttu-id="30300-124">這裡您可以輸入執行的虛擬機器 (VM) 的必要的 toospin hello NGFW 的資訊。</span><span class="sxs-lookup"><span data-stu-id="30300-124">Here you can enter information required toospin up a virtual machine (VM) that runs hello NGFW.</span></span> <span data-ttu-id="30300-125">遵循 hello 步驟並提供所需的 hello NGFW 資訊。</span><span class="sxs-lookup"><span data-stu-id="30300-125">Follow hello steps and provide hello NGFW information required.</span></span> <span data-ttu-id="30300-126">選取 [確定] tooapply。</span><span class="sxs-lookup"><span data-stu-id="30300-126">Select OK tooapply.</span></span>
   <span data-ttu-id="30300-127">![建立虛擬機器 toorun NGFW][6]</span><span class="sxs-lookup"><span data-stu-id="30300-127">![Create virtual machine toorun NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="30300-128">僅透過 NGFW 路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="30300-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="30300-129">傳回 toohello**建議**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="30300-129">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="30300-130">在您透過資訊安全中心加入 NGFW 後會產生新的項目，稱為「僅透過 NGFW 路由傳送流量」 。</span><span class="sxs-lookup"><span data-stu-id="30300-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="30300-131">只有當您透過資訊安全中心安裝了 NGFW，才會建立這項建議。</span><span class="sxs-lookup"><span data-stu-id="30300-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="30300-132">如果您有網際網路對向端點時，資訊安全中心會建議您設定強制傳入的流量 tooyour 透過您 NGFW VM 的網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="30300-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic tooyour VM through your NGFW.</span></span>

1. <span data-ttu-id="30300-133">在 hello**建議刀鋒視窗**，選取**只透過 NGFW 流量路由傳送**。</span><span class="sxs-lookup"><span data-stu-id="30300-133">In hello **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="30300-134">![僅透過 NGFW 路由傳送流量][7]</span><span class="sxs-lookup"><span data-stu-id="30300-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="30300-135">這會開啟刀鋒視窗中 hello**只透過 NGFW 流量路由傳送**，其中會列出您可以路由傳送流量的 Vm。</span><span class="sxs-lookup"><span data-stu-id="30300-135">This opens hello blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="30300-136">Hello 清單中選取 VM。</span><span class="sxs-lookup"><span data-stu-id="30300-136">Select a VM from hello list.</span></span>
   <span data-ttu-id="30300-137">![選取 VM][8]</span><span class="sxs-lookup"><span data-stu-id="30300-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="30300-138">Hello 刀鋒視窗中的選取 VM 隨即開啟，顯示相關的輸入的規則。</span><span class="sxs-lookup"><span data-stu-id="30300-138">A blade for hello selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="30300-139">說明提供後續可能步驟的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="30300-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="30300-140">選取**編輯輸入的規則**tooproceed 編輯的輸入的規則。</span><span class="sxs-lookup"><span data-stu-id="30300-140">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span> <span data-ttu-id="30300-141">hello 期望是**來源**未設定太**任何**hello 網際網路對向端點連結與 hello NGFW。</span><span class="sxs-lookup"><span data-stu-id="30300-141">hello expectation is that **Source** is not set too**Any** for hello Internet-facing endpoints linked with hello NGFW.</span></span> <span data-ttu-id="30300-142">toolearn 進一步了解 hello 屬性 hello 輸入規則，請參閱[NSG 規則](../virtual-network/virtual-networks-nsg.md#nsg-rules)。</span><span class="sxs-lookup"><span data-stu-id="30300-142">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="30300-143">![設定規則 toolimit 存取][9]
   ![編輯輸入的規則][10]</span><span class="sxs-lookup"><span data-stu-id="30300-143">![Configure rules toolimit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="30300-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="30300-144">See also</span></span>
<span data-ttu-id="30300-145">這份文件範例說明了如何 tooimplement 會 hello 資訊安全中心建議 「 新增產生防火牆 下一步 」。</span><span class="sxs-lookup"><span data-stu-id="30300-145">This document showed you how tooimplement hello Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="30300-146">toolearn 深入了解 NGFWs 和 hello 的檢查點協力廠商解決方案，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="30300-146">toolearn more about NGFWs and hello Check Point partner solution, see hello following:</span></span>

* [<span data-ttu-id="30300-147">新一代防火牆</span><span class="sxs-lookup"><span data-stu-id="30300-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="30300-148">檢查點 vSEC</span><span class="sxs-lookup"><span data-stu-id="30300-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="30300-149">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="30300-149">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="30300-150">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 安全性原則。</span><span class="sxs-lookup"><span data-stu-id="30300-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="30300-151">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="30300-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="30300-152">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="30300-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="30300-153">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="30300-153">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="30300-154">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="30300-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="30300-155">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="30300-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="30300-156">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="30300-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
