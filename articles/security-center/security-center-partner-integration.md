---
title: "Azure 資訊安全中心中的夥伴整合 | Microsoft Docs"
description: "了解 Azure 資訊安全中心如何與夥伴整合，以提高您 Azure 資源的整體安全性。"
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
ms.openlocfilehash: 44beafeff5cbe58ac8ca37632879f6ffc2b67e53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="partner-integration-in-azure-security-center"></a><span data-ttu-id="249cd-103">Azure 資訊安全中心中的夥伴整合</span><span class="sxs-lookup"><span data-stu-id="249cd-103">Partner integration in Azure Security Center</span></span>

<span data-ttu-id="249cd-104">在本文中，我們將說明 Azure 資訊安全中心如何與夥伴整合，以協助您提高整體安全性。</span><span class="sxs-lookup"><span data-stu-id="249cd-104">In this article, we describe how Azure Security Center integrates with partners to help you enhance overall security.</span></span> <span data-ttu-id="249cd-105">資訊安全中心在 Azure 中提供整合體驗，並利用 Azure Marketplace 進行夥伴認證和計費。</span><span class="sxs-lookup"><span data-stu-id="249cd-105">Security Center offers an integrated experience in Azure, and takes advantage of the Azure Marketplace for partner certification and billing.</span></span>

> [!NOTE] 
> <span data-ttu-id="249cd-106">從 2017 年 6 月開始，資訊安全中心會使用 Microsoft Monitoring Agent 來收集和儲存資料。</span><span class="sxs-lookup"><span data-stu-id="249cd-106">As of June 2017, Security Center uses the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="249cd-107">如需詳細資訊，請參閱 [Azure 資訊安全中心平台移轉](security-center-platform-migration.md)。</span><span class="sxs-lookup"><span data-stu-id="249cd-107">For more information, see [Azure Security Center platform migration](security-center-platform-migration.md).</span></span> <span data-ttu-id="249cd-108">本文中的資訊說明轉換至 Microsoft Monitoring Agent 後的資訊安全中心功能。</span><span class="sxs-lookup"><span data-stu-id="249cd-108">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>

## <a name="why-deploy-partner-solutions-from-security-center"></a><span data-ttu-id="249cd-109">為什麼要從資訊安全中心部署夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="249cd-109">Why deploy partner solutions from Security Center</span></span>

<span data-ttu-id="249cd-110">運用資訊安全中心中的夥伴整合有四個主要原因：</span><span class="sxs-lookup"><span data-stu-id="249cd-110">Four main reasons to leverage partner integration in Security Center are:</span></span>

- <span data-ttu-id="249cd-111">**部署方式簡單**。</span><span class="sxs-lookup"><span data-stu-id="249cd-111">**Ease of deployment**.</span></span> <span data-ttu-id="249cd-112">依照資訊安全中心的建議來部署夥伴解決方案更加容易。</span><span class="sxs-lookup"><span data-stu-id="249cd-112">Deploying a partner solution by following the Security Center recommendation is much easier.</span></span> <span data-ttu-id="249cd-113">使用預設的安裝和網路拓撲，可以全面自動化部署程序。</span><span class="sxs-lookup"><span data-stu-id="249cd-113">The deployment process can be fully automated by using a default setup and network topology.</span></span> <span data-ttu-id="249cd-114">或者，客戶可以選擇半自動的選項以取得更多彈性和自訂。</span><span class="sxs-lookup"><span data-stu-id="249cd-114">Alternatively, customers can choose a semi-automated option for more flexibility and customization.</span></span>
- <span data-ttu-id="249cd-115">**整合偵測**。</span><span class="sxs-lookup"><span data-stu-id="249cd-115">**Integrated detections**.</span></span> <span data-ttu-id="249cd-116">來自夥伴解決方案的安全性事件會自動收集、彙總以及顯示為資訊安全中心警示和事件的一部分。</span><span class="sxs-lookup"><span data-stu-id="249cd-116">Security events from partner solutions are automatically collected, aggregated, and displayed as part of Security Center alerts and incidents.</span></span> <span data-ttu-id="249cd-117">這些事件也會與來自其他來源的偵測整合，以提供進階的威脅偵測功能。</span><span class="sxs-lookup"><span data-stu-id="249cd-117">These events also are fused with detections from other sources to provide advanced threat-detection capabilities.</span></span>
- <span data-ttu-id="249cd-118">**統一的健康情況監視與管理**。</span><span class="sxs-lookup"><span data-stu-id="249cd-118">**Unified health monitoring and management**.</span></span> <span data-ttu-id="249cd-119">客戶可使用整合式的健全狀況事件，一眼監視所有夥伴解決方案。</span><span class="sxs-lookup"><span data-stu-id="249cd-119">Customers can use integrated health events to monitor all partner solutions at a glance.</span></span> <span data-ttu-id="249cd-120">提供基本管理功能，而且可以讓您輕鬆使用夥伴解決方案存取進階設定。</span><span class="sxs-lookup"><span data-stu-id="249cd-120">Basic management is available, with easy access to advanced setup by using the partner solution.</span></span>
- <span data-ttu-id="249cd-121">**匯出至 SIEM**。</span><span class="sxs-lookup"><span data-stu-id="249cd-121">**Export to SIEM**.</span></span> <span data-ttu-id="249cd-122">客戶現在可以使用 Azure log integration (預覽)，以 Common Event Format (CEF) 格式將所有資訊安全中心與夥伴的警示匯出至內部部署 Security Information and Event Management (SIEM) 系統中。</span><span class="sxs-lookup"><span data-stu-id="249cd-122">Customers can export all Security Center and partner alerts in Common Event Format (CEF) to on-premises Security Information and Event Management (SIEM) systems by using Azure log integration (preview).</span></span>


