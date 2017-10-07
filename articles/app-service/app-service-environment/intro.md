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
# <a name="introduction-tooapp-service-environments"></a>簡介 tooApp 服務環境 #
 
## <a name="overview"></a>概觀 ##

Azure App Service Environment 是 Azure App Service 的功能，可提供完全隔離和專用的環境，以便安全地大規模執行 App Service 應用程式。 此功能可裝載 [Web 應用程式][webapps]、[行動應用程式][mobileapps]、[API 應用程式][APIapps]和[函數][Functions]。

App Service Environment (ASE) 適合需要下列項目的應用程式工作負載：

- 非常高的延展性。
- 隔離和安全的網路存取。
- 高記憶體使用率。

客戶可以在單一 Azure 區域中或跨多個 Azure 區域建立多個 ASE。 這種彈性讓 ASE 很適合用於水平調整無狀態應用程式層的規模，以支援高 RPS 的工作負載。

ASEs 隔離的 toorunning 只有單一客戶的應用程式，而且一律會部署到虛擬網路。 客戶可以精確控制輸入和輸出的應用程式網路流量。 應用程式可以建立高速的安全連接，透過 Vpn tooon 內部公司資源。

所有文件及如何-tooinstructions 有關 ASEs 位於 hello [App Service 環境的讀我檔案][ASEReadme]:

* ASE 可透過安全的網路存取，提供高延展性的應用程式裝載。 如需詳細資訊，請參閱 hello [AzureCon 深入探討](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/)ASEs 上。
* 多個 ASEs 可以水平方式是使用的 tooscale。 如需詳細資訊，請參閱[如何向上地理分散的應用程式使用量 tooset](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/)。
* 可以使用的 tooconfigure 安全性架構，ASEs，hello AzureCon 深入了解所示。 toosee hello AzureCon 深入了解所示的 hello 安全性架構的設定方式，請參閱 hello[有關的文章 tooimplement 多層式的安全性架構](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security)App Service 環境。
* 在 ASE 中執行之應用程式的存取權可能會受到 Web 應用程式防火牆 (WAF) 等上游裝置的管制。 如需詳細資訊，請參閱[設定 App Service Environment 的 WAF](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall)。

## <a name="dedicated-environment"></a>專用的環境 ##

Ase 中是專專門 tooa 單一訂用帳戶，而且可以裝載 100 個執行個體。 hello 範圍可以跨 100 個執行個體中單一應用程式服務計劃 too100 單一執行個體應用程式服務計劃，以及兩者之間的所有項目。

ASE 是由前端和背景工作角色所組成。 前端負責處理 HTTP/HTTPS 終止和 ASE 中應用程式要求的自動負載平衡。 前端會自動加入為 hello hello ASE 中的應用程式服務計劃會向外延展。

背景工作角色是裝載客戶應用程式的角色。 背景工作角色可以三個固定的大小提供：

* 單核心/3.5 GB RAM
* 雙核心/7 GB RAM
* 四核心/14 GB RAM

客戶不需要 toomanage 前端和背景工作。 所有的基礎結構會隨客戶的 App Service 方案相應放大而自動新增。 應用程式服務計劃所建立，或在 ase 中縮放，hello 必須加入或移除視基礎結構。

沒有所支付的 hello 基礎結構，並不會變更與 hello ASE hello 大小 ase 中單層每月費率。 此外，每個 App Service 方案核心都會有其成本。 在 ase 中託管的所有應用程式位於 hello 隔離定價 SKU。 如需定價的 ase 中的資訊，請參閱 hello[應用程式服務定價][ Pricing]頁面上，並檢閱 ASEs hello 可用選項。

## <a name="virtual-network-support"></a>虛擬網路支援 ##

您只能在 Azure Resource Manager 虛擬網路中建立 ASE。 toolearn 進一步了解 Azure 虛擬網路，請參閱 hello [Azure 虛擬網路常見問題集](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/)。 ASE 一律存在於虛擬網路；更精確地說，是虛擬網路的子網路內。 您可以使用 hello 安全性功能的虛擬網路 toocontrol 傳入和傳出網路通訊，您的應用程式。

ASE 可以是具有公用 IP 位址的網際網路對應，或只具有 Azure 內部負載平衡器 (ILB) 位址的內部對應。

[網路安全性群組][ NSGs]限制 ase 中的所在位置的輸入的網路通訊 toohello 子網路。 您可以使用 Nsg toorun 應用程式背後上游的裝置和服務，例如 WAFs 和網路 SaaS 提供者。

應用程式也經常會需要 tooaccess 公司資源，例如內部資料庫和 web 服務。 如果您部署的 VPN 連線 toohello 在內部部署網路的虛擬網路中的 hello ASE，hello hello ASE 中的應用程式可以存取 hello 在內部部署資源。 無論是 hello VPN，則為 true，此功能會[站對站](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/)或[Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN。

如需有關 ASE 與虛擬網路和內部部署網路搭配運作方式的詳細資訊，請參閱 [App Service Environment 的網路考量][ASENetwork]。

## <a name="app-service-environment-v1"></a>App Service 環境 v1 ##

App Service Environment 有兩個版本：ASEv1 和 ASEv2。 hello 上述資訊為基礎 ASEv2。 此區段會顯示 hello ASEv2 ASEv1 之間的差異。 

您需要 toomanage ASEv1，所有的手動 hello 資源。 含有 hello 前端、 背景工作，與用於 IP SSL 的 IP 位址。 您可以調整您的應用程式服務計劃之前，您需要 toofirst 它擴充想 toohost hello 背景工作集區。

ASEv1 使用與 ASEv2 不同的定價模式。 在 ASEv1 中，您需要支付每個配置的核心。 其中包括用於前端或未裝載任何工作負載之背景工作角色的核心。 ASEv1，在 ase 中的 hello 預設最大標尺大小會是 55 主機總計。 包括背景工作角色與前端。 一個利用 tooASEv1 是它可以部署在傳統的虛擬網路和資源管理員的虛擬網路中。 toolearn 深入了解 ASEv1，請參閱[App Service 環境 v1 簡介][ASEv1Intro]。

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
