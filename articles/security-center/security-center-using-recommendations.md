---
title: "aaaUse Azure 資訊安全中心建議 tooenhance 安全性 |Microsoft 文件"
description: " 了解 toouse 安全性原則和建議 Azure 資訊安全中心 toohelp 降低安全性攻擊。 "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: bd314350a5abfceea3e171f2e1b55afe4549c1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-security-center-recommendations-tooenhance-security"></a><span data-ttu-id="5e80d-103">使用 Azure 資訊安全中心建議 tooenhance 安全性</span><span class="sxs-lookup"><span data-stu-id="5e80d-103">Use Azure Security Center recommendations tooenhance security</span></span>
<span data-ttu-id="5e80d-104">您可以設定安全性原則，然後實作 hello Azure 資訊安全中心所提供的建議，以減少 hello 機會的重大的安全性事件。</span><span class="sxs-lookup"><span data-stu-id="5e80d-104">You can reduce hello chances of a significant security event by configuring a security policy and then implementing hello recommendations provided by Azure Security Center.</span></span> <span data-ttu-id="5e80d-105">本文章將示範如何 toouse 安全性原則和建議的資訊安全中心 toohelp 降低安全性攻擊。</span><span class="sxs-lookup"><span data-stu-id="5e80d-105">This article shows you how toouse security policies and recommendations in Security Center toohelp mitigate a security attack.</span></span>

