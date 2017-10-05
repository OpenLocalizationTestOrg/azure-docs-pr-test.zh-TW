---
title: "App Service 環境 v1 簡介"
description: "了解可提供安全、VNet 聯結、專用延展單位的 App Service 環境 v1 功能，以便執行您所有的應用程式。"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 38cb79eb32bd61cdbfb6da91d50e6713d71a2b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-app-service-environment-v1"></a><span data-ttu-id="23a48-103">App Service 環境 v1 簡介</span><span class="sxs-lookup"><span data-stu-id="23a48-103">Introduction to App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="23a48-104">這篇文章是關於 App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="23a48-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="23a48-105">有較新版本的 App Service 環境，更易於使用，並且可以在功能更強大的基礎結構上執行。</span><span class="sxs-lookup"><span data-stu-id="23a48-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="23a48-106">若要深入了解新版本，請從 [App Service 環境簡介](../app-service/app-service-environment/intro.md)開始。</span><span class="sxs-lookup"><span data-stu-id="23a48-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="23a48-107">概觀</span><span class="sxs-lookup"><span data-stu-id="23a48-107">Overview</span></span>
<span data-ttu-id="23a48-108">App Service 環境是 Azure App Service 的[高階][PremiumTier]服務方案選項，提供完全隔離的專用環境，能夠極為安全地執行 Azure App Service 應用程式，包括 [Web Apps][WebApps]、[Mobile Apps][MobileApps]和 [API Apps][APIApps]。</span><span class="sxs-lookup"><span data-stu-id="23a48-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="23a48-109">適合應用程式工作負載的 App Service 環境需要：</span><span class="sxs-lookup"><span data-stu-id="23a48-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="23a48-110">非常高的延展性</span><span class="sxs-lookup"><span data-stu-id="23a48-110">Very high scale</span></span>
* <span data-ttu-id="23a48-111">隔離和安全的網路存取</span><span class="sxs-lookup"><span data-stu-id="23a48-111">Isolation and secure network access</span></span>

<span data-ttu-id="23a48-112">客戶可以在單一 Azure 區域，以及跨多個 Azure 區域中建立多個 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="23a48-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="23a48-113">這使得 App Service 環境很適合用來水平調整無狀態應用程式層的規模，以支援高 RPS 工作負載。</span><span class="sxs-lookup"><span data-stu-id="23a48-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="23a48-114">App Service 環境已經過隔離，可執行只有單一客戶的應用程式，且一律會部署到虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23a48-114">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="23a48-115">客戶對於輸入和輸出的應用程式網路流量都有更細微的控制，且應用程式可以透過虛擬網路建立與內部部署公司資源的高速安全連線。</span><span class="sxs-lookup"><span data-stu-id="23a48-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="23a48-116">您可以在 [應用程式服務環境的讀我檔案](../app-service/app-service-app-service-environments-readme.md)中取得 App Service 環境的所有相關文章與做法。</span><span class="sxs-lookup"><span data-stu-id="23a48-116">All articles and How-To's about App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="23a48-117">如需 App Service Environment 如何提供高延展性和安全的網路存取的概觀，請參閱關於 App Service Environment 的 [AzureCon 深入探討][AzureConDeepDive]！</span><span class="sxs-lookup"><span data-stu-id="23a48-117">For an overview of how App Service Environments enable high scale and secure network access, see the [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="23a48-118">如需使用多個 App Service Environment 水平延展的深入探討，請參閱關於如何設定[地理位置分散的應用程式使用量][GeodistributedAppFootprint]一文。</span><span class="sxs-lookup"><span data-stu-id="23a48-118">For a deep-dive on horizontally scaling using multiple App Service Environments see the article on how to setup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="23a48-119">若要查看 AzureCon Deep Dive 中顯示之安全性架構的設定方式，請參閱有關使用 App Service Environment 實作 [分層安全性架構](app-service-app-service-environment-layered-security.md) 的文章。</span><span class="sxs-lookup"><span data-stu-id="23a48-119">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="23a48-120">在 App Service 環境中執行之應用程式的存取權可能會受到 Web 應用程式防火牆 (WAF) 等上游裝置的管制。</span><span class="sxs-lookup"><span data-stu-id="23a48-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="23a48-121">[設定 App Service Environment 的 WAF](app-service-app-service-environment-web-application-firewall.md) 上的文章將說明這種情況。</span><span class="sxs-lookup"><span data-stu-id="23a48-121">The article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="23a48-122">專用計算資源</span><span class="sxs-lookup"><span data-stu-id="23a48-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="23a48-123">App Service Environment 中的所有計算資源皆專屬於單一訂用帳戶，且 App Service Environment可以設定最多五十 (50) 個計算資源，讓單一應用程式獨佔使用。</span><span class="sxs-lookup"><span data-stu-id="23a48-123">All of the compute resources in an App Service Environment are dedicated exclusively to a single subscription, and an App Service Environment can be configured with up to fifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="23a48-124">App Service Environment 是由前端計算資源集區，以及一到三個背景工作計算資源集區所組成。</span><span class="sxs-lookup"><span data-stu-id="23a48-124">An App Service Environment is composed of a front-end compute resource pool, as well as one to three worker compute resource pools.</span></span> 

