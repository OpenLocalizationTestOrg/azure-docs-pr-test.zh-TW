---
title: "在 Azure 中的 aaaIP 地址類型 |Microsoft 文件"
description: "了解 Azure 中的公用和私人 IP 位址。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 402d3707c00f0b3bf3ef1febd5ade66223da74bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Azure 中的 IP 位址類型及配置方法
您可以指派 IP 位址 tooAzure 資源 toocommunicate 與其他 Azure 資源，您的內部部署網路，且 hello 網際網路。 您可以在 Azure 中使用兩種類型的 IP 位址：

* **公用 IP 位址**： 用於與 hello 包括公開的 Azure 服務的網際網路通訊
* **私用 IP 位址**： 所使用的通訊，在 Azure 虛擬網路 (VNet)，並在內部網路，當您使用的 VPN 閘道或 ExpressRoute 電路 tooextend 網路 tooAzure。

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。  本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](virtual-network-ip-addresses-overview-classic.md)。
> 

如果您已熟悉 hello 傳統部署模型，請檢查 hello [IP 位址之間傳統的差異和資源管理員](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments)。

## <a name="public-ip-addresses"></a>公用 IP 位址
公用 IP 位址允許與網際網路和 Azure 公開服務的 Azure 資源 toocommunicate 例如[Azure Redis 快取](https://azure.microsoft.com/services/cache/)， [Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)， [SQL 資料庫](../sql-database/sql-database-technical-overview.md)，和[Azure 儲存體](../storage/common/storage-introduction.md)。

在 Azure 資源管理員中， [公用 IP](resource-groups-networking.md#public-ip-address) 位址是有自己的屬性的資源。 您可以將公用 IP 位址資源，與任何 hello 下列資源：

* 虛擬機器 (VM)
* 網際網路對應負載平衡器
* VPN 閘道
* 應用程式閘道

### <a name="allocation-method"></a>配置方法
有兩種方法，將 IP 位址配置 tooa*公用*IP 資源-*動態*或*靜態*。 hello 預設配置方法是*動態*，其中一個 IP 位址是**不**hello 其建立時配置。 相反地，當您啟動 （或建立） 相關聯的 hello 資源 （例如 VM 或負載平衡器），會配置 hello 公用 IP 位址。 當您停止 （或刪除） hello 資源時，會釋放 hello IP 位址。 當您停止並啟動資源時，這會導致 hello IP 位址 toochange。

tooensure hello IP 位址 hello 相關聯的資源仍在 hello 相同，您可以設定 hello 配置方法明確太*靜態*。 在此情況下會立即指派 IP 位址。 只有當您刪除 hello 資源或太變更其配置方法時，才將其釋放*動態*。

> [!NOTE]
> 即使當您將 hello 配置方法太*靜態*，您不能指定 hello 實際 IP 位址指派 toohello*公用 IP 資源*。 相反地，它取得配置中的 hello Azure 位置中可用的 IP 位址集區中建立 hello 資源。
>

Hello 下列案例中通常會使用靜態公用 IP 位址：

* 使用者需要 tooupdate 防火牆規則 toocommunicate 與您的 Azure 資源。
* DNS 名稱解析，其中當 IP 位址發生變更時將需要更新 A 記錄。
* 您的 Azure 資源與其他使用 IP 位址型安全性模型的應用程式或服務進行通訊。
* 您使用 SSL 憑證連結的 tooan IP 位址。

> [!NOTE]
> hello IP 範圍清單的公用 IP 位址 （動態/靜態） 配置 tooAzure 資源從中發行在[Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。
>

### <a name="dns-hostname-resolution"></a>DNS 主機名稱解析
您可以指定建立對應的公用 IP 資源的 DNS 網域名稱標籤*domainnamelabel*。*位置*。 cloudapp.azure.com toohello 公用 IP 位址在 hello Azure 受管理 DNS 伺服器。 比方說，如果您建立的公用 IP 資源**contoso**為*domainnamelabel*在 hello**美國西部**Azure*位置*，hello完整網域名稱 (FQDN) **contoso.westus.cloudapp.azure.com**將解析的 hello 資源 toohello 公用 IP 位址。 您可以使用這個 FQDN toocreate 指向 toohello 公用 IP 位址，在 Azure 中的自訂網域 CNAME 記錄。

> [!IMPORTANT]
> 所建立的每個網域名稱標籤必須是 Azure 位置中唯一的。  
>

### <a name="virtual-machines"></a>虛擬機器
您可以將關聯公用 IP 位址與[Windows](../virtual-machines/windows/overview.md)或[Linux](../virtual-machines/virtual-machines-linux-about.md) VM，藉由指定 tooits**網路介面**。 在具有多個網路介面之 VM 的 hello 情況下，您可以將其指派 toohello*主要*僅限網路介面。 您可以指定動態或靜態公用 IP 位址 tooa VM。

### <a name="internet-facing-load-balancers"></a>網際網路對應負載平衡器
您可以將關聯公用 IP 位址與[Azure 負載平衡器](../load-balancer/load-balancer-overview.md)，藉由指定 toohello 負載平衡器**前端**組態。 此公用 IP 位址可做為負載平衡的虛擬 IP 位址 (VIP)。 您可以指定動態或靜態公用 IP 位址 tooa 負載平衡器前端。 您也可以指派多個公用 IP 位址 tooa 負載平衡器前端，可讓[多重 VIP](../load-balancer/load-balancer-multivip.md)案例類似 ssl 網站的多租用戶環境。

### <a name="vpn-gateways"></a>VPN 閘道
[Azure VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)是使用的 tooconnect Azure 虛擬網路 (VNet) tooother Azure Vnet 或 tooan 在內部部署網路。 您需要 tooassign 公用 IP 位址 tooits **IP 組態**tooenable 它 toocommunicate 與 hello 遠端網路。 目前，您只能指派*動態*公用 IP 位址 tooa VPN 閘道。

### <a name="application-gateways"></a>應用程式閘道
您可以將公用 IP 位址與 Azure[應用程式閘道](../application-gateway/application-gateway-introduction.md)，藉由指定 toohello 閘道**前端**組態。 此公用 IP 位址可做為負載平衡的 VIP。 目前，您只能指派*動態*公用 IP 位址 tooan 應用程式閘道前端組態。

### <a name="at-a-glance"></a>快速總覽
下方的 hello 表格會顯示 hello 特定的屬性，透過它可以是公用 IP 位址相關聯的 tooa 最上層資源和可用 hello 可能是配置方法 （動態或靜態）。

| 最上層資源 | IP 位址關聯 | 動態 | 靜態 |
| --- | --- | --- | --- |
| 虛擬機器 |Linux |是 |是 |
| 負載平衡器 |前端組態 |是 |是 |
| VPN 閘道 |閘道 IP 組態 |是 |否 |
| 前端 |前端組態 |是 |否 |

## <a name="private-ip-addresses"></a>私人 IP 位址
私用 IP 位址允許與其他資源中的 Azure 資源 toocommunicate[虛擬網路](virtual-networks-overview.md)或內部部署網路透過 VPN 閘道或 ExpressRoute 循環，而不使用網際網路連線的 IP 位址。

在 hello Azure Resource Manager 部署模型中，私人 IP 位址會是下列類型的 Azure 資源相關聯的 toohello:

* VM
* 內部負載平衡器 (ILB)
* 應用程式閘道

### <a name="allocation-method"></a>配置方法
私人 IP 位址配置從 hello 位址附加 hello 子網路 toowhich hello 資源的範圍。 hello 本身 hello 子網路的位址範圍是 hello VNet 的位址範圍的一部分。

私人 IP 位址有兩種配置方法：「動態」或「靜態」。 hello 預設配置方法是*動態*，其中 hello IP 位址自動配置從 hello 資源 （使用 DHCP） 的子網路。 當您停止並啟動 hello 資源時，可以變更此 IP 位址。

您可以設定 hello 配置方法太*靜態*tooensure hello IP 位址會維持 hello 相同。 在此情況下，您也需要 tooprovide 有效的 IP 位址是 hello 資源的子網路的一部分。

靜態私人 IP 位址通常用於：

* 做為網域控制站或 DNS 伺服器的 VM。
* 需要使用 IP 位址的防火牆規則的資源。
* 其他應用程式/資源透過 IP 位址存取的資源。

### <a name="virtual-machines"></a>虛擬機器
私人 IP 位址指派 toohello**網路介面**的[Windows](../virtual-machines/windows/overview.md)或[Linux](../virtual-machines/virtual-machines-linux-about.md) VM。 如果是多重網路介面 VM，每個介面都會取得指派的私人 IP 位址。 您可以指定 hello 配置方法為動態或靜態網路介面。

#### <a name="internal-dns-hostname-resolution-for-vms"></a>內部 DNS 主機名稱解析 (適用於 VM)
除非明確設定自訂 DNS 伺服器，否則所有 Azure VM 預設都會設定 [Azure 受管理 DNS 伺服器](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) 。 這些 DNS 伺服器提供內部名稱解析位於 hello 內相同的 Vm 的 VNet。

當您建立 VM 時，hello hostname tooits 私人 IP 位址的對應新增 toohello Azure 受管理 DNS 伺服器。 如果 VM 多重網路介面，hello 主機名稱會對應 hello 主要網路介面的 toohello 私人 IP 位址。

使用 Azure 受管理 DNS 伺服器設定的 Vm 將會無法 tooresolve hello 主機名稱的 VNet tootheir 私用 IP 位址內的所有 Vm。

### <a name="internal-load-balancers-ilb--application-gateways"></a>內部負載平衡器 (ILB) 與應用程式閘道
您可以指派私用的 IP 位址 toohello**前端**組態[Azure 內部負載平衡器](../load-balancer/load-balancer-internal-overview.md)(ILB) 或[Azure 應用程式閘道](../application-gateway/application-gateway-introduction.md)。 此私用的 IP 位址會做為內部端點，且可存取的只有 toohello 資源中的虛擬網路 (VNet) 和 hello 遠端網路連線 toohello VNet。 您可以指派是動態或靜態私人 IP 位址 toohello 前端組態。

### <a name="at-a-glance"></a>快速總覽
hello 表會顯示 hello 特定的屬性，透過它可以是私人 IP 位址，相關聯的 tooa 最上層資源和可用 hello 可能是配置方法 （動態或靜態）。

| 最上層資源 | IP 位址關聯 | 動態 | 靜態 |
| --- | --- | --- | --- |
| 虛擬機器 |Linux |是 |是 |
| 負載平衡器 |前端組態 |是 |是 |
| 前端 |前端組態 |是 |是 |

## <a name="limits"></a>限制
hello 加諸於 IP 位址的限制會以完整的 hello[限制的網路功能](../azure-subscription-service-limits.md#networking-limits)在 Azure 中。 這些限制是針對每一區域和每一訂用帳戶。 您可以[連絡支援人員](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)toohello 最大的限制，根據您的商務需求向上 tooincrease hello 預設限制。

## <a name="pricing"></a>價格
公用 IP 位址可能需要少許費用。 toolearn 進一步了解 IP 位址定價在 Azure 中，檢閱 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。

## <a name="next-steps"></a>後續步驟
* [部署與使用 hello Azure 入口網站的靜態公用 IP 的 VM](virtual-network-deploy-static-pip-arm-portal.md)
* [使用範本部署使用靜態公用 IP 的 VM](virtual-network-deploy-static-pip-arm-template.md)
* [以靜態私人 IP 位址使用 hello Azure 入口網站部署的 VM](virtual-networks-static-private-ip-arm-pportal.md)
