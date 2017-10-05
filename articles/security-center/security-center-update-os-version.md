---
title: "Azure 資訊安全中心的更新作業系統版本 | Microsoft Docs"
description: "本文說明了如何實作 Azure 資訊安全中心建議的「更新作業系統版本」。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: aa372492-ecdb-4368-8fdd-d8ed31e216ee
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: ce0d178914907750e5da59f223a4b1e04b9bb6fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="ff81f-103">Azure 資訊安全中心的更新作業系統版本</span><span class="sxs-lookup"><span data-stu-id="ff81f-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="ff81f-104">對於雲端服務中的虛擬機器 (VM)，如果有更新的版本可用，則 Azure 資訊安全中心會建議更新作業系統 (OS)。</span><span class="sxs-lookup"><span data-stu-id="ff81f-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that the operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="ff81f-105">只監視生產位置中執行的雲端服務 Web 角色和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="ff81f-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="ff81f-106">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="ff81f-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="ff81f-107">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="ff81f-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="ff81f-108">實作建議</span><span class="sxs-lookup"><span data-stu-id="ff81f-108">Implement the recommendation</span></span>
1. <span data-ttu-id="ff81f-109">在 [建議] 刀鋒視窗中，選取 [更新作業系統版本]。</span><span class="sxs-lookup"><span data-stu-id="ff81f-109">In the **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="ff81f-110">![更新作業系統版本][1]</span><span class="sxs-lookup"><span data-stu-id="ff81f-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="ff81f-111">[更新作業系統版本] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="ff81f-111">This opens the blade **Update OS version**.</span></span> <span data-ttu-id="ff81f-112">遵循此刀鋒視窗中的步驟來更新作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="ff81f-112">Follow the steps in this blade to update the OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="ff81f-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ff81f-113">See also</span></span>
<span data-ttu-id="ff81f-114">本文說明了如何實作資訊安全中心建議的「更新作業系統版本」。</span><span class="sxs-lookup"><span data-stu-id="ff81f-114">This article showed you how to implement the Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="ff81f-115">若要深入了解雲端服務和更新雲端服務的作業系統版本，請參閱：</span><span class="sxs-lookup"><span data-stu-id="ff81f-115">To learn more about cloud services and updating the OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="ff81f-116">雲端服務概觀</span><span class="sxs-lookup"><span data-stu-id="ff81f-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="ff81f-117">如何更新雲端服務</span><span class="sxs-lookup"><span data-stu-id="ff81f-117">How to update a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="ff81f-118">如何設定雲端服務</span><span class="sxs-lookup"><span data-stu-id="ff81f-118">How to Configure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="ff81f-119">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="ff81f-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="ff81f-120">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) --了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="ff81f-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ff81f-121">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ff81f-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ff81f-122">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) -- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="ff81f-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="ff81f-123">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="ff81f-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="ff81f-124">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) -- 了解如何監視合作夥伴解決方案的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="ff81f-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="ff81f-125">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="ff81f-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ff81f-126">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 取得最新的 Azure 安全性新聞和資訊。</span><span class="sxs-lookup"><span data-stu-id="ff81f-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-update-os-version/update-os-version.png
