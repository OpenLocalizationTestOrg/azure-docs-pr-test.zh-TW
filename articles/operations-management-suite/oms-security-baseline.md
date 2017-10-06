---
title: "管理組件安全性和稽核解決方案基準 aaaOperations |Microsoft 文件"
description: "本文件說明如何 toouse OMS 安全性和稽核解決方案 tooperform 相容性和安全性用途的所有受監視電腦的基準評估。"
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
ms.openlocfilehash: ea52408cb9d2598728fe3826a946067e1c99318f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="47b4d-103">Operations Management Suite 安全性和稽核解決方案中的基準評估</span><span class="sxs-lookup"><span data-stu-id="47b4d-103">Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="47b4d-104">這份文件可協助您 toouse [Operations Management Suite (OMS) 的安全性和稽核解決方案](operations-management-suite-overview.md)基準評估功能 tooaccess hello 受監視資源的安全的狀態。</span><span class="sxs-lookup"><span data-stu-id="47b4d-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-baseline-assessment"></a><span data-ttu-id="47b4d-105">什麼是基準評估？</span><span class="sxs-lookup"><span data-stu-id="47b4d-105">What is Baseline Assessment?</span></span>
<span data-ttu-id="47b4d-106">Microsoft 與全球產業和政府組織共同定義可代表高度安全伺服器部署的 Windows 組態。</span><span class="sxs-lookup"><span data-stu-id="47b4d-106">Microsoft, together with industry and government organizations worldwide, defines a Windows configuration that represents highly secure server deployments.</span></span> <span data-ttu-id="47b4d-107">此組態是一組登錄機碼、稽核原則設定和安全性原則設定，以及 Microsoft 對於這些設定的建議值。</span><span class="sxs-lookup"><span data-stu-id="47b4d-107">This configuration is a set of registry keys, audit policy settings, and security policy settings along with Microsoft’s recommended values for these settings.</span></span> <span data-ttu-id="47b4d-108">這組規則也稱為安全性基準。</span><span class="sxs-lookup"><span data-stu-id="47b4d-108">This set of rules is known as Security baseline.</span></span> <span data-ttu-id="47b4d-109">OMS 安全性和稽核基準評估功能可以順暢地掃描所有電腦的相容性。</span><span class="sxs-lookup"><span data-stu-id="47b4d-109">OMS Security and Audit baseline assessment capability can seamlessly scan all your computers for compliance.</span></span> 

<span data-ttu-id="47b4d-110">規則類型有三種：</span><span class="sxs-lookup"><span data-stu-id="47b4d-110">There are three types of rules:</span></span>

* <span data-ttu-id="47b4d-111">**登錄規則**︰檢查登錄機碼是否正確設定。</span><span class="sxs-lookup"><span data-stu-id="47b4d-111">**Registry rules**: check that registry keys are set correctly.</span></span>
* <span data-ttu-id="47b4d-112">**稽核原則規則**︰稽核原則相關規則。</span><span class="sxs-lookup"><span data-stu-id="47b4d-112">**Audit policy rules**: rules regarding your audit policy.</span></span>
* <span data-ttu-id="47b4d-113">**安全性原則規則**： 規則 hello 電腦上有關 hello 使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="47b4d-113">**Security policy rules**: rules regarding hello user’s permissions on hello machine.</span></span>

> [!NOTE]
> <span data-ttu-id="47b4d-114">讀取[使用 OMS 安全性 tooassess hello 安全性組態基準](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/)這項功能的簡要概觀。</span><span class="sxs-lookup"><span data-stu-id="47b4d-114">Read [Use OMS Security tooassess hello Security Configuration Baseline](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) for a brief overview of this feature.</span></span>
> 
> 

## <a name="security-baseline-assessment"></a><span data-ttu-id="47b4d-115">安全性基準評估</span><span class="sxs-lookup"><span data-stu-id="47b4d-115">Security Baseline Assessment</span></span>
<span data-ttu-id="47b4d-116">您可以檢閱目前的安全性基準評估受 OMS 安全性和稽核使用 hello 儀表板的所有電腦。</span><span class="sxs-lookup"><span data-stu-id="47b4d-116">You can review your current security baseline assessment for all computers that are monitored by OMS Security and Audit using hello dashboard.</span></span>  <span data-ttu-id="47b4d-117">執行下列步驟 tooaccess hello 安全性基準評估的儀表板的 hello:</span><span class="sxs-lookup"><span data-stu-id="47b4d-117">Execute hello following steps tooaccess hello security baseline assessment dashboard:</span></span>

1. <span data-ttu-id="47b4d-118">在 hello **Microsoft Operations Management Suite**主要儀表板中，按一下**安全性和稽核**磚。</span><span class="sxs-lookup"><span data-stu-id="47b4d-118">In hello **Microsoft Operations Management Suite** main dashboard, click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="47b4d-119">在 hello**安全性和稽核**儀表板，按一下 **基準評估**下**安全性網域**。</span><span class="sxs-lookup"><span data-stu-id="47b4d-119">In hello **Security and Audit** dashboard, click **Baseline Assessment** under **Security Domains**.</span></span> <span data-ttu-id="47b4d-120">hello**安全性基準評估**儀表板會顯示 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="47b4d-120">hello **Security Baseline Assessment** dashboard appears as shown in hello following image:</span></span>
   
    ![OMS 安全性和稽核基準評估](./media/oms-security-baseline/oms-security-baseline-fig1.png)

