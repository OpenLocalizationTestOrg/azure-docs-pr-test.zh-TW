---
title: "在 Azure 資訊安全中心新增新一代防火牆 | Microsoft Docs"
description: "本文件說明如何實作 Azure 資訊安全中心建議的「新增新一代防火牆」與「僅透過 NGFW 路由傳送流量」。"
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
ms.openlocfilehash: 30589d0a943517c03394a3aae7c03c8094e78c1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="462ea-103">在 Azure 資訊安全中心新增新一代防火牆</span><span class="sxs-lookup"><span data-stu-id="462ea-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="462ea-104">Azure 資訊安全中心可能會建議您新增由 Microsoft 合作夥伴提供的新一代防火牆 (NGFW)，以提升您的安全防護。</span><span class="sxs-lookup"><span data-stu-id="462ea-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> <span data-ttu-id="462ea-105">本文件逐步解說如何進行這項操作的範例。</span><span class="sxs-lookup"><span data-stu-id="462ea-105">This document walks you through an example of how to do this.</span></span>

> [!NOTE]
> <span data-ttu-id="462ea-106">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="462ea-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="462ea-107">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="462ea-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="462ea-108">實作建議</span><span class="sxs-lookup"><span data-stu-id="462ea-108">Implement the recommendation</span></span>
1. <span data-ttu-id="462ea-109">在 [建議] 刀鋒視窗中，選取 [新增新一代防火牆]。</span><span class="sxs-lookup"><span data-stu-id="462ea-109">In the **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="462ea-110">![][1]</span><span class="sxs-lookup"><span data-stu-id="462ea-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="462ea-111">在 [新增新一代防火牆]  刀鋒視窗中，選取一個端點。</span><span class="sxs-lookup"><span data-stu-id="462ea-111">In the **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="462ea-112">![選取端點][2]</span><span class="sxs-lookup"><span data-stu-id="462ea-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="462ea-113">第二個 [新增新一代防火牆]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="462ea-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="462ea-114">您可以選擇使用現有的解決方案 (如果有的話)，或是建立新的解決方案。</span><span class="sxs-lookup"><span data-stu-id="462ea-114">You can choose to use an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="462ea-115">此範例中沒有任何可用的現有解決方案，因此我們將建立一個 NGFW。</span><span class="sxs-lookup"><span data-stu-id="462ea-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="462ea-116">![新建新一代防火牆][3]</span><span class="sxs-lookup"><span data-stu-id="462ea-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="462ea-117">若要建立 NGFW，請從整合式合作夥伴的清單中選取一個解決方案。</span><span class="sxs-lookup"><span data-stu-id="462ea-117">To create an NGFW, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="462ea-118">在此範例中，我們會選取 [檢查點]。</span><span class="sxs-lookup"><span data-stu-id="462ea-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="462ea-119">![選取新一代防火牆解決方案][4]</span><span class="sxs-lookup"><span data-stu-id="462ea-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="462ea-120">[檢查點]  刀鋒視窗隨即開啟，為您提供合作夥伴解決方案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="462ea-120">The **Check Point** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="462ea-121">選取資訊刀鋒視窗中的 [建立]  。</span><span class="sxs-lookup"><span data-stu-id="462ea-121">Select **Create** in the information blade.</span></span>
   <span data-ttu-id="462ea-122">![防火牆資訊刀鋒視窗][5]</span><span class="sxs-lookup"><span data-stu-id="462ea-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="462ea-123">[建立虛擬機器]  刀鋒視窗就會開啟。</span><span class="sxs-lookup"><span data-stu-id="462ea-123">The **Create virtual machine** blade opens.</span></span> <span data-ttu-id="462ea-124">您可在此輸入啟動將執行 NGFW 的虛擬機器 (VM) 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="462ea-124">Here you can enter information required to spin up a virtual machine (VM) that runs the NGFW.</span></span> <span data-ttu-id="462ea-125">依照下列步驟執行，並提供所需的 NGFW 資訊。</span><span class="sxs-lookup"><span data-stu-id="462ea-125">Follow the steps and provide the NGFW information required.</span></span> <span data-ttu-id="462ea-126">選取 [確定] 以套用。</span><span class="sxs-lookup"><span data-stu-id="462ea-126">Select OK to apply.</span></span>
   <span data-ttu-id="462ea-127">![建立虛擬機器以執行 NGFW][6]</span><span class="sxs-lookup"><span data-stu-id="462ea-127">![Create virtual machine to run NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="462ea-128">僅透過 NGFW 路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="462ea-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="462ea-129">返回 [建議]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="462ea-129">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="462ea-130">在您透過資訊安全中心加入 NGFW 後會產生新的項目，稱為「僅透過 NGFW 路由傳送流量」 。</span><span class="sxs-lookup"><span data-stu-id="462ea-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="462ea-131">只有當您透過資訊安全中心安裝了 NGFW，才會建立這項建議。</span><span class="sxs-lookup"><span data-stu-id="462ea-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="462ea-132">如果您有網際網路面向的端點，資訊安全中心會建議您設定網路安全性群組規則，強制透過 NGFW 將輸入流量傳送到 VM。</span><span class="sxs-lookup"><span data-stu-id="462ea-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic to your VM through your NGFW.</span></span>

1. <span data-ttu-id="462ea-133">在 [建議] 刀鋒視窗中，選取 [僅透過 NGFW 路由傳送流量]。</span><span class="sxs-lookup"><span data-stu-id="462ea-133">In the **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="462ea-134">![僅透過 NGFW 路由傳送流量][7]</span><span class="sxs-lookup"><span data-stu-id="462ea-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="462ea-135">這樣會開啟 [僅透過 NGFW 路由傳送流量] 刀鋒視窗，其中列出您可以路由傳送流量的 VM。</span><span class="sxs-lookup"><span data-stu-id="462ea-135">This opens the blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="462ea-136">從清單中選取 VM。</span><span class="sxs-lookup"><span data-stu-id="462ea-136">Select a VM from the list.</span></span>
   <span data-ttu-id="462ea-137">![選取 VM][8]</span><span class="sxs-lookup"><span data-stu-id="462ea-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="462ea-138">所選 VM 的刀鋒視窗隨即開啟，其中顯示相關的輸入規則。</span><span class="sxs-lookup"><span data-stu-id="462ea-138">A blade for the selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="462ea-139">說明提供後續可能步驟的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="462ea-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="462ea-140">選取 [編輯輸入規則]  繼續編輯輸入規則。</span><span class="sxs-lookup"><span data-stu-id="462ea-140">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span> <span data-ttu-id="462ea-141">預期的情況是與 NGFW 連結的網際網路面向端點其 [來源] 不設定為 [任何]。</span><span class="sxs-lookup"><span data-stu-id="462ea-141">The expectation is that **Source** is not set to **Any** for the Internet-facing endpoints linked with the NGFW.</span></span> <span data-ttu-id="462ea-142">若要深入了解輸入規則的內容，請參閱 [NSG 規則](../virtual-network/virtual-networks-nsg.md#nsg-rules)。</span><span class="sxs-lookup"><span data-stu-id="462ea-142">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="462ea-143">![設定規則以限制存取][9]
   ![編輯輸入規則][10]</span><span class="sxs-lookup"><span data-stu-id="462ea-143">![Configure rules to limit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="462ea-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="462ea-144">See also</span></span>
<span data-ttu-id="462ea-145">本文件說明如何實作資訊安全中心建議的「新增新一代防火牆」。</span><span class="sxs-lookup"><span data-stu-id="462ea-145">This document showed you how to implement the Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="462ea-146">若要了解 NGFW 與檢查點合作夥伴解決方案的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="462ea-146">To learn more about NGFWs and the Check Point partner solution, see the following:</span></span>

* [<span data-ttu-id="462ea-147">新一代防火牆</span><span class="sxs-lookup"><span data-stu-id="462ea-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="462ea-148">檢查點 vSEC</span><span class="sxs-lookup"><span data-stu-id="462ea-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="462ea-149">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="462ea-149">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="462ea-150">[設定 Azure 資訊安全中心的安全性原則](security-center-policies.md) -- 了解如何設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="462ea-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="462ea-151">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="462ea-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="462ea-152">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) -- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="462ea-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="462ea-153">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="462ea-153">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="462ea-154">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) -- 了解如何監視合作夥伴解決方案的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="462ea-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="462ea-155">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="462ea-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="462ea-156">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="462ea-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

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
