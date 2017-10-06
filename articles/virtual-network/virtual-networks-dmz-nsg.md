---
title: "aaaAzure DMZ 範例 – 建立簡單的周邊網路與 Nsg |Microsoft 文件"
description: "建置具有網路安全性群組 (NSG) 的 DMZ"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a>範例 1 – 使用 NSG 搭配 Azure Resource Manager 範本建立簡單的 DMZ
[傳回 toohello 安全性界限最佳作法頁面][HOME]

> [!div class="op_single_selector"]
> * [Resource Manager 範本](virtual-networks-dmz-nsg.md)
> * [傳統 - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

此範例會建立包含四個 Windows 伺服器和網路安全性群組的基本 DMZ。 這個範例會說明每個 hello 相關的範本區段 tooprovide 更深入的了解每個步驟。 另外還有流量案例 > 一節 tooprovide 逐步深入流量就會繼續進行的 hello 周邊網路中的 hello 保護層。 最後，在 hello references 區段中是 hello 完成範本的程式碼和指示 toobuild 此環境 tootest 和試驗各種案例。 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

![具有 NSG 的輸入 DMZ][1]

## <a name="environment-description"></a>環境描述
在此範例中的訂用帳戶包含 hello 下列資源：

* 單一資源群組
* 含有兩個子網路的虛擬網路；“FrontEnd” 和 “BackEnd”
* 已套用的 tooboth 子網路的網路安全性群組
* 一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)
* 兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)
* 一個代表 DNS 伺服器的 Windows Server ("DNS01")
* Hello 應用程式 web 伺服器相關聯的公用 IP 位址

在 hello 參考區段中，沒有連結 tooan Azure Resource Manager 範本建置這個範例中所述的 hello 環境。 建置 hello Vm 和虛擬網路，由 hello 範例範本，雖然不詳述於本文件說明。 

**toobuild 此環境**（詳細的指示是在 hello 的這份文件的 references 區段中;）

1. 部署 hello Azure 資源管理員範本： [Azure 快速入門範本][Template]
2. 安裝在 hello 範例應用程式：[範例應用程式指令碼][SampleApp]

>[!NOTE]
>在此情況下，hello IIS 伺服器 tooRDP tooany 後端伺服器作為 「 跳躍方塊 」。 第一部 RDP toohello IIS 伺服器，然後從 hello IIS 伺服器的 RDP toohello 後端伺服器。 或者，可以將公用 IP 與每個伺服器 NIC 相關聯以便更容易 RDP。
> 
>

hello 下列各節提供 hello 網路安全性群組和其運作方式如這個範例藉由查核透過金鑰行 hello Azure Resource Manager 範本的詳細的描述。

## <a name="network-security-groups-nsg"></a>網路安全性群組 (NSG)
此範例會組建 NSG 群組，然後載入六個規則。 

>[!TIP]
>一般而言，您應該先建立特定的 「 允許 」 規則，然後上次 hello 一般 「 拒絕 」 規則。 指派優先順序的 hello 規定哪些規則會先評估。 一旦流量找到 tooapply tooa 特定規則，則會不評估任何進一步的規則。 NSG 規則可套用在 hello 中輸入或輸出方向 （從 hello 觀點 hello 子網路）。
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

沒有預設輸出的規則，可讓流量輸出 toohello 網際網路。 在此範例中，我們會允許輸出流量，並不會修改任何輸出規則。 tooapply 安全性原則 tootraffic 雙向，使用者定義路由是必要項，會在 「 範例 3 」 探索上 hello[安全性界限最佳作法頁面][HOME]。

會詳細討論每個規則，如下所示︰

