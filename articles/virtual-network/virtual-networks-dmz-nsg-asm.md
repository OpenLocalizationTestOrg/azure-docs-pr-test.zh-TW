---
title: "aaaAzure DMZ 範例 – 建立簡單的周邊網路與 Nsg |Microsoft 文件"
description: "建置具有網路安全性群組 (NSG) 的 DMZ"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>範例 1 – 使用 NSG 搭配傳統 PowerShell 建立簡單的 DMZ
[傳回 toohello 安全性界限最佳作法頁面][HOME]

> [!div class="op_single_selector"]
> * [Resource Manager 範本](virtual-networks-dmz-nsg.md)
> * [傳統 - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

此範例會建立包含四個 Windows 伺服器和網路安全性群組的基本 DMZ。 這個範例會說明每個相關 PowerShell 命令 tooprovide hello 更深入的了解每個步驟。 另外還有流量案例 > 一節 tooprovide 的深入了解逐步如何流量就會繼續進行 hello 層級的防禦 hello 周邊網路。 最後，在 hello references 區段中是 hello 完整程式碼和指示 toobuild 此環境 tootest 和試驗各種案例。 

![具有 NSG 的輸入 DMZ][1]

## <a name="environment-description"></a>環境描述
在此範例中的訂用帳戶包含 hello 下列資源：

* 兩個雲端服務：“FrontEnd001” 和 “BackEnd001”
* 一個虛擬網路 “CorpNetwork”，包含兩個子網路：“FrontEnd” 和 “BackEnd”
* 已套用的 tooboth 子網路的網路安全性群組
* 一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)
* 兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)
* 一個代表 DNS 伺服器的 Windows Server ("DNS01")

在 hello 參考區段中，沒有建立大多數的 hello 環境在此範例中所述的 PowerShell 指令碼。 建置 hello Vm 和虛擬網路，由 hello 範例指令碼，雖然不詳述於本文件說明。 

toobuild hello 環境。

1. 儲存 hello 網路組態 xml 檔案包含在 hello 參考一節 （名稱、 位置和 IP 位址 toomatch hello 指定案例與更新）
2. Hello 指令碼 toomatch hello 環境 hello 指令碼中的更新 hello 使用者變數是 toobe 執行 （訂用帳戶、 服務名稱等等）
3. 在 PowerShell 中執行 hello 指令碼

>[!Note]
>表示在 hello PowerShell 指令碼中的 hello 區域必須符合表示 hello 網路組態 xml 檔中的 hello 區域。
>
>

一旦 hello 指令碼執行成功的其他選擇性步驟可能會，hello 參考一節中兩個指令碼 tooset hello web 伺服器和應用程式伺服器與簡單的 web 應用程式 tooallow 測試此周邊網路設定。

hello 下列各節提供網路安全性群組和其運作方式如這個範例的逐步解說的 hello PowerShell 指令碼的索引鍵行的詳細的的描述。

## <a name="network-security-groups-nsg"></a>網路安全性群組 (NSG)
此範例會組建 NSG 群組，然後載入六個規則。 

> [!TIP]
> 一般而言，您應該先建立特定的 「 允許 」 規則，然後上次 hello 一般 「 拒絕 」 規則。 指派優先順序的 hello 規定哪些規則會先評估。 一旦流量找到 tooapply tooa 特定規則，則會不評估任何進一步的規則。 NSG 規則可套用在 hello 中輸入或輸出方向 （從 hello 觀點 hello 子網路）。
> 
> 

以宣告方式，下列規則的 hello 正在建置輸入流量：

1. 允許內部 DNS 流量 (連接埠 53)
2. 允許從 hello 網際網路 tooany VM 的 RDP 流量 （連接埠 3389）
3. 允許從 hello 網際網路 tooweb 伺服器 (IIS01) 的 HTTP 流量 （連接埠 80）
4. 允許從 IIS01 tooAppVM1 任何流量 （所有連接埠）
5. 任何流量 （所有連接埠），從 hello 網際網路 toohello 拒絕整個 VNet （這兩個子網路）
6. 拒絕任何從 hello Frontend 子網路 toohello 後端子網路的流量 （所有連接埠）

