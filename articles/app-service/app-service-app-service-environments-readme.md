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
# <a name="app-service-environment-documentation"></a>App Service 環境文件
App Service 環境是 Azure App Service 的[高階][PremiumTier]服務方案選項，提供完全隔離的專用環境，能夠極為安全地執行 Azure App Service 應用程式，包括 [Web Apps][WebApps]、[Mobile Apps][MobileApps]和 [API Apps][APIApps]。  

適合應用程式工作負載的 App Service 環境需要：

* 非常高的延展性
* 隔離和安全的網路存取

客戶可以在單一 Azure 區域，以及跨多個 Azure 區域中建立多個 App Service 環境。  這使得 App Service 環境很適合用來水平調整無狀態應用程式層的規模，以支援高 RPS 工作負載。

App Service 環境隔離的 toorunning 只有單一客戶的應用程式，而且一律部署至虛擬網路。  客戶可以使用[網路安全性群組][NetworkSecurityGroups]，精確控制輸入和輸出應用程式網路流量。  應用程式也可以建立安全的高速連線透過虛擬網路 tooon 內部公司資源。

應用程式經常需要 tooaccess 公司資源，例如內部資料庫和 web 服務。  只要是可透過[站對站][SiteToSite] VPN 和 [Azure ExpressRoute][ExpressRoute] 連接來取得的資源，App Service 環境上執行的應用程式都可以存取。

* [何謂 App Service 環境？](../app-service-web/app-service-app-service-environment-intro.md)
* [建立 App Service 環境](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [在 App Service 環境中建立應用程式](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [使用 App Service 環境建立和使用內部負載平衡器](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [設定 App Service 環境](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [在 App Service 環境中調整應用程式](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [網路安全性與架構](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a>作法
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a>影片
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
