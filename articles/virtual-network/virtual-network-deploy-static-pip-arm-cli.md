---
title: "aaaCreate VM 使用靜態公用 IP 位址-Azure CLI 2.0 |Microsoft 文件"
description: "了解 toocreate 具有靜態公用 IP 位址使用的 VM hello Azure 命令列介面 (CLI) 2.0 的方式。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a><span data-ttu-id="f0e4a-103">建立具有靜態公用 IP 位址使用 hello Azure CLI 2.0 的 VM</span><span class="sxs-lookup"><span data-stu-id="f0e4a-103">Create a VM with a static public IP address using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0e4a-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f0e4a-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="f0e4a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0e4a-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="f0e4a-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f0e4a-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="f0e4a-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f0e4a-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="f0e4a-108">範本</span><span class="sxs-lookup"><span data-stu-id="f0e4a-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="f0e4a-109">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="f0e4a-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="f0e4a-110">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="f0e4a-111">本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="f0e4a-112"><a name = "create"></a>建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="f0e4a-112"><a name = "create"></a>Create hello VM</span></span>

<span data-ttu-id="f0e4a-113">您可以完成這項工作中使用 Azure CLI 2.0 （即本文） hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-113">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="f0e4a-114">hello 中的值""hello 遵循的步驟中的 hello 變數被 hello 案例的設定建立資源。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-114">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="f0e4a-115">變更為適用於您環境的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-115">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="f0e4a-116">安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)如果您還沒有安裝它。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-116">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="f0e4a-117">Hello hello 中的步驟，以建立適用於 Linux Vm 的 SSH 公開金鑰和私密金鑰組[適用於 Linux Vm 建立 SSH 公開金鑰和私密金鑰組](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-117">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="f0e4a-118">從命令殼層，登入與 hello 命令`az login`。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-118">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="f0e4a-119">建立 hello VM 正在執行 Linux 或 Mac 電腦遵循的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-119">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="f0e4a-120">hello Azure 公用 IP 位址、 虛擬網路、 網路介面，且 VM 資源必須全部存在於 hello 相同位置。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-120">hello Azure public IP address, virtual network, network interface, and VM resources must all exist in hello same location.</span></span> <span data-ttu-id="f0e4a-121">雖然 hello 資源皆具有 tooexist hello 中相同的資源群組，在 hello 下列指令碼一樣。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-121">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
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
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

<span data-ttu-id="f0e4a-122">此外 toocreating VM，hello 指令碼會建立：</span><span class="sxs-lookup"><span data-stu-id="f0e4a-122">In addition toocreating a VM, hello script creates:</span></span>
- <span data-ttu-id="f0e4a-123">單一高階管理磁碟依預設，但您擁有 hello 磁碟類型，您可以建立其他選項。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-123">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="f0e4a-124">讀取 hello[建立 Linux VM，使用 Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)文件以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-124">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="f0e4a-125">虛擬網路、子網路、NIC 和公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="f0e4a-126">或者，您可以使用「現有」虛擬網路、子網路、NIC 或公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="f0e4a-127">如何 toouse 現有網路資源而建立額外的資源，請輸入的 toolearn `az vm create -h`。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-127">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="f0e4a-128"><a name = "validate"></a>驗證 VM 建立和公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f0e4a-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="f0e4a-129">輸入 hello 命令`az resource list --resouce-group IaaSStory --output table`toosee hello 資源 hello 指令碼所建立的清單。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-129">Enter hello command `az resource list --resouce-group IaaSStory --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="f0e4a-130">傳回輸出的 hello 中應該有五個資源： 網路介面、 磁碟、 公用 IP 位址、 虛擬網路和虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-130">There should be five resources in hello returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="f0e4a-131">輸入 hello 命令`az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-131">Enter hello command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="f0e4a-132">在 hello 傳回輸出，請注意 hello 值**IpAddress**和 hello 該值的**PublicIpAllocationMethod**是*靜態*。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-132">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="f0e4a-133">在執行之前 hello 下列命令，移除 hello <>、 取代*使用者名稱*hello 名稱用於 hello**使用者名稱**變數在 hello 指令碼，並取代*ipAddress*以 hello **ipAddress** hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-133">Before executing hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="f0e4a-134">Hello 執行的下列命令 tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-134">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="f0e4a-135"><a name= "clean-up"></a>移除 hello VM 和相關聯的資源</span><span class="sxs-lookup"><span data-stu-id="f0e4a-135"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="f0e4a-136">建議您刪除 hello 資源建立在這個練習中，如果您不會在生產環境中使用它們。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-136">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="f0e4a-137">VM、公用 IP 位址和磁碟資源在佈建後就會產生費用。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="f0e4a-138">在此練習，請完成下列步驟的 hello 期間建立 tooremove hello 資源：</span><span class="sxs-lookup"><span data-stu-id="f0e4a-138">tooremove hello resources created during this exercise, complete hello following steps:</span></span>

1. <span data-ttu-id="f0e4a-139">在 hello 資源群組中，執行 hello tooview hello 資源`az resource list --resource-group IaaSStory`命令。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-139">tooview hello resources in hello resource group, run hello `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="f0e4a-140">請確認沒有在 hello 資源群組中，在本文中的 hello 指令碼所建立的 hello 資源以外的資源。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-140">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="f0e4a-141">所有的資源建立在這個練習中，執行 hello toodelete`az group delete -n IaaSStory`命令。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-141">toodelete all resources created in this exercise, run hello `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="f0e4a-142">hello 命令會刪除 hello 資源群組和它所包含的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-142">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0e4a-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0e4a-143">Next steps</span></span>

<span data-ttu-id="f0e4a-144">任何網路流量從 VM 建立本文章中的 hello tooand。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-144">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="f0e4a-145">您可以定義的限制，可以傳送 hello 網路介面、 hello 的子網路，或兩者都從 tooand hello 流量輸入和輸出規則內 NSG。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-145">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from hello network interface, hello subnet, or both.</span></span> <span data-ttu-id="f0e4a-146">深入了解 Nsg，讀取 hello toolearn [NSG 概觀](virtual-networks-nsg.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="f0e4a-146">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
