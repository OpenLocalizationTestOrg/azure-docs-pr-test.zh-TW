---
title: "在 Azure 資訊安全中心處理安全性警示 | Microsoft Docs"
description: "本文件可協助您使用「Azure 資訊安全中心」功能來處理安全性事件。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: a302f8cb2555eef469a24da2523fdd9b97cc5730
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="85b8e-103">在 Azure 資訊安全中心處理安全性事件</span><span class="sxs-lookup"><span data-stu-id="85b8e-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="85b8e-104">對安全性警示進行分級和調查是很耗時的工作，即使是最熟練的安全性分析師也是如此，而且對許多人來說，即使要知道從何著手都相當困難。</span><span class="sxs-lookup"><span data-stu-id="85b8e-104">Triaging and investigating security alerts can be time consuming for even the most skilled security analysts, and for many it is hard to even know where to begin.</span></span> <span data-ttu-id="85b8e-105">透過使用[分析](security-center-detection-capabilities.md)來連結不同[安全性警示](security-center-managing-and-responding-alerts.md)之間的資訊，資訊安全中心可以提供關於攻擊活動和所有相關警示的單一檢視，讓您快速了解攻擊者所採取的動作以及受到影響的資源。</span><span class="sxs-lookup"><span data-stu-id="85b8e-105">By using [analytics](security-center-detection-capabilities.md) to connect the information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of the related alerts – you can quickly understand what actions the attacker took and what resources were impacted.</span></span>

<span data-ttu-id="85b8e-106">本文件將討論如何使用資訊安全中心的安全性警示功能，協助您處理安全性事件。</span><span class="sxs-lookup"><span data-stu-id="85b8e-106">This document discusses how to use security alert capability in Security Center to assist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="85b8e-107">什麼是安全性事件？</span><span class="sxs-lookup"><span data-stu-id="85b8e-107">What is a security incident?</span></span>
<span data-ttu-id="85b8e-108">在資訊安全中心內，安全性事件是符合 [攻擊鏈](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) 模式之資源的所有警示彙總。</span><span class="sxs-lookup"><span data-stu-id="85b8e-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="85b8e-109">事件會出現在 [ [安全性警示](security-center-managing-and-responding-alerts.md) ] 圖格和刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="85b8e-109">Incidents appear in the [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="85b8e-110">事件會顯示相關警示的清單，以讓您取得所引發的每個警示的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="85b8e-110">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="85b8e-111">管理安全性事件</span><span class="sxs-lookup"><span data-stu-id="85b8e-111">Managing security incidents</span></span>
<span data-ttu-id="85b8e-112">您可以查看 [安全性警示] 圖格來檢閱目前的安全性事件。</span><span class="sxs-lookup"><span data-stu-id="85b8e-112">You can review your current security incidents by looking at the security alerts tile.</span></span> <span data-ttu-id="85b8e-113">存取 Azure 入口網站，然後依照下列步驟進行，以查看每個安全性事件的詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="85b8e-113">Access the Azure Portal and follow the steps below to see more details about each security incident:</span></span>

1. <span data-ttu-id="85b8e-114">您會在 [資訊安全中心] 儀表板看到 [安全性警示]  圖格。</span><span class="sxs-lookup"><span data-stu-id="85b8e-114">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![資訊安全中心的 [安全性警示] 圖格](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="85b8e-116">按一下此圖格來加以展開，如果偵測到安全性事件，它便會出現在安全性警示圖形下方，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85b8e-116">Click on this tile to expand it and if a security incident is detected, it will appear under the security alerts graph as shown  below:</span></span>

    ![安全性事件](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="85b8e-118">請注意，安全性事件描述具有不同於其他警示的圖示。</span><span class="sxs-lookup"><span data-stu-id="85b8e-118">Notice that the security incident description has a different icon compared to other alerts.</span></span> <span data-ttu-id="85b8e-119">按一下圖示即可檢視此事件的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="85b8e-119">Click on it to view more details about this incident.</span></span>

    ![安全性事件](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="85b8e-121">在 [事件] 刀鋒視窗中，您會看到此安全性事件的詳細資訊，其中包含事件的完整描述、嚴重性 (在本例中是 [高])、目前狀態 (在本例中仍為 [作用中]，這代表使用者尚未對其執行動作 - 在 [安全性警示] 刀鋒視窗中的事件上按一下右鍵即可執行)、受到攻擊的資源 (在本例中是 [VM1])、事件的修復步驟，而最下方的窗格則是此事件所包含的警示。</span><span class="sxs-lookup"><span data-stu-id="85b8e-121">On the **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies the user hasn't taken an action to it - this can be done by right clicking on the incident in the **Security alerts** blade), the attacked resource (in this case *VM1*), the remediation steps for the incident, and in the bottom pane you have the alerts that were included in this incident.</span></span> <span data-ttu-id="85b8e-122">如果您想要取得每個警示的詳細資訊，只要按一下警示便會開啟另一個刀鋒視窗，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85b8e-122">If you want to obtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![安全性事件](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="85b8e-124">此刀鋒視窗上的資訊視警示而異。</span><span class="sxs-lookup"><span data-stu-id="85b8e-124">The information on this blade will vary according to the alert.</span></span> <span data-ttu-id="85b8e-125">如需如何管理這些警示的詳細資訊，請閱讀 [管理及回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) 。</span><span class="sxs-lookup"><span data-stu-id="85b8e-125">Read [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how to manage these alerts.</span></span> <span data-ttu-id="85b8e-126">關於這項功能的一些重要考量︰</span><span class="sxs-lookup"><span data-stu-id="85b8e-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="85b8e-127">有新的篩選器可讓您將檢視自訂為 [僅事件] 和/或 [僅警示]。</span><span class="sxs-lookup"><span data-stu-id="85b8e-127">A new filter enables you to customize your view to Incident only, Alerts only, or both.</span></span>
* <span data-ttu-id="85b8e-128">相同的警示可以做為事件的一部分存在 (如果適用)，以及顯示為獨立警示。</span><span class="sxs-lookup"><span data-stu-id="85b8e-128">The same alert can exist as part of an Incident (if applicable), as well as to be visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="85b8e-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="85b8e-129">See also</span></span>
<span data-ttu-id="85b8e-130">在本文件中，您已了解如何使用資訊安全中心的安全性事件功能。</span><span class="sxs-lookup"><span data-stu-id="85b8e-130">In this document, you learned how to use the security incident capability in Security Center.</span></span> <span data-ttu-id="85b8e-131">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="85b8e-131">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="85b8e-132">管理及回應 Azure 資訊安全中心的安全性警示</span><span class="sxs-lookup"><span data-stu-id="85b8e-132">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="85b8e-133">Azure 資訊安全中心的偵測功能</span><span class="sxs-lookup"><span data-stu-id="85b8e-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="85b8e-134">Azure 資訊安全中心規劃和操作指南</span><span class="sxs-lookup"><span data-stu-id="85b8e-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="85b8e-135">管理及回應 Azure 資訊安全中心的安全性警示</span><span class="sxs-lookup"><span data-stu-id="85b8e-135">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="85b8e-136">[Azure 資訊安全中心常見問題集](security-center-faq.md)-- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="85b8e-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="85b8e-137">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="85b8e-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
