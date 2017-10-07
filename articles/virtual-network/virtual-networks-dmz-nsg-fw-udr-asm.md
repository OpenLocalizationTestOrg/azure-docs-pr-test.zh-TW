---
title: "範例-aaaDMZ 建置 DMZ tooProtect 網路使用防火牆、 UDR，以及 NSG |Microsoft 文件"
description: "建置具有防火牆、使用者定義的路由 (UDR) 和網路安全性群組 (NSG) 的 DMZ"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a>範例 3 – 建置 DMZ tooProtect 網路使用防火牆、 UDR，以及 NSG
[傳回 toohello 安全性界限最佳作法頁面][HOME]

此範例會建立 DMZ，其內含防火牆、四個 Windows 伺服器、使用者定義的路由、IP 轉送和網路安全性群組。 它也將會逐步每 hello 相關命令 tooprovide 更深入的了解每個步驟。 另外還有流量案例 > 一節 tooprovide 的深入了解逐步如何流量就會繼續進行 hello 層級的防禦 hello 周邊網路。 最後，在 hello references 區段中是 hello 完整程式碼和指示 toobuild 此環境 tootest 和試驗各種案例。 

![具有 NVA、NSG 和 UDR 的雙向 DMZ][1]

## <a name="environment-setup"></a>環境設定
在此範例中沒有包含 hello 下列訂用帳戶：

* 三個雲端服務：“SecSvc001”、“FrontEnd001” 和 “BackEnd001”
* 一個虛擬網路 "CorpNetwork"，包含三個子網路：“SecNet”、“FrontEnd” 和 “BackEnd”
* 網路的虛擬設備，在此範例中，防火牆連接 toohello SecNet 子網路
* 一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)
* 兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)
* 一個代表 DNS 伺服器的 Windows Server ("DNS01")

在下面 hello references 區段中沒有將建置大部分 hello 環境上面所述的 PowerShell 指令碼。 建置 hello Vm 和虛擬網路，由 hello 範例指令碼，雖然不詳述於本文件說明。

toobuild hello 環境：

1. 儲存 hello 網路組態 xml 檔案包含在 hello 參考一節 （名稱、 位置和 IP 位址 toomatch hello 指定案例與更新）
2. Hello 指令碼 toomatch hello 環境 hello 指令碼中的更新 hello 使用者變數是 toobe 執行 （訂用帳戶、 服務名稱等等）
3. 在 PowerShell 中執行 hello 指令碼

**請注意**： 表示 hello PowerShell 指令碼中的 hello 區域必須符合表示 hello 網路組態 xml 檔中的 hello 區域。

Hello 指令碼順利執行之後可能會進入 hello 後指令碼的步驟：

1. 設定 hello 防火牆規則，這會涵蓋 hello 下面的一節中： 防火牆規則的描述。
2. （選擇性） 在 hello references 區段中是兩個指令碼 tooset hello web 伺服器和應用程式伺服器，以測試此 DMZ 設定簡單的 web 應用程式 tooallow。

一旦 hello 指令碼順利執行 hello 防火牆規則需要 toobe 完成，這在 hello 一節中說明： 防火牆規則。

## <a name="user-defined-routing-udr"></a>使用者定義的路由 (UDR)
根據預設，下列系統路由 hello 的定義如下：

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

hello VNETLocal 一律為 hello 定義位址首碼的 hello VNet 的該特定的網路 （亦即它將變更從 VNet tooVNet 根據每個特定的 VNet 的定義方式）。 hello 路由是靜態的而且預設上述剩餘的系統。

與優先順序，路由透過 hello 最長的前置詞比對 (LPM) 方法來處理，因此 hello hello 資料表中最明確的路由會套用 tooa 目的地位址。

因此，流量 （例如 toohello DNS01 伺服器，10.0.2.4） 給 hello 區域網路 (10.0.0.0/16) 就會路由傳送跨 toohello 10.0.0.0/16 路由到期的 hello VNet tooits 目的地。 換句話說，如 10.0.2.4，hello 10.0.0.0/16 路由 hello 最明確的路由，即使是 hello 10.0.0.0/8/8 以及 0.0.0.0/0 也會無法套用，但是因為它是以較不特定他們不會影響此流量。 因此 hello 流量 too10.0.2.4 會擁有下一個躍點的 hello 區域 VNet 和直接路由傳送 toohello 目的地。

如果流量設計的目的 10.1.1.1 比方說，hello 10.0.0.0/16 路由不會套用，但 hello 10.0.0.0/8 hello 最適合的而此 hello 流量會卸除 （「 黑色書背 」），因為 hello 下一個躍點為 Null。 

如果 hello 目的地未套用 tooany hello Null 前置詞或 hello VNETLocal 前置詞，則它會遵循 hello 最不特定路由，0.0.0.0/0，並傳送出 toohello 網際網路的 hello 下一個躍點，因此 Azure 的網際網路邊緣外。

如果在 hello 路由表中有兩個相同的前置詞，hello 如下 hello hello 路由 「 來源 」 屬性為基礎的喜好設定順序：

1. 「 VirtualAppliance"= 使用者定義的路由手動新增的 toohello 資料表
2. "VPNGateway"= 動態路由 (BGP 混合式網路搭配使用時)，加入動態網路通訊協定，這些路由會隨著時間變更為 hello 動態的通訊協定會自動反映變更，所以網路中
3. "Default"= hello 系統路由 hello 區域 VNet 和 hello 靜態項目上的 hello 路由表中所示。

> [!NOTE]
> 您現在可以使用 ExpressRoute 與 VPN 閘道 tooforce 輸出使用使用者定義路由 (UDR)，並輸入的跨單位流量 toobe 路由的 tooa 網路的虛擬設備 (NVA)。
> 
> 

#### <a name="creating-hello-local-routes"></a>建立 hello 區域路由
在此範例中，需要兩個路由表，分別指派給 hello 前端和 Backend 子網路。 每個資料表會載入適當的 hello 指定子網路的靜態路由。 為了 hello 此範例中，每一個資料表具有三個路由：

1. 沒有下個躍點定義 tooallow 本機子網路流量 toobypass hello 防火牆的本機子網路流量
2. 下個躍點定義防火牆為使用虛擬網路流量，這會覆寫，可讓本機 VNet 流量 tooroute 直接 hello 預設規則
3. 所有剩餘的流量 (0/0)，與下個躍點定義為 hello 防火牆

一旦建立 hello 路由表是繫結的 tootheir 子網路。 如 hello 前端子網路路由表，一旦建立並繫結 toohello 子網路看起來應該像這樣：

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


