---
title: "aaaIntroduction tooAzure App Service 環境"
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
ms.openlocfilehash: 9261041333cf59374974a039edf89c4983c45cdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environments"></a><span data-ttu-id="575d8-103">簡介 tooApp 服務環境</span><span class="sxs-lookup"><span data-stu-id="575d8-103">Introduction tooApp Service environments</span></span> #
 
## <a name="overview"></a><span data-ttu-id="575d8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="575d8-104">Overview</span></span> ##

<span data-ttu-id="575d8-105">Azure App Service Environment 是 Azure App Service 的功能，可提供完全隔離和專用的環境，以便安全地大規模執行 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="575d8-105">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="575d8-106">此功能可裝載 [Web 應用程式][webapps]、[行動應用程式][mobileapps]、[API 應用程式][APIapps]和[函數][Functions]。</span><span class="sxs-lookup"><span data-stu-id="575d8-106">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIapps], and [functions][Functions].</span></span>

<span data-ttu-id="575d8-107">App Service Environment (ASE) 適合需要下列項目的應用程式工作負載：</span><span class="sxs-lookup"><span data-stu-id="575d8-107">App Service environments (ASEs) are appropriate for application workloads that require:</span></span>

- <span data-ttu-id="575d8-108">非常高的延展性。</span><span class="sxs-lookup"><span data-stu-id="575d8-108">Very high scale.</span></span>
- <span data-ttu-id="575d8-109">隔離和安全的網路存取。</span><span class="sxs-lookup"><span data-stu-id="575d8-109">Isolation and secure network access.</span></span>
- <span data-ttu-id="575d8-110">高記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="575d8-110">High memory utilization.</span></span>

<span data-ttu-id="575d8-111">客戶可以在單一 Azure 區域中或跨多個 Azure 區域建立多個 ASE。</span><span class="sxs-lookup"><span data-stu-id="575d8-111">Customers can create multiple ASEs within a single Azure region or across multiple Azure regions.</span></span> <span data-ttu-id="575d8-112">這種彈性讓 ASE 很適合用於水平調整無狀態應用程式層的規模，以支援高 RPS 的工作負載。</span><span class="sxs-lookup"><span data-stu-id="575d8-112">This flexibility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="575d8-113">ASEs 隔離的 toorunning 只有單一客戶的應用程式，而且一律會部署到虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="575d8-113">ASEs are isolated toorunning only a single customer's applications and are always deployed into a virtual network.</span></span> <span data-ttu-id="575d8-114">客戶可以精確控制輸入和輸出的應用程式網路流量。</span><span class="sxs-lookup"><span data-stu-id="575d8-114">Customers have fine-grained control over inbound and outbound application network traffic.</span></span> <span data-ttu-id="575d8-115">應用程式可以建立高速的安全連接，透過 Vpn tooon 內部公司資源。</span><span class="sxs-lookup"><span data-stu-id="575d8-115">Applications can establish high-speed secure connections over VPNs tooon-premises corporate resources.</span></span>

<span data-ttu-id="575d8-116">所有文件及如何-tooinstructions 有關 ASEs 位於 hello [App Service 環境的讀我檔案][ASEReadme]:</span><span class="sxs-lookup"><span data-stu-id="575d8-116">All articles and how-tooinstructions about ASEs are available in hello [README for App Service environments][ASEReadme]:</span></span>

