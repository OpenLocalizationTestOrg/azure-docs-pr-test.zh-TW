---
title: "在 Azure 資訊安全中心 aaaApply 系統更新 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議 * * 套用系統更新 * * 和 * * 在系統更新 * * 後重新開機。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="4581c-103">在 Azure 資訊安全中心套用系統更新</span><span class="sxs-lookup"><span data-stu-id="4581c-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="4581c-104">Azure 資訊安全中心每日監視 Windows 和 Linux 虛擬機器 (VM) 是否有遺漏的作業系統更新。</span><span class="sxs-lookup"><span data-stu-id="4581c-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="4581c-105">資訊安全中心會根據 Windows VM 上設定的服務，從 Windows Update 或 Windows Server Update Services (WSUS) 擷取可用的安全性和重大更新清單。</span><span class="sxs-lookup"><span data-stu-id="4581c-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="4581c-106">資訊安全中心也會檢查 hello 最新更新 Linux 系統中。</span><span class="sxs-lookup"><span data-stu-id="4581c-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="4581c-107">如果您的 VM 遺漏系統更新，資訊安全中心會建議您套用系統更新</span><span class="sxs-lookup"><span data-stu-id="4581c-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="4581c-108">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="4581c-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="4581c-109">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="4581c-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="4581c-110">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="4581c-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="4581c-111">在 hello**建議**刀鋒視窗中，選取**套用系統更新**。</span><span class="sxs-lookup"><span data-stu-id="4581c-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![套用系統更新][1]
2. <span data-ttu-id="4581c-113">hello**套用系統更新**刀鋒視窗隨即開啟並顯示遺漏的系統更新 Vm 的清單。</span><span class="sxs-lookup"><span data-stu-id="4581c-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="4581c-114">選取 VM。</span><span class="sxs-lookup"><span data-stu-id="4581c-114">Select a VM.</span></span>

   ![選取 VM][2]
3. <span data-ttu-id="4581c-116">隨即開啟一個刀鋒視窗，其中顯示該 VM 的遺漏更新的清單。</span><span class="sxs-lookup"><span data-stu-id="4581c-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="4581c-117">選取系統更新。</span><span class="sxs-lookup"><span data-stu-id="4581c-117">Select a system update.</span></span> <span data-ttu-id="4581c-118">在此範例中，我們選取 KB3156016。</span><span class="sxs-lookup"><span data-stu-id="4581c-118">In this example, let’s select KB3156016.</span></span>

   ![遺漏的安全性更新][3]

4. <span data-ttu-id="4581c-120">Hello 中的 hello 步驟**安全性更新**刀鋒視窗 tooapply hello 遺失更新。</span><span class="sxs-lookup"><span data-stu-id="4581c-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![安全性更新][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="4581c-122">在系統更新之後重新開機</span><span class="sxs-lookup"><span data-stu-id="4581c-122">Reboot after system updates</span></span>
1. <span data-ttu-id="4581c-123">傳回 toohello**建議**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4581c-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="4581c-124">在您套用系統更新之後會產生新的項目，稱為「在系統更新之後重新開機」。</span><span class="sxs-lookup"><span data-stu-id="4581c-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="4581c-125">此項目可讓您知道您需要 tooreboot hello VM toocomplete hello 套用的程序的系統更新。</span><span class="sxs-lookup"><span data-stu-id="4581c-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![在系統更新之後重新開機][5]
2. <span data-ttu-id="4581c-127">選取 [在系統更新之後重新開機] 。</span><span class="sxs-lookup"><span data-stu-id="4581c-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="4581c-128">這會開啟**重新啟動已暫止 toocomplete 系統更新**刀鋒視窗中顯示的 Vm，您需要 toorestart toocomplete hello 清單適用於系統更新程序。</span><span class="sxs-lookup"><span data-stu-id="4581c-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![重新啟動擱置中][6]

<span data-ttu-id="4581c-130">重新啟動 hello VM 從 Azure toocomplete hello 程序。</span><span class="sxs-lookup"><span data-stu-id="4581c-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="4581c-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4581c-131">See also</span></span>
<span data-ttu-id="4581c-132">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="4581c-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="4581c-133">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="4581c-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4581c-134">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="4581c-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4581c-135">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="4581c-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="4581c-136">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="4581c-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="4581c-137">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="4581c-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="4581c-138">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="4581c-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="4581c-139">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="4581c-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