1. 網路安全性群組資源必須是具現化的 toohold hello 規則：

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. 在此範例中的 hello 第一個規則可讓 DNS hello 後端子網路上所有的內部網路 toohello DNS 伺服器之間的流量。 hello 規則有一些重要的參數：
  * 「 destinationAddressPrefix"-規則可以使用稱為 「 預設標記 」 的位址首碼的特殊類型，這些標記是允許輕鬆 tooaddress 的位址前置詞的較大類別目錄的系統提供的識別項。 此規則會使用 hello 預設標記 「 網際網路 」 toosignify 任何 hello VNet 外部位址。 其他前置詞標籤為 VirtualNetwork 和 AzureLoadBalancer。
  * 「方向」表示此規則會生效的傳輸流量方向。 hello 方向是從 hello 的觀點來看 hello 子網路或虛擬機器 （取決於位置會繫結此 NSG）。 因此如果方向是 「 輸入 」 流量輸入 hello 子網路、 hello 規則將會套用，且離開 hello 子網路的流量不會受到此規則。
  * "Priority"設定 hello 順序評估流量。 hello hello 數字 hello 高 hello 優先順序。 當規則適用於特定 tooa 流量時，則會不處理任何進一步的規則。 因此如果優先權 1 的規則允許流量，和優先順序為 2 的規則，拒絕的流量，而且這兩個規則套用 tootraffic 則 hello 流量 someserver.mycompany.com tooflow （因為規則 1 有更高的優先順序花費效果，並套用任何進一步的規則）。
  * “Access” 指出受此規則影響的流量是要封鎖 ("Deny") 或允許 ("Allow")。

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. 此規則可讓您從 hello 網際網路 toohello RDP 連接埠上 hello 的任何伺服器上的 RDP 流量 tooflow 繫結的子網路。 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. 這個規則允許輸入的網際網路流量 toohit hello web 伺服器。 此規則不會變更 hello 路由行為。 hello 規則僅允許針對 IIS01 toopass 的流量。 因此從 hello 網際網路的流量是否有 hello web 伺服器，做為其目的地，此規則會允許它，並停止進一步處理規則。 （在 hello 規則優先順序 140 所有其他傳入的網際網路流量會封鎖）。 如果您只在處理 HTTP 流量，這項規則可以更進一步地限制的 tooonly 允許目的地連接埠 80。

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. 此規則可讓從 hello IIS01 伺服器流量 toopass toohello AppVM01 伺服器，更新規則封鎖所有其他前端 tooBackend 流量。 應加入這項規則，如果 hello 連接埠已知的 tooimprove。 例如，如果 hello IIS 伺服器已達到只有 SQL Server 上 AppVM01，hello 目的地連接埠範圍應該變更"*"（任何） too1433 (hello SQL 連接埠) 進而較小的輸入的攻擊介面上 AppVM01 應該 hello web 應用程式不會受到危害。

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. 此規則會拒絕 hello 網際網路 tooany 網路上的伺服器 hello 流量。 Hello 規則優先順序 110 和 120 hello 效果為 tooallow 只有輸入的網際網路流量 toohello 防火牆和伺服器上的 RDP 連接埠而封鎖所有其他項目。 此規則是 「 保險 」 規則 tooblock 未預期的所有流程。

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. hello 最終規則，拒絕來自 hello Frontend 子網路 toohello 後端子網路流量。 由於這個規則唯一的輸入的規則，（從後端 toohello 前端 hello) 允許反向的流量。

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a>流量案例
#### <a name="allowed-internet-tooweb-server"></a>(*允許*) 網際網路 tooweb 伺服器
1. 網際網路使用者要求 HTTP 頁面從 hello 與 hello IIS01 NIC 的 NIC 相關聯的 hello 公用 IP 位址
2. hello 公用 IP 位址傳送流量 toohello 朝向 IIS01 VNet （hello web 伺服器）
3. Frontend 子網路開始處理輸入規則：
  1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
  2. NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則
  3. NSG 規則 3 (網際網路 tooIIS01) 會套用，流量會允許中停止的規則處理
4. 流量叫用內部 IP 位址的 hello web 伺服器 IIS01 (10.0.1.5)
5. IIS01 接聽 web 流量、 收到此要求，並開始處理 hello 要求
6. IIS01 詢問 hello SQL Server 上 AppVM01 資訊
7. Frontend 子網路上沒有輸出規則，允許流量
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
13. 由於沒有 hello Frontend 子網路上的輸出規則，允許 hello 回應而 hello 網際網路使用者會收到要求的 hello 網頁。

#### <a name="allowed-rdp-tooiis-server"></a>(*允許*) RDP tooIIS 伺服器
1. 網際網路上的伺服器系統管理員要求在 hello 與 hello （透過入口網站或 PowerShell hello 可以找到這個公用 IP 位址） IIS01 NIC 的 NIC 相關聯的 hello 公用 IP 位址上的 RDP 工作階段 tooIIS01
2. hello 公用 IP 位址傳送流量 toohello 朝向 IIS01 VNet （hello web 伺服器）
3. Frontend 子網路開始處理輸入規則：
  1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
  2. NSG 規則 2 (RDP) 適用，允許流量，停止處理規則
4. 由於沒有輸出規則，會套用預設規則並允許傳回的流量
5. 已啟用 RDP 工作階段
6. IIS01 會提示您輸入 hello 使用者名稱和密碼

>[!NOTE]
>在此情況下，hello IIS 伺服器 tooRDP tooany 後端伺服器作為 「 跳躍方塊 」。 第一部 RDP toohello IIS 伺服器，然後從 hello IIS 伺服器的 RDP toohello 後端伺服器。
>
>

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

#### <a name="denied-rdp-toobackend"></a>(*拒絕*) RDP toobackend
1. 網際網路使用者嘗試 tooRDP tooserver AppVM01
2. 因為沒有與此伺服器的 NIC 相關聯的公用 IP 位址，此流量會永遠不會輸入 hello VNet，並不會連線到 hello 伺服器
3. 不過，如果因為某些原因已啟用公用 IP 位址，NSG 規則 2 (RDP) 會允許此流量

>[!NOTE]
>在此情況下，hello IIS 伺服器 tooRDP tooany 後端伺服器作為 「 跳躍方塊 」。 第一部 RDP toohello IIS 伺服器，然後從 hello IIS 伺服器的 RDP toohello 後端伺服器。
>
>

