---
title: "使用 Azure 資訊安全中心回應安全性事件 | Microsoft Docs"
description: "本文件說明如何使用 Azure 資訊安全中心執行事件回應案例。"
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 6cd6c822eb255893feac2536d7bae034380094b2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a><span data-ttu-id="77cc8-103">使用 Azure 資訊安全中心進行事件回應</span><span class="sxs-lookup"><span data-stu-id="77cc8-103">Using Azure Security Center for an incident response</span></span>
<span data-ttu-id="77cc8-104">許多組織都了解如何只在遭受攻擊之後回應安全性事件。</span><span class="sxs-lookup"><span data-stu-id="77cc8-104">Many organizations learn how to respond to security incidents only after suffering an attack.</span></span> <span data-ttu-id="77cc8-105">為了降低成本和損害，一定要在攻擊發生前備妥事件回應計劃。</span><span class="sxs-lookup"><span data-stu-id="77cc8-105">To reduce costs and damage, it’s important to have an incident response plan in place before an attack takes place.</span></span> <span data-ttu-id="77cc8-106">您可以在不同階段的事件回應使用 Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="77cc8-106">You can use Azure Security Center in different stages of an incident response.</span></span>

## <a name="incident-response-planning"></a><span data-ttu-id="77cc8-107">事件回應計劃</span><span class="sxs-lookup"><span data-stu-id="77cc8-107">Incident response planning</span></span>
<span data-ttu-id="77cc8-108">有效的計劃取決於三項核心功能：有能力保護、偵測及回應威脅。</span><span class="sxs-lookup"><span data-stu-id="77cc8-108">An effective plan depends on three core capabilities: being able to protect, detect, and respond to threats.</span></span> <span data-ttu-id="77cc8-109">保護是有關防止事件、偵測是有關及早識別威脅，而回應是有關遏止攻擊者及還原系統以緩和缺口的影響。</span><span class="sxs-lookup"><span data-stu-id="77cc8-109">Protection is about preventing incidents, detection is about identifying threats early, and response is about evicting the attacker and restoring systems to mitigate the impacts of a breach.</span></span>

<span data-ttu-id="77cc8-110">本文將使用[雲端中的 Microsoft Azure 安全性回應](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678)一文中的安全性事件回應階段，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="77cc8-110">This article will use the security incident response stages from the [Microsoft Azure Security Response in the Cloud](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) article, as shown in the following diagram:</span></span>

![事件回應生命週期](./media/security-center-incident-response/security-center-incident-response-fig1.png)

<span data-ttu-id="77cc8-112">您可在偵測、評估和診斷階段使用資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="77cc8-112">You can use Security Center during the Detect, Assess, and Diagnose stages.</span></span> <span data-ttu-id="77cc8-113">以下是如何在三個初始事件回應階段中，善用資訊安全中心的範例︰</span><span class="sxs-lookup"><span data-stu-id="77cc8-113">Here are examples of how Security Center can be useful during the three initial incident response stages:</span></span>

* <span data-ttu-id="77cc8-114">**偵測**︰檢閱事件調查的首次指示。</span><span class="sxs-lookup"><span data-stu-id="77cc8-114">**Detect**: review the first indication of an event investigation.</span></span>
  * <span data-ttu-id="77cc8-115">範例：檢閱在 [資訊安全中心] 儀表板中，引發高優先順序安全性警示的初始驗證。</span><span class="sxs-lookup"><span data-stu-id="77cc8-115">Example: review the initial verification that a high-priority security alert was raised in the Security Center dashboard.</span></span>
* <span data-ttu-id="77cc8-116">**評估**︰執行初始評估，以取得可疑活動的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="77cc8-116">**Assess**: perform the initial assessment to obtain more information about the suspicious activity.</span></span>
  * <span data-ttu-id="77cc8-117">範例︰取得有關安全性警示的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="77cc8-117">Example: obtain more information about the security alert.</span></span>
