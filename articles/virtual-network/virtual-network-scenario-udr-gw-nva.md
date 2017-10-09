---
title: "aaaHybrid 連線與 2 層應用程式 |Microsoft 文件"
description: "深入了解如何 toodeploy 虛擬設備以及 UDR toocreate 在 Azure 中的多層式應用程式環境"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 1f509bec-bdd1-470d-8aa4-3cf2bb7f6134
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/05/2016
ms.author: jdial
ms.openlocfilehash: 53599862289dbf9c6ab3289b0cb8dda6430f20f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-appliance-scenario"></a>虛擬設備的案例
在較大的 Azure 客戶之間常見的案例是 hello 需要 tooprovide 兩層式應用程式公開 toohello 網際網路，同時允許存取 toohello 回復層從內部部署資料中心。 本文件將逐步引導您使用使用者定義的路由 (UDR)、 VPN 閘道和網路的虛擬應用裝置 toodeploy 的案例符合下列需求的 hello 兩層式環境：

* Web 應用程式必須能夠從 hello 公開的網際網路。
* Web 伺服器裝載 hello 應用程式必須能夠 tooaccess 後端應用程式伺服器。
* 來自 hello 網際網路 toohello web 應用程式的所有流量必須都通過防火牆的虛擬設備。 這個虛擬設備只用於網際網路流量。
* 將 toohello 應用程式伺服器的所有流量必須都通過防火牆的虛擬設備。 此虛擬應用裝置將用於存取 toohello 後端結束伺服器，以及存取來自 hello 與內部網路透過 VPN 閘道。
* 系統管理員必須能夠 toomanage hello 防火牆虛擬應用程式從他們的內部部署電腦、 使用協力廠商防火牆專門用於管理用途的虛擬設備。

這是標準的 DMZ 和受保護網路的 DMZ 案例。 您可利用 NSG、防火牆虛擬設備或兩者的組合，在 Azure 中建構這類案例。 hello 表會顯示 hello 優缺點 Nsg 與防火牆虛擬應用裝置之間的部分。

|  | 優點 | 缺點 |
| --- | --- | --- |
| NSG |無成本。 <br/>整合到 Azure RBAC。 <br/>可在 ARM 範本中建立規則。 |大型環境中的複雜性各有不同。 |
| 防火牆 |完全掌控資料面。 <br/>透過防火牆主控台集中管理。 |防火牆設備的成本。 <br/>不與 Azure RBAC 相整合。 |

下方的 hello 解決方案會使用防火牆虛擬應用裝置 tooimplement DMZ/保護網路案例。

## <a name="considerations"></a>考量
您可以將上述說明今天、，如下所示，使用不同的功能在 Azure 中的 hello 環境的部署。

* **虛擬網路 (VNet)**。 Azure VNet 的作用類似的方式 tooan 在內部部署網路，而且可以分割成子網路 tooprovide 流量隔離和的重要性分離一或多個。
* **虛擬設備**。 數個合作夥伴提供 hello 可用於 hello 有三個防火牆上面所述的 Azure Marketplace 中的虛擬設備。 
* **使用者定義路由 (UDR)**。 路由表可以包含 UDRs Azure 網路 toocontrol hello 封包流量的 VNet 中所使用。 這些路由表可以套用的 toosubnets。 在 Azure 中的 hello 最新功能是 hello 能力 tooapply 路由表 toohello GatewaySubnet，提供 hello 能力 tooforward 進入 hello Azure VNet 從混合式連線 tooa 虛擬應用裝置的所有流量。
* **IP 轉送**。 根據預設，hello Azure 網路引擎轉送封包 toovirtual 網路介面卡 (Nic) 只有 hello 封包目的地 IP 位址符合 hello NIC 的 IP 位址。 因此，如果 UDR 定義 tooa 指定虛擬應用裝置必須傳送封包，hello Azure 網路引擎會卸除的封包。 tooensure hello 封包傳遞 tooa （在本例中為虛擬應用裝置） 不是 hello 實際目的地為 hello 封包的 VM，您需要 IP 轉送 tooenable hello 虛擬應用裝置。
* **網路安全性群組 (NSG)**。 以下的 hello 範例不會使用 Nsg，但您可以使用此方案 toofurther 篩選 hello 流量進出這些子網路和 Nic 套用 Nsg toohello 子網路和/或 Nic。

![IPv6 網路連線](./media/virtual-network-scenario-udr-gw-nva/figure01.png)

在此範例中沒有包含 hello 下列訂用帳戶：

* 2 資源群組，不會顯示 hello 圖表中。 
  * **ONPREMRG**。 包含所有的資源需要 toosimulate 在內部部署網路。
  * **AZURERG**。 包含針對 hello Azure 虛擬網路環境所需的所有資源。 
