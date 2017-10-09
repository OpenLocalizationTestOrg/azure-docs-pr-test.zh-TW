---
title: "具有多個 Nic-Azure CLI 2.0 VM aaaCreate |Microsoft 文件"
description: "了解與使用多個 Nic VM toocreate hello Azure CLI 2.0 的方式。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a>建立與使用 Azure CLI 2.0 hello 的多個 Nic VM

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。  本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](virtual-network-deploy-multinic-classic-cli.md)。
>

## <a name="create"></a>建立 hello VM

您可以完成這項工作中使用 Azure CLI 2.0 （即本文） hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md)。 hello 中的值""hello 遵循的步驟中的 hello 變數被 hello 案例的設定建立資源。 變更為適用於您環境的 hello 值。

1. 安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)如果您還沒有安裝它。
2. Hello hello 中的步驟，以建立適用於 Linux Vm 的 SSH 公開金鑰和私密金鑰組[適用於 Linux Vm 建立 SSH 公開金鑰和私密金鑰組](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。
3. 從命令殼層，登入與 hello 命令`az login`。
4. 建立 hello VM 正在執行 Linux 或 Mac 電腦遵循的 hello 指令碼。 hello 指令碼會建立資源群組、 一個虛擬網路 (VNet) 兩個子網路、 兩個 Nic，與具有 hello 兩個 Nic VM 附加 tooit。 Hello Nic 的其中一個是連接的 tooone 子網路，並指派靜態的公用和私用 IP 位址。 hello 其他 NIC 是連接的 toohello 其他子網路，並指派靜態私人 IP 位址和公用 IP 位址。 hello NIC、 公用 IP 位址、 虛擬網路，且 VM 資源必須全部存在於 hello 相同位置和訂用帳戶。 雖然 hello 資源皆具有 tooexist hello 中相同的資源群組，在 hello 下列指令碼一樣。

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

此外 toocreating 有兩個 Nic VM，hello 指令碼會建立：
- 單一高階管理磁碟依預設，但您擁有 hello 磁碟類型，您可以建立其他選項。 讀取 hello[建立 Linux VM，使用 Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)文件以取得詳細資料。
- 具有兩個子網路和一個公用 IP 位址的虛擬網路。 或者，您可以使用「現有」虛擬網路、子網路、NIC 或公用 IP 位址資源。 如何 toouse 現有網路資源而建立額外的資源，請輸入的 toolearn `az vm create -h`。

## <a name = "validate"></a>驗證 VM 建立和 NIC

1. 輸入 hello 命令`az resource list --resouce-group Multi-NIC-VM --output table`toosee hello 資源 hello 指令碼所建立的清單。 傳回輸出的 hello 中應該有六個資源： 兩個 Nic，一個磁碟、 一個公用 IP 位址，一個虛擬網路，以及虛擬機器。
2. 輸入 hello 命令`az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`。 在 hello 傳回輸出，請注意 hello 值**IpAddress**和 hello 該值的**PublicIpAllocationMethod**是*靜態*。
3. 執行下列命令的 hello 之前，先移除 hello <>、 取代*使用者名稱*hello 名稱用於 hello**使用者名稱**變數在 hello 指令碼，並取代*ipAddress*以 hello **ipAddress** hello 上一個步驟。 Hello 執行的下列命令 tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`。 
4. 一旦連接 toohello VM 後，執行 hello`sudo ifconfig`命令 toosee *eth0*和*eth1*介面。 每個 NIC 已被指派 hello 靜態私人 IP 位址由 hello Azure DHCP 伺服器 hello 指令碼中指定。 hello 分派 toohello Nic 的 IP 和 MAC 位址不會變更直到刪除 VM hello。 我們建議，您不會變更 IP 位址內的作業系統，因為它可以停用連線 toohello 電腦。 公用 IP 位址不會出現在 hello 作業系統，因為它們是網路位址轉譯 tooand 從 hello hello Azure 基礎結構的私用 IP 位址。

## <a name= "clean-up"></a>移除 hello VM 和相關聯的資源

建議您刪除 hello 資源建立在這個練習中，如果您不會在生產環境中使用它們。 VM、公用 IP 位址和磁碟資源在佈建後就會產生費用。 在此練習，請完成下列步驟的 hello 期間建立 tooremove hello 資源：
1. 在 hello 資源群組中，執行 hello tooview hello 資源`az resource list --resource-group Multi-NIC-VM`命令。
2. 請確認沒有在 hello 資源群組中，在本文中的 hello 指令碼所建立的 hello 資源以外的資源。 
3. 所有的資源建立在這個練習中，執行 hello toodelete`az group delete --name Multi-NIC-VM`命令。 hello 命令會刪除 hello 資源群組和它所包含的所有 hello 資源。

## <a name="next-steps"></a>後續步驟

任何網路流量從 VM 建立本文章中的 hello tooand。 您可以定義的限制，可以從每個網路介面、 每個子網路，或兩者都 tooand hello 流量輸入和輸出規則內 NSG。 深入了解 Nsg，讀取 hello toolearn [NSG 概觀](virtual-networks-nsg.md)發行項。