* <span data-ttu-id="575d8-117">ASE 可透過安全的網路存取，提供高延展性的應用程式裝載。</span><span class="sxs-lookup"><span data-stu-id="575d8-117">ASEs enable high-scale app hosting with secure network access.</span></span> <span data-ttu-id="575d8-118">如需詳細資訊，請參閱 hello [AzureCon 深入探討](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/)ASEs 上。</span><span class="sxs-lookup"><span data-stu-id="575d8-118">For more information, see hello [AzureCon Deep Dive](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) on ASEs.</span></span>
* <span data-ttu-id="575d8-119">多個 ASEs 可以水平方式是使用的 tooscale。</span><span class="sxs-lookup"><span data-stu-id="575d8-119">Multiple ASEs can be used tooscale horizontally.</span></span> <span data-ttu-id="575d8-120">如需詳細資訊，請參閱[如何向上地理分散的應用程式使用量 tooset](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/)。</span><span class="sxs-lookup"><span data-stu-id="575d8-120">For more information, see [how tooset up a geo-distributed app footprint](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).</span></span>
* <span data-ttu-id="575d8-121">可以使用的 tooconfigure 安全性架構，ASEs，hello AzureCon 深入了解所示。</span><span class="sxs-lookup"><span data-stu-id="575d8-121">ASEs can be used tooconfigure security architecture, as shown in hello AzureCon Deep Dive.</span></span> <span data-ttu-id="575d8-122">toosee hello AzureCon 深入了解所示的 hello 安全性架構的設定方式，請參閱 hello[有關的文章 tooimplement 多層式的安全性架構](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security)App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="575d8-122">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello [article on how tooimplement a layered security architecture](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) with App Service environments.</span></span>
* <span data-ttu-id="575d8-123">在 ASE 中執行之應用程式的存取權可能會受到 Web 應用程式防火牆 (WAF) 等上游裝置的管制。</span><span class="sxs-lookup"><span data-stu-id="575d8-123">Apps running on ASEs can have their access gated by upstream devices, such as web application firewalls (WAFs).</span></span> <span data-ttu-id="575d8-124">如需詳細資訊，請參閱[設定 App Service Environment 的 WAF](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall)。</span><span class="sxs-lookup"><span data-stu-id="575d8-124">For more information, see [Configure a WAF for App Service environments](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).</span></span>

## <a name="dedicated-environment"></a><span data-ttu-id="575d8-125">專用的環境</span><span class="sxs-lookup"><span data-stu-id="575d8-125">Dedicated environment</span></span> ##

<span data-ttu-id="575d8-126">Ase 中是專專門 tooa 單一訂用帳戶，而且可以裝載 100 個執行個體。</span><span class="sxs-lookup"><span data-stu-id="575d8-126">An ASE is dedicated exclusively tooa single subscription and can host 100 instances.</span></span> <span data-ttu-id="575d8-127">hello 範圍可以跨 100 個執行個體中單一應用程式服務計劃 too100 單一執行個體應用程式服務計劃，以及兩者之間的所有項目。</span><span class="sxs-lookup"><span data-stu-id="575d8-127">hello range can span 100 instances in a single App Service plan too100 single-instance App Service plans, and everything in between.</span></span>

<span data-ttu-id="575d8-128">ASE 是由前端和背景工作角色所組成。</span><span class="sxs-lookup"><span data-stu-id="575d8-128">An ASE is composed of front ends and workers.</span></span> <span data-ttu-id="575d8-129">前端負責處理 HTTP/HTTPS 終止和 ASE 中應用程式要求的自動負載平衡。</span><span class="sxs-lookup"><span data-stu-id="575d8-129">Front ends are responsible for HTTP/HTTPS termination and automatic load balancing of app requests within an ASE.</span></span> <span data-ttu-id="575d8-130">前端會自動加入為 hello hello ASE 中的應用程式服務計劃會向外延展。</span><span class="sxs-lookup"><span data-stu-id="575d8-130">Front ends are automatically added as hello App Service plans in hello ASE are scaled out.</span></span>

<span data-ttu-id="575d8-131">背景工作角色是裝載客戶應用程式的角色。</span><span class="sxs-lookup"><span data-stu-id="575d8-131">Workers are roles that host customer apps.</span></span> <span data-ttu-id="575d8-132">背景工作角色可以三個固定的大小提供：</span><span class="sxs-lookup"><span data-stu-id="575d8-132">Workers are available in three fixed sizes:</span></span>

* <span data-ttu-id="575d8-133">單核心/3.5 GB RAM</span><span class="sxs-lookup"><span data-stu-id="575d8-133">One core/3.5 GB RAM</span></span>
* <span data-ttu-id="575d8-134">雙核心/7 GB RAM</span><span class="sxs-lookup"><span data-stu-id="575d8-134">Two core/7 GB RAM</span></span>
* <span data-ttu-id="575d8-135">四核心/14 GB RAM</span><span class="sxs-lookup"><span data-stu-id="575d8-135">Four core/14 GB RAM</span></span>

