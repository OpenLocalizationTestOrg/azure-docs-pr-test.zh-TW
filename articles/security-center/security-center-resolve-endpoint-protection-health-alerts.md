---
title: "解決 Azure 資訊安全中心的端點保護健全狀況警示 | Microsoft Docs"
description: "本文件說明如何實作 Azure 資訊安全中心建議的「解決端點保護健全狀況警示」。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 5e6b136d6bd3b11fb82126d104fd0cb149255118
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="d262f-103">解決 Azure 資訊安全中心的端點保護健全狀況警示</span><span class="sxs-lookup"><span data-stu-id="d262f-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="d262f-104">Azure 資訊安全中心建議您先解決偵測到的端點保護健全狀況警示。</span><span class="sxs-lookup"><span data-stu-id="d262f-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="d262f-105">資訊安全中心可讓您查看哪些虛擬機器 (VM) 發生端點保護失敗及失敗的數目。</span><span class="sxs-lookup"><span data-stu-id="d262f-105">Security Center enables you to see which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="d262f-106">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="d262f-106">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="d262f-107">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="d262f-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="d262f-108">實作建議</span><span class="sxs-lookup"><span data-stu-id="d262f-108">Implement the recommendation</span></span>
1. <span data-ttu-id="d262f-109">在 [建議] 刀鋒視窗中，選取 [解決端點保護健全狀況警示]。</span><span class="sxs-lookup"><span data-stu-id="d262f-109">In the **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="d262f-110">![解決端點保護健全狀況警示][1]</span><span class="sxs-lookup"><span data-stu-id="d262f-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="d262f-111">這樣會開啟 [端點保護失敗]  刀鋒視窗，其中列出失敗的 VM 和每部 VM 的失敗數目。</span><span class="sxs-lookup"><span data-stu-id="d262f-111">This opens the blade **Endpoint Protection failure** which lists VMs with failures and the number of failures for each VM.</span></span> <span data-ttu-id="d262f-112">從清單中選取 VM。</span><span class="sxs-lookup"><span data-stu-id="d262f-112">Select a VM from the list.</span></span>
   <span data-ttu-id="d262f-113">![Endpoint protection failure][2]</span><span class="sxs-lookup"><span data-stu-id="d262f-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="d262f-114">隨即開啟選取的 VM 的 [失敗清單]  刀鋒視窗，並顯示失敗的清單。</span><span class="sxs-lookup"><span data-stu-id="d262f-114">A **Failures List** blade opens for the selected VM, displaying a list of failures.</span></span> <span data-ttu-id="d262f-115">從清單中選取要深入了解的失敗。</span><span class="sxs-lookup"><span data-stu-id="d262f-115">Select a failure from the list to learn more.</span></span> <span data-ttu-id="d262f-116">便會開啟一個含有所選失敗相關資訊的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d262f-116">This opens a blade with information about the selected failure.</span></span>
   <span data-ttu-id="d262f-117">![Failures list][3]
    ![失敗事件][4]</span><span class="sxs-lookup"><span data-stu-id="d262f-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="d262f-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d262f-118">See also</span></span>
<span data-ttu-id="d262f-119">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="d262f-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="d262f-120">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md)--了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="d262f-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d262f-121">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md)-- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d262f-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d262f-122">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md)-- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="d262f-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="d262f-123">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md)-- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="d262f-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="d262f-124">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) -- 了解如何監視合作夥伴解決方案的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="d262f-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="d262f-125">[Azure 資訊安全中心常見問題集](security-center-faq.md)-- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="d262f-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="d262f-126">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-- 取得最新的 Azure 安全性新聞和資訊。</span><span class="sxs-lookup"><span data-stu-id="d262f-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
