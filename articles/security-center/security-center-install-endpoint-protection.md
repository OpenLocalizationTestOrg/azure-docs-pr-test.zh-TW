---
title: "在 Azure 資訊安全中心安裝端點保護 | Microsoft Docs"
description: "本文件說明如何實作 Azure 資訊安全中心建議的「安裝端點保護」。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="b90ae-103">在 Azure 資訊安全中心安裝端點保護</span><span class="sxs-lookup"><span data-stu-id="b90ae-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="b90ae-104">如果尚未啟用 Endpoint Protection，則 Azure 資訊安全中心建議您在 Azure 虛擬機器 (VM) 上安裝 Endpoint Protection。</span><span class="sxs-lookup"><span data-stu-id="b90ae-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="b90ae-105">這項建議僅適用於 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="b90ae-105">This recommendation applies to Windows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="b90ae-106">此範例部署會使用 Microsoft Antimalware。</span><span class="sxs-lookup"><span data-stu-id="b90ae-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="b90ae-107">請參閱 [Azure 資訊安全中心中的夥伴整合](security-center-partner-integration.md#partners-that-integrate-with-security-center)以取得與資訊安全中心整合的夥伴清單。</span><span class="sxs-lookup"><span data-stu-id="b90ae-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="b90ae-108">實作建議</span><span class="sxs-lookup"><span data-stu-id="b90ae-108">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="b90ae-109">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="b90ae-109">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="b90ae-110">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="b90ae-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="b90ae-111">在 [建議] 刀鋒視窗中，選取 [安裝端點保護]。</span><span class="sxs-lookup"><span data-stu-id="b90ae-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="b90ae-112">![選取安裝端點保護][1]</span><span class="sxs-lookup"><span data-stu-id="b90ae-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="b90ae-113">[安裝 Endpoint Protection] 刀鋒視窗隨即開啟，並顯示沒有 Endpoint Protection 的 VM 清單。</span><span class="sxs-lookup"><span data-stu-id="b90ae-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="b90ae-114">從清單中選取您想要安裝 Endpoint Protection 的 VM，然後按一下 [在 VM 上安裝]。</span><span class="sxs-lookup"><span data-stu-id="b90ae-114">Select from the list the VMs that you want to install endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="b90ae-115">![選取要安裝 Endpoint Protection 的 VM][2]</span><span class="sxs-lookup"><span data-stu-id="b90ae-115">![Select VMs to install Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="b90ae-116">[選取 Endpoint Protection] 刀鋒視窗隨即開啟，讓您選取想要使用的 Endpoint Protection 解決方案。</span><span class="sxs-lookup"><span data-stu-id="b90ae-116">The **Select Endpoint Protection** blade opens to allow you to select the endpoint protection solution you want to use.</span></span> <span data-ttu-id="b90ae-117">在此範例中，讓我們選取 [Microsoft Antimalware] 。</span><span class="sxs-lookup"><span data-stu-id="b90ae-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="b90ae-118">![][3]</span><span class="sxs-lookup"><span data-stu-id="b90ae-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="b90ae-119">將會顯示 Endpoint Protection 解決方案的其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b90ae-119">Additional information about the endpoint protection solution is displayed.</span></span> <span data-ttu-id="b90ae-120">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="b90ae-120">Select **Create**.</span></span>
   <span data-ttu-id="b90ae-121">![建立反惡意程式碼解決方案][4]</span><span class="sxs-lookup"><span data-stu-id="b90ae-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="b90ae-122">在 [加入擴充功能] 刀鋒視窗上輸入必要的組態設定，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b90ae-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="b90ae-123">若要深入了解組態設定，請參閱 [預設和自訂的反惡意程式碼組態](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration)。</span><span class="sxs-lookup"><span data-stu-id="b90ae-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="b90ae-124">[Microsoft Antimalware](../security/azure-security-antimalware.md)現在已在選取的 VM 上使用。</span><span class="sxs-lookup"><span data-stu-id="b90ae-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="b90ae-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b90ae-125">See also</span></span>
<span data-ttu-id="b90ae-126">本文說明了如何實作資訊安全中心建議的「安裝端點保護」。</span><span class="sxs-lookup"><span data-stu-id="b90ae-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="b90ae-127">若要深入了解如何在 Azure 中啟用反惡意程式碼軟體，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="b90ae-127">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span></span>

* <span data-ttu-id="b90ae-128">[適用於雲端服務和虛擬機器的 Microsoft Antimalware](../security/azure-security-antimalware.md) -- 了解如何部署 Microsoft Antimalware。</span><span class="sxs-lookup"><span data-stu-id="b90ae-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span></span>

<span data-ttu-id="b90ae-129">若要深入了解資訊安全中心，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="b90ae-129">To learn more about Security Center, see the following documents:</span></span>

* <span data-ttu-id="b90ae-130">[設定 Azure 資訊安全中心的安全性原則](security-center-policies.md) -- 了解如何設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="b90ae-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="b90ae-131">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b90ae-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b90ae-132">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) -- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="b90ae-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="b90ae-133">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="b90ae-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="b90ae-134">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) -- 了解如何監視合作夥伴解決方案的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="b90ae-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="b90ae-135">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="b90ae-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="b90ae-136">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="b90ae-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