與這些規則繫結的 tooeach 子網路中，輸入 hello Internet toohello 網頁伺服器從 HTTP 要求是否兩者的規則 3 （允許） 及 5 （拒絕） 將會套用，但由於規則 3 具有較高的優先順序，只將套用的規則 5 就不會發生。 因此 hello HTTP 要求會允許 toohello web 伺服器。 如果該相同流量已嘗試 tooreach hello DNS01 伺服器，hello 第一個 tooapply 和 hello 流量就不會允許 toopass toohello 伺服器是規則 5 （拒絕）。 規則 6 (Deny) 會封鎖從交談 toohello 後端的子網路 （除了規則 1 和 4 中允許的流量） hello Frontend 子網路中，如果攻擊者竊取 hello web 上的應用程式 hello 前端，hello 攻擊者就此規則集可保護 hello 後端 」 網路有限存取 toohello 後端 「 受保護 」 (只公開 hello AppVM01 伺服器上的 tooresources) 網路。

沒有預設輸出的規則，可讓流量輸出 toohello 網際網路。 在此範例中，我們會允許輸出流量，並不會修改任何輸出規則。 toolock 下兩個方向的流量，使用者定義路由是必要項，會在 「 範例 3 」 探索上 hello[安全性界限最佳作法頁面][HOME]。

每個規則中討論更多詳細資料，如下所示 (**注意**: hello 遵循清單開頭，以貨幣符號的任何項目 (例如： $NSGName) 是此文件 hello 參考 > 一節中的 hello 指令碼的使用者定義變數):

1. 第一次網路安全性群組必須建置 toohold hello 規則：

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. 在此範例中的 hello 第一個規則可讓 DNS hello 後端子網路上所有的內部網路 toohello DNS 伺服器之間的流量。 hello 規則有一些重要的參數：
   
   * 「類型」表示此規則會生效的傳輸流量方向。 hello 方向是從 hello 的觀點來看 hello 子網路或虛擬機器 （取決於位置會繫結此 NSG）。 因此如果類型是 「 輸入 」 流量輸入 hello 子網路、 hello 規則將會套用，且離開 hello 子網路的流量不會受到此規則。
   * "Priority"設定 hello 順序評估流量。 hello hello 數字 hello 高 hello 優先順序。 當規則適用於特定 tooa 流量時，則會不處理任何進一步的規則。 因此如果優先權 1 的規則允許流量，和優先順序為 2 的規則，拒絕的流量，而且這兩個規則套用 tootraffic 則 hello 流量 someserver.mycompany.com tooflow （因為規則 1 有更高的優先順序花費效果，並套用任何進一步的規則）。
   * “Action” 指出受此規則影響的流量是要封鎖或允許。

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. 此規則可讓您從 hello 網際網路 toohello RDP 連接埠上 hello 的任何伺服器上的 RDP 流量 tooflow 繫結的子網路。 此規則使用兩種特殊位址前置詞：“VIRTUAL_NETWORK” 和 “INTERNET”。 這些標記是簡單的方式 tooaddress 較大的類別目錄的位址前置詞。

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. 這個規則允許輸入的網際網路流量 toohit hello web 伺服器。 此規則不會變更 hello 路由行為。 hello 規則僅允許針對 IIS01 toopass 的流量。 因此從 hello 網際網路的流量是否有 hello web 伺服器，做為其目的地，此規則會允許它，並停止進一步處理規則。 （在 hello 規則優先順序 140 所有其他傳入的網際網路流量會封鎖）。 如果您只在處理 HTTP 流量，這項規則可以更進一步地限制的 tooonly 允許目的地連接埠 80。

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. 此規則可讓從 hello IIS01 伺服器流量 toopass toohello AppVM01 伺服器，更新規則封鎖所有其他前端 tooBackend 流量。 應加入這項規則，如果 hello 連接埠已知的 tooimprove。 例如，如果 hello IIS 伺服器已達到只有 SQL Server 上 AppVM01，hello 目的地連接埠範圍應該變更"*"（任何） too1433 (hello SQL 連接埠) 進而較小的輸入的攻擊介面上 AppVM01 應該 hello web 應用程式不會受到危害。

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. 此規則會拒絕 hello 網際網路 tooany 網路上的伺服器 hello 流量。 Hello 規則優先順序 110 和 120 hello 效果為 tooallow 只有輸入的網際網路流量 toohello 防火牆和伺服器上的 RDP 連接埠而封鎖所有其他項目。 此規則是 「 保險 」 規則 tooblock 未預期的所有流程。
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. hello 最終規則，拒絕來自 hello Frontend 子網路 toohello 後端子網路流量。 由於這個規則唯一的輸入的規則，（從後端 toohello 前端 hello) 允許反向的流量。

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a>流量案例
#### <a name="allowed-internet-tooweb-server"></a>(*允許*) 網際網路 tooweb 伺服器
1. 網際網路使用者從 FrontEnd001.CloudApp.Net (網際網路面向雲端服務) 要求 HTTP 頁面
2. 雲端服務會傳遞流量透過連接埠 80 IIS01 朝上開啟端點 （hello web 伺服器）
3. Frontend 子網路開始處理輸入規則：
   1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
   2. NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則
   3. NSG 規則 3 (網際網路 tooIIS01) 會套用，流量會允許中停止的規則處理
