---
title: "aaaPartner 整合 Azure 資訊安全中心 |Microsoft 文件"
description: "深入了解 Azure 資訊安全中心如何與夥伴 tooenhance 整合您的 Azure 資源的整體安全性。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a><span data-ttu-id="1a611-103">Azure 資訊安全中心中的夥伴整合</span><span class="sxs-lookup"><span data-stu-id="1a611-103">Partner integration in Azure Security Center</span></span>

<span data-ttu-id="1a611-104">在本文中，我們說明如何與夥伴 toohelp 整合 Azure 資訊安全中心增強整體安全性。</span><span class="sxs-lookup"><span data-stu-id="1a611-104">In this article, we describe how Azure Security Center integrates with partners toohelp you enhance overall security.</span></span> <span data-ttu-id="1a611-105">資訊安全中心提供了整合式的體驗，在 Azure 中，並利用 hello Azure Marketplace 夥伴憑證和計費。</span><span class="sxs-lookup"><span data-stu-id="1a611-105">Security Center offers an integrated experience in Azure, and takes advantage of hello Azure Marketplace for partner certification and billing.</span></span>

> [!NOTE] 
> <span data-ttu-id="1a611-106">為準，年 6 月 2017年資訊安全中心會使用 hello Microsoft Monitoring Agent toocollect 和存放區資料。</span><span class="sxs-lookup"><span data-stu-id="1a611-106">As of June 2017, Security Center uses hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="1a611-107">如需詳細資訊，請參閱 [Azure 資訊安全中心平台移轉](security-center-platform-migration.md)。</span><span class="sxs-lookup"><span data-stu-id="1a611-107">For more information, see [Azure Security Center platform migration](security-center-platform-migration.md).</span></span> <span data-ttu-id="1a611-108">本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。</span><span class="sxs-lookup"><span data-stu-id="1a611-108">hello information in this article represents Security Center functionality after transition toohello Microsoft Monitoring Agent.</span></span>
>

## <a name="why-deploy-partner-solutions-from-security-center"></a><span data-ttu-id="1a611-109">為什麼要從資訊安全中心部署夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="1a611-109">Why deploy partner solutions from Security Center</span></span>

<span data-ttu-id="1a611-110">有四個主要原因 tooleverage 夥伴資訊安全中心整合：</span><span class="sxs-lookup"><span data-stu-id="1a611-110">Four main reasons tooleverage partner integration in Security Center are:</span></span>

- <span data-ttu-id="1a611-111">**部署方式簡單**。</span><span class="sxs-lookup"><span data-stu-id="1a611-111">**Ease of deployment**.</span></span> <span data-ttu-id="1a611-112">下列 hello 資訊安全中心建議部署協力廠商方案就能更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="1a611-112">Deploying a partner solution by following hello Security Center recommendation is much easier.</span></span> <span data-ttu-id="1a611-113">使用預設的安裝程式和網路拓撲，可以全面自動化 hello 部署程序。</span><span class="sxs-lookup"><span data-stu-id="1a611-113">hello deployment process can be fully automated by using a default setup and network topology.</span></span> <span data-ttu-id="1a611-114">或者，客戶可以選擇半自動的選項以取得更多彈性和自訂。</span><span class="sxs-lookup"><span data-stu-id="1a611-114">Alternatively, customers can choose a semi-automated option for more flexibility and customization.</span></span>
- <span data-ttu-id="1a611-115">**整合偵測**。</span><span class="sxs-lookup"><span data-stu-id="1a611-115">**Integrated detections**.</span></span> <span data-ttu-id="1a611-116">來自夥伴解決方案的安全性事件會自動收集、彙總以及顯示為資訊安全中心警示和事件的一部分。</span><span class="sxs-lookup"><span data-stu-id="1a611-116">Security events from partner solutions are automatically collected, aggregated, and displayed as part of Security Center alerts and incidents.</span></span> <span data-ttu-id="1a611-117">這些事件也被 fused 進階威脅偵測功能，其他來源 tooprovide 的偵測結果。</span><span class="sxs-lookup"><span data-stu-id="1a611-117">These events also are fused with detections from other sources tooprovide advanced threat-detection capabilities.</span></span>
- <span data-ttu-id="1a611-118">**統一的健康情況監視與管理**。</span><span class="sxs-lookup"><span data-stu-id="1a611-118">**Unified health monitoring and management**.</span></span> <span data-ttu-id="1a611-119">客戶可以使用整合式健全狀況事件 toomonitor 所有協力廠商解決方案一目了然。</span><span class="sxs-lookup"><span data-stu-id="1a611-119">Customers can use integrated health events toomonitor all partner solutions at a glance.</span></span> <span data-ttu-id="1a611-120">使用，讓您輕鬆存取 tooadvanced 安裝程式使用 hello 協力廠商解決方案的基本管理。</span><span class="sxs-lookup"><span data-stu-id="1a611-120">Basic management is available, with easy access tooadvanced setup by using hello partner solution.</span></span>
- <span data-ttu-id="1a611-121">**匯出 tooSIEM**。</span><span class="sxs-lookup"><span data-stu-id="1a611-121">**Export tooSIEM**.</span></span> <span data-ttu-id="1a611-122">客戶可以匯出所有的資訊安全中心，並且夥伴警示通用事件格式 (CEF) tooon 內部部署安全性資訊和事件管理 (SIEM) 系統使用 Azure 記錄檔整合 （預覽）。</span><span class="sxs-lookup"><span data-stu-id="1a611-122">Customers can export all Security Center and partner alerts in Common Event Format (CEF) tooon-premises Security Information and Event Management (SIEM) systems by using Azure log integration (preview).</span></span>


