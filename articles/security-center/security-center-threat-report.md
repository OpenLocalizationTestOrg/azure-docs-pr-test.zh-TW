---
title: "Azure 資訊安全中心威脅情報報告 | Microsoft Docs"
description: "本文件可協助您在調查期間使用 Azure 資訊安全中心威脅情報報告，找出更多關於安全性警示的資訊。"
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: b4310cf4e6849c67031b3ec8b1fd5957e35f7ea6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a><span data-ttu-id="fa694-103">Azure 資訊安全中心威脅情報報告</span><span class="sxs-lookup"><span data-stu-id="fa694-103">Azure Security Center Threat Intelligence Report</span></span>
<span data-ttu-id="fa694-104">本文件說明 Azure 資訊安全中心威脅情報報告可如何協助您深入了解產生安全性警示的威脅。</span><span class="sxs-lookup"><span data-stu-id="fa694-104">This document explains how Azure Security Center Threat Intelligent Reports can help you learn more about a threat that generated a security alert.</span></span>

## <a name="what-is-a-threat-intelligence-report"></a><span data-ttu-id="fa694-105">何謂威脅情報報告？</span><span class="sxs-lookup"><span data-stu-id="fa694-105">What is a threat intelligence report?</span></span>
<span data-ttu-id="fa694-106">資訊安全中心威脅偵測的運作方式如下：監視來自 Azure 資源、網路和已連線合作夥伴解決方案的安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="fa694-106">Security Center threat detection works by monitoring security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="fa694-107">它會分析這項資訊 (通常是來自多個來源的相互關聯資訊) 以識別威脅。</span><span class="sxs-lookup"><span data-stu-id="fa694-107">It analyzes this information, often correlating information from multiple sources, to identify threats.</span></span> <span data-ttu-id="fa694-108">此程序為資訊安全中心[偵測功能](security-center-detection-capabilities.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="fa694-108">This process is part of the Security Center [detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="fa694-109">當資訊安全中心識別到威脅時，便會觸發[安全性警示](security-center-managing-and-responding-alerts.md)，其內含關於特定事件的詳細資訊，包括修復方面的建議。</span><span class="sxs-lookup"><span data-stu-id="fa694-109">When Security Center identifies a threat, it will trigger a [security alert](security-center-managing-and-responding-alerts.md), which contains detailed information regarding a particular event, including suggestions for remediation.</span></span> <span data-ttu-id="fa694-110">為了協助事件回應小組調查和修復威脅，資訊安全中心包含威脅情報報告，報告中含有偵測到之威脅的相關資訊，包括如下資訊：</span><span class="sxs-lookup"><span data-stu-id="fa694-110">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected, including information such as the:</span></span>

* <span data-ttu-id="fa694-111">攻擊者的身分識別或關聯 (如果有提供這項資訊)</span><span class="sxs-lookup"><span data-stu-id="fa694-111">Attacker’s identity or associations (if this information is available)</span></span>
* <span data-ttu-id="fa694-112">攻擊者的目標</span><span class="sxs-lookup"><span data-stu-id="fa694-112">Attackers’ objectives</span></span>
* <span data-ttu-id="fa694-113">目前和過往的攻擊活動 (如果有提供這項資訊)</span><span class="sxs-lookup"><span data-stu-id="fa694-113">Current and historical attack campaigns (if this information is available)</span></span>
* <span data-ttu-id="fa694-114">攻擊者的策略、工具和程序</span><span class="sxs-lookup"><span data-stu-id="fa694-114">Attackers’ tactics, tools and procedures</span></span>
* <span data-ttu-id="fa694-115">關聯的入侵指標 (IoC)，例如 URL 和檔案雜湊</span><span class="sxs-lookup"><span data-stu-id="fa694-115">Associated indicators of compromise (IoC) such as URLs and file hashes</span></span>
* <span data-ttu-id="fa694-116">受害者研究 (Victimology)，亦即在業界和地理區域方面的盛行情況，可協助您判斷 Azure 資源是否有風險</span><span class="sxs-lookup"><span data-stu-id="fa694-116">Victimology, which is the industry and geographic prevalence to assist you in determining if your Azure resources are at risk</span></span>
* <span data-ttu-id="fa694-117">緩和與修復資訊</span><span class="sxs-lookup"><span data-stu-id="fa694-117">Mitigation and remediation information</span></span>

> [!NOTE]
> <span data-ttu-id="fa694-118">任何特定報告中所含的資訊數量各有不同；詳細程度視惡意程式碼的活動和盛行情況而定。</span><span class="sxs-lookup"><span data-stu-id="fa694-118">The amount of information in any particular report will vary; the level of detail is based on the malware’s activity and prevalence.</span></span>
>
>

<span data-ttu-id="fa694-119">資訊安全中心有三種威脅報告，不同攻擊會提供不同的報告。</span><span class="sxs-lookup"><span data-stu-id="fa694-119">Security Center has three types of threat reports, which can vary according to the attack.</span></span> <span data-ttu-id="fa694-120">所提供的報告如下︰</span><span class="sxs-lookup"><span data-stu-id="fa694-120">The reports available are:</span></span>

* <span data-ttu-id="fa694-121">**群組活動報告**︰提供攻擊者、其目標和策略的深入探討。</span><span class="sxs-lookup"><span data-stu-id="fa694-121">**Activity Group Report**: provides deep dives into attackers, their objectives and tactics.</span></span>
* <span data-ttu-id="fa694-122">**活動報告**︰著重說明特定攻擊活動的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fa694-122">**Campaign Report**: focuses on details of specific attack campaigns.</span></span>
* <span data-ttu-id="fa694-123">**威脅摘要報告**︰涵蓋先前兩種報告的所有項目。</span><span class="sxs-lookup"><span data-stu-id="fa694-123">**Threat Summary Report**: covers all of the items in the previous two reports.</span></span>

<span data-ttu-id="fa694-124">這種類型的資訊在[事件回應](security-center-incident-response.md)程序期間非常有用，因為該期間會持續進行調查，以了解攻擊來源、攻擊者的動機，以及日後該如何緩和此問題。</span><span class="sxs-lookup"><span data-stu-id="fa694-124">This type of information is very useful during the [incident response](security-center-incident-response.md) process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

## <a name="how-to-access-the-threat-intelligence-report"></a><span data-ttu-id="fa694-125">如何存取威脅情報報告？</span><span class="sxs-lookup"><span data-stu-id="fa694-125">How to access the threat intelligence report?</span></span>
<span data-ttu-id="fa694-126">您可以查看 [安全性警示]  圖格來檢視目前的警示。</span><span class="sxs-lookup"><span data-stu-id="fa694-126">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="fa694-127">開啟 Azure 入口網站並遵循下列步驟來查看有關每個警示的更多詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="fa694-127">Open the Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="fa694-128">您會在「資訊安全中心」的儀表板看到 [安全性警示]  圖格。</span><span class="sxs-lookup"><span data-stu-id="fa694-128">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>
2. <span data-ttu-id="fa694-129">按一下圖格便可開啟 [安全性警示] 刀鋒視窗，其中包含有關警示的更多詳細資料，按一下您想了解的安全性警示即可取得更多相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fa694-129">Click the tile to open the **Security alerts** blade that contains more details about the alerts and click in the security alert that you want to obtain more information about.</span></span>

    ![安全性警示](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. <span data-ttu-id="fa694-131">在此案例中，[已執行的可疑處理程序] 刀鋒視窗會顯示警示的詳細資料，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="fa694-131">In this case the **Suspicious process executed** blade shows the details about the alert as shown in the figure below:</span></span>

    ![安全性警示詳細資料](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. <span data-ttu-id="fa694-133">根據警示類型而定，針對每個安全性警示所提供的資訊數量會有所不同。</span><span class="sxs-lookup"><span data-stu-id="fa694-133">The amount of information available for each security alert will vary according to the type of alert.</span></span> <span data-ttu-id="fa694-134">[報告] 欄位中有威脅情報報告的連結。</span><span class="sxs-lookup"><span data-stu-id="fa694-134">In the **REPORTS** field you have a link to the threat intelligence report.</span></span> <span data-ttu-id="fa694-135">按一下連結，便會出現另一個含有 PDF 檔案的瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="fa694-135">Click on it and another browser window will appear with PDF file.</span></span>

   ![儲存體選擇](./media/security-center-threat-report/security-center-threat-report-fig3.png)

<span data-ttu-id="fa694-137">您可以從這裡下載此報告的 PDF，深入了解偵測到的安全性問題，並根據所提供的資訊採取動作。</span><span class="sxs-lookup"><span data-stu-id="fa694-137">From here you can download the PDF for this report and read more about the security issue that was detected and take actions based on the information provided.</span></span>

## <a name="see-also"></a><span data-ttu-id="fa694-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fa694-138">See also</span></span>
<span data-ttu-id="fa694-139">在本文件中，您已了解 Azure 資訊安全中心威脅情報報告如何在安全性警示調查期間幫上忙。</span><span class="sxs-lookup"><span data-stu-id="fa694-139">In this document, you learned how Azure Security Center Threat Intelligent Reports can help during an investigation about security alerts.</span></span> <span data-ttu-id="fa694-140">若要深入了解「Azure 資訊安全中心」，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="fa694-140">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="fa694-141">[Azure 資訊安全中心常見問題集](security-center-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="fa694-141">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="fa694-142">尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="fa694-142">Find frequently asked questions about using the service.</span></span>
* [<span data-ttu-id="fa694-143">善用 Azure 資訊安全中心進行事件回應</span><span class="sxs-lookup"><span data-stu-id="fa694-143">Leveraging Azure Security Center for Incident Response</span></span>](security-center-incident-response.md)
* [<span data-ttu-id="fa694-144">Azure 資訊安全中心的偵測功能</span><span class="sxs-lookup"><span data-stu-id="fa694-144">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* <span data-ttu-id="fa694-145">[Azure 資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="fa694-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="fa694-146">了解如何規劃及了解採用 Azure 資訊安全中心的設計考量。</span><span class="sxs-lookup"><span data-stu-id="fa694-146">Learn how to plan and understand the design considerations to adopt Azure Security Center.</span></span>
* <span data-ttu-id="fa694-147">[管理及回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="fa694-147">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span> <span data-ttu-id="fa694-148">了解如何管理和回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="fa694-148">Learn how to manage and respond to security alerts.</span></span>
* [<span data-ttu-id="fa694-149">在 Azure 資訊安全中心處理安全性事件</span><span class="sxs-lookup"><span data-stu-id="fa694-149">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* <span data-ttu-id="fa694-150">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)。</span><span class="sxs-lookup"><span data-stu-id="fa694-150">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="fa694-151">尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="fa694-151">Find blog posts about Azure security and compliance.</span></span>
