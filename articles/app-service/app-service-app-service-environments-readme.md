---
title: "aaaApp Service 環境 |Microsoft 文件"
description: "何謂 Azure App Service 環境？ 簡介 tooApp Service 環境。"
keywords: "azure app service 環境, 虛擬網路, 安全網路"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 1db5c057-3c56-4537-b580-cdd21fe3f3a7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: stefsch
ms.openlocfilehash: 1b59fed4e5a72d4c4805e1dca203747e07e77103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="ae57e-105">App Service 環境文件</span><span class="sxs-lookup"><span data-stu-id="ae57e-105">App Service Environment Documentation</span></span>
<span data-ttu-id="ae57e-106">App Service 環境是 Azure App Service 的[高階][PremiumTier]服務方案選項，提供完全隔離的專用環境，能夠極為安全地執行 Azure App Service 應用程式，包括 [Web Apps][WebApps]、[Mobile Apps][MobileApps]和 [API Apps][APIApps]。</span><span class="sxs-lookup"><span data-stu-id="ae57e-106">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="ae57e-107">適合應用程式工作負載的 App Service 環境需要：</span><span class="sxs-lookup"><span data-stu-id="ae57e-107">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="ae57e-108">非常高的延展性</span><span class="sxs-lookup"><span data-stu-id="ae57e-108">Very high scale</span></span>
* <span data-ttu-id="ae57e-109">隔離和安全的網路存取</span><span class="sxs-lookup"><span data-stu-id="ae57e-109">Isolation and secure network access</span></span>

<span data-ttu-id="ae57e-110">客戶可以在單一 Azure 區域，以及跨多個 Azure 區域中建立多個 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="ae57e-110">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="ae57e-111">這使得 App Service 環境很適合用來水平調整無狀態應用程式層的規模，以支援高 RPS 工作負載。</span><span class="sxs-lookup"><span data-stu-id="ae57e-111">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="ae57e-112">App Service 環境隔離的 toorunning 只有單一客戶的應用程式，而且一律部署至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ae57e-112">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="ae57e-113">客戶可以使用[網路安全性群組][NetworkSecurityGroups]，精確控制輸入和輸出應用程式網路流量。</span><span class="sxs-lookup"><span data-stu-id="ae57e-113">Customers have fine-grained control over both inbound and outbound application network traffic using [network security groups][NetworkSecurityGroups].</span></span>  <span data-ttu-id="ae57e-114">應用程式也可以建立安全的高速連線透過虛擬網路 tooon 內部公司資源。</span><span class="sxs-lookup"><span data-stu-id="ae57e-114">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="ae57e-115">應用程式經常需要 tooaccess 公司資源，例如內部資料庫和 web 服務。</span><span class="sxs-lookup"><span data-stu-id="ae57e-115">Apps frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="ae57e-116">只要是可透過[站對站][SiteToSite] VPN 和 [Azure ExpressRoute][ExpressRoute] 連接來取得的資源，App Service 環境上執行的應用程式都可以存取。</span><span class="sxs-lookup"><span data-stu-id="ae57e-116">Apps running on App Service Environments can access resources reachable via [Site-to-Site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* [<span data-ttu-id="ae57e-117">何謂 App Service 環境？</span><span class="sxs-lookup"><span data-stu-id="ae57e-117">What is an App Service Environment?</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
* [<span data-ttu-id="ae57e-118">建立 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="ae57e-118">Creating an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="ae57e-119">在 App Service 環境中建立應用程式</span><span class="sxs-lookup"><span data-stu-id="ae57e-119">Creating Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="ae57e-120">使用 App Service 環境建立和使用內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="ae57e-120">Creating and Using an Internal Load Balancer with App Service Environments</span></span>](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [<span data-ttu-id="ae57e-121">設定 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="ae57e-121">Configuring an App Service Environment</span></span>](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [<span data-ttu-id="ae57e-122">在 App Service 環境中調整應用程式</span><span class="sxs-lookup"><span data-stu-id="ae57e-122">Scaling Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [<span data-ttu-id="ae57e-123">網路安全性與架構</span><span class="sxs-lookup"><span data-stu-id="ae57e-123">Network Security and Architecture</span></span>](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a><span data-ttu-id="ae57e-124">作法</span><span class="sxs-lookup"><span data-stu-id="ae57e-124">How To's</span></span>
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a><span data-ttu-id="ae57e-125">影片</span><span class="sxs-lookup"><span data-stu-id="ae57e-125">Videos</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]



<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
