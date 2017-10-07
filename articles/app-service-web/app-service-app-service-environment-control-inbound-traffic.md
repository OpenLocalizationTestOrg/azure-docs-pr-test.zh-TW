---
title: "aaaHow tooControl 連入流量 tooan App Service 環境"
description: "深入了解如何 tooconfigure 網路安全性規則 toocontrol 輸入流量 tooan App Service 環境。"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: 
ms.assetid: 4cc82439-8791-48a4-9485-de6d8e1d1a08
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: stefsch
ms.openlocfilehash: e7c6e6201db6a1ea77f7a2eee29a3b5445175495
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontrol-inbound-traffic-tooan-app-service-environment"></a>如何 tooControl 連入流量 tooan App Service 環境
## <a name="overview"></a>概觀
您可以在 Azure Resource Manager 虛擬網路**或**傳統部署模型[虛擬網路][virtualnetwork]中建立 App Service Environment。  新的虛擬網路與新的子網路可以在建立 App Service 環境的 hello 階段定義。  或者亦可在先前既存的虛擬網路和既存的子網路中建立 APP Service 環境。  在 2016 年 6 月所進行的變更之後，ASE 也可以部署到使用公用位址範圍或 RFC1918 位址空間 (也就是私人位址) 的虛擬網路。  如需有關建立 App Service 環境的詳細資訊，請參閱[如何 tooCreate App Service 環境][HowToCreateAnAppServiceEnvironment]。

App Service 環境必須一定要建立子網路內因為子網路提供網路界限，這可以是使用的 toolock 向上游裝置和服務背後的輸入流量，使得 HTTP 及 HTTPS 流量為只接受來自特定上游IP 位址。

您可以使用[網路安全性群組][NetworkSecurityGroups]來控制子網路上的輸入和輸出網路流量。 控制輸入的流量需要建立網路安全性群組中的網路安全性規則，然後指派 hello 網路安全性群組 hello 子網路包含 hello App Service 環境。

網路安全性群組指派之後 tooa 子網路，App Service 環境會允許/封鎖根據 hello hello 中的輸入的流量 tooapps 允許和拒絕 hello 網路安全性群組中定義的規則。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="inbound-network-ports-used-in-an-app-service-environment"></a>App Service Environment 中使用的輸入網路連接埠
之前鎖定與網路安全性群組的輸入網路流量，是重要的 tooknow hello 的 App Service 環境所使用的必要和選擇性的網路連接埠。  不小心關閉關閉流量 toosome 連接埠可能會導致遺失 App Service 環境中的功能。

hello 以下是使用 App Service 環境的連接埠的清單。 除非明確註明，否則所有連接埠為 **TCP**：

* 454：Azure 基礎結構透過 SSL 用來管理和維護 App Service 環境的**必要連接埠**。  不會封鎖流量 toothis 連接埠。  此連接埠永遠是繫結的 toohello 公用 VIP 的 ase。
* 455：Azure 基礎結構透過 SSL 用來管理和維護 App Service 環境的**必要連接埠**。  不會封鎖流量 toothis 連接埠。  此連接埠永遠是繫結的 toohello 公用 VIP 的 ase。
* 80： 預設通訊埠的傳入 HTTP 流量 tooapps App Service 環境中的應用程式服務方案中執行。  ILB 啟用 ase 中，在此連接埠是 hello ASE 繫結的 toohello ILB 位址。
* 443： 預設通訊埠的輸入 SSL 流量 tooapps App Service 環境中的應用程式服務方案中執行。  ILB 啟用 ase 中，在此連接埠是 hello ASE 繫結的 toohello ILB 位址。
* 21：FTP 的控制通道。  如果未使用 FTP，就可以安全地封鎖此連接埠。  在 ILB 啟用 ase 中，此連接埠可能繫結的 toohello ILB ase 中的位址。
* 990：FTPS 的控制通道。  如果未使用 FTPS，就可以安全地封鎖此連接埠。  在 ILB 啟用 ase 中，此連接埠可能繫結的 toohello ILB ase 中的位址。
* 10001-10020：FTP 的資料通道。  做為與 hello 控制通道，這些連接埠可以安全地封鎖如果不使用 FTP。  ILB 啟用 ase 中，在此連接埠可能繫結的 toohello ASE 的 ILB 位址。
* 4016：用於 Visual Studio 2012 的遠端偵錯。  如果未使用 hello 功能，就可以安全地封鎖這個連接埠。  ILB 啟用 ase 中，在此連接埠是 hello ASE 繫結的 toohello ILB 位址。
* 4018：用於 Visual Studio 2013 的遠端偵錯。  如果未使用 hello 功能，就可以安全地封鎖這個連接埠。  ILB 啟用 ase 中，在此連接埠是 hello ASE 繫結的 toohello ILB 位址。
* 4020：用於 Visual Studio 2015 的遠端偵錯。  如果未使用 hello 功能，就可以安全地封鎖這個連接埠。  ILB 啟用 ase 中，在此連接埠是 hello ASE 繫結的 toohello ILB 位址。

