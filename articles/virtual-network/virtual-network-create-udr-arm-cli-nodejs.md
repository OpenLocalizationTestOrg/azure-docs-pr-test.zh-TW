---
title: "使用 aaaControl 路由和虛擬裝置 hello Azure CLI 1.0 |Microsoft 文件"
description: "了解如何使用 toocontrol 路由和虛擬裝置 hello Azure CLI 1.0。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a>建立使用者定義的路由 (UDR) 使用 hello Azure CLI 1.0

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [範本](virtual-network-create-udr-arm-template.md)
> * [PowerShell (傳統)](virtual-network-create-udr-classic-ps.md)
> * [CLI (傳統)](virtual-network-create-udr-classic-cli.md)

建立自訂路由和使用 Azure CLI hello 的虛擬應用裝置。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作 

您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本： 

- [Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -hello 資源管理部署模型我們下一個層代 CLI 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

下列的 hello 範例 Azure CLI 命令預期已經根據上述的 hello 案例建立簡單的環境。 如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before)，按一下 **部署 tooAzure**，取代 hello 預設參數值如果有必要，並遵循中的 hello 指示 hello 入口網站。


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>建立 hello UDR hello 前端子網路
toocreate hello 路由表和路由所需的 hello 前端子網路，根據 hello 案例以上版本，請遵循下列 hello 步驟。

1. 執行下列命令 toocreate hello hello 前端子網路路由表：

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    輸出：
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    參數：
   
   * **-g (or --resource-group)**。 將會建立 hello UDR hello 資源群組的名稱。 在本文案例中為 *TestRG*。
   * **-l (或 --location)**。 Hello 新 UDR 建立所在的 azure 區域。 在本文案例中為 *westus*。
   * **-n (or --name)**。 名稱 hello 新 UDR。 在本文案例中為 *UDR-FrontEnd*。
2. 執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 後端子 (192.168.2.0/24) toohello **FW1** VM (已將 192.168.0.4):

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    輸出：
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    參數：
   
   * **-r (或 --route-table-name)**。 將會加入 hello 路由 hello 路由表的名稱。 在本文案例中為 *UDR-FrontEnd*。
   * **-a (或 --address-prefix)**。 Hello 封包會指向其中的子網路的位址前置詞。 在本文案例中為 *192.168.2.0/24*。
   * **-y (或 --next-hop-type)**。 將傳送流量的目標物件類型。 可能的值為 VirtualAppliance、VirtualNetworkGateway、VNETLocal、Internet 或 None。
   * **-p (或 --next-hop-ip-address)**。 下個躍點的 IP 位址。 在本文案例中為 *192.168.0.4*。
3. Hello 執行的下列命令以 hello 上面所建立的 tooassociate hello 路由表**前端**子網路：

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    輸出：
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    參數：
   
   * **-e (或 --vnet-name)**。 Hello hello 子網路所在的 VNet 的名稱。 在本文案例中為 *TestVNet*。

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>建立 hello UDR hello 後端子網路
toocreate hello 路由表和路由所需的 hello 後端子根據上述步驟的完整 hello hello 案例：

1. 執行下列命令 toocreate hello hello 後端子網路路由表：

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. 執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 前端的子網路 (192.168.1.0/24) toohello **FW1** VM (已將 192.168.0.4):

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. 執行 hello 下列命令以 hello tooassociate hello 路由表**後端**子網路：

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>啟用 FW1 上的 IP 轉送
tooenable 在 hello NIC 所使用的 IP 轉送**FW1**，完成下列步驟 hello:

1. 執行之後，請注意 hello 值 hello 命令**啟用 IP 轉送**。 才應該設定太*false*。

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    輸出：
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. 執行下列命令 tooenable IP 轉送的 hello:

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    輸出：
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    參數：
   
   * **-f (或 --enable-ip-forwarding)**。 *true* 或 *false*。

