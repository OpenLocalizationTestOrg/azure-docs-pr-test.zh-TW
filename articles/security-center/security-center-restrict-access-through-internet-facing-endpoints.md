---
title: "在 Azure 資訊安全中心限制透過網際網路面向端點的存取 | Microsoft Docs"
description: "本文件說明了如何實作 Azure 資訊安全中心建議的「限制透過網際網路面向端點的存取」。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: f7309c617f1705205e2c9f1b1b48d141391d45da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="ec569-103">在 Azure 資訊安全中心限制透過網際網路面向端點的存取</span><span class="sxs-lookup"><span data-stu-id="ec569-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="ec569-104">如果您的任一網路安全性群組 (NSG) 有一或多個輸入規則允許來自任何來源 IP 位址的存取，Azure 資訊安全中心會建議您限制透過網際網路面向端點的存取。</span><span class="sxs-lookup"><span data-stu-id="ec569-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="ec569-105">開放任一來源 IP 位址的存取可能會讓攻擊者存取您的資源。</span><span class="sxs-lookup"><span data-stu-id="ec569-105">Opening access to “any” may enable attackers to access your resources.</span></span> <span data-ttu-id="ec569-106">資訊安全中心會建議您編輯這些輸入規則，以限制只有實際上需要存取權的來源 IP 位址才能存取。</span><span class="sxs-lookup"><span data-stu-id="ec569-106">Security Center will recommend that you edit these inbound rules to restrict access to source IP addresses that actually need access.</span></span>

<span data-ttu-id="ec569-107">有「任何」來源的任何非 Web 連接埠，就會產生這項建議。</span><span class="sxs-lookup"><span data-stu-id="ec569-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="ec569-108">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="ec569-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="ec569-109">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="ec569-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="ec569-110">實作建議</span><span class="sxs-lookup"><span data-stu-id="ec569-110">Implement the recommendation</span></span>
1. <span data-ttu-id="ec569-111">在 [建議] 刀鋒視窗中，選取 [限制透過網際網路面向端點的存取]。</span><span class="sxs-lookup"><span data-stu-id="ec569-111">In the **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![限制透過網際網路面向端點的存取][1]
2. <span data-ttu-id="ec569-113">這樣會開啟 [限制透過網際網路面向端點的存取] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ec569-113">This opens the blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="ec569-114">此刀鋒視窗會列出虛擬機器 (VM) 與導致潛在安全性問題的輸入規則。</span><span class="sxs-lookup"><span data-stu-id="ec569-114">This blade lists the virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="ec569-115">選取 VM。</span><span class="sxs-lookup"><span data-stu-id="ec569-115">Select a VM.</span></span>

   ![選取 VM][2]
3. <span data-ttu-id="ec569-117">[NSG]  刀鋒視窗會顯示網路安全性群組資訊、相關的輸入規則和關聯的 VM。</span><span class="sxs-lookup"><span data-stu-id="ec569-117">The **NSG** blade displays Network Security Group information, related inbound rules, and the associated VM.</span></span> <span data-ttu-id="ec569-118">選取 [編輯輸入規則]  繼續編輯輸入規則。</span><span class="sxs-lookup"><span data-stu-id="ec569-118">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span>

   ![[網路安全性群組] 刀鋒視窗][3]
4. <span data-ttu-id="ec569-120">在 [輸入安全性規則]  刀鋒視窗中選取要編輯的輸入規則。</span><span class="sxs-lookup"><span data-stu-id="ec569-120">On the **Inbound security rules** blade select the inbound rule to edit.</span></span> <span data-ttu-id="ec569-121">在此範例中，我們選取 [允許 Web] 。</span><span class="sxs-lookup"><span data-stu-id="ec569-121">In this example, let’s select **AllowWeb**.</span></span>

   ![輸入安全性規則][4]

   <span data-ttu-id="ec569-123">注意，您也可以選取 [預設規則]  以查看所有 NSG 包含的預設規則集。</span><span class="sxs-lookup"><span data-stu-id="ec569-123">Note, you can also select **Default rules** to see the set of default rules contained by all NSGs.</span></span> <span data-ttu-id="ec569-124">預設規則無法刪除，但因為其會指派為較低優先權，因此可以由您所建立的規則覆寫預設規則。</span><span class="sxs-lookup"><span data-stu-id="ec569-124">The default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by the rules that you create.</span></span> <span data-ttu-id="ec569-125">深入了解[預設規則](../virtual-network/virtual-networks-nsg.md#default-rules)。</span><span class="sxs-lookup"><span data-stu-id="ec569-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![預設規則][5]
5. <span data-ttu-id="ec569-127">在 [允許 Web] 刀鋒視窗中編輯輸入規則的內容，讓**來源**是 IP 位址或 IP 位址區塊。</span><span class="sxs-lookup"><span data-stu-id="ec569-127">On the **AllowWeb** blade, edit the properties of the inbound rule so that the **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="ec569-128">若要深入了解輸入規則的內容，請參閱 [NSG 規則](../virtual-network/virtual-networks-nsg.md#nsg-rules)。</span><span class="sxs-lookup"><span data-stu-id="ec569-128">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![編輯輸入規則][6]

## <a name="see-also"></a><span data-ttu-id="ec569-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ec569-130">See also</span></span>
<span data-ttu-id="ec569-131">本文說明了如何實作資訊安全中心建議的「限制透過網際網路面向端點的存取」。</span><span class="sxs-lookup"><span data-stu-id="ec569-131">This article showed you how to implement the Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="ec569-132">若要深入了解啟用 NSG 與規則，請參閱下列項目：</span><span class="sxs-lookup"><span data-stu-id="ec569-132">To learn more about enabling NSGs and rules, see the following:</span></span>

* [<span data-ttu-id="ec569-133">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="ec569-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="ec569-134">如何使用 Azure 入口網站管理 NSG</span><span class="sxs-lookup"><span data-stu-id="ec569-134">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="ec569-135">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="ec569-135">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="ec569-136">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md)--了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="ec569-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ec569-137">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md)-- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ec569-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ec569-138">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md)-- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="ec569-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="ec569-139">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md)-- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="ec569-139">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="ec569-140">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) -- 了解如何監視合作夥伴解決方案的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="ec569-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="ec569-141">[Azure 資訊安全中心常見問題集](security-center-faq.md)-- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="ec569-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ec569-142">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-- 取得最新的 Azure 安全性新聞和資訊。</span><span class="sxs-lookup"><span data-stu-id="ec569-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