<span data-ttu-id="23a48-125">前端集區包含負責處理 SSL 終止以及 App Service Environment 中應用程式要求的自動負載平衡的計算資源。</span><span class="sxs-lookup"><span data-stu-id="23a48-125">The front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="23a48-126">每個背景工作集區都含有配置給 [App Service 方案][AppServicePlan]的計算資源，其中又包含一或多個 Azure App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="23a48-126">Each worker pool contains compute resources allocated to [App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="23a48-127">因為 App Service Environment 中可有多達三個不同的背景工作集區，所以您有彈性可為每個背景工作集區選擇不同的計算資源。</span><span class="sxs-lookup"><span data-stu-id="23a48-127">Since there can be up to three different worker pools in an App Service Environment, you have the flexibility to choose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="23a48-128">比方說，您可以針對主要用於開發或測試應用程式的 App Service 方案，建立一個計算資源較不強大的背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="23a48-128">For example, this allows you to create one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="23a48-129">第二個 (或甚至第三個) 背景工作集區可以使用比較強大的運算資源，以供 App Service 方案執行生產應用程式。</span><span class="sxs-lookup"><span data-stu-id="23a48-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="23a48-130">如需前端和背景工作集區可用計算資源數量的詳細資訊，請參閱[如何設定 App Service Environment][HowToConfigureanAppServiceEnvironment]。</span><span class="sxs-lookup"><span data-stu-id="23a48-130">For more details on the quantity of compute resources available to the front-end and worker pools, see [How To Configure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="23a48-131">如需 App Service Environment 中支援的可用計算資源大小的詳細資訊，請參閱 [App Service 定價][AppServicePricing]頁面，並檢閱 Premium 定價層中 App Service Environment可用的選項。</span><span class="sxs-lookup"><span data-stu-id="23a48-131">For details on the available compute resource sizes supported in an App Service Environment, consult the [App Service Pricing][AppServicePricing] page and review the available options for App Service Environments in the Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="23a48-132">虛擬網路支援</span><span class="sxs-lookup"><span data-stu-id="23a48-132">Virtual Network Support</span></span>
<span data-ttu-id="23a48-133">App Service Environment 可以在 Azure Resource Manager 虛擬網路或者傳統式部署模型虛擬網路其中之一中建立 ([更多有關虛擬網路的資訊][MoreInfoOnVirtualNetworks])。</span><span class="sxs-lookup"><span data-stu-id="23a48-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="23a48-134">因為 App Service Environment 一律存在於虛擬網路中，而且更精確來說是在虛擬網路的子網路內，所以您可以運用虛擬網路的安全性功能來控制傳入和傳出網路通訊。</span><span class="sxs-lookup"><span data-stu-id="23a48-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage the security features of virtual networks to control both inbound and outbound network communications.</span></span>  

<span data-ttu-id="23a48-135">App Service Environment 可以是具有公用 IP 位址的網際網路對向，或只具有 Azure 內部負載平衡器 (ILB) 位址的內部對向。</span><span class="sxs-lookup"><span data-stu-id="23a48-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="23a48-136">您可以使用[網路安全性群組][NetworkSecurityGroups]將傳入網路通訊限制為 App Service Environment 所在的子網路。</span><span class="sxs-lookup"><span data-stu-id="23a48-136">You can use [network security groups][NetworkSecurityGroups] to restrict inbound network communications to the subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="23a48-137">這可讓您在上游裝置和服務 (例如 Ｗeb 應用程式防火牆和網路 SaaS 提供者) 背後執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="23a48-137">This allows you to run apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="23a48-138">應用程式也經常需要存取公司資源，例如內部資料庫和 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="23a48-138">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="23a48-139">常見的方法是讓這些端點僅可用於在 Azure 虛擬網路中傳送的內部網路流量。</span><span class="sxs-lookup"><span data-stu-id="23a48-139">A common approach is to make these endpoints available only to internal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="23a48-140">一旦 App Service Environment 加入與內部服務相同的虛擬網路，在此環境中執行的應用程式即可存取這些內部服務，包括可透過[站台對站台][SiteToSite]和 [Azure ExpressRoute][ExpressRoute] 連線聯繫的端點。</span><span class="sxs-lookup"><span data-stu-id="23a48-140">Once an App Service Environment is joined to the same virtual network as the internal services, apps running in the environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="23a48-141">如需 App Service Environment 如何搭配虛擬網路和內部部署網路使用的詳細資訊，請參閱下列文章：[網路架構][NetworkArchitectureOverview]、[控制輸入流量][ControllingInboundTraffic]和[安全地連接到後端][SecurelyConnectingToBackends]。</span><span class="sxs-lookup"><span data-stu-id="23a48-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult the following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting to Backends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="23a48-142">開始使用</span><span class="sxs-lookup"><span data-stu-id="23a48-142">Getting started</span></span>
<span data-ttu-id="23a48-143">若要開始使用 App Service 環境，請參閱[如何建立 App Service 環境][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="23a48-143">To get started with App Service Environments, see [How To Create An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="23a48-144">您可以在 [應用程式服務環境的讀我檔案](../app-service/app-service-app-service-environments-readme.md)中取得 App Service 環境的所有相關文章與做法。</span><span class="sxs-lookup"><span data-stu-id="23a48-144">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="23a48-145">如需有關 Azure App Service 平台的詳細資訊，請參閱 [Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="23a48-145">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="23a48-146">如需 App Service Environment 網路架構的概觀，請參閱[網路架構概觀][NetworkArchitectureOverview]一文。</span><span class="sxs-lookup"><span data-stu-id="23a48-146">For an overview of the App Service Environment network architecture, see the [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="23a48-147">如需搭配 ExpressRoute 使用 App Service Environment 的詳細資訊，請參閱 [Express Route 與 App Service Environment][NetworkConfigDetailsForExpressRoute]一文。</span><span class="sxs-lookup"><span data-stu-id="23a48-147">For details on using an App Service Environment with ExpressRoute, see the following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


