---
title: "使用 aaaControl 路由和虛擬裝置 hello Azure CLI 2.0 |Microsoft 文件"
description: "了解如何使用 toocontrol 路由和虛擬裝置 hello Azure CLI 2.0。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a>建立使用者定義的路由 (UDR) 使用 hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [範本](virtual-network-create-udr-arm-template.md)
> * [PowerShell (傳統部署)](virtual-network-create-udr-classic-ps.md)
> * [CLI (傳統部署)](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作 

您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本： 

- [Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – 我們 CLI hello 傳統和資源管理部署模型 
- [Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -hello 資源管理部署模型 （即本文） 我們下一個層代 CLI

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

下列的 hello 範例 Azure CLI 命令預期已經根據上述的 hello 案例建立簡單的環境。 如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before)，按一下 **部署 tooAzure**，取代 hello 預設參數值如果有必要，並遵循中的 hello 指示 hello 入口網站。


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>建立 hello UDR hello 前端子網路
toocreate hello 路由表和路由所需的 hello 前端子網路，根據 hello 案例以上版本，請遵循下列 hello 步驟。

1. 建立 hello 前端子網路路由表以 hello [az 網路路由表建立](/cli/azure/network/route-table#create)命令：

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    輸出：

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. 建立路由傳送所有流量 toohello 後端子 (192.168.2.0/24) toohello **FW1** VM (已將 192.168.0.4) 使用 hello [az 網路路由表路由建立](/cli/azure/network/route-table/route#create)命令：

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    輸出：

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    參數：

    * **--route-table-name**。 將會加入 hello 路由 hello 路由表的名稱。 在本文案例中為 *UDR-FrontEnd*。
    * **--address-prefix**。 Hello 封包會指向其中的子網路的位址前置詞。 在本文案例中為 *192.168.2.0/24*。
    * **--next-hop-type**。 將傳送流量的目標物件類型。 可能的值為 VirtualAppliance、VirtualNetworkGateway、VNETLocal、Internet 或 None。
    * **--next-hop-ip-address**。 下個躍點的 IP 位址。 在本文案例中為 *192.168.0.4*。

3. 執行 hello [az 網路 vnet 子網路更新](/cli/azure/network/vnet/subnet#update)命令 tooassociate hello 路由表上面建立以 hello**前端**子網路：

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    輸出：

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    參數：
    
    * **--vnet-name**。 Hello hello 子網路所在的 VNet 的名稱。 在本文案例中為 *TestVNet*。

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>建立 hello UDR hello 後端子網路

toocreate hello 路由表和路由所需的 hello 後端子根據上述步驟的完整 hello hello 案例：

1. 執行下列命令 toocreate hello hello 後端子網路路由表：

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. 執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 前端的子網路 (192.168.1.0/24) toohello **FW1** VM (已將 192.168.0.4):

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. 執行 hello 下列命令以 hello tooassociate hello 路由表**後端**子網路：

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>啟用 FW1 上的 IP 轉送

tooenable 在 hello NIC 所使用的 IP 轉送**FW1**，完成下列步驟 hello:

1. 執行 hello [az 網路 nic 顯示](/cli/azure/network/nic#show)命令搭配 JMESPATH 篩選 toodisplay hello 目前**啟用 ip 轉送**值**啟用 IP 轉送**。 才應該設定太*false*。

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    輸出：

        false

2. 執行下列命令 tooenable IP 轉送的 hello:

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    您可以檢查 hello 輸出資料流處理的 toohello 主控台中，或只重新測試特定的 hello **enableIpForwarding**值：

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    輸出：

        true

    參數：

    **--ip-forwarding**：*true* 或 *false*。

