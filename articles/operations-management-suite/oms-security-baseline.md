---
title: "Operations Management Suite 安全性和稽核解決方案基準 | Microsoft Docs"
description: "本文件說明如何針對相容性和安全性目的，使用 OMS 安全性和稽核解決方案來執行所有受監視電腦的基準評估。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d538eee4dccdbf158baab8908ebfff56713bde95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="e6565-103">Operations Management Suite 安全性和稽核解決方案中的基準評估</span><span class="sxs-lookup"><span data-stu-id="e6565-103">Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="e6565-104">本文件協助您使用 [Operations Management Suite (OMS) 安全性和稽核解決方案](operations-management-suite-overview.md)的基準評估功能，存取受監視資源的安全狀態。</span><span class="sxs-lookup"><span data-stu-id="e6565-104">This document helps you to use [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) baseline assessment capabilities to access the secure state of your monitored resources.</span></span>

## <a name="what-is-baseline-assessment"></a><span data-ttu-id="e6565-105">什麼是基準評估？</span><span class="sxs-lookup"><span data-stu-id="e6565-105">What is Baseline Assessment?</span></span>
<span data-ttu-id="e6565-106">Microsoft 與全球產業和政府組織共同定義可代表高度安全伺服器部署的 Windows 組態。</span><span class="sxs-lookup"><span data-stu-id="e6565-106">Microsoft, together with industry and government organizations worldwide, defines a Windows configuration that represents highly secure server deployments.</span></span> <span data-ttu-id="e6565-107">此組態是一組登錄機碼、稽核原則設定和安全性原則設定，以及 Microsoft 對於這些設定的建議值。</span><span class="sxs-lookup"><span data-stu-id="e6565-107">This configuration is a set of registry keys, audit policy settings, and security policy settings along with Microsoft’s recommended values for these settings.</span></span> <span data-ttu-id="e6565-108">這組規則也稱為安全性基準。</span><span class="sxs-lookup"><span data-stu-id="e6565-108">This set of rules is known as Security baseline.</span></span> <span data-ttu-id="e6565-109">OMS 安全性和稽核基準評估功能可以順暢地掃描所有電腦的相容性。</span><span class="sxs-lookup"><span data-stu-id="e6565-109">OMS Security and Audit baseline assessment capability can seamlessly scan all your computers for compliance.</span></span> 

<span data-ttu-id="e6565-110">規則類型有三種：</span><span class="sxs-lookup"><span data-stu-id="e6565-110">There are three types of rules:</span></span>

* <span data-ttu-id="e6565-111">**登錄規則**︰檢查登錄機碼是否正確設定。</span><span class="sxs-lookup"><span data-stu-id="e6565-111">**Registry rules**: check that registry keys are set correctly.</span></span>
* <span data-ttu-id="e6565-112">**稽核原則規則**︰稽核原則相關規則。</span><span class="sxs-lookup"><span data-stu-id="e6565-112">**Audit policy rules**: rules regarding your audit policy.</span></span>
* <span data-ttu-id="e6565-113">**安全性原則規則**︰使用者的電腦使用權限相關規則。</span><span class="sxs-lookup"><span data-stu-id="e6565-113">**Security policy rules**: rules regarding the user’s permissions on the machine.</span></span>

> [!NOTE]
> <span data-ttu-id="e6565-114">如需這項功能的概觀，請參閱[使用 OMS 安全性來評估安全性組態基準](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/)。</span><span class="sxs-lookup"><span data-stu-id="e6565-114">Read [Use OMS Security to assess the Security Configuration Baseline](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) for a brief overview of this feature.</span></span>
> 
> 

## <a name="security-baseline-assessment"></a><span data-ttu-id="e6565-115">安全性基準評估</span><span class="sxs-lookup"><span data-stu-id="e6565-115">Security Baseline Assessment</span></span>
<span data-ttu-id="e6565-116">您可以使用儀表板，針對 OMS 安全性和稽核監視的所有電腦，檢閱目前的安全性基準評估。</span><span class="sxs-lookup"><span data-stu-id="e6565-116">You can review your current security baseline assessment for all computers that are monitored by OMS Security and Audit using the dashboard.</span></span>  <span data-ttu-id="e6565-117">執行下列步驟以存取安全性基準評估儀表板︰</span><span class="sxs-lookup"><span data-stu-id="e6565-117">Execute the following steps to access the security baseline assessment dashboard:</span></span>

1. <span data-ttu-id="e6565-118">在 [Microsoft Operations Management Suite] 主儀表板中，按一下 [安全性和稽核] 圖格。</span><span class="sxs-lookup"><span data-stu-id="e6565-118">In the **Microsoft Operations Management Suite** main dashboard, click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="e6565-119">在 [安全性和稽核] 儀表板中，按一下 [安全性網域] 下的 [基準評估]。</span><span class="sxs-lookup"><span data-stu-id="e6565-119">In the **Security and Audit** dashboard, click **Baseline Assessment** under **Security Domains**.</span></span> <span data-ttu-id="e6565-120">[安全性基準評估]儀表板隨即出現，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="e6565-120">The **Security Baseline Assessment** dashboard appears as shown in the following image:</span></span>
   
    ![OMS 安全性和稽核基準評估](./media/oms-security-baseline/oms-security-baseline-fig1.png)