<span data-ttu-id="47b4d-122">此儀表板分成三個主要區域︰</span><span class="sxs-lookup"><span data-stu-id="47b4d-122">This dashboard is divided in three major areas:</span></span>

* <span data-ttu-id="47b4d-123">**電腦比較 toobaseline**： 這個區段讓 hello 可供存取且 hello 的傳遞 hello 評估的電腦百分比的電腦數目的摘要。</span><span class="sxs-lookup"><span data-stu-id="47b4d-123">**Computers compared toobaseline**: this section gives a summary of hello number of computers that were accessed and hello percentage of computers that passed hello assessment.</span></span> <span data-ttu-id="47b4d-124">它也會提供 hello 前 10 台電腦及 hello 百分比結果 hello 評估。</span><span class="sxs-lookup"><span data-stu-id="47b4d-124">It also gives hello top 10 computers and hello percentage result for hello assessment.</span></span>
* <span data-ttu-id="47b4d-125">**所需規則的狀態**： 此區段已依嚴重性的 hello 意圖 toobring 感知的 hello 失敗規則，且失敗規則的類型。</span><span class="sxs-lookup"><span data-stu-id="47b4d-125">**Required Rules Status**: this section has hello intent toobring awareness of hello failed rules by severity and failed rules by type.</span></span> <span data-ttu-id="47b4d-126">尋找您可以快速識別大部分 hello 失敗規則 toohello 第一個圖形都非常重要，或不。</span><span class="sxs-lookup"><span data-stu-id="47b4d-126">By looking toohello first graph you can quickly identify if most hello failed rules are critical, or not.</span></span> <span data-ttu-id="47b4d-127">同時也提供一份 hello 前 10 個失敗的規則的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="47b4d-127">It also gives a list of hello top 10 failed rules and their severity.</span></span> <span data-ttu-id="47b4d-128">hello 第二個圖表會顯示 hello hello 評估期間失敗的規則類型。</span><span class="sxs-lookup"><span data-stu-id="47b4d-128">hello second graph shows hello type of rule that failed during hello assessment.</span></span> 
* <span data-ttu-id="47b4d-129">**遺失基準評估電腦**： 本節列出 hello 電腦已無法存取到期 toooperating 系統不相容的問題或失敗。</span><span class="sxs-lookup"><span data-stu-id="47b4d-129">**Computers missing baseline assessment**: this section list hello computers that were not accessed due toooperating system incompatibility or failures.</span></span> 

### <a name="accessing-computers-compared-toobaseline"></a><span data-ttu-id="47b4d-130">存取電腦比較 toobaseline</span><span class="sxs-lookup"><span data-stu-id="47b4d-130">Accessing computers compared toobaseline</span></span>
<span data-ttu-id="47b4d-131">在理想情況下的所有電腦都必須符合的 hello 安全性基準評估。</span><span class="sxs-lookup"><span data-stu-id="47b4d-131">Ideally all your computers are be compliant with hello security baseline assessment.</span></span> <span data-ttu-id="47b4d-132">不過，在某些情況下，應該不會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="47b4d-132">However it is expected that in some circumstances this doesn't happen.</span></span> <span data-ttu-id="47b4d-133">Hello 安全性管理程序的一部分，它是重要 tooinclude 檢閱 hello 無法 toopass 安全性評估通過所有測試的電腦。</span><span class="sxs-lookup"><span data-stu-id="47b4d-133">As part of hello security management process, it is important tooinclude reviewing hello computers that failed toopass all security assessment tests.</span></span> <span data-ttu-id="47b4d-134">藉由選取 hello 選項是快速 toovisualize**存取電腦**位於 hello**電腦比較 toobaseline** > 一節。</span><span class="sxs-lookup"><span data-stu-id="47b4d-134">A quick way toovisualize that is by selecting hello option **Computers accessed** located in hello **Computers compared toobaseline** section.</span></span> <span data-ttu-id="47b4d-135">您應該會看到 hello 記錄搜尋結果顯示 hello 的電腦清單中 hello 遵循畫面所示：</span><span class="sxs-lookup"><span data-stu-id="47b4d-135">You should see hello log search result showing hello list of computers as shows in hello following screen:</span></span>

![存取的電腦結果](./media/oms-security-baseline/oms-security-baseline-fig2.png)

<span data-ttu-id="47b4d-137">hello 搜尋結果會顯示以資料表格式，其中 hello 第一個資料行具有 hello 電腦名稱，而 hello 第二個色彩有 hello 失敗的規則數目。</span><span class="sxs-lookup"><span data-stu-id="47b4d-137">hello search result is shown in a table format, where hello first column has hello computer name and hello second color has hello number of rules that failed.</span></span> <span data-ttu-id="47b4d-138">tooretrieve hello 有關 hello 的規則類型失敗，按一下 hello hello 電腦名稱除了失敗的規則數目。</span><span class="sxs-lookup"><span data-stu-id="47b4d-138">tooretrieve hello information regarding hello type of rule that failed, click in hello number of failed rules besides hello computer name.</span></span> <span data-ttu-id="47b4d-139">您應該會看到結果類似 toohello hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="47b4d-139">You should see a result similar toohello one shown in hello following image:</span></span>

