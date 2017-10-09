---
title: "aaaIntroduction tooApp Service 環境 v1"
description: "深入了解 hello App Service 環境 v1 功能，可提供安全、 VNet 聯結、 專用的擴充單元執行所有應用程式。"
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
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a><span data-ttu-id="981e7-103">簡介 tooApp Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="981e7-103">Introduction tooApp Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="981e7-104">這篇文章是關於 hello App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="981e7-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="981e7-105">沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。</span><span class="sxs-lookup"><span data-stu-id="981e7-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="981e7-106">有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。</span><span class="sxs-lookup"><span data-stu-id="981e7-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="981e7-107">概觀</span><span class="sxs-lookup"><span data-stu-id="981e7-107">Overview</span></span>
<span data-ttu-id="981e7-108">App Service 環境是 Azure App Service 的[高階][PremiumTier]服務方案選項，提供完全隔離的專用環境，能夠極為安全地執行 Azure App Service 應用程式，包括 [Web Apps][WebApps]、[Mobile Apps][MobileApps]和 [API Apps][APIApps]。</span><span class="sxs-lookup"><span data-stu-id="981e7-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="981e7-109">適合應用程式工作負載的 App Service 環境需要：</span><span class="sxs-lookup"><span data-stu-id="981e7-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="981e7-110">非常高的延展性</span><span class="sxs-lookup"><span data-stu-id="981e7-110">Very high scale</span></span>
* <span data-ttu-id="981e7-111">隔離和安全的網路存取</span><span class="sxs-lookup"><span data-stu-id="981e7-111">Isolation and secure network access</span></span>

<span data-ttu-id="981e7-112">客戶可以在單一 Azure 區域，以及跨多個 Azure 區域中建立多個 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="981e7-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="981e7-113">這使得 App Service 環境很適合用來水平調整無狀態應用程式層的規模，以支援高 RPS 工作負載。</span><span class="sxs-lookup"><span data-stu-id="981e7-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="981e7-114">App Service 環境隔離的 toorunning 只有單一客戶的應用程式，而且一律部署至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="981e7-114">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="981e7-115">客戶有更細微的控制網路流量都傳入和傳出應用程式，與應用程式可以建立安全的高速連線透過虛擬網路 tooon 內部公司資源。</span><span class="sxs-lookup"><span data-stu-id="981e7-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="981e7-116">所有發行項以及如何-將的有關應用程式服務環境位於 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="981e7-116">All articles and How-To's about App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="981e7-117">如需如何應用程式服務環境啟用高擴充能力和保護概觀網路存取，請參閱 hello [AzureCon 深入探討][ AzureConDeepDive]應用程式服務環境 ！</span><span class="sxs-lookup"><span data-stu-id="981e7-117">For an overview of how App Service Environments enable high scale and secure network access, see hello [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="981e7-118">深入了解水平縮放比例使用多個應用程式服務環境請參閱 hello 文件如何 toosetup[地理分散的應用程式使用量][GeodistributedAppFootprint]。</span><span class="sxs-lookup"><span data-stu-id="981e7-118">For a deep-dive on horizontally scaling using multiple App Service Environments see hello article on how toosetup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="981e7-119">toosee hello AzureCon 深入了解所示的 hello 安全性架構的設定方式，請參閱 hello 文件實作[分層安全性架構](app-service-app-service-environment-layered-security.md)與應用程式服務環境。</span><span class="sxs-lookup"><span data-stu-id="981e7-119">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="981e7-120">在 App Service 環境中執行之應用程式的存取權可能會受到 Web 應用程式防火牆 (WAF) 等上游裝置的管制。</span><span class="sxs-lookup"><span data-stu-id="981e7-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="981e7-121">上的文件： hello[應用程式服務環境中設定 WAF](app-service-app-service-environment-web-application-firewall.md)涵蓋這種情況。</span><span class="sxs-lookup"><span data-stu-id="981e7-121">hello article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="981e7-122">專用計算資源</span><span class="sxs-lookup"><span data-stu-id="981e7-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="981e7-123">Hello 運算資源的應用程式服務環境中的所有專用專門 tooa 單一訂用帳戶，而且 App Service 環境可以設定 toofifty (50) 計算資源，專供單一應用程式。</span><span class="sxs-lookup"><span data-stu-id="981e7-123">All of hello compute resources in an App Service Environment are dedicated exclusively tooa single subscription, and an App Service Environment can be configured with up toofifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="981e7-124">App Service 環境是由前端的計算資源集區，以及一個 toothree 工作者計算資源集區所組成。</span><span class="sxs-lookup"><span data-stu-id="981e7-124">An App Service Environment is composed of a front-end compute resource pool, as well as one toothree worker compute resource pools.</span></span> 

