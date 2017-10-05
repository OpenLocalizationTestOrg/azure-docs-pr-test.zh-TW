---
title: "Azure App Service Environment 簡介"
description: "Azure App Service Environment 簡要概觀"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: e21c4c3e2c212d86a0dbe2211564c2e3a1acf819
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-app-service-environments"></a><span data-ttu-id="e16f5-103">App Service Environment 簡介</span><span class="sxs-lookup"><span data-stu-id="e16f5-103">Introduction to App Service environments</span></span> #
 
## <a name="overview"></a><span data-ttu-id="e16f5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e16f5-104">Overview</span></span> ##

<span data-ttu-id="e16f5-105">Azure App Service Environment 是 Azure App Service 的功能，可提供完全隔離和專用的環境，以便安全地大規模執行 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e16f5-105">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="e16f5-106">此功能可裝載 [Web 應用程式][webapps]、[行動應用程式][mobileapps]、[API 應用程式][APIapps]和[函數][Functions]。</span><span class="sxs-lookup"><span data-stu-id="e16f5-106">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIapps], and [functions][Functions].</span></span>

<span data-ttu-id="e16f5-107">App Service Environment (ASE) 適合需要下列項目的應用程式工作負載：</span><span class="sxs-lookup"><span data-stu-id="e16f5-107">App Service environments (ASEs) are appropriate for application workloads that require:</span></span>

- <span data-ttu-id="e16f5-108">非常高的延展性。</span><span class="sxs-lookup"><span data-stu-id="e16f5-108">Very high scale.</span></span>
- <span data-ttu-id="e16f5-109">隔離和安全的網路存取。</span><span class="sxs-lookup"><span data-stu-id="e16f5-109">Isolation and secure network access.</span></span>
- <span data-ttu-id="e16f5-110">高記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="e16f5-110">High memory utilization.</span></span>

<span data-ttu-id="e16f5-111">客戶可以在單一 Azure 區域中或跨多個 Azure 區域建立多個 ASE。</span><span class="sxs-lookup"><span data-stu-id="e16f5-111">Customers can create multiple ASEs within a single Azure region or across multiple Azure regions.</span></span> <span data-ttu-id="e16f5-112">這種彈性讓 ASE 很適合用於水平調整無狀態應用程式層的規模，以支援高 RPS 的工作負載。</span><span class="sxs-lookup"><span data-stu-id="e16f5-112">This flexibility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="e16f5-113">ASE 已經過隔離，可執行只有單一客戶的應用程式，且一律會部署到虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e16f5-113">ASEs are isolated to running only a single customer's applications and are always deployed into a virtual network.</span></span> <span data-ttu-id="e16f5-114">客戶可以精確控制輸入和輸出的應用程式網路流量。</span><span class="sxs-lookup"><span data-stu-id="e16f5-114">Customers have fine-grained control over inbound and outbound application network traffic.</span></span> <span data-ttu-id="e16f5-115">應用程式可以透過 VPN 建立內部部署公司資源的高速安全連線。</span><span class="sxs-lookup"><span data-stu-id="e16f5-115">Applications can establish high-speed secure connections over VPNs to on-premises corporate resources.</span></span>

<span data-ttu-id="e16f5-116">您可以在 [App Service Environment 的 README][ASEReadme] 中取得 ASE 的所有相關文章與做法指示：</span><span class="sxs-lookup"><span data-stu-id="e16f5-116">All articles and how-to instructions about ASEs are available in the [README for App Service environments][ASEReadme]:</span></span>

