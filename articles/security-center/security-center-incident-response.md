---
title: "與 Azure 資訊安全中心 aaaRespond toosecurity 事件 |Microsoft 文件"
description: "本文件說明如何 toouse Azure 安全性中心的事件回應案例。"
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
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a><span data-ttu-id="1601c-103">使用 Azure 資訊安全中心進行事件回應</span><span class="sxs-lookup"><span data-stu-id="1601c-103">Using Azure Security Center for an incident response</span></span>
<span data-ttu-id="1601c-104">許多組織了解如何 toorespond toosecurity 事件之後，才遭受攻擊。</span><span class="sxs-lookup"><span data-stu-id="1601c-104">Many organizations learn how toorespond toosecurity incidents only after suffering an attack.</span></span> <span data-ttu-id="1601c-105">tooreduce 成本和損害，很重要 toohave 之前攻擊會發生事件的回應計劃中的地方。</span><span class="sxs-lookup"><span data-stu-id="1601c-105">tooreduce costs and damage, it’s important toohave an incident response plan in place before an attack takes place.</span></span> <span data-ttu-id="1601c-106">您可以在不同階段的事件回應使用 Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="1601c-106">You can use Azure Security Center in different stages of an incident response.</span></span>

## <a name="incident-response-planning"></a><span data-ttu-id="1601c-107">事件回應計劃</span><span class="sxs-lookup"><span data-stu-id="1601c-107">Incident response planning</span></span>
<span data-ttu-id="1601c-108">三個的核心功能的有效計劃而定： 所能 tooprotect，偵測，並回應 toothreats。</span><span class="sxs-lookup"><span data-stu-id="1601c-108">An effective plan depends on three core capabilities: being able tooprotect, detect, and respond toothreats.</span></span> <span data-ttu-id="1601c-109">保護是防止的事件，是關於早期識別威脅的偵測和回應收回 hello 攻擊者，以及還原系統 toomitigate hello 影響有入侵。</span><span class="sxs-lookup"><span data-stu-id="1601c-109">Protection is about preventing incidents, detection is about identifying threats early, and response is about evicting hello attacker and restoring systems toomitigate hello impacts of a breach.</span></span>

<span data-ttu-id="1601c-110">此發行項將會使用從 hello hello 安全性事件回應階段[hello 雲端中的 Microsoft Azure 安全性回應](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678)文章 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="1601c-110">This article will use hello security incident response stages from hello [Microsoft Azure Security Response in hello Cloud](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) article, as shown in hello following diagram:</span></span>

![事件回應生命週期](./media/security-center-incident-response/security-center-incident-response-fig1.png)

<span data-ttu-id="1601c-112">您可以使用資訊安全中心階段 hello 偵測、 評估和診斷。</span><span class="sxs-lookup"><span data-stu-id="1601c-112">You can use Security Center during hello Detect, Assess, and Diagnose stages.</span></span> <span data-ttu-id="1601c-113">以下是範例的如何資訊安全中心功能非常適合在 hello 三個初始事件回應階段期間：</span><span class="sxs-lookup"><span data-stu-id="1601c-113">Here are examples of how Security Center can be useful during hello three initial incident response stages:</span></span>

* <span data-ttu-id="1601c-114">**偵測**： 檢閱 hello 事件進行調查，第一個指示。</span><span class="sxs-lookup"><span data-stu-id="1601c-114">**Detect**: review hello first indication of an event investigation.</span></span>
  * <span data-ttu-id="1601c-115">範例： 檢閱 hello 初始驗證的高安全性警示發生 hello 資訊安全中心儀表板中。</span><span class="sxs-lookup"><span data-stu-id="1601c-115">Example: review hello initial verification that a high-priority security alert was raised in hello Security Center dashboard.</span></span>
* <span data-ttu-id="1601c-116">**評估**： 執行 hello 初始評估 tooobtain hello 可疑活動的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1601c-116">**Assess**: perform hello initial assessment tooobtain more information about hello suspicious activity.</span></span>
  * <span data-ttu-id="1601c-117">範例： 取得 hello 安全性警示的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1601c-117">Example: obtain more information about hello security alert.</span></span>
