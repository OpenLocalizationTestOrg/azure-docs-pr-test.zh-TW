---
title: "aaaEnable Azure 資訊安全中心中的網路安全性群組 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 啟用網路安全性群組 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="eaf85-103">在 Azure 資訊安全中心啟用網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="eaf85-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="eaf85-104">如果尚未啟用網路安全性群組 (NSG)，Azure 資訊安全中心會建議您啟用。</span><span class="sxs-lookup"><span data-stu-id="eaf85-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="eaf85-105">Nsg 包含存取控制清單 (ACL) 規則，允許或拒絕網路流量 tooyour 虛擬網路中的 VM 執行個體的清單。</span><span class="sxs-lookup"><span data-stu-id="eaf85-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="eaf85-106">NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。</span><span class="sxs-lookup"><span data-stu-id="eaf85-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="eaf85-107">NSG 與子網路產生關聯時，hello ACL 規則適用於 tooall hello VM 執行個體中子網路。</span><span class="sxs-lookup"><span data-stu-id="eaf85-107">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="eaf85-108">此外，流量 tooan 個別 VM 可能會限制進一步將 NSG 直接 toothat VM。</span><span class="sxs-lookup"><span data-stu-id="eaf85-108">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span> <span data-ttu-id="eaf85-109">toolearn 更看到[網路安全性群組 (NSG) 是什麼？](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="eaf85-109">toolearn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="eaf85-110">如果您沒有啟用 Nsg，資訊安全中心會呈現兩個建議 tooyou： 啟用網路安全性群組的相關子網路和虛擬機器上啟用網路安全性群組上。</span><span class="sxs-lookup"><span data-stu-id="eaf85-110">If you do not have NSGs enabled, Security Center presents two recommendations tooyou: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="eaf85-111">您選擇哪一個層級、 子網路或 VM，tooapply Nsg。</span><span class="sxs-lookup"><span data-stu-id="eaf85-111">You choose which level, subnet or VM, tooapply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="eaf85-112">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="eaf85-112">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="eaf85-113">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="eaf85-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="eaf85-114">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="eaf85-114">Implement hello recommendation</span></span>
1. <span data-ttu-id="eaf85-115">在 hello**建議**刀鋒視窗中，選取**啟用網路安全性群組**子網路上或在虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="eaf85-115">In hello **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="eaf85-116">![啟用網路安全性群組][1]</span><span class="sxs-lookup"><span data-stu-id="eaf85-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="eaf85-117">這會開啟刀鋒視窗中 hello**設定遺失的網路安全性群組**子網路或虛擬機器，根據您選取的 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="eaf85-117">This opens hello blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on hello recommendation that you selected.</span></span> <span data-ttu-id="eaf85-118">選取子網路或虛擬機器 tooconfigure NSG 上。</span><span class="sxs-lookup"><span data-stu-id="eaf85-118">Select a subnet or a virtual machine tooconfigure an NSG on.</span></span>

   ![針對子網路設定 NSG][2]

   ![針對 VM 設定 NSG][3]
3. <span data-ttu-id="eaf85-121">在 hello**選擇網路安全性群組**刀鋒視窗中，選取現有的 NSG，或選取**建立新**toocreate NSG。</span><span class="sxs-lookup"><span data-stu-id="eaf85-121">On hello **Choose network security group** blade, select an existing NSG or select **Create new** toocreate an NSG.</span></span>

   ![選擇網路安全性群組][4]

<span data-ttu-id="eaf85-123">如果您建立 NSG，請依照下列中的 hello 步驟[toomanage Nsg 使用 hello Azure 入口網站的方式](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)toocreate NSG 並設定安全性規則。</span><span class="sxs-lookup"><span data-stu-id="eaf85-123">If you create an NSG, follow hello steps in [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="eaf85-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="eaf85-124">See also</span></span>
<span data-ttu-id="eaf85-125">這篇文章會示範如何 tooimplement 會 hello 資訊安全中心建議 」 啟用網路安全性群組 」 的子網路或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="eaf85-125">This article showed you how tooimplement hello Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="eaf85-126">toolearn 進一步了解啟用 Nsg，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="eaf85-126">toolearn more about enabling NSGs, see hello following:</span></span>

* [<span data-ttu-id="eaf85-127">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="eaf85-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="eaf85-128">如何使用 toomanage Nsg hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="eaf85-128">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="eaf85-129">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="eaf85-129">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="eaf85-130">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="eaf85-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="eaf85-131">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="eaf85-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="eaf85-132">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="eaf85-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="eaf85-133">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="eaf85-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="eaf85-134">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="eaf85-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="eaf85-135">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="eaf85-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="eaf85-136">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。</span><span class="sxs-lookup"><span data-stu-id="eaf85-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
