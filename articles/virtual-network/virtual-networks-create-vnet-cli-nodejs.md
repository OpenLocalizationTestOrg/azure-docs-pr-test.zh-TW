---
title: "虛擬網路使用 aaaCreate hello Azure CLI 1.0 |Microsoft 文件"
description: "了解如何使用虛擬網路的 toocreate hello Azure CLI 1.0 |資源管理員。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a>建立虛擬網路使用 Azure CLI hello

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure 有兩個部署模型：Azure Resource Manager 和傳統。 Microsoft 建議您建立透過 hello Resource Manager 部署模型的資源。 深入了解 toolearn hello hello 兩個模型之間的差異讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)發行項。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -hello 資源管理部署模型我們下一個層代 CLI
- [Azure CLI 1.0](#create-a-virtual-network) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>建立虛擬網路

虛擬網路使用 toocreate hello Azure CLI，完成下列步驟的 hello:

1. 在安裝和設定步驟的下列 hello Azure CLI hello hello[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)發行項。

2. 建立 VNet 和子網路：

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    預期的輸出：
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    使用的參數：

   * **--vnet**。 建立 hello VNet toobe 的名稱。 在本文案例中為 *TestVNet*
   * **-e (或 --address-space)**。 VNet 位址空間。 在本文案例中為 *192.168.0.0*
   * **-i (或 -cidr)**。 CIDR 格式的網路遮罩。 在本文案例中為 *16*。
   * **-n (或 --subnet-name**)。 Hello 第一個子網路的名稱。 在本文案例中為 *FrontEnd*。
   * **-p (或 --subnet-start-ip)**。 子網路的起始 IP 位址或子網路位址空間。 在本文案例中為 *192.168.1.0*。
   * **-r (或 --subnet-cidr)**。 CIDR 格式的子網路網路遮罩。 在本文案例中為 *24*。
   * **-l (或 --location)**。 Hello VNet 建立所在的 azure 區域。 在本文案例中為「美國中部」 。

3. 建立子網路：

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    預期的輸出：

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    使用的參數：

   * **-t (或 --vnet-name)**。 Hello hello 子網路將會建立的 VNet 的名稱。 在本文案例中為 *TestVNet*。
   * **-n (or --name)**。 Hello 新的子網路的名稱。 在本文案例中為 *BackEnd*。
   * **-a (或 --address-prefix)**。 子網路 CIDR 區塊。 在本文案例中為 *192.168.2.0/24*。
   
4. tooview hello 屬性 hello 新的 VNet:

    ```azurecli
    azure network vnet show
    ```
   
    預期的輸出：
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a>後續步驟

深入了解如何 tooconnect:

- 藉由讀取 hello 的虛擬機器 (VM) tooa 虛擬網路[建立 Linux VM](../virtual-machines/linux/quick-create-cli.md)發行項。 而不是在 hello 步驟中的 hello 文件建立 VNet 和子網路，您可以選取的 VM 的現有 VNet 和子網路 tooconnect。
- 藉由讀取 hello hello 虛擬網路的虛擬網路 tooother[連接 Vnet](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)發行項。
- 使用站對站虛擬私人網路 (VPN) 或 ExpressRoute 電路 hello 虛擬網路 tooan 在內部部署網路。 深入了解如何藉由讀取 hello [VNet tooan 在內部部署網路使用站對站 VPN 連線](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)和[連結 VNet tooan ExpressRoute 電路](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)。