<span data-ttu-id="e6565-122">此儀表板分成三個主要區域︰</span><span class="sxs-lookup"><span data-stu-id="e6565-122">This dashboard is divided in three major areas:</span></span>

* <span data-ttu-id="e6565-123">**與基準比對的電腦**︰這個區段提供已存取的電腦數和通過評估的電腦百分比摘要。</span><span class="sxs-lookup"><span data-stu-id="e6565-123">**Computers compared to baseline**: this section gives a summary of the number of computers that were accessed and the percentage of computers that passed the assessment.</span></span> <span data-ttu-id="e6565-124">它也會提供評估中排前 10 名的電腦和百分比結果。</span><span class="sxs-lookup"><span data-stu-id="e6565-124">It also gives the top 10 computers and the percentage result for the assessment.</span></span>
* <span data-ttu-id="e6565-125">**需要的規則狀態**︰這個區段的用意是要提醒大家注意失敗的規則 (依嚴重性) 和失敗的規則 (依類型)。</span><span class="sxs-lookup"><span data-stu-id="e6565-125">**Required Rules Status**: this section has the intent to bring awareness of the failed rules by severity and failed rules by type.</span></span> <span data-ttu-id="e6565-126">查看第一張圖，您即可快速識別大部分的失敗規則是否重大。</span><span class="sxs-lookup"><span data-stu-id="e6565-126">By looking to the first graph you can quickly identify if most the failed rules are critical, or not.</span></span> <span data-ttu-id="e6565-127">該圖還提供排前 10 名的失敗規則與其嚴重性。</span><span class="sxs-lookup"><span data-stu-id="e6565-127">It also gives a list of the top 10 failed rules and their severity.</span></span> <span data-ttu-id="e6565-128">第二張圖會顯示在評估期間失敗的規則類型。</span><span class="sxs-lookup"><span data-stu-id="e6565-128">The second graph shows the type of rule that failed during the assessment.</span></span> 
* <span data-ttu-id="e6565-129">**遺失基準評估的電腦**︰這個區段列出因為作業系統不相容或失敗而無法存取的電腦。</span><span class="sxs-lookup"><span data-stu-id="e6565-129">**Computers missing baseline assessment**: this section list the computers that were not accessed due to operating system incompatibility or failures.</span></span> 

### <a name="accessing-computers-compared-to-baseline"></a><span data-ttu-id="e6565-130">存取與基準比對的電腦</span><span class="sxs-lookup"><span data-stu-id="e6565-130">Accessing computers compared to baseline</span></span>
<span data-ttu-id="e6565-131">在理想情況下，您所有的電腦都會符合安全性基準評估。</span><span class="sxs-lookup"><span data-stu-id="e6565-131">Ideally all your computers are be compliant with the security baseline assessment.</span></span> <span data-ttu-id="e6565-132">不過，在某些情況下，應該不會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="e6565-132">However it is expected that in some circumstances this doesn't happen.</span></span> <span data-ttu-id="e6565-133">在安全性管理程序中，請務必包含檢閱未通過所有安全性評估測試的電腦。</span><span class="sxs-lookup"><span data-stu-id="e6565-133">As part of the security management process, it is important to include reviewing the computers that failed to pass all security assessment tests.</span></span> <span data-ttu-id="e6565-134">選取位於 [與基準比對的電腦] 區段中的 [存取的電腦] 選項，即可快速呈現該資料。</span><span class="sxs-lookup"><span data-stu-id="e6565-134">A quick way to visualize that is by selecting the option **Computers accessed** located in the **Computers compared to baseline** section.</span></span> <span data-ttu-id="e6565-135">您應該會看到記錄檔搜尋結果顯示如下列畫面所示的電腦清單︰</span><span class="sxs-lookup"><span data-stu-id="e6565-135">You should see the log search result showing the list of computers as shows in the following screen:</span></span>

![存取的電腦結果](./media/oms-security-baseline/oms-security-baseline-fig2.png)

<span data-ttu-id="e6565-137">搜尋結果會以表格表格式顯示，其中第一欄為電腦名稱，而第二欄為失敗的規則數目。</span><span class="sxs-lookup"><span data-stu-id="e6565-137">The search result is shown in a table format, where the first column has the computer name and the second color has the number of rules that failed.</span></span> <span data-ttu-id="e6565-138">若要擷取失敗的規則類型相關資訊，請按一下電腦名稱旁邊的失敗規則數目。</span><span class="sxs-lookup"><span data-stu-id="e6565-138">To retrieve the information regarding the type of rule that failed, click in the number of failed rules besides the computer name.</span></span> <span data-ttu-id="e6565-139">您應該會看到類似下圖所示的結果︰</span><span class="sxs-lookup"><span data-stu-id="e6565-139">You should see a result similar to the one shown in the following image:</span></span>

