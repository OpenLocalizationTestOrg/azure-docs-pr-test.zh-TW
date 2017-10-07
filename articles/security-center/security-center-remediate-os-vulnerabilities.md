---
title: "Azure 資訊安全中心中的 aaaRemediate 作業系統弱點 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 修復作業系統弱點 * *。"
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
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="98023-103">修復 Azure 資訊安全中心的 OS 弱點</span><span class="sxs-lookup"><span data-stu-id="98023-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="98023-104">Azure 資訊安全中心會分析每日虛擬機器 (VM) 作業系統 (OS) 的組態可以讓 hello VM 更容易遭受 tooattack 和建議的組態變更 tooaddress 這些弱點。</span><span class="sxs-lookup"><span data-stu-id="98023-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make hello VM more vulnerable tooattack and recommends configuration changes tooaddress these vulnerabilities.</span></span> <span data-ttu-id="98023-105">資訊安全中心建議 VM 的作業系統組態與 hello 建議組態規則不相符時，解決弱點。</span><span class="sxs-lookup"><span data-stu-id="98023-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match hello recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="98023-106">如需有關 hello 受監視的特定組態的詳細資訊，請參閱 hello[建議的組態設定的規則清單](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)。</span><span class="sxs-lookup"><span data-stu-id="98023-106">For more information on hello specific configurations being monitored, see hello [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="98023-107">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="98023-107">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="98023-108">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="98023-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="98023-109">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="98023-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="98023-110">在 hello**建議**刀鋒視窗中，選取**修復作業系統弱點**。</span><span class="sxs-lookup"><span data-stu-id="98023-110">In hello **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="98023-111">![修復 OS 弱點][1]</span><span class="sxs-lookup"><span data-stu-id="98023-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="98023-112">hello**修復作業系統弱點**刀鋒視窗會開啟，並列出其不符合建議的設定規則的 hello 的 OS 設定 Vm。</span><span class="sxs-lookup"><span data-stu-id="98023-112">hello **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match hello recommended configuration rules.</span></span>  <span data-ttu-id="98023-113">針對每個 VM，hello 刀鋒視窗中識別：</span><span class="sxs-lookup"><span data-stu-id="98023-113">For each VM, hello blade identifies:</span></span>

   * <span data-ttu-id="98023-114">**失敗的規則**-hello hello VM 的 OS 設定的規則數目失敗。</span><span class="sxs-lookup"><span data-stu-id="98023-114">**FAILED RULES** -- hello number of rules that hello VM's OS configuration failed.</span></span>
   * <span data-ttu-id="98023-115">**上次掃描時間**--hello 日期和時間資訊安全中心上次掃描 hello VM 的 OS 設定。</span><span class="sxs-lookup"><span data-stu-id="98023-115">**LAST SCAN TIME** -- hello date and time that Security Center last scanned hello VM’s OS configuration.</span></span>
   * <span data-ttu-id="98023-116">**狀態**-hello hello 弱點的目前狀態：</span><span class="sxs-lookup"><span data-stu-id="98023-116">**STATE** -- hello current state of hello vulnerability:</span></span>

     * <span data-ttu-id="98023-117">開啟： hello 的弱點可能會有尚未找出尚未</span><span class="sxs-lookup"><span data-stu-id="98023-117">Open: hello vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="98023-118">在進度： Hello 的弱點可能會目前套用，您不需要任何動作</span><span class="sxs-lookup"><span data-stu-id="98023-118">In Progress: hello vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="98023-119">判斷是否已解決： hello 的弱點可能會已解決 （當 hello 問題已解決，hello 項目會呈現灰色）</span><span class="sxs-lookup"><span data-stu-id="98023-119">Resolved: hello vulnerability was already addressed (when hello issue has been resolved, hello entry is grayed out)</span></span>
   * <span data-ttu-id="98023-120">**嚴重性**-所有的弱點可能會設定 tooa 嚴重性低，表示應該處理弱點，但不需要立即注意。</span><span class="sxs-lookup"><span data-stu-id="98023-120">**SEVERITY** -- All vulnerabilities are set tooa severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="98023-121">選取 VM。</span><span class="sxs-lookup"><span data-stu-id="98023-121">Select a VM.</span></span> <span data-ttu-id="98023-122">刀鋒視窗中的，VM 會開啟，並顯示 hello 規則失敗。</span><span class="sxs-lookup"><span data-stu-id="98023-122">A blade for that VM opens and displays hello rules that have failed.</span></span>
   <span data-ttu-id="98023-123">![失敗的設定規則][2]</span><span class="sxs-lookup"><span data-stu-id="98023-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="98023-124">選取規則。</span><span class="sxs-lookup"><span data-stu-id="98023-124">Select a rule.</span></span> <span data-ttu-id="98023-125">在此範例中，我們選取 [密碼必須符合複雜性需求] 。</span><span class="sxs-lookup"><span data-stu-id="98023-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="98023-126">刀鋒視窗會開啟描述 hello 失敗規則和 hello 的影響。</span><span class="sxs-lookup"><span data-stu-id="98023-126">A blade opens describing hello failed rule and hello impact.</span></span> <span data-ttu-id="98023-127">檢閱 hello 詳細資料，並考慮如何套用作業系統設定。</span><span class="sxs-lookup"><span data-stu-id="98023-127">Review hello details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="98023-128">![Hello 失敗規則描述][3]</span><span class="sxs-lookup"><span data-stu-id="98023-128">![Description for hello failed rule][3]</span></span>

  <span data-ttu-id="98023-129">資訊安全中心 configuration 規則使用通用組態列舉 (CCE) tooassign 唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="98023-129">Security Center uses Common Configuration Enumeration (CCE) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="98023-130">在這個刀鋒視窗上提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="98023-130">hello following information is provided on this blade:</span></span>

  - <span data-ttu-id="98023-131">名稱 -- 規則的名稱</span><span class="sxs-lookup"><span data-stu-id="98023-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="98023-132">嚴重性 -- 嚴重、重要或警告的 CCE 嚴重性值</span><span class="sxs-lookup"><span data-stu-id="98023-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="98023-133">Hello 規則的 CCIED-CCE 唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="98023-133">CCIED -- CCE unique identifier for hello rule</span></span>
  - <span data-ttu-id="98023-134">說明 -- 規則的說明</span><span class="sxs-lookup"><span data-stu-id="98023-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="98023-135">弱點 -- 不套用規則的弱點或風險說明</span><span class="sxs-lookup"><span data-stu-id="98023-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="98023-136">影響 -- 套用規則時的業務影響</span><span class="sxs-lookup"><span data-stu-id="98023-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="98023-137">預期值 — 值預期會在資訊安全中心會分析您的 VM OS 組態，根據 hello 規則</span><span class="sxs-lookup"><span data-stu-id="98023-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="98023-138">資訊安全中心所使用的 hello 規則對您 VM OS 的組態分析期間規則作業-規則作業</span><span class="sxs-lookup"><span data-stu-id="98023-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="98023-139">VM OS 設定針對 hello 規則的分析後傳回的實際值--值</span><span class="sxs-lookup"><span data-stu-id="98023-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="98023-140">評估結果 -- 分析的結果︰通過、失敗</span><span class="sxs-lookup"><span data-stu-id="98023-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="98023-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="98023-141">See also</span></span>