> [!NOTE]
> <span data-ttu-id="5e80d-106">這篇文章是根據 hello 角色和概念，hello 資訊安全中心[規劃及作業指南](security-center-planning-and-operations-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="5e80d-106">This article builds on hello roles and concepts introduced in hello Security Center [planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="5e80d-107">它是個不錯的主意 tooreview hello 規劃指南，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="5e80d-107">It’s a good idea tooreview hello planning guide before continuing.</span></span>
>
>

## <a name="managing-security-recommendations"></a><span data-ttu-id="5e80d-108">管理安全性建議</span><span class="sxs-lookup"><span data-stu-id="5e80d-108">Managing security recommendations</span></span>
<span data-ttu-id="5e80d-109">安全性原則定義 hello 組 hello 指定訂用帳戶或資源群組中資源的建議使用的控制項。</span><span class="sxs-lookup"><span data-stu-id="5e80d-109">A security policy defines hello set of controls that are recommended for resources within hello specified subscription or resource group.</span></span> <span data-ttu-id="5e80d-110">資訊安全中心，您可以定義原則根據 tooyour 公司的安全性需求。</span><span class="sxs-lookup"><span data-stu-id="5e80d-110">In Security Center, you define policies according tooyour company's security requirements.</span></span> <span data-ttu-id="5e80d-111">詳細資訊，請參閱 toolearn[設定安全性原則資訊安全中心](security-center-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="5e80d-111">toolearn more, see [Set security policies in Security Center](security-center-policies.md).</span></span>

<span data-ttu-id="5e80d-112">資源群組的安全性原則被繼承自 hello 訂用帳戶層級。</span><span class="sxs-lookup"><span data-stu-id="5e80d-112">Security policies for resource groups are inherited from hello subscription level.</span></span>

![安全性原則繼承][1]

<span data-ttu-id="5e80d-114">如果您需要特定的資源群組中的自訂原則，您可以停用 hello 資源群組中的繼承。</span><span class="sxs-lookup"><span data-stu-id="5e80d-114">If you need custom policies in specific resource groups, you can disable inheritance in hello resource group.</span></span> <span data-ttu-id="5e80d-115">toodisable，hello 安全性原則 刀鋒視窗上設定繼承 tooUnique 和自訂的資訊安全中心會顯示建議的 hello 控制項。</span><span class="sxs-lookup"><span data-stu-id="5e80d-115">toodisable, set Inheritance tooUnique on hello Security policy blade and customize hello controls that Security Center shows recommendations for.</span></span>

<span data-ttu-id="5e80d-116">比方說，如果您有不需要 hello SQL Database 的透明資料加密 (TDE) 原則的工作負載時，關閉 hello hello 訂用帳戶層級的原則，並只有在需要 SQL TDE 的地方 hello 資源群組中啟用它。</span><span class="sxs-lookup"><span data-stu-id="5e80d-116">For example, if you have workloads that do not require hello SQL Database Transparent Data Encryption (TDE) policy, turn off hello policy at hello subscription level and enable it only in hello resources groups where SQL TDE is required.</span></span>

> [!NOTE]
> <span data-ttu-id="5e80d-117">如果沒有訂用帳戶層級的原則與資源群組層級原則之間的衝突，會優先 hello 資源群組層級原則。</span><span class="sxs-lookup"><span data-stu-id="5e80d-117">If there is a conflict between subscription level policy and resource group level policy, hello resource group level policy takes precedence.</span></span>
>
>

<span data-ttu-id="5e80d-118">資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="5e80d-118">Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="5e80d-119">當資訊安全中心識別潛在的安全性漏洞時，它會建立 hello 安全性原則中設定的 hello 控制項為基礎的建議。</span><span class="sxs-lookup"><span data-stu-id="5e80d-119">When Security Center identifies potential security vulnerabilities, it creates recommendations based on hello controls set in hello security policy.</span></span> <span data-ttu-id="5e80d-120">hello 建議會引導您完成設定所需的 hello 安全性控制項的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="5e80d-120">hello recommendations guide you through hello process of configuring hello needed security controls.</span></span>

<span data-ttu-id="5e80d-121">資訊安全中心目前的原則建議著重於系統更新、作業系統設定、子網路和虛擬機器 (VM) 上的網路安全性群組、SQL Database 稽核、SQL Database TDE 和 Web 應用程式防火牆。</span><span class="sxs-lookup"><span data-stu-id="5e80d-121">Current policy recommendations in Security Center focus on system updates, OS configuration, network security groups on subnets and virtual machines (VMs), SQL Database Auditing, SQL Database TDE, and web application firewalls.</span></span> <span data-ttu-id="5e80d-122">Hello 最新的資訊安全中心建議涵蓋範圍，請參閱[管理資訊安全中心的安全性建議](security-center-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="5e80d-122">For hello most up-to-date coverage of Security Center recommendations, see [Managing security recommendations in Security Center](security-center-recommendations.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="5e80d-123">案例</span><span class="sxs-lookup"><span data-stu-id="5e80d-123">Scenario</span></span>
<span data-ttu-id="5e80d-124">這個案例顯示如何 toouse 資訊安全中心 toohelp 減少 hello 機會重大的安全性事件的監視資訊安全中心建議及採取動作。</span><span class="sxs-lookup"><span data-stu-id="5e80d-124">This scenario shows you how toouse Security Center toohelp reduce hello chances of a significant security incident by monitoring Security Center recommendations and taking action.</span></span> <span data-ttu-id="5e80d-125">hello 案例使用 hello 虛構公司 Contoso，而角色中呈現 hello 資訊安全中心[規劃及作業指南](security-center-planning-and-operations-guide.md#security-roles-and-access-controls)。</span><span class="sxs-lookup"><span data-stu-id="5e80d-125">hello scenario uses hello fictitious company, Contoso, and roles presented in hello Security Center [planning and operations guide](security-center-planning-and-operations-guide.md#security-roles-and-access-controls).</span></span> <span data-ttu-id="5e80d-126">hello 角色代表個人和小組可能會使用資訊安全中心 tooperform 不同安全性相關的工作。</span><span class="sxs-lookup"><span data-stu-id="5e80d-126">hello roles represent individuals and teams that may use Security Center tooperform different security-related tasks.</span></span> <span data-ttu-id="5e80d-127">hello 角色如下：</span><span class="sxs-lookup"><span data-stu-id="5e80d-127">hello roles are:</span></span>

![案例角色][2]

<span data-ttu-id="5e80d-129">Contoso 最近移轉其內部部署資源 tooAzure 部分。</span><span class="sxs-lookup"><span data-stu-id="5e80d-129">Contoso recently migrated some of their on-premises resources tooAzure.</span></span> <span data-ttu-id="5e80d-130">Contoso 想 tooimplement 和維護減少其資源 hello 雲端中的弱點可能會 tooa 安全性攻擊的保護。</span><span class="sxs-lookup"><span data-stu-id="5e80d-130">Contoso wants tooimplement and maintain protections that reduce their vulnerability tooa security attack of their resources in hello cloud.</span></span>

## <a name="recommended-solution"></a><span data-ttu-id="5e80d-131">建議的解決方案</span><span class="sxs-lookup"><span data-stu-id="5e80d-131">Recommended solution</span></span>
<span data-ttu-id="5e80d-132">方案是 toouse 資訊安全中心 tooprevent 和偵測安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="5e80d-132">A solution is toouse Security Center tooprevent and detect security vulnerabilities.</span></span> <span data-ttu-id="5e80d-133">Contoso 有存取 tooSecurity 中心透過其 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e80d-133">Contoso has access tooSecurity Center via their Azure subscription.</span></span> <span data-ttu-id="5e80d-134">hello[免費層](security-center-pricing.md)的資訊安全中心會自動啟用上所有的 Azure 訂用帳戶，且其訂用帳戶中所有 Vm 上啟用資料收集。</span><span class="sxs-lookup"><span data-stu-id="5e80d-134">hello [Free tier](security-center-pricing.md) of Security Center is automatically enabled on all Azure subscriptions and data collection is enabled on all VMs in their subscription.</span></span>

<span data-ttu-id="5e80d-135">任職於 Contoso IT 安全部門的 David 使用資訊安全中心設定**安全性原則**。</span><span class="sxs-lookup"><span data-stu-id="5e80d-135">David, in Contoso’s IT Security, configures a **security policy** using Security Center.</span></span> <span data-ttu-id="5e80d-136">資訊安全中心會分析 hello Contoso 的 Azure 資源安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="5e80d-136">Security Center analyzes hello security state of Contoso’s Azure resources.</span></span> <span data-ttu-id="5e80d-137">當資訊安全中心識別潛在的安全性漏洞時，它會建立**建議**hello 安全性原則中設定的 hello 控制項為基礎。</span><span class="sxs-lookup"><span data-stu-id="5e80d-137">When Security Center identifies potential security vulnerabilities, it creates **recommendations** based on hello controls set in hello security policy.</span></span>

<span data-ttu-id="5e80d-138">雲端工作負載擁有者 Jeff 負責根據 Contoso 的安全性原則，實作和維護防護措施。</span><span class="sxs-lookup"><span data-stu-id="5e80d-138">Jeff, a cloud workload owner, is responsible for implementing and maintaining protections in accordance with Contoso’s security policies.</span></span> <span data-ttu-id="5e80d-139">Jeff 可以監視由資訊安全中心 tooapply 保護 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="5e80d-139">Jeff can monitor hello recommendations created by Security Center tooapply protections.</span></span> <span data-ttu-id="5e80d-140">hello 建議引導 Jeff 完成 hello 程序設定所需的 hello 安全性控制項。</span><span class="sxs-lookup"><span data-stu-id="5e80d-140">hello recommendations guide Jeff through hello process of configuring hello needed security controls.</span></span>

<span data-ttu-id="5e80d-141">中的 Jeff tooimplement 順序和維護保護，避免安全性弱點，他必須：</span><span class="sxs-lookup"><span data-stu-id="5e80d-141">In order for Jeff tooimplement and maintain protections and eliminate security vulnerabilities, he needs to:</span></span>

- <span data-ttu-id="5e80d-142">監視資訊安全中心提供的安全性建議</span><span class="sxs-lookup"><span data-stu-id="5e80d-142">Monitor security recommendations provided by Security Center</span></span>
- <span data-ttu-id="5e80d-143">評估安全性建議，並決定是否應該套用或解除</span><span class="sxs-lookup"><span data-stu-id="5e80d-143">Evaluate security recommendations and decide if he should apply or dismiss</span></span>
- <span data-ttu-id="5e80d-144">套用安全性建議</span><span class="sxs-lookup"><span data-stu-id="5e80d-144">Apply security recommendations</span></span>

<span data-ttu-id="5e80d-145">讓我們遵循 Jeff 的步驟 toosee 他使用方式的資訊安全中心建議 tooguide 他透過設定控制項 tooeliminate 安全性弱點的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="5e80d-145">Let’s follow Jeff’s steps toosee how he uses Security Center recommendations tooguide him through hello process of configuring controls tooeliminate security vulnerabilities.</span></span>

## <a name="how-tooimplement-this-solution"></a><span data-ttu-id="5e80d-146">如何 tooimplement 此解決方案</span><span class="sxs-lookup"><span data-stu-id="5e80d-146">How tooimplement this solution</span></span>
<span data-ttu-id="5e80d-147">Jeff 登入太[Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)和開啟 hello 資訊安全中心主控台。</span><span class="sxs-lookup"><span data-stu-id="5e80d-147">Jeff signs in too[Azure portal](https://azure.microsoft.com/features/azure-portal/) and opens hello Security Center console.</span></span> <span data-ttu-id="5e80d-148">監視活動其每日的一部分，他會檢查 toosee 是否有安全性建議執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5e80d-148">As part of his daily monitoring activities, he checks toosee if there are security recommendations by performing hello following steps:</span></span>

1. <span data-ttu-id="5e80d-149">Jeff 選取 hello**建議**磚 tooopen hello**建議**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5e80d-149">Jeff selects hello **Recommendations** tile tooopen hello **Recommendations** blade.</span></span>
   <span data-ttu-id="5e80d-150">![選取 hello 建議磚][3]</span><span class="sxs-lookup"><span data-stu-id="5e80d-150">![Select hello recommendations tile][3]</span></span>
2. <span data-ttu-id="5e80d-151">Jeff 檢閱 hello 建議事項的清單。</span><span class="sxs-lookup"><span data-stu-id="5e80d-151">Jeff reviews hello list of recommendations.</span></span> <span data-ttu-id="5e80d-152">他會看到資訊安全中心提供建議的優先順序，從最高優先權 toolowest 優先權 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="5e80d-152">He sees that Security Center has provided hello list of recommendations in priority order, from highest priority toolowest priority.</span></span> <span data-ttu-id="5e80d-153">他決定 tooaddress hello 清單上的優先建議。</span><span class="sxs-lookup"><span data-stu-id="5e80d-153">He decides tooaddress a High priority recommendation on hello list.</span></span> <span data-ttu-id="5e80d-154">他選取**安裝 Endpoint Protection**上 hello**建議**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5e80d-154">He selects **Install Endpoint Protection** on hello **Recommendations** blade.</span></span>
3. <span data-ttu-id="5e80d-155">hello**安裝 Endpoint Protection**刀鋒視窗會開啟不啟用的反惡意程式碼的情況下顯示的 Vm 清單。</span><span class="sxs-lookup"><span data-stu-id="5e80d-155">hello **Install Endpoint Protection** blade opens displaying a list of VMs without antimalware enabled.</span></span> <span data-ttu-id="5e80d-156">Jeff 檢閱 hello 的 Vm 清單中，選取所有的 Vm，然後選取**3 個 Vm 上安裝**。</span><span class="sxs-lookup"><span data-stu-id="5e80d-156">Jeff reviews hello list of VMs, selects all VMs, and then selects **Install on 3 VMs**.</span></span>
   <span data-ttu-id="5e80d-157">![安裝端點保護][4]</span><span class="sxs-lookup"><span data-stu-id="5e80d-157">![Install endpoint protection][4]</span></span>
4. <span data-ttu-id="5e80d-158">hello**選取 Endpoint Protection**刀鋒視窗中開啟提供 Jeff 與兩個反惡意程式碼解決方案。</span><span class="sxs-lookup"><span data-stu-id="5e80d-158">hello **Select Endpoint Protection** blade opens providing Jeff with two antimalware solutions.</span></span> <span data-ttu-id="5e80d-159">Jeff 選取 hello **Microsoft 反惡意程式碼**方案。</span><span class="sxs-lookup"><span data-stu-id="5e80d-159">Jeff selects hello **Microsoft Antimalware** solution.</span></span>
5. <span data-ttu-id="5e80d-160">會顯示 hello 反惡意程式碼解決方案的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="5e80d-160">Additional information about hello antimalware solution is displayed.</span></span> <span data-ttu-id="5e80d-161">Jeff 選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5e80d-161">Jeff selects **Create**.</span></span>
   <span data-ttu-id="5e80d-162">![Microsoft antimalware][5]</span><span class="sxs-lookup"><span data-stu-id="5e80d-162">![Microsoft antimalware][5]</span></span>
6. <span data-ttu-id="5e80d-163">Jeff 在 hello 輸入 hello 所需的組態設定**安裝**刀鋒視窗，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="5e80d-163">Jeff enters hello required configuration settings on hello **Install** blade and selects **OK**.</span></span>

<span data-ttu-id="5e80d-164">[Microsoft 反惡意程式碼](../security/azure-security-antimalware.md)現在 hello 上的作用中選取 Vm。</span><span class="sxs-lookup"><span data-stu-id="5e80d-164">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

<span data-ttu-id="5e80d-165">Jeff 會繼續透過 hello 高優先順序和優先順序建議 toomove 決策實作。</span><span class="sxs-lookup"><span data-stu-id="5e80d-165">Jeff continues toomove through hello high priority and medium priority recommendations, making decisions on implementation.</span></span> <span data-ttu-id="5e80d-166">Jeff 參考 hello[管理安全性建議](security-center-recommendations.md)toounderstand hello 建議，和每一項功能如果他適用於文件。</span><span class="sxs-lookup"><span data-stu-id="5e80d-166">Jeff references hello [Managing security recommendations](security-center-recommendations.md) article toounderstand hello recommendations and what each one does if he applies it.</span></span>

<span data-ttu-id="5e80d-167">Jeff 學習， [Microsoft Security Response Center (MSRC)](../security/azure-security-response-center.md)執行選取的安全性監視的 hello Azure 網路和基礎結構，並從第三方接收威脅情報和濫用抱怨。</span><span class="sxs-lookup"><span data-stu-id="5e80d-167">Jeff learns that [Microsoft Security Response Center (MSRC)](../security/azure-security-response-center.md) performs select security monitoring of hello Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span> <span data-ttu-id="5e80d-168">如果 Jeff Contoso 的 Azure 訂用帳戶提供安全性連絡人詳細資料，Microsoft 連絡人 Contoso 如果 hello MSRC 會探索該 Contoso 的客戶資料已存取非法或未經授權的合作對象。</span><span class="sxs-lookup"><span data-stu-id="5e80d-168">If Jeff provides security contact details for Contoso’s Azure subscription, Microsoft contacts Contoso if hello MSRC discovers that Contoso’s customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="5e80d-169">讓我們依照 Jeff 他適用於 hello**提供安全性連絡人詳細資料**建議 （嚴重性的建議中 hello 上述建議清單中）。</span><span class="sxs-lookup"><span data-stu-id="5e80d-169">Let’s follow Jeff as he applies hello **Provide security contact details** recommendation (a recommendation with severity of Medium in hello list of recommendations above).</span></span>

1. <span data-ttu-id="5e80d-170">Jeff 選取**提供安全性連絡人詳細資料**上 hello**建議**刀鋒視窗中，這會開啟 hello**提供安全性連絡人詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5e80d-170">Jeff selects **Provide security contact details** on hello **Recommendations** blade, which opens hello **Provide security contact details** blade.</span></span>
2. <span data-ttu-id="5e80d-171">Jeff 在 選取 hello Azure 訂用帳戶 tooprovide 連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="5e80d-171">Jeff selects hello Azure subscription tooprovide contact information on.</span></span> <span data-ttu-id="5e80d-172">第二個 [提供安全性連絡人詳細資料]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="5e80d-172">A second **Provide security contact details** blade opens.</span></span>
   <span data-ttu-id="5e80d-173">![安全性連絡人詳細資料][6]</span><span class="sxs-lookup"><span data-stu-id="5e80d-173">![Security contact details][6]</span></span>
3. <span data-ttu-id="5e80d-174">在 hello 第二個**提供安全性連絡人詳細資料**刀鋒視窗中，Jeff 輸入：</span><span class="sxs-lookup"><span data-stu-id="5e80d-174">On hello second **Provide security contact details** blade, Jeff enters:</span></span>

  - <span data-ttu-id="5e80d-175">（沒有他可以輸入的電子郵件地址限制 toohello 數目） 的逗號分隔的 hello 安全性連絡人的電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="5e80d-175">hello security contact email addresses separated by commas (there is not a limit toohello number of email addresses that he can enter)</span></span>
  - <span data-ttu-id="5e80d-176">一個安全性連絡人電話號碼</span><span class="sxs-lookup"><span data-stu-id="5e80d-176">one security contact phone number</span></span>

4. <span data-ttu-id="5e80d-177">Jeff 也會開啟 hello 選項**傳送給我以電子郵件警示的相關**tooreceive 有關高嚴重性警示的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="5e80d-177">Jeff also turns on hello option **Send me emails about alerts** tooreceive emails about high severity alerts.</span></span>
5. <span data-ttu-id="5e80d-178">Jeff 選取**確定**tooapply hello 安全性連絡資訊 tooContoso 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e80d-178">Jeff selects **OK** tooapply hello security contact information tooContoso’s subscription.</span></span>

<span data-ttu-id="5e80d-179">最後，Jeff 檢閱 hello 低優先順序建議**修復作業系統的弱點可能會**並決定不適用這項建議。</span><span class="sxs-lookup"><span data-stu-id="5e80d-179">Finally, Jeff reviews hello low priority recommendation **Remediate OS vulnerabilities** and determines that this recommendation is not applicable.</span></span> <span data-ttu-id="5e80d-180">他想 toodismiss hello 建議。</span><span class="sxs-lookup"><span data-stu-id="5e80d-180">He wants toodismiss hello recommendation.</span></span> <span data-ttu-id="5e80d-181">Jeff 選取 hello 三個點顯示 toohello 權限，然後選取**解除**。</span><span class="sxs-lookup"><span data-stu-id="5e80d-181">Jeff selects hello three dots that appear toohello right, and then selects **Dismiss**.</span></span>
   <span data-ttu-id="5e80d-182">![解除建議][7]</span><span class="sxs-lookup"><span data-stu-id="5e80d-182">![Dismiss recommendation][7]</span></span>

## <a name="conclusion"></a><span data-ttu-id="5e80d-183">結論</span><span class="sxs-lookup"><span data-stu-id="5e80d-183">Conclusion</span></span>
<span data-ttu-id="5e80d-184">監控資訊安全中心的建議可能有助於在發生攻擊之前消除安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="5e80d-184">Monitoring recommendations in Security Center may help you eliminate security vulnerabilities before an attack occurs.</span></span> <span data-ttu-id="5e80d-185">您可以使用資訊安全中心的安全性原則來實作和維護防護措施，以防止安全性事件。</span><span class="sxs-lookup"><span data-stu-id="5e80d-185">You can prevent a security incident by implementing and maintaining protections with security policies in Security Center.</span></span>

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