此範例中，針對 hello 下列命令會使用的 toobuild hello 路由表中，新增使用者定義的路由，然後再繫結 hello 路由表 tooa 子網路 (請注意，貨幣符號開頭如下的任何項目 (例如： $BESubnet) 中的 hello 指令碼的使用者定義變數hello 參考本文件一節）：

1. 必須建立第一個 hello 基底路由表。 這個程式碼片段會顯示 hello 建立 hello 資料表 hello 後端子網路。 Hello 的指令碼中對應的資料表也會建立為 hello Frontend 子網路。
   
     New-AzureRouteTable -Name $BERouteTableName `
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. 一旦建立 hello 路由表，就可以新增特定的使用者定義的路由。 在這個片段中，會透過 hello 虛擬應用裝置 （$VMIP [0]，變數是在 [hello hello 虛擬設備稍早在 hello 指令碼中建立時指派的 IP 位址使用的 toopass） 路由傳送所有流量 (0.0.0.0/0)。 在 hello 指令碼對應的規則也會建立 hello 前端資料表中。
   
     Get-AzureRouteTable $BERouteTableName | `
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. hello 路由項目上方將會覆寫 hello"0.0.0.0/0 」，預設路由但 hello 預設 10.0.0.0/16 規則還是現有的讓流量 hello VNet tooroute 內直接 toohello 目的地和 toohello 網路的虛擬設備。 toocorrect 必須新增此行為 hello 遵循規則。
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. 此時沒有所做的選擇 toobe。 以上述兩個路由 hello 所有流量會路由都傳送 toohello 防火牆進行評估，甚至在單一子網路內的流量。 這可能需要，不過 tooallow 流量內的子網路 tooroute 本機而不需要涉入 hello 防火牆可以加入第三個、 非常特定的規則。 此路由狀態的任何位址 destine 就可以只 hello 本機子網路的路由那里直接 (NextHopType = VNETLocal)。
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. 最後，與 hello 路由表建立並填入使用者定義的路由，hello 資料表現在必須繫結的 tooa 子網路。 在 hello 指令碼 hello 前端路由表也是繫結的 toohello Frontend 子網路。 以下是 hello hello 後端子網路的繫結指令碼。
   
     Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a>IP 轉送
附屬功能 tooUDR，是 IP 轉送。 這是 設定虛擬應用裝置，好讓它 tooreceive 流量未特別定址 toohello 應用裝置，然後轉寄該流量 tooits 最終目的端。

例如，如果流量從 AppVM01 使得要求 toohello DNS01 伺服器，UDR 會路由此 toohello 防火牆。 與 IP 轉送已啟用，將接受 hello 應用裝置 (10.0.0.4) 並再轉寄 tooits 最終目的端 (10.0.2.4) hello hello DNS01 目的地 (10.0.2.4) 流量。 不含 IP 轉送 hello 防火牆上啟用，流量就不會接受 hello 應用裝置即使 hello 路由表有 hello 防火牆為 hello 下一個躍點。 

> [!IMPORTANT]
> 它是關鍵 tooremember tooenable IP 轉送 」 搭配使用者定義之路由。
> 
> 

設定 IP 轉送是單一命令，可在建立 VM 時執行。 Hello 流程，此範例 hello 程式碼片段朝向 hello hello 指令碼的結尾，並與 hello UDR 命令分組：

1. 呼叫 hello VM 執行個體是您的虛擬應用裝置，請在此情況下，hello 防火牆並啟用 IP 轉送 」 (請注意，紅色貨幣符號開頭的任何項目 (例如： $VMName[0]) 是這份文件 hello 參考 > 一節中的 hello 指令碼的使用者定義變數。 hello 零以括號，[0] 代表 hello 的 Vm，而不需修改 hello 範例指令碼 toowork hello 陣列中的第一個 VM，必須是第一個 VM (VM 0) 的 hello hello 防火牆）：
   
     Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | `
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a>網路安全性群組 (NSG)
此範例會建置 NSG 群組，然後在其中載入單一規則。 此群組，就只有 toohello 前端及後端的子網路 (不 hello SecNet) 繫結。 以宣告方式建立 hello 下列規則：

1. 任何流量 （所有連接埠），從 hello 網際網路 toohello 拒絕整個 VNet （所有的子網路）

雖然此範例使用 NSG，但它的主要目的是做為防止人為設定錯誤的第二道防線。 我們希望 tooblock 所有傳入的流量 hello 網際網路 tooeither hello 前端或後端子網路流量只應該流經 hello SecNet 子網路 toohello 防火牆 （然後如果適當 toohello 前端或後端上子網路）。 此外，以 hello UDR 規則的地方，任何未將它轉換 hello 前端或後端的子網路的流量會被導向出 toohello 防火牆 (感謝您 tooUDR)。 hello 防火牆將會看到這個非對稱式資料流，然後會卸除 hello 輸出流量。 因此有三個層級的安全性保護 hello 前端和後端子網路。1) 沒有開啟端點上 hello FrontEnd001 和 BackEnd001 雲端服務，2) Nsg 拒絕流量從 hello 網際網路，3) hello 卸除對稱流量的防火牆。

在此範例中的 hello 網路安全性群組相關的一個有趣的一點是它包含一個規則，底下所示，也就是 toodeny 網際網路流量 toohello 整個虛擬網路會包括子網路-安全性 hello。 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

不過，因為 hello NSG 僅繫結 toohello 前端和後端子網路，hello 規則不處理流量的輸入 toohello 安全性子網路。 如此一來，即使 hello NSG 規則會指出沒有網際網路流量 tooany 位址上 hello VNet，因為 hello NSG 從未繫結 toohello 安全性子網路，將流量 toohello 安全性子網路。

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a>防火牆規則
Hello 防火牆上轉送規則需要 toobe 建立。 因為 hello 防火牆封鎖或轉送所有輸入、 輸出和內部 VNet 流量需要許多的防火牆規則。 此外，所有傳入的流量會叫用 hello 安全性服務公用 IP 位址 （在不同的連接埠），toobe 處理 hello 防火牆。 最佳作法是在稍後設定 hello 子網路和防火牆規則 tooavoid 重新作業之前 toodiagram hello 邏輯流程。 hello 圖是此範例中的 hello 防火牆規則的邏輯檢視：

![Hello 防火牆規則的邏輯檢視][2]

> [!NOTE]
> 根據網路虛擬應用裝置中使用的 hello，hello 管理連接埠而異。 在此範例中，所參考的 Barracuda NextGen 防火牆使用連接埠 22、801 和 807。 請參閱 hello 應用裝置廠商文件 toofind hello 確切使用連接埠正在使用的 hello 裝置的管理。
> 
> 

### <a name="logical-rule-description"></a>邏輯規則說明
Hello 邏輯在圖中，由於 hello 防火牆是 hello 該子，網路上唯一的資源，而且這個圖表會顯示 hello 防火牆規則和如何在邏輯上允許或拒絕流量和不 hello 實際路由的路徑，不會顯示 hello 安全性子網路。 此外，hello 外部連接埠為 hello RDP 流量會更高範圍的連接埠 (8014 – 8026) 和已選取的 toosomewhat 對齊 hello 與選取的最後一個 hello 本機 IP 位址更容易閱讀的兩個八位元 （例如本機伺服器位址 10.0.1.4 相關聯外部連接埠 8014），但是無法使用任何更高版本的非衝突連接埠。

在此範例中，我們需要 7 種規則，以下說明這些規則類型：

* 外部規則 (適用於輸入流量)：
  1. 防火牆管理規則： 這個應用程式重新導向規則允許流量 toopass toohello 管理連接埠的 hello 網路的虛擬設備。
  2. RDP 規則 （適用於每個 windows 伺服器）： 這些四項規則 （每個伺服器一個） 將允許的 hello 管理個別的伺服器，透過 RDP。 這也可能集結成一個規則視 hello 的 hello 網路正在使用的虛擬應用裝置的功能而定。
  3. 應用程式流量規則： 有兩個應用程式流量規則，先針對 hello 前端 web 流量，hello 和 hello hello 後端流量 （例如 web 伺服器 toodata 層） 的第二個。 這些規則的 hello 組態將取決於 hello （您的伺服器放置的位置） 的網路架構及流量 （流動的方向 hello 流量，及使用哪些連接埠）。
     * hello 第一個規則可讓 hello 實際的應用程式流量 tooreach hello 應用程式伺服器。 Hello 其他規則允許針對安全性、 管理等，而應用程式規則是允許外部使用者或服務 tooaccess hello 應用程式。 針對此範例中，連接埠 80 上沒有單一的 web 伺服器，因此單一防火牆應用程式規則將會重新導向輸入的流量 toohello 外部 IP，toohello web 伺服器的內部 IP 位址。 hello 重新導向流量的工作階段會 NAT 有 toohello 內部伺服器。
     * 第二個應用程式流量規則的 hello hello 後端規則 tooallow hello Web 伺服器 tootalk toohello AppVM01 伺服器 （但不是 AppVM02），透過任何連接埠。
* 內部規則 (適用於內部 VNet 流量)
  1. 輸出 tooInternet 規則： 這項規則將會允許來自任何網路流量 toopass toohello 選取網路。 此規則通常是預設的規則已經 hello 在防火牆上，但是已停用狀態。 在此範例中，應啟用此規則。
  2. DNS 規則： 這個規則允許只有 DNS （連接埠 53） 流量 toopass toohello DNS 伺服器。 針對會封鎖大部分的流量 hello 前端 toohello 後端從這個環境，此規則特別允許 DNS 來自任何區域子網路。
  3. 子網路 tooSubnet 規則： 這項規則是的 tooallow hello 後的任何伺服器端 hello 前端子網路上的子網路 tooconnect tooany 伺服器 （但不是 hello 反向）。
* （適用於不符合上述 hello 的流量） 的保全規則：
  1. 拒絕所有流量的規則： 這應該一律 hello 最終規則 （依據優先順序） 且因此如果流量流失敗時 toomatch hello 之前它就會卸除此規則的規則。 這是預設規則且通常會啟動，一般來說並不需要修改。

> [!TIP]
> Hello 第二個應用程式流量規則，在任何連接埠允許的簡單的這個範例，在真實案例 hello 最特定的連接埠和位址範圍應使用的 tooreduce hello 受攻擊面，此規則。
> 
> 

<br />

> [!IMPORTANT]
> 所有上述規則 hello 建立之後，請務必將允許或拒絕所需的每個規則 tooensure 流量 tooreview hello 優先順序。 例如，hello 規則是依優先順序。 它是簡單 toobe 鎖定 hello 防火牆到期 toomis 排序規則。 基本上，確保 hello 防火牆本身的 hello 管理永遠 hello 絕對最高優先權規則。
> 
> 

### <a name="rule-prerequisites"></a>規則的必要條件
必要條件 hello 虛擬機器執行 hello 防火牆，其中一個是公用端點。 Hello 防火牆 tooprocess 流量 hello 適當的公用端點必須為開啟狀態。 有三種類型的流量，在此範例中。1） 管理的傳輸 toocontrol hello 防火牆和防火牆規則、 2) RDP 流量 toocontrol hello windows 伺服器，以及 3） 應用程式的流量。 這些邏輯檢視上述的 hello 防火牆規則的下半部是 hello 中 hello 上方的流量類型的三個資料行。

> [!IMPORTANT]
> 此索引鍵 takeway 是 tooremember，**所有**流量將通過 hello 防火牆。 因此 tooremote 桌面 toohello IIS01 伺服器，即使它是在 hello Front End 雲端服務和 hello 前端子網路，tooaccess 此我們需要 tooRDP toohello 防火牆的伺服器連接埠 8014，，然後允許 hello 防火牆 tooroute hello RDP 要求內部toohello IIS01 RDP 連接埠。 hello Azure 入口網站的 [連線] 按鈕將無法運作，所以沒有直接的 RDP 路徑 tooIIS01 （就可以看到 hello 入口網站）。 這表示所有連線 hello 從網際網路將 toohello 安全性服務和連接埠，例如 secscv001.cloudapp.net:xxxx (參考 hello 上方圖表 hello 對應的外部連接埠和內部 IP 和連接埠)。
> 
> 

端點可在 VM 建立 hello 時開啟或張貼組建，因為在 hello 範例指令碼中完成，而且此程式碼片段所示 (請注意，以貨幣符號的任何項目開頭 (例如： $VMName[$i]) 是 hello referen 中的 hello 指令碼的使用者定義變數本文件 ce 一節。 hello"$i 」 中，[$i]，代表特定 VM 的 Vm 陣列中的 hello 陣列編號）：

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

雖然不清楚如下所示金額 toohello 使用變數，但端點是**只**hello 安全性雲端服務上開啟。 這是處理的所有傳入的流量 tooensure （路由傳送，NAT，卸除） hello 防火牆。

管理用戶端將會需要 toobe PC toomanage hello 防火牆上安裝，並建立所需的 hello 組態。 Toomanage hello 裝置的方式，請參閱 hello 文件從您的防火牆 （或其他 NVA） 廠商。 hello 這個區段和 hello 下一步 區段中，防火牆規則建立的其餘部分將說明 hello 透過 hello 廠商管理用戶端 （也就不是 hello Azure 入口網站或 PowerShell） 本身，hello 防火牆設定。

用戶端下載及連接 toohello Barracuda 用在此範例中的指示可在這裡找到： [Barracuda NG 系統管理員](https://techlib.barracuda.com/NG61/NGAdmin)

一旦登入 hello 防火牆但建立防火牆規則之前，有兩種必要的物件類別，可簡化建立 hello 規則;網路和服務的物件。

此範例中，三個具名的網路物件應該定義 （一個用於 hello Frontend 子網路和 hello 後端子網路，也 hello hello DNS 伺服器 IP 位址的網路物件）。 toocreate 具名網路。從 hello Barracuda NG 管理用戶端儀表板開始，瀏覽 toohello 設定] 索引標籤、 hello 操作的組態區段中按一下 [規則集，然後在 hello 防火牆物件功能表上，按一下 「 網路 」 然後 hello 編輯網路功能表中按一下 [新增]。 hello 網路物件現在可以建立，藉由新增 hello 名稱與 hello 前置詞：

![建立 FrontEnd 網路物件][3]

這會建立 hello FrontEnd 子網路的具名的網路，應該為 hello 後端的子網路以及建立類似的物件。 現在您可以更輕鬆地在 hello 防火牆規則中依名稱參考 hello 子網路。

Hello DNS 伺服器物件：

![建立 DNS 伺服器物件][4]

DNS 規則 hello 文件中的更新版本中，系統會使用這個單一 IP 位址的參考。

hello 第二個必要條件物件是服務物件。 這些會代表每部伺服器的 hello RDP 連線通訊埠。 由於 hello 現有 RDP 服務物件繫結的 toohello 預設 RDP 連接埠，3389，建立新的服務可以 tooallow 流量從 hello 外部連接埠 (8014 8026)。 新的連接埠也可以加入現有 RDP service toohello，但為了便於示範，可以建立個別規則的每個伺服器 hello。 toocreate 新 RDP 規則的伺服器。hello Barracuda NG 管理用戶端儀表板，從開始瀏覽 toohello 設定 索引標籤，在 hello 操作設定區段按一下規則集，然後 hello 防火牆物件功能表上，向下捲動服務的 hello 清單底下，按一下 服務，然後選取 hello「 RDP 」 服務。 按一下滑鼠右鍵並選取 [複製]，然後按一下滑鼠右鍵並選取 [貼上]。 現在會有可供編輯的 RDP-Copy1 服務物件。 RDP Copy1 上按一下滑鼠右鍵並選取 [編輯]，hello 編輯服務物件的視窗會隨即快顯如下所示：

![預設 RDP 規則的複本][5]

hello 值接著可以編輯的 toorepresent hello 特定伺服器的 RDP 服務。 上述預設 AppVM01 hello RDP 規則應該修改的 tooreflect 新的服務名稱、 描述和外部的 RDP 連接埠用於 hello 圖 8 圖表 (注意： hello RDP 預設值是 3389 toohello 外部連接埠正在使用這個變更 hello 連接埠AppVM01 hello 外部連接埠的 hello 案例中的特定伺服器為 8025） hello 已修改的服務如下所示：

![AppVM01 規則][6]

此程序必須重複的 toocreate RDP 服務 hello 剩餘的伺服器。AppVM02、 DNS01 和 IIS01。 這些服務的 hello 建立會讓 hello 規則建立更簡單且更明顯 hello 下一節。

> [!NOTE]
> Hello 防火牆 RDP 服務不需要有兩個原因。1） 第一個 hello 防火牆 VM 是 Linux 型映像會使用 SSH 連接埠 22 VM 管理，而不是 RDP 和 2） 通訊埠 22，因此 hello 下述 tooallow 管理連線能力的第一個管理規則允許兩個其他管理連接埠。
> 
> 

### <a name="firewall-rules-creation"></a>建立防火牆規則
此範例使用三種類型的防火牆規則，它們各有不同的圖示：

hello 應用程式重新導向規則：![應用程式重新導向圖示][7]

hello 目的地 NAT 規則：![目的地 NAT 圖示][8]

hello 傳遞規則：![傳遞圖示][9]

這些規則的詳細資訊可以在 hello Barracuda 網站上找到。

toocreate hello 下列規則 （或確認現有的預設規則），從 hello Barracuda NG 管理用戶端儀表板開始，瀏覽 toohello 設定 索引標籤、 在 hello 操作設定 區段按一下 規則集。 方格呼叫時，「 主要規則 」 會顯示 hello 現有使用中且已停用此防火牆規則。 Hello 右上角的此方格是很小，綠色"+"按鈕，再按一下這個 toocreate 新的規則 (請注意： 您的防火牆可能 「 鎖定 」 的變更，如果您看到一個按鈕標示 「 鎖定 」，而且您會無法 toocreate 或編輯規則，請按一下此按鈕 「 解除鎖定 」 hello 太規則 set，並允許編輯)。 如果您想 tooedit 現有的規則，就會選取該規則、 以滑鼠右鍵按一下並選取 編輯規則。

一旦您的規則建立和/或修改，它們必須是推入 toohello 防火牆，然後啟動，如果這不是 hello 規則變更不會生效。 hello 推播和啟動處理程序說明如下 hello 詳細資料的規則描述。

每個規則的 hello 細節所需的 toocomplete 此範例中所述，如下所示：

* **防火牆規則管理**： 此應用程式重新導向規則允許流量的 hello 網路虛擬應用裝置，在此範例中 Barracuda NextGen 防火牆 toopass toohello 管理連接埠。 hello 管理連接埠為 801、 807 和選擇性 22。 hello 外部和內部連接埠是 hello 相同 （也就是沒有連接埠轉譯）。 此 SETUP-MGMT-ACCESS 規則 (在 Barracuda NextGen 防火牆 6.1 版中) 是預設規則，且為預設啟用。
  
    ![防火牆管理規則][10]

> [!TIP]
> hello 這個規則中的來源位址空間可以是任何，如果 hello 已知管理 IP 位址範圍時，減少此領域也會減少 hello 攻擊介面 toohello 管理連接埠。
> 
> 

* **RDP 規則**： 這些目的地 NAT 規則將允許的 hello 管理個別的伺服器，透過 RDP。
  此規則有四個所需的重要欄位 toocreate:
  
  1. 來源 – tooallow RDP 從任何地方，hello 「 任何 」 用於 hello 來源欄位的參考。
  2. 服務 – 使用適當的服務物件建立更早版本，在此情況下"AppVM01 RDP"hello，hello 外部連接埠重新導向 toohello 伺服器本機 IP 位址和 tooport 3386 （hello 預設 RDP 連接埠）。 這個特定的規則是供 RDP 存取 tooAppVM01。
  3. 目的地 – 應 hello *hello 防火牆上的本機連接埠*，[DCHP 1 本機 IP] 或 eth0 如果使用靜態 Ip。 hello 序數編號 （eth0、 eth1 等） 可能會不同，如果您的網路應用裝置有多個本機介面。 這是 hello 連接埠 hello 防火牆送出從 （可能為接收埠的 hello hello 相同），是在 hello 目標清單欄位的 hello 實際的路由的目的地。
  4. 重新導向 – 這一節說明虛擬應用裝置 hello tooultimately 而重新導向此流量。 hello 最簡單的重新導向是 tooplace hello IP 和連接埠 （選用） 在 hello 目標清單的欄位。 如果沒有連接埠是使用的 hello hello 傳入要求上的目的地連接埠將會使用 （亦即未轉譯），如果連接埠指定 hello 連接埠也會是 NAT 會連同 hello IP 位址。
     
     ![防火牆 RDP 規則][11]
     
     總共四個 RDP 規則需要 toobe 建立： 
     
     | 規則名稱 | 伺服器 | 服務 | 目標清單 |
     | --- | --- | --- | --- |
     | RDP-to-IIS01 |IIS01 |IIS01 RDP |10.0.1.4:3389 |
     | RDP-to-DNS01 |DNS01 |DNS01 RDP |10.0.2.4:3389 |
     | RDP-to-AppVM01 |AppVM01 |AppVM01 RDP |10.0.2.5:3389 |
     | RDP-to-AppVM02 |AppVM02 |AppVm02 RDP |10.0.2.6:3389 |

> [!TIP]
> 縮小下 hello 來源 hello 範圍和服務欄位將會減少 hello 受攻擊面。 應該使用，可讓功能 hello 最有限的範圍。
> 
> 

* **應用程式流量規則**： 有兩個應用程式流量規則，先針對 hello 前端 web 流量，hello 和 hello hello 後端流量 （例如 web 伺服器 toodata 層） 的第二個。 這些規則將取決於 hello （您的伺服器放置的位置） 的網路架構及流量 （流動的方向 hello 流量，及使用哪些連接埠）。
  
    先討論是 hello 前端網路流量的規則：
  
    ![防火牆 Web 規則][12]
  
    此目的地 NAT 規則可讓 hello 實際的應用程式流量 tooreach hello 應用程式伺服器。 Hello 其他規則允許針對安全性、 管理等，而應用程式規則是允許外部使用者或服務 tooaccess hello 應用程式。 針對此範例中，連接埠 80 上沒有單一的 web 伺服器，因此 hello 單一防火牆應用程式規則將會重新導向輸入的流量 toohello 外部 IP，toohello web 伺服器的內部 IP 位址。
  
    **請注意**： 沒有指定在 hello 目標清單的欄位中的通訊埠，因此 hello 輸入連接埠 80 （或 hello 選取服務為 443） 將會使用 hello hello web 伺服器的重新導向。 如果 hello web 伺服器正在接聽不同的通訊埠，如連接埠 8080，hello 目標清單的欄位可能是更新的 too10.0.1.4:8080 tooallow 以及 hello 連接埠重新導向。
  
    下一個應用程式流量規則是的 hello hello 透過任何服務的後端規則 tooallow hello Web 伺服器 tootalk toohello AppVM01 伺服器 （但不是 AppVM02）：
  
    ![防火牆 AppVM01 規則][13]
  
    此階段規則可讓 IIS 上任何伺服器 hello 前端子網路 tooreach hello AppVM01 （IP 位址 10.0.2.5） 上任何連接埠，使用 hello web 應用程式所需的任何通訊協定 tooaccess 資料。
  
    在這個螢幕擷取畫面 」\<明確目的地\>"hello 目的地欄位 toosignify 10.0.2.5 中做 hello 目的地。 這可以是明確所示的具名網路物件 （為 「 已完成在 hello hello DNS 伺服器的先決條件）。 這是總 toohello hello 防火牆的系統管理員將使用 toowhich 方法。 hello 第一個空白資料列下按兩下 tooadd 10.0.2.5 Explict Desitnation，為\<明確目的地\>快顯的 hello 視窗中輸入 hello 位址。
  
    由於這是內部的流量，以便太設定 hello 連線方法，沒有 NAT 需要此傳遞規則之後，「 否 SNAT"。
  
    **請注意**： 如果只會有一個，或是已知特定數目的網頁伺服器、 網路物件資源可能會建立 toobe 更特定 toothose 確切的 IP 位址而不是，此規則中的 hello 來源網路是 hello 前端子網路上的任何資源hello 整個 Frontend 子網路。

> [!TIP]
> 此規則使用"Any"toomake hello 範例應用程式更容易 toosetup 並用 hello 服務，這也可讓 ICMPv4 (ping) 中的單一規則。 不過，這不是建議的作法。 hello 連接埠和通訊協定 （「 服務 」） 應該縮小 toohello 最小可能在跨界限可讓應用程式作業 tooreduce hello 受攻擊面。
> 
> 

<br />

> [!TIP]
> 雖然此規則會顯示正在使用的明確目的參考，以一致的方法應該用於整個 hello 防火牆設定。 建議您在名為的網路物件的 hello 用於整個更容易閱讀，並可支援性。 hello 的明確目的地是使用此處的唯一 tooshow 替代參考方法，通常不建議 （特別是針對複雜的組態）。
> 
> 

* **輸出 tooInternet 規則**： 此傳遞規則以允許從任何來源網路 toopass toohello 選取目的地網路的流量。 此規則是 hello Barracuda NextGen 在防火牆上，通常已經預設規則，但處於停用狀態。 此規則上按一下滑鼠右鍵，可以存取 hello 啟用 Rule 命令。 如下所示的 hello 規則已修改過的 tooadd hello 兩本機子網路做為參考，此規則的這個文件 toohello 來源屬性 hello 必要條件一節中所建立。
  
    ![防火牆輸出規則][14]
* **DNS 規則**： 此傳遞規則允許只有 DNS （連接埠 53） 流量 toopass toohello DNS 伺服器。 針對會封鎖大部分的流量 hello 前端 toohello 後端從這個環境，此規則特別允許 DNS。
  
    ![防火牆 DNS 規則][15]
  
    **請注意**： 在此畫面次的 hello 連線方法是否包含。 此規則為內部 IP toointernal IP 位址流量，因為沒有 NATing 是必要，但是這個 hello 連線方式設定過此階段規則的"No SNAT"。
* **子網路 tooSubnet 規則**： 此傳遞規則是預設規則已啟動，並修改的 tooallow 回 hello 上的任何伺服器端的子網路 tooconnect tooany 伺服器 hello 前端子網路。 此規則為內部所有流量以便 hello 連線方式設定 tooNo SNAT。
  
    ![防火牆內部 VNet 規則][16]
  
    **請注意**: hello 雙向核取方塊未核取 （也不是簽入大多數規則），這是極大的這項規則，因為它可讓規則 「 單向 」 這，可以從 hello 後端子 toohello 前端網路，起始的連線但不是 hello 反向。 如果核取該核取方塊，此規則就會啟用雙向流量，從我們的邏輯圖來看並不需要這麼做。
* **拒絕所有流量規則**： 應一律為 hello 最終規則 （依據優先順序），因此如果流量流失敗 toomatch 任何上述規則 hello 它就會卸除此規則。 這是預設規則且通常會啟動，一般來說並不需要修改。 
  
    ![防火牆拒絕規則][17]

> [!IMPORTANT]
> 所有上述規則 hello 建立之後，請務必將允許或拒絕所需的每個規則 tooensure 流量 tooreview hello 優先順序。 例如，hello 規則是 hello 順序他們應該會顯示 hello 的轉送規則 hello Barracuda 管理用戶端在主要方格中。
> 
> 

## <a name="rule-activation"></a>啟用規則
Hello 規則集必須是與 hello ruleset 修改 toohello hello 邏輯圖表的規格上, 傳 toohello 防火牆，然後啟動。

![防火牆規則啟用][18]

在 hello 右上角的 hello 管理用戶端都是叢集的按鈕。 按一下 hello 傳送變更 按鈕 toosend hello 修改規則 toohello 防火牆，然後按一下 hello 「 啟用 」 按鈕。

與 hello 啟用 hello 防火牆規則集的範例環境的這個組建已完成。

## <a name="traffic-scenarios"></a>流量案例
> [!IMPORTANT]
> 索引鍵 takeway 是 tooremember，**所有**流量將通過 hello 防火牆。 因此 tooremote 桌面 toohello IIS01 伺服器，即使它是在 hello Front End 雲端服務和 hello 前端子網路，tooaccess 此我們需要 tooRDP toohello 防火牆的伺服器連接埠 8014，，然後允許 hello 防火牆 tooroute hello RDP 要求內部toohello IIS01 RDP 連接埠。 hello Azure 入口網站的 [連線] 按鈕將無法運作，所以沒有直接的 RDP 路徑 tooIIS01 （就可以看到 hello 入口網站）。 這表示所有連線 hello 從網際網路將 toohello 安全性服務和連接埠，例如 secscv001.cloudapp.net:xxxx。
> 
> 

針對這些案例，hello 下列防火牆規則應該有：

1. 防火牆管理
2. RDP tooIIS01
3. RDP tooDNS01
4. RDP tooAppVM01
5. RDP tooAppVM02
6. 應用程式流量 toohello Web
7. 應用程式流量 tooAppVM01
8. 輸出 toohello 網際網路
9. 前端 tooDNS01
10. 內部子網路的流量 （只後端 toofront 結束）
11. 全部拒絕

hello 實際的防火牆規則集最有可能很多其他規則中加入 toothese，比此處所列的 hello，hello 任何給定的防火牆規則也會有不同的優先順序數字。 此清單和相關聯的數字是 tooprovide 只這些 11 個規則和 hello 相對優先權彼此之間的相關性。 換句話說，hello 實際在防火牆上，hello"RDP tooIIS01 」 可能是規則數字 5，但只要它是之下 hello 「 防火牆管理 」 規則，其會與此清單的 hello 意圖對齊 hello"RDP tooDNS01 」 規則。 hello 清單也有助於 hello 以下案例允許為求簡單明瞭。例如：「FW 規則 9 (DNS)」。 為求簡潔，四個 RDP 規則將會是共同的 hello 稱，"hello RDP 規則"hello 流量案例時 tooRDP 不相關。

也請記得網路安全性群組會就地升級輸入網際網路上的流量 hello 前端和後端子網路。

#### <a name="allowed-internet-tooweb-server"></a>（允許）網際網路 tooWeb 伺服器
1. 網際網路使用者從 SecSvc001.CloudApp.Net (網際網路面向雲端服務) 要求 HTTP 頁面
2. 雲端服務將流量透過開啟連接埠 80 上 10.0.0.4:80 的 toofirewall 介面上的端點
3. 指派 tooSecurity 子網路，所以系統 NSG 規則允許流量 toofirewall 沒有 NSG
4. 流量達到 hello 防火牆 (10.0.1.4) 的內部 IP 位址
5. 防火牆開始處理規則：
   1. FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則
   2. FW 規則 2-5 （RDP 規則） 不套用，請移動 toonext 規則
   3. FW 規則 6 (應用程式： Web) 會套用，允許流量，防火牆 Nat 它 too10.0.1.4 (IIS01)
6. hello Frontend 子網路會開始處理輸入的規則：
   1. NSG 規則 1 （封鎖網際網路） 並不適用 (此流量已 NAT 像 hello 防火牆，因此 hello 來源位址現在是 hello 防火牆，它會在 hello 安全性子網路上，看到 hello Frontend 子網路 NSG toobe 「 本機 」 流量，因此允許)，移動 toonext 規則
   2. 預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則
7. IIS01 接聽 web 流量、 收到此要求，並開始處理 hello 要求
8. IIS01 嘗試後端子網路上的 FTP 工作階段 tooAppVM01 tooinitiates
9. Frontend 子網路上的 hello UDR 路由可讓 hello 防火牆 hello 下一個躍點
10. Frontend 子網路上沒有輸出規則，允許流量
11. 防火牆開始處理規則：
    1. FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則
    2. 不適用 FW 規則 2-5 （RDP 規則），移動 toonext 規則
    3. FW 規則 6 (應用程式： Web) 不會套用，請移動 toonext 規則
    4. FW 規則 7 (應用程式： 後端) 會套用，允許流量，防火牆將轉送流量 too10.0.2.5 (AppVM01)
12. hello 後端子網路會開始處理輸入的規則：
    1. NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則
    2. 預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則
13. AppVM01 收到 hello 要求，並起始 hello 工作階段，而會回應
14. 後端子網路上的 hello UDR 路由可讓 hello 防火牆 hello 下一個躍點
15. 因為允許在後端子網路 hello 回應 hello 沒有輸出 NSG 規則
16. 因為這傳回流量上建立之工作階段 hello 防火牆傳送 hello 回應後 toohello 網頁伺服器 (IIS01)
17. Frontend 子網路開始處理輸入規則：
    1. NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則
    2. 預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則
18. hello IIS 伺服器收到 hello 回應、 完成 AppVM01，hello 交易，然後完成 建立 hello HTTP 回應，這個 HTTP 回應會傳送 toohello 要求者
19. 由於有允許前端子網路 hello 回應 hello 上的沒有輸出 NSG 規則
20. hello HTTP 回應的叫用 hello 防火牆和 NAT 工作階段因為這是建立 hello 回應 tooan 接受 hello 防火牆
21. hello 防火牆會重新導向 hello 回應後 toohello 網際網路使用者
22. 由於沒有任何輸出 NSG 規則或 UDR 躍點 hello Frontend 子網路上允許 hello 回應，而 hello 網際網路使用者會收到要求的 hello 網頁。

#### <a name="allowed-internet-rdp-toobackend"></a>（允許）網際網路 RDP tooBackend
1. 網際網路上的伺服器系統管理員要求 RDP 工作階段 tooAppVM01 透過 SecSvc001.CloudApp.Net:8025，8025 所在 hello"RDP tooAppVM01 」 防火牆規則的 hello 指派給使用者的連接埠號碼
2. hello 雲端服務則傳遞 8025 toofirewall 介面連接埠上 10.0.0.4:8025 流量通過 hello 開放式端點
3. 指派 tooSecurity 子網路，所以系統 NSG 規則允許流量 toofirewall 沒有 NSG
4. 防火牆開始處理規則：
   1. FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則
   2. 不會套用 FW 規則 2 (RDP IIS)，移動 toonext 規則
   3. FW 規則 3 (RDP DNS01) 不會套用移動 toonext 規則
   4. FW 規則 4 (RDP AppVM01) 會套用，允許流量，防火牆 Nat 它 too10.0.2.5:3386 （AppVM01 上的 RDP 連接埠）
5. hello 後端子網路會開始處理輸入的規則：
   1. NSG 規則 1 （封鎖網際網路） 並不適用 (此流量已 NAT 像 hello 防火牆，因此 hello 來源位址現在是 hello 防火牆，它會在 hello 安全性子網路上，看到 hello 後端子網路 NSG toobe 「 本機 」 流量，因此允許)，移動 toonext 規則
   2. 預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則
6. AppVM01 正在接聽 RDP 流量並回應
7. 由於沒有輸出 NSG 規則，會套用預設規則並允許傳回的流量
8. UDR 路由傳出流量 toohello 防火牆為 hello 下一個躍點
9. 因為這傳回流量上建立之工作階段 hello 防火牆傳送 hello 回應後 toohello 網際網路使用者
10. 已啟用 RDP 工作階段
11. AppVM01 會提示輸入使用者名稱和密碼

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(允許) DNS 伺服器上的 Web 伺服器 DNS 查閱
1. Web 伺服器，IIS01，需要的資料摘要在 www.data.gov，但需要 tooresolve hello 位址。
2. hello 的網路組態 hello VNet 清單 DNS01 (10.0.2.4 hello 後端子網路上) 做為主要 DNS 伺服器 hello，IIS01 傳送 hello DNS 要求 tooDNS01
3. UDR 路由傳出流量 toohello 防火牆為 hello 下一個躍點
4. 沒有輸出的 NSG 規則是繫結的 toohello Frontend 子網路，允許流量
5. 防火牆開始處理規則：
   1. FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則
   2. 不適用 FW 規則 2-5 （RDP 規則），移動 toonext 規則
   3. 不適用 FW 規則 6 和 7 （應用程式的規則），移動 toonext 規則
   4. FW 規則 8 (tooInternet) 不會套用移動 toonext 規則
   5. FW 規則 9 (DNS) 會套用，允許流量，防火牆將轉送流量 too10.0.2.4 (DNS01)
6. hello 後端子網路會開始處理輸入的規則：
   1. NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則
   2. 預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則
7. DNS 伺服器收到 hello 要求
8. DNS 伺服器沒有快取的 hello 位址和要求的根 DNS 伺服器上 hello 網際網路
9. UDR 路由傳出流量 toohello 防火牆為 hello 下一個躍點
10. Backend 子網路上沒有輸出 NSG 規則，允許流量
11. 防火牆開始處理規則：
    1. FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則
    2. 不適用 FW 規則 2-5 （RDP 規則），移動 toonext 規則
    3. 不適用 FW 規則 6 和 7 （應用程式的規則），移動 toonext 規則
    4. FW 規則 8 (tooInternet) 會套用，允許流量，工作階段已 SNAT 推出 tooroot hello 網際網路上的 DNS 伺服器
12. 網際網路 DNS 伺服器回應，因為此工作階段起始從 hello 防火牆，hello 回應接受 hello 防火牆
13. 因為這是已建立的工作階段，hello 防火牆轉送 hello 回應 toohello 起始伺服器，DNS01
14. hello 後端子網路會開始處理輸入的規則：
    1. NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則
    2. 預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則
15. hello DNS 伺服器會接收和快取 hello 回應，並再回應 toohello 初始要求後 tooIIS01
16. 後端子網路上的 hello UDR 路由可讓 hello 防火牆 hello 下一個躍點
17. Hello 後端子網路上不存在任何輸出 NSG 規則，允許流量
18. 這是建立之工作階段上 hello 防火牆，轉寄 hello 回應 hello 防火牆後 toohello IIS 伺服器
19. Frontend 子網路開始處理輸入規則：
    1. 套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則
    2. hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量
20. IIS01 DNS01 收到 hello 回應

#### <a name="allowed-backend-server-toofrontend-server"></a>（允許）後端伺服器 tooFrontend 伺服器
1. 系統管理員登入透過 RDP tooAppVM02 要求直接從 hello IIS01 伺服器，透過 windows 檔案總管中的檔案
2. 後端子網路上的 hello UDR 路由可讓 hello 防火牆 hello 下一個躍點
3. 因為允許在後端子網路 hello 回應 hello 沒有輸出 NSG 規則
4. 防火牆開始處理規則：
   1. FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則
   2. 不適用 FW 規則 2-5 （RDP 規則），移動 toonext 規則
   3. 不適用 FW 規則 6 和 7 （應用程式的規則），移動 toonext 規則
   4. FW 規則 8 (tooInternet) 不會套用移動 toonext 規則
   5. 不會套用 FW 規則 9 (DNS)，移動 toonext 規則
   6. FW 規則 10 （內部子網路） 會套用，允許流量，防火牆會傳遞流量 too10.0.1.4 (IIS01)
5. Frontend 子網路開始處理輸入規則：
   1. NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則
   2. 預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則
6. 假設適當的驗證和授權，IIS01 接受 hello 要求和回應
7. Frontend 子網路上的 hello UDR 路由可讓 hello 防火牆 hello 下一個躍點
8. 由於有允許前端子網路 hello 回應 hello 上的沒有輸出 NSG 規則
9. 因為這是現有的工作階段上 hello 防火牆允許此回應與 hello 防火牆傳回 hello 回應 tooAppVM02
10. Backend 子網路開始處理輸入規則：
    1. NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則
    2. 預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則
11. AppVM02 收到 hello 回應

#### <a name="denied-internet-direct-tooweb-server"></a>（拒絕）網際網路直接 tooWeb 伺服器
1. 網際網路的使用者嘗試 tooaccess hello web 伺服器，IIS01，透過 hello FrontEnd001.CloudApp.Net 服務
2. 因為沒有開啟以供 HTTP 流量的端點，這就不會通過 hello 雲端服務，並不會連線到 hello 伺服器
3. 如果基於某些原因，hello 端點處於開啟狀態，在 hello Frontend 子網路上的 hello NSG （區塊網際網路） 會封鎖此流量
4. 最後，hello 前端子網路 UDR 路由傳送會從 IIS01 toohello 防火牆 hello 下一個躍點，為傳送任何輸出流量，而且 hello 防火牆會認為這是對稱的流量，卸除 hello 輸出回應因此會有至少三個獨立層的防禦之間 hello 網際網路和 IIS01 透過防止未經授權的/不適當的存取其雲端服務。

#### <a name="denied-internet-toobackend-server"></a>（拒絕）網際網路 tooBackend 伺服器
1. 網際網路的使用者嘗試 tooaccess AppVM01 上的檔案，即可透過 hello BackEnd001.CloudApp.Net 服務
2. 因為不有開啟的檔案共用的任何端點，這不會傳送 hello 雲端服務，並不會連線到 hello 伺服器
3. 如果基於某些原因，hello 端點處於開啟狀態，hello NSG （區塊網際網路） 會封鎖此流量
4. 最後，hello UDR 路由就會從 AppVM01 toohello 防火牆 hello 下一個躍點，為傳送任何輸出流量，而且 hello 防火牆會認為這是對稱的流量，卸除 hello 輸出回應因此有防禦機制以之間至少三個獨立的圖層hello 網際網路和 AppVM01，透過其雲端服務，防止未經授權的/不適當的存取。

#### <a name="denied-frontend-server-toobackend-server"></a>（拒絕）前端伺服器 tooBackend 伺服器
1. 假設 IIS01 已遭到洩露，而且正在嘗試伺服器 tooscan hello 後端子網路的惡意程式碼。
2. hello 前端子網路 UDR 路由傳送會傳送任何輸出流量從 IIS01 toohello 防火牆為 hello 下一個躍點。 這不是可改變的 hello 危害 VM。
3. 如果 hello 要求 tooAppVM01 或可能無法 hello （因為 tooFW 規則 7 和 9） 的防火牆允許流量的 DNS 查閱 toohello DNS 伺服器 hello 防火牆會處理 hello 流量。 所有其他流量則會遭 FW 規則 11 (全部拒絕) 封鎖。
4. 進階威脅偵測是否已啟用 hello 防火牆 （其未涵蓋在本文件中，請參閱進階威脅功能您特定的網路應用裝置 hello 廠商文件），甚至會允許 hello 基本轉送規則的流量在這個討論如果 hello 流量包含已知的簽章或進階的威脅規則的旗標的模式，就無法防止文件。

#### <a name="denied-internet-dns-lookup-on-dns-server"></a>(拒絕) DNS 伺服器上的網際網路 DNS 查閱
1. 網際網路的使用者嘗試 toolookup DNS01 內部 DNS 記錄透過 BackEnd001.CloudApp.Net 服務 
2. 因為沒有開啟以供 DNS 流量的端點，這就不會通過 hello 雲端服務，並不會連線到 hello 伺服器
3. 如果基於某些原因，hello 端點處於開啟狀態，hello Frontend 子網路上的 hello NSG 規則 （區塊網際網路） 會封鎖此流量
4. 最後，hello 後端子網路 UDR 路由傳送會從 DNS01 toohello 防火牆 hello 下一個躍點，為傳送任何輸出流量，而且 hello 防火牆會認為這是對稱的流量，卸除輸出回應因此會有至少三個獨立層的 hello防禦之間 hello 網際網路和 DNS01 透過防止未經授權的/不適當的存取其雲端服務。

#### <a name="denied-internet-toosql-access-through-firewall"></a>（拒絕）透過防火牆存取網際網路 tooSQL
1. 網際網路使用者從 SecSvc001.CloudApp.Net (網際網路面向雲端服務) 要求 SQL 資料
2. 因為沒有開啟以供 SQL 的端點，這不會傳送 hello 雲端服務，並不會到達 hello 防火牆
3. 如果基於某些原因，SQL 端點處於開啟狀態，hello 防火牆就會開始處理規則：
   1. FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則
   2. FW 規則 2-5 （RDP 規則） 不套用，請移動 toonext 規則
   3. 不適用 FW 規則 6 和 7 （應用程式的規則），移動 toonext 規則
   4. FW 規則 8 (tooInternet) 不會套用移動 toonext 規則
   5. 不會套用 FW 規則 9 (DNS)，移動 toonext 規則
   6. 不會套用 FW 規則 10 （內部子網路），移動 toonext 規則
   7. FW 規則 11 (全部拒絕) 適用，封鎖流量，停止處理規則

## <a name="references"></a>參考
### <a name="main-script-and-network-config"></a>主要的指令碼和網路組態
在 PowerShell 指令碼檔案中儲存 hello 完整的指令碼。 將儲存到檔案中名為"NetworkConf2.xml"hello 網路組態。
視需要修改 hello 使用者定義的變數。 執行 hello 指令碼，然後遵循 hello 防火牆規則設定指示上述。

#### <a name="full-script"></a>完整指令碼
此指令碼，會根據 hello 使用者定義的變數：

1. 連接 tooan Azure 訂用帳戶
2. 建立新的儲存體帳戶
3. 建立新的 VNet 和 hello 網路組態檔中所定義的三個子網路
4. 建置五部虛擬機器：1 個防火牆和 4 個 Windows Server VM
5. 設定 UDR，包括：
   1. 建立兩個新的路由表
   2. 新增路由 toohello 資料表
   3. 繫結資料表 tooappropriate 子網路
6. 啟用 hello NVA 中的 IP 轉送
7. 設定 NSG，包括：
   1. 建立 NSG
   2. 新增規則
   3. 繫結 hello NSG toohello 適當的子網路

此 PowerShell 指令碼應該在連線到網際網路的電腦或伺服器上本機執行。

> [!IMPORTANT]
> 此指令碼在執行時，PowerShell 中可能會跳出警告或其他參考訊息。 只有紅色字體的錯誤訊息才需要擔心。
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>網路組態檔
儲存此 xml 檔，以更新的位置，並新增 hello 連結 toothis 檔案 toohello $NetworkConfigFile 變數上述 hello 指令碼中。

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>範例應用程式指令碼
如果您想 tooinstall 範例應用程式，和其他周邊網路的範例，其中一個已提供在 hello 下列連結：[範例應用程式指令碼][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "具有 NVA、NSG 和 UDR 的雙向 DMZ"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Hello 防火牆規則的邏輯檢視"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "建立前端網路物件"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "建立 DNS 伺服器物件"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "預設 RDP 規則的複本"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 規則"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "應用程式重新導向圖示"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "目的地 NAT 圖示"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "傳遞圖示"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "防火牆管理規則"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "防火牆 RDP 規則"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "防火牆 Web 規則"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "防火牆 AppVM01 規則"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "防火牆輸出規則"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "防火牆 DNS 規則"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "防火牆內部 VNet 規則"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "防火牆拒絕規則"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "防火牆規則啟用"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
