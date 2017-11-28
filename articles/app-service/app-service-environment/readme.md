---
title: "aaaAzure App Service 環境讀我檔案"
description: "列出描述 Azure App Service 環境的 hello 文件"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 6edc74804ded7497e70c31c9e08252257add4415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="0ce55-103">App Service Environment 環境文件</span><span class="sxs-lookup"><span data-stu-id="0ce55-103">App Service environment documentation</span></span>
 <span data-ttu-id="0ce55-104">Azure App Service Environment 是 Azure App Service 的功能，可提供完全隔離和專用的環境，以便安全地大規模執行 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ce55-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="0ce55-105">此功能可裝載 [Web 應用程式][webapps]、[行動裝置應用程式][mobileapps]、[API 應用程式][APIApps]及[函式][Functions]。</span><span class="sxs-lookup"><span data-stu-id="0ce55-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="0ce55-106">適合應用程式工作負載的 App Service Environment (ASE) 需要：</span><span class="sxs-lookup"><span data-stu-id="0ce55-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="0ce55-107">非常高的延展性。</span><span class="sxs-lookup"><span data-stu-id="0ce55-107">Very high scale.</span></span>
* <span data-ttu-id="0ce55-108">隔離和安全的網路存取。</span><span class="sxs-lookup"><span data-stu-id="0ce55-108">Isolation and secure network access.</span></span>

<span data-ttu-id="0ce55-109">客戶可以在單一 Azure 區域中和跨多個 Azure 區域建立多個 ASE。</span><span class="sxs-lookup"><span data-stu-id="0ce55-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="0ce55-110">這種靈活性讓 ASE 很適合用於水平調整無狀態應用程式層的規模，以支援高 RPS 的工作負載。</span><span class="sxs-lookup"><span data-stu-id="0ce55-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="0ce55-111">ASEs 隔離的 toorunning 只有單一客戶的應用程式，而且一律會部署到 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0ce55-111">ASEs are isolated toorunning only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="0ce55-112">客戶可以使用[網路安全性群組][NSGs]，同時精確控制輸入和輸出應用程式網路流量。</span><span class="sxs-lookup"><span data-stu-id="0ce55-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="0ce55-113">應用程式也可以建立安全的高速連線透過虛擬網路 tooon 內部公司資源。</span><span class="sxs-lookup"><span data-stu-id="0ce55-113">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="0ce55-114">應用程式經常需要 tooaccess 公司資源，例如內部資料庫和 web 服務。</span><span class="sxs-lookup"><span data-stu-id="0ce55-114">Apps frequently need tooaccess corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="0ce55-115">執行於 ASE 上的應用程式可透過[站對站][SiteToSite] VPN 連線和[Azure ExpressRoute][ExpressRoute] 連線來存取資源。</span><span class="sxs-lookup"><span data-stu-id="0ce55-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="0ce55-116">[何謂 App Service Environment？][Intro]</span><span class="sxs-lookup"><span data-stu-id="0ce55-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="0ce55-117">[建立 App Service Environment][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="0ce55-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="0ce55-118">[建立內部負載平衡器 App Service Environment][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="0ce55-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="0ce55-119">[使用 App Service Environment][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="0ce55-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="0ce55-120">[網路考量和 hello App Service 環境][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="0ce55-120">[Networking considerations and hello App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="0ce55-121">[從範本建立 App Service Environment][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="0ce55-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="0ce55-122">影片</span><span class="sxs-lookup"><span data-stu-id="0ce55-122">Videos</span></span>
<span data-ttu-id="0ce55-123">Hello 企業版與 Azure 應用程式服務的主要現代化 PaaS</span><span class="sxs-lookup"><span data-stu-id="0ce55-123">Master Modern PaaS for hello Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="0ce55-124">部署高度可擴充且安全的應用程式</span><span class="sxs-lookup"><span data-stu-id="0ce55-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="0ce55-125">在 Azure App Service 上執行企業 Web 和行動裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="0ce55-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="0ce55-126">App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="0ce55-126">App Service Environment v1</span></span> ##
<span data-ttu-id="0ce55-127">App Service Environment 有兩個版本：ASEv1 和 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="0ce55-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="0ce55-128">如需 ASEv1 的資訊，請參閱 [App Service Environment v1 文件][ASEv1README]。</span><span class="sxs-lookup"><span data-stu-id="0ce55-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


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
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