<span data-ttu-id="575d8-136">客戶不需要 toomanage 前端和背景工作。</span><span class="sxs-lookup"><span data-stu-id="575d8-136">Customers do not need toomanage front ends and workers.</span></span> <span data-ttu-id="575d8-137">所有的基礎結構會隨客戶的 App Service 方案相應放大而自動新增。</span><span class="sxs-lookup"><span data-stu-id="575d8-137">All infrastructure is automatically added as customers scale out their App Service plans.</span></span> <span data-ttu-id="575d8-138">應用程式服務計劃所建立，或在 ase 中縮放，hello 必須加入或移除視基礎結構。</span><span class="sxs-lookup"><span data-stu-id="575d8-138">As App Service plans are created or scaled in an ASE, hello required infrastructure is added or removed as appropriate.</span></span>

<span data-ttu-id="575d8-139">沒有所支付的 hello 基礎結構，並不會變更與 hello ASE hello 大小 ase 中單層每月費率。</span><span class="sxs-lookup"><span data-stu-id="575d8-139">There is a flat monthly rate for an ASE that pays for hello infrastructure and doesn't change with hello size of hello ASE.</span></span> <span data-ttu-id="575d8-140">此外，每個 App Service 方案核心都會有其成本。</span><span class="sxs-lookup"><span data-stu-id="575d8-140">In addition, there is a cost per App Service plan core.</span></span> <span data-ttu-id="575d8-141">在 ase 中託管的所有應用程式位於 hello 隔離定價 SKU。</span><span class="sxs-lookup"><span data-stu-id="575d8-141">All apps hosted in an ASE are in hello Isolated pricing SKU.</span></span> <span data-ttu-id="575d8-142">如需定價的 ase 中的資訊，請參閱 hello[應用程式服務定價][ Pricing]頁面上，並檢閱 ASEs hello 可用選項。</span><span class="sxs-lookup"><span data-stu-id="575d8-142">For information on pricing for an ASE, see hello [App Service pricing][Pricing] page and review hello available options for ASEs.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="575d8-143">虛擬網路支援</span><span class="sxs-lookup"><span data-stu-id="575d8-143">Virtual network support</span></span> ##

<span data-ttu-id="575d8-144">您只能在 Azure Resource Manager 虛擬網路中建立 ASE。</span><span class="sxs-lookup"><span data-stu-id="575d8-144">An ASE can be created only in an Azure Resource Manager virtual network.</span></span> <span data-ttu-id="575d8-145">toolearn 進一步了解 Azure 虛擬網路，請參閱 hello [Azure 虛擬網路常見問題集](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/)。</span><span class="sxs-lookup"><span data-stu-id="575d8-145">toolearn more about Azure virtual networks, see hello [Azure virtual networks FAQ](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/).</span></span> <span data-ttu-id="575d8-146">ASE 一律存在於虛擬網路；更精確地說，是虛擬網路的子網路內。</span><span class="sxs-lookup"><span data-stu-id="575d8-146">An ASE always exists in a virtual network, and more precisely, within a subnet of a virtual network.</span></span> <span data-ttu-id="575d8-147">您可以使用 hello 安全性功能的虛擬網路 toocontrol 傳入和傳出網路通訊，您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="575d8-147">You can use hello security features of virtual networks toocontrol inbound and outbound network communications for your apps.</span></span>

<span data-ttu-id="575d8-148">ASE 可以是具有公用 IP 位址的網際網路對應，或只具有 Azure 內部負載平衡器 (ILB) 位址的內部對應。</span><span class="sxs-lookup"><span data-stu-id="575d8-148">An ASE can be either internet-facing with a public IP address or internal-facing with only an Azure internal load balancer (ILB) address.</span></span>

<span data-ttu-id="575d8-149">[網路安全性群組][ NSGs]限制 ase 中的所在位置的輸入的網路通訊 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="575d8-149">[Network Security Groups][NSGs] restrict inbound network communications toohello subnet where an ASE resides.</span></span> <span data-ttu-id="575d8-150">您可以使用 Nsg toorun 應用程式背後上游的裝置和服務，例如 WAFs 和網路 SaaS 提供者。</span><span class="sxs-lookup"><span data-stu-id="575d8-150">You can use NSGs toorun apps behind upstream devices and services such as WAFs and network SaaS providers.</span></span>