<span data-ttu-id="98023-142">本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議"補救作業系統弱點。 」</span><span class="sxs-lookup"><span data-stu-id="98023-142">This article showed you how tooimplement hello Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="98023-143">您可以檢閱 hello 組組態規則[這裡](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)。</span><span class="sxs-lookup"><span data-stu-id="98023-143">You can review hello set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="98023-144">資訊安全中心會使用組態規則 CCE （通用組態列舉） tooassign 唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="98023-144">Security Center uses CCE (Common Configuration Enumeration) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="98023-145">請瀏覽 hello [CCE](https://nvd.nist.gov/cce/index.cfm)如需詳細資訊的站台。</span><span class="sxs-lookup"><span data-stu-id="98023-145">Visit hello [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="98023-146">toolearn 有關資訊安全中心的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="98023-146">toolearn more about Security Center, see hello following resources:</span></span>

* <span data-ttu-id="98023-147">[Azure 資訊安全中心支援的平台](security-center-os-coverage.md) - 提供支援的 Windows 與 Linux VM 清單。</span><span class="sxs-lookup"><span data-stu-id="98023-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="98023-148">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="98023-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="98023-149">[在 Azure 資訊安全中心管理安全性建議](security-center-recommendations.md) - 了解建議如何協助您保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="98023-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="98023-150">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="98023-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="98023-151">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="98023-151">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="98023-152">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="98023-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="98023-153">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="98023-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="98023-154">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) - 尋找有關 Azure 安全性與合規性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="98023-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
