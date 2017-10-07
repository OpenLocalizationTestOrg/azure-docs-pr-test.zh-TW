---
title: "aaaVirtual 網路和 Windows Azure 中的虛擬機器 |Microsoft 文件"
description: "深入了解網路與 Azure 中建立 Windows 虛擬機器的 toohello 基本概念。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5493e9f7-7d45-4e98-be9a-657a53708746
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: e28a4782f9f6c69f6101e45dbb560ccd694a1e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-networks-and-windows-virtual-machines-in-azure"></a>Azure 中的虛擬網路和 Windows 虛擬機器 

當您建立 Azure 虛擬機器 (VM) 時，您必須建立[虛擬網路](../../virtual-network/virtual-networks-overview.md) (VNet)，或使用現有的 VNet。 您也需要的 toodecide Vm 的預定的 toobe hello VNet 上存取的方式。 請務必太[計劃之前建立的資源](../../virtual-network/virtual-network-vnet-plan-design-arm.md)，並確定您了解 hello[限制的網路資源](../../azure-subscription-service-limits.md#networking-limits)。

在下列圖 hello，Vm 會表示為網頁伺服器和資料庫伺服器。 每一組 Vm 會指派 tooseparate hello VNet 中的子網路。

![Azure 虛擬網路](./media/network-overview/vnetoverview.png)

您可以建立 VNet 之前建立的 VM，或建立 VM 時，您可以建立 hello VNet。 您必須自行建立 VNet，否則系統會在您建立 VM 時為您建立 VNet。

您建立這些資源 toosupport 通訊 vm:

- 網路介面
- IP 位址
- 虛擬網路和子網路

此外 toothose 基本的資源，您也應該考慮這些選擇性的資源：

- 網路安全性群組
- 負載平衡器 

## <a name="network-interfaces"></a>網路介面

A[網路介面 (NIC)](../../virtual-network/virtual-network-network-interface.md)是 hello 互相連線的 VM 虛擬網路 (VNet) 之間。 VM 必須有至少一個 NIC，但可以有一個以上，視您所建立的 VM hello hello 大小而定。 若要了解每個 VM 大小支援幾個 NIC，請參閱 [Azure 中的虛擬機器大小](sizes.md)。 

如果您想 toocreate 具有多個 NIC 的 VM，您必須使用至少兩部建立 hello VM。  建立之後，您可以新增其他 Nic toohello hello 的 VM 大小所支援的數字，但是您無法新增其他 Nic tooa 只有其中一個所建立的 VM，不論多少 Nic 支援 hello VM 大小。 

如果 hello VM 加入 tooan 可用性設定組，hello 可用性設定組內的所有 Vm 必須都有一或多個 Nic。 Vm 具有多個 NIC 不需要 toohave hello 相同數目的 Nic，但必須都是至少兩個。

因為 hello VM，VM 必須存在於每個連結 NIC tooa hello 相同的位置和訂用帳戶。 每個 NIC 的連線的 tooa 存在於 hello 相同的 VNet 必須 Azure 位置和訂用帳戶為 hello nic。 NIC 建立之後，您可以變更它所連接的 hello 子網路，但您無法變更 hello VNet 連接到。  每個 NIC 附加的 tooa hello VM 刪除之前不會變更 MAC 位址指派給 VM。

下表列出您可以使用 toocreate 網路介面的 hello 方法。

| 方法 | 說明 |
| ------ | ----------- |
| Azure 入口網站 | 當您建立 VM hello Azure 入口網站中時，網路介面會自動建立了 （您無法使用您建立個別的 NIC）。 hello 入口網站建立 VM 只能有一個 nic。 如果您想 toocreate 具有多個 NIC 的 VM，您必須使用不同的方法來建立它。 |
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) | 使用[新增 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)以 hello **-PublicIpAddressId**參數 tooprovide hello 識別碼 hello 公用 IP 位址，您先前建立。 |
| [Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md) | tooprovide hello 識別碼的 hello 公用 IP 位址，您先前建立的是，使用[az 網路 nic 建立](https://docs.microsoft.com/cli/azure/network/nic#create)以 hello **-公用 ip 位址**參數。 |
| [範本](../../virtual-network/virtual-network-deploy-multinic-arm-template.md) | 使用[虛擬網路中具有公用 IP 位址的網路介面](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet)做為使用範本部署網路介面的指南。 |

## <a name="ip-addresses"></a>IP 位址 

您可以指派這種[IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)tooa 在 Azure 中的 NIC:

- **公用 IP 位址**-使用 toocommunicate 輸入和輸出 （不含網路位址轉譯 (NAT)） 以 hello 網際網路和其他 Azure 資源未連線 tooa VNet。 指派的公用 IP 位址 tooa NIC 是選擇性的。 公用 IP 位址有象徵性費用，而每個訂用帳戶都有可用的數目上限。
- **私用 IP 位址**-用於在 VNet、 內部網路和 hello （與 NAT) 的網際網路通訊。 您必須指定至少一個私人 IP 位址 tooa VM。 深入了解在 Azure 中，NAT toolearn 讀取[了解 Azure 中的輸出連線](../../load-balancer/load-balancer-outbound-connections.md)。