## <a name="partners-that-integrate-with-security-center"></a><span data-ttu-id="249cd-123">與資訊安全中心整合的夥伴</span><span class="sxs-lookup"><span data-stu-id="249cd-123">Partners that integrate with Security Center</span></span>

<span data-ttu-id="249cd-124">資訊安全中心目前與下列這些解決方案整合︰</span><span class="sxs-lookup"><span data-stu-id="249cd-124">Currently, Security Center integrates with these solutions:</span></span>

- <span data-ttu-id="249cd-125">Endpoint protection ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html)、Symantec 以及 [適用於 Azure 雲端服務和虛擬機器的 Microsoft 反惡意程式碼軟體](https://docs.microsoft.com/azure/security/azure-security-antimalware))</span><span class="sxs-lookup"><span data-stu-id="249cd-125">Endpoint protection ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec, and [Microsoft Antimalware for Azure Cloud Services and Virtual Machines](https://docs.microsoft.com/azure/security/azure-security-antimalware))</span></span> 
- <span data-ttu-id="249cd-126">Web 應用程式防火牆 ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall)、[F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html)、[Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF)、[Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets)，以及 [Azure 應用程式閘道](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/))</span><span class="sxs-lookup"><span data-stu-id="249cd-126">Web application firewall ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets), and [Azure Application Gateway](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/))</span></span> 
- <span data-ttu-id="249cd-127">新一代防火牆 ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/)、[Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/)、[Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) 和 [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html))</span><span class="sxs-lookup"><span data-stu-id="249cd-127">Next-generation firewall ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2), and [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html))</span></span> 
- <span data-ttu-id="249cd-128">弱點評估 ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))</span><span class="sxs-lookup"><span data-stu-id="249cd-128">Vulnerability assessment ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))</span></span>  

<span data-ttu-id="249cd-129">資訊安全中心會隨時間擴展這些類別內夥伴的數目，並加入新的類別。</span><span class="sxs-lookup"><span data-stu-id="249cd-129">Over time, Security Center will expand the number of partners within these categories, and add new categories.</span></span> 

## <a name="deploy-a-partner-solution"></a><span data-ttu-id="249cd-130">部署夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="249cd-130">Deploy a partner solution</span></span>

<span data-ttu-id="249cd-131">根據您的 Azure 環境設定和您定義的安全性原則，資訊安全中心可能會建議您部署夥伴解決方案。</span><span class="sxs-lookup"><span data-stu-id="249cd-131">Based on the setup of your Azure environment and the security policy you defined, Security Center might recommend that you deploy a partner solution.</span></span> <span data-ttu-id="249cd-132">此資訊安全中心建議將引導您完成選取和安裝夥伴解決方案的程序。</span><span class="sxs-lookup"><span data-stu-id="249cd-132">The Security Center recommendation guides you through the process of selecting and installing a partner solution.</span></span> <span data-ttu-id="249cd-133">整體部署體驗可能會根據您使用的解決方案類型和夥伴而有所不同。</span><span class="sxs-lookup"><span data-stu-id="249cd-133">The overall deployment experience might vary, depending on the type of solution and partner you use.</span></span> <span data-ttu-id="249cd-134">如需詳細資訊，請參閱下列文章。</span><span class="sxs-lookup"><span data-stu-id="249cd-134">For more information, see the following articles:</span></span>