* <span data-ttu-id="1601c-118">**診斷**︰進行技術性調查，並找出圍堵、緩和及因應策略。</span><span class="sxs-lookup"><span data-stu-id="1601c-118">**Diagnose**: conduct a technical investigation and identify containment, mitigation, and workaround strategies.</span></span>
  * <span data-ttu-id="1601c-119">範例： 請遵循 hello 補救步驟的資訊安全中心述該特定安全性警示。</span><span class="sxs-lookup"><span data-stu-id="1601c-119">Example: follow hello remediation steps described by Security Center in that particular security alert.</span></span>

<span data-ttu-id="1601c-120">hello 案例，如下所示顯示您如何 tooleverage 資訊安全中心期間 hello 偵測、 評估，並診斷/回應安全性事件的階段。</span><span class="sxs-lookup"><span data-stu-id="1601c-120">hello scenario that follows shows you how tooleverage Security Center during hello Detect, Assess, and Diagnose/Respond stages of a security incident.</span></span> <span data-ttu-id="1601c-121">在資訊安全中心內，[安全性事件](security-center-incident.md)是符合[攻擊鏈](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/)模式之資源的所有警示彙總。</span><span class="sxs-lookup"><span data-stu-id="1601c-121">In Security Center, a [security incident](security-center-incident.md) is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="1601c-122">事件會出現在 hello[安全性警示](security-center-managing-and-responding-alerts.md)磚和刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1601c-122">Incidents appear in hello [Security alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="1601c-123">事件會顯示 hello 相關警示清單，可讓您 tooobtain 每次出現的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1601c-123">An incident reveals hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="1601c-124">資訊安全中心也會提供獨立安全性警示，它也可以使用的 tootrack 關閉可疑的活動。</span><span class="sxs-lookup"><span data-stu-id="1601c-124">Security Center also presents standalone security alerts that can also be used tootrack down a suspicious activity.</span></span>

## <a name="scenario"></a><span data-ttu-id="1601c-125">案例</span><span class="sxs-lookup"><span data-stu-id="1601c-125">Scenario</span></span>
<span data-ttu-id="1601c-126">Contoso 最近移轉某些其內部部署資源 tooAzure，包括一些虛擬機器為基礎的業務工作負載和 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1601c-126">Contoso recently migrated some of their on-premises resources tooAzure, including some virtual machine-based line-of-business workloads and SQL databases.</span></span> <span data-ttu-id="1601c-127">Contoso 的核心電腦安全性事件回應小組 (CSIRT) 目前因為尚未整合與其目前事件回應工具的安全性情報，而無法順利調查安全性問題。</span><span class="sxs-lookup"><span data-stu-id="1601c-127">Currently, Contoso's Core Computer Security Incident Response Team (CSIRT) has a problem investigating security issues because of security intelligence not being integrated with their current incident response tools.</span></span> <span data-ttu-id="1601c-128">這種欠缺整合期間 hello 偵測階段 （太多誤判），以及評估 hello 和診斷階段期間，也會發生問題。</span><span class="sxs-lookup"><span data-stu-id="1601c-128">This lack of integration introduces a problem during hello Detect stage (too many false positives), as well as during hello Assess and Diagnose stages.</span></span> <span data-ttu-id="1601c-129">做為此移轉一部分，其決定 tooopt 中的資訊安全中心 toohelp 它們解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="1601c-129">As part of this migration, they decided tooopt in for Security Center toohelp them address this problem.</span></span>

<span data-ttu-id="1601c-130">onboarded hello 後第一階段中完成這個移轉的所有資源，並解決所有 hello 資訊安全中心的安全性建議事項。</span><span class="sxs-lookup"><span data-stu-id="1601c-130">hello first phase of this migration finished after they onboarded all resources and addressed all of hello security recommendations from Security Center.</span></span> <span data-ttu-id="1601c-131">Contoso CSIRT 是 hello 掌管電腦安全性事件的處理。</span><span class="sxs-lookup"><span data-stu-id="1601c-131">Contoso CSIRT is hello focal point for dealing with computer security incidents.</span></span> <span data-ttu-id="1601c-132">hello 小組一群人負責處理任何安全性事件所組成。</span><span class="sxs-lookup"><span data-stu-id="1601c-132">hello team consists of a group of people with responsibilities for dealing with any security incident.</span></span> <span data-ttu-id="1601c-133">hello 小組成員已清楚定義責任 tooensure 保持回應的任何區域未涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="1601c-133">hello team members have clearly defined duties tooensure that no area of response is left uncovered.</span></span>