<span data-ttu-id="981e7-125">hello 前端集區包含負責為 App Service 環境內的應用程式要求的格式自動負載平衡 SSL 終止的計算資源。</span><span class="sxs-lookup"><span data-stu-id="981e7-125">hello front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="981e7-126">每個背景工作集區包含計算資源配置太[應用程式服務方案][AppServicePlan]，其中又包含一或多個 Azure App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="981e7-126">Each worker pool contains compute resources allocated too[App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="981e7-127">因為可能有向上 toothree 不同的背景工作集區的 App Service 環境中，您會有每個背景工作集區 hello 彈性 toochoose 不同的計算資源。</span><span class="sxs-lookup"><span data-stu-id="981e7-127">Since there can be up toothree different worker pools in an App Service Environment, you have hello flexibility toochoose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="981e7-128">比方說，這可讓您使用的較不強大的運算資源 toocreate 一個背景工作集區的應用程式服務方案適用於開發或測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="981e7-128">For example, this allows you toocreate one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="981e7-129">第二個 (或甚至第三個) 背景工作集區可以使用比較強大的運算資源，以供 App Service 方案執行生產應用程式。</span><span class="sxs-lookup"><span data-stu-id="981e7-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="981e7-130">如需有關 hello 數量運算資源可用 toohello 前端和背景工作集區的詳細資訊，請參閱[如何 tooConfigure App Service 環境][HowToConfigureanAppServiceEnvironment]。</span><span class="sxs-lookup"><span data-stu-id="981e7-130">For more details on hello quantity of compute resources available toohello front-end and worker pools, see [How tooConfigure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="981e7-131">針對詳細資料上可用的 hello 計算 App Service 環境中支援的資源大小，請參閱 hello[應用程式服務定價][ AppServicePricing]頁面上，並檢閱應用程式服務環境的 hello 可用選項在 [hello Premium 定價層。</span><span class="sxs-lookup"><span data-stu-id="981e7-131">For details on hello available compute resource sizes supported in an App Service Environment, consult hello [App Service Pricing][AppServicePricing] page and review hello available options for App Service Environments in hello Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="981e7-132">虛擬網路支援</span><span class="sxs-lookup"><span data-stu-id="981e7-132">Virtual Network Support</span></span>
<span data-ttu-id="981e7-133">App Service Environment 可以在 Azure Resource Manager 虛擬網路或者傳統式部署模型虛擬網路其中之一中建立 ([更多有關虛擬網路的資訊][MoreInfoOnVirtualNetworks])。</span><span class="sxs-lookup"><span data-stu-id="981e7-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="981e7-134">因為在虛擬網路中，永遠存在 App Service 環境及更精確地說內的虛擬網路子網路，您可以利用 hello 安全性功能的虛擬網路 toocontrol 這兩個輸入和輸出的網路通訊。</span><span class="sxs-lookup"><span data-stu-id="981e7-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage hello security features of virtual networks toocontrol both inbound and outbound network communications.</span></span>  

<span data-ttu-id="981e7-135">App Service Environment 可以是具有公用 IP 位址的網際網路對向，或只具有 Azure 內部負載平衡器 (ILB) 位址的內部對向。</span><span class="sxs-lookup"><span data-stu-id="981e7-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="981e7-136">您可以使用[網路安全性群組][ NetworkSecurityGroups] toorestrict 輸入 App Service 環境的所在位置的網路通訊 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="981e7-136">You can use [network security groups][NetworkSecurityGroups] toorestrict inbound network communications toohello subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="981e7-137">這可讓您 toorun 背後上游的裝置和服務，例如 web 應用程式防火牆和網路 SaaS 提供者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="981e7-137">This allows you toorun apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="981e7-138">應用程式也經常會需要 tooaccess 公司資源，例如內部資料庫和 web 服務。</span><span class="sxs-lookup"><span data-stu-id="981e7-138">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="981e7-139">常見的方法是 toomake 這些端點可用的唯一 toointernal 的網路流量流入 Azure 虛擬網路內。</span><span class="sxs-lookup"><span data-stu-id="981e7-139">A common approach is toomake these endpoints available only toointernal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="981e7-140">App Service 環境一旦聯結的 toohello hello 內部服務、 在 hello 環境中執行的應用程式的相同虛擬網路可以存取它們，包括可透過連線端點[站對站][ SiteToSite]和[Azure ExpressRoute] [ ExpressRoute]連線。</span><span class="sxs-lookup"><span data-stu-id="981e7-140">Once an App Service Environment is joined toohello same virtual network as hello internal services, apps running in hello environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="981e7-141">針對應用程式服務環境的虛擬網路和內部部署網路的運作方式的更多詳細資料，請參閱下列文件的 hello[網路架構][NetworkArchitectureOverview]，[控制輸入流量][ControllingInboundTraffic]，和[安全地連接 tooBackends][SecurelyConnectingToBackends]。</span><span class="sxs-lookup"><span data-stu-id="981e7-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult hello following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting tooBackends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="981e7-142">開始使用</span><span class="sxs-lookup"><span data-stu-id="981e7-142">Getting started</span></span>
<span data-ttu-id="981e7-143">tooget 開始使用應用程式服務環境中，請參閱[如何 tooCreate App Service 環境][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="981e7-143">tooget started with App Service Environments, see [How tooCreate An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="981e7-144">所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="981e7-144">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="981e7-145">如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="981e7-145">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="981e7-146">如需 hello App Service 環境的網路架構的概觀，請參閱 hello[網路架構概觀][ NetworkArchitectureOverview]發行項。</span><span class="sxs-lookup"><span data-stu-id="981e7-146">For an overview of hello App Service Environment network architecture, see hello [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="981e7-147">如需透過 ExpressRoute，使用 App Service 環境的詳細資訊，請參閱下列文章 hello [Express Route 和應用程式服務環境][NetworkConfigDetailsForExpressRoute]。</span><span class="sxs-lookup"><span data-stu-id="981e7-147">For details on using an App Service Environment with ExpressRoute, see hello following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

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


