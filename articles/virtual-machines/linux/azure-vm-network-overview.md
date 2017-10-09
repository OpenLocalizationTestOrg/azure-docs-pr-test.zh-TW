---
title: "aaaAzure 和 Linux VM 網路概觀 |Microsoft 文件"
description: "Azure 與 Linux VM 網路概觀。"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Azure 與 Linux VM 網路概觀
## <a name="virtual-networks"></a>虛擬網路
Azure 虛擬網路 (VNet) 是網路的您自己 hello 雲端中的表示法。 它是 hello 的隔離的邏輯專用的 Azure 雲端 tooyour 訂用帳戶。 您也可以完全控制 hello IP 位址區塊、 DNS 設定、 安全性原則，以及此網路內的路由表。 您也可以進一步將 VNet 分成子網路，並啟動 Azure IaaS 虛擬機器 (VM) 和/或雲端服務 (PaaS 角色執行個體)。 此外，您可以使用其中一種可在 Azure 中的 hello 連線選項的 hello 虛擬網路 tooyour 在內部部署網路連線。 基本上，您可以展開您的網路 tooAzure，並且可以完全控制在使用 Azure 提供的企業規模的 hello 優點的 IP 位址區塊。

* [虛擬網路概觀](../../virtual-network/virtual-networks-overview.md)

toocreate 使用 VNet hello Azure CLI，移這裡 toofollow hello 逐步解說。

* [如何使用 VNet toocreate hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>網路安全性群組
網路安全性群組 (NSG) 包含存取控制清單 (ACL) 規則，允許或拒絕網路流量 tooyour 虛擬網路中的 VM 執行個體的清單。 NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。 將 nsg 關聯與子網路產生關聯時，hello ACL 規則適用於 tooall hello VM 執行個體中子網路。 此外，流量 tooan 個別 VM 可能會限制其他關聯 NSG 直接 toothat VM。

* [什麼是網路安全性群組 (NSG)？](../../virtual-network/virtual-networks-nsg.md)
* [如何在 toocreate Nsg hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>使用者定義的路由
當您在 Azure 中新增虛擬機器 (Vm) tooa 虛擬網路 (VNet) 時，您會發現 hello Vm 會自動無法 toocommunicate 彼此 hello 網路上。 您不需要 toospecify 閘道，即使 hello Vm 位於不同的子網路。 hello 也適用於來自 hello Vm toohello 通訊公用網際網路，以及混合式連線從 Azure tooyour 擁有資料中心已存在時，甚至 tooyour 與內部網路。

* [什麼是使用者定義路由和 IP 轉送？](../../virtual-network/virtual-networks-udr-overview.md)
* [在 hello Azure CLI 中建立 UDR](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a>FQDN tooyour Linux VM 建立關聯
Hello Azure 入口網站中建立虛擬機器 (VM) 時使用 hello Resource Manager 部署模型，公用 IP 資源 hello 虛擬機器會自動建立。 您使用此 IP 位址 tooremotely 存取 hello VM。 雖然 hello 入口網站不會建立一個完整的網域名稱或 FQDN，根據預設，您可以加入一個，一旦建立 hello VM。

* [在 hello Azure 入口網站中建立完整網域名稱](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>網路介面
網路介面 (NIC) 是虛擬機器 (VM) 與 hello 基礎軟體網路之間的 hello 互相連線。 本文說明的網路介面，且它 hello Azure Resource Manager 部署模型中的使用方式。

* [虛擬網路介面](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>虛擬 NIC 和 DNS 標籤
如果您的伺服器，您需要 toobe 持續性，但該伺服器會被視為牛與終止並經常部署，您會想 toouse 標記 hello VNET 您 NIC 的 toopersist hello 名稱上的 DNS。  以 hello 遵循逐步解說中，您將設定持續具名的 NIC 與靜態 ip 位址。

* [使用 Azure CLI hello 建立完整的 Linux 環境](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>虛擬網路閘道
使用虛擬網路閘道 toosend 網路流量的 Azure 虛擬網路與內部部署位置之間和 Azure (VNet 對 VNet) 內的虛擬網路之間。 當您設定 VPN 閘道時，您必須建立及設定虛擬網路閘道和虛擬網路閘道連線。

* [關於 VPN 閘道](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>內部負載平衡
Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。 hello 負載平衡器連入流量的各項雲端服務中的狀況良好的服務執行個體或虛擬機器中負載平衡器集可提供高可用性。 Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。

* [建立使用 Azure CLI hello 內部負載平衡器](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

