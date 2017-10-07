---
title: "虛擬網路-Azure CLI 2.0 aaaCreate |Microsoft 文件"
description: "了解如何使用虛擬網路的 toocreate hello Azure CLI 2.0。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a>建立虛擬網路使用 Azure CLI 2.0 hello

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure 有兩個部署模型：Azure Resource Manager 和傳統。 Microsoft 建議您建立透過 hello Resource Manager 部署模型的資源。 深入了解 toolearn hello hello 兩個模型之間的差異讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)發行項。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – 我們 CLI hello 傳統和資源管理部署模型
- [Azure CLI 2.0](#create-a-virtual-network) -hello 資源管理部署模型 （即本文） 我們下一個層代 CLI'
 
    您也可以建立 VNet 資源管理員 」 透過使用其他工具，或從 hello 下列清單中選取不同的選項來建立 VNet 透過 hello 傳統部署模型：

> [!div class="op_single_selector"]
> * [入口網站](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [範本](virtual-networks-create-vnet-arm-template-click.md)
> * [入口網站 (傳統)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (傳統)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (傳統)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a>建立虛擬網路

虛擬網路使用 toocreate hello Azure CLI 2.0 中，完成下列步驟的 hello:

1. 安裝及最新設定 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。

2. 建立資源群組的 VNet 使用 hello [az 群組建立](/cli/azure/group#create)命令與 hello`--name`和`--location`引數：

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. 建立 VNet 和子網路：

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    預期的輸出：
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    使用的參數：

    - `--name TestVNet`： 建立 hello VNet toobe 名稱。
    - `--resource-group TestRG`: # hello 資源群組名稱控制 hello 資源。 
    - `--location centralus`: hello 哪些 toodeploy 位置。
    - `--address-prefix 192.168.0.0/16`: hello 位址前置詞和區塊。  
    - `--subnet-name FrontEnd`: hello hello 子網路名稱。
    - `--subnet-prefix 192.168.1.0/24`: hello 位址前置詞和區塊。

    在 hello toolist hello 的基本資訊 toouse 接下來命令時，您可以查詢 hello VNet 使用[查詢篩選器](/cli/azure/query-az-cli2):

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    這會產生下列輸出的 hello:

        Where      Name      Group

        centralus  TestVNet  TestRG

4. 建立子網路：

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    預期的輸出：

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    使用的參數：

    - `--address-prefix 192.168.2.0/24`：子網路 CIDR 區塊。
    - `--name BackEnd`: Hello 新的子網路的名稱。
    - `--resource-group TestRG`: hello 資源群組。
    - `--vnet-name TestVNet`: hello hello 擁有 VNet 名稱。

5. 查詢 hello 屬性的 hello 新的 VNet:

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    預期的輸出：

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. 查詢 hello 子網路的 hello 的屬性：

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    預期的輸出：

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a>後續步驟

深入了解如何 tooconnect:

- 藉由讀取 hello 的虛擬機器 (VM) tooa 虛擬網路[建立 Linux VM](../virtual-machines/linux/quick-create-cli.md)發行項。 而不是在 hello 步驟中的 hello 文件建立 VNet 和子網路，您可以選取的 VM 的現有 VNet 和子網路 tooconnect。
- 藉由讀取 hello hello 虛擬網路的虛擬網路 tooother[連接 Vnet](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)發行項。
- 使用站對站虛擬私人網路 (VPN) 或 ExpressRoute 電路 hello 虛擬網路 tooan 在內部部署網路。 深入了解如何藉由讀取 hello [VNet tooan 在內部部署網路使用站對站 VPN 連線](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)和[連結 VNet tooan ExpressRoute 電路](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)。