- [<span data-ttu-id="249cd-135">安裝端點保護</span><span class="sxs-lookup"><span data-stu-id="249cd-135">Install endpoint protection</span></span>](security-center-install-endpoint-protection.md)
- [<span data-ttu-id="249cd-136">新增 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="249cd-136">Add a web application firewall</span></span>](security-center-add-web-application-firewall.md)
- [<span data-ttu-id="249cd-137">新增新一代防火牆</span><span class="sxs-lookup"><span data-stu-id="249cd-137">Add a next-generation firewall</span></span>](security-center-add-next-generation-firewall.md)
- [<span data-ttu-id="249cd-138">未安裝弱點評估</span><span class="sxs-lookup"><span data-stu-id="249cd-138">Vulnerability assessment not installed</span></span>](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a><span data-ttu-id="249cd-139">管理夥伴解決方案</span><span class="sxs-lookup"><span data-stu-id="249cd-139">Manage partner solutions</span></span>

<span data-ttu-id="249cd-140">在部署後，若要檢視解決方案的健康情況相關資訊並執行基本管理工作，請在 [資訊安全中心] 刀鋒視窗中，選取 [夥伴解決方案] 選項。</span><span class="sxs-lookup"><span data-stu-id="249cd-140">After deployment, to view information about the health of the solution and perform basic management tasks, on the **Security Center** blade, select the **Partner solutions** option.</span></span> <span data-ttu-id="249cd-141">如需管理資訊安全中心中合作夥伴解決方案的相關資訊，請參閱[透過 Azure 資訊安全中心監視夥伴解決方案](security-center-partner-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="249cd-141">For more information about managing partner solutions in Security Center, see [Monitor partner solutions with Azure Security Center](security-center-partner-solutions.md).</span></span>

![夥伴整合](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> <span data-ttu-id="249cd-143">Symantec Endpoint Protection 支援僅限於探索。</span><span class="sxs-lookup"><span data-stu-id="249cd-143">Symantec endpoint protection support is limited to discovery.</span></span> <span data-ttu-id="249cd-144">無法使用健康情況警示。</span><span class="sxs-lookup"><span data-stu-id="249cd-144">No health alerts are available.</span></span>
>

## <a name="see-also"></a><span data-ttu-id="249cd-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="249cd-145">See also</span></span>

<span data-ttu-id="249cd-146">在本文中，您已了解如何在 Azure 資訊安全中心中整合夥伴解決方案。</span><span class="sxs-lookup"><span data-stu-id="249cd-146">In this article, you learned how to integrate partner solutions in Azure Security Center.</span></span> <span data-ttu-id="249cd-147">如要深入了解資訊安全中心，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="249cd-147">To learn more about Security Center, see the following articles:</span></span>

* [<span data-ttu-id="249cd-148">資訊安全中心規劃和操作指南</span><span class="sxs-lookup"><span data-stu-id="249cd-148">Security Center planning and operations guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="249cd-149">在資訊安全中心管理和回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="249cd-149">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="249cd-150">資訊安全中心不同類型的安全性警示</span><span class="sxs-lookup"><span data-stu-id="249cd-150">Security alerts by type in Security Center</span></span>](security-center-alerts-type.md)
* <span data-ttu-id="249cd-151">[資訊安全中心的安全性健康情況監視](security-center-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="249cd-151">[Security health monitoring in Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="249cd-152">了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="249cd-152">Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="249cd-153">[使用資訊安全中心監視夥伴解決方案](security-center-partner-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="249cd-153">[Monitoring partner solutions with Security Center](security-center-partner-solutions.md).</span></span> <span data-ttu-id="249cd-154">了解如何監視合作夥伴解決方案的健全狀態。</span><span class="sxs-lookup"><span data-stu-id="249cd-154">Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="249cd-155">[Azure 資訊安全中心常見問題](security-center-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="249cd-155">[Azure Security Center FAQs](security-center-faq.md).</span></span> <span data-ttu-id="249cd-156">取得有關使用服務常見問題的答案。</span><span class="sxs-lookup"><span data-stu-id="249cd-156">Get answers to frequently asked questions about using the service.</span></span>
* <span data-ttu-id="249cd-157">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)。</span><span class="sxs-lookup"><span data-stu-id="249cd-157">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="249cd-158">尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="249cd-158">Find blog posts about Azure security and compliance.</span></span>
