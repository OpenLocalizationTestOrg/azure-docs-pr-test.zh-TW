---
title: "修復 Azure 資訊安全中心的 OS 弱點 | Microsoft Docs"
description: "本文件說明如何實作 Azure 資訊安全中心建議的「修復 OS 弱點」。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="b4f55-103">修復 Azure 資訊安全中心的 OS 弱點</span><span class="sxs-lookup"><span data-stu-id="b4f55-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="b4f55-104">Azure 資訊安全中心每天會分析可能造成虛擬機器 (VM) 更容易受到攻擊的 VM 作業系統 (OS) 組態，並建議進行組態變更來處理這些弱點。</span><span class="sxs-lookup"><span data-stu-id="b4f55-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span></span> <span data-ttu-id="b4f55-105">當 VM 的 OS 設定不符合建議的設定規則時，資訊安全中心會建議您解決這些弱點。</span><span class="sxs-lookup"><span data-stu-id="b4f55-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="b4f55-106">如需受監視之特定設定的詳細資訊，請參閱[建議的設定規則清單](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)。</span><span class="sxs-lookup"><span data-stu-id="b4f55-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="b4f55-107">實作建議</span><span class="sxs-lookup"><span data-stu-id="b4f55-107">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="b4f55-108">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="b4f55-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="b4f55-109">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="b4f55-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="b4f55-110">在 [建議] 刀鋒視窗中，選取 [修復 OS 弱點]。</span><span class="sxs-lookup"><span data-stu-id="b4f55-110">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="b4f55-111">![修復 OS 弱點][1]</span><span class="sxs-lookup"><span data-stu-id="b4f55-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="b4f55-112">[修復 OS 弱點] 刀鋒視窗會開啟並列出您的 VM 和不符合建議的設定規則的 OS 設定。</span><span class="sxs-lookup"><span data-stu-id="b4f55-112">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span></span>  <span data-ttu-id="b4f55-113">針對每部 VM，此刀鋒視窗會識別︰</span><span class="sxs-lookup"><span data-stu-id="b4f55-113">For each VM, the blade identifies:</span></span>

   * <span data-ttu-id="b4f55-114">**失敗規則** -- VM 的 OS 設定不符合的規則數目。</span><span class="sxs-lookup"><span data-stu-id="b4f55-114">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span></span>
   * <span data-ttu-id="b4f55-115">**上次掃描時間** -- 資訊安全中心上次掃描 VM OS 設定的日期與時間。</span><span class="sxs-lookup"><span data-stu-id="b4f55-115">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span></span>
   * <span data-ttu-id="b4f55-116">**狀態** -- 弱點的目前狀態：</span><span class="sxs-lookup"><span data-stu-id="b4f55-116">**STATE** -- The current state of the vulnerability:</span></span>

     * <span data-ttu-id="b4f55-117">未處理：尚未解決的弱點</span><span class="sxs-lookup"><span data-stu-id="b4f55-117">Open: The vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="b4f55-118">進行中：正在將建議套用到弱點，您不需要採取任何動作</span><span class="sxs-lookup"><span data-stu-id="b4f55-118">In Progress: The vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="b4f55-119">已解決：弱點已解決 (問題已解決時，該項目會呈現灰色)。</span><span class="sxs-lookup"><span data-stu-id="b4f55-119">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span></span>
   * <span data-ttu-id="b4f55-120">**嚴重性** -- 所有弱點設為「低」嚴重性，表示弱點應解決，但不需要立即處理。</span><span class="sxs-lookup"><span data-stu-id="b4f55-120">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="b4f55-121">選取 VM。</span><span class="sxs-lookup"><span data-stu-id="b4f55-121">Select a VM.</span></span> <span data-ttu-id="b4f55-122">該 VM 的刀鋒視窗會開啟並顯示失敗的規則。</span><span class="sxs-lookup"><span data-stu-id="b4f55-122">A blade for that VM opens and displays the rules that have failed.</span></span>
   <span data-ttu-id="b4f55-123">![失敗的設定規則][2]</span><span class="sxs-lookup"><span data-stu-id="b4f55-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="b4f55-124">選取規則。</span><span class="sxs-lookup"><span data-stu-id="b4f55-124">Select a rule.</span></span> <span data-ttu-id="b4f55-125">在此範例中，我們選取 [密碼必須符合複雜性需求] 。</span><span class="sxs-lookup"><span data-stu-id="b4f55-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="b4f55-126">隨即開啟說明失敗的規則和影響的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b4f55-126">A blade opens describing the failed rule and the impact.</span></span> <span data-ttu-id="b4f55-127">檢閱詳細資訊，並考慮如何套用作業系統設定。</span><span class="sxs-lookup"><span data-stu-id="b4f55-127">Review the details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="b4f55-128">![失敗規則的說明][3]</span><span class="sxs-lookup"><span data-stu-id="b4f55-128">![Description for the failed rule][3]</span></span>

  <span data-ttu-id="b4f55-129">資訊安全中心會使用一般設定列舉 (CCE) 指派設定規則的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="b4f55-129">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="b4f55-130">此刀鋒視窗上提供下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="b4f55-130">The following information is provided on this blade:</span></span>

  - <span data-ttu-id="b4f55-131">名稱 -- 規則的名稱</span><span class="sxs-lookup"><span data-stu-id="b4f55-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="b4f55-132">嚴重性 -- 嚴重、重要或警告的 CCE 嚴重性值</span><span class="sxs-lookup"><span data-stu-id="b4f55-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="b4f55-133">CCIED -- 規則的 CCE 唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="b4f55-133">CCIED -- CCE unique identifier for the rule</span></span>
  - <span data-ttu-id="b4f55-134">說明 -- 規則的說明</span><span class="sxs-lookup"><span data-stu-id="b4f55-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="b4f55-135">弱點 -- 不套用規則的弱點或風險說明</span><span class="sxs-lookup"><span data-stu-id="b4f55-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="b4f55-136">影響 -- 套用規則時的業務影響</span><span class="sxs-lookup"><span data-stu-id="b4f55-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="b4f55-137">預期值 -- 資訊安全中心對照規則分析 VM OS 設定時的預期值</span><span class="sxs-lookup"><span data-stu-id="b4f55-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="b4f55-138">規則作業 -- 資訊安全中心對照規則分析 VM OS 設定時使用的規則作業</span><span class="sxs-lookup"><span data-stu-id="b4f55-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="b4f55-139">實際值 -- 對照規則分析 VM OS 設定時的傳回值</span><span class="sxs-lookup"><span data-stu-id="b4f55-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="b4f55-140">評估結果 -- 分析的結果︰通過、失敗</span><span class="sxs-lookup"><span data-stu-id="b4f55-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="b4f55-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b4f55-141">See also</span></span>
