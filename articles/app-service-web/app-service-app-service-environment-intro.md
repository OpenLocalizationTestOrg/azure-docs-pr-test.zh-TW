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
# <a name="introduction-tooapp-service-environment-v1"></a>簡介 tooApp Service 環境 v1

> [!NOTE]
> 這篇文章是關於 hello App Service 環境 v1。  沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。 有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。
> 

## <a name="overview"></a>概觀
App Service 環境是 Azure App Service 的[高階][PremiumTier]服務方案選項，提供完全隔離的專用環境，能夠極為安全地執行 Azure App Service 應用程式，包括 [Web Apps][WebApps]、[Mobile Apps][MobileApps]和 [API Apps][APIApps]。  

適合應用程式工作負載的 App Service 環境需要：

* 非常高的延展性
* 隔離和安全的網路存取

客戶可以在單一 Azure 區域，以及跨多個 Azure 區域中建立多個 App Service 環境。  這使得 App Service 環境很適合用來水平調整無狀態應用程式層的規模，以支援高 RPS 工作負載。

App Service 環境隔離的 toorunning 只有單一客戶的應用程式，而且一律部署至虛擬網路。  客戶有更細微的控制網路流量都傳入和傳出應用程式，與應用程式可以建立安全的高速連線透過虛擬網路 tooon 內部公司資源。

所有發行項以及如何-將的有關應用程式服務環境位於 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。

如需如何應用程式服務環境啟用高擴充能力和保護概觀網路存取，請參閱 hello [AzureCon 深入探討][ AzureConDeepDive]應用程式服務環境 ！

深入了解水平縮放比例使用多個應用程式服務環境請參閱 hello 文件如何 toosetup[地理分散的應用程式使用量][GeodistributedAppFootprint]。

toosee hello AzureCon 深入了解所示的 hello 安全性架構的設定方式，請參閱 hello 文件實作[分層安全性架構](app-service-app-service-environment-layered-security.md)與應用程式服務環境。

在 App Service 環境中執行之應用程式的存取權可能會受到 Web 應用程式防火牆 (WAF) 等上游裝置的管制。  上的文件： hello[應用程式服務環境中設定 WAF](app-service-app-service-environment-web-application-firewall.md)涵蓋這種情況。 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>專用計算資源
Hello 運算資源的應用程式服務環境中的所有專用專門 tooa 單一訂用帳戶，而且 App Service 環境可以設定 toofifty (50) 計算資源，專供單一應用程式。

App Service 環境是由前端的計算資源集區，以及一個 toothree 工作者計算資源集區所組成。 

hello 前端集區包含負責為 App Service 環境內的應用程式要求的格式自動負載平衡 SSL 終止的計算資源。 

每個背景工作集區包含計算資源配置太[應用程式服務方案][AppServicePlan]，其中又包含一或多個 Azure App Service 應用程式。  因為可能有向上 toothree 不同的背景工作集區的 App Service 環境中，您會有每個背景工作集區 hello 彈性 toochoose 不同的計算資源。  

比方說，這可讓您使用的較不強大的運算資源 toocreate 一個背景工作集區的應用程式服務方案適用於開發或測試應用程式。  第二個 (或甚至第三個) 背景工作集區可以使用比較強大的運算資源，以供 App Service 方案執行生產應用程式。

如需有關 hello 數量運算資源可用 toohello 前端和背景工作集區的詳細資訊，請參閱[如何 tooConfigure App Service 環境][HowToConfigureanAppServiceEnvironment]。  

針對詳細資料上可用的 hello 計算 App Service 環境中支援的資源大小，請參閱 hello[應用程式服務定價][ AppServicePricing]頁面上，並檢閱應用程式服務環境的 hello 可用選項在 [hello Premium 定價層。

## <a name="virtual-network-support"></a>虛擬網路支援
App Service Environment 可以在 Azure Resource Manager 虛擬網路或者傳統式部署模型虛擬網路其中之一中建立 ([更多有關虛擬網路的資訊][MoreInfoOnVirtualNetworks])。  因為在虛擬網路中，永遠存在 App Service 環境及更精確地說內的虛擬網路子網路，您可以利用 hello 安全性功能的虛擬網路 toocontrol 這兩個輸入和輸出的網路通訊。  

App Service Environment 可以是具有公用 IP 位址的網際網路對向，或只具有 Azure 內部負載平衡器 (ILB) 位址的內部對向。

您可以使用[網路安全性群組][ NetworkSecurityGroups] toorestrict 輸入 App Service 環境的所在位置的網路通訊 toohello 子網路。  這可讓您 toorun 背後上游的裝置和服務，例如 web 應用程式防火牆和網路 SaaS 提供者的應用程式。

應用程式也經常會需要 tooaccess 公司資源，例如內部資料庫和 web 服務。  常見的方法是 toomake 這些端點可用的唯一 toointernal 的網路流量流入 Azure 虛擬網路內。  App Service 環境一旦聯結的 toohello hello 內部服務、 在 hello 環境中執行的應用程式的相同虛擬網路可以存取它們，包括可透過連線端點[站對站][ SiteToSite]和[Azure ExpressRoute] [ ExpressRoute]連線。

針對應用程式服務環境的虛擬網路和內部部署網路的運作方式的更多詳細資料，請參閱下列文件的 hello[網路架構][NetworkArchitectureOverview]，[控制輸入流量][ControllingInboundTraffic]，和[安全地連接 tooBackends][SecurelyConnectingToBackends]。 

## <a name="getting-started"></a>開始使用
tooget 開始使用應用程式服務環境中，請參閱[如何 tooCreate App Service 環境][HowToCreateAnAppServiceEnvironment]

所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。

如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。

如需 hello App Service 環境的網路架構的概觀，請參閱 hello[網路架構概觀][ NetworkArchitectureOverview]發行項。

如需透過 ExpressRoute，使用 App Service 環境的詳細資訊，請參閱下列文章 hello [Express Route 和應用程式服務環境][NetworkConfigDetailsForExpressRoute]。

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


