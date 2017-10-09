---
title: "aaaInstall Azure 資訊安全中心中的 Endpoint Protection |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 安裝 Endpoint Protection * *。"
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
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="f4893-103">在 Azure 資訊安全中心安裝端點保護</span><span class="sxs-lookup"><span data-stu-id="f4893-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="f4893-104">如果尚未啟用 Endpoint Protection，則 Azure 資訊安全中心建議您在 Azure 虛擬機器 (VM) 上安裝 Endpoint Protection。</span><span class="sxs-lookup"><span data-stu-id="f4893-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="f4893-105">這項建議適用於僅 tooWindows Vm。</span><span class="sxs-lookup"><span data-stu-id="f4893-105">This recommendation applies tooWindows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="f4893-106">此範例部署會使用 Microsoft Antimalware。</span><span class="sxs-lookup"><span data-stu-id="f4893-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="f4893-107">請參閱 [Azure 資訊安全中心中的夥伴整合](security-center-partner-integration.md#partners-that-integrate-with-security-center)以取得與資訊安全中心整合的夥伴清單。</span><span class="sxs-lookup"><span data-stu-id="f4893-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="f4893-108">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="f4893-108">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="f4893-109">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="f4893-109">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="f4893-110">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="f4893-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="f4893-111">在 hello**建議**刀鋒視窗中，選取**安裝 Endpoint Protection**。</span><span class="sxs-lookup"><span data-stu-id="f4893-111">In hello **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="f4893-112">![選取安裝端點保護][1]</span><span class="sxs-lookup"><span data-stu-id="f4893-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="f4893-113">hello**安裝 Endpoint Protection**刀鋒視窗隨即開啟並顯示沒有端點保護的 Vm 清單。</span><span class="sxs-lookup"><span data-stu-id="f4893-113">hello **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="f4893-114">選取從 hello 清單 hello Vm 上想 tooinstall endpoint protection，並按一下**Vm 上安裝**。</span><span class="sxs-lookup"><span data-stu-id="f4893-114">Select from hello list hello VMs that you want tooinstall endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="f4893-115">![在 選取 Vm tooinstall Endpoint Protection][2]</span><span class="sxs-lookup"><span data-stu-id="f4893-115">![Select VMs tooinstall Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="f4893-116">hello**選取 Endpoint Protection**刀鋒視窗會開啟 tooallow 您 tooselect hello 端點保護解決方案想 toouse。</span><span class="sxs-lookup"><span data-stu-id="f4893-116">hello **Select Endpoint Protection** blade opens tooallow you tooselect hello endpoint protection solution you want toouse.</span></span> <span data-ttu-id="f4893-117">在此範例中，讓我們選取 [Microsoft Antimalware] 。</span><span class="sxs-lookup"><span data-stu-id="f4893-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="f4893-118">![][3]</span><span class="sxs-lookup"><span data-stu-id="f4893-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="f4893-119">會顯示 hello 端點保護解決方案的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="f4893-119">Additional information about hello endpoint protection solution is displayed.</span></span> <span data-ttu-id="f4893-120">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="f4893-120">Select **Create**.</span></span>
   <span data-ttu-id="f4893-121">![建立反惡意程式碼解決方案][4]</span><span class="sxs-lookup"><span data-stu-id="f4893-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="f4893-122">Hello 上輸入 hello 所需的組態設定**加入擴充**刀鋒視窗中，然後再選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="f4893-122">Enter hello required configuration settings on hello **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="f4893-123">toolearn 深入了解 hello 組態設定，請參閱[預設和自訂反惡意程式碼設定](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration)。</span><span class="sxs-lookup"><span data-stu-id="f4893-123">toolearn more about hello configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="f4893-124">[Microsoft 反惡意程式碼](../security/azure-security-antimalware.md)現在 hello 上的作用中選取 Vm。</span><span class="sxs-lookup"><span data-stu-id="f4893-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="f4893-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f4893-125">See also</span></span>
<span data-ttu-id="f4893-126">本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議 < 安裝 Endpoint Protection >。</span><span class="sxs-lookup"><span data-stu-id="f4893-126">This article showed you how tooimplement hello Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="f4893-127">toolearn 進一步了解啟用 Microsoft 反惡意程式碼在 Azure 中，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4893-127">toolearn more about enabling Microsoft Antimalware in Azure, see hello following document:</span></span>

* <span data-ttu-id="f4893-128">[雲端服務和虛擬機器的 Microsoft 反惡意程式碼](../security/azure-security-antimalware.md)-了解如何 toodeploy Microsoft 反惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="f4893-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how toodeploy Microsoft Antimalware.</span></span>

<span data-ttu-id="f4893-129">toolearn 有關資訊安全中心的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4893-129">toolearn more about Security Center, see hello following documents:</span></span>

* <span data-ttu-id="f4893-130">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 安全性原則。</span><span class="sxs-lookup"><span data-stu-id="f4893-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="f4893-131">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f4893-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f4893-132">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="f4893-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="f4893-133">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="f4893-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="f4893-134">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="f4893-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="f4893-135">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="f4893-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="f4893-136">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="f4893-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