4. 流量叫用內部 IP 位址的 hello web 伺服器 IIS01 (10.0.1.5)
5. IIS01 接聽 web 流量、 收到此要求，並開始處理 hello 要求
6. IIS01 詢問 hello SQL Server 上 AppVM01 資訊
7. Frontend 子網路上沒有輸出規則，所以允許流量
8. hello 後端子網路會開始處理輸入的規則：
   1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
   2. NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則
   3. NSG 規則 3 (網際網路 tooFirewall) 不會套用移動 toonext 規則
   4. NSG 規則 4 (IIS01 tooAppVM01) 會套用，流量會允許中停止的規則處理
9. AppVM01 收到 hello SQL 查詢並予以回應
10. 由於 hello 後端子網路上有沒有輸出的規則，允許 hello 回應
11. Frontend 子網路開始處理輸入規則：
    1. 套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則
    2. hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量。
12. hello IIS 伺服器收到 hello SQL 回應，並完成 hello HTTP 回應，並將傳送 toohello 要求者
13. 因為 hello Frontend 子網路上沒有任何輸出規則 hello 回應，而 hello 網際網路使用者會收到要求的 hello 網頁。

#### <a name="allowed-rdp-toobackend"></a>(*允許*) RDP toobackend
1. 網際網路上的伺服器系統管理員要求的 BackEnd001.CloudApp.Net:xxxxx 其中 xxxxx 是 RDP tooAppVM01 hello 隨機指派通訊埠編號上的 RDP 工作階段 tooAppVM01 （hello Azure 入口網站上或透過 PowerShell，可以找到 hello 指派連接埠）
2. Backend 子網路開始處理輸入規則：
   1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
   2. NSG 規則 2 (RDP) 適用，允許流量，停止處理規則
3. 由於沒有輸出規則，會套用預設規則並允許傳回的流量
4. 已啟用 RDP 工作階段
5. AppVM01 會提示您輸入 hello 使用者名稱和密碼

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(允許) DNS 伺服器上的 Web 伺服器 DNS 查閱
1. Web 伺服器，IIS01，需要的資料摘要在 www.data.gov，但需要 tooresolve hello 位址。
2. hello 的網路組態 hello VNet 清單 DNS01 (10.0.2.4 hello 後端子網路上) 做為主要 DNS 伺服器 hello，IIS01 傳送 hello DNS 要求 tooDNS01
3. Frontend 子網路上沒有輸出規則，允許流量
4. Backend 子網路開始處理輸入規則：
   * NSG 規則 1 (DNS) 適用，允許流量，停止處理規則
5. DNS 伺服器收到 hello 要求
6. DNS 伺服器沒有快取的 hello 位址和要求的根 DNS 伺服器上 hello 網際網路
7. Backend 子網路上沒有輸出規則，允許流量
8. 網際網路 DNS 伺服器回應，因為此工作階段已在內部起始，hello 允許回應
9. DNS 伺服器快取 hello 回應及回應 toohello 初始要求後 tooIIS01
10. Backend 子網路上沒有輸出規則，允許流量
11. Frontend 子網路開始處理輸入規則：
    1. 套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則
    2. hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量
12. IIS01 DNS01 收到 hello 回應

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(允許) Web 伺服器存取 AppVM01 上的檔案
1. IIS01 要求 AppVM01 上的檔案
2. Frontend 子網路上沒有輸出規則，允許流量
3. hello 後端子網路會開始處理輸入的規則：
   1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
   2. NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則
   3. NSG 規則 3 (網際網路 tooIIS01) 不會套用移動 toonext 規則
   4. NSG 規則 4 (IIS01 tooAppVM01) 會套用，流量會允許中停止的規則處理