* <span data-ttu-id="77cc8-118">**診斷**︰進行技術性調查，並找出圍堵、緩和及因應策略。</span><span class="sxs-lookup"><span data-stu-id="77cc8-118">**Diagnose**: conduct a technical investigation and identify containment, mitigation, and workaround strategies.</span></span>
  * <span data-ttu-id="77cc8-119">範例︰遵循資訊安全中心在該特定安全性警示中所描述的補救步驟。</span><span class="sxs-lookup"><span data-stu-id="77cc8-119">Example: follow the remediation steps described by Security Center in that particular security alert.</span></span>

<span data-ttu-id="77cc8-120">接下來的案例示範如何在安全性事件的偵測、評估和回應階段善用資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="77cc8-120">The scenario that follows shows you how to leverage Security Center during the Detect, Assess, and Diagnose/Respond stages of a security incident.</span></span> <span data-ttu-id="77cc8-121">在資訊安全中心內，[安全性事件](security-center-incident.md)是符合[攻擊鏈](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/)模式之資源的所有警示彙總。</span><span class="sxs-lookup"><span data-stu-id="77cc8-121">In Security Center, a [security incident](security-center-incident.md) is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="77cc8-122">事件會出現在 [[安全性警示](security-center-managing-and-responding-alerts.md)] 圖格和刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="77cc8-122">Incidents appear in the [Security alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="77cc8-123">事件會顯示相關警示的清單，以讓您取得所引發的每個警示的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="77cc8-123">An incident reveals the list of related alerts, which enables you to obtain more information about each occurrence.</span></span> <span data-ttu-id="77cc8-124">資訊安全中心也會呈現獨立安全性警示，這類警示也可用來追蹤可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="77cc8-124">Security Center also presents standalone security alerts that can also be used to track down a suspicious activity.</span></span>

## <a name="scenario"></a><span data-ttu-id="77cc8-125">案例</span><span class="sxs-lookup"><span data-stu-id="77cc8-125">Scenario</span></span>
<span data-ttu-id="77cc8-126">Contoso 最近將一些內部部署資源移轉至 Azure，包括一些以虛擬機器為基礎的商務營運工作負載和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="77cc8-126">Contoso recently migrated some of their on-premises resources to Azure, including some virtual machine-based line-of-business workloads and SQL databases.</span></span> <span data-ttu-id="77cc8-127">Contoso 的核心電腦安全性事件回應小組 (CSIRT) 目前因為尚未整合與其目前事件回應工具的安全性情報，而無法順利調查安全性問題。</span><span class="sxs-lookup"><span data-stu-id="77cc8-127">Currently, Contoso's Core Computer Security Incident Response Team (CSIRT) has a problem investigating security issues because of security intelligence not being integrated with their current incident response tools.</span></span> <span data-ttu-id="77cc8-128">缺乏此種整合會在偵測階段帶來問題 (太多誤判)，也會在評估和診斷階段造成問題。</span><span class="sxs-lookup"><span data-stu-id="77cc8-128">This lack of integration introduces a problem during the Detect stage (too many false positives), as well as during the Assess and Diagnose stages.</span></span> <span data-ttu-id="77cc8-129">在此移轉過程中，他們決定選擇加入資訊安全中心，以協助他們解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="77cc8-129">As part of this migration, they decided to opt in for Security Center to help them address this problem.</span></span>

<span data-ttu-id="77cc8-130">此移轉的第一個階段會在所有資源上架並解決資訊安全中心的所有安全性建議後完成。</span><span class="sxs-lookup"><span data-stu-id="77cc8-130">The first phase of this migration finished after they onboarded all resources and addressed all of the security recommendations from Security Center.</span></span> <span data-ttu-id="77cc8-131">Contoso CSIRT 是處理電腦安全性事件的焦點。</span><span class="sxs-lookup"><span data-stu-id="77cc8-131">Contoso CSIRT is the focal point for dealing with computer security incidents.</span></span> <span data-ttu-id="77cc8-132">該小組是由一群負責處理任何安全性事件的人員所組成。</span><span class="sxs-lookup"><span data-stu-id="77cc8-132">The team consists of a group of people with responsibilities for dealing with any security incident.</span></span> <span data-ttu-id="77cc8-133">小組成員已清楚定義職責，以確保涵蓋所有的回應區域。</span><span class="sxs-lookup"><span data-stu-id="77cc8-133">The team members have clearly defined duties to ensure that no area of response is left uncovered.</span></span>

<span data-ttu-id="77cc8-134">基於此案例的目的，我們會將重點放在屬於 Contoso CSIRT 的下列人物的角色︰</span><span class="sxs-lookup"><span data-stu-id="77cc8-134">For the purpose of this scenario, we're going to focus on the roles of the following personas that are part of Contoso CSIRT:</span></span>

![事件回應生命週期](./media/security-center-incident-response/security-center-incident-response-fig2.png)

<span data-ttu-id="77cc8-136">Judy 負責安全性作業。</span><span class="sxs-lookup"><span data-stu-id="77cc8-136">Judy is in security operations.</span></span> <span data-ttu-id="77cc8-137">她的職責包括︰</span><span class="sxs-lookup"><span data-stu-id="77cc8-137">Her responsibilities include:</span></span>

* <span data-ttu-id="77cc8-138">隨時監視及回應安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="77cc8-138">Monitoring and responding to security threats around the clock.</span></span>
* <span data-ttu-id="77cc8-139">視需要提升至雲端工作負載擁有者或安全性分析師。</span><span class="sxs-lookup"><span data-stu-id="77cc8-139">Escalating to the cloud workload owner or security analyst as needed.</span></span>

<span data-ttu-id="77cc8-140">Sam 是安全性分析師，他的職責包括︰</span><span class="sxs-lookup"><span data-stu-id="77cc8-140">Sam is a security analyst and his responsibilities include:</span></span>

* <span data-ttu-id="77cc8-141">調查攻擊。</span><span class="sxs-lookup"><span data-stu-id="77cc8-141">Investigating attacks.</span></span>
* <span data-ttu-id="77cc8-142">修復警示。</span><span class="sxs-lookup"><span data-stu-id="77cc8-142">Remediating alerts.</span></span>
* <span data-ttu-id="77cc8-143">與工作負載擁有者一起來判斷和套用緩和措施。</span><span class="sxs-lookup"><span data-stu-id="77cc8-143">Working with workload owners to determine and apply mitigations.</span></span>

<span data-ttu-id="77cc8-144">如您所見，Judy 和 Sam 的責任不同，而他們必須共同合作以分享資訊安全中心的資訊。</span><span class="sxs-lookup"><span data-stu-id="77cc8-144">As you can see, Judy and Sam have different responsibilities, and they must work together to share Security Center information.</span></span>

## <a name="recommended-solution"></a><span data-ttu-id="77cc8-145">建議的解決方案</span><span class="sxs-lookup"><span data-stu-id="77cc8-145">Recommended solution</span></span>
<span data-ttu-id="77cc8-146">由於 Judy 和 Sam 有不同的角色，他們將會使用資訊安全中心的不同區域來取得日常活動的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="77cc8-146">Since Judy and Sam have different roles, they'll be using different areas of Security Center to obtain relevant information for their daily activities.</span></span> <span data-ttu-id="77cc8-147">Judy 會在其日常監視中使用 [安全性警示]。</span><span class="sxs-lookup"><span data-stu-id="77cc8-147">Judy will use **Security alerts** as part of her daily monitoring.</span></span>

![安全性警示](./media/security-center-incident-response/security-center-incident-response-fig3.png)

<span data-ttu-id="77cc8-149">Judy 會在偵測和評估階段使用 [安全性警示]。</span><span class="sxs-lookup"><span data-stu-id="77cc8-149">Judy will use Security alerts during the Detect and Assess stages.</span></span> <span data-ttu-id="77cc8-150">Judy 完成初步評估後，如果需要進一步調查，她可能會向 Sam 呈報問題。</span><span class="sxs-lookup"><span data-stu-id="77cc8-150">After Judy finishes the initial assessment, she might escalate the issue to Sam if additional investigation is required.</span></span> <span data-ttu-id="77cc8-151">此時 Sam 會使用資訊安全中心所提供的資訊，有時搭配其他資料來源，以移至診斷階段。</span><span class="sxs-lookup"><span data-stu-id="77cc8-151">At this point, Sam will use the information that was provided by Security Center, sometimes in conjunction with other data sources, to move to the Diagnose stage.</span></span>

## <a name="how-to-implement-this-solution"></a><span data-ttu-id="77cc8-152">如何實作此解決方案</span><span class="sxs-lookup"><span data-stu-id="77cc8-152">How to implement this solution</span></span>
<span data-ttu-id="77cc8-153">為了查看您如何在事件回應案例中使用 Azure 資訊安全中心，我們將遵循 Judy 在偵測和評估階段中的步驟，並查看 Sam 如何診斷問題。</span><span class="sxs-lookup"><span data-stu-id="77cc8-153">To see how you would use Azure Security Center in an incident response scenario, we’ll follow Judy’s steps in the Detect and Assess stages, and then see what Sam does to diagnose the issue.</span></span>

### <a name="detect-and-assess-incident-response-stages"></a><span data-ttu-id="77cc8-154">偵測和評估事件回應階段</span><span class="sxs-lookup"><span data-stu-id="77cc8-154">Detect and Assess incident response stages</span></span>
<span data-ttu-id="77cc8-155">Judy 登入了 Azure 入口網站，並在資訊安全中心主控台進行工作。</span><span class="sxs-lookup"><span data-stu-id="77cc8-155">Judy signed in to the Azure portal and is working in the Security Center console.</span></span> <span data-ttu-id="77cc8-156">在她的日常監視活動中，她會執行下列步驟，以便開始檢閱高優先順序的安全性警示︰</span><span class="sxs-lookup"><span data-stu-id="77cc8-156">As part of her daily monitoring activities, she started reviewing high-priority security alerts by performing the following steps:</span></span>

1. <span data-ttu-id="77cc8-157">按一下 [安全性警示] 圖格，然後存取 [安全性警示] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="77cc8-157">Click the **Security alerts** tile and access the **Security alerts** blade.</span></span>
    <span data-ttu-id="77cc8-158">![安全性警示刀鋒視窗](./media/security-center-incident-response/security-center-incident-response-fig4.png)</span><span class="sxs-lookup"><span data-stu-id="77cc8-158">![Security alert blade](./media/security-center-incident-response/security-center-incident-response-fig4.png)</span></span>

   > [!NOTE]
   > <span data-ttu-id="77cc8-159">基於此案例的目的，Judy 即將對 [惡意 SQL 活動] 警示執行評估，如上圖所示。</span><span class="sxs-lookup"><span data-stu-id="77cc8-159">For the purpose of this scenario, Judy is going to perform an assessment on the Malicious SQL activity alert, as seen in the preceding figure.</span></span>
   >
   >
2. <span data-ttu-id="77cc8-160">按一下**惡意 SQL 活動**警示，然後檢閱中的受攻擊的資源**惡意 SQL 活動**刀鋒視窗：![事件詳細資料](./media/security-center-incident-response/security-center-incident-response-fig5.png)</span><span class="sxs-lookup"><span data-stu-id="77cc8-160">Click the **Malicious SQL activity** alert and review the attacked resources in the **Malicious SQL activity** blade:  ![Incident details](./media/security-center-incident-response/security-center-incident-response-fig5.png)</span></span>

    <span data-ttu-id="77cc8-161">在此刀鋒視窗中，Judy 可以做一些筆記：受攻擊資源的相關資訊、此攻擊的發生次數，以及其偵測時間。</span><span class="sxs-lookup"><span data-stu-id="77cc8-161">In this blade, Judy can take notes regarding the attacked resources, how many times this attack happened, and when it was detected.</span></span>
3. <span data-ttu-id="77cc8-162">按一下 [受到攻擊的資源]  以取得有關此攻擊的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="77cc8-162">Click the **attacked resource** to obtain more information about this attack.</span></span>

<span data-ttu-id="77cc8-163">讀取說明之後，Judy 確信這不是誤判，她就應該向 Sam 呈報此案例。</span><span class="sxs-lookup"><span data-stu-id="77cc8-163">After reading the description, Judy is convinced that this is not a false positive and that she should escalate this case to Sam.</span></span>

### <a name="diagnose-incident-response-stage"></a><span data-ttu-id="77cc8-164">診斷事件回應階段</span><span class="sxs-lookup"><span data-stu-id="77cc8-164">Diagnose incident response stage</span></span>
<span data-ttu-id="77cc8-165">Sam 會收到來自 Judy 的案例，開始檢閱資訊安全中心所建議的修復步驟。</span><span class="sxs-lookup"><span data-stu-id="77cc8-165">Sam receives the case from Judy and starts reviewing the remediation steps that Security Center suggested.</span></span>

![事件回應生命週期](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a><span data-ttu-id="77cc8-167">其他資源</span><span class="sxs-lookup"><span data-stu-id="77cc8-167">Additional resources</span></span>
<span data-ttu-id="77cc8-168">事件回應小組也可以利用 [[安全性中心 Power BI](security-center-powerbi.md)] 功能的優勢，查看不同類型的報告。</span><span class="sxs-lookup"><span data-stu-id="77cc8-168">The incident response team can also take advantage of the [Security Center Power BI](security-center-powerbi.md) capability to see different types of reports.</span></span> <span data-ttu-id="77cc8-169">這些報告可以在進一步調查時，幫助他們視覺化、分析和篩選建議和安全性警示。</span><span class="sxs-lookup"><span data-stu-id="77cc8-169">These reports can help them during further investigation to visualize, analyze, and filter recommendations and security alerts.</span></span> <span data-ttu-id="77cc8-170">對於在調查過程中使用其安全性資訊和事件管理 (SIEM) 解決方案的公司而言，他們也可以[整合資訊安全中心與其解決方案](security-center-integrating-alerts-with-log-integration.md)。</span><span class="sxs-lookup"><span data-stu-id="77cc8-170">For companies that use their security information and event management (SIEM) solution during the investigation process, they can also [integrate Security Center with their solution](security-center-integrating-alerts-with-log-integration.md).</span></span> <span data-ttu-id="77cc8-171">您也可以使用 [Azure 記錄整合工具](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/)來整合 Azure 稽核記錄檔和虛擬機器 (VM) 安全性事件。</span><span class="sxs-lookup"><span data-stu-id="77cc8-171">You can also integrate Azure audit logs and virtual machine (VM) security events by using the [Azure log integration tool](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/).</span></span> <span data-ttu-id="77cc8-172">若要調查攻擊，您可以搭配使用此資訊與資訊安全中心所提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="77cc8-172">To investigate an attack, you can use this information in conjunction with the information that Security Center provides.</span></span>

## <a name="conclusion"></a><span data-ttu-id="77cc8-173">結論</span><span class="sxs-lookup"><span data-stu-id="77cc8-173">Conclusion</span></span>
<span data-ttu-id="77cc8-174">事件發生前召集小組對組織而言非常重要，可正面影響事件的處理方式。</span><span class="sxs-lookup"><span data-stu-id="77cc8-174">Assembling a team before an incident occurs is very important to your organization and will positively influence how incidents are handled.</span></span> <span data-ttu-id="77cc8-175">擁有可監視資源的適當工具，有助於這個小組採取正確的步驟來修復安全性事件。</span><span class="sxs-lookup"><span data-stu-id="77cc8-175">Having the right tools to monitor resources can help this team to take accurate steps to remediate a security incident.</span></span> <span data-ttu-id="77cc8-176">資訊安全中心[偵測功能](security-center-detection-capabilities.md)會協助 IT 部門快速地回應安全性事件並修復安全性問題。</span><span class="sxs-lookup"><span data-stu-id="77cc8-176">Security Center [detection capabilities](security-center-detection-capabilities.md) can assist IT to quickly respond to security incidents and remediate security issues.</span></span>