#### <a name="denied-web-toobackend-server"></a>(*拒絕*) Web toobackend 伺服器
1. 網際網路使用者嘗試 tooaccess AppVM01 上的檔案
2. 因為沒有與此伺服器的 NIC 相關聯的公用 IP 位址，此流量會永遠不會輸入 hello VNet，並不會連線到 hello 伺服器
3. 如果基於某些原因，已啟用的公用 IP 位址，NSG 規則 5 (網際網路 tooVNet) 會封鎖此流量

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(拒絕) DNS 伺服器上的 Web DNS 查閱
1. 網際網路使用者嘗試 toolook 上 DNS01 內部 DNS 記錄
2. 因為沒有與此伺服器的 NIC 相關聯的公用 IP 位址，此流量會永遠不會輸入 hello VNet，並不會連線到 hello 伺服器
3. 如果基於某些原因，已啟用的公用 IP 位址，NSG 規則 5 (網際網路 tooVNet) 會封鎖此流量 (注意： 因為 hello 要求來源位址不會套用規則 1 」 (DNS) 是 hello 網際網路和規則 1 僅適用於 toohello hello 來源為區域 VNet)

#### <a name="denied-sql-access-on-hello-web-server"></a>(*拒絕*) hello web 伺服器上的 SQL 存取
1. 網際網路使用者向 IIS01 要求 SQL 資料
2. 因為沒有與此伺服器的 NIC 相關聯的公用 IP 位址，此流量會永遠不會輸入 hello VNet，並不會連線到 hello 伺服器
3. 如果基於某些原因，已啟用的公用 IP 位址，hello Frontend 子網路會開始處理輸入的規則：
  1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
  2. NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則
  3. NSG 規則 3 (網際網路 tooIIS01) 會套用，流量會允許中停止的規則處理
4. 流量叫用內部 IP 位址的 hello IIS01 (10.0.1.5)
5. IIS01 未接聽通訊埠 1433，因此沒有回應 toohello 要求

## <a name="conclusion"></a>結論
這個範例是相當簡單且直接正向的方式，隔離 hello 後端的輸入流量子網路。

您可以在[這裡][HOME]找到更多範例和網路安全性界限的概觀。

## <a name="references"></a>參考
### <a name="azure-resource-manager-template"></a>Azure Resource Manager 範本
這個範例會使用預先定義的 Azure Resource Manager 範本 Microsoft 維護的 GitHub 儲存機制中，並開啟 toohello 社群。 此範本可以直接從 GitHub，部署或下載並修改 toofit 您的需求。 

hello 主要範本位於 hello 檔中名為"azuredeploy.json。 」 此範本可以透過 PowerShell 或 CLI 送 （與 hello 相關聯的 「 azuredeploy.parameters.json 」 檔案） toodeploy 此範本。 我找到 hello 最簡單的方式是 toouse hello hello README.md 頁面，在 GitHub 上的 「 部署 tooAzure 」 按鈕。

toodeploy hello 範本，從 GitHub 和 hello Azure 入口網站建置這個範例，請遵循下列步驟：

1. 從瀏覽器中，瀏覽 toohello[範本][Template]
2. 按一下 hello 」 部署 tooAzure 」 按鈕 （或 hello"視覺化 」 按鈕 toosee 此範本的圖形表示法）
3. 在 hello 參數刀鋒視窗中，輸入 hello 儲存體帳戶、 使用者名稱和密碼，然後按一下  **確定**
5. 建立此部署的資源群組 (您可以使用現有的資源群組，但建議您建立新的以獲得最佳結果)
6. 如有必要，變更 hello 訂用帳戶和位置設定您的 VNet。
7. 按一下**檢查 法律條款**，閱讀 hello 條款，然後按一下**購買**tooagree。
8. 按一下**建立**toobegin hello 部署此範本。
9. 一旦 hello 部署順利完成時，瀏覽的 toohello 內設定此部署 toosee hello 資源建立資源群組。

>[!NOTE]
>此範本可讓 RDP toohello IIS01 僅限伺服器 (尋找 hello IIS01 公用 IP 上 hello 入口網站)。 在此情況下，hello IIS 伺服器 tooRDP tooany 後端伺服器作為 「 跳躍方塊 」。 第一部 RDP toohello IIS 伺服器，然後從 hello IIS 伺服器的 RDP toohello 後端伺服器。
>
>

tooremove 此部署，刪除 hello 資源群組和所有子資源也將一併刪除。

#### <a name="sample-application-scripts"></a>範例應用程式指令碼
一旦 hello 範本順利執行，您可以設定 hello web 伺服器和應用程式伺服器與簡單的 web 應用程式 tooallow 測試此周邊網路設定。 tooinstall 這個及其他 DMZ 範例的範例應用程式，其中提供了在 hello 下列連結：[範例應用程式指令碼][SampleApp]

## <a name="next-steps"></a>後續步驟

* 部署此範例
* 建置 hello 範例應用程式
* 測試流經此 DMZ 的不同流量

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "具有 NSG 的輸入 DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md