<span data-ttu-id="1601c-134">為了 hello 這種情況下，我們會 toofocus 上的下列角色，屬於 Contoso CSIRT hello hello 角色：</span><span class="sxs-lookup"><span data-stu-id="1601c-134">For hello purpose of this scenario, we're going toofocus on hello roles of hello following personas that are part of Contoso CSIRT:</span></span>

![事件回應生命週期](./media/security-center-incident-response/security-center-incident-response-fig2.png)

<span data-ttu-id="1601c-136">Judy 負責安全性作業。</span><span class="sxs-lookup"><span data-stu-id="1601c-136">Judy is in security operations.</span></span> <span data-ttu-id="1601c-137">她的職責包括︰</span><span class="sxs-lookup"><span data-stu-id="1601c-137">Her responsibilities include:</span></span>

* <span data-ttu-id="1601c-138">監視及回應 hello 時鐘周圍 toosecurity 威脅。</span><span class="sxs-lookup"><span data-stu-id="1601c-138">Monitoring and responding toosecurity threats around hello clock.</span></span>
* <span data-ttu-id="1601c-139">擴大 toohello 雲端工作負載擁有者或安全性分析師所需。</span><span class="sxs-lookup"><span data-stu-id="1601c-139">Escalating toohello cloud workload owner or security analyst as needed.</span></span>

<span data-ttu-id="1601c-140">Sam 是安全性分析師，他的職責包括︰</span><span class="sxs-lookup"><span data-stu-id="1601c-140">Sam is a security analyst and his responsibilities include:</span></span>

* <span data-ttu-id="1601c-141">調查攻擊。</span><span class="sxs-lookup"><span data-stu-id="1601c-141">Investigating attacks.</span></span>
* <span data-ttu-id="1601c-142">修復警示。</span><span class="sxs-lookup"><span data-stu-id="1601c-142">Remediating alerts.</span></span>
* <span data-ttu-id="1601c-143">使用工作負載擁有者 toodetermine 並套用防護功能。</span><span class="sxs-lookup"><span data-stu-id="1601c-143">Working with workload owners toodetermine and apply mitigations.</span></span>

<span data-ttu-id="1601c-144">如您所見，Judy 與 Sam 有不同的責任，以及必須一起運作 tooshare 資訊安全中心資訊。</span><span class="sxs-lookup"><span data-stu-id="1601c-144">As you can see, Judy and Sam have different responsibilities, and they must work together tooshare Security Center information.</span></span>

## <a name="recommended-solution"></a><span data-ttu-id="1601c-145">建議的解決方案</span><span class="sxs-lookup"><span data-stu-id="1601c-145">Recommended solution</span></span>
<span data-ttu-id="1601c-146">由於 Judy 與 Sam 有不同的角色，他們將日常活動的使用資訊安全中心 tooobtain 相關資訊的不同區域。</span><span class="sxs-lookup"><span data-stu-id="1601c-146">Since Judy and Sam have different roles, they'll be using different areas of Security Center tooobtain relevant information for their daily activities.</span></span> <span data-ttu-id="1601c-147">Judy 會在其日常監視中使用 [安全性警示]。</span><span class="sxs-lookup"><span data-stu-id="1601c-147">Judy will use **Security alerts** as part of her daily monitoring.</span></span>

![安全性警示](./media/security-center-incident-response/security-center-incident-response-fig3.png)

<span data-ttu-id="1601c-149">Judy 將 hello 偵測和評估階段期間使用安全性警示。</span><span class="sxs-lookup"><span data-stu-id="1601c-149">Judy will use Security alerts during hello Detect and Assess stages.</span></span> <span data-ttu-id="1601c-150">Judy hello 初始評估完成時，她可能會提升 hello 問題 tooSam 是否需要進一步調查。</span><span class="sxs-lookup"><span data-stu-id="1601c-150">After Judy finishes hello initial assessment, she might escalate hello issue tooSam if additional investigation is required.</span></span> <span data-ttu-id="1601c-151">此時，Sam 將使用 hello 已提供的資訊安全中心，有時搭配其他資料來源，toomove toohello 診斷階段。</span><span class="sxs-lookup"><span data-stu-id="1601c-151">At this point, Sam will use hello information that was provided by Security Center, sometimes in conjunction with other data sources, toomove toohello Diagnose stage.</span></span>

