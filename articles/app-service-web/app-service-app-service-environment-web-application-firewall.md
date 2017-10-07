---
title: "aaaConfiguring App Service 環境的 Web 應用程式防火牆 (WAF)"
description: "了解如何 tooconfigure web 應用程式防火牆前面 App Service 環境。"
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>設定 App Service 環境的 Web 應用程式防火牆 (WAF)
## <a name="overview"></a>概觀
Web 應用程式防火牆像 hello [azure Barracuda WAF](https://www.barracuda.com/programs/azure)位於 hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/)可協助您保護 web 應用程式藉由檢查傳入的 web 流量 tooblock SQL資料隱碼攻擊、 跨網站指令碼、 惡意程式碼上傳 （& s） 應用程式 DDoS 和其他攻擊。 它也會檢驗 hello 回應 hello 後端 web 伺服器中的資料遺失防護 (DLP)。 結合 hello 隔離和其他調整應用程式服務環境所提供，這樣的理想環境 toohost 商務關鍵的 web 應用程式需要 toowithstand 惡意要求和高容量的流量。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>設定
我們將會設定這個文件，而只有 hello WAF 的流量可達到 hello App Service 環境將無法再存取 hello DMZ 從多個負載背後我們 App Service 環境之間取得平衡 Barracuda WAF 的執行個體。 我們也會有我們 Barracuda WAF 執行個體 tooload 平衡前面的 Azure 流量管理員跨 Azure 資料中心和區域。 Hello 安裝程式的高層級圖表看起來會像下面顯示的內容。

![架構][Architecture] 

> 注意： 與 hello 引進[App Service 環境的支援 ILB](app-service-environment-with-internal-load-balancer.md)，您可以設定 hello ASE toobe 存取 hello 周邊網路，只能使用 toohello 私人網路。 
> 
> 

## <a name="configuring-your-app-service-environment"></a>設定 App Service 環境
tooconfigure App Service 環境參考太[文件](app-service-web-how-to-create-an-app-service-environment.md)hello 主旨。 建立 App Service 環境之後，您可以建立[Web 應用程式](app-service-web-overview.md)， [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md)和[行動應用程式](../app-service-mobile/app-service-mobile-value-prop.md)在此環境中，將所有會受到保護後 hello WAF 我們設定 hello 下一節。

## <a name="configuring-your-barracuda-waf-cloud-service"></a>設定 Barracuda WAF 雲端服務
Barracuda 具有在 Azure 中於虛擬機器上部署其 WAF 的 [詳細文章](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) 。 但因為我們想要的備援性，而且導入單一失敗點，您會想成 hello toodeploy 至少 2 WAF 執行個體 Vm 相同的雲端服務時遵循下列指示。

### <a name="adding-endpoints-toocloud-service"></a>加入端點 tooCloud 服務
一旦您擁有 2 或您的雲端服務中的多個 WAF VM 執行個體，您就可以使用 hello [Azure 入口網站](https://portal.azure.com/)hello 圖所示，應用程式所使用的 tooadd HTTP 和 HTTPS 端點。

![設定端點][ConfigureEndpoint]

如果您的應用程式使用其他端點，請確定 tooadd 這些 toothis 清單。 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>透過管理入口網站設定 Barracuda WAF
Barracuda WAF 使用 TCP 連接埠 8000，以透過其管理入口網站進行設定。 由於我們有多個執行個體的 hello WAF Vm 必須 toorepeat hello 步驟的每個 VM 執行個體。 

> 附註： 一旦您完成 WAF 組態之後，移除 hello TCP/8000 端點從所有您 WAF Vm tookeep 您 WAF 安全。
> 
> 

加入所示 hello 圖 tooconfigure Barracuda WAF hello 管理端點。

![加入管理端點][AddManagementEndpoint]

在您的雲端服務上使用瀏覽器 toobrowse toohello 管理端點。 如果您的雲端服務呼叫 test.cloudapp.net，您會藉由瀏覽 toohttp://test.cloudapp.net:8000 存取此端點。 登入頁面。 您應該會看到類似下面的，您可以使用登入您在 hello WAF VM 安裝階段中指定的認證。

![管理登入頁面][ManagementLoginPage]

一次您登入您應該會看到儀表板為 hello 中 hello 映像，請在下方將會顯示 hello WAF 保護的相關基本統計資料。

![管理儀表板][ManagementDashboard]

按一下 hello 服務索引標籤可讓您設定您 WAF 保護服務。 如需設定 Barracuda WAF 的詳細資料，您可以查閱 [其文件](https://techlib.barracuda.com/waf/getstarted1)。 Hello 下例 Azure Web 應用程式中已設定服務 HTTP 和 HTTPS 上的流量。

![管理加入服務][ManagementAddServices]

> 注意： 根據您的應用程式的設定方式，和 App Service 環境中使用的功能，您需要 tooforward 流量的 TCP 通訊埠 80 和 443 以外例如如果 IP SSL 設定的 Web 應用程式。 如需應用程式服務環境中使用的網路連接埠的清單，請參閱太[文件控制項連入流量](app-service-app-service-environment-control-inbound-traffic.md)網路連接埠 > 一節。
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>設定 Microsoft Azure 流量管理員 (選擇性)
如果您的應用程式可在多個區域，則您會想 tooload 平衡它們背後[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)。 讓您加入端點中 hello toodo [Azure 傳統入口網站](https://manage.azure.com)hello 圖所示，在 hello Traffic Manager 設定檔中使用您 WAF hello 雲端服務名稱。 

![流量管理員端點][TrafficManagerEndpoint]

如果您的應用程式需要驗證，請確定您有不需要進行任何驗證的應用程式的 hello 可用性的 Traffic Manager tooping 某些資源。 您可以設定下 hello 設定 區段中的 hello URL 上 hello [Azure 傳統入口網站](https://manage.azure.com)如下所示。

![設定流量管理員][ConfigureTrafficManager]

tooforward hello Traffic Manager ping 從 WAF tooyour 應用程式，您會需要 toosetup 網站翻譯應用程式上 Barracuda WAF tooforward 流量 tooyour hello 下面範例所示。

![網站轉譯][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>保護流量 tooApp 服務環境使用網路安全性群組群組 (NSG)
請遵循 hello[控制項連入流量文件](app-service-app-service-environment-control-inbound-traffic.md)為限制的詳細資訊只要使用您的雲端服務的 hello VIP 位址流量從 hello WAF tooyour App Service 環境。 以下是針對 TCP 通訊埠 80 執行這項工作的範例 Powershell 命令。

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Hello SourceAddressPrefix 取代 hello WAF 的雲端服務的虛擬 IP 位址 (VIP)。

> 注意： 當您刪除然後重新建立 hello 雲端服務，將會變更 hello VIP 的雲端服務。 請確定 tooupdate hello IP 位址在這樣做之後，hello 網路資源群組中的。 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