* 名為 VNet **onpremvnet**用的 toomimic 在內部部署資料中心的區段如下所示。
  * **onpremsn1**。 包含執行 Ubuntu toomimic 在內部部署伺服器的虛擬機器 (VM) 的子網路。
  * **onpremsn2**。 包含執行 Ubuntu toomimic-內部部署電腦系統管理員使用的 VM 子網路。
* 還有一個名為防火牆虛擬設備**OPFW**上**onpremvnet**太用 toomaintain 通道**azurevnet**。
* 名為 **azurevnet** 的 VNet 分段，如下所示。
  * **azsn1**。 專用於 hello 外部防火牆的外部防火牆子網路。 所有的網際網路流量都會從這個子網路進入。 此子網路只包含連結的 NIC toohello 外部防火牆。
  * **azsn2**。 裝載執行做為從 hello 網際網路存取的 web 伺服器的 VM 子網路的前端。
  * **azsn3**。 裝載執行會 hello 前端 web 伺服器來存取後端應用程式伺服器的 VM 子網路的後端。
  * **azsn4**。 管理子網路會使用專門 tooprovide 管理存取 tooall 防火牆虛擬應用裝置。 此子網路只包含 hello 解決方案中使用的虛擬應用裝置每個防火牆的 NIC。
  * **GatewaySubnet**。 Azure 的混合式連線子網路所需的 Azure Vnet 與其他網路之間的 ExpressRoute 與 VPN 閘道 tooprovide 連線。 
* 有 3 的防火牆虛擬應用裝置，在 hello **azurevnet**網路。 
  * **AZF1**。 公開外部防火牆 toohello 公用網際網路，在 Azure 中使用公用 IP 位址資源。 您需要 tooensure 3 NIC 的虛擬設備已從 hello 服務商場或直接從您的應用裝置廠商，來佈建的範本。
  * **AZF2**。 使用 toocontrol 之間流量的內部防火牆**azsn2**和**azsn3**。 這也是 3-NIC 的虛擬設備。
  * **AZF3**。 管理防火牆存取 tooadministrators hello 從內部部署資料中心，並已連線的 tooa 管理子網路使用 toomanage 所有防火牆應用裝置。 您可以在 hello Marketplace 中找到 2 NIC 的虛擬設備範本，或要求直接從您的應用裝置廠商。

