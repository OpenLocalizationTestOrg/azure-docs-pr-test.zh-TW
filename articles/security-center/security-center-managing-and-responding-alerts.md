---
title: "在 Azure 資訊安全中心管理安全性警示 | Microsoft Docs"
description: "本文件可協助您使用「Azure 資訊安全中心」功能來管理及回應安全性警示。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: 56fcfbfdbe15749132ba6a27861142fd564063c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="managing-and-responding-to-security-alerts-in-azure-security-center"></a><span data-ttu-id="40b5f-103">管理及回應 Azure 資訊安全中心的安全性警示</span><span class="sxs-lookup"><span data-stu-id="40b5f-103">Managing and responding to security alerts in Azure Security Center</span></span>
<span data-ttu-id="40b5f-104">本文件可協助您使用 Azure 資訊安全中心來管理及回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="40b5f-104">This document helps you use Azure Security Center to manage and respond to security alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="40b5f-105">若要啟用進階偵測，請升級至 Azure 資訊安全中心標準。</span><span class="sxs-lookup"><span data-stu-id="40b5f-105">To enable advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="40b5f-106">提供 60 天的免費試用。</span><span class="sxs-lookup"><span data-stu-id="40b5f-106">A free 60-day trial is available.</span></span> <span data-ttu-id="40b5f-107">若要升級，請選取[安全性原則](security-center-policies.md)中的 [定價層]。</span><span class="sxs-lookup"><span data-stu-id="40b5f-107">To upgrade, select Pricing Tier in the [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="40b5f-108">若要深入了解，請參閱 [Azure 資訊安全中心價格](security-center-pricing.md)。</span><span class="sxs-lookup"><span data-stu-id="40b5f-108">See [Azure Security Center pricing](security-center-pricing.md) to learn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="40b5f-109">什麼是安全性警示：</span><span class="sxs-lookup"><span data-stu-id="40b5f-109">What are security alerts?</span></span>
<span data-ttu-id="40b5f-110">資訊安全中心會自動收集、分析及整合您 Azure 資源、網路和已連線的合作夥伴解決方案 (例如防火牆和端點保護解決方案) 的記錄檔資料，來偵測真正的威脅並減少誤判情形。</span><span class="sxs-lookup"><span data-stu-id="40b5f-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives.</span></span> <span data-ttu-id="40b5f-111">「資訊安全中心」會顯示優先安全性警示清單，以及需要您快速調查問題的資訊，和如何修復攻擊行為的建議。</span><span class="sxs-lookup"><span data-stu-id="40b5f-111">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="40b5f-112">如需資訊安全中心偵測功能運作方式的詳細資訊，請閱讀 [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="40b5f-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="40b5f-113">管理安全性警示</span><span class="sxs-lookup"><span data-stu-id="40b5f-113">Managing security alerts</span></span>
<span data-ttu-id="40b5f-114">您可以查看 [安全性警示]  圖格來檢視目前的警示。</span><span class="sxs-lookup"><span data-stu-id="40b5f-114">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="40b5f-115">開啟 Azure 入口網站並遵循下列步驟來查看有關每個警示的更多詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="40b5f-115">Open Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="40b5f-116">您會在「資訊安全中心」的儀表板看到 [安全性警示]  圖格。</span><span class="sxs-lookup"><span data-stu-id="40b5f-116">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![資訊安全中心的 [安全性警示] 圖格](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="40b5f-118">按一下圖格，開啟 [安全性警示]  刀鋒視窗，其中包括與警示相關的詳細資料，如下所示。</span><span class="sxs-lookup"><span data-stu-id="40b5f-118">Click the tile to open the **Security alerts** blade that contains more details about the alerts as shown below.</span></span>

   ![資訊安全中心的 [安全性警示] 刀鋒視窗](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="40b5f-120">這個刀鋒視窗的底部會顯示每個警示的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="40b5f-120">In the bottom part of this blade are the details for each alert.</span></span> <span data-ttu-id="40b5f-121">如要為警示排序，請按一下您要做為排序依據的的資料行。</span><span class="sxs-lookup"><span data-stu-id="40b5f-121">To sort, click the column that you want to sort by.</span></span> <span data-ttu-id="40b5f-122">下列為每個資料行的定義：</span><span class="sxs-lookup"><span data-stu-id="40b5f-122">The definition for each column is given below:</span></span>

* <span data-ttu-id="40b5f-123">**描述**：警示的簡短說明。</span><span class="sxs-lookup"><span data-stu-id="40b5f-123">**Description**: A brief explanation of the alert.</span></span>
* <span data-ttu-id="40b5f-124">**計數**：在特定一天偵測到這個特定類型的所有警示清單。</span><span class="sxs-lookup"><span data-stu-id="40b5f-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="40b5f-125">**偵測者**：負責觸發警示的服務。</span><span class="sxs-lookup"><span data-stu-id="40b5f-125">**Detected by**: The service that was responsible for triggering the alert.</span></span>
* <span data-ttu-id="40b5f-126">**日期**：事件發生的日期。</span><span class="sxs-lookup"><span data-stu-id="40b5f-126">**Date**: The date that the event occurred.</span></span>
* <span data-ttu-id="40b5f-127">**狀態**：該警示目前的狀態。</span><span class="sxs-lookup"><span data-stu-id="40b5f-127">**State**: The current state for that alert.</span></span> <span data-ttu-id="40b5f-128">狀態分為兩種：</span><span class="sxs-lookup"><span data-stu-id="40b5f-128">There are two types of states:</span></span>
  * <span data-ttu-id="40b5f-129">**使用中**：已偵測到安全性警示。</span><span class="sxs-lookup"><span data-stu-id="40b5f-129">**Active**: The security alert has been detected.</span></span>
* <span data-ttu-id="40b5f-130">**嚴重性**：嚴重性層級，分為高、中或低。</span><span class="sxs-lookup"><span data-stu-id="40b5f-130">**Severity**: The severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="40b5f-131">篩選警示</span><span class="sxs-lookup"><span data-stu-id="40b5f-131">Filtering alerts</span></span>
<span data-ttu-id="40b5f-132">您可以根據日期、狀態及嚴重性來篩選警示。</span><span class="sxs-lookup"><span data-stu-id="40b5f-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="40b5f-133">如果您需要縮小顯示的安全性警示檢視範圍，篩選警示會相當有用。</span><span class="sxs-lookup"><span data-stu-id="40b5f-133">Filtering alerts can be useful for scenarios where you need to narrow the scope of security alerts show.</span></span> <span data-ttu-id="40b5f-134">例如，您可能想確認在過去 24 小時發生的安全性警示，因為您正在調查系統中可能的入侵行動。</span><span class="sxs-lookup"><span data-stu-id="40b5f-134">For example, you might you want to address security alerts that occurred in the last 24 hours because you are investigating a potential breach in the system.</span></span>

1. <span data-ttu-id="40b5f-135">按一下 [安全性警示] 刀鋒視窗上的 [篩選]。</span><span class="sxs-lookup"><span data-stu-id="40b5f-135">Click **Filter** on the **Security Alerts** blade.</span></span> <span data-ttu-id="40b5f-136">即會開啟 [篩選]  刀鋒視窗，您可以選取想要查看的日期、狀態和嚴重性值。</span><span class="sxs-lookup"><span data-stu-id="40b5f-136">The **Filter** blade opens and you select the date, state, and severity values you wish to see.</span></span>

    ![篩選資訊安全中心的警示](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-to-security-alerts"></a><span data-ttu-id="40b5f-138">回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="40b5f-138">Respond to security alerts</span></span>
<span data-ttu-id="40b5f-139">選取一個安全性警示以深入了解觸發警示的事件；如果發現項目，您需要進行一些步驟來阻止攻擊。</span><span class="sxs-lookup"><span data-stu-id="40b5f-139">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="40b5f-140">安全性警示會依類型及日期區分。</span><span class="sxs-lookup"><span data-stu-id="40b5f-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="40b5f-141">按一下安全性警示會開啟刀鋒視窗，其中包括已分組的警示清單。</span><span class="sxs-lookup"><span data-stu-id="40b5f-141">Clicking a security alert will open a blade containing a list of the grouped alerts.</span></span>

![對於 Azure 資訊安全中心的安全性警示的回應](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="40b5f-143">在此案例中，所觸發的警示是關於可疑的遠端桌面通訊協定 (RDP) 活動。</span><span class="sxs-lookup"><span data-stu-id="40b5f-143">In this case, the alerts that were triggered refer to suspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="40b5f-144">第一個資料行顯示哪些資源遭到攻擊；第二個資料行顯示資源遭受攻擊的次數；第三個資料行顯示攻擊的時間；第四個資料行顯示警示的狀態；而第五個資料行顯示攻擊的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="40b5f-144">The first column shows which resources were attacked; the second shows how many times the resource was attacked; the third shows the time of the attack; the fourth shows state of the alert; and the fifth shows the severity of the attack.</span></span> <span data-ttu-id="40b5f-145">在檢閱這項資訊後，按一下遭到攻擊的資源，隨即會開啟新的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="40b5f-145">After reviewing this information, click the resource that was attacked and a new blade will open.</span></span>

![對於如何處理 Azure 資訊安全中心的安全性警示的建議](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="40b5f-147">在此刀鋒視窗的 [說明]  欄位中，您會找到關於這個事件的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="40b5f-147">In the **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="40b5f-148">這些額外的詳細資料可供深入了解什麼會觸發安全性警示、目標資源、來源 IP 位址 (若適用)，以及有關如何補救的建議。</span><span class="sxs-lookup"><span data-stu-id="40b5f-148">These additional details offer insight into what triggered the security alert, the target resource, when applicable the source IP address, and recommendations about how to remediate.</span></span>  <span data-ttu-id="40b5f-149">在某些情況下，來源 IP 位址會是空的 (不適用)，因為並非所有的 Windows 安全性事件記錄檔都包含 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="40b5f-149">In some instances, the source IP address will be empty (not available) because not all Windows security events logs include the IP address.</span></span>

<span data-ttu-id="40b5f-150">資訊安全中心會根據安全性警示，建議您不同的補救方法。</span><span class="sxs-lookup"><span data-stu-id="40b5f-150">The remediation suggested by Security Center will vary according to the security alert.</span></span> <span data-ttu-id="40b5f-151">在某些情況下，您可能必須使用其他的 Azure 功能來實作建議的補救方法。</span><span class="sxs-lookup"><span data-stu-id="40b5f-151">In some cases, you may have to use other Azure capabilities to implement the recommended remediation.</span></span> <span data-ttu-id="40b5f-152">例如，這個攻擊的補救方法是使用[網路 ACL](../virtual-network/virtual-networks-acl.md) 或[網路安全性群組](../virtual-network/virtual-networks-nsg.md)規則，將產生此攻擊的 IP 位址列入封鎖清單。</span><span class="sxs-lookup"><span data-stu-id="40b5f-152">For example, the remediation for this attack is to blacklist the IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="40b5f-153">如需不同警示類型的詳細資訊，請閱讀 [Azure 資訊安全中心不同類型的安全性警示](security-center-alerts-type.md)。</span><span class="sxs-lookup"><span data-stu-id="40b5f-153">For more information on the different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="40b5f-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="40b5f-154">See also</span></span>
<span data-ttu-id="40b5f-155">在本文件中，您了解到如何在資訊安全中心設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="40b5f-155">In this document, you learned how to configure security policies in Security Center.</span></span> <span data-ttu-id="40b5f-156">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="40b5f-156">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="40b5f-157">在 Azure 資訊安全中心處理安全性事件</span><span class="sxs-lookup"><span data-stu-id="40b5f-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="40b5f-158">Azure 資訊安全中心的偵測功能</span><span class="sxs-lookup"><span data-stu-id="40b5f-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="40b5f-159">Azure 資訊安全中心規劃和操作指南</span><span class="sxs-lookup"><span data-stu-id="40b5f-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="40b5f-160">[Azure 資訊安全中心常見問題集](security-center-faq.md) – 尋找使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="40b5f-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="40b5f-161">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="40b5f-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
