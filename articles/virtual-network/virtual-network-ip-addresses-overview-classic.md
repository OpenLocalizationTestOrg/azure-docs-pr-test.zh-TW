---
title: "在 Azure （傳統） aaaIP 地址類型 |Microsoft 文件"
description: "了解 Azure 中的公用和私人 IP 位址 (傳統)。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 2f8664ab-2daf-43fa-bbeb-be9773efc978
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 7e09a5ad5b5f2d55329152b5d843de3c4455d1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-classic-in-azure"></a>Azure 中的 IP 位址類型及配置方法 (傳統)
您可以指派 IP 位址 tooAzure 資源 toocommunicate 與其他 Azure 資源，您的內部部署網路，且 hello 網際網路。 您可以在 Azure 中使用兩種類型的 IP 位址：公用和私人。

公用 IP 位址可用來與 hello 網際網路，包括 Azure 公開服務的通訊。

當您使用的 VPN 閘道或 ExpressRoute 電路 tooextend 網路 tooAzure 私用 IP 位址用於 Azure 的虛擬網路 (VNet)、 雲端服務和內部部署網路內的通訊。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。  本文說明如何使用 hello 傳統部署模型。 Microsoft 建議大部分的新部署使用 Resource Manager。 深入了解 IP 位址資源管理員 中透過讀取 hello [IP 位址](virtual-network-ip-addresses-overview-arm.md)發行項。