## <a name="how-tooimplement-this-solution"></a><span data-ttu-id="1601c-152">如何 tooimplement 此解決方案</span><span class="sxs-lookup"><span data-stu-id="1601c-152">How tooimplement this solution</span></span>
<span data-ttu-id="1601c-153">toosee 如何在事件回應案例中，您會使用 Azure 資訊安全中心，我們將在 hello 偵測與評估階段中，請遵循 Judy 的步驟，然後就會看到 Sam 用途 toodiagnose hello 問題。</span><span class="sxs-lookup"><span data-stu-id="1601c-153">toosee how you would use Azure Security Center in an incident response scenario, we’ll follow Judy’s steps in hello Detect and Assess stages, and then see what Sam does toodiagnose hello issue.</span></span>

### <a name="detect-and-assess-incident-response-stages"></a><span data-ttu-id="1601c-154">偵測和評估事件回應階段</span><span class="sxs-lookup"><span data-stu-id="1601c-154">Detect and Assess incident response stages</span></span>
<span data-ttu-id="1601c-155">Judy 登入 toohello Azure 入口網站，並在 hello 資訊安全中心主控台中正常運作。</span><span class="sxs-lookup"><span data-stu-id="1601c-155">Judy signed in toohello Azure portal and is working in hello Security Center console.</span></span> <span data-ttu-id="1601c-156">監視活動其每日的一部分，她開始檢閱執行警示 hello 步驟的高安全性：</span><span class="sxs-lookup"><span data-stu-id="1601c-156">As part of her daily monitoring activities, she started reviewing high-priority security alerts by performing hello following steps:</span></span>

1. <span data-ttu-id="1601c-157">按一下 hello**安全性警示**磚和存取 hello**安全性警示**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1601c-157">Click hello **Security alerts** tile and access hello **Security alerts** blade.</span></span>
    <span data-ttu-id="1601c-158">![安全性警示刀鋒視窗](./media/security-center-incident-response/security-center-incident-response-fig4.png)</span><span class="sxs-lookup"><span data-stu-id="1601c-158">![Security alert blade](./media/security-center-incident-response/security-center-incident-response-fig4.png)</span></span>

   > [!NOTE]
   > <span data-ttu-id="1601c-159">為了 hello 這種情況下，Judy 是進行 tooperform hello 惡意 SQL 活動警示，請評估 hello 前圖所示。</span><span class="sxs-lookup"><span data-stu-id="1601c-159">For hello purpose of this scenario, Judy is going tooperform an assessment on hello Malicious SQL activity alert, as seen in hello preceding figure.</span></span>
   >
   >
2. <span data-ttu-id="1601c-160">按一下 hello**惡意 SQL 活動**警示，並檢閱 hello 中的 hello 攻擊資源**惡意 SQL 活動**刀鋒視窗：![事件詳細資料](./media/security-center-incident-response/security-center-incident-response-fig5.png)</span><span class="sxs-lookup"><span data-stu-id="1601c-160">Click hello **Malicious SQL activity** alert and review hello attacked resources in hello **Malicious SQL activity** blade:  ![Incident details](./media/security-center-incident-response/security-center-incident-response-fig5.png)</span></span>

    <span data-ttu-id="1601c-161">在這個刀鋒視窗中，Judy 可以記下 hello 遭受攻擊的資源，如何多次這種攻擊發生，而且當它偵測到。</span><span class="sxs-lookup"><span data-stu-id="1601c-161">In this blade, Judy can take notes regarding hello attacked resources, how many times this attack happened, and when it was detected.</span></span>
3. <span data-ttu-id="1601c-162">按一下 hello**攻擊資源**tooobtain 這種攻擊的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1601c-162">Click hello **attacked resource** tooobtain more information about this attack.</span></span>