## <a name="partners-that-integrate-with-security-center"></a><span data-ttu-id="1a611-123">與資訊安全中心整合的夥伴</span><span class="sxs-lookup"><span data-stu-id="1a611-123">Partners that integrate with Security Center</span></span>

<span data-ttu-id="1a611-124">資訊安全中心目前與下列這些解決方案整合︰</span><span class="sxs-lookup"><span data-stu-id="1a611-124">Currently, Security Center integrates with these solutions:</span></span>

- <span data-ttu-id="1a611-125">Endpoint protection ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html)、Symantec 以及 [適用於 Azure 雲端服務和虛擬機器的 Microsoft 反惡意程式碼軟體](https://docs.microsoft.com/azure/security/azure-security-antimalware))</span><span class="sxs-lookup"><span data-stu-id="1a611-125">Endpoint protection ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec, and [Microsoft Antimalware for Azure Cloud Services and Virtual Machines](https://docs.microsoft.com/azure/security/azure-security-antimalware))</span></span> 
- <span data-ttu-id="1a611-126">Web 應用程式防火牆 ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall)、[F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html)、[Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF)、[Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets)，以及 [Azure 應用程式閘道](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/))</span><span class="sxs-lookup"><span data-stu-id="1a611-126">Web application firewall ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets), and [Azure Application Gateway](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/))</span></span> 
- <span data-ttu-id="1a611-127">新一代防火牆 ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/)、[Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/)、[Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) 和 [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html))</span><span class="sxs-lookup"><span data-stu-id="1a611-127">Next-generation firewall ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2), and [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html))</span></span> 
- <span data-ttu-id="1a611-128">弱點評估 ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))</span><span class="sxs-lookup"><span data-stu-id="1a611-128">Vulnerability assessment ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))</span></span>  

<span data-ttu-id="1a611-129">經過一段時間，將展開 hello 在這些分類中中的夥伴數目的資訊安全中心，並將其加入新的類別目錄中。</span><span class="sxs-lookup"><span data-stu-id="1a611-129">Over time, Security Center will expand hello number of partners within these categories, and add new categories.</span></span> 

## <a name="deploy-a-partner-solution"></a><span data-ttu-id="1a611-130">部署夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="1a611-130">Deploy a partner solution</span></span>

