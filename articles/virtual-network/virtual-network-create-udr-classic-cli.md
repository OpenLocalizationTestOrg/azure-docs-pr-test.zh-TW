---
title: "在 Azure 虛擬網路的 CLI-傳統路由 aaaControl |Microsoft 文件"
description: "了解如何使用 Vnet 中的路由 toocontrol hello hello 傳統部署模型中的 Azure CLI"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a>控制路由和使用 （傳統） 的虛擬應用程式使用 hello Azure CLI

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [範本](virtual-network-create-udr-arm-template.md)
> * [PowerShell (傳統)](virtual-network-create-udr-classic-ps.md)
> * [CLI (傳統)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello 傳統部署模型。 您也可以[控制路由，並在 hello Resource Manager 部署模型中使用虛擬應用裝置](virtual-network-create-udr-arm-cli.md)。

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

下列的 hello 範例 Azure CLI 命令預期已經根據上述的 hello 案例建立簡單的環境。 如果您想 toorun hello 命令，因為它們會顯示在此文件，建立所示的 hello 環境[建立 VNet （傳統） 使用 Azure CLI hello](virtual-networks-create-vnet-classic-cli.md)。

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>建立 hello UDR hello 前端子網路
toocreate hello 路由表和路由所需的 hello 前端子網路，根據 hello 案例以上版本，請遵循下列 hello 步驟。

1. 執行下列命令 tooswitch tooclassic 模式 hello:

    ```azurecli
    azure config mode asm
    ```

    輸出：

        info:    New mode is asm

2. 執行下列命令 toocreate hello hello 前端子網路路由表：

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    輸出：
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    參數：
   
   * **-l (或 --location)**。 Hello 新的 NSG 建立所在的 azure 區域。 在本文案例中為 *westus*。
   * **-n (or --name)**。 名稱 hello 新的 NSG。 在本文案例中為 *NSG-FrontEnd*。
3. 執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 後端子 (192.168.2.0/24) toohello **FW1** VM (已將 192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    輸出：
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    參數：
   
   * **-r (或 --route-table-name)**。 將會加入 hello 路由 hello 路由表的名稱。 在本文案例中為 *UDR-FrontEnd*。
   * **-a (或 --address-prefix)**。 Hello 封包會指向其中的子網路的位址前置詞。 在本文案例中為 *192.168.2.0/24*。
   * **-t (或 --next-hop-type)**。 將傳送流量的目標物件類型。 可能的值為 VirtualAppliance、VirtualNetworkGateway、VNETLocal、Internet 或 None。
   * **-p (或 --next-hop-ip-address)**。 下個躍點的 IP 位址。 在本文案例中為 *192.168.0.4*。
4. Hello 執行的下列命令建立以 hello tooassociate hello 路由表**前端**子網路：

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    輸出：
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    參數：
   
   * **-t (或 --vnet-name)**。 Hello hello 子網路所在的 VNet 的名稱。 在本文案例中為 *TestVNet*。
   * **-n (或 --subnet-name)**。 將加入 hello 子網路 hello 路由表名稱。 在本文案例中為 *FrontEnd*。

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>建立 hello UDR hello 後端子網路
toocreate hello 路由表和路由所需的 hello 後端子根據 hello 案例中，完成下列步驟的 hello:

1. 執行下列命令 toocreate hello hello 後端子網路路由表：

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. 執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 前端的子網路 (192.168.1.0/24) toohello **FW1** VM (已將 192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. 執行 hello 下列命令以 hello tooassociate hello 路由表**後端**子網路：

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