<span data-ttu-id="1601c-163">閱讀後 hello 描述，會將 Judy 相信這不是誤判和她應該擴大此案例 tooSam。</span><span class="sxs-lookup"><span data-stu-id="1601c-163">After reading hello description, Judy is convinced that this is not a false positive and that she should escalate this case tooSam.</span></span>

### <a name="diagnose-incident-response-stage"></a><span data-ttu-id="1601c-164">診斷事件回應階段</span><span class="sxs-lookup"><span data-stu-id="1601c-164">Diagnose incident response stage</span></span>
<span data-ttu-id="1601c-165">Sam Judy 從收到 hello 案例，並啟動 檢閱建議的資訊安全中心的 hello 修復步驟。</span><span class="sxs-lookup"><span data-stu-id="1601c-165">Sam receives hello case from Judy and starts reviewing hello remediation steps that Security Center suggested.</span></span>

![事件回應生命週期](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a><span data-ttu-id="1601c-167">其他資源</span><span class="sxs-lookup"><span data-stu-id="1601c-167">Additional resources</span></span>
<span data-ttu-id="1601c-168">hello 事件回應小組也可以利用的 hello[安全性中心 Power BI](security-center-powerbi.md)功能 toosee 不同類型的報表。</span><span class="sxs-lookup"><span data-stu-id="1601c-168">hello incident response team can also take advantage of hello [Security Center Power BI](security-center-powerbi.md) capability toosee different types of reports.</span></span> <span data-ttu-id="1601c-169">這些報告可以協助他們進一步調查 toovisualize 期間、 分析和篩選器的建議和安全性警示。</span><span class="sxs-lookup"><span data-stu-id="1601c-169">These reports can help them during further investigation toovisualize, analyze, and filter recommendations and security alerts.</span></span> <span data-ttu-id="1601c-170">對公司來說，在 hello 調查程序時使用其安全性資訊和事件管理 (SIEM) 解決方案，他們也可以[整合與解決方案的資訊安全中心](security-center-integrating-alerts-with-log-integration.md)。</span><span class="sxs-lookup"><span data-stu-id="1601c-170">For companies that use their security information and event management (SIEM) solution during hello investigation process, they can also [integrate Security Center with their solution](security-center-integrating-alerts-with-log-integration.md).</span></span> <span data-ttu-id="1601c-171">您也可以使用 hello 整合 Azure 稽核記錄檔和虛擬機器 (VM) 的安全性事件[Azure 記錄檔整合工具](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/)。</span><span class="sxs-lookup"><span data-stu-id="1601c-171">You can also integrate Azure audit logs and virtual machine (VM) security events by using hello [Azure log integration tool](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/).</span></span> <span data-ttu-id="1601c-172">tooinvestigate 攻擊，您可以使用這項資訊搭配 hello 資訊安全中心提供。</span><span class="sxs-lookup"><span data-stu-id="1601c-172">tooinvestigate an attack, you can use this information in conjunction with hello information that Security Center provides.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1601c-173">結論</span><span class="sxs-lookup"><span data-stu-id="1601c-173">Conclusion</span></span>
<span data-ttu-id="1601c-174">事件發生之前，執行組合小組是非常重要的 tooyour 組織和正面影響事件的處理方式。</span><span class="sxs-lookup"><span data-stu-id="1601c-174">Assembling a team before an incident occurs is very important tooyour organization and will positively influence how incidents are handled.</span></span> <span data-ttu-id="1601c-175">Hello 適當的工具 toomonitor 資源可協助此小組 tootake 精確步驟 tooremediate 安全性事件。</span><span class="sxs-lookup"><span data-stu-id="1601c-175">Having hello right tools toomonitor resources can help this team tootake accurate steps tooremediate a security incident.</span></span> <span data-ttu-id="1601c-176">資訊安全中心[偵測功能](security-center-detection-capabilities.md)可以協助 IT tooquickly 回應 toosecurity 事件並修復安全性問題。</span><span class="sxs-lookup"><span data-stu-id="1601c-176">Security Center [detection capabilities](security-center-detection-capabilities.md) can assist IT tooquickly respond toosecurity incidents and remediate security issues.</span></span>