![存取的電腦結果詳細資料](./media/oms-security-baseline/oms-security-baseline-fig3.png)

<span data-ttu-id="e6565-141">在此搜尋結果中，您可看見存取的規則總數、重大失敗規則、警告規則和資訊失敗規則的數目。</span><span class="sxs-lookup"><span data-stu-id="e6565-141">In this search result, you have the total of accessed rules, the number of critical rules that failed, the warning rules and the information failed rules.</span></span>

### <a name="accessing-required-rules-status"></a><span data-ttu-id="e6565-142">存取需要的規則狀態</span><span class="sxs-lookup"><span data-stu-id="e6565-142">Accessing required rules status</span></span>
<span data-ttu-id="e6565-143">取得通過評估的電腦數百分比相關資訊之後，建議您根據重要性取得更多哪些規則失敗的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e6565-143">After obtaining the information regarding the percentage number of computers that passed the assessment, you may want to obtain more information about which rules are failing according to the criticality.</span></span> <span data-ttu-id="e6565-144">此視覺效果可協助您設定哪些電腦應先處理的優先順序，以確保它們會在下一次評估中相容。</span><span class="sxs-lookup"><span data-stu-id="e6565-144">This visualization helps you to prioritize which computers should be addressed first to ensure they will be compliant in the next assessment.</span></span> <span data-ttu-id="e6565-145">將滑鼠移至圖形的「重大」部分 (位於 [需要的規則狀態] 下的 [失敗的規則 (依嚴重性)] 圖格中) 並且按一下。</span><span class="sxs-lookup"><span data-stu-id="e6565-145">Hover over the Critical part of the graph located in the **Failed rules by severity** tile, under **Required rules status** and click it.</span></span> <span data-ttu-id="e6565-146">您應該會看到類似以下畫面的結果：</span><span class="sxs-lookup"><span data-stu-id="e6565-146">You should see a result similar to the following screen:</span></span>

![依嚴重性的失敗規則詳細資料](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

<span data-ttu-id="e6565-148">在此記錄檔結果中，您會看到失敗的基準規則類型、此規則的描述，以及此安全性規則的Common Configuration Enumeration (CCE) ID。</span><span class="sxs-lookup"><span data-stu-id="e6565-148">In this log result you see the type of baseline rule that failed, the description of this rule, and the Common Configuration Enumeration (CCE) ID of this security rule.</span></span> <span data-ttu-id="e6565-149">這些屬性應足以執行更正動作，以修正目標電腦的這個問題。</span><span class="sxs-lookup"><span data-stu-id="e6565-149">These attributes should be enough to perform a corrective action to fix this problem in the target computer.</span></span>

> [!NOTE]
> <span data-ttu-id="e6565-150">如需 CCE 的詳細資訊，請存取 [National Vulnerability Database](https://nvd.nist.gov/cce/index.cfm)。</span><span class="sxs-lookup"><span data-stu-id="e6565-150">For more information about CCE, access the [National Vulnerability Database](https://nvd.nist.gov/cce/index.cfm).</span></span>
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="e6565-151">存取遺失基準評估的電腦</span><span class="sxs-lookup"><span data-stu-id="e6565-151">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="e6565-152">OMS 支援 Windows Server 2008 R2 至 Windows Server 2012 R2 的網域成員和網域控制站基準設定檔。</span><span class="sxs-lookup"><span data-stu-id="e6565-152">OMS supports the domain member and Domain Controller baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span></span> <span data-ttu-id="e6565-153">Windows Server 2016 基準尚未定案，將在發佈後盡快新增。</span><span class="sxs-lookup"><span data-stu-id="e6565-153">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="e6565-154">透過 OMS 安全性和稽核基準評估掃描的其他所有作業系統會顯示在 [遺失基準評估的電腦] 區段之下。</span><span class="sxs-lookup"><span data-stu-id="e6565-154">All other operating systems scanned via OMS Security and Audit baseline assessment appears under the **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="e6565-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e6565-155">See also</span></span>
<span data-ttu-id="e6565-156">在本文件中，您已了解 OMS 安全性和稽核基準評估。</span><span class="sxs-lookup"><span data-stu-id="e6565-156">In this document, you learned about OMS Security and Audit baseline assessment.</span></span> <span data-ttu-id="e6565-157">若要深入了解 OMS 安全性，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="e6565-157">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="e6565-158">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="e6565-158">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="e6565-159">在 Operations Management Suite 安全性和稽核內監視及回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="e6565-159">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="e6565-160">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="e6565-160">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

