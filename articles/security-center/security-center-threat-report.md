---
title: "資訊安全中心 threat intelligence 報表 aaaAzure |Microsoft 文件"
description: "這份文件可協助您 toouse Azure 安全性中心威脅智慧型報告期間調查 toofind 有關安全性警示的詳細資訊。"
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
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a><span data-ttu-id="61fd9-103">Azure 資訊安全中心威脅情報報告</span><span class="sxs-lookup"><span data-stu-id="61fd9-103">Azure Security Center Threat Intelligence Report</span></span>
<span data-ttu-id="61fd9-104">本文件說明 Azure 資訊安全中心威脅情報報告可如何協助您深入了解產生安全性警示的威脅。</span><span class="sxs-lookup"><span data-stu-id="61fd9-104">This document explains how Azure Security Center Threat Intelligent Reports can help you learn more about a threat that generated a security alert.</span></span>

## <a name="what-is-a-threat-intelligence-report"></a><span data-ttu-id="61fd9-105">何謂威脅情報報告？</span><span class="sxs-lookup"><span data-stu-id="61fd9-105">What is a threat intelligence report?</span></span>
<span data-ttu-id="61fd9-106">資訊安全中心威脅偵測的運作方式是監視從您的 Azure 資源、 hello 網路和連線的交易夥伴方案的安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="61fd9-106">Security Center threat detection works by monitoring security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="61fd9-107">它會分析這項資訊通常相互關聯多個來源，tooidentify 威脅的資訊。</span><span class="sxs-lookup"><span data-stu-id="61fd9-107">It analyzes this information, often correlating information from multiple sources, tooidentify threats.</span></span> <span data-ttu-id="61fd9-108">此程序屬於 hello 資訊安全中心[偵測功能](security-center-detection-capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="61fd9-108">This process is part of hello Security Center [detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="61fd9-109">當資訊安全中心識別到威脅時，便會觸發[安全性警示](security-center-managing-and-responding-alerts.md)，其內含關於特定事件的詳細資訊，包括修復方面的建議。</span><span class="sxs-lookup"><span data-stu-id="61fd9-109">When Security Center identifies a threat, it will trigger a [security alert](security-center-managing-and-responding-alerts.md), which contains detailed information regarding a particular event, including suggestions for remediation.</span></span> <span data-ttu-id="61fd9-110">tooassist 事件回應小組調查並補救威脅，資訊安全中心包含威脅情報包含報表的 hello 威脅所偵測到，包括下列資訊的相關資訊:</span><span class="sxs-lookup"><span data-stu-id="61fd9-110">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected, including information such as the:</span></span>

* <span data-ttu-id="61fd9-111">攻擊者的身分識別或關聯 (如果有提供這項資訊)</span><span class="sxs-lookup"><span data-stu-id="61fd9-111">Attacker’s identity or associations (if this information is available)</span></span>
* <span data-ttu-id="61fd9-112">攻擊者的目標</span><span class="sxs-lookup"><span data-stu-id="61fd9-112">Attackers’ objectives</span></span>
* <span data-ttu-id="61fd9-113">目前和過往的攻擊活動 (如果有提供這項資訊)</span><span class="sxs-lookup"><span data-stu-id="61fd9-113">Current and historical attack campaigns (if this information is available)</span></span>
* <span data-ttu-id="61fd9-114">攻擊者的策略、工具和程序</span><span class="sxs-lookup"><span data-stu-id="61fd9-114">Attackers’ tactics, tools and procedures</span></span>
* <span data-ttu-id="61fd9-115">關聯的入侵指標 (IoC)，例如 URL 和檔案雜湊</span><span class="sxs-lookup"><span data-stu-id="61fd9-115">Associated indicators of compromise (IoC) such as URLs and file hashes</span></span>
* <span data-ttu-id="61fd9-116">Victimology，也就是 hello 產業和地理普遍性 tooassist 您在判斷您的 Azure 資源有風險</span><span class="sxs-lookup"><span data-stu-id="61fd9-116">Victimology, which is hello industry and geographic prevalence tooassist you in determining if your Azure resources are at risk</span></span>
* <span data-ttu-id="61fd9-117">緩和與修復資訊</span><span class="sxs-lookup"><span data-stu-id="61fd9-117">Mitigation and remediation information</span></span>

> [!NOTE]
> <span data-ttu-id="61fd9-118">hello 任何特定的報表中的資訊數量而異。hello 層級的詳細資料根據 hello 惡意程式碼的活動和普遍性而定。</span><span class="sxs-lookup"><span data-stu-id="61fd9-118">hello amount of information in any particular report will vary; hello level of detail is based on hello malware’s activity and prevalence.</span></span>
>
>

<span data-ttu-id="61fd9-119">資訊安全中心有三種類型的威脅的報表，所以可能會相應 toohello 攻擊。</span><span class="sxs-lookup"><span data-stu-id="61fd9-119">Security Center has three types of threat reports, which can vary according toohello attack.</span></span> <span data-ttu-id="61fd9-120">可用的 hello 報告為：</span><span class="sxs-lookup"><span data-stu-id="61fd9-120">hello reports available are:</span></span>

* <span data-ttu-id="61fd9-121">**群組活動報告**︰提供攻擊者、其目標和策略的深入探討。</span><span class="sxs-lookup"><span data-stu-id="61fd9-121">**Activity Group Report**: provides deep dives into attackers, their objectives and tactics.</span></span>
* <span data-ttu-id="61fd9-122">**活動報告**︰著重說明特定攻擊活動的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="61fd9-122">**Campaign Report**: focuses on details of specific attack campaigns.</span></span>
* <span data-ttu-id="61fd9-123">**威脅 [摘要] 報表**： 涵蓋所有 hello hello 先前的兩個報表中的項目。</span><span class="sxs-lookup"><span data-stu-id="61fd9-123">**Threat Summary Report**: covers all of hello items in hello previous two reports.</span></span>

<span data-ttu-id="61fd9-124">這種類型的資訊會很有幫助期間 hello[事件回應](security-center-incident-response.md)處理序中，沒有 hello 攻擊、 hello 攻擊者的動機，以及正在進行調查 toounderstand hello 來源 toodo toomitigate 這繼續進行後續步驟發生問題。</span><span class="sxs-lookup"><span data-stu-id="61fd9-124">This type of information is very useful during hello [incident response](security-center-incident-response.md) process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

## <a name="how-tooaccess-hello-threat-intelligence-report"></a><span data-ttu-id="61fd9-125">如何 tooaccess hello threat intelligence 報表嗎？</span><span class="sxs-lookup"><span data-stu-id="61fd9-125">How tooaccess hello threat intelligence report?</span></span>
<span data-ttu-id="61fd9-126">您可以檢閱您目前的警示，藉由查看 hello**安全性警示**磚。</span><span class="sxs-lookup"><span data-stu-id="61fd9-126">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="61fd9-127">開啟 hello Azure 入口網站，並遵循以下 toosee hello 步驟有關每種警示的更多詳細資料：</span><span class="sxs-lookup"><span data-stu-id="61fd9-127">Open hello Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="61fd9-128">在 hello 資訊安全中心儀表板中，您會看到 hello**安全性警示**磚。</span><span class="sxs-lookup"><span data-stu-id="61fd9-128">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>
2. <span data-ttu-id="61fd9-129">按一下 hello 磚 tooopen hello**安全性警示**刀鋒視窗，其中包含 hello 警示的更多詳細資料，然後按一下您想 tooobtain hello 安全性警示中的詳細資訊的相關。</span><span class="sxs-lookup"><span data-stu-id="61fd9-129">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts and click in hello security alert that you want tooobtain more information about.</span></span>

    ![安全性警示](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. <span data-ttu-id="61fd9-131">在此情況下 hello**可疑的處理程序執行**刀鋒視窗會顯示 hello hello 圖所示的 hello 警示的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="61fd9-131">In this case hello **Suspicious process executed** blade shows hello details about hello alert as shown in hello figure below:</span></span>

    ![安全性警示詳細資料](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. <span data-ttu-id="61fd9-133">hello 可用於每個安全性警示的資訊數量而異相應 toohello 類型的警示。</span><span class="sxs-lookup"><span data-stu-id="61fd9-133">hello amount of information available for each security alert will vary according toohello type of alert.</span></span> <span data-ttu-id="61fd9-134">在 hello**報表**您有一個連結 toohello threat intelligence 報表的欄位。</span><span class="sxs-lookup"><span data-stu-id="61fd9-134">In hello **REPORTS** field you have a link toohello threat intelligence report.</span></span> <span data-ttu-id="61fd9-135">按一下連結，便會出現另一個含有 PDF 檔案的瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="61fd9-135">Click on it and another browser window will appear with PDF file.</span></span>

   ![儲存體選擇](./media/security-center-threat-report/security-center-threat-report-fig3.png)

<span data-ttu-id="61fd9-137">從這裡您可以下載的 hello 偵測到此報表和讀取 hello 安全性問題的 PDF，並根據所提供的 hello 資訊採取動作。</span><span class="sxs-lookup"><span data-stu-id="61fd9-137">From here you can download hello PDF for this report and read more about hello security issue that was detected and take actions based on hello information provided.</span></span>

## <a name="see-also"></a><span data-ttu-id="61fd9-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="61fd9-138">See also</span></span>
<span data-ttu-id="61fd9-139">在本文件中，您已了解 Azure 資訊安全中心威脅情報報告如何在安全性警示調查期間幫上忙。</span><span class="sxs-lookup"><span data-stu-id="61fd9-139">In this document, you learned how Azure Security Center Threat Intelligent Reports can help during an investigation about security alerts.</span></span> <span data-ttu-id="61fd9-140">toolearn 進一步了解 Azure 資訊安全中心，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="61fd9-140">toolearn more about Azure Security Center, see hello following:</span></span>

* <span data-ttu-id="61fd9-141">[Azure 資訊安全中心常見問題集](security-center-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="61fd9-141">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="61fd9-142">尋找有關使用 hello 服務常見問題。</span><span class="sxs-lookup"><span data-stu-id="61fd9-142">Find frequently asked questions about using hello service.</span></span>
* [<span data-ttu-id="61fd9-143">善用 Azure 資訊安全中心進行事件回應</span><span class="sxs-lookup"><span data-stu-id="61fd9-143">Leveraging Azure Security Center for Incident Response</span></span>](security-center-incident-response.md)
* [<span data-ttu-id="61fd9-144">Azure 資訊安全中心的偵測功能</span><span class="sxs-lookup"><span data-stu-id="61fd9-144">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* <span data-ttu-id="61fd9-145">[Azure 資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="61fd9-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="61fd9-146">深入了解如何 tooplan 並了解 hello 設計考量 tooadopt Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="61fd9-146">Learn how tooplan and understand hello design considerations tooadopt Azure Security Center.</span></span>
* <span data-ttu-id="61fd9-147">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="61fd9-147">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span> <span data-ttu-id="61fd9-148">深入了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="61fd9-148">Learn how toomanage and respond toosecurity alerts.</span></span>
* [<span data-ttu-id="61fd9-149">在 Azure 資訊安全中心處理安全性事件</span><span class="sxs-lookup"><span data-stu-id="61fd9-149">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* <span data-ttu-id="61fd9-150">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)。</span><span class="sxs-lookup"><span data-stu-id="61fd9-150">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="61fd9-151">尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="61fd9-151">Find blog posts about Azure security and compliance.</span></span>
