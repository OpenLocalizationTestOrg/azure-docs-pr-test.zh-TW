---
title: "在 Azure 資訊安全中心啟用 VM 代理程式 | Microsoft Docs"
description: "本文件說明如何實作 Azure 資訊安全中心建議的「啟用 VM 代理程式」。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 337a7adfd93c76882a749685702bea6d1524c96a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="92b6b-103">在 Azure 資訊安全中心啟用 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="92b6b-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="92b6b-104">VM 代理程式必須安裝在虛擬機器 (VM) 上，才能 [啟用資料收集](security-center-enable-data-collection.md)。</span><span class="sxs-lookup"><span data-stu-id="92b6b-104">The VM Agent must be installed on virtual machines (VMs) in order to [enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="92b6b-105">Azure 資訊安全中心可讓您查看哪些 VM 需要 VM 代理程式，而且會建議您在那些 VM 上啟用 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="92b6b-105">Azure Security Center enables you to see which VMs require the VM Agent and will recommend that you enable the VM Agent on those VMs.</span></span>

<span data-ttu-id="92b6b-106">預設會為從 Azure Marketplace 部署的 VM 安裝「VM 代理程式」。</span><span class="sxs-lookup"><span data-stu-id="92b6b-106">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="92b6b-107">如需如何安裝 VM 代理程式的相關資訊，請參閱 [VM 代理程式和擴充功能 – 第 2 部分](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) 。</span><span class="sxs-lookup"><span data-stu-id="92b6b-107">The article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="92b6b-108">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="92b6b-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="92b6b-109">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="92b6b-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="92b6b-110">實作建議</span><span class="sxs-lookup"><span data-stu-id="92b6b-110">Implement the recommendation</span></span>
1. <span data-ttu-id="92b6b-111">在 [建議] 刀鋒視窗中，選取 [啟用 VM 代理程式]。</span><span class="sxs-lookup"><span data-stu-id="92b6b-111">In the **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="92b6b-112">![啟用 VM 代理程式][1]</span><span class="sxs-lookup"><span data-stu-id="92b6b-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="92b6b-113">這會開啟 [VM 代理程式遺失或沒有回應] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="92b6b-113">This opens the blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="92b6b-114">此刀鋒視窗會列出需要 VM 代理程式的 VM。</span><span class="sxs-lookup"><span data-stu-id="92b6b-114">This blade lists the VMs that require the VM Agent.</span></span> <span data-ttu-id="92b6b-115">依照刀鋒視窗中的指示安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="92b6b-115">Follow the instructions on the blade to install the VM agent.</span></span>
   <span data-ttu-id="92b6b-116">![VM 代理程式已遺失][2]</span><span class="sxs-lookup"><span data-stu-id="92b6b-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="92b6b-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="92b6b-117">See also</span></span>
<span data-ttu-id="92b6b-118">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="92b6b-118">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="92b6b-119">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md)--了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="92b6b-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="92b6b-120">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md)-- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="92b6b-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="92b6b-121">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md)-- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="92b6b-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="92b6b-122">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md)-- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="92b6b-122">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="92b6b-123">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) -- 了解如何監視合作夥伴解決方案的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="92b6b-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="92b6b-124">[Azure 資訊安全中心常見問題集](security-center-faq.md)-- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="92b6b-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="92b6b-125">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-- 取得最新的 Azure 安全性新聞和資訊。</span><span class="sxs-lookup"><span data-stu-id="92b6b-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
