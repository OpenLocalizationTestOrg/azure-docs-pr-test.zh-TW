---
title: "在 Azure 資訊安全中心 aaaHandling 安全性警示 |Microsoft 文件"
description: "這份文件可協助您 toouse Azure 資訊安全中心功能 toohandle 安全性事件。"
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
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="cb5ab-103">在 Azure 資訊安全中心處理安全性事件</span><span class="sxs-lookup"><span data-stu-id="cb5ab-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="cb5ab-104">分級和調查安全性警示可能會很費時甚至 hello 熟練安全性分析師和許多很難 tooeven 知道哪裡 toobegin。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-104">Triaging and investigating security alerts can be time consuming for even hello most skilled security analysts, and for many it is hard tooeven know where toobegin.</span></span> <span data-ttu-id="cb5ab-105">使用[分析](security-center-detection-capabilities.md)tooconnect hello 資訊之間相異[安全性警示](security-center-managing-and-responding-alerts.md)、 資訊安全中心可以提供攻擊行銷活動的單一檢視，和所有 hello 相關警示 – 您可以快速了解採用何種動作 hello 攻擊者，以及哪些資源受到影響。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-105">By using [analytics](security-center-detection-capabilities.md) tooconnect hello information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of hello related alerts – you can quickly understand what actions hello attacker took and what resources were impacted.</span></span>

<span data-ttu-id="cb5ab-106">本文將討論如何 toouse 安全性警示功能的資訊安全中心 tooassist 您處理安全性事件。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-106">This document discusses how toouse security alert capability in Security Center tooassist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="cb5ab-107">什麼是安全性事件？</span><span class="sxs-lookup"><span data-stu-id="cb5ab-107">What is a security incident?</span></span>
<span data-ttu-id="cb5ab-108">在資訊安全中心內，安全性事件是符合 [攻擊鏈](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) 模式之資源的所有警示彙總。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="cb5ab-109">事件會出現在 hello[安全性警示](security-center-managing-and-responding-alerts.md)磚和刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-109">Incidents appear in hello [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="cb5ab-110">事件會顯示 hello 相關警示清單，可讓您 tooobtain 每次出現的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-110">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="cb5ab-111">管理安全性事件</span><span class="sxs-lookup"><span data-stu-id="cb5ab-111">Managing security incidents</span></span>
<span data-ttu-id="cb5ab-112">您可以藉由查看 hello 安全性警示磚檢閱目前的安全性事件。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-112">You can review your current security incidents by looking at hello security alerts tile.</span></span> <span data-ttu-id="cb5ab-113">存取 hello Azure 入口網站，並遵循每個安全性事件的詳細的 toosee hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="cb5ab-113">Access hello Azure Portal and follow hello steps below toosee more details about each security incident:</span></span>

1. <span data-ttu-id="cb5ab-114">在 hello 資訊安全中心儀表板中，您會看到 hello**安全性警示**磚。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-114">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![資訊安全中心的 [安全性警示] 圖格](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="cb5ab-116">按一下此磚 tooexpand，如果安全性事件偵測到，它會出現在 hello 安全性警示圖形如下所示：</span><span class="sxs-lookup"><span data-stu-id="cb5ab-116">Click on this tile tooexpand it and if a security incident is detected, it will appear under hello security alerts graph as shown  below:</span></span>

    ![安全性事件](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="cb5ab-118">請注意 hello 安全性事件描述有不同的圖示比較 tooother 警示。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-118">Notice that hello security incident description has a different icon compared tooother alerts.</span></span> <span data-ttu-id="cb5ab-119">按一下以 tooview 更詳細說明有關此事件。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-119">Click on it tooview more details about this incident.</span></span>

    ![安全性事件](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="cb5ab-121">在 hello**事件**刀鋒視窗，您將查看更多的詳細說明關於此安全性事件，其中包括完整描述，其嚴重性 （即在此情況下高），其目前狀態 (在此情況下仍*主動*，這表示 hello 使用者尚未採取動作 tooit-作法是以滑鼠右鍵按一下在 hello hello 事件**安全性警示**刀鋒視窗)，hello 遭受攻擊的資源 (在此情況下*VM1*)，hello hello 事件的修復步驟，而且 hello 下方窗格中，您必須已包含在此事件中的 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-121">On hello **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies hello user hasn't taken an action tooit - this can be done by right clicking on hello incident in hello **Security alerts** blade), hello attacked resource (in this case *VM1*), hello remediation steps for hello incident, and in hello bottom pane you have hello alerts that were included in this incident.</span></span> <span data-ttu-id="cb5ab-122">如果您想 tooobtain 上每個警示的詳細資訊，直接按一下它和另一個刀鋒視窗上的開啟，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cb5ab-122">If you want tooobtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![安全性事件](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="cb5ab-124">在這個刀鋒視窗上的 hello 資訊而異相應 toohello 警示。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-124">hello information on this blade will vary according toohello alert.</span></span> <span data-ttu-id="cb5ab-125">讀取[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)如需有關如何 toomanage 這些警示。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-125">Read [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how toomanage these alerts.</span></span> <span data-ttu-id="cb5ab-126">關於這項功能的一些重要考量︰</span><span class="sxs-lookup"><span data-stu-id="cb5ab-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="cb5ab-127">新的篩選器可讓您 toocustomize 檢視 tooIncident，警示，或兩者。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-127">A new filter enables you toocustomize your view tooIncident only, Alerts only, or both.</span></span>
* <span data-ttu-id="cb5ab-128">相同的警示可以存在的事件 （如果適用），以及顯示為獨立警示 toobe 一部分的 hello。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-128">hello same alert can exist as part of an Incident (if applicable), as well as toobe visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="cb5ab-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cb5ab-129">See also</span></span>
<span data-ttu-id="cb5ab-130">在本文件中，您學會如何 toouse hello 資訊安全中心的安全性事件功能。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-130">In this document, you learned how toouse hello security incident capability in Security Center.</span></span> <span data-ttu-id="cb5ab-131">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="cb5ab-131">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="cb5ab-132">管理及回應 toosecurity Azure 資訊安全中心警示</span><span class="sxs-lookup"><span data-stu-id="cb5ab-132">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="cb5ab-133">Azure 資訊安全中心的偵測功能</span><span class="sxs-lookup"><span data-stu-id="cb5ab-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="cb5ab-134">Azure 資訊安全中心規劃和操作指南</span><span class="sxs-lookup"><span data-stu-id="cb5ab-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="cb5ab-135">管理及回應 toosecurity Azure 資訊安全中心警示</span><span class="sxs-lookup"><span data-stu-id="cb5ab-135">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="cb5ab-136">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="cb5ab-137">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="cb5ab-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