## <a name="public-ip-addresses"></a>公用 IP 位址
公用 IP 位址允許與網際網路和 Azure 公開服務的 Azure 資源 toocommunicate 例如[Azure Redis 快取](https://azure.microsoft.com/services/cache/)， [Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)， [SQL 資料庫](../sql-database/sql-database-technical-overview.md)，和[Azure 儲存體](../storage/common/storage-introduction.md)。

公用 IP 位址都以下列資源類型的 hello:

* 雲端服務
* IaaS 虛擬機器 (VM)
* PaaS 角色執行個體
* VPN 閘道
* 應用程式閘道

### <a name="allocation-method"></a>配置方法
當公用 IP 位址需求 toobe 指派 tooan Azure 資源時，它是*動態*配置從可用的公用 IP 集區就會建立 hello 位置 hello 資源內的位址。 停止 hello 資源時，會釋放此 IP 位址。 如果雲端服務，此情況發生時停止所有 hello 角色執行個體，這可以避免使用*靜態*（保留） 的 IP 位址 (請參閱[雲端服務](#Cloud-services))。

> [!NOTE]
> hello IP 範圍清單的公用 IP 位址配置 tooAzure 資源從中發行在[Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。
> 
> 

### <a name="dns-hostname-resolution"></a>DNS 主機名稱解析
當您建立雲端服務或 IaaS VM 時，您會需要 tooprovide 雲端服務 DNS 名稱在 Azure 中的所有資源而言是唯一的。 這會建立對應中 hello Azure 受管理 DNS 伺服器*dnsname*。.cloudapp.net toohello 公用 IP 位址的 hello 資源。 比方說，當您建立雲端服務使用的雲端服務 DNS 名稱**contoso**，hello 完整網域名稱 (FQDN) **contoso.cloudapp.net**解析 tooa 公用 IP 位址 (VIP)hello 雲端服務。 您可以使用這個 FQDN toocreate 指向 toohello 公用 IP 位址，在 Azure 中的自訂網域 CNAME 記錄。

### <a name="cloud-services"></a>雲端服務
雲端服務一律會有公用 IP 位址參照的 tooas 虛擬 IP 位址 (VIP)。 您可以在雲端服務 tooassociate 不同連接埠 中的 Vm 與 hello 雲端服務內的角色執行個體上的 hello VIP toointernal 連接埠建立端點。 

雲端服務可以包含多個 IaaS Vm，或 PaaS 角色執行個體，全部都透過公開 hello 相同雲端服務 VIP。 您也可以指派[多個 Vip tooa 雲端服務](../load-balancer/load-balancer-multivip.md)，可讓多個 VIP 的案例，例如多租用戶環境與 ssl 的網站。

您可以確保雲端服務的 hello 公用 IP 位址會維持相同，即使所有 hello 角色執行個體都已停止使用 hello*靜態*公用 IP 位址、 參照的 tooas[保留 IP](virtual-networks-reserved-public-ip.md)。 您可以在特定位置中建立靜態 （保留） IP 資源，並將它指派 tooany 雲端服務在該位置。 您不能指定 hello 保留 IP hello 實際 IP 位址，它會從它建立 hello 位置中可用的 IP 位址集區配置。 直到您明確刪除，此 IP 位址才會釋出。

靜態 （保留） 的公用 IP 位址中通常會使用 hello 案例其中一項雲端服務：

* 由使用者需要防火牆規則 toobe 安裝。
* 取決於外部 DNS 名稱解析，而動態 IP 會需要更新 A 記錄。
* 會取用使用以 IP 為基礎之安全性模型的外部 Web 服務。
* 使用 SSL 憑證連結的 tooan IP 位址。

> [!NOTE]
> 當您建立傳統 VM，容器 *雲端服務* 是由 Azure 建立，具有一個虛擬 IP 位址 (VIP)。 當 hello 建立透過入口網站中，預設值 RDP 或 SSH*端點*hello 入口網站讓您能透過 hello 雲端服務 VIP 連接 toohello VM 設定。 可以保留此雲端服務 VIP，有效地提供保留的 IP 位址 tooconnect toohello VM。 您可以設定多個端點，以開啟其他連接埠。
> 
> 

### <a name="iaas-vms-and-paas-role-instances"></a>IaaS VM 和 PaaS 角色執行個體
您可以指定公用 IP 位址直接 tooan IaaS [VM](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)或雲端服務內的 PaaS 角色執行個體。 這是參考的 tooas 執行個體層級公用 IP 位址 ([ILPIP](virtual-networks-instance-level-public-ip.md))。 此公用 IP 位址只能是靜態。

> [!NOTE]
> 這點不同於 hello VIP hello 雲端服務是 IaaS Vm 或 PaaS 角色執行個體的容器，因為雲端服務可以包含多個 IaaS Vm 或 PaaS 角色執行個體，全部都透過 hello 公開相同的雲端服務 VIP。
> 
> 

### <a name="vpn-gateways"></a>VPN 閘道
A [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)可以是使用的 tooconnect Azure VNet tooother Azure Vnet 或內部網路。 VPN 閘道的公用 IP 位址指派*動態*，可讓與 hello 遠端網路的通訊。

### <a name="application-gateways"></a>應用程式閘道
Azure[應用程式閘道](../application-gateway/application-gateway-introduction.md)可以用於的 Layer7 HTTP 為基礎的負載平衡 tooroute 網路流量。 應用程式閘道的公用 IP 位址指派*動態*，做為 hello 負載平衡的 VIP。

### <a name="at-a-glance"></a>速覽
hello 下表顯示多個公用 IP 位址的能力 tooassign hello 可能是配置方法 （動態/靜態），與每個資源類型。

| 資源 | 動態 | 靜態 | 多個 IP 位址 |
| --- | --- | --- | --- |
| 雲端服務 |是 |是 |是 |
| IaaS VM 或 PaaS 角色執行個體 |是 |否 |否 |
| VPN 閘道 |是 |否 |否 |
| 應用程式閘道 |是 |否 |否 |

## <a name="private-ip-addresses"></a>私人 IP 位址
私用 IP 位址允許與其他資源的 Azure 資源 toocommunicate 中雲端服務或[虛擬網路](virtual-networks-overview.md)(VNet)，或 tooon 內部部署網路 （透過 VPN 閘道或 ExpressRoute 循環），而不使用連線到網際網路的 IP 位址。

在 Azure 傳統部署模型中，私人 IP 位址可以指派 toohello 下列 Azure 資源：

* IaaS VM 和 PaaS 角色執行個體
* 內部負載平衡器
* 應用程式閘道

### <a name="iaas-vms-and-paas-role-instances"></a>IaaS VM 和 PaaS 角色執行個體
使用 hello 傳統部署模型建立的虛擬機器 (Vm) 會一律放在雲端服務中，類似 tooPaaS 角色執行個體。 hello 行為的私人 IP 位址因此如下的這些資源。

它是重要的 toonote 可能是雲端服務部署在兩種方式：

* 成為獨立  雲端服務，其不在虛擬網路中。
* 成為虛擬網路的一部分。

#### <a name="allocation-method"></a>配置方法
如果是*獨立*雲端服務、 私人 IP 位址配置的資源取得*動態*hello Azure 資料中心內的私用 IP 位址範圍。 它可以用僅用於通訊與 hello 內其他 Vm 相同雲端服務。 Hello 資源就會停止並啟動時，才能變更此 IP 位址。

萬一私用的資源取得虛擬網路內部署的雲端服務，從 hello hello 位址範圍配置的 IP 位址相關聯的子網路 （如其網路設定中指定）。 此私用 IP 位址可以用於 hello VNet 中的所有 Vm 之間的通訊。

此外，如果是 VNet 中的雲端服務，預設會動態  配置私人 IP 位址 (使用 DHCP)。 Hello 資源就會停止並啟動時，才能變更其項目。 tooensure hello IP 位址會維持 hello 相同，您就需要 tooset hello 配置方法太*靜態*，並提供有效的 IP 位址 hello 對應的位址範圍內。

靜態私人 IP 位址通常用於：

* 做為網域控制站或 DNS 伺服器的 VM。
* 需要使用 IP 位址的防火牆規則的 VM。
* 正在執行其他應用程式透過 IP 位址存取之服務的 VM。

#### <a name="internal-dns-hostname-resolution"></a>內部 DNS 主機名稱解析
除非明確設定自訂 DNS 伺服器，否則所有 Azure VM 和 PaaS 角色執行個體預設都會設定 [Azure 受管理 DNS 伺服器](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) 。 這些 DNS 伺服器提供內部名稱解析的 Vm 和角色執行個體中的 hello 相同的 VNet 或雲端服務。

當您建立 VM 時，hello hostname tooits 私人 IP 位址的對應新增 toohello Azure 受管理 DNS 伺服器。 發生多個 NIC VM hello 主機名稱會對應 toohello 私人 IP 位址的 hello 主要的 nic。 不過，此對應資訊是限制的 tooresources 內 hello 相同雲端服務或 VNet。

中的情況下*獨立*雲端服務，您將會無法 tooresolve hostname hello 內的所有 Vm/角色執行個體的相同雲端服務只。 如果 VNet 中的雲端服務，您會在無法 tooresolve hello VNet 內的所有 hello Vm/角色執行個體的主機名稱。

### <a name="internal-load-balancers-ilb--application-gateways"></a>內部負載平衡器 (ILB) 與應用程式閘道
您可以指派私用的 IP 位址 toohello**前端**組態[Azure 內部負載平衡器](../load-balancer/load-balancer-internal-overview.md)(ILB) 或[Azure 應用程式閘道](../application-gateway/application-gateway-introduction.md)。 此私用的 IP 位址會做為內部端點，且可存取的只有 toohello 資源中的虛擬網路 (VNet) 和 hello 遠端網路連線 toohello VNet。 您可以指派是動態或靜態私人 IP 位址 toohello 前端組態。 您也可以指派多個私人 IP 位址 tooenable 多重 vip 案例。

### <a name="at-a-glance"></a>速覽
下方的 hello 表格顯示多個私人 IP 位址的能力 tooassign hello 可能是配置方法 （動態/靜態），與每個資源類型。

| 資源 | 動態 | 靜態 | 多個 IP 位址 |
| --- | --- | --- | --- |
| VM (位於獨立  雲端服務中) |是 |是 |是 |
| PaaS 角色執行個體 (位於獨立  雲端服務中) |是 |否 |是 |
| VM 或 PaaS 角色執行個體 (位於 VNet 中) |是 |是 |是 |
| 內部負載平衡器前端 |是 |是 |是 |
| 應用程式閘道前端 |是 |是 |是 |

## <a name="limits"></a>限制
hello 表會顯示 hello 限制加諸於 IP 定址在 Azure 中每個訂閱。 您可以[連絡支援人員](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)toohello 最大的限制，根據您的商務需求向上 tooincrease hello 預設限制。

|  | 預設限制 | 上限 |
| --- | --- | --- |
| 公用 IP 位址 (動態) |5 |連絡支援人員 |
| 保留的公用 IP 位址 |20 |連絡支援人員 |
| 每個部署 (雲端服務) 的公用 VIP |5 |連絡支援人員 |
| 每個部署 (雲端服務) 的私人 VIP (ILB) |1 |1 |

請確定您先閱讀 hello 一組完整[限制的網路功能](../azure-subscription-service-limits.md#networking-limits)在 Azure 中。

## <a name="pricing"></a>價格
在大多數情況下，公用 IP 位址是免費的。 沒有名義電量 toouse 其他及/或靜態公用 IP 位址。 請確定您了解 hello[公用 Ip 的定價結構](https://azure.microsoft.com/pricing/details/ip-addresses/)。

## <a name="differences-between-resource-manager-and-classic-deployments"></a>Resource Manager 與傳統部署之間的差異
以下是資源管理員和 hello 傳統部署模型中的 IP 定址功能的比較。

|  | 資源 | 傳統 | Resource Manager |
| --- | --- | --- | --- |
| **公用 IP 位址** |***VM*** |參照的 tooas ILPIP （僅動態） |參考 tooas 公用 IP （動態或靜態） |
|  ||指派的 tooan IaaS VM 或 PaaS 角色執行個體 |相關聯的 toohello VM NIC | |
|  |***網際網路對向負載平衡器*** |參考 tooas VIP （動態） 或保留的 IP （靜態） |參考 tooas 公用 IP （動態或靜態） | |
|  ||指派的 tooa 雲端服務 |相關聯的 toohello 負載平衡器的前端組態 | |
|  | | | |
| **私人 IP 位址** |***VM*** |參考的 DIP tooas |參考 tooas 私人 IP 位址 |
|  ||指派的 tooan IaaS VM 或 PaaS 角色執行個體 |指派的 toohello VM NIC | |
|  |***內部負載平衡器 (ILB)*** |指派的 toohello ILB （動態或靜態） |指派的 toohello ILB 前端組態 （動態或靜態） | |

## <a name="next-steps"></a>後續步驟
* [以靜態私人 IP 位址的 VM 部署](virtual-networks-static-private-ip-classic-pportal.md)使用 hello Azure 入口網站。

