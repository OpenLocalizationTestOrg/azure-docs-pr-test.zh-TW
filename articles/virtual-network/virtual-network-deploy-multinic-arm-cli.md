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
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a><span data-ttu-id="f5907-103">建立與使用 Azure CLI 2.0 hello 的多個 Nic VM</span><span class="sxs-lookup"><span data-stu-id="f5907-103">Create a VM with multiple NICs using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f5907-104">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="f5907-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="f5907-105">本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](virtual-network-deploy-multinic-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="f5907-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <span data-ttu-id="f5907-106"><a name="create"></a>建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="f5907-106"><a name="create"></a>Create hello VM</span></span>

<span data-ttu-id="f5907-107">您可以完成這項工作中使用 Azure CLI 2.0 （即本文） hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="f5907-107">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="f5907-108">hello 中的值""hello 遵循的步驟中的 hello 變數被 hello 案例的設定建立資源。</span><span class="sxs-lookup"><span data-stu-id="f5907-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="f5907-109">變更為適用於您環境的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="f5907-109">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="f5907-110">安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)如果您還沒有安裝它。</span><span class="sxs-lookup"><span data-stu-id="f5907-110">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="f5907-111">Hello hello 中的步驟，以建立適用於 Linux Vm 的 SSH 公開金鑰和私密金鑰組[適用於 Linux Vm 建立 SSH 公開金鑰和私密金鑰組](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f5907-111">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="f5907-112">從命令殼層，登入與 hello 命令`az login`。</span><span class="sxs-lookup"><span data-stu-id="f5907-112">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="f5907-113">建立 hello VM 正在執行 Linux 或 Mac 電腦遵循的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f5907-113">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="f5907-114">hello 指令碼會建立資源群組、 一個虛擬網路 (VNet) 兩個子網路、 兩個 Nic，與具有 hello 兩個 Nic VM 附加 tooit。</span><span class="sxs-lookup"><span data-stu-id="f5907-114">hello script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="f5907-115">Hello Nic 的其中一個是連接的 tooone 子網路，並指派靜態的公用和私用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f5907-115">One of hello NICs is connected tooone subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="f5907-116">hello 其他 NIC 是連接的 toohello 其他子網路，並指派靜態私人 IP 位址和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f5907-116">hello other NIC is connected toohello other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="f5907-117">hello NIC、 公用 IP 位址、 虛擬網路，且 VM 資源必須全部存在於 hello 相同位置和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5907-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="f5907-118">雖然 hello 資源皆具有 tooexist hello 中相同的資源群組，在 hello 下列指令碼一樣。</span><span class="sxs-lookup"><span data-stu-id="f5907-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

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

<span data-ttu-id="f5907-119">此外 toocreating 有兩個 Nic VM，hello 指令碼會建立：</span><span class="sxs-lookup"><span data-stu-id="f5907-119">In addition toocreating a VM with two NICs, hello script creates:</span></span>
- <span data-ttu-id="f5907-120">單一高階管理磁碟依預設，但您擁有 hello 磁碟類型，您可以建立其他選項。</span><span class="sxs-lookup"><span data-stu-id="f5907-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="f5907-121">讀取 hello[建立 Linux VM，使用 Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)文件以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f5907-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="f5907-122">具有兩個子網路和一個公用 IP 位址的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f5907-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="f5907-123">或者，您可以使用「現有」虛擬網路、子網路、NIC 或公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="f5907-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="f5907-124">如何 toouse 現有網路資源而建立額外的資源，請輸入的 toolearn `az vm create -h`。</span><span class="sxs-lookup"><span data-stu-id="f5907-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="f5907-125"><a name = "validate"></a>驗證 VM 建立和 NIC</span><span class="sxs-lookup"><span data-stu-id="f5907-125"><a name = "validate"></a>Validate VM creation and NICs</span></span>

1. <span data-ttu-id="f5907-126">輸入 hello 命令`az resource list --resouce-group Multi-NIC-VM --output table`toosee hello 資源 hello 指令碼所建立的清單。</span><span class="sxs-lookup"><span data-stu-id="f5907-126">Enter hello command `az resource list --resouce-group Multi-NIC-VM --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="f5907-127">傳回輸出的 hello 中應該有六個資源： 兩個 Nic，一個磁碟、 一個公用 IP 位址，一個虛擬網路，以及虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f5907-127">There should be six resources in hello returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="f5907-128">輸入 hello 命令`az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`。</span><span class="sxs-lookup"><span data-stu-id="f5907-128">Enter hello command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="f5907-129">在 hello 傳回輸出，請注意 hello 值**IpAddress**和 hello 該值的**PublicIpAllocationMethod**是*靜態*。</span><span class="sxs-lookup"><span data-stu-id="f5907-129">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="f5907-130">執行下列命令的 hello 之前，先移除 hello <>、 取代*使用者名稱*hello 名稱用於 hello**使用者名稱**變數在 hello 指令碼，並取代*ipAddress*以 hello **ipAddress** hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f5907-130">Before running hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="f5907-131">Hello 執行的下列命令 tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`。</span><span class="sxs-lookup"><span data-stu-id="f5907-131">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="f5907-132">一旦連接 toohello VM 後，執行 hello`sudo ifconfig`命令 toosee *eth0*和*eth1*介面。</span><span class="sxs-lookup"><span data-stu-id="f5907-132">Once connected toohello VM, run hello `sudo ifconfig` command toosee *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="f5907-133">每個 NIC 已被指派 hello 靜態私人 IP 位址由 hello Azure DHCP 伺服器 hello 指令碼中指定。</span><span class="sxs-lookup"><span data-stu-id="f5907-133">Each NIC has been assigned hello static private IP addresses specified in hello script by hello Azure DHCP servers.</span></span> <span data-ttu-id="f5907-134">hello 分派 toohello Nic 的 IP 和 MAC 位址不會變更直到刪除 VM hello。</span><span class="sxs-lookup"><span data-stu-id="f5907-134">hello IP and MAC addresses assigned toohello NICs do not change until hello VM is deleted.</span></span> <span data-ttu-id="f5907-135">我們建議，您不會變更 IP 位址內的作業系統，因為它可以停用連線 toohello 電腦。</span><span class="sxs-lookup"><span data-stu-id="f5907-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity toohello computer.</span></span> <span data-ttu-id="f5907-136">公用 IP 位址不會出現在 hello 作業系統，因為它們是網路位址轉譯 tooand 從 hello hello Azure 基礎結構的私用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f5907-136">Public IP addresses do not appear within hello operating system, as they are network address translated tooand from hello private IP address by hello Azure infrastructure.</span></span>

## <span data-ttu-id="f5907-137"><a name= "clean-up"></a>移除 hello VM 和相關聯的資源</span><span class="sxs-lookup"><span data-stu-id="f5907-137"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="f5907-138">建議您刪除 hello 資源建立在這個練習中，如果您不會在生產環境中使用它們。</span><span class="sxs-lookup"><span data-stu-id="f5907-138">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="f5907-139">VM、公用 IP 位址和磁碟資源在佈建後就會產生費用。</span><span class="sxs-lookup"><span data-stu-id="f5907-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="f5907-140">在此練習，請完成下列步驟的 hello 期間建立 tooremove hello 資源：</span><span class="sxs-lookup"><span data-stu-id="f5907-140">tooremove hello resources created during this exercise, complete hello following steps:</span></span>
1. <span data-ttu-id="f5907-141">在 hello 資源群組中，執行 hello tooview hello 資源`az resource list --resource-group Multi-NIC-VM`命令。</span><span class="sxs-lookup"><span data-stu-id="f5907-141">tooview hello resources in hello resource group, run hello `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="f5907-142">請確認沒有在 hello 資源群組中，在本文中的 hello 指令碼所建立的 hello 資源以外的資源。</span><span class="sxs-lookup"><span data-stu-id="f5907-142">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="f5907-143">所有的資源建立在這個練習中，執行 hello toodelete`az group delete --name Multi-NIC-VM`命令。</span><span class="sxs-lookup"><span data-stu-id="f5907-143">toodelete all resources created in this exercise, run hello `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="f5907-144">hello 命令會刪除 hello 資源群組和它所包含的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="f5907-144">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5907-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5907-145">Next steps</span></span>

<span data-ttu-id="f5907-146">任何網路流量從 VM 建立本文章中的 hello tooand。</span><span class="sxs-lookup"><span data-stu-id="f5907-146">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="f5907-147">您可以定義的限制，可以從每個網路介面、 每個子網路，或兩者都 tooand hello 流量輸入和輸出規則內 NSG。</span><span class="sxs-lookup"><span data-stu-id="f5907-147">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from each network interface, each subnet, or both.</span></span> <span data-ttu-id="f5907-148">深入了解 Nsg，讀取 hello toolearn [NSG 概觀](virtual-networks-nsg.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="f5907-148">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