您可以指派公用 IP 位址 tooVMs 或面對網際網路的負載平衡器。 您可以指派私人 IP 位址 tooVMs 和內部負載平衡器。 您指派 IP 位址 tooa VM 使用的網路介面。

有兩種方法中的 IP 位址配置的資源 tooa 動態或靜態。 hello 預設配置方法為動態磁碟，在建立時未配置的 IP 位址。 相反地，當您建立的 VM，或啟動已停止的 VM 可以配置 hello 的 IP 位址。 當您停止或刪除 hello VM 時，會釋放 hello IP 位址。 

tooensure hello IP 位址，VM 會保持 hello 相同，您可以明確地設定 hello 配置方法 toostatic。 在此情況下會立即指派 IP 位址。 只有當您刪除 hello VM 或變更其配置方法 toodynamic 釋放它。
    
下表列出您可以使用 IP 位址 toocreate hello 方法。

| 方法 | 說明 |
| ------ | ----------- |
| [Azure 入口網站](../../virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | 根據預設，公用 IP 位址是動態而且 hello 相關聯的位址 toothem hello VM 已停止或刪除時，可能會變更。 一律 hello VM 的 tooguarantee 使用 hello 相同的公開 IP 位址，建立靜態公用 IP 位址。 根據預設，hello 入口網站建立 VM 時指派動態私用 IP 位址 tooa NIC。 您可以變更此 toostatic hello 建立 VM 之後。|
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | 您使用[新增 AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)以 hello **-AllocationMethod**參數做為動態或靜態。 |
| [Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | 您使用[az 網路公用 ip 建立](https://docs.microsoft.com/cli/azure/network/public-ip#create)以 hello **-配置方法**參數做為動態或靜態。 |
| [範本](../../virtual-network/virtual-network-deploy-static-pip-arm-template.md) | 使用[虛擬網路中具有公用 IP 位址的網路介面](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet)做為使用範本部署公用 IP 位址的指南。 |

建立公用 IP 位址之後，您可以將它與 VM 藉由指定 tooa nic。

## <a name="virtual-network-and-subnets"></a>虛擬網路和子網路

子網路是 hello VNet 中某個範圍的 IP 位址。 您可以針對組織和安全性，將 VNet 分割成多個子網路。 在 VM 中的每個 NIC 是一個 VNet 中的連接的 tooone 子網路。 Nic 已連線的 toosubnets （相同或不同） VNet 中可與對方進行通訊，而不需要任何額外的設定。

當您設定 VNet 時，您會指定 hello 拓撲，包括 hello 可用的位址空間和子網路。 如果 hello VNet 連接 toobe tooother Vnet 或內部部署網路，您必須選取不會重疊的位址範圍。 hello IP 位址是私用，並不能從 hello 網際網路，這是僅適用於例如 10.0.0.0/8、 172.16.0.0/12 或 192.168.0.0/16 hello 非 routeable IP 位址存取。 現在，Azure 會將任何位址範圍才會連線到 hello VNet、 互連的 Vnet 內和從內部部署位置中的 hello 私人 VNet IP 位址空間的一部分。 

如果您在組織中其他人負責 hello 內部網路中工作時，您應該先 toothat 人員與前，先選取您的位址空間。 請確定沒有重疊，讓他們知道您想要 toouse hello 空間 toouse 讓它們不試 hello 相同的 IP 位址範圍。 

根據預設，沒有安全性界限之間沒有子網路，因此在這些子網路的每個 Vm 可以彼此通訊 tooone 另一個。 不過，您可以設定網路安全性群組 (Nsg)，可讓您 toocontrol hello 流量流程 tooand 從子網路和 Vm 所傳來的 tooand。 

下表列出您可以使用 toocreate VNet 和子網路的 hello 方法。   

| 方法 | 說明 |
| ------ | ----------- |
| [Azure 入口網站](../../virtual-network/virtual-networks-create-vnet-arm-pportal.md) | 如果您要讓 Azure 為您建立 VNet，當您建立 VM 時，會包含 hello VNet 的 hello 資源群組名稱的組合 hello 名稱和**vnet**。 hello 位址空間是 10.0.0.0/24，hello 必要的子網路名稱是**預設**，而且 10.0.0.0/24 hello 子網路位址範圍。 |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-vnet-arm-ps.md) | 您使用[新增 AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig)和[新增 AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) toocreate 的子網路以及 VNet。 您也可以使用[新增 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) tooadd 子網路 tooan 現有 VNet。 |
| [Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md) | hello 子網路和 hello VNet 會建立在 hello 相同的時間。 提供**-子網路-名稱**參數太[az 網路 vnet 建立](https://docs.microsoft.com/cli/azure/network/vnet#create)hello 子網路名稱。 |
| [範本](../../virtual-network/virtual-networks-create-vnet-arm-template-click.md) | hello 最簡單方式 toocreate VNet 和子網路是 toodownload 現有的範本，例如[兩個子網路與虛擬網路](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)，並修改您的需求。 |

## <a name="network-security-groups"></a>網路安全性群組

A[網路安全性群組 (NSG)](../../virtual-network/virtual-networks-nsg.md)包含清單的存取控制清單 (ACL) 規則，允許或拒絕網路流量 toosubnets、 Nic，或兩者。 Nsg 可以與子網路或個別的 Nic 已連線的 tooa 子網路產生關聯。 NSG 與子網路產生關聯時，hello ACL 規則適用於 tooall hello Vm 子網路中。 此外，流量的 tooan 個別的 NIC 可以將 NSG 關聯，以限制直接 tooa nic。

NSG 包含兩組規則：輸入和輸出。 hello 優先順序規則必須是每一組唯一的。 每個規則都有通訊協定、來源和目的地連接埠範圍、位址前置詞、流量方向、優先順序和存取類型的屬性。 

所有 NSG 都包含一組預設規則。 無法刪除 hello 預設規則，但它們指派 hello 最低優先權，因為它們會覆寫由您所建立的 hello 規則。 

當您建立關聯 NSG tooa NIC 時，hello NSG 中的 hello 網路存取規則會套用只有 toothat nic。 如果 NSG 會套用的 tooa 單一 NIC 上的多個 NIC VM，不會影響流量 toohello 其他 Nic。 您可以將不同 Nsg tooa NIC （或 VM，視 hello 部署模型而定） 與 hello NIC 或 VM 繫結至子網路。 優先順序是根據 hello 方向的流量提供。

請務必太[計劃](../../virtual-network/virtual-networks-nsg.md#planning)Nsg 當您計劃的 Vm 和 VNet。

下表列出您可以使用網路安全性群組 toocreate hello 方法。

| 方法 | 說明 |
| ------ | ----------- |
| [Azure 入口網站](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md) | 當您在 hello Azure 入口網站中建立 VM 時，NSG 會自動建立並關聯的 toohello NIC hello 入口網站建立。 hello NSG hello 名稱是 hello hello VM 名稱的組合和**-nsg**。 此 NSG 包含一個輸入的規則優先順序 1000年、 服務組 tooRDP、 hello 通訊協定集 tooTCP、 連接埠設定 too3389，以及設定 tooAllow 動作。 如果您想 tooallow 任何其他輸入的流量 toohello VM，您必須加入額外的規則 toohello NSG。 |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-nsg-arm-ps.md) | 使用[新增 AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig)並提供所需的 hello 規則資訊。 使用[新增 AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) toocreate hello NSG。 使用[組 AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) tooconfigure hello NSG hello 子網路。 使用[組 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) tooadd hello NSG toohello VNet。 |
| [Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md) | 使用[az 網路 nsg 建立](https://docs.microsoft.com/cli/azure/network/nsg#create)tooinitially 建立 hello NSG。 使用[az 網路 nsg 規則建立](https://docs.microsoft.com/cli/azure/network/nsg/rule#create)tooadd 規則 toohello NSG。 使用[az 網路 vnet 子網路更新](https://docs.microsoft.com/en-us/cli/azure/network/vnet/subnet#update)tooadd hello NSG toohello 子網路。 |
| [範本](../../virtual-network/virtual-networks-create-nsg-arm-template.md) | 使用[建立網路安全性群組](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create)做為使用範本部署網路安全性群組的指南。 |

## <a name="load-balancers"></a>負載平衡器

[Azure 負載平衡器](../../load-balancer/load-balancer-overview.md)tooyour 應用程式提供高可用性和網路效能。 您可以設定負載平衡器太[平衡連入網際網路流量](../../load-balancer/load-balancer-internet-overview.md)tooVMs 或[平衡在 VNet 中的 Vm 之間的流量](../../load-balancer/load-balancer-internal-overview.md)。 負載平衡器也可以平衡內部部署電腦與 Vm 之間的流量在跨內部部署網路或將外部流量 tooa 特定 VM。

hello 負載平衡器對應傳入和傳出流量之間 hello 公用 IP 位址和連接埠上 hello 負載平衡器與 hello 私人 IP 位址和連接埠 hello VM。

當您建立負載平衡器時，您也必須考慮下列組態元素︰

- **前端 IP 組態** – 負載平衡器可以包含一或多個前端 IP 位址 (亦稱為虛擬 IP (VIP))。 這些 IP 位址做為輸入 hello 流量。
- **後端位址集區**– 發佈 hello NIC toowhich 負載相關聯的 IP 位址。
- **NAT 規則**-定義如何輸入的流量流經 hello 前端 IP 和分散式的 toohello 後端 IP。
- **負載平衡器規則**-對應指定的前端 IP 和連接埠組合 tooa 組後端 IP 位址和連接埠組合。 單一負載平衡器可以有多個負載平衡規則。 每個規則都是與 VM 相關聯的前端 IP 和連接埠以及後端 IP 和連接埠的組合。
- **[探查](../../load-balancer/load-balancer-custom-probe-overview.md)** -監視 hello Vm 的健全狀況。 Hello 負載平衡器探查失敗 toorespond，當停止傳送新的連線 toohello 狀況不良的 VM。 hello 現有的連接不受影響，還新的連線傳送 toohealthy Vm。

下表列出您可以使用 toocreate 網際網路對向負載平衡器的 hello 方法。

| 方法 | 說明 |
| ------ | ----------- |
| Azure 入口網站 | 您目前無法建立使用 hello Azure 入口網站使用網際網路對向負載平衡器。 |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-internet-arm-ps.md) | tooprovide hello 識別碼的 hello 公用 IP 位址，您先前建立的是，使用[新增 AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig)以 hello **-PublicIpAddress**參數。 使用[新增 AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate hello hello 後端位址集區設定。 使用[新增 AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate 輸入 NAT 規則 hello 前端 IP 組態建立相關聯。 使用[新增 AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello 探查，您需要。 使用[新增 AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) toocreate hello 負載平衡器組態。 使用[新增 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate hello 負載平衡器。|
| [Azure CLI](../../load-balancer/load-balancer-get-started-internet-arm-cli.md) | 使用[az 網路 lb 建立](https://docs.microsoft.com/cli/azure/network/lb#create)toocreate hello 初始負載平衡器組態。 使用[az 網路 lb 前端 ip 建立](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create)tooadd hello 公用 IP 位址先前建立的。 使用[az 網路 lb 位址集區建立](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create)tooadd hello hello 後端位址集區設定。 使用[az 網路 lb 輸入-nat-規則建立](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create)tooadd NAT 規則。 使用[az 網路 lb 規則建立](https://docs.microsoft.com/cli/azure/network/lb/rule#create)tooadd hello 負載平衡器規則。 使用[az 網路 lb 探查建立](https://docs.microsoft.com/cli/azure/network/lb/probe#create)tooadd hello 探查。 |
| [範本](../../load-balancer/load-balancer-get-started-internet-arm-template.md) | 使用[2 個 Vm 在負載平衡器上 hello LB 設定 NAT 規則](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules)做為部署負載平衡器，使用範本的指南。 |
    
下表列出您可以使用內部負載平衡器 toocreate hello 方法。

| 方法 | 說明 |
| ------ | ----------- |
| Azure 入口網站 | 您目前無法建立內部負載平衡器使用 hello Azure 入口網站。 |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-ilb-arm-ps.md) | tooprovide hello 網路子網路，使用中的私人 IP 位址[新增 AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig)以 hello **-PrivateIpAddress**參數。 使用[新增 AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate hello hello 後端位址集區設定。 使用[新增 AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate 輸入 NAT 規則 hello 前端 IP 組態建立相關聯。 使用[新增 AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello 探查，您需要。 使用[新增 AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) toocreate hello 負載平衡器組態。 使用[新增 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate hello 負載平衡器。|
| [Azure CLI](../../load-balancer/load-balancer-get-started-ilb-arm-cli.md) | 使用 hello [az 網路 lb 建立](https://docs.microsoft.com/cli/azure/network/lb#create)命令 toocreate hello 初始負載平衡器組態。 toodefine hello 私人 IP 位址，使用[az 網路 lb 前端 ip 建立](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create)以 hello **-私用 ip 位址**參數。 使用[az 網路 lb 位址集區建立](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create)tooadd hello hello 後端位址集區設定。 使用[az 網路 lb 輸入-nat-規則建立](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create)tooadd NAT 規則。 使用[az 網路 lb 規則建立](https://docs.microsoft.com/cli/azure/network/lb/rule#create)tooadd hello 負載平衡器規則。 使用[az 網路 lb 探查建立](https://docs.microsoft.com/cli/azure/network/lb/probe#create)tooadd hello 探查。|
| [範本](../../load-balancer/load-balancer-get-started-ilb-arm-template.md) | 使用[2 個 Vm 在負載平衡器上 hello LB 設定 NAT 規則](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer)做為部署負載平衡器，使用範本的指南。 |

## <a name="vms"></a>VM

Vm 中可建立 hello 相同 VNet，而且它們可以連接 tooeach 其他使用私人 IP 位址。 它們可以連接，即使它們位於不同子網路不 hello 需要 tooconfigure 閘道或使用公用 IP 位址。 tooput 入 VNet Vm，您建立 hello VNet，然後當您建立每個 VM，您將其指派 toohello VNet 和子網路。 VM 會在部署或啟動期間取得其網路設定。  

VM 會在部署時被指派 IP 位址。 如果您將多部 VM 部署至 VNet 或子網路，它們會在啟動時被指派 IP 位址。 動態 IP 位址 (DIP) 是 hello 與 VM 相關聯內部 IP 位址。 您可以配置靜態 DIP tooa VM。 如果您配置的靜態 DIP，您應該考慮使用特定子網路 tooavoid 意外地重複使用另一個 vm 的靜態 DIP。  

如果您建立的 VM，而稍後想 toomigrate 它入 VNet，它不是簡單的組態變更。 您必須重新部署至 hello VNet hello VM。 hello 最簡單的方式 tooredeploy 為 toodelete hello VM，但不是含任何磁碟附加 tooit，，然後重新建立 hello VM 使用 hello hello VNet 中的原始磁碟。 

下表列出您可以使用 toocreate VM 在 VNet 中的 hello 方法。

| 方法 | 說明 |
| ------ | ----------- |
| [Azure 入口網站](../virtual-machines-windows-hero-tutorial.md) | 使用 hello 預設網路設定，則先前所述 toocreate 具有單一 NIC VM toocreate 具有多個 Nic 的 VM，您必須使用不同的方法。 |
| [Azure PowerShell](../virtual-machines-windows-ps-create.md) | 包括的 hello 使用[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooadd hello NIC 您先前建立 toohello VM 組態。 |
| [範本](ps-template.md) | 使用[非常簡單的 Windows VM 部署](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)做為使用範本部署 VM 的指南。 |

## <a name="next-steps"></a>後續步驟

- 深入了解如何 tooconfigure[使用者定義的路由與 IP 轉送](../../virtual-network/virtual-networks-udr-overview.md)。 
- 深入了解如何 tooconfigure [VNet tooVNet 連線](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)。
- 了解如何太[疑難排解路由](../../virtual-network/virtual-network-routes-troubleshoot-portal.md)。