<span data-ttu-id="b4f55-142">本文說明了如何實作資訊安全中心建議的「修復 OS 弱點」。</span><span class="sxs-lookup"><span data-stu-id="b4f55-142">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="b4f55-143">您可在[這裡](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)檢閱設定規則集。</span><span class="sxs-lookup"><span data-stu-id="b4f55-143">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="b4f55-144">資訊安全中心會使用 CCE (一般設定列舉) 指派設定規則的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="b4f55-144">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="b4f55-145">如需詳細資訊，請造訪 [CCE](https://nvd.nist.gov/cce/index.cfm) 網站。</span><span class="sxs-lookup"><span data-stu-id="b4f55-145">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="b4f55-146">若要深入了解資訊安全中心，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="b4f55-146">To learn more about Security Center, see the following resources:</span></span>

* <span data-ttu-id="b4f55-147">[Azure 資訊安全中心支援的平台](security-center-os-coverage.md) - 提供支援的 Windows 與 Linux VM 清單。</span><span class="sxs-lookup"><span data-stu-id="b4f55-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="b4f55-148">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) - 了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="b4f55-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b4f55-149">[在 Azure 資訊安全中心管理安全性建議](security-center-recommendations.md) - 了解建議如何協助您保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b4f55-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b4f55-150">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) - 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="b4f55-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="b4f55-151">[在 Azure 資訊安全中心管理與回應安全性警示](security-center-managing-and-responding-alerts.md) - 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="b4f55-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="b4f55-152">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) - 了解如何監視合作夥伴解決方案的健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="b4f55-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="b4f55-153">[Azure 資訊安全中心常見問題集](security-center-faq.md) - 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="b4f55-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="b4f55-154">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) - 尋找有關 Azure 安全性與合規性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="b4f55-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
