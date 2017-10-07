---
title: "使用 Express Route aaaNetwork 組態詳細資料"
description: "虛擬網路中執行應用程式服務環境的網路組態詳細資料連接 tooan ExpressRoute 電路。"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 34b49178-2595-4d32-9b41-110c96dde6bf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: stefsch
ms.openlocfilehash: 85bbc45cfed619485957ee2a898aa0a7604173cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-configuration-details-for-app-service-environments-with-expressroute"></a>使用 ExpressRoute 之 App Service 環境的網路組態詳細資料
## <a name="overview"></a>概觀
客戶可以連接[Azure ExpressRoute] [ ExpressRoute]電路 tootheir 虛擬網路基礎結構，進而擴充其內部部署網路 tooAzure。  您可以在這個[虛擬網路][virtualnetwork]基礎結構的子網路中建立 App Service 環境。  Hello App Service 環境上執行應用程式可以僅透過 hello ExpressRoute 連線，然後建立可存取的安全連線 tooback 端資源。  

您可以在 Azure Resource Manager 虛擬網路**或**傳統式部署模型虛擬網路中建立 App Service 環境。  在 2016 年 6 月所進行的最新變更之後，ASE 現在也可以部署到使用公用位址範圍或 RFC1918 位址空間 (也就是私人位址) 的虛擬網路。 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="required-network-connectivity"></a>需要的網路連線
有可能一開始符合 ExpressRoute 的虛擬網路連接 tooan 中的應用程式服務環境的網路連線需求。  App Service 環境將會要求所有順序 toofunction 中的 hello 下列正確：

* 傳出的網路連線 tooAzure 儲存體端點全球連接埠 80 和 443 上。  這包括端點位於 hello 與 hello App Service 環境中，相同的區域，以及儲存體端點位於**其他**Azure 區域。  Azure 儲存體端點解決下列 DNS 網域的 hello 下： *.table.core.windows.net*， *account>.blob.core.windows.net*， *queue.core.windows.net*和*file.core.windows.net*。  
* 傳出的網路連線 toohello Azure 檔案服務在連接埠 445。
* 傳出的網路連線 tooSql DB 端點位於 hello 相同為 App Service 環境的 hello 地區。  Sql DB 端點解析 hello 下列網域下： *.database.windows.net*。  這需要開啟存取 tooports 1433 11000 11999 和 14000 14999。  如需詳細資訊，請參閱 [Sql Database V12 連接埠使用方式](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md)一文。
* 傳出的網路連線 toohello Azure 管理平面端點 （ASM 和 ARM 端點）。  這包括的傳出連線 tooboth *management.core.windows.net*和*management.azure.com*。 
* 傳出的網路連線太*ocsp.msocsp.com*， *mscrl.microsoft.com*和*crl.microsoft.com*。這是所需的 toosupport SSL 功能。
* 必須能夠解析所有 hello 端點 hello hello 虛擬網路的 DNS 設定，且網域中所述 hello 較早的點。  如果無法解析這些端點，App Service 環境建立嘗試將會失敗，而且現有的 App Service 環境會標示為狀況不良。
* 需要有連接埠 53 的輸出存取，才能與 DNS 伺服器通訊。
* 如果自訂的 DNS 伺服器上有 hello 另一端的 VPN 閘道，hello DNS 伺服器必須是包含 hello App Service 環境的 hello 子網路觸達。 
* hello 傳出的網路路徑無法通過內部公司 proxy，也不可以是強制通道 tooon 內部部署。  這麼做會變更 hello 從 hello App Service 環境的輸出網路流量的有效 NAT 位址。  變更輸出網路流量 App Service 環境的 hello NAT 位址，將導致上面所列失敗 toomany hello 端點的連線。  這會導致 App Service 環境建立嘗試失敗，而之前狀況良好的 App Service 環境會標示為狀況不良。  
* 輸入網路存取 toorequired 連接埠的應用程式服務環境中所述，必須允許[文章][requiredports]。

