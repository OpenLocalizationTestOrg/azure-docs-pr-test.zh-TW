---
title: "在 Azure 中的 aaaNetwork 安全性群組 |Microsoft 文件"
description: "了解如何 tooisolate 和控制流量虛擬網路使用網路安全性群組在 Azure 中使用分散式的 hello 防火牆內。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 20e850fc-6456-4b5f-9a3f-a8379b052bc9
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 3528ce833dab17977327c3c9ae0e78316e5e6a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="filter-network-traffic-with-network-security-groups"></a>使用網路安全性群組來篩選網路流量

網路安全性群組 (NSG) 包含可允許或拒絕網路流量 tooresources 連接 tooAzure 虛擬網路 (VNet) 安全性規則的清單。 Nsg 可以是相關聯的 toosubnets，個別 Vm （傳統），或個別的網路介面 (NIC) 附加 tooVMs （資源管理員）。 當 NSG 相關聯的 tooa 子網路，hello 規則適用於 tooall 資源連線的 toohello 子網路。 流量可以進一步限制也關聯 NSG tooa VM 或 nic。

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。 本文將說明如何使用這兩個模型，但 Microsoft 建議的最新的部署使用 hello 資源管理員的模型。

## <a name="nsg-resource"></a>NSG 資源
Nsg 包含下列屬性的 hello:

| 屬性 | 說明 | 條件約束 | 考量 |
| --- | --- | --- | --- |
| 名稱 |Hello NSG 的名稱 |必須是唯一 hello 區域內。<br/>可以包含字母、數字、底線、句號和連字號。<br/>必須以字母或數字開頭。<br/>必須以字母、數字或底線結尾。<br/>不能超過 80 個字元。 |因為您可能需要數個 Nsg toocreate，請確定您擁有可讓您 Nsg 輕鬆 tooidentify hello 函式命名慣例。 |
| 區域 |Azure[區域](https://azure.microsoft.com/regions)hello NSG 建立的位置。 |Nsg 只能是關聯的 tooresources 內 hello hello NSG 與相同的區域。 |每個區域，可以有多少 Nsg 相關 toolearn 讀取 hello [Azure 限制](../azure-subscription-service-limits.md#virtual-networking-limits-classic)發行項。|
| 資源群組 |hello[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)NSG 存在於 hello。 |雖然 NSG 存在於資源群組中，可能很關聯的 tooresources 在資源群組中，只要 hello 資源屬於 hello 與 hello NSG 的相同 Azure 區域。 |資源群組在一起，因為部署單位的多個資源都使用的 toomanage。<br/>您可以考慮分組 hello NSG 與它相關聯的資源。 |
| 規則 |定義允許或拒絕流量的輸入或輸出規則。 | |請參閱 hello [NSG 規則](#Nsg-rules)本文一節。 |

> [!NOTE]
> 以端點為基礎的 Acl 和網路安全性上不支援群組 hello 相同的 VM 執行個體。 如果您想 toouse NSG，且已備妥端點 ACL，請先移除 hello 端點 ACL。 toolearn tooremove ACL，如何讀取 hello[管理存取控制清單 (Acl) 的 PowerShell，透過端點](virtual-networks-acl-powershell.md)發行項。
> 

### <a name="nsg-rules"></a>NSG 規則
NSG 規則包含下列屬性的 hello:

| 屬性 | 說明 | 條件約束 | 考量 |
| --- | --- | --- | --- |
| **名稱** |Hello 規則的名稱。 |必須是唯一 hello 區域內。<br/>可以包含字母、數字、底線、句號和連字號。<br/>必須以字母或數字開頭。<br/>必須以字母、數字或底線結尾。<br/>不能超過 80 個字元。 |您可能有數個 NSG 中的規則，因此請確定您遵循命名慣例，可讓您 tooidentify hello 函式的規則。 |
| **通訊協定** |通訊協定 toomatch hello 規則。 |TCP、UDP 或 * |使用 * 因為通訊協定包含 ICMP （東西流量），做為以及 UDP 和 TCP，而且可能會減少您需要的規則的 hello 數目。<br/>在 hello 相同時，使用 * 可能是過於廣泛的方法，因此建議您使用 * 只在必要時。 |
| **來源連接埠範圍** |來源連接埠範圍 toomatch hello 規則。 |單一連接埠號碼從 1 too65535，連接埠範圍 (範例： 1-65535)，或 * （適用於所有連接埠）。 |來源連接埠可以是暫時的。 除非您的用戶端程式是使用特定連接埠，否則在大部分情況下請使用 *。<br/>儘可能 tooavoid hello 需要多個規則，再試一次 toouse 連接埠範圍。<br/>多個連接埠或連接埠範圍不可使用逗號分組。 |
| **目的地連接埠範圍** |目的地連接埠範圍 toomatch hello 規則。 |單一連接埠號碼從 1 too65535，連接埠範圍 (範例： 1-65535)，或\*（適用於所有連接埠）。 |儘可能 tooavoid hello 需要多個規則，再試一次 toouse 連接埠範圍。<br/>多個連接埠或連接埠範圍不可使用逗號分組。 |
| **來源位址首碼** |來源位址前置詞或標記 toomatch hello 規則。 |單一 IP 位址 (例如：10.10.10.10)、IP 子網路 (例如：192.168.1.0/24)、[預設標籤](#default-tags)或 * (用於所有位址)。 |請考慮使用範圍的預設標記和 * tooreduce hello 的規則數目。 |
| **Destination address prefix** |目的地位址前置詞或標記 toomatch hello 規則。 | 單一 IP 位址 (例如：10.10.10.10)、IP 子網路 (例如：192.168.1.0/24)、[預設標籤](#default-tags)或 * (用於所有位址)。 |請考慮使用範圍的預設標記和 * tooreduce hello 的規則數目。 |
| **Direction** |Hello 規則的流量 toomatch 的方向。 |輸入或輸出。 |輸入和輸出規則會根據方向分別處理。 |
| **優先順序** |Hello 依優先順序會檢查規則。 一旦套用規則，就不會再測試規則是否符合。 | 100 和 4096 之間的數字。 | 請考慮建立您可能會在建立 hello 未來跳躍新規則的每個規則 tooleave 空間 100 的優先權規則。 |
| **Access** |類型存取 tooapply hello 規則會比對。 | 允許或拒絕。 | 請記住，如果允許規則中找不到封包，hello 封包會卸除。 |

NSG 包含兩組規則：輸入和輸出。 hello 優先順序規則必須是每一組唯一的。 

![NSG 規則處理](./media/virtual-network-nsg-overview/figure3.png) 

hello 如上圖所示 NSG 規則的處理方式。

### <a name="default-tags"></a>預設標籤
預設標記是系統提供的識別項 tooaddress 分類的 IP 位址。 您可以使用預設標記中 hello**來源位址首碼**和**目的地位址首碼**任何規則的屬性。 有三個您可使用的預設標籤：

* **VirtualNetwork** （資源管理員） (**VIRTUAL_NETWORK**的傳統): 此標記包含 hello 虛擬網路位址空間 （在 Azure 中定義的 CIDR 範圍），針對所有連線在內部部署位址空間，以及連接Azure Vnet （區域網路）。
* **AzureLoadBalancer** (Resource Manager) (適用於傳統部署的 **AZURE_LOADBALANCER**)：這個標籤代表 Azure 基礎結構的負載平衡器。 hello 標記會轉譯的 tooan 源自 Azure 的健全狀況探查位置的 Azure 資料中心 IP。
* **網際網路**（資源管理員） (**網際網路**的傳統): 此標記代表位於 hello 虛擬網路外可經由公用網際網路的 hello IP 位址空間。 hello 範圍包括 hello [Azure 所擁有的公用 IP 空間](https://www.microsoft.com/download/details.aspx?id=41653)。

### <a name="default-rules"></a>預設規則
所有 NSG 都包含一組預設規則。 無法刪除 hello 預設規則，但它們指派 hello 最低優先權，因為它們會覆寫由您所建立的 hello 規則。 

hello 預設規則允許及不允許流量，如下所示：
- 虛擬網路中的流量起始和結束同時允許輸入和輸出方向。
- **網際網路︰**允許輸出流量，但會封鎖輸入流量。
- **負載平衡器：**允許 Azure 負載平衡器 tooprobe hello 和健康狀態的 Vm 角色執行個體。 如果您不使用負載平衡的集合，則可以覆寫此規則。

**輸入預設規則**

| 名稱 | 優先順序 | 來源 IP | 來源連接埠 | 目的地 IP | 目的地連接埠 | 通訊協定 | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVNetInBound |65000 | VirtualNetwork | * | VirtualNetwork | * | * | 允許 |
| AllowAzureLoadBalancerInBound | 65001 | AzureLoadBalancer | * | * | * | * | 允許 |
| DenyAllInBound |65500 | * | * | * | * | * | 拒絕 |

**輸出預設規則**

| 名稱 | 優先順序 | 來源 IP | 來源連接埠 | 目的地 IP | 目的地連接埠 | 通訊協定 | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVnetOutBound | 65000 | VirtualNetwork | * | VirtualNetwork | * | * | 允許 |
| AllowInternetOutBound | 65001 | * | * | Internet | * | * | 允許 |
| DenyAllOutBound | 65500 | * | * | * | * | * | 拒絕 |

## <a name="associating-nsgs"></a>建立 NSG 關聯
您可以將關聯 NSG tooVMs、 的 Nic 和子網路，視您使用，，如下所示的 hello 部署模型而定：

* **VM （僅傳統）：**套用安全性規則 tooall 流量，從中 hello VM。 
* **NIC （資源管理員）：**套用安全性規則 tooall 流量，從中 hello NIC hello NSG 與其相關聯。 在多個 NIC VM 中，您可以套用不同的 （或相同 hello） NSG tooeach NIC 個別。 
* **子網路 （「 資源管理員 」 和 「 傳統 」）：**安全性規則套用至 azure 或從任何資源 tooany 流量連接 toohello VNet。

您可以將不同 Nsg tooa VM （或 NIC，視 hello 部署模型而定） 與 hello NIC 或 VM 連線到子網路。 安全性規則套用的 toohello 流量 hello 中的每個 NSG 中的優先順序，依下列順序：

- **輸入流量**

  1. **NSG 套用 toosubnet:** hello 封包的 nsg 關聯的子網路具有比對的規則 toodeny 流量，如果卸除。

  2. **NSG 套用 tooNIC** （資源管理員） 或 VM （傳統）： 如果 VM\NIC NSG 具有相符的規則，拒絕的流量，封包，會卸除 hello VM\NIC，即使 NSG 的子網路具有相符的規則，允許流量。

- **輸出流量**

  1. **NSG 套用 tooNIC** （資源管理員） 或 VM （傳統）： 如果 VM\NIC NSG 有相符的規則，拒絕的流量，就會捨棄封包。

  2. **NSG 套用 toosubnet:**如果 NSG 的子網路具有相符的規則，拒絕的流量，封包被丟棄，即使 VM\NIC NSG 具有相符的規則，允許流量。

> [!NOTE]
> 雖然您可以只將單一 NSG tooa 子網路、 VM 或 NIC;您可以將關聯 hello 相同 NSG tooas 許多資源，您的需要。
>

## <a name="implementation"></a>實作
您可以實作 Nsg hello 資源管理員或使用下列工具 hello 傳統部署模型中：

| 部署工具 | 傳統 | Resource Manager |
| --- | --- | --- |
| Azure 入口網站   | 是 | [是](virtual-networks-create-nsg-arm-pportal.md) |
| PowerShell     | [是](virtual-networks-create-nsg-classic-ps.md) | [是](virtual-networks-create-nsg-arm-ps.md) |
| Azure CLI **V1**   | [是](virtual-networks-create-nsg-classic-cli.md) | [是](virtual-networks-create-nsg-cli-nodejs.md) |
| Azure CLI **V2**   | 否 | [是](virtual-networks-create-nsg-arm-cli.md) |
| Azure Resource Manager 範本   | 否  | [是](virtual-networks-create-nsg-arm-template.md) |

## <a name="planning"></a>規劃
在實作之前 Nsg，您需要 tooanswer hello 下列問題：

1. 您想從 toofilter 流量 tooor 什麼類型的資源？ 您可以取得各種資源，例如 NIC (Resource Manager)、VM (傳統)、雲端服務、應用程式服務環境和 VM 擴展集。 
2. 是您想要從連接中的現有 Vnet toosubnets toofilter 流量的 hello 資源嗎？

規劃 Azure 中的網路安全性的詳細資訊，請參閱 hello[雲端服務和網路安全性](../best-practices-network-security.md)發行項。 

## <a name="design-considerations"></a>設計考量
一旦您知道 hello 答案 toohello 問題中 hello[規劃](#Planning)區段中，檢閱下列各節定義 Nsg 之前的 hello:

### <a name="limits"></a>限制
您可以在訂用帳戶的 Nsg 的 toohello 數目和每個 NSG 的規則數目沒有限制。 深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。

### <a name="vnet-and-subnet-design"></a>VNet 和子網路的設計
Nsg 可以套用的 toosubnets，因為您可以透過您的資源群組的子網路，並套用 Nsg toosubnets 降低 hello Nsg 的數目。  如果您決定 tooapply Nsg toosubnets，您可能會發現，現有的 Vnet 子網路，您有不使用定義及 Nsg 記住。 您可能需要 toodefine 新的 Vnet 和子網路 toosupport NSG 設計和部署您新資源 tooyour 新的子網路。 接著，您無法定義現有的資源 toohello 新的子網路移轉策略 toomove。 

### <a name="special-rules"></a>特殊規則
如果您封鎖 hello 下列規則所允許的流量，您的基礎結構無法與 Azure 的基本服務：

* **Hello 主機節點的虛擬 IP:**基本基礎結構服務，例如 DHCP、 DNS 及狀況監控透過提供 hello 虛擬化主機 IP 位址 168.63.129.16。 這個公用 IP 位址所屬 tooMicrosoft 且 hello 唯一虛擬化的 IP 位址在所有區域用於此目的。 此 IP 位址對應 toohello 實體 IP 位址 hello server 電腦 （主機節點） 的裝載 hello VM。 hello 主機節點做為 hello DHCP 轉送、 hello DNS 遞迴解析程式，以及 hello 探查來源 hello 負載平衡器健全狀況探查與 hello 機器健全狀況探查。 通訊 toothis IP 位址不是攻擊。
* **授權 (金鑰管理服務)**：在 VM 中執行的 Windows 映像必須獲得授權。 tooensure 授權，要求會傳送 toohello 金鑰管理服務主機伺服器可處理這類查詢。 hello 要求是透過輸出連接埠 1688年。

### <a name="icmp-traffic"></a>ICMP 流量
hello 目前的 NSG 規則只允許通訊協定*TCP*或*UDP*。 *ICMP*沒有特定的標記。 不過，允許 ICMP 流量是 VNet 中的 hello AllowVNetInBound 預設規則，以允許從任何連接埠和通訊協定 hello VNet 內的流量 tooand。

### <a name="subnets"></a>子網路
* 請考慮您的工作負載需要的階層的 hello 數目。 每一層可以使用子網路，與套用的 NSG toohello 子網路隔離。 
* 如果您需要 tooimplement 子網路的 VPN 閘道或 ExpressRoute 循環時，請勿**不**套用 NSG toothat 子網路。 如果您這麼做，跨 VNet 或跨單位連線將會失敗。 
* 如果您需要 tooimplement 網路虛擬應用裝置 (NVA)，連接 hello NVA tooits 自己的子網路，然後從 hello NVA 建立使用者定義的路由 (UDR) tooand。 您可以實作的子網路層級 NSG toofilter 流量進出此子網路。 深入了解 UDRs，讀取 hello toolearn[使用者定義的路由](virtual-networks-udr-overview.md)發行項。

### <a name="load-balancers"></a>負載平衡器
* 請考慮 hello 負載平衡和網路位址轉譯 (NAT) 規則，每個工作負載所使用的每個負載平衡器。 NAT 規則都包含 Nic （資源管理員） 或 Vm/雲端服務角色執行個體 （傳統） 的繫結的 tooa 後端集區。 請考慮建立 NSG 針對每個後端集區中，允許只會透過實作 hello 負載平衡器中的 hello 規則對應的流量。 建立每個後端集區 NSG，可以保證會同時篩選直接 （而非透過 hello 負載平衡器），傳 toohello 後端集區的流量。
* 在傳統的部署中，您會建立對應的 Vm 或角色執行個體上的負載平衡器 tooports 上的連接埠的端點。 您也可以透過 Resource Manager 建立自己個別對外公開的負載平衡器。 hello hello VM 中的實際通訊埠或角色執行個體，不在負載平衡器所公開的 hello 連接埠的連入流量的 hello 目的地連接埠。 hello 來源連接埠和位址 hello 連接 toohello VM 位於連接埠和位址 hello hello 網際網路中的遠端電腦，而不 hello 連接埠和 hello 負載平衡器所公開的位址。
* 當您建立內部負載平衡器 (ILB) 通過的 Nsg toofilter 流量時，hello 來源連接埠和位址範圍套用為 hello 原始電腦，不 hello 負載平衡器。 hello 目的地連接埠和位址範圍是 hello 目的地電腦，不 hello 負載平衡器。

### <a name="other"></a>其他
* 以端點為基礎的存取控制清單 (ACL) 和 Nsg hello 上不支援相同的 VM 執行個體。 如果您想 toouse NSG，且已備妥端點 ACL，請先移除 hello 端點 ACL。 如需有關資訊 tooremove 端點 ACL，請參閱 hello[管理端點 Acl](virtual-networks-acl-powershell.md)發行項。
* 資源管理員 中，您可以使用 NSG 相關聯 tooa NIC 的 Vm 與每個 NIC 為基礎的多個 Nic tooenable 管理 （遠端存取）。 唯一 Nsg tooeach NIC 建立關聯可讓 Nic 的流量類型分隔。
* 類似 toohello 的負載平衡器、 篩選來自其他 Vnet 流量時，您必須使用 hello 來源位址範圍的 hello 遠端電腦時，不會 hello 連接 hello Vnet 的閘道。
* 許多 Azure 服務不能連接的 tooVNets。 如果一項 Azure 資源無法連線的 tooa VNet，您無法使用 NSG toofilter 流量 toohello 資源。  Hello 服務可以連線的 tooa VNet 是否使用 toodetermine 讀取 hello 文件以 hello 服務。

## <a name="sample-deployment"></a>部署範例
tooillustrate hello 應用程式的此篇文章中的 hello 資訊，請考慮 hello 下列圖片所示的兩層式應用程式的常見的案例：

![NSG](./media/virtual-network-nsg-overview/figure1.png)

Hello 圖表所示，hello *Web1*和*Web2* Vm 會連線的 toohello*前端*子網路和 hello *DB1*和*DB2* Vm 會連線的 toohello*後端*子網路。  這兩個子網路屬於 hello *TestVNet* VNet。 hello 應用程式元件每個執行的 Azure VM 連接 tooa VNet 內。 hello 案例具有下列需求的 hello:

1. 分隔的 hello WEB 和 DB 伺服器之間的流量。
2. 負載平衡規則從 hello 負載平衡器 tooall web 伺服器連接埠 80 上的轉送流量。
3. 負載平衡器 NAT 規則轉送流量進入 hello 負載平衡器上的連接埠 50001 tooport 3389，hello WEB1 VM 上。
4. 沒有存取 toohello 前端或後端 Vm 從 hello 網際網路，除了需求 2 和 3。
5. 從 hello WEB 或 DB 伺服器沒有傳出網際網路存取。
6. 從 hello FrontEnd 子網路的存取為 allowed tooport 3389 的任何 web 伺服器。
7. 從 hello FrontEnd 子網路的存取為 allowed tooport 3389 任何 DB 伺服器。
8. 從 hello FrontEnd 子網路的存取為 allowed tooport 1433 的所有資料庫伺服器。
9. 區隔 DB 伺服器中不同 NIC 上的管理流量 (連接埠 3389) 和資料庫流量 (1433)。

需求 1-6 （除了需求 3 和 4） 是所有的局部的 toosubnet 空格。 hello 下列 Nsg 符合 hello 先前的需求降至最低所需的 Nsg 的 hello 數目：

### <a name="frontend"></a>FrontEnd
**輸入規則**

| 規則 | Access | 優先順序 | 來源位址範圍 | 來源連接埠 | 目的地連接埠範圍 | 目的地連接埠 | 通訊協定 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-HTTP-Internet | 允許 | 100 | Internet | * | * | 80 | TCP |
| Allow-Inbound-RDP-Internet | 允許 | 200 | Internet | * | * | 3389 | TCP |
| Deny-Inbound-All | 拒絕 | 300 | Internet | * | * | * | TCP |

**輸出規則**

| 規則 | Access | 優先順序 | 來源位址範圍 | 來源連接埠 | 目的地連接埠範圍 | 目的地連接埠 | 通訊協定 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All |拒絕 |100 | * | * | Internet | * | * |

### <a name="backend"></a>BackEnd
**輸入規則**

| 規則 | Access | 優先順序 | 來源位址範圍 | 來源連接埠 | 目的地連接埠範圍 | 目的地連接埠 | 通訊協定 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | 拒絕 | 100 | Internet | * | * | * | * |

**輸出規則**

| 規則 | Access | 優先順序 | 來源位址範圍 | 來源連接埠 | 目的地連接埠範圍 | 目的地連接埠 | 通訊協定 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | 拒絕 | 100 | * | * | Internet | * | * |

下列 Nsg 會建立並關聯 tooNICs hello 遵循 Vm 中的 hello:

### <a name="web1"></a>WEB1
**輸入規則**

| 規則 | Access | 優先順序 | 來源位址範圍 | 來源連接埠 | 目的地連接埠範圍 | 目的地連接埠 | 通訊協定 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Internet | 允許 | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | 允許 | 200 | Internet | * | * | 80 | TCP |

> [!NOTE]
> hello hello 一個規則的來源位址範圍是**網際網路**，不 hello 虛擬 IP 位址的 hello 負載平衡器。 hello 來源連接埠是 *、 不 500001。 針對負載平衡器 NAT 規則不會 hello 與 NSG 安全性規則相同。 NSG 安全性規則都相關的 toohello 原始來源和最終目的地的流量，**不**hello hello 兩者之間的負載平衡器。 
> 
> 

### <a name="web2"></a>WEB2
**輸入規則**

| 規則 | Access | 優先順序 | 來源位址範圍 | 來源連接埠 | 目的地連接埠範圍 | 目的地連接埠 | 通訊協定 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Inbound-RDP-Internet | 拒絕 | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | 允許 | 200 | Internet | * | * | 80 | TCP |

### <a name="db-servers-management-nic"></a>DB 伺服器 (管理 NIC)
**輸入規則**

| 規則 | Access | 優先順序 | 來源位址範圍 | 來源連接埠 | 目的地連接埠範圍 | 目的地連接埠 | 通訊協定 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Front-end | 允許 | 100 | 192.168.1.0/24 | * | * | 3389 | TCP |

### <a name="db-servers-database-traffic-nic"></a>DB 伺服器 (資料庫流量 NIC)
**輸入規則**

| 規則 | Access | 優先順序 | 來源位址範圍 | 來源連接埠 | 目的地連接埠範圍 | 目的地連接埠 | 通訊協定 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-SQL-Front-end | 允許 | 100 | 192.168.1.0/24 | * | * | 1433 | TCP |

由於某些 hello Nsg 相關聯的 tooindividual Nic，hello 規則是部署透過資源管理員的資源。 視子網路與 NIC 的關聯方式而定，會結合兩者的規則。 

## <a name="next-steps"></a>後續步驟
* [部署 NSG (Resource Manager)](virtual-networks-create-nsg-arm-pportal.md)。
* [部署 NSG (傳統)](virtual-networks-create-nsg-classic-ps.md).
* [管理 NSG 記錄檔](virtual-network-nsg-manage-log.md)。
* [針對 NSG 進行疑難排解] (virtual-network-nsg-troubleshoot-portal.md)
