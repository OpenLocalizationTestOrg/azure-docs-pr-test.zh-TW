---
title: "具有多個 IP 位址使用 hello Azure CLI 2.0 aaaVM |Microsoft 文件"
description: "了解如何 tooassign 多個 IP 位址 tooa 虛擬機器使用 hello Azure CLI 2.0 |資源管理員。"
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a>使用 Azure CLI 2.0 hello toovirtual 機器指派多個 IP 位址

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

本文說明如何透過 hello Azure Resource Manager 部署模型使用的虛擬機器 (VM) toocreate hello Azure CLI 2.0。 Tooresources 透過 hello 傳統部署模型所建立，無法指派多個 IP 位址。 深入了解 Azure 的部署模型，讀取 hello toolearn[了解部署模型](../resource-manager-deployment-model.md)發行項。

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>建立有多個 IP 位址的 VM

您可以完成這項工作中使用 Azure CLI 2.0 （即本文） hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md)。 變更為適用於您環境的 hello 值。 hello 遵循的步驟說明如何 toocreate 範例 VM 具有多個 IP 位址，hello 案例中所述。 視您的實作而定，變更 "" 中的變數值和 IP 位址類型。 

1. 安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)如果您還沒有安裝它。
2. Hello hello 中的步驟，以建立適用於 Linux Vm 的 SSH 公開金鑰和私密金鑰組[適用於 Linux Vm 建立 SSH 公開金鑰和私密金鑰組](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。
3. 從命令殼層，登入與 hello 命令`az login`選取 hello 訂用帳戶正在使用。
4. 建立 hello VM 正在執行 Linux 或 Mac 電腦遵循的 hello 指令碼。 hello 指令碼會建立資源群組、 一個虛擬網路 (VNet)、 使用三個 IP 組態，一個 NIC 和 VM 與 hello 兩個 Nic 附加 tooit。 hello NIC、 公用 IP 位址、 虛擬網路，且 VM 資源必須全部存在於 hello 相同位置和訂用帳戶。 雖然 hello 資源皆具有 tooexist hello 中相同的資源群組，在 hello 下列指令碼一樣。

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

此外 toocreating 與 3 的 IP 組態的 NIC 的 VM，hello 指令碼會建立：

- 單一高階管理磁碟依預設，但您擁有 hello 磁碟類型，您可以建立其他選項。 讀取 hello[建立 Linux VM，使用 Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)文件以取得詳細資料。
- 具有一個子網路和兩個公用 IP 位址的虛擬網路。 或者，您可以使用「現有」虛擬網路、子網路、NIC 或公用 IP 位址資源。 如何 toouse 現有網路資源而建立額外的資源，請輸入的 toolearn `az vm create -h`。

公用 IP 位址需要少許費用。 進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。 沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。 深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。

建立 hello VM 之後，輸入 hello`az network nic show --name MyNic1 --resource-group myResourceGroup`命令 tooview hello NIC 組態。 輸入 hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview hello IP 組態的清單相關聯 toohello nic。

新增 hello 私人 IP 位址 toohello VM 作業系統 hello hello 作業系統的步驟，以[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。

## <a name="add"></a>新增 IP 位址 tooa VM

您可以加入其他私人和公用 IP 位址 tooan 現有 NIC 的完成 hello 遵循的步驟。 hello 範例是根據 hello[案例](#Scenario)本文中所述。

1. 開啟命令殼層，然後完成單一工作階段內剩餘步驟，本節中的 hello。 如果您還沒有安裝和設定 Azure CLI，完成 hello 步驟 hello [Azure CLI 2.0 安裝](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項與登入 tooyour Azure 帳戶以 hello`az-login`命令。

2. 完成下列各節，您的需求為基礎的 hello 的其中一個 hello 步驟：

    **新增私人 IP 位址**
    
    tooadd 私用 IP 位址 tooa NIC，您必須建立使用 hello 命令所示的 IP 組態。 hello 靜態 IP 位址必須是未使用的 hello 子網路位址。

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    使用唯一組態名稱和私人 IP 位址 (適用於具有靜態 IP 位址的組態)，視需要建立最多的組態。

    **新增公用 IP 位址**
    
    公用 IP 位址會藉由將它 tooeither 加入新的 IP 設定或現有的 IP 組態。 視需要完成 hello hello 以下各節，其中的步驟。

    公用 IP 位址需要少許費用。 進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。 沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。 深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。

    - **關聯的 hello 資源 tooa 新的 IP 設定**
    
        每當您在新的 IP 組態中新增公用 IP 位址時，也必須新增私人 IP 位址，因為所有的 IP 組態都必須有一個私人 IP 位址。 您可以新增現有的公用 IP 位址資源，或建立一個新的資源。 toocreate 一個新輸入 hello 下列命令：
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        新的 IP 設定，以靜態私人 IP 位址和相關聯的 hello toocreate *myPublicIP3*公用 IP 位址資源，請輸入下列命令的 hello:

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - **關聯的 hello 資源 tooan 現有 IP 組態**公用 IP 位址資源只能是關聯的 tooan 還沒有相關聯的 IP 組態。 您可以判斷 IP 組態是否有相關聯的公用 IP 位址，輸入下列命令的 hello:

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        傳回的輸出︰
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        因為 hello **PublicIpAddressId**資料行*IpConfig 3*空白的 hello 輸出，沒有公用 IP 位址資源 tooit 目前相關聯。 您可以新增現有公用 IP 位址資源 tooIpConfig-3，或輸入下列其中一個命令 toocreate hello:

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        輸入下列命令 tooassociate hello 公用 IP 位址資源 toohello 現有 IP 設定名為 hello *IPConfig 3*:
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. 檢視 hello 私用 IP 位址與 hello 公用 IP 位址資源識別碼指派的 toohello NIC 輸入 hello 下列命令：

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    傳回的輸出︰ <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. 新增 hello 的私人 IP 位址新增 toohello NIC toohello VM 作業系統的 hello 中的 hello 指示[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。 請勿將 hello 公用 IP 位址 toohello 作業系統。

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