* <span data-ttu-id="e16f5-117">ASE 可透過安全的網路存取，提供高延展性的應用程式裝載。</span><span class="sxs-lookup"><span data-stu-id="e16f5-117">ASEs enable high-scale app hosting with secure network access.</span></span> <span data-ttu-id="e16f5-118">如需詳細資訊，請參閱為 ASE 提供的 [AzureCon 深入探討](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="e16f5-118">For more information, see the [AzureCon Deep Dive](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) on ASEs.</span></span>
* <span data-ttu-id="e16f5-119">您可以使用多個 ASE 進行水平調整。</span><span class="sxs-lookup"><span data-stu-id="e16f5-119">Multiple ASEs can be used to scale horizontally.</span></span> <span data-ttu-id="e16f5-120">如需詳細資訊，請參閱[如何設定異地分散應用程式使用量](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/)。</span><span class="sxs-lookup"><span data-stu-id="e16f5-120">For more information, see [how to set up a geo-distributed app footprint](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).</span></span>
* <span data-ttu-id="e16f5-121">您可以將 ASE 用於設定安全性架構，如 AzureCon 深入探討所示。</span><span class="sxs-lookup"><span data-stu-id="e16f5-121">ASEs can be used to configure security architecture, as shown in the AzureCon Deep Dive.</span></span> <span data-ttu-id="e16f5-122">若要了解 AzureCon 深入探討中示範之安全性架構的設定方式，請參閱有關如何透過 App Service Environment [實行分層安全性架構的文章](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security)。</span><span class="sxs-lookup"><span data-stu-id="e16f5-122">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the [article on how to implement a layered security architecture](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) with App Service environments.</span></span>
* <span data-ttu-id="e16f5-123">在 ASE 中執行之應用程式的存取權可能會受到 Web 應用程式防火牆 (WAF) 等上游裝置的管制。</span><span class="sxs-lookup"><span data-stu-id="e16f5-123">Apps running on ASEs can have their access gated by upstream devices, such as web application firewalls (WAFs).</span></span> <span data-ttu-id="e16f5-124">如需詳細資訊，請參閱[設定 App Service Environment 的 WAF](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall)。</span><span class="sxs-lookup"><span data-stu-id="e16f5-124">For more information, see [Configure a WAF for App Service environments](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).</span></span>

## <a name="dedicated-environment"></a><span data-ttu-id="e16f5-125">專用的環境</span><span class="sxs-lookup"><span data-stu-id="e16f5-125">Dedicated environment</span></span> ##

<span data-ttu-id="e16f5-126">ASE 以獨佔方式專屬於單一訂用帳戶，並可以裝載 100 個執行個體。</span><span class="sxs-lookup"><span data-stu-id="e16f5-126">An ASE is dedicated exclusively to a single subscription and can host 100 instances.</span></span> <span data-ttu-id="e16f5-127">不管是單一 App Service 方案中的 100 個執行個體或 100 個單一執行個體的 App Service 方案，只要加總之執行個體數在 100 以下皆可。</span><span class="sxs-lookup"><span data-stu-id="e16f5-127">The range can span 100 instances in a single App Service plan to 100 single-instance App Service plans, and everything in between.</span></span>

<span data-ttu-id="e16f5-128">ASE 是由前端和背景工作角色所組成。</span><span class="sxs-lookup"><span data-stu-id="e16f5-128">An ASE is composed of front ends and workers.</span></span> <span data-ttu-id="e16f5-129">前端負責處理 HTTP/HTTPS 終止和 ASE 中應用程式要求的自動負載平衡。</span><span class="sxs-lookup"><span data-stu-id="e16f5-129">Front ends are responsible for HTTP/HTTPS termination and automatic load balancing of app requests within an ASE.</span></span> <span data-ttu-id="e16f5-130">前端會隨 ASE 中的 App Service 方案相應放大而自動新增。</span><span class="sxs-lookup"><span data-stu-id="e16f5-130">Front ends are automatically added as the App Service plans in the ASE are scaled out.</span></span>

<span data-ttu-id="e16f5-131">背景工作角色是裝載客戶應用程式的角色。</span><span class="sxs-lookup"><span data-stu-id="e16f5-131">Workers are roles that host customer apps.</span></span> <span data-ttu-id="e16f5-132">背景工作角色可以三個固定的大小提供：</span><span class="sxs-lookup"><span data-stu-id="e16f5-132">Workers are available in three fixed sizes:</span></span>

* <span data-ttu-id="e16f5-133">單核心/3.5 GB RAM</span><span class="sxs-lookup"><span data-stu-id="e16f5-133">One core/3.5 GB RAM</span></span>
* <span data-ttu-id="e16f5-134">雙核心/7 GB RAM</span><span class="sxs-lookup"><span data-stu-id="e16f5-134">Two core/7 GB RAM</span></span>
* <span data-ttu-id="e16f5-135">四核心/14 GB RAM</span><span class="sxs-lookup"><span data-stu-id="e16f5-135">Four core/14 GB RAM</span></span>

<span data-ttu-id="e16f5-136">客戶不需要管理前端和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="e16f5-136">Customers do not need to manage front ends and workers.</span></span> <span data-ttu-id="e16f5-137">所有的基礎結構會隨客戶的 App Service 方案相應放大而自動新增。</span><span class="sxs-lookup"><span data-stu-id="e16f5-137">All infrastructure is automatically added as customers scale out their App Service plans.</span></span> <span data-ttu-id="e16f5-138">隨著 App Service 方案建立或相應縮小 ASE，會視需要將基礎結構新增或移除。</span><span class="sxs-lookup"><span data-stu-id="e16f5-138">As App Service plans are created or scaled in an ASE, the required infrastructure is added or removed as appropriate.</span></span>

<span data-ttu-id="e16f5-139">ASE 會有一般每月費率來支付基礎結構，且不會依 ASE 的大小而變更。</span><span class="sxs-lookup"><span data-stu-id="e16f5-139">There is a flat monthly rate for an ASE that pays for the infrastructure and doesn't change with the size of the ASE.</span></span> <span data-ttu-id="e16f5-140">此外，每個 App Service 方案核心都會有其成本。</span><span class="sxs-lookup"><span data-stu-id="e16f5-140">In addition, there is a cost per App Service plan core.</span></span> <span data-ttu-id="e16f5-141">ASE 中裝載的所有應用程式都會位於隔離價格 SKU 中。</span><span class="sxs-lookup"><span data-stu-id="e16f5-141">All apps hosted in an ASE are in the Isolated pricing SKU.</span></span> <span data-ttu-id="e16f5-142">如需有關 ASE 價格的資訊，請參閱 [App Service 價格][Pricing]頁面並檢閱 ASE 的可用選項。</span><span class="sxs-lookup"><span data-stu-id="e16f5-142">For information on pricing for an ASE, see the [App Service pricing][Pricing] page and review the available options for ASEs.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="e16f5-143">虛擬網路支援</span><span class="sxs-lookup"><span data-stu-id="e16f5-143">Virtual network support</span></span> ##

<span data-ttu-id="e16f5-144">您只能在 Azure Resource Manager 虛擬網路中建立 ASE。</span><span class="sxs-lookup"><span data-stu-id="e16f5-144">An ASE can be created only in an Azure Resource Manager virtual network.</span></span> <span data-ttu-id="e16f5-145">若要深入了解 Azure 虛擬網路，請參閱 [Azure 虛擬網路常見問題集](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/)。</span><span class="sxs-lookup"><span data-stu-id="e16f5-145">To learn more about Azure virtual networks, see the [Azure virtual networks FAQ](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/).</span></span> <span data-ttu-id="e16f5-146">ASE 一律存在於虛擬網路；更精確地說，是虛擬網路的子網路內。</span><span class="sxs-lookup"><span data-stu-id="e16f5-146">An ASE always exists in a virtual network, and more precisely, within a subnet of a virtual network.</span></span> <span data-ttu-id="e16f5-147">您可以使用虛擬網路的安全性功能控制應用程式的輸入和輸出網路通訊。</span><span class="sxs-lookup"><span data-stu-id="e16f5-147">You can use the security features of virtual networks to control inbound and outbound network communications for your apps.</span></span>

<span data-ttu-id="e16f5-148">ASE 可以是具有公用 IP 位址的網際網路對應，或只具有 Azure 內部負載平衡器 (ILB) 位址的內部對應。</span><span class="sxs-lookup"><span data-stu-id="e16f5-148">An ASE can be either internet-facing with a public IP address or internal-facing with only an Azure internal load balancer (ILB) address.</span></span>

<span data-ttu-id="e16f5-149">[網路安全性群組][NSGs]會將輸入網路通訊限制於 ASE 所在的子網路。</span><span class="sxs-lookup"><span data-stu-id="e16f5-149">[Network Security Groups][NSGs] restrict inbound network communications to the subnet where an ASE resides.</span></span> <span data-ttu-id="e16f5-150">您可以使用 NSG 在上游裝置和服務 (例如 WAF 和網路 SaaS 提供者) 背後執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="e16f5-150">You can use NSGs to run apps behind upstream devices and services such as WAFs and network SaaS providers.</span></span>

<span data-ttu-id="e16f5-151">應用程式也經常需要存取公司資源，例如內部資料庫和 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e16f5-151">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span> <span data-ttu-id="e16f5-152">如果您在具有內部部署網路 VPN 連線的虛擬網路中部署 ASE，ASE 中的應用程式便可以存取內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="e16f5-152">If you deploy the ASE in a virtual network that has a VPN connection to the on-premises network, the apps in the ASE can access the on-premises resources.</span></span> <span data-ttu-id="e16f5-153">無論 VPN 是[站對站](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/)或 [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN，此功能都可適用。</span><span class="sxs-lookup"><span data-stu-id="e16f5-153">This capability is true regardless of whether the VPN is a [site-to-site](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) or [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.</span></span>

<span data-ttu-id="e16f5-154">如需有關 ASE 與虛擬網路和內部部署網路搭配運作方式的詳細資訊，請參閱 [App Service Environment 的網路考量][ASENetwork]。</span><span class="sxs-lookup"><span data-stu-id="e16f5-154">For more information on how ASEs work with virtual networks and on-premises networks, see [App Service Environment network considerations][ASENetwork].</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="e16f5-155">App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="e16f5-155">App Service Environment v1</span></span> ##

<span data-ttu-id="e16f5-156">App Service Environment 有兩個版本：ASEv1 和 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="e16f5-156">App Service Environment has two versions: ASEv1 and ASEv2.</span></span> <span data-ttu-id="e16f5-157">前述資訊架構在 ASEv2 上。</span><span class="sxs-lookup"><span data-stu-id="e16f5-157">The preceding information was based on ASEv2.</span></span> <span data-ttu-id="e16f5-158">本節說明 ASEv1 與 ASEv2 之間的差異。</span><span class="sxs-lookup"><span data-stu-id="e16f5-158">This section shows you the differences between ASEv1 and ASEv2.</span></span> 

<span data-ttu-id="e16f5-159">在 ASEv1 中，您必須手動管理所有資源。</span><span class="sxs-lookup"><span data-stu-id="e16f5-159">In ASEv1, you need to manage all of the resources manually.</span></span> <span data-ttu-id="e16f5-160">其中包括前端、背景工作角色和用於 IP 型 SSL 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e16f5-160">That includes the front ends, workers, and IP addresses used for IP-based SSL.</span></span> <span data-ttu-id="e16f5-161">首先，您必須將想要在其中裝載的背景工作角色集區相應放大，才能相應放大 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="e16f5-161">Before you can scale out your App Service plan, you need to first scale out the worker pool where you want to host it.</span></span>

<span data-ttu-id="e16f5-162">ASEv1 使用與 ASEv2 不同的定價模式。</span><span class="sxs-lookup"><span data-stu-id="e16f5-162">ASEv1 uses a different pricing model from ASEv2.</span></span> <span data-ttu-id="e16f5-163">在 ASEv1 中，您需要支付每個配置的核心。</span><span class="sxs-lookup"><span data-stu-id="e16f5-163">In ASEv1, you pay for each core allocated.</span></span> <span data-ttu-id="e16f5-164">其中包括用於前端或未裝載任何工作負載之背景工作角色的核心。</span><span class="sxs-lookup"><span data-stu-id="e16f5-164">That includes cores used for front ends or workers that aren't hosting any workloads.</span></span> <span data-ttu-id="e16f5-165">在 ASEv1 中，ASE 的預設最大調整大小總計是 55 個主機，</span><span class="sxs-lookup"><span data-stu-id="e16f5-165">In ASEv1, the default maximum-scale size of an ASE is 55 total hosts.</span></span> <span data-ttu-id="e16f5-166">包括背景工作角色與前端。</span><span class="sxs-lookup"><span data-stu-id="e16f5-166">That includes workers and front ends.</span></span> <span data-ttu-id="e16f5-167">ASEv1 的其中一個優點，是可以部署在傳統虛擬網路和 Resource Manager虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="e16f5-167">One advantage to ASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span></span> <span data-ttu-id="e16f5-168">若要深入了解 ASEv1，請參閱 [App Service Environment v1 簡介][ASEv1Intro]。</span><span class="sxs-lookup"><span data-stu-id="e16f5-168">To learn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span></span>

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
