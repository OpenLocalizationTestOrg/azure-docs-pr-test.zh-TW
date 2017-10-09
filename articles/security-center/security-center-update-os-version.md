---
title: "在 Azure 資訊安全中心 aaaUpdate 作業系統版本 |Microsoft 文件"
description: "本文章將示範如何 tooimplement hello Azure 資訊安全中心建議事項 * * 更新的 OS 版本 * *。"
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
ms.openlocfilehash: f3497d7266da40d3a965f9cb8e84392d2aaa28f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="fda5e-103">Azure 資訊安全中心的更新作業系統版本</span><span class="sxs-lookup"><span data-stu-id="fda5e-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="fda5e-104">中的虛擬機器 (Vm) 雲端服務，Azure 資訊安全中心會建議 hello 作業系統 (OS) 如果沒有可用的較新版本更新。</span><span class="sxs-lookup"><span data-stu-id="fda5e-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that hello operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="fda5e-105">只監視生產位置中執行的雲端服務 Web 角色和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="fda5e-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="fda5e-106">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="fda5e-106">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="fda5e-107">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="fda5e-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="fda5e-108">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="fda5e-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="fda5e-109">在 hello**建議**刀鋒視窗中，選取**更新的 OS 版本**。</span><span class="sxs-lookup"><span data-stu-id="fda5e-109">In hello **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="fda5e-110">![更新作業系統版本][1]</span><span class="sxs-lookup"><span data-stu-id="fda5e-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="fda5e-111">這會開啟刀鋒視窗中 hello**更新的 OS 版本**。</span><span class="sxs-lookup"><span data-stu-id="fda5e-111">This opens hello blade **Update OS version**.</span></span> <span data-ttu-id="fda5e-112">遵循此刀鋒視窗 tooupdate hello 作業系統版本中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="fda5e-112">Follow hello steps in this blade tooupdate hello OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="fda5e-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fda5e-113">See also</span></span>
<span data-ttu-id="fda5e-114">本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議 「 更新作業系統版本。 」</span><span class="sxs-lookup"><span data-stu-id="fda5e-114">This article showed you how tooimplement hello Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="fda5e-115">toolearn 深入了解雲端服務和雲端服務中，更新 hello OS 版本，請參閱：</span><span class="sxs-lookup"><span data-stu-id="fda5e-115">toolearn more about cloud services and updating hello OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="fda5e-116">雲端服務概觀</span><span class="sxs-lookup"><span data-stu-id="fda5e-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="fda5e-117">如何 tooupdate 雲端服務</span><span class="sxs-lookup"><span data-stu-id="fda5e-117">How tooupdate a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="fda5e-118">如何 tooConfigure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="fda5e-118">How tooConfigure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="fda5e-119">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="fda5e-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="fda5e-120">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="fda5e-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="fda5e-121">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="fda5e-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="fda5e-122">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="fda5e-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="fda5e-123">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="fda5e-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="fda5e-124">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="fda5e-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="fda5e-125">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="fda5e-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="fda5e-126">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。</span><span class="sxs-lookup"><span data-stu-id="fda5e-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-update-os-version/update-os-version.png