<span data-ttu-id="575d8-151">應用程式也經常會需要 tooaccess 公司資源，例如內部資料庫和 web 服務。</span><span class="sxs-lookup"><span data-stu-id="575d8-151">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span> <span data-ttu-id="575d8-152">如果您部署的 VPN 連線 toohello 在內部部署網路的虛擬網路中的 hello ASE，hello hello ASE 中的應用程式可以存取 hello 在內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="575d8-152">If you deploy hello ASE in a virtual network that has a VPN connection toohello on-premises network, hello apps in hello ASE can access hello on-premises resources.</span></span> <span data-ttu-id="575d8-153">無論是 hello VPN，則為 true，此功能會[站對站](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/)或[Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN。</span><span class="sxs-lookup"><span data-stu-id="575d8-153">This capability is true regardless of whether hello VPN is a [site-to-site](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) or [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.</span></span>

<span data-ttu-id="575d8-154">如需有關 ASE 與虛擬網路和內部部署網路搭配運作方式的詳細資訊，請參閱 [App Service Environment 的網路考量][ASENetwork]。</span><span class="sxs-lookup"><span data-stu-id="575d8-154">For more information on how ASEs work with virtual networks and on-premises networks, see [App Service Environment network considerations][ASENetwork].</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="575d8-155">App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="575d8-155">App Service Environment v1</span></span> ##

<span data-ttu-id="575d8-156">App Service Environment 有兩個版本：ASEv1 和 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="575d8-156">App Service Environment has two versions: ASEv1 and ASEv2.</span></span> <span data-ttu-id="575d8-157">hello 上述資訊為基礎 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="575d8-157">hello preceding information was based on ASEv2.</span></span> <span data-ttu-id="575d8-158">此區段會顯示 hello ASEv2 ASEv1 之間的差異。</span><span class="sxs-lookup"><span data-stu-id="575d8-158">This section shows you hello differences between ASEv1 and ASEv2.</span></span> 

<span data-ttu-id="575d8-159">您需要 toomanage ASEv1，所有的手動 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="575d8-159">In ASEv1, you need toomanage all of hello resources manually.</span></span> <span data-ttu-id="575d8-160">含有 hello 前端、 背景工作，與用於 IP SSL 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="575d8-160">That includes hello front ends, workers, and IP addresses used for IP-based SSL.</span></span> <span data-ttu-id="575d8-161">您可以調整您的應用程式服務計劃之前，您需要 toofirst 它擴充想 toohost hello 背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="575d8-161">Before you can scale out your App Service plan, you need toofirst scale out hello worker pool where you want toohost it.</span></span>

<span data-ttu-id="575d8-162">ASEv1 使用與 ASEv2 不同的定價模式。</span><span class="sxs-lookup"><span data-stu-id="575d8-162">ASEv1 uses a different pricing model from ASEv2.</span></span> <span data-ttu-id="575d8-163">在 ASEv1 中，您需要支付每個配置的核心。</span><span class="sxs-lookup"><span data-stu-id="575d8-163">In ASEv1, you pay for each core allocated.</span></span> <span data-ttu-id="575d8-164">其中包括用於前端或未裝載任何工作負載之背景工作角色的核心。</span><span class="sxs-lookup"><span data-stu-id="575d8-164">That includes cores used for front ends or workers that aren't hosting any workloads.</span></span> <span data-ttu-id="575d8-165">ASEv1，在 ase 中的 hello 預設最大標尺大小會是 55 主機總計。</span><span class="sxs-lookup"><span data-stu-id="575d8-165">In ASEv1, hello default maximum-scale size of an ASE is 55 total hosts.</span></span> <span data-ttu-id="575d8-166">包括背景工作角色與前端。</span><span class="sxs-lookup"><span data-stu-id="575d8-166">That includes workers and front ends.</span></span> <span data-ttu-id="575d8-167">一個利用 tooASEv1 是它可以部署在傳統的虛擬網路和資源管理員的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="575d8-167">One advantage tooASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span></span> <span data-ttu-id="575d8-168">toolearn 深入了解 ASEv1，請參閱[App Service 環境 v1 簡介][ASEv1Intro]。</span><span class="sxs-lookup"><span data-stu-id="575d8-168">toolearn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span></span>

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
