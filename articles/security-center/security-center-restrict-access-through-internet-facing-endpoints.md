---
title: "透過 Azure 資訊安全中心中的網際網路對向端點 aaaRestrict 存取 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 限制存取透過網際網路對向端點 * *。"
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
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="b16b6-103">在 Azure 資訊安全中心限制透過網際網路面向端點的存取</span><span class="sxs-lookup"><span data-stu-id="b16b6-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="b16b6-104">如果您的任一網路安全性群組 (NSG) 有一或多個輸入規則允許來自任何來源 IP 位址的存取，Azure 資訊安全中心會建議您限制透過網際網路面向端點的存取。</span><span class="sxs-lookup"><span data-stu-id="b16b6-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="b16b6-105">開啟存取太 「 任何 」 可能會讓攻擊者 tooaccess 您的資源。</span><span class="sxs-lookup"><span data-stu-id="b16b6-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="b16b6-106">資訊安全中心會建議您編輯這些輸入的規則 toorestrict 存取 toosource IP 位址，實際需要的存取。</span><span class="sxs-lookup"><span data-stu-id="b16b6-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="b16b6-107">有「任何」來源的任何非 Web 連接埠，就會產生這項建議。</span><span class="sxs-lookup"><span data-stu-id="b16b6-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="b16b6-108">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="b16b6-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="b16b6-109">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="b16b6-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="b16b6-110">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="b16b6-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="b16b6-111">在 hello**建議刀鋒視窗**，選取**限制存取透過網際網路對向端點**。</span><span class="sxs-lookup"><span data-stu-id="b16b6-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![限制透過網際網路面向端點的存取][1]
2. <span data-ttu-id="b16b6-113">這會開啟刀鋒視窗中 hello**限制存取透過網際網路對向端點**。</span><span class="sxs-lookup"><span data-stu-id="b16b6-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="b16b6-114">此刀鋒視窗會列出 hello 虛擬機器 (Vm) 的輸入建立潛在的安全性問題的規則。</span><span class="sxs-lookup"><span data-stu-id="b16b6-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="b16b6-115">選取 VM。</span><span class="sxs-lookup"><span data-stu-id="b16b6-115">Select a VM.</span></span>

   ![選取 VM][2]
3. <span data-ttu-id="b16b6-117">hello **NSG**刀鋒視窗會顯示網路安全性群組的詳細資訊，相關的輸入規則，以及 hello 相關聯的 VM。</span><span class="sxs-lookup"><span data-stu-id="b16b6-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="b16b6-118">選取**編輯輸入的規則**tooproceed 編輯的輸入的規則。</span><span class="sxs-lookup"><span data-stu-id="b16b6-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![[網路安全性群組] 刀鋒視窗][3]
4. <span data-ttu-id="b16b6-120">在 hello**輸入安全性規則**刀鋒視窗中選取 hello tooedit 輸入的規則。</span><span class="sxs-lookup"><span data-stu-id="b16b6-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="b16b6-121">在此範例中，我們選取 [允許 Web] 。</span><span class="sxs-lookup"><span data-stu-id="b16b6-121">In this example, let’s select **AllowWeb**.</span></span>

   ![輸入安全性規則][4]

   <span data-ttu-id="b16b6-123">請注意，您也可以選取**預設規則**toosee hello 組由所有 Nsg 包含預設規則。</span><span class="sxs-lookup"><span data-stu-id="b16b6-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="b16b6-124">無法刪除 hello 預設規則，但因為他們指派較低的優先順序，它們會覆寫由您所建立的 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="b16b6-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="b16b6-125">深入了解[預設規則](../virtual-network/virtual-networks-nsg.md#default-rules)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![預設規則][5]
5. <span data-ttu-id="b16b6-127">在 hello **AllowWeb**刀鋒視窗中，編輯 hello 屬性，因此，hello hello 輸入規則的**來源**是 IP 位址或 IP 位址區塊。</span><span class="sxs-lookup"><span data-stu-id="b16b6-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="b16b6-128">toolearn 進一步了解 hello 屬性 hello 輸入規則，請參閱[NSG 規則](../virtual-network/virtual-networks-nsg.md#nsg-rules)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![編輯輸入規則][6]

## <a name="see-also"></a><span data-ttu-id="b16b6-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b16b6-130">See also</span></span>
<span data-ttu-id="b16b6-131">本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議 「 限制存取透過網際網路對向端點 」。</span><span class="sxs-lookup"><span data-stu-id="b16b6-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="b16b6-132">toolearn 進一步了解啟用 Nsg 及規則，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="b16b6-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="b16b6-133">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="b16b6-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="b16b6-134">如何使用 toomanage Nsg hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b16b6-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="b16b6-135">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="b16b6-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="b16b6-136">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="b16b6-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b16b6-137">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md)-- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b16b6-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b16b6-138">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="b16b6-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="b16b6-139">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)-了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="b16b6-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="b16b6-140">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="b16b6-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="b16b6-141">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="b16b6-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="b16b6-142">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。</span><span class="sxs-lookup"><span data-stu-id="b16b6-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
