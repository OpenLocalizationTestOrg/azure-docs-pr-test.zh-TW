---
title: "確認連線：Azure ExpressRoute 疑難排解指南 | Microsoft Docs"
description: "此頁面提供疑難排解與驗證結束 tooend 連線，ExpressRoute 電路的指示。"
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a>確認 ExpressRoute 連線
ExpressRoute，擴充到 hello Microsoft 雲端的內部部署網路，透過連線服務提供者來實現的私用連接，牽涉到下列三個不同的網路區域的 hello:

-   客戶網路
-   提供者網路
-   Microsoft 資料中心

本文件的 hello 目的是 toohelp 使用者 tooidentify 位置 （或即使） 有連線問題存在，而且內的區域，藉此 tooseek 協助從適當的團隊 tooresolve hello 問題。 如果 Microsoft 支援，則需要的 tooresolve 發生問題，開啟支援票證給[Microsoft 支援服務][Support]。

> [!IMPORTANT]
> 本文件是預定的 toohelp 診斷並修正簡單的問題。 它不是預期的 toobe Microsoft 支援的取代項目。 開啟支援票證給[Microsoft 支援服務][ Support]如果您是使用所提供的 hello 指引無法 toosolve hello 問題。
>
>

## <a name="overview"></a>概觀
hello 下列圖表顯示 hello 邏輯客戶網路 tooMicrosoft 網路使用 ExpressRoute 連線。
[![1]][1]

在之前圖表 hello，hello 數字會表示金鑰的網路點。 hello 網路點通常透過這份文件所參考其相關的數字。

依據 hello ExpressRoute 連線能力模型 （雲端 Exchange 代管、 點對點乙太網路連線或 Any-any (IPVPN)） hello 網路點 3 和 4 可能參數 （第 2 層的裝置）。 hello 所述的索引鍵的網路點如下所示：

1.  客戶計算裝置 (例如，伺服器或電腦)
2.  CE︰客戶邊緣路由器 
3.  PE (面對 CE)︰面對客戶邊緣路由器的提供者邊緣路由器/交換器。 指 tooas PE CEs 本文件中。
4.  PE (面對 MSEE)︰面對 MSEE 的提供者邊緣路由器/交換器。 指 tooas PE MSEEs 本文件中。
5.  MSEE：Microsoft Enterprise Edge (MSEE) ExpressRoute 路由器
6.  虛擬網路 (VNet) 閘道器
7.  計算 hello Azure VNet 上的裝置

如果使用 hello 雲端 Exchange 代管或點對點乙太網路連線的連線模型，hello 客戶邊緣路由器 (2) 會建立 BGP 對等與 MSEEs (5)。 網路點 3 和 4 仍會存在，但會化做透明的第 2 層裝置。

如果使用 hello Any-any (IPVPN) 連接模型，則 hello PEs （MSEE 面對） (4) 會建立 BGP 對等與 MSEEs (5)。 路由會再傳播後 toohello 客戶網路透過 hello IPVPN 服務提供者網路。

>[!NOTE]
>為了讓 ExpressRoute 有高可用性，Microsoft 需要在 MSEE (5) 和 PE-MSEE (4) 之間有一組備援的 BGP 工作階段。 我們也鼓勵您在客戶網路和 PE-CE 之間有一組備援的網路路徑。 不過，在任何-any (IPVPN) 連線模型中，單一的 CE 裝置 (2) 可能是連線的 tooone 或更多的 PEs (3)。
>
>

