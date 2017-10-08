---
title: "Azure App Service 環境 aaaNetworking 考量"
description: "說明 hello ASE 網路流量以及 tooset Nsg 和 UDRs 與您 ASE"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 955a4d84-94ca-418d-aa79-b57a5eb8cb85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ccompy
ms.openlocfilehash: d4d3000f4d4d75814b1e6d47079d967334eb1a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-an-app-service-environment"></a>App Service Environment 的網路考量 #

## <a name="overview"></a>概觀 ##

 Azure [App Service Environment][Intro] 是將 Azure App Service 部署到您 Azure 虛擬網路 (VNet) 中子網路的一種部署。 App Service Environment (ASE) 有二種部署類型：

- **外部 ASE**： 公開 hello ASE 裝載應用程式的可存取網際網路的 IP 位址。 如需詳細資訊，請參閱[建立外部 ASE][MakeExternalASE]。
- **ILB ASE**： 公開 hello ASE 裝載您的 VNet 內的 IP 位址上的應用程式。 內部負載平衡器 (ILB)，這就是為什麼它稱為 ILB ASE hello 內部端點。 如需詳細資訊，請參閱[建立和使用 ILB ASE][MakeILBASE]。

App Service Environment 現在有兩個版本：ASEv1 和 ASEv2。 如需 ASEv1 資訊，請參閱[簡介 tooApp Service 環境 v1][ASEv1Intro]。 ASEv1 可以部署至傳統或 Resource Manager VNet 中。 ASEv2 只能部署至 Resource Manager VNet 中。

從 ase 中移 toohello 的所有呼叫網際網路都離開 hello VNet 透過 hello ASE 指派的 VIP。 hello 此 VIP 的公用 IP 然後 hello 的來源 IP 是從 hello ASE 移 toohello 的所有呼叫網際網路。 如果您 ASE 中的 hello 應用程式進行呼叫 tooresources VNet 中或透過 VPN，hello 來源 IP 是 hello 的由您 ASE hello 子網路中 Ip 的其中一個。 因為 hello ASE hello VNet 內，它也可以存取 hello VNet，而不需要任何額外的設定中的資源。 如果 hello VNet 連接的 tooyour 在內部部署網路，您 ASE 中的應用程式也那里可以存取 tooresources。 您不需要 tooconfigure hello ASE 或您的應用程式任何進一步。

![外部 ASE][1] 

如果您有外部 ASE，hello 公用 VIP 也是 ASE 應用程式解決 toofor hello 端點：

* HTTP/S。 
* FTP/S。 
* Web 部署。
* 遠端偵錯。

![ILB ASE][2]

如果您有 ILB ASE，hello ILB 的 IP 位址會是 hello 的 HTTP/S、 FTP/S、 web 部署和遠端偵錯的 hello 端點。

hello 一般應用程式存取連接埠是：

| 使用 | 從 | 太|
|----------|---------|-------------|
|  HTTP/HTTPS  | 可由使用者設定 |  80、443 |
|  FTP/FTPS    | 可由使用者設定 |  21、990、10001-10020 |
|  Visual Studio 遠端偵錯  |  可由使用者設定 |  4016、4018、4020、4022 |