<span data-ttu-id="1a611-131">根據 hello Azure 環境的 hello 安全性原則所定義的設定資訊安全中心可能會建議您部署協力廠商解決方案。</span><span class="sxs-lookup"><span data-stu-id="1a611-131">Based on hello setup of your Azure environment and hello security policy you defined, Security Center might recommend that you deploy a partner solution.</span></span> <span data-ttu-id="1a611-132">hello 資訊安全中心建議會引導您完成選取並安裝協力廠商解決方案 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="1a611-132">hello Security Center recommendation guides you through hello process of selecting and installing a partner solution.</span></span> <span data-ttu-id="1a611-133">hello 整體部署經驗可能有所不同，hello 的方案和您使用協力廠商的型別。</span><span class="sxs-lookup"><span data-stu-id="1a611-133">hello overall deployment experience might vary, depending on hello type of solution and partner you use.</span></span> <span data-ttu-id="1a611-134">如需詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="1a611-134">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="1a611-135">安裝端點保護</span><span class="sxs-lookup"><span data-stu-id="1a611-135">Install endpoint protection</span></span>](security-center-install-endpoint-protection.md)
- [<span data-ttu-id="1a611-136">新增 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="1a611-136">Add a web application firewall</span></span>](security-center-add-web-application-firewall.md)
- [<span data-ttu-id="1a611-137">新增新一代防火牆</span><span class="sxs-lookup"><span data-stu-id="1a611-137">Add a next-generation firewall</span></span>](security-center-add-next-generation-firewall.md)
- [<span data-ttu-id="1a611-138">未安裝弱點評估</span><span class="sxs-lookup"><span data-stu-id="1a611-138">Vulnerability assessment not installed</span></span>](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a><span data-ttu-id="1a611-139">管理夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="1a611-139">Manage partner solutions</span></span>

<span data-ttu-id="1a611-140">部署之後，tooview 有關 hello hello 方案的健全狀況與資訊的基本管理工作，對 hello**資訊安全中心**刀鋒視窗中，選取 hello**合作夥伴解決方案**選項。</span><span class="sxs-lookup"><span data-stu-id="1a611-140">After deployment, tooview information about hello health of hello solution and perform basic management tasks, on hello **Security Center** blade, select hello **Partner solutions** option.</span></span> <span data-ttu-id="1a611-141">如需管理資訊安全中心中合作夥伴解決方案的相關資訊，請參閱[透過 Azure 資訊安全中心監視夥伴解決方案](security-center-partner-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="1a611-141">For more information about managing partner solutions in Security Center, see [Monitor partner solutions with Azure Security Center](security-center-partner-solutions.md).</span></span>

![夥伴整合](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> <span data-ttu-id="1a611-143">Symantec endpoint protection 支援是有限的 toodiscovery。</span><span class="sxs-lookup"><span data-stu-id="1a611-143">Symantec endpoint protection support is limited toodiscovery.</span></span> <span data-ttu-id="1a611-144">無法使用健康情況警示。</span><span class="sxs-lookup"><span data-stu-id="1a611-144">No health alerts are available.</span></span>
>

## <a name="see-also"></a><span data-ttu-id="1a611-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1a611-145">See also</span></span>

<span data-ttu-id="1a611-146">在本文中，您學會如何 toointegrate 合作夥伴 Azure 資訊安全中心中的解決方案。</span><span class="sxs-lookup"><span data-stu-id="1a611-146">In this article, you learned how toointegrate partner solutions in Azure Security Center.</span></span> <span data-ttu-id="1a611-147">toolearn 有關資訊安全中心的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="1a611-147">toolearn more about Security Center, see hello following articles:</span></span>

* [<span data-ttu-id="1a611-148">資訊安全中心規劃和操作指南</span><span class="sxs-lookup"><span data-stu-id="1a611-148">Security Center planning and operations guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="1a611-149">管理及回應 toosecurity 警示資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="1a611-149">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="1a611-150">資訊安全中心不同類型的安全性警示</span><span class="sxs-lookup"><span data-stu-id="1a611-150">Security alerts by type in Security Center</span></span>](security-center-alerts-type.md)
* <span data-ttu-id="1a611-151">[資訊安全中心的安全性健康情況監視](security-center-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="1a611-151">[Security health monitoring in Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="1a611-152">了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="1a611-152">Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="1a611-153">[使用資訊安全中心監視夥伴解決方案](security-center-partner-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="1a611-153">[Monitoring partner solutions with Security Center](security-center-partner-solutions.md).</span></span> <span data-ttu-id="1a611-154">了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="1a611-154">Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="1a611-155">[Azure 資訊安全中心常見問題](security-center-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="1a611-155">[Azure Security Center FAQs](security-center-faq.md).</span></span> <span data-ttu-id="1a611-156">取得使用 hello 服務的相關常見問題的解答 toofrequently。</span><span class="sxs-lookup"><span data-stu-id="1a611-156">Get answers toofrequently asked questions about using hello service.</span></span>
* <span data-ttu-id="1a611-157">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)。</span><span class="sxs-lookup"><span data-stu-id="1a611-157">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="1a611-158">尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="1a611-158">Find blog posts about Azure security and compliance.</span></span>
