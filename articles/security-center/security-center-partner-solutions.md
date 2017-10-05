---
title: "在 Azure 資訊安全中心管理合作夥伴解決方案 | Microsoft Docs"
description: "本文件逐步引導您使用 Azure 資訊安全中心，讓您監視與您的 Azure 訂用帳戶整合之合作夥伴解決方案的健康狀態，一目了然。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: 2ebb930e877c5027f4d7b0a316a7f5ebe84471b1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="30e72-103">使用 Azure 資訊安全中心監視合作夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="30e72-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="30e72-104">本文件逐步引導您在 Azure 資訊安全中心監視合作夥伴解決方案的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="30e72-104">This document walks you through how to monitor the health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="30e72-105">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="30e72-105">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="30e72-106">本文件不是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="30e72-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="30e72-107">監視合作夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="30e72-107">Monitoring partner solutions</span></span>
<span data-ttu-id="30e72-108">[資訊安全中心] 刀鋒視窗上的 [合作夥伴解決方案] 磚可讓您監視與您的 Azure 訂用帳戶整合之合作夥伴解決方案的健康狀態，一目了然。</span><span class="sxs-lookup"><span data-stu-id="30e72-108">The **Partner solutions** tile on the **Security Center** blade lets you monitor at a glance the health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![合作夥伴解決方案圖格][1]

<span data-ttu-id="30e72-110">[合作夥伴解決方案] 圖格會顯示已與您訂用帳戶整合的合作夥伴解決方案數目。</span><span class="sxs-lookup"><span data-stu-id="30e72-110">The **Partner solutions** tile displays the number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="30e72-111">如果沒有任何已整合的解決方案，此圖格就會顯示數字零。</span><span class="sxs-lookup"><span data-stu-id="30e72-111">If there are no solutions integrated, the tile displays the number zero.</span></span>

<span data-ttu-id="30e72-112">若要檢視合作夥伴解決方案的健康狀態：</span><span class="sxs-lookup"><span data-stu-id="30e72-112">To view the health of your partner solutions:</span></span>

1. <span data-ttu-id="30e72-113">選取 [合作夥伴解決方案]  圖格。</span><span class="sxs-lookup"><span data-stu-id="30e72-113">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="30e72-114">[合作夥伴解決方案] 刀鋒視窗隨即開啟，當中會顯示已連接到「資訊安全中心」的合作夥伴解決方案清單。</span><span class="sxs-lookup"><span data-stu-id="30e72-114">The **Partner solutions** blade opens displaying a list of your partner solutions connected to Security Center.</span></span>

   ![合作夥伴解決方案][3]

   <span data-ttu-id="30e72-116">合作夥伴解決方案的狀態可以是︰</span><span class="sxs-lookup"><span data-stu-id="30e72-116">The status of a partner solution can be:</span></span>

   * <span data-ttu-id="30e72-117">受保護 (綠色) - 沒有任何健康問題。</span><span class="sxs-lookup"><span data-stu-id="30e72-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="30e72-118">狀況不良 (紅色) - 有需要立即注意的健康狀態問題。</span><span class="sxs-lookup"><span data-stu-id="30e72-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="30e72-119">停止報告 (橘色) - 解決方案已停止報告其健康狀態。</span><span class="sxs-lookup"><span data-stu-id="30e72-119">Stopped reporting (orange) - the solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="30e72-120">未知保護狀態 (橘色) - 此時解決方案的健康狀態因為將新資源加入至現有解決方案的程序失敗，而呈現未知狀態</span><span class="sxs-lookup"><span data-stu-id="30e72-120">Unknown protection status (orange) - the health of the solution is unknown at this time due to a failed process of adding a new resource to the existing solution.</span></span>
   * <span data-ttu-id="30e72-121">未報告 (灰色) - 解決方案尚未報告任何狀態，如果解決方案最近連接且仍在部署中，則可能未報告解決方案的狀態。</span><span class="sxs-lookup"><span data-stu-id="30e72-121">Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="30e72-122">選取合作夥伴解決方案。</span><span class="sxs-lookup"><span data-stu-id="30e72-122">Select a partner solution.</span></span> <span data-ttu-id="30e72-123">在此範例中，我們將選取 [Qualys] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="30e72-123">In this example, lets select the **Qualys** solution.</span></span>  <span data-ttu-id="30e72-124">隨即開啟一個刀鋒視窗，其中顯示合作夥伴解決方案的狀態和解決方案相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="30e72-124">A blade opens showing you the status of the partner solution and the solution's associated resources.</span></span> <span data-ttu-id="30e72-125">選取 [解決方案主控台]  以開啟此解決方案的合作夥伴管理體驗。</span><span class="sxs-lookup"><span data-stu-id="30e72-125">Select **Solution console** to open the partner management experience for this solution.</span></span>

   ![合作夥伴解決方案詳細資料][4]
3. <span data-ttu-id="30e72-127">返回 [Qualys] 刀鋒視窗，然後選取 [連結 VM]。</span><span class="sxs-lookup"><span data-stu-id="30e72-127">Go back to the **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="30e72-128">[連結應用程式]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="30e72-128">The **Link Applications** blade opens.</span></span> <span data-ttu-id="30e72-129">您可以在這裡將資源連接到合作夥伴解決方案。</span><span class="sxs-lookup"><span data-stu-id="30e72-129">Here you can connect resources to the partner solution.</span></span>

   ![將資源連結至第三方解決方案][5]

## <a name="next-steps"></a><span data-ttu-id="30e72-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30e72-131">Next steps</span></span>
<span data-ttu-id="30e72-132">在本文件中，已向您介紹「資訊安全中心」的 [合作夥伴解決方案]  圖格。</span><span class="sxs-lookup"><span data-stu-id="30e72-132">In this document, you were introduced to the **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="30e72-133">如要深入了解資訊安全中心，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="30e72-133">To learn more about Security Center, see the following articles:</span></span>

* <span data-ttu-id="30e72-134">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) — 了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="30e72-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="30e72-135">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) — 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="30e72-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="30e72-136">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) — 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="30e72-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="30e72-137">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) — 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="30e72-137">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="30e72-138">[Azure 資訊安全中心常見問題集](security-center-faq.md) — 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="30e72-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="30e72-139">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 取得最新的 Azure 安全性新聞和資訊。</span><span class="sxs-lookup"><span data-stu-id="30e72-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
