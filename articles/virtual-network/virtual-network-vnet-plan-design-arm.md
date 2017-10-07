---
title: "aaaAzure 虛擬網路 (VNet) 計劃和設計指南 |Microsoft 文件"
description: "了解如何 tooplan 和設計 Azure 中的虛擬網路根據隔離、 連接及位置需求。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 3a4a9aea-7608-4d2e-bb3c-40de2e537200
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/08/2016
ms.author: jdial
ms.openlocfilehash: f3ffadf8cf254f64b1f86b44f90315d2bc679f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-and-design-azure-virtual-networks"></a>規劃和設計 Azure 虛擬網路
建立與 VNet tooexperiment 很簡單，但有可能是因為，您會透過時間 toosupport hello 生產環境需求，您的組織中部署多個 Vnet。 以一些規劃和設計，您將會是能 toodeploy Vnet，並且 hello 資源，您需要更有效地連接。 如果您不熟悉的 Vnet，建議您[深入了解 Vnet](virtual-networks-overview.md)和[如何 toodeploy](virtual-networks-create-vnet-arm-pportal.md)一個才能繼續。

## <a name="plan"></a>規劃
徹底了解 Azure 訂用帳戶、區域和網路資源是成功的關鍵。 您可以使用以下考量事項 hello 清單做為起點。 一旦您了解這些考量，您可以定義 hello 需求，您的網路設計。

### <a name="considerations"></a>考量
之前回應 hello 規劃以下的問題，請考慮下列 hello:

* 您在 Azure 中建立的所有項目都是由一或多個資源所組成。 虛擬機器 (VM) 是資源，hello 網路介面卡 (NIC) 的 VM 所使用的是資源、 hello NIC 使用公用 IP 位址是資源，hello VNet hello NIC 已連線的 toois 資源。
* 您可在 [Azure 區域](https://azure.microsoft.com/regions/#services) 和訂用帳戶中建立資源。 資源只能連接的 tooa 虛擬網路 hello 中已有相同的地區和訂用帳戶 hello 資源。
* 您可以使用，以連接虛擬網路 tooeach 其他：
    * **[虛擬網路對等互連](virtual-network-peering-overview.md)**: hello 虛擬網路必須存在於 hello 相同 Azure 區域。 如同 hello 資源是已連線的 toohello，所以虛擬網路中的資源之間的頻寬是 hello 相同相同虛擬網路。
    * **Azure [VPN 閘道](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)**: hello 虛擬網路可以位於 hello 相同，或不同 Azure 區域。 透過 VPN 閘道連線的虛擬網路中的資源之間的頻寬會受到 hello 頻寬的 hello VPN 閘道。
* 您可以將 Vnet tooyour 在內部部署網路連線使用其中一種 hello[連線選項](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)Azure 中可用。
* 不同的資源可以群組在一起在[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)，讓您更容易 toomanage hello 資源做為一個單位。 資源群組可以包含多個區域的資源，只要 hello 資源所屬 toohello 相同訂用帳戶。

### <a name="define-requirements"></a>定義需求
使用下方的 hello 問題做為起點，您的 Azure 網路設計。    

1. 哪些 Azure 位置將您使用 toohost Vnet 嗎？
2. 您需要這些 Azure 位置之間的 tooprovide 通訊嗎？
3. 您 Azure VNet(s) 與您在內部部署資料中心之間需要 tooprovide 通訊？
4. 您的解決方式需要多少個基礎結構即服務 (IaaS) VM、雲端服務角色和 Web 應用程式？
5. 您需要 tooisolate 流量根據 Vm （也就是前端 web 伺服器和後端資料庫伺服器） 的群組嗎？
6. 您需要使用虛擬應用裝置 toocontrol 流量的流程嗎？
7. 執行工作的使用者需要不同組的使用權限 toodifferent Azure 資源？

### <a name="understand-vnet-and-subnet-properties"></a>了解 VNet 和子網路屬性
VNet 和子網路資源有助於定義在 Azure 中執行之工作負載的安全性範圍。 VNET 可由一組位址空間集合所界定 (此集合定義為 CIDR 區塊)。

> [!NOTE]
> 網路管理員都熟悉 CIDR 標記法。 如果您不熟悉 CIDR，請 [深入了解](http://whatismyipaddress.com/cidr)。
>
>

Vnet 包含下列屬性的 hello。

| 屬性 | 說明 | 條件約束 |
| --- | --- | --- |
| **name** |VNet 名稱 |向上 too80 字元的字串。 可以包含字母、數字、底線、句號或連字號。 必須以字母或數字開頭。 必須以字母、數字或底線結尾。 可以包含大寫或小寫字母。 |
| **位置** |Azure 位置 （也參考的 tooas 地區）。 |必須 hello 的其中一個有效的 Azure 位置。 |
| **addressSpace** |位址首碼 hello VNet 以 CIDR 標記法所組成的集合。 |必須是有效的 CIDR 位址區塊陣列，包括公用 IP 位址範圍。 |
| **子網路** |組成 hello VNet 的子網路的集合 |請參閱 hello 下的子網路內容表。 |
| **dhcpOptions** |包含名為 **dnsServers**之單一必要屬性的物件。 | |
| **dnsServers** |使用的 hello VNet DNS 伺服器的陣列。 如果未指定任何伺服器，則會使用 Azure 內部名稱解析。 |必須是 too10 DNS 伺服器 IP 位址所組成的陣列。 |

子網路是 VNET 的子資源，而且有助於使用 IP 位址首碼來定義 CIDR 區塊內位址空間的區段。 Nic 可以加入 toosubnets，並已連線的 tooVMs，提供各種工作負載的連線。

子網路包含下列屬性的 hello。

| 屬性 | 說明 | 條件約束 |
| --- | --- | --- |
| **name** |子網路名稱 |向上 too80 字元的字串。 可以包含字母、數字、底線、句號或連字號。 必須以字母或數字開頭。 必須以字母、數字或底線結尾。 可以包含大寫或小寫字母。 |
| **位置** |Azure 位置 （也參考的 tooas 地區）。 |必須 hello 的其中一個有效的 Azure 位置。 |
| **addressPrefix** |Hello 子網路，以 CIDR 標記法所組成的單一位址首碼 |必須是單一屬於下列其中一個 hello VNet 位址空間 CIDR 區塊。 |
| **networkSecurityGroup** |NSG 套用 toohello 子網路 | |
| **routeTable** |路由表套用 toohello 子網路 | |
| **ipConfigurations** |Nic 已連線的 toohello 子網路所使用的 IP 組態物件的集合 | |

### <a name="name-resolution"></a>名稱解析
根據預設，使用您的 VNet [Azure 提供名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md)tooresolve 名稱置於 hello VNet，而是放 hello 公用網際網路。 不過，如果您連接您的 Vnet tooyour 在內部部署資料中心，您需要 tooprovide[您自己的 DNS 伺服器](virtual-networks-name-resolution-for-vms-and-role-instances.md)tooresolve 網路之間的名稱。  

### <a name="limits"></a>限制
檢閱在 hello hello 網路限制[Azure 限制](../azure-subscription-service-limits.md#networking-limits)您的設計不會與任何 hello 限制相衝突的發行項 tooensure。 您可以開啟支援票證來提高部分限制。

### <a name="role-based-access-control-rbac"></a>角色型存取控制 (RBAC)
您可以使用[Azure rbac 進行](../active-directory/role-based-access-built-in-roles.md)toocontrol hello 層級的存取不同的使用者可能會在 Azure 中設有 toodifferent 資源。 如此一來您可以隔離您根據其需求的小組所完成的 hello 工作。

因為虛擬網路的遠端而言，使用者在 hello**網路參與者**角色擁有完整控制權 Azure 資源管理員虛擬網路資源。 同樣地，使用者在 hello**傳統網路參與者**角色擁有完整控制權傳統虛擬網路資源。

> [!NOTE]
> 您也可以[建立您自己的角色](../active-directory/role-based-access-control-configure.md)tooseparate 您的系統管理需求。
>
>

## <a name="design"></a>設計
一旦您知道 hello 答案 toohello 問題中 hello[規劃](#Plan)區段中，檢閱 hello 以下，然後再定義您的 Vnet。

### <a name="number-of-subscriptions-and-vnets"></a>訂用帳戶和 VNet 數目
您應該考慮建立多個 Vnet hello 下列案例中：

* **Vm 需要放在不同的 Azure 位置 toobe**。 Azure 中的 Vnet 有區域性。 不能跨區使用。 因此您需要至少一個 VNet，針對每個您想 toohost Vm 中的 Azure 位置。
* **需要 toobe 彼此完全隔離的工作負載**。 您可以建立個別的 Vnet，而該甚至使用 hello 相同的 IP 位址空間，從另一個 tooisolate 不同的工作負載。

請記住，上面您所看到的 hello 限制是每個區域，每個訂閱。 這表示您可以使用多個訂用帳戶 tooincrease hello 限制的資源，您可以在 Azure 中維護。 您可以使用站對站 VPN 或 ExpressRoute 電路，tooconnect Vnet 不同訂用帳戶中。

### <a name="subscription-and-vnet-design-patterns"></a>訂用帳戶和 VNet 設計模式
hello 表顯示一些常見設計模式中使用的訂閱和 Vnet。

| 案例 | 圖表 | 優點 | 缺點 |
| --- | --- | --- | --- |
| 單一訂用帳戶，每個應用程式有兩個 Vnet |![單一訂用帳戶](./media/virtual-network-vnet-plan-design-arm/figure1.png) |只有一個訂用帳戶 toomanage。 |每個 Azure 區域的 VNet 數目上限。 您之後會需要更多訂用帳戶。 檢閱 hello [Azure 限制](../azure-subscription-service-limits.md#networking-limits)文件以取得詳細資料。 |
| 每個應用程式有一個訂用帳戶，每個應用程式有兩個 VNet |![單一訂用帳戶](./media/virtual-network-vnet-plan-design-arm/figure2.png) |每個訂用帳戶只使用兩個 VNet。 |更難 toomanage 有太多應用程式時。 |
| 每個業務單位有一個訂用帳戶，每個應用程式有兩個 VNet。 |![單一訂用帳戶](./media/virtual-network-vnet-plan-design-arm/figure3.png) |平衡訂用帳戶與 VNet 的數目。 |每個業務單位 (訂用帳戶) 的 VNet 數目上限。 檢閱 hello [Azure 限制](../azure-subscription-service-limits.md#networking-limits)文件以取得詳細資料。 |
| 每個業務單位有一個訂用帳戶，每個應用程式群組有兩個 VNet。 |![單一訂用帳戶](./media/virtual-network-vnet-plan-design-arm/figure4.png) |平衡訂用帳戶與 VNet 的數目。 |必須使用子網路和 NSG 隔離應用程式。 |

### <a name="number-of-subnets"></a>子網路數目
您應該考慮下列案例的 hello 在 VNet 中的多個子網路：

* **子網路中的所有 NIC 沒有足夠的私人 IP 位址**。 如果您的子網路位址空間未包含足夠的 IP 位址的 Nic hello 子網路中的 hello 數目，您需要 toocreate 多個子網路。 請注意，Azure 會保留 5 從無法使用每個子網路的私人 IP 位址： hello 前和最後一個 hello 位址空間 （hello 子網路位址及多點傳送） 和 3 的地址 toobe 用於內部 （DHCP 和 DNS） 位址。
* **安全性**。 您可以使用多層結構，然後套用不同的工作負載的 Vm 與其他的子網路 tooseparate 群組[網路安全性群組 (Nsg)](virtual-networks-nsg.md#subnets)用於這些子網路。
* **混合式連線**。 您也可以使用 VPN 閘道與 ExpressRoute 電路[連接](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)Vnet tooone 另一個，和 tooyour 內部部署資料中心。 VPN 閘道和 ExpressRoute 電路都需要建立自己 toobe 的子網路。
* **虛擬應用裝置**。 您可以在 Azure VNet 中使用虛擬應用裝置，例如防火牆、WAN 加速器或 VPN 閘道。 當您這樣做時，您需要太[路由傳送流量](virtual-networks-udr-overview.md)toothose 應用裝置並將它們隔離在自己的子網路。

### <a name="subnet-and-nsg-design-patterns"></a>子網路和 NSG 設計模式
hello 表顯示一些常見設計模式中的使用子網路。

| 案例 | 圖表 | 優點 | 缺點 |
| --- | --- | --- | --- |
| 單一子網路，每個應用程式層的每個應用程式有多個 NSG |![單一子網路](./media/virtual-network-vnet-plan-design-arm/figure5.png) |只有一個子網路 toomanage。 |多個 Nsg 需要 tooisolate 每個應用程式。 |
| 每個應用程式有一個子網路，每個應用程式層有多個 NSG |![每個應用程式的子網路](./media/virtual-network-vnet-plan-design-arm/figure6.png) |較少的 Nsg toomanage。 |多重子網路 toomanage。 |
| 每個應用程式層有一個子網路，每個應用程式有多個 NSG。 |![每一層級的子網路](./media/virtual-network-vnet-plan-design-arm/figure7.png) |平衡子網路與 NSG 的數目。 |每個訂用帳戶的 NSG 數目上限。 檢閱 hello [Azure 限制](../azure-subscription-service-limits.md#networking-limits)文件以取得詳細資料。 |
| 每個應用程式層的每個應用程式有一個子網路，每個子網路有多個 NSG |![每個應用程式的每個層級的子網路](./media/virtual-network-vnet-plan-design-arm/figure8.png) |NSG 數目可能比較少。 |多重子網路 toomanage。 |

## <a name="sample-design"></a>設計範例
tooillustrate hello 應用程式的此篇文章中的 hello 資訊，請考慮下列案例中的 hello。

您任職的公司在北美洲有 2 個資料中心，在歐洲也有兩個資料中心。 識別 6 不同維護此客戶對向應用程式 2 不同商務單位您想為試驗 toomigrate tooAzure。 hello hello 應用程式的基本架構如下所示：

* App1、App2、App3 和 App4 是在執行 Ubuntu 的 Linux 伺服器上裝載的 Web 應用程式。 每個應用程式連接 tooa 個別的應用程式伺服器裝載在 Linux 伺服器上的 RESTful 服務。 hello RESTful 服務連接 tooa 後端 MySQL 資料庫。
* App5 和 App6 是在執行 Windows Server 2012 R2 的 Windows 伺服器上裝載的 Web 應用程式。 每個應用程式連接 tooa 後端 SQL Server 資料庫。
* 所有應用程式目前裝載於其中一個在北美的 hello 公司的資料中心。
* hello 在內部部署資料中心使用 hello 10.0.0.0/8 位址空間。

您需要 toodesign 符合下列需求的 hello 的虛擬網路解決方案：

* 每個業務單位不應該受其他業務單位的資源耗用量所影響。
* 您應該更容易 Vnet 和子網路 toomake 管理 hello 量降到最低。
* 每個業務單位應該具有適用於所有應用程式的單一測試/開發 VNet。
* 每個應用程式會裝載於每個大陸 (北美洲與歐洲) 的 2 個不同 Azure 資料中心。
* 每個應用程式會彼此完全隔離。
* 透過 hello 網際網路客戶可以存取每個應用程式使用 HTTP。
* 使用者已連線的 toohello 在內部部署資料中心可以存取每個應用程式使用加密的通道。
* 連接 tooon 內部部署資料中心應該使用現有的 VPN 裝置。
* hello 公司的網路群組必須有一個 hello VNet 組態的完整控制權。
* 每個業務單位中的開發人員應該只能夠 toodeploy Vm tooexisting 子網路。
* 將移轉所有的應用程式，因為它們是 tooAzure (增益 shift)。
* 每個位置中的 hello 資料庫應該複寫 tooother Azure 位置一天一次。
* 每個應用程式應使用 5 個前端 Web 伺服器、2 個應用程式伺服器 (必要時) 以及 2 個資料庫伺服器。

### <a name="plan"></a>規劃
您應該開始您計畫在 hello hello 問題要回答的設計[定義需求](#Define-requirements)區段如下所示。

1. 哪些 Azure 位置將您使用 toohost Vnet 嗎？

    北美洲的 2 個位置，以及歐洲的 2 個位置。 您應該挑選 hello 您現有的內部部署資料中心的實體位置為基礎。 如此一來您的連線，從實體位置 tooAzure 會有更好的延遲。
2. 您需要這些 Azure 位置之間的 tooprovide 通訊嗎？

    是。 因為 hello 資料庫必須為複寫的 tooall 位置。
3. 您 Azure VNet(s) 與您在內部部署資料中心之間需要 tooprovide 通訊？

    是。 因為使用者連接 toohello 在內部部署資料中心必須透過加密通道能夠 tooaccess hello 應用程式。
4. 您的解決方案需要多少部 IaaS VM？

    200 部 IaaS VM。 App1、App2、App3 和 App4 各需要 5 部 Web 伺服器、2 部應用程式伺服器，以及 2 部資料庫伺服器。 總計每個應用程式有 9 部 IaaS VM，或 36 部 IaaS VM。 App5 和 App6 各需要 5 部 Web 伺服器和 2 部資料庫伺服器。 總計每個應用程式有 7 部 IaaS VM，或 14 部 IaaS VM。 因此，每個 Azure 區域中的所有應用程式需要 50 部 IaaS VM。 因為我們需要 toouse 4 區域，將會是 200 的 IaaS Vm。

    您也將您的 Azure IaaS Vm 與內部部署網路之間需要 tooprovide DNS 伺服器在每個 VNet，或您的內部部署資料中心 tooresolve 名稱。
5. 您需要 tooisolate 流量根據 Vm （也就是前端 web 伺服器和後端資料庫伺服器） 的群組嗎？

    是。 每個應用程式應該彼此完全隔離，而且每個應用程式層也應該隔離。
6. 您需要使用虛擬應用裝置 toocontrol 流量的流程嗎？

    否。 虛擬應用裝置可以是使用的 tooprovide 更多控制流量的流程，包括更多詳細的資料平面記錄。
7. 執行工作的使用者需要不同組的使用權限 toodifferent Azure 資源？

    是。 hello 網路小組需要完整控制權 hello 虛擬網路設定，而開發人員應該只能夠 toodeploy 它們 Vm toopre 現有子網路。

### <a name="design"></a>設計
您應該遵循 hello 設計指定訂用帳戶、 Vnet、 子網路和 Nsg。 我們會在此討論 NSG，但您應該先深入了解 [NSG](virtual-networks-nsg.md) ，再完成您的設計。

**訂用帳戶和 VNet 數目**

相關的 toosubscriptions 與 Vnet hello 下列需求︰

* 每個業務單位不應該受其他業務單位的資源耗用量所影響。
* 您應該 Vnet 和子網路的 hello 數量降到最低。
* 每個業務單位應該具有適用於所有應用程式的單一測試/開發 VNet。
* 每個應用程式會裝載於每個大陸 (北美洲與歐洲) 的 2 個不同 Azure 資料中心。

根據上述需求，每個業務單位都需有一個訂用帳戶。 如此一來，業務單位的資源耗用量就不會計入其他業務單位的限制。 因為您想要 Vnet toominimize hello 數目，您應該考慮使用 hello 和**一個訂用帳戶每個業務單位，每個群組的應用程式的兩個 Vnet**模式如下所示。

![單一訂用帳戶](./media/virtual-network-vnet-plan-design-arm/figure9.png)

您也會需要為每個 VNet 的 toospecify hello 位址空間。 因為您需要 hello 之間的連線內部部署資料中心 hello Azure 區域 hello 用於 Azure Vnet 的位址空間不衝突與 hello 與內部網路，並使用每個 VNet hello 位址空間應互不衝突與其他現有的 Vnet。 您可以使用這些需求 hello hello toosatisfy 表中的位址空間。  

| **訂用帳戶** | **VNet** | **Azure 區域** | **位址空間** |
| --- | --- | --- | --- |
| BU1 |ProdBU1US1 |美國西部 |172.16.0.0/16 |
| BU1 |ProdBU1US2 |美國東部 |172.17.0.0/16 |
| BU1 |ProdBU1EU1 |北歐 |172.18.0.0/16 |
| BU1 |ProdBU1EU2 |西歐 |172.19.0.0/16 |
| BU1 |TestDevBU1 |美國西部 |172.20.0.0/16 |
| BU2 |TestDevBU2 |美國西部 |172.21.0.0/16 |
| BU2 |ProdBU2US1 |美國西部 |172.22.0.0/16 |
| BU2 |ProdBU2US2 |美國東部 |172.23.0.0/16 |
| BU2 |ProdBU2EU1 |北歐 |172.24.0.0/16 |
| BU2 |ProdBU2EU2 |西歐 |172.25.0.0/16 |

**子網路數和 NSG 的數目**

相關的 toosubnets 和 Nsg hello 下列需求︰

* 您應該 Vnet 和子網路的 hello 數量降到最低。
* 每個應用程式會彼此完全隔離。
* 透過 hello 網際網路客戶可以存取每個應用程式使用 HTTP。
* 使用者已連線的 toohello 在內部部署資料中心可以存取每個應用程式使用加密的通道。
* 連接 tooon 內部部署資料中心應該使用現有的 VPN 裝置。
* 每個位置中的 hello 資料庫應該複寫 tooother Azure 位置一天一次。

根據這些需求，您就無法使用應用程式層，每一個子網路，並使用 Nsg toofilter 流量，每個應用程式。 如此一來，每個 VNet 只有 3 個子網路 (前端、應用程式層和資料層)，而每個子網路的每個應用程式有一個 NSG。 在此情況下，您應該考慮使用 hello**一個子網路，每個應用程式層，每個應用程式的 Nsg**設計模式。 hello 下圖代表 hello hello 設計模式的 hello 使用**ProdBU1US1** VNet。

![每一層級一個子網路，每一層級的每個應用程式一個 NSG](./media/virtual-network-vnet-plan-design-arm/figure11.png)

不過，您也需要 toocreate 額外的子網路的 hello hello Vnet，與您在內部部署資料中心之間的 VPN 連線能力。 而且您必須針對每個子網路的 toospecify hello 位址空間。 hello 下圖顯示的範例解決方案**ProdBU1US1** VNet。 您會為每個 VNet 複寫此案例。 每個顏色都代表不同的應用程式。

![VNet 範例](./media/virtual-network-vnet-plan-design-arm/figure10.png)

**存取控制**

hello 以下是相關的 tooaccess 控制項：

* hello 公司的網路群組必須有一個 hello VNet 組態的完整控制權。
* 每個業務單位中的開發人員應該只能夠 toodeploy Vm tooexisting 子網路。

根據這些需求，您可以加入使用者從網路內建小組 toohello hello**網路參與者**每個訂用帳戶; 中的角色和應用程式開發人員建立 hello 自訂的角色，每個訂用帳戶提供這些權限 tooadd Vm tooexisting 子網路。

## <a name="next-steps"></a>後續步驟
* [部署虛擬網路](virtual-networks-create-vnet-arm-template-click.md) 。
* 了解如何太[負載平衡](../load-balancer/load-balancer-overview.md)IaaS Vm 和[管理透過多個 Azure 區域路由](../traffic-manager/traffic-manager-overview.md)。
* 深入了解[Nsg 及如何 tooplan 和設計](virtual-networks-nsg.md)NSG 方案。
* 深入了解您的 [跨單位和 VNet 連線選項](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)。