確保有效的 DNS 基礎結構並加以設定和維護的 hello 虛擬網路可以滿足 hello DNS 需求。  如果任何原因 hello DNS 設定會變更在建立 App Service 環境之後，開發人員可以強制的 App Service 環境 toopick hello 新的 DNS 設定。  觸發輪流的環境重新開機，使用 「 重新啟動 」 圖示位於的 hello 頂端的 hello App Service 環境管理刀鋒視窗中 hello hello [Azure 入口網站][ NewPortal]會導致 hello 環境 toopick建立 hello 新的 DNS 設定。

hello 傳入的網路存取可以滿足需求設定[網路安全性群組][ NetworkSecurityGroups] hello App Service 環境的子網路 tooallow hello 所需存取此中所述[文章][requiredports]。

## <a name="enabling-outbound-network-connectivity-for-an-app-service-environment"></a>啟用 App Service 環境的輸出網路連線
新建立的 ExpressRoute 循環預設會通告允許輸出網際網路連線的預設路由。  這項設定的 App Service 環境將會無法 tooconnect tooother Azure 端點。

不過，一般客戶組態為 toodefine 自己強制傳出網際網路流量 tooinstead 流程的預設路由 (0.0.0.0/0) 內部。  此流量必定中斷應用程式服務環境，因為 hello 傳出流量會被封鎖在內部，或 NAT 的 tooan 無法辨識組無法再使用不同的 Azure 端點的位址。

hello 解決方案是 toodefine 一個 （或更多） 使用者定義的路由 (UDRs) 包含 hello App Service 環境的 hello 子網路上。  UDR 定義特定子網路的路由，則會採用而不是 hello 預設路由。

可能的話，我們建議下列組態 toouse hello:

* hello ExpressRoute 組態通告 0.0.0.0/0，並依預設強制通道連接所有輸出流量的內部。
* 包含 hello App Service 環境的 hello UDR 套用 toohello 子網路都會定義 0.0.0.0/0 下一個躍點類型為網際網路 （其中一個範例就是向本文章中較遠）。

hello 聯合的影響這些步驟是，hello 子網路層級 UDR 會優先於 hello ExpressRoute 強制通道，以確保從 hello App Service 環境的對外網際網路存取。

> [!IMPORTANT]
> hello UDR 中定義的路由**必須**會不夠具體太 hello ExpressRoute 組態的優先順序高於任何路由通告。  下列 hello 範例使用 hello 廣泛 0.0.0.0/0 位址範圍，並在這種情況可能會不小心覆寫使用更特定的位址範圍的路由通告。
> 
> ExpressRoute 組態不支援應用程式服務環境的**跨通告從 hello 公用互連路徑 toohello 私用對等互連路徑的路由**。  已設定公用對等互連的 ExpressRoute 組態，會收到來自 Microsoft 的一大組 Microsoft Azure IP 位址範圍的路由通告。  如果這些位址範圍在 hello 私用對等互連路徑跨通告，hello 最終結果會是從 hello App Service 環境的子網路的所有輸出網路封包將會強制通道 tooa 客戶的內部部署網路基礎結構。  App Service 環境目前不支援這個網路流量。  一個方案 toothis 問題就是從 hello 公用互連路徑 toohello 私用對等互連路徑 toostop 跨廣告路由。
> 
> 

如需使用者定義路由的背景資訊，請參閱此[概觀][UDROverview]。  

建立及設定使用者定義的路由的詳細資訊可在此[如何 tooGuide][UDRHowTo]。

## <a name="example-udr-configuration-for-an-app-service-environment"></a>App Service 環境的範例 UDR 組態
**必要條件**

1. 安裝 Azure Powershell 從 hello [Azure 下載頁面][ AzureDownloads] （年 6 月 2015年或更新版本）。  在 < 命令列工具 > 下會在 [Windows Powershell]，將會安裝 hello 最新版的 Powershell cmdlet 的 「 安裝 」 連結。
2. 建議您建立唯一的子網路，以專供 App Service 環境使用。  這可確保該 hello UDRs 套用 toohello 子網路只會開啟 hello App Service 環境的輸出流量。
3. **重要**： 不要將部署直到 App Service 環境的 hello**之後**hello 組態步驟會遵循。  這可確保輸出的網路連線已可用，然後再嘗試 toodeploy App Service 環境。