4. AppVM01 收到 hello 要求和回應檔案 （假設已獲授權存取）
5. 由於 hello 後端子網路上有沒有輸出的規則，允許 hello 回應
6. Frontend 子網路開始處理輸入規則：
   1. 套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則
   2. hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量。
7. hello IIS 伺服器收到 hello 檔案

#### <a name="denied-web-toobackend-server"></a>(*拒絕*) Web toobackend 伺服器
1. 網際網路使用者嘗試 tooaccess AppVM01 上的檔案，即可透過 hello BackEnd001.CloudApp.Net 服務
2. 因為不沒有開啟的檔案共用的任何端點，此流量不會傳送 hello 雲端服務，並不會連線到 hello 伺服器
3. 如果基於某些原因，hello 端點處於開啟狀態，NSG 規則 5 (網際網路 tooVNet) 會封鎖此流量

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(拒絕) DNS 伺服器上的 Web DNS 查閱
1. 網際網路使用者嘗試註冊的內部 DNS 記錄上 DNS01 hello BackEnd001.CloudApp.Net 服務透過 toolook
2. 因為沒有開啟以供 DNS 的端點，此流量不會傳送 hello 雲端服務，並不會連線到 hello 伺服器
3. 如果基於某些原因，hello 端點處於開啟狀態，NSG 規則 5 (網際網路 tooVNet) 會封鎖此流量 (注意： 不原因有兩個適用於該規則 1 」 (DNS)、 第一個 hello 來源位址是 hello 網際網路，此規則只適用於 toohello 也為 hello 本機 VNet 來源此規則是允許規則，讓它永遠不會拒絕的流量）

#### <a name="denied-web-toosql-access-through-firewall"></a>(*拒絕*) Web tooSQL 透過防火牆存取
1. 網際網路使用者從 FrontEnd001.CloudApp.Net (網際網路面向雲端服務) 要求 SQL 資料
2. 因為沒有開啟以供 SQL 的端點，此流量不會傳送 hello 雲端服務，並不會到達 hello 防火牆
3. 如果端點處於開啟狀態的因為某些原因，hello Frontend 子網路會開始處理輸入的規則：
   1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
   2. NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則
   3. NSG 規則 3 (網際網路 tooIIS01) 會套用，流量會允許中停止的規則處理
4. 流量叫用內部 IP 位址的 hello IIS01 (10.0.1.5)
5. IIS01 未接聽通訊埠 1433，因此沒有回應 toohello 要求

## <a name="conclusion"></a>結論
這個範例是相當簡單且直接正向的方式，隔離 hello 後端的輸入流量子網路。

您可以在[這裡][HOME]找到更多範例和網路安全性界限的概觀。

## <a name="references"></a>參考
### <a name="main-script-and-network-config"></a>主要的指令碼和網路組態
在 PowerShell 指令碼檔案中儲存 hello 完整的指令碼。 Hello 儲存到檔案中的網路設定名為"NetworkConf1.xml。 」
修改 hello 使用者定義的變數做為必要且執行 hello 指令碼。

#### <a name="full-script"></a>完整指令碼
此指令碼，會根據 hello 使用者定義的變數。

1. 連接 tooan Azure 訂用帳戶
2. 建立儲存體帳戶
3. 建立 VNet 和 hello 網路組態檔中所定義的兩個子網路
4. 建立四個 Windows Server VM
5. 設定 NSG，包括：
   * 建立 NSG
   * 在其中填入規則
   * 繫結 hello NSG toohello 適當的子網路

此 PowerShell 指令碼應該在連線到網際網路的電腦或伺服器上本機執行。

> [!IMPORTANT]
> 此指令碼在執行時，PowerShell 中可能會跳出警告或其他參考訊息。 只有紅色字體的錯誤訊息才需要擔心。
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

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

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a>網路組態檔
與更新的位置儲存此 xml 檔並加入 hello 連結 toothis 檔案 toohello $NetworkConfigFile 變數 hello 上述指令碼中。

```XML
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
```

#### <a name="sample-application-scripts"></a>範例應用程式指令碼
如果您想 tooinstall 範例應用程式，和其他周邊網路的範例，其中一個已提供在 hello 下列連結：[範例應用程式指令碼][SampleApp]

## <a name="next-steps"></a>後續步驟
* 更新並儲存 XML 檔案
* 執行 hello PowerShell 指令碼 toobuild hello 環境
* 安裝 hello 範例應用程式
* 測試流經此 DMZ 的不同流量

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "具有 NSG 的輸入 DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