toovalidate ExpressRoute 電路，hello 遵循步驟涵蓋 （有相關聯的 hello 數字指示 hello 網路點）：
1. [確認路線的佈建和狀態 (5)](#validate-circuit-provisioning-and-state)
2. [確認至少已設定一個 ExpressRoute 對等互連 (5)](#validate-peering-configuration)
3. [驗證 ARP 之間 Microsoft 和 hello 服務提供者 （介於 4 到 5 之間的連結）](#validate-arp-between-microsoft-and-the-service-provider)
4. [驗證 BGP 和上 hello MSEE (4 too5 和 5 too6 如果 VNet 連接之間的 BGP) 路由](#validate-bgp-and-routes-on-the-msee)
5. [核取 hello 流量統計資料 （流量通過 5）](#check-the-traffic-statistics)

多個驗證和檢查將會加入 hello 未來，查看每個月 ！

##<a name="validate-circuit-provisioning-and-state"></a>確認路線的佈建和狀態
Hello 連接模型，不論 ExpressRoute 電路會具有 toobe 建立，因此服務產生循環的佈建金鑰。 佈建 ExpressRoute 路線會在 PE-MSEE (4) 和 MSEE (5) 之間建立備援的第 2 層連線。 如需有關 toocreate，如何修改、 佈建，以及確認 ExpressRoute 電路的詳細資訊，請參閱 hello 文章[建立及修改 ExpressRoute 電路][CreateCircuit]。

>[!TIP]
>服務機碼可唯一識別 ExpressRoute 路線。 大部分的這份文件中所述的 hello powershell 命令需要此金鑰。 此外，您需要協助來自 Microsoft 或 ExpressRoute 合作夥伴 tootroubleshoot ExpressRoute 問題，提供 hello 服務金鑰 tooreadily 識別 hello 循環。
>
>

###<a name="verification-via-hello-azure-portal"></a>透過 hello Azure 入口網站的驗證
在 hello Azure 入口網站，可以檢查的 ExpressRoute 電路的 hello 狀態選取![2][2] hello 在左提要欄位的功能表，然後選取 hello ExpressRoute 電路。 選取 ExpressRoute 電路列出 [所有資源] 下會開啟 hello ExpressRoute 電路刀鋒視窗。 在 hello ![3][3]區段 hello 刀鋒視窗中，hello ExpressRoute essentials 列出 hello 下列螢幕擷取畫面所示：

![4][4]    

在 hello ExpressRoute Essentials*電路狀態*指出 hello hello Microsoft 端上的 hello 循環狀態。 *提供者狀態*指出是否 hello 電路已*已佈建/未佈建*hello 服務提供者端。 

為操作的 ExpressRoute 電路 toobe，hello*電路狀態*必須*啟用*和 hello*提供者狀態*必須是*已佈建*.

>[!NOTE]
>如果 hello*電路狀態*是未啟用，請連絡[Microsoft 支援服務][Support]。 如果 hello*提供者狀態*為未佈建，請連絡您的服務提供者。
>
>

###<a name="verification-via-powershell"></a>透過 PowerShell 進行確認
toolist 所有 hello ExpressRoute 電路的資源群組中，請使用下列命令的 hello:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
>您可以透過 hello Azure 入口網站來取得資源群組名稱。 請參閱此文件的 hello 先前小節，並注意該 hello 資源群組名稱會列在 hello 範例螢幕擷取畫面。
>
>

tooselect 特定的 ExpressRoute 電路，在資源群組中，下列命令使用 hello:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

範例回應：

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

tooconfirm 如果 ExpressRoute 電路是否運作正常，請特別注意 toohello 下列欄位：

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
>如果 hello *CircuitProvisioningState*是未啟用，請連絡[Microsoft 支援服務][Support]。 如果 hello *ServiceProviderProvisioningState*為未佈建，請連絡您的服務提供者。
>
>

###<a name="verification-via-powershell-classic"></a>透過 PowerShell (傳統) 進行確認
toolist 所有 hello ExpressRoute 電路訂用帳戶，請使用下列命令的 hello:

    Get-AzureDedicatedCircuit

tooselect 特定的 ExpressRoute 電路，使用下列命令的 hello:

    Get-AzureDedicatedCircuit -ServiceKey **************************************

範例回應：

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

tooconfirm 如果 ExpressRoute 電路是否運作正常，請特別注意 toohello 下列欄位： ServiceProviderProvisioningState： 佈建狀態： 啟用

>[!NOTE]
>如果 hello*狀態*是未啟用，請連絡[Microsoft 支援服務][Support]。 如果 hello *ServiceProviderProvisioningState*為未佈建，請連絡您的服務提供者。
>
>

##<a name="validate-peering-configuration"></a>確認對等互連組態
Hello 服務提供者已完成的 hello 佈建 hello ExpressRoute 循環之後，可以透過 hello MSEE Pr (4) 和 MSEEs (5) 之間的 ExpressRoute 電路建立路由組態。 其中一個、 兩個或三個啟用的路由內容，可以有每個 ExpressRoute 電路： Azure 私用對等互連 （流量 tooprivate 虛擬網路在 Azure 中）、 Azure 公用對等 （在 Azure 中流量 toopublic IP 位址，） 和 Microsoft 對等互連 (流量 tooOffice 365和 Dynamics 365）。 如需有關如何 toocreate 和修改路由組態，請參閱 hello 文章[建立及修改 ExpressRoute 電路的路由][CreatePeering]。

###<a name="verification-via-hello-azure-portal"></a>透過 hello Azure 入口網站的驗證
>[!IMPORTANT]
>Hello ExpressRoute 對等互連是其中的 Azure 入口網站中沒有已知的錯誤*不*如果 hello 服務提供者所設定的 hello 入口網站中顯示。 加入透過 hello 入口網站或 PowerShell ExpressRoute 對等互連*hello 服務提供者設定會覆寫*。 此動作會中斷 hello hello ExpressRoute 電路的路由和需要 hello 支援 hello 服務提供者 toorestore hello 設定並重新建立一般路由。 只能修改 hello ExpressRoute 對等互連，確定該 hello 服務提供者會提供僅第 2 層服務 ！
>
>

<p/>
>[!NOTE]
>如果第 3 層所提供的 hello 服務提供者和 hello 對等互連是空白的 hello 入口網站中，PowerShell 可以使用的 toosee hello 服務設定提供者設定。
>
>

在 hello Azure 入口網站，可以檢查 ExpressRoute 循環的狀態選取![2][2] hello 在左提要欄位的功能表，然後選取 hello ExpressRoute 電路。 選取 ExpressRoute 電路列出 [所有資源] 下會開啟 hello ExpressRoute 電路刀鋒視窗。 在 hello ![3][3] hello 刀鋒視窗中，hello ExpressRoute hello 下列螢幕擷取畫面所示，會被列 essentials 區段：

![5][5]

在上述範例中的 hello，記下 Azure 私用對等互連的路由內容會啟用，而不會啟用公用 Azure 和 Microsoft 對等互連的路由內容。 已成功啟用的對等互連內容也會有列出 hello 主要和次要的點對點 （需要 BGP） 子網路。 hello/30 子網路用於 hello MSEEs hello 介面 IP 位址和 PE MSEEs。 

>[!NOTE]
>如果未啟用的對等互連，請檢查 hello 主要和次要的子網路指派比對上 PE MSEEs hello 組態。 如果沒有，toochange hello 組態 MSEE 路由器上，請參閱太[建立及修改 ExpressRoute 電路的路由][CreatePeering]
>
>

###<a name="verification-via-powershell"></a>透過 PowerShell 進行確認
tooget hello Azure 私用對等互連設定詳細資料，使用下列命令的 hello:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

以下是已成功設定私人對等互連的回應範例︰

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 已成功啟用的對等內容，就必須列出 hello 主要和次要的位址首碼。 hello/30 子網路用於 hello MSEEs hello 介面 IP 位址和 PE MSEEs。

tooget hello Azure 公用對等互連設定詳細資料，使用下列命令的 hello:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

tooget hello Microsoft 對等互連設定詳細資料，請使用下列命令的 hello:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

如未設定對等互連，會顯示錯誤訊息。 Hello 電路內未設定時 hello 所述的對等 （Azure 公用對等互連，在此範例中） 的範例回應：

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
>如果未啟用的對等互連，檢查上 hello hello 指派的主要和次要子相符項目 hello 組態如果連結 PE MSEE。 也請檢查 hello 更正*VlanId*， *AzureASN*，和*PeerASN* MSEEs 上使用，且如果這些值對應 toohello hello 上使用的連結 PE MSEE。 如果選擇 MD5 雜湊，hello 共用的金鑰應該是相同 MSEE 和 PE MSEE 組上。 toochange hello 組態在 hello MSEE 路由器上的參閱太 [建立及修改 ExpressRoute 電路的路由] [CreatePeering]。  
>
>

### <a name="verification-via-powershell-classic"></a>透過 PowerShell (傳統) 進行確認
tooget hello Azure 私用對等互連設定詳細資料，使用下列命令的 hello:

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

以下是已成功設定私人對等互連的回應範例︰

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

已成功，啟用的對等的內容會有列出 hello 主要和次要對等子網路。 hello/30 子網路用於 hello MSEEs hello 介面 IP 位址和 PE MSEEs。

tooget hello Azure 公用對等互連設定詳細資料，使用下列命令的 hello:

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

tooget hello Microsoft 對等互連設定詳細資料，請使用下列命令的 hello:

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
>如果第 3 層對等互連已 hello 服務提供者所設定，設定透過 hello 入口網站或 PowerShell hello ExpressRoute 對等互連會覆寫 hello 服務提供者設定。 重設 hello 提供者端的對等設定需要 hello hello 服務提供者支援。 只能修改 hello ExpressRoute 對等互連，確定該 hello 服務提供者會提供僅第 2 層服務 ！
>
>

<p/>
>[!NOTE]
>如果未啟用的對等互連，請檢查 hello 主要和次要對等子網路指派比對 hello 上的設定 hello 如果連結 PE MSEE。 也請檢查 hello 更正*VlanId*， *AzureAsn*，和*PeerAsn* MSEEs 上使用，且如果這些值對應 toohello hello 上使用的連結 PE MSEE。 toochange hello 組態在 hello MSEE 路由器上的參閱太 [建立及修改 ExpressRoute 電路的路由] [CreatePeering]。
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a>Microsoft 與 hello 服務提供者之間驗證 ARP
本節使用 PowerShell (傳統) 命令。 如果您已經使用 PowerShell 的 Azure 資源管理員命令，請確定您有系統管理員/共同管理員存取 toohello 訂閱透過[Azure 傳統入口網站][OldPortal]。 疑難排解使用 Azure 資源管理員的命令，請參閱 toohello [hello Resource Manager 部署模型中的取得 ARP 表格][ ARP]文件。

>[!NOTE]
>可以使用 tooget ARP hello Azure 入口網站和 Azure 資源管理員 PowerShell 命令。 如果發生錯誤與 hello Azure 資源管理員 PowerShell 命令，傳統的 PowerShell 命令應能當做傳統的 PowerShell 命令也會搭配 Azure 資源管理員的 ExpressRoute 電路。
>
>

tooget hello 與 hello 私用對等互連 hello 主要 MSEE 路由器的 ARP 表格，請使用下列命令的 hello:

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Hello 命令，在 hello 成功案例的範例回應：

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

同樣地，您可以檢查 hello ARP 表格，從在 hello hello MSEE*主要*/*次要*路徑，如*私人*/ *公用*/*Microsoft*對等互連。

hello 下列範例顯示 hello 回應 hello 命令的對等互連的不存在。

    ARP Info:
       
>[!NOTE]
>如果沒有 hello ARP 表格 hello 介面的 IP 位址對應 tooMAC 位址，檢閱 hello 下列資訊：
>1. 如果 hello/30 子網路的 hello 第一個 IP 位址指派 hello 連結之間 hello MSEE PR 並用 MSEE MSEE PR hello 介面上 Azure 一律使用 MSEEs hello 第二個 IP 位址。
>2. 請確認是否 hello 客戶 （C-已標記） 和服務 （S 已標記） 的 VLAN 標記符合二者 MSEE PR 和 MSEE 組。
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a>驗證 BGP 和 hello MSEE 上的路由
本節使用 PowerShell (傳統) 命令。 如果您已經使用 PowerShell 的 Azure 資源管理員命令，請確定您有系統管理員/共同管理員存取 toohello 訂閱透過[Azure 傳統入口網站][OldPortal]

>[!NOTE]
>tooget BGP 資訊，這兩個 hello 可以使用 Azure 入口網站和 Azure 資源管理員 PowerShell 命令。 如果發生錯誤與 hello Azure 資源管理員 PowerShell 命令，傳統的 PowerShell 命令應能當做傳統的 PowerShell 命令也會搭配 Azure 資源管理員的 ExpressRoute 電路。
>
>

tooget hello 路由表 （BGP 芳鄰） 摘要特定路由內容，請使用下列命令的 hello:

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

以下是回應範例：

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

Hello 前面範例所示，hello 命令會為有用 toodetermine 的時間長度尚未建立 hello 路由的內容。 它也會指出 hello 對等路由器通告的路由前置詞數目。

>[!NOTE]
>如果 hello 狀態為作用中或閒置，請檢查 hello 主要和次要對等子網路指派比對 hello 上的設定 hello 如果連結 PE MSEE。 也請檢查 hello 更正*VlanId*， *AzureAsn*，和*PeerAsn* MSEEs 上使用，且如果這些值對應 toohello hello 上使用的連結 PE MSEE。 如果選擇 MD5 雜湊，hello 共用的金鑰應該是相同 MSEE 和 PE MSEE 組上。 toochange hello 組態在 hello MSEE 路由器上的參閱太[建立及修改 ExpressRoute 電路的路由][CreatePeering]。
>
>

<p/>
>[!NOTE]
>如果一段特定的對等互連，不連線到特定目的地，請檢查 hello 路由表的 hello MSEEs 屬於 toohello 特定對等的內容。 如果 hello 路由表中存在相符的前置詞 （可能是 Nat IP），然後檢查是否有防火牆/NSG Acl hello 路徑上，並允許 hello 流量。
>
>

tooget hello 完整路由表從 MSEE hello*主要*hello 特定路徑*私人*路由內容，下列命令使用 hello:

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Hello 命令的範例成功結果是：

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

同樣地，您可以檢查 hello 路由表，從在 hello hello MSEE*主要*/*次要*路徑，如*私人*/ *公用*/*Microsoft*對等的內容。

hello 下列範例顯示 hello 回應 hello 命令的對等互連的不存在：

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a>核取 hello 流量統計資料
tooget hello 和縮小-結合主要和次要路徑流量統計資料-位元組的對等的內容時，下列命令使用 hello:

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

Hello 命令的輸出範例是：

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

用於不存在，互連 hello 命令的輸出範例是：

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a>後續步驟
詳細的資訊或說明，請參閱下列連結查看 hello:

- [Microsoft 支援服務][Support]
- [建立和修改 ExpressRoute 路線][CreateCircuit]
- [建立和修改 ExpressRoute 路線的路由][CreatePeering]

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "ExpressRoute 邏輯連線"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "所有資源圖示"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "概觀圖示"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute 基本資料螢幕擷取畫面範例"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute 基本資料螢幕擷取畫面範例"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