![存取的電腦結果詳細資料](./media/oms-security-baseline/oms-security-baseline-fig3.png)

<span data-ttu-id="47b4d-141">在搜尋結果中，您有存取規則的 hello 總數、 hello 嚴重失敗的規則數目 hello 警告規則和 hello 資訊失敗規則。</span><span class="sxs-lookup"><span data-stu-id="47b4d-141">In this search result, you have hello total of accessed rules, hello number of critical rules that failed, hello warning rules and hello information failed rules.</span></span>

### <a name="accessing-required-rules-status"></a><span data-ttu-id="47b4d-142">存取需要的規則狀態</span><span class="sxs-lookup"><span data-stu-id="47b4d-142">Accessing required rules status</span></span>
<span data-ttu-id="47b4d-143">取得相關的電腦傳送嗨評估 hello 百分比數字的 hello 資訊之後，您可能想的 tooobtain 失敗相應 toohello 重要性的規則的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="47b4d-143">After obtaining hello information regarding hello percentage number of computers that passed hello assessment, you may want tooobtain more information about which rules are failing according toohello criticality.</span></span> <span data-ttu-id="47b4d-144">此視覺效果可協助您 tooprioritize 哪些電腦應該處理第一個 tooensure 將無法相容 hello 下一個評估中。</span><span class="sxs-lookup"><span data-stu-id="47b4d-144">This visualization helps you tooprioritize which computers should be addressed first tooensure they will be compliant in hello next assessment.</span></span> <span data-ttu-id="47b4d-145">將滑鼠停留在 hello 很重要的一部分位於 hello hello 圖形**失敗規則依嚴重性**磚，在**所需規則的狀態**，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="47b4d-145">Hover over hello Critical part of hello graph located in hello **Failed rules by severity** tile, under **Required rules status** and click it.</span></span> <span data-ttu-id="47b4d-146">您應該會看到下列畫面結果類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="47b4d-146">You should see a result similar toohello following screen:</span></span>

![依嚴重性的失敗規則詳細資料](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

<span data-ttu-id="47b4d-148">這個記錄檔結果中，您會看到 hello 基準規則失敗，這個規則，與此安全性規則的 hello 通用組態列舉 (CCE) 識別碼 hello 描述的類型。</span><span class="sxs-lookup"><span data-stu-id="47b4d-148">In this log result you see hello type of baseline rule that failed, hello description of this rule, and hello Common Configuration Enumeration (CCE) ID of this security rule.</span></span> <span data-ttu-id="47b4d-149">這些屬性應該是足夠 tooperform 矯正措施 toofix hello 目標電腦中的這個問題。</span><span class="sxs-lookup"><span data-stu-id="47b4d-149">These attributes should be enough tooperform a corrective action toofix this problem in hello target computer.</span></span>

> [!NOTE]
> <span data-ttu-id="47b4d-150">如需有關 CCE 的詳細資訊，請存取 hello[國家 （地區） 的弱點可能會資料庫](https://nvd.nist.gov/cce/index.cfm)。</span><span class="sxs-lookup"><span data-stu-id="47b4d-150">For more information about CCE, access hello [National Vulnerability Database](https://nvd.nist.gov/cce/index.cfm).</span></span>
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="47b4d-151">存取遺失基準評估的電腦</span><span class="sxs-lookup"><span data-stu-id="47b4d-151">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="47b4d-152">OMS hello 網域成員和網域控制站基準設定檔在 Windows Server 2008 R2 上最多可支援 tooWindows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="47b4d-152">OMS supports hello domain member and Domain Controller baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="47b4d-153">Windows Server 2016 基準尚未定案，將在發佈後盡快新增。</span><span class="sxs-lookup"><span data-stu-id="47b4d-153">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="47b4d-154">透過 OMS 安全性和稽核基準評估掃描的所有其他作業系統之下 hello**遺失基準評估電腦**> 一節。</span><span class="sxs-lookup"><span data-stu-id="47b4d-154">All other operating systems scanned via OMS Security and Audit baseline assessment appears under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="47b4d-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="47b4d-155">See also</span></span>
<span data-ttu-id="47b4d-156">在本文件中，您已了解 OMS 安全性和稽核基準評估。</span><span class="sxs-lookup"><span data-stu-id="47b4d-156">In this document, you learned about OMS Security and Audit baseline assessment.</span></span> <span data-ttu-id="47b4d-157">toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="47b4d-157">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="47b4d-158">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="47b4d-158">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="47b4d-159">監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="47b4d-159">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="47b4d-160">在 Operations Management Suite 安全性和稽核解決方案內監視資源</span><span class="sxs-lookup"><span data-stu-id="47b4d-160">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

