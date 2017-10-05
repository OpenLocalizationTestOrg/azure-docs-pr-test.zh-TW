---
title: "在 Azure 資訊安全中心套用系統更新 | Microsoft Docs"
description: "本文件說明如何實作 Azure 資訊安全中心建議的「套用系統更新」和「在系統更新之後重新開機」。"
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
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="950cc-103">在 Azure 資訊安全中心套用系統更新</span><span class="sxs-lookup"><span data-stu-id="950cc-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="950cc-104">Azure 資訊安全中心每日監視 Windows 和 Linux 虛擬機器 (VM) 是否有遺漏的作業系統更新。</span><span class="sxs-lookup"><span data-stu-id="950cc-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="950cc-105">資訊安全中心會根據 Windows VM 上設定的服務，從 Windows Update 或 Windows Server Update Services (WSUS) 擷取可用的安全性和重大更新清單。</span><span class="sxs-lookup"><span data-stu-id="950cc-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="950cc-106">資訊安全中心也會檢查 Linux 系統中的最新更新。</span><span class="sxs-lookup"><span data-stu-id="950cc-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="950cc-107">如果您的 VM 遺漏系統更新，資訊安全中心會建議您套用系統更新</span><span class="sxs-lookup"><span data-stu-id="950cc-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="950cc-108">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="950cc-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="950cc-109">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="950cc-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="950cc-110">實作建議</span><span class="sxs-lookup"><span data-stu-id="950cc-110">Implement the recommendation</span></span>
1. <span data-ttu-id="950cc-111">在 [建議] 刀鋒視窗中，選取 [套用系統更新]。</span><span class="sxs-lookup"><span data-stu-id="950cc-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![套用系統更新][1]
2. <span data-ttu-id="950cc-113">[套用系統更新]  刀鋒視窗會開啟，顯示 VM 遺漏的系統更新的清單。</span><span class="sxs-lookup"><span data-stu-id="950cc-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="950cc-114">選取 VM。</span><span class="sxs-lookup"><span data-stu-id="950cc-114">Select a VM.</span></span>

   ![選取 VM][2]
3. <span data-ttu-id="950cc-116">隨即開啟一個刀鋒視窗，其中顯示該 VM 的遺漏更新的清單。</span><span class="sxs-lookup"><span data-stu-id="950cc-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="950cc-117">選取系統更新。</span><span class="sxs-lookup"><span data-stu-id="950cc-117">Select a system update.</span></span> <span data-ttu-id="950cc-118">在此範例中，我們選取 KB3156016。</span><span class="sxs-lookup"><span data-stu-id="950cc-118">In this example, let’s select KB3156016.</span></span>

   ![遺漏的安全性更新][3]

4. <span data-ttu-id="950cc-120">請依照 [安全性更新]  刀鋒視窗中的步驟，套用遺漏的更新。</span><span class="sxs-lookup"><span data-stu-id="950cc-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![安全性更新][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="950cc-122">在系統更新之後重新開機</span><span class="sxs-lookup"><span data-stu-id="950cc-122">Reboot after system updates</span></span>
1. <span data-ttu-id="950cc-123">返回 [建議]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="950cc-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="950cc-124">在您套用系統更新之後會產生新的項目，稱為「在系統更新之後重新開機」。</span><span class="sxs-lookup"><span data-stu-id="950cc-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="950cc-125">此項目可讓您知道您需要重新啟動 VM 以完成套用系統更新的程序。</span><span class="sxs-lookup"><span data-stu-id="950cc-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![在系統更新之後重新開機][5]
2. <span data-ttu-id="950cc-127">選取 [在系統更新之後重新開機] 。</span><span class="sxs-lookup"><span data-stu-id="950cc-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="950cc-128">這會開啟 [重新啟動正在等待以完成系統更新]  刀鋒視窗，其中顯示 VM，您必須加以重新啟動才能完成套用系統清單更新的程序。</span><span class="sxs-lookup"><span data-stu-id="950cc-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![重新啟動擱置中][6]

<span data-ttu-id="950cc-130">從 Azure 重新啟動 VM 以完成程序。</span><span class="sxs-lookup"><span data-stu-id="950cc-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="950cc-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="950cc-131">See also</span></span>
<span data-ttu-id="950cc-132">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="950cc-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="950cc-133">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) --了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="950cc-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="950cc-134">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="950cc-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="950cc-135">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) -- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="950cc-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="950cc-136">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="950cc-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="950cc-137">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) -- 了解如何監視合作夥伴解決方案的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="950cc-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="950cc-138">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="950cc-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="950cc-139">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="950cc-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