## <a name="user-defined-routing-udr"></a>使用者定義的路由 (UDR)
在 Azure 中的每個子網路可以是連結的 tooa UDR 使用資料表 toodefine 該子起始的流量路由方式。 如果已不定義任何 UDRs，Azure 會使用預設路由 tooallow 流量 tooflow 從一個子網路 tooanother。 toobetter UDRs 了解，請瀏覽[什麼是使用者定義的路由與 IP 轉送](virtual-networks-udr-overview.md#ip-forwarding)。

tooensure 通訊都會透過 hello 正確的防火牆應用裝置中，根據上述 hello 最後一個需求，您需要 toocreate hello 下列路由表包含在 UDRs **azurevnet**。

### <a name="azgwudr"></a>azgwudr
在此案例中，hello 只從內部部署 tooAzure 流動的流量會使用的 toomanage hello 防火牆連線太**AZF3**，及流量必須經過 hello 內部防火牆， **AZF2**。 因此，只有一個路由是必要的 hello **GatewaySubnet**如下所示。

| 目的地 | 下一個躍點 | 說明 |
| --- | --- | --- |
| 10.0.4.0/24 |10.0.3.11 |可讓內部部署傳輸 tooreach 管理防火牆**AZF3** |

### <a name="azsn2udr"></a>azsn2udr
| 目的地 | 下一個躍點 | 說明 |
| --- | --- | --- |
| 10.0.3.0/24 |10.0.2.11 |可讓主控透過 hello 應用程式伺服器的流量 toohello 後端子網路**AZF2** |
| 0.0.0.0/0 |10.0.2.10 |可讓所有透過路由其他流量 toobe **AZF1** |

### <a name="azsn3udr"></a>azsn3udr
| 目的地 | 下一個躍點 | 說明 |
| --- | --- | --- |
| 10.0.2.0/24 |10.0.3.10 |允許流量太**azsn2**應用程式透過伺服器 toohello 網頁伺服器從 tooflow **AZF2** |

您也需要 toocreate 路由表中的 hello 子網路**onpremvnet** toomimic hello 內部部署資料中心。

### <a name="onpremsn1udr"></a>onpremsn1udr
| 目的地 | 下一個躍點 | 說明 |
| --- | --- | --- |
| 192.168.2.0/24 |192.168.1.4 |允許流量太**onpremsn2**透過**OPFW** |

### <a name="onpremsn2udr"></a>onpremsn2udr
| 目的地 | 下一個躍點 | 說明 |
| --- | --- | --- |
| 10.0.3.0/24 |192.168.2.4 |允許流量 toohello 備份子網路透過 Azure 中**OPFW** |
| 192.168.1.0/24 |192.168.2.4 |允許流量太**onpremsn1**透過**OPFW** |

## <a name="ip-forwarding"></a>IP 轉送
UDR 和 IP 轉送 」 是您可以使用組合 tooallow 虛擬應用裝置 toobe 用 toocontrol 流量流程在 Azure VNet 中的功能。  虛擬應用裝置只是執行以某種方式，例如防火牆或 NAT 裝置的應用程式使用 toohandle 網路流量的 VM。

此 VM 必須是能夠 tooreceive 連入流量的虛擬應用裝置中並未提及 tooitself。 tooallow VM tooreceive 流量定址 tooother 目的地，您必須啟用 IP 轉送 hello VM。 這是 Azure 設定，不是在 hello 客體作業系統設定。 某些類型的應用程式 toohandle 您的虛擬設備仍需要 toorun hello 連入流量，並適當地路由傳送。

toolearn 深入了解 IP 轉送，請瀏覽[什麼是使用者定義的路由與 IP 轉送](virtual-networks-udr-overview.md#ip-forwarding)。

例如，假設您有下列安裝程式在 Azure vnet 中的 hello:

* 子網路 **onpremsn1** 包含名為 **onpremvm1** 的 VM。
* 子網路 **onpremsn2** 包含名為 **onpremvm2** 的 VM。
* 名為虛擬應用裝置**OPFW**太連接**onpremsn1**和**onpremsn2**。
* 使用者定義路由連結太**onpremsn1**指定所有流量太**onpremsn2**必須太傳送**OPFW**。

在這點時，如果**onpremvm1**的連線嘗試 tooestablish **onpremvm2**、 hello UDR 將用於和的流量將傳送太**OPFW**為 hello 下一個躍點。 請記住，hello 實際封包目的地未變更，它仍指出**onpremvm2** hello 目的地。 

不含 IP 轉送 」 啟用**OPFW**hello Azure 虛擬網路的邏輯將會卸除 hello 封包，因為它只允許封包傳送 toobe tooa VM，如果 hello VM 的 IP 位址是 hello hello 封包的目的地。

使用 IP 轉送，hello Azure 虛擬網路的邏輯會轉送 hello 封包 tooOPFW，而不需要變更其原始目的地位址。 **OPFW**必須處理 hello 封包，並判斷哪些 toodo 它們。

上述 toowork hello 案例中，您必須啟用 IP 轉送 」 hello Nic 上**OPFW**， **AZF1**， **AZF2**，和**AZF3**適用於路由 (hello 的連結的 toohello 管理子網路以外的所有 Nic)。 

## <a name="firewall-rules"></a>防火牆規則
如上面所述，IP 轉送只可確保傳送封包 toohello 虛擬應用裝置。 您的應用裝置仍然需要 toodecide 哪些 toodo 與這些封包。 在上述的 hello 情況下，您將需要 toocreate hello 依照您的應用裝置中的規則：

### <a name="opfw"></a>OPFW
OPFW 代表包含 hello 下列規則在內部部署裝置：

* **路由**: too10.0.0.0/16 的所有流量 (**azurevnet**) 必須透過通道傳送**ONPREMAZURE**。
* **原則**︰允許 **port2** 和 **ONPREMAZURE** 之間所有的雙向流量。

### <a name="azf1"></a>AZF1
AZF1 代表 Azure 的虛擬應用裝置，以包含 hello 下列規則：

* **原則**︰允許 **port1** 和 **port2** 之間所有的雙向流量。

### <a name="azf2"></a>AZF2
AZF2 代表 Azure 的虛擬應用裝置，以包含 hello 下列規則：

* **路由**: too10.0.0.0/16 的所有流量 (**onpremvnet**) 必須透過傳送 toohello Azure 閘道 IP 位址 (例如 10.0.0.1) **port1**。
* **原則**︰允許 **port1** 和 **port2** 之間所有的雙向流量。

## <a name="network-security-groups-nsgs"></a>網路安全性群組 (NSG)
這個案例中不會使用 NSG。 不過，您可以套用 Nsg tooeach 子網路 toorestrict 傳入和傳出流量。 比方說，您可以套用 hello 遵循 NSG 規則 toohello 外部 FW 子網路。

**連入**

* 允許從任何 VM 上的 hello 網際網路 tooport 80 的所有 TCP 流量 hello 子網路中。
* 從網際網路 hello 拒絕所有其他流量。

**連出**

* 拒絕所有流量 toohello 網際網路。

## <a name="high-level-steps"></a>高階步驟
toodeploy 此案例中，遵循 hello 高階步驟下方。

1. 登入 tooyour Azure 訂用帳戶。
2. 如果您想 toodeploy VNet toomimic hello 內部部署網路，佈建 hello 資源屬於**ONPREMRG**。
3. 佈建 hello 資源屬於**AZURERG**。
4. 從佈建 hello 通道**onpremvnet**太**azurevnet**。
5. 佈建的所有資源後，登入太**onpremvm2**間的 ping 10.0.3.101 tootest 連線**onpremsn2**和**azsn3**。