## <a name="outbound-connectivity-and-dns-requirements"></a>輸出連線和 DNS 需求
App Service 環境 toofunction 正常運作，它也需要能夠存取外部 toovarious 端點。 Hello hello 」 所需的網路連接性 」 一節中的 hello ase 中所使用的外部端點的完整清單位於[expressroute 的網路組態](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity)發行項。

App Service 環境需要有效的 DNS 基礎結構，設定 hello 虛擬網路。  如果任何原因 hello DNS 設定會變更在建立 App Service 環境之後，開發人員可以強制的 App Service 環境 toopick hello 新的 DNS 設定。  觸發輪流的環境重新開機，使用 「 重新啟動 」 圖示位於的 hello 頂端的 hello App Service 環境管理刀鋒視窗中 hello hello [Azure 入口網站][ NewPortal]會導致 hello 環境 toopick建立 hello 新的 DNS 設定。

也建議 hello vnet 上的任何自訂 DNS 伺服器會預先時間先前 toocreating App Service 環境的安裝程式。  如果在建立 App Service 環境期間變更虛擬網路的 DNS 設定，，因而造成 hello App Service 環境建立程序失敗。  同樣地，如果自訂的 DNS 伺服器 hello 存在於另一端的 VPN 閘道和 hello DNS 伺服器會為無法連線到或無法使用，hello App Service 環境的建立程序也會失敗。

## <a name="creating-a-network-security-group"></a>建立網路安全性群組
如需如何網路安全性群組工作的完整細節，請參閱 hello 下列[資訊][NetworkSecurityGroups]。  hello Azure 服務管理下例修飾上反白顯示的網路安全性群組，而且著重於設定與套用安全性群組 tooa 子網路，其中包含 App Service 環境。