**步驟 1：建立具名路由表**

hello 下列程式碼片段會建立稱為 「 DirectInternetRouteTable"hello West US Azure 區域中的路由表：

    New-AzureRouteTable -Name 'DirectInternetRouteTable' -Location uswest

**步驟 2: Hello 路由表中建立一個或多個路由**

您將需要 tooadd 其中一個或多個路由 toohello 路由表中順序 tooenable 的對外網際網路存取。  

hello 建議的方法來設定輸出存取 toohello 網際網路是 toodefine 0.0.0.0/0，如下所示的路由。

    Get-AzureRouteTable -Name 'DirectInternetRouteTable' | Set-AzureRoute -RouteName 'Direct Internet Range 0' -AddressPrefix 0.0.0.0/0 -NextHopType Internet

請記住該 0.0.0.0/0 代表廣泛的位址範圍，而且在這種情況將會覆寫通告 hello ExpressRoute 的更特定的位址範圍。  toore-逐一查看 hello 前面的建議，與 0.0.0.0/0 路由 UDR 應該用於搭配只會通告以及 0.0.0.0/0 ExressRoute 組態。 

或者，您可以下載完整和更新的由 Azure 使用中的 CIDR 範圍清單。  hello Xml 檔案包含所有 hello Azure IP 位址範圍可從 hello [Microsoft Download Center][DownloadCenterAddressRanges]。  

不過請注意，這些範圍會隨時間變更，因此必要定期手動更新 toohello 使用者定義的路由 tookeep 同步。此外，因為沒有上限的預設值的 100 中單一 UDR 路由，您將需要太 「 摘要 」 hello Azure IP 位址的限制範圍 toofit hello 100 路由限制內，記住該 UDR 定義的路由需要比 hello 路由通告的更具體的 toobe 您ExpressRoute。  

**步驟 3： 建立關聯的 hello 路由表 toohello 子網路包含 hello App Service 環境**

hello 最後一個組態步驟是 tooassociate hello 路由表 toohello 子網路將會部署 App Service 環境的 hello。  hello 下列命令將關聯 hello"DirectInternetRouteTable"toohello"ASESubnet 」，最後將會包含 App Service 環境。

    Set-AzureSubnetRouteTable -VirtualNetworkName 'YourVirtualNetworkNameHere' -SubnetName 'ASESubnet' -RouteTableName 'DirectInternetRouteTable'


**步驟 4：最後步驟**

一旦 hello 路由表繫結的 toohello 子網路，它會建議 toofirst 測試，並確認 hello 預期效果。  例如，將虛擬機器部署到 hello 子網路，並確認：

* 輸出流量 tooboth Azure 和非 Azure 端點所提及稍早在本文章列為**不**流動向 hello ExpressRoute 電路。  它是非常重要的 tooverify 這種行為，因為從 hello 子網路的輸出流量是否仍強制通道的內部，App Service 環境將一律失敗。 
* Hello 端點的 DNS 查閱之前所述所有解析正確。 

一旦確認 hello 上述步驟，您將需要 toodelete hello 虛擬機器，因為 hello 子網路需要 toobe"empty"在建立 App Service 環境的 hello 時間 hello。

然後繼續建立 App Service 環境！

## <a name="getting-started"></a>開始使用
所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。

tooget 開始使用應用程式服務環境中，請參閱[簡介 tooApp Service 環境][IntroToAppServiceEnvironment]

如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[requiredports]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[NetworkSecurityGroups]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[UDROverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-overview/
[UDRHowTo]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-how-to/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureDownloads]: http://azure.microsoft.com/en-us/downloads/ 
[DownloadCenterAddressRanges]: http://www.microsoft.com/download/details.aspx?id=41653  
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[NewPortal]:  https://portal.azure.com


<!-- IMAGES -->