這適用於您位於外部 ASE 或 ILB ASE 上的情況。 如果您在外部 ase 中，您會遇到 hello 公用 VIP 的這些通訊埠。 如果您在 ILB ase 中，您會遇到 hello ILB 這些通訊埠。 若您鎖定連接埠 443，則可能會影響某些 hello 入口網站中公開的功能。 如需詳細資訊，請參閱[入口網站相依性](#portaldep)。

## <a name="ase-dependencies"></a>ASE 相依性 ##

ASE 輸入存取相依性為：

| 使用 | 從 | 太|
|-----|------|----|
| 管理 | App Service 管理位址 | ASE 子網路：454、455 |
|  ASE 內部通訊 | ASE 子網路：所有連接埠 | ASE 子網路：所有連接埠
|  允許 Azure Load Balancer 輸入 | Azure Load Balancer | ASE 子網路：所有連接埠
|  應用程式指派的 IP 位址 | 應用程式指派的位址 | ASE 子網路：所有連接埠

hello 輸入的流量提供命令和控制的 hello ASE 中新增 toosystem 監視。 此流量的 hello 來源 Ip 會列在 hello [ASE 管理位址][ ASEManagement]文件。 hello 網路安全性設定必須從所有 Ip 連接埠 454 和 455 上 tooallow 存取。

Hello ASE 子網路有許多連接埠所使用的內部元件通訊，以及他們可以變更。  這需要所有的 hello hello ASE 子網路 toobe 存取從 hello ASE 子網路中的連接埠。 

Hello 和之間的通訊 hello Azure 負載平衡器 hello ASE 子網路 hello 最小連接埠開啟該需要 toobe 為 454、 455 和 16001。 保持運作流量 hello 負載平衡器與 hello ASE 之間會使用 hello 16001 連接埠。 如果您使用 ILB ase 中，您可以鎖定下 toojust hello 454，455，16001 連接埠的流量。  如果您使用外部 ase 中則需要 tootake 到帳戶 hello 一般應用程式存取連接埠。  如果您使用的指派的應用程式位址則需要 tooopen 它 tooall 連接埠。  將位址指派 tooa 特定的應用程式，然後 hello 負載平衡器將會使用預先 toosend HTTP 和 HTTPS 流量 toohello ASE 未知的連接埠。

如果您使用指派的應用程式的 IP 位址則需要 tooallow hello Ip 指派 tooyour 應用程式 toohello ASE 子網路流量。

對於輸出存取，ASE 取決於多個外部系統。 這些系統相依性所定義的 DNS 名稱，而不要對應 tooa 固定的一組 IP 位址。 因此，hello ASE 必須能夠存取外部 hello ASE 子網路 tooall 從各種不同的連接埠上的外部 Ip。 Ase 中具有下列輸出相依性的 hello:

| 使用 | 從 | 太|
|-----|------|----|
| Azure 儲存體 | ASE 子網路 | table.core.windows.net、blob.core.windows.net、queue.core.windows.net、file.core.windows.net：80、443、445 (只有 ASEv1 才需要 445) |
| Azure SQL Database | ASE 子網路 | database.windows.net：1433、11000-11999、14000-14999 (如需詳細資訊，請參閱 [SQL Database V12 連接埠用法](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md))|
| Azure 管理 | ASE 子網路 | management.core.windows.net、management.azure.com：443 
| SSL 憑證驗證 |  ASE 子網路            |  ocsp.msocsp.com、mscrl.microsoft.com、crl.microsoft.com：443
| Azure Active Directory        | ASE 子網路            |  網際網路：443
| App Service 管理        | ASE 子網路            |  網際網路：443
| Azure DNS                     | ASE 子網路            |  網際網路：53
| ASE 內部通訊    | ASE 子網路：所有連接埠 |  ASE 子網路：所有連接埠

如果 hello ASE 失去存取 toothese 相依性，它會停止運作。 發生的長時間不夠，hello ASE 已暫停。

### <a name="customer-dns"></a>客戶 DNS ###

如果 hello 的 VNet 設定的客戶定義的 DNS 伺服器，hello 租用戶工作負載會使用它。 hello ASE 仍然需要使用 Azure DNS toocommunicate 進行管理。 

如果 hello 的 VNet 設定的 DNS 客戶上 hello VPN 的另一端，hello DNS 伺服器必須是包含 hello ASE hello 子網路觸達。

<a name="portaldep"></a>

## <a name="portal-dependencies"></a>入口網站相依性 ##

在加法 toohello ASE 功能相依性，有幾個額外的項目相關的 toohello 入口網站體驗。 部份 hello Azure 入口網站中的 hello 功能取決於直接存取 too_SCM site_。 Azure App Service 中的每個應用程式都有兩個 URL。 hello 第一個 URL 是 tooaccess 您的應用程式。 hello 第二個 URL 是 tooaccess hello SCM 站台，這也稱為 hello _Kudu 主控台_。 使用 hello SCM 站台的功能包括：

-   Web Job
-   Functions
-   記錄串流
-   Kudu
-   擴充功能
-   處理序總管
-   主控台

當您使用 ILB ASE 時，hello SCM 站台不是從 hello VNet 之外存取網際網路。 當您的應用程式裝載於 ILB ase 中時，某些功能將無法運作，從 hello 入口網站。  

許多相依於 hello SCM 站台的這些功能也會提供直接在 hello Kudu 主控台中。 您可以連接 tooit 直接而不是使用 hello 入口網站。 如果您的應用程式裝載在 ILB ase 中，使用在您發行認證 toosign。 hello URL tooaccess hello SCM 的站台在 ILB ase 中裝載的應用程式具有下列格式的 hello: 

```
<appname>.scm.<domain name hello ILB ASE was created with> 
```

如果 ILB ASE hello 網域名稱*contoso.net*和您的應用程式名稱是*testapp*，hello 應用程式已達*testapp.contoso.net*。 hello SCM 站台，它會在達到*testapp.scm.contoso.net*。

### <a name="functions-and-web-jobs"></a>函式和 Web 工作 ###

函式和 Web 工作相依於 hello SCM 站台，但即使您的應用程式中 ILB ase 中，只要您的瀏覽器可以到達 hello SCM 站台支援在 hello 入口網站使用。  如果您使用 ILB ASE 使用自我簽署的憑證，您將需要 tooenable 憑證您瀏覽器 tootrust。  IE 與表示 hello 憑證的邊緣具有 toobe 在 hello 電腦信任存放區。  如果您使用 Chrome，則這表示您接受 hello 瀏覽器中的 hello 憑證稍早假定直接叫用 hello scm 站台。  hello 最好的解決方案是 toouse hello 瀏覽器信任鏈結中的商業憑證。  

## <a name="ase-ip-addresses"></a>ASE IP 位址 ##

Ase 中有幾個 IP 位址 toobe 留意。 如下：

- **公用輸入 IP 位址**：用於外部 ASE 中的應用程式流量，以及外部 ASE 和 ILB ASE 中的管理流量。
- **輸出的公用 IP**： 做為 hello"from"IP hello ASE 傳出連線該保持 hello VNet，這不 VPN 下路由傳送。
- **ILB IP 位址**：如果您是使用 ILB ASE。
- **應用程式指派之以 IP 為主的 SSL 位址**：只有在使用外部 ASE 並已設定以 IP 為主的 SSL 時才能使用。

所有這些 IP 位址會輕鬆地顯示在 ASEv2 hello Azure 入口網站中從 hello ASE UI。 如果您有 ILB ase 中時，會列出 hello hello ILB 的 IP。

![IP 位址][3]

### <a name="app-assigned-ip-addresses"></a>應用程式指派的 IP 位址 ###

使用外部 ase 中，您可以指派 IP 位址 tooindividual 應用程式。 您無法在 ILB ASE 的情況下那樣做。 如需有關如何 tooconfigure 應用程式 toohave 它自己的 IP 位址，請參閱[繫結現有自訂 SSL 憑證 tooAzure web 應用程式](../../app-service-web/app-service-web-tutorial-custom-ssl.md)。

當應用程式有它自己的 IP SSL 位址時，hello ASE 會保留兩個連接埠 toomap toothat IP 位址。 一個連接埠是 HTTP 流量，hello 其他連接埠是 https。 這些連接埠會列在 hello ASE hello IP 位址區段中的 UI。 流量必須是能夠 tooreach 這些連接埠的 hello VIP 或 hello 應用程式都無法存取。 這項需求是重要 tooremember，當您設定網路安全性群組 (Nsg)。

## <a name="network-security-groups"></a>網路安全性群組 ##

[網路安全性群組][ NSGs]提供 hello 能力 toocontrol VNet 中的網路存取。 當您使用 hello 入口網站時，就會隱含拒絕規則在 hello 最低優先順序 toodeny 的所有項目。 您所建立的是您的允許規則。

在 ase 中，您不需要存取 toohello Vm 使用 toohost hello ASE 本身。 它們處於由 Microsoft 管理的訂用帳戶之中。 如果您想在 hello ASE toorestrict 存取 toohello 應用程式，設定 Nsg hello ASE 子網路上。 這樣做，請特別注意 toohello ASE 相依性。 如果您封鎖任何相依性，hello ASE 會停止運作。

透過 hello Azure 入口網站或 PowerShell，可以設定 Nsg。 這裡 hello 資訊會顯示 hello Azure 入口網站。 您建立和管理 Nsg hello 入口網站中，為受到最上層資源**網路**。

當 hello 輸入和輸出需求會納入考量時，hello Nsg 看起來應該類似這個範例所示的 toohello Nsg。 hello VNet 位址範圍是_192.168.250.0/16_，而且 hello 子網路中的 hello ASE _192.168.251.128/25_。

hello 前兩個輸入的需求 hello ASE toofunction 會顯示在 hello 在此範例中的 hello 清單最上方。 它們啟用 ASE 管理，並允許 hello ASE toocommunicate 與其本身。 hello 其他項目可設定的所有租用戶都與可控制網路存取 toohello ASE 裝載應用程式。 

![輸入安全性規則][4]

預設規則可讓 hello VNet tootalk toohello ASE 子網路中的 hello Ip。 另一個預設規則可讓 hello 負載平衡器，也稱為 hello 公用 VIP，以 hello ASE toocommunicate。 toosee hello 預設規則，選取**預設規則**下一步 toohello**新增**圖示。 如果您將的拒絕所有其他項目規則 hello NSG 規則顯示之後，您可以防止 hello VIP 與 hello ASE 之間的流量。 tooprevent 流量從內部 hello VNet，新增您自己的規則 tooallow 輸入。 來源相等 tooAzureLoadBalancer 用於目的地為**任何**，而且連接埠範圍為 **\*** 。 Hello NSG 規則是套用的 toohello ASE 子網路，因為您不需要 toobe 特定 hello 目的地中。

如果您指派的 IP 位址 tooyour 應用程式，請確定您開啟的連接埠的 hello。 toosee hello 連接埠，選取**App Service 環境** > **IP 位址**。  

需要所有 hello 遵循規則的輸出所示的 hello 項目，除了 hello 最後一個項目。 它們可讓網路存取 toohello ASE 相依性已依照本文稍早記下。 如果封鎖它們任何一項，ASE 會停止運作。 hello hello 清單中的最後一個項目可讓您 ASE toocommunicate，與您的 VNet 中的其他資源。

![輸出安全性規則][5]

Nsg 定義後，請將它們指派您 ASE 所在 toohello 子網路。 如果您不記得 hello ASE VNet 或子網路，您可以從 hello ASE 管理入口網站中看到它。 tooassign hello NSG tooyour 子網路 toohello 子網路 UI，請選取 hello NSG。

## <a name="routes"></a>路由 ##

路由最常在您使用 Azure ExpressRoute 設定 VNet 時造成問題。 VNet 中有三種類型的路由：

-   系統路由
-   BGP 路由
-   使用者定義的路由 (UDR)

BGP 路由會覆寫系統路由。 UDR 會覆寫 BGP 路由。 如需 Azure 虛擬網路中關於路由的詳細資訊，請參閱[使用者定義路由概觀][UDRs]。

hello Azure SQL database hello ASE 使用 toomanage hello 系統有防火牆。 它需要從 hello ASE 公用 VIP 通訊 toooriginate。 如果他們傳送 hello ExpressRoute 連接並查詢其他 IP 位址，將會拒絕從 hello ASE 連線 toohello SQL 資料庫。

如果回覆 tooincoming 管理要求會傳送 hello ExpressRoute，hello 回覆地址是 hello 原始目的地不同。 不符的情形會中斷 hello TCP 通訊。

針對 ASE toowork 時透過 ExpressRoute，您的 VNet 設定 hello 最簡單的事 toodo 是：

-   設定 ExpressRoute tooadvertise _0.0.0.0/0_。 根據預設，它會使用強制通道將所有輸出流量傳送至內部部署網路。
-   建立 UDR。 將它套用 toohello 子網路，其中包含的位址前置詞的 hello ASE _0.0.0.0/0_和下個躍點類型_網際網路_。

如果您進行這兩個變更時，源自 hello ASE 子網路的網際網路目的地流量運作不下 hello ExpressRoute 和 hello ASE 來強制。 

> [!IMPORTANT]
> hello UDR 中定義的路由必須夠特定 tootake 優先順序透過通告 hello ExpressRoute 組態的任何路由。 hello 前述範例使用 hello 廣泛 0.0.0.0/0 位址範圍。 因此有可能會不小心由使用更明確位址範圍的路由通告所覆寫。
>
> ASEs 不支援跨通告從 hello 公用互連路徑 toohello 私用對等互連路徑的路由的 ExpressRoute 組態。 已設定公用對等互連的 ExpressRoute 設定，會收到來自 Microsoft 的路由通告。 hello 公告包含 Microsoft Azure IP 位址範圍的大型集合。 如果 hello 位址範圍是跨通告 hello 私用對等互連路徑上，從 hello ASE 的子網路的所有輸出網路封包將會強制通道的 tooa 客戶的內部部署網路基礎結構。 ASE 目前不支援這個網路流量。 一個方案 toothis 問題就是從 hello 公用互連路徑 toohello 私用對等互連路徑 toostop 跨廣告路由。

toocreate UDR，請遵循下列步驟：

1. 移 toohello Azure 入口網站。 選取 [網路] > [路由表]。

2. 在 hello 中建立新的路由表相同的區域 VNet。

3. 從您的路由表 UI 內，選取 [路由] > [新增]。

4. 設定 hello**下個躍點類型**太**網際網路**和 hello**位址首碼**太**0.0.0.0/0**。 選取 [ **儲存**]。

    接著您看到類似下列 hello:

    ![功能性路由][6]

5. 建立 hello 新的路由表之後，請包含您 ASE toohello 子網路。 從 hello 入口網站中的 hello 清單中選取路由表。 儲存 hello 變更之後，您應該看見 hello Nsg 以及記下與您的子網路的路由。

    ![NSG 和路由][7]

### <a name="deploy-into-existing-azure-virtual-networks-that-are-integrated-with-expressroute"></a>部署到與 ExpressRoute 整合的現有 Azure 虛擬網路 ###

toodeploy VNet 與 ExpressRoute，整合到您 ASE 預先設定您想要部署的 hello ASE hello 子網路。 然後使用 資源管理員範本 toodeploy 它。 在 VNet 中的 toocreate ase 中已經有設定 ExpressRoute:

- 建立子網路 toohost hello ASE。

    > [!NOTE]
    > 沒有其他可以在 hello 子網路但 hello ASE 中。 為確定 toochoose 容許未來成長的位址空間。 您之後無法變更此設定。 我們建議使用包含 128 個位址的 `/25` 大小。

- 稍早所述，建立 UDRs （例如，路由表），並將其設定 hello 子網路上。
- 使用資源管理員範本中所述建立 hello ASE[建立 ase 中使用資源管理員範本][MakeASEfromTemplate]。

<!--Image references-->
[1]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow.png
[2]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow2.png
[3]: ./media/network_considerations_with_an_app_service_environment/networkase-ipaddresses.png
[4]: ./media/network_considerations_with_an_app_service_environment/networkase-inboundnsg.png
[5]: ./media/network_considerations_with_an_app_service_environment/networkase-outboundnsg.png
[6]: ./media/network_considerations_with_an_app_service_environment/networkase-udr.png
[7]: ./media/network_considerations_with_an_app_service_environment/networkase-subnet.png

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
[ASEManagement]: ./management-addresses.md