**注意：**可以設定網路安全性群組，以圖形方式使用 hello [Azure 入口網站](https://portal.azure.com)或透過 Azure PowerShell。

網路安全性群組首次會建立為與訂用帳戶相關聯的獨立實體。 因為在 Azure 的區域中，會建立網路安全性群組，確認該 hello 網路安全性小組已建立 hello 相同為 App Service 環境的 hello 地區。

hello 下列示範如何建立網路安全性群組：

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

網路安全性小組建立之後，一或多個網路安全性規則會加入 tooit。  由於 hello 組規則會隨著時間變更，因此建議 toospace 出 hello 編號配置用於規則優先順序 toomake 它輕鬆 tooinsert 其他規則一段時間。

下列的 hello 範例顯示明確授與存取 toohello 管理連接埠所需的 hello Azure 基礎結構 toomanage 並維護 App Service 環境的規則。  請注意，所有管理流量流程透過 SSL 受到用戶端憑證，因此即使 hello 連接埠已開啟他們都無法存取由 Azure 的管理基礎結構的任何實體。

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP


當鎖定存取 tooport 80 和 443 太 「 隱藏 」 App Service 環境上游裝置或服務後，您將需要 tooknow hello 上游的 IP 位址。  例如，如果您正在使用 web 應用程式的防火牆 (WAF)，hello WAF 必須時使用它自己的 IP 位址 （或位址） proxy 處理流量 tooa 下游的 App Service 環境。  您將需要 toouse hello 這個 IP 位址*SourceAddressPrefix*網路安全性規則的參數。

在 hello 下列範例中，明確地允許從特定的上游 IP 位址的輸入的流量。  hello 位址*1.2.3.4*上游 WAF hello IP 位址做為預留位置。  變更您上游的裝置或服務所使用的 hello 值 toomatch hello 位址。

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTP" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTPS" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

如果想要使用 FTP 支援，hello 下列規則可用來當作範本 toogrant 存取 toohello FTP 控制連接埠和資料通道連接埠。  由於 FTP 是可設定狀態的通訊協定，您可能無法透過傳統的 HTTP/HTTPS 的防火牆或 proxy 裝置可以 tooroute FTP 流量。  在此情況下，您將需要 tooset hello *SourceAddressPrefix* tooa 不同值，例如 hello IP 位址範圍的開發人員套件或部署在執行的 FTP 用戶端的電腦。 

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPCtrl" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '21' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPDataRange" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '10001-10020' -Protocol TCP

(**附註：** hello 預覽期間可能會變更 hello 資料通道連接埠範圍。)

如果使用 Visual Studio 遠端偵錯時，下列規則的 hello 示範 toogrant 的存取方式。  因為每個支援的 Visual Studio 版本使用不同的連接埠進行遠端偵錯，所以每個版本會有個別的規則。  如同 FTP 存取，遠端偵錯流量可能不會透過傳統 WAF 或 Proxy 裝置正確傳送。  hello *SourceAddressPrefix*您可以改為將執行 Visual Studio 程式開發人員電腦 toohello IP 位址範圍。

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2012" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4016' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2013" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4018' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2015" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4020' -Protocol TCP

## <a name="assigning-a-network-security-group-tooa-subnet"></a>指定網路安全性群組 tooa 子網路
網路安全性群組已拒絕存取 tooall 外部流量的預設安全性規則。  hello 自結合 hello，上面所述的網路安全性規則的結果，hello 封鎖輸入的流量的預設安全性規則，從來源位址範圍的資料傳輸相關聯的*允許*動作就可以toosend 流量 tooapps App Service 環境中執行。

網路安全性群組安全性規則後，它必須包含 hello App Service 環境 toobe 指派 toohello 子網路。  hello 分派命令參考兩個 hello hello 虛擬網路的名稱以及 hello hello hello App Service 環境建立所在的子網路名稱，hello App Service 環境的所在位置。  

hello 下面範例是網路安全性群組指派 tooa 子網路與虛擬網路：

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

一旦 hello 網路安全性的群組指派可成功 （hello 分派是長時間執行的作業伺服器，可能需要幾分鐘的時間 toocomplete），僅輸入流量比對*允許*規則將會成功連線到 hello 應用程式中的應用程式服務的環境。

完整性 hello 下列範例會示範如何 tooremove，因此解譯關聯 hello 網路安全性群組從 hello 子網路：

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Remove-AzureNetworkSecurityGroupFromSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

## <a name="special-considerations-for-explicit-ip-ssl"></a>明確 IP-SSL 的特殊考量
如果應用程式已設定使用明確的 IP SSL 位址 (適用於*只*有公開 VIP 的 tooASEs)，而不是使用 hello App Service 環境的 hello 預設 IP 位址，HTTP 和 HTTPS 流量進入 hello 子網路的流程透過一組不同的連接埠 80 和 443 以外的連接埠。

從 hello App Service 環境的詳細資料 UX 刀鋒視窗的 hello 入口網站使用者介面中可以找到 hello 個別對每個 IP SSL 位址所使用的連接埠。  選取 [所有設定] --> [IP 位址]。  hello 「 IP 位址 」 刀鋒視窗中顯示的 hello App Service 環境中，明確地設定所有 IP SSL 位址的資料表是使用的 tooroute hello 特殊的通訊埠組合以及 HTTP 及 HTTPS 流量相關聯每個 IP SSL 位址。  它是需要 toobe 設定網路安全性群組中的規則時，為 hello DestinationPortRange 參數使用此連接埠配對。

設定的 toouse IP SSL 上 ase 中的應用程式時，外部客戶看不到，而且不需要 tooworry hello 特殊連接埠組對應的相關。  流量 toohello 應用程式通常會流 toohello 設定 IP SSL 位址。  hello 轉譯 toohello 特殊的通訊埠組合自動期間進行的作業在內部 hello 最後階段路由傳送流量至 hello 子網路包含 hello ASE。 

## <a name="getting-started"></a>開始使用
tooget 開始使用應用程式服務環境中，請參閱[簡介 tooApp Service 環境][IntroToAppServiceEnvironment]

所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。

如需周圍安全地從 App Service 環境連接 toobackend 資源的應用程式的詳細資訊，請參閱[安全地從 App Service 環境連接 tooBackend 資源][SecurelyConnecttoBackend]

如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[SecurelyConnecttoBackend]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NewPortal]:  https://portal.azure.com  

<!-- IMAGES -->

