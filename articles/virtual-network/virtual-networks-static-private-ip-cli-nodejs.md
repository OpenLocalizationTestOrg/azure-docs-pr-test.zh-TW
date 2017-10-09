---
title: "對於 Azure CLI 1.0 的 Vm-aaaConfigure 私人 IP 位址 |Microsoft 文件"
description: "了解 tooconfigure 私人 IP 位址的虛擬機器使用 hello Azure 命令列介面 (CLI) 1.0 的方式。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a><span data-ttu-id="fc351-103">設定使用 Azure CLI 1.0 hello 為虛擬機器的私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="fc351-103">Configure private IP addresses for a virtual machine using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="fc351-104">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="fc351-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="fc351-105">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="fc351-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="fc351-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="fc351-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="fc351-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -我們的下一代 CLI hello 資源管理部署模型</span><span class="sxs-lookup"><span data-stu-id="fc351-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="fc351-108">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="fc351-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="fc351-109">您也可以[管理 hello 傳統部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="fc351-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="fc351-110">下列的 hello 範例 Azure CLI 命令預期簡單的環境中已經建立。</span><span class="sxs-lookup"><span data-stu-id="fc351-110">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="fc351-111">如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境中所述[建立 vnet](virtual-networks-create-vnet-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="fc351-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="fc351-112">如何 toospecify 靜態私人 IP 位址建立 VM 時</span><span class="sxs-lookup"><span data-stu-id="fc351-112">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="fc351-113">名為的 VM toocreate *DNS01*在 hello*前端*名為 VNet 的子網路*TestVNet*以靜態私人 ip 位址的*192.168.1.101*，請遵循下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="fc351-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="fc351-114">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="fc351-114">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="fc351-115">執行 hello **azure 組態模式**命令 tooswitch tooResource 管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fc351-115">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="fc351-116">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="fc351-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="fc351-117">執行 hello **azure 網路的公用 ip 建立**toocreate hello VM 的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="fc351-117">Run hello **azure network public-ip create** toocreate a public IP for hello VM.</span></span> <span data-ttu-id="fc351-118">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="fc351-118">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="fc351-119">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="fc351-119">Expected output:</span></span>
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * <span data-ttu-id="fc351-120">**-g (or --resource-group)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="fc351-121">在將要建立的 hello 資源群組 hello 公用 IP 的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc351-121">Name of hello resource group hello public IP will be created in.</span></span>
   * <span data-ttu-id="fc351-122">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-122">**-n (or --name)**.</span></span> <span data-ttu-id="fc351-123">Hello 公用 IP 的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc351-123">Name of hello public IP.</span></span>
   * <span data-ttu-id="fc351-124">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-124">**-l (or --location)**.</span></span> <span data-ttu-id="fc351-125">將會建立 hello 公用 IP 的 azure 區域。</span><span class="sxs-lookup"><span data-stu-id="fc351-125">Azure region where hello public IP will be created.</span></span> <span data-ttu-id="fc351-126">在本文案例中為 *centralus*。</span><span class="sxs-lookup"><span data-stu-id="fc351-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="fc351-127">執行 hello **azure 網路的 nic 建立**命令 toocreate 以靜態私人 ip 位址的 NIC。</span><span class="sxs-lookup"><span data-stu-id="fc351-127">Run hello **azure network nic create** command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="fc351-128">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="fc351-128">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="fc351-129">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="fc351-129">Expected output:</span></span>
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * <span data-ttu-id="fc351-130">**-a (or --private-ip-address)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="fc351-131">Hello NIC 私用靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="fc351-131">Static private IP address for hello NIC.</span></span>
   * <span data-ttu-id="fc351-132">**-m (or --subnet-vnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="fc351-133">Hello VNet 將會建立 hello NIC 的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc351-133">Name of hello VNet where hello NIC will be created.</span></span>
   * <span data-ttu-id="fc351-134">**-k (or --subnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="fc351-135">將會建立 hello NIC 的 hello 子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc351-135">Name of hello subnet where hello NIC will be created.</span></span>
5. <span data-ttu-id="fc351-136">執行 hello **azure vm 建立**命令 toocreate hello 使用 hello 公用 IP 與 NIC VM 上面所建立。</span><span class="sxs-lookup"><span data-stu-id="fc351-136">Run hello **azure vm create** command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="fc351-137">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="fc351-137">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="fc351-138">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="fc351-138">Expected output:</span></span>
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * <span data-ttu-id="fc351-139">**-y (or --os-type)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="fc351-140">類型的作業系統 hello VM，或是*Windows*或*Linux*。</span><span class="sxs-lookup"><span data-stu-id="fc351-140">Type of operating system for hello VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="fc351-141">**-f (or --nic-name)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="fc351-142">將使用 hello NIC hello VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc351-142">Name of hello NIC hello VM will use.</span></span>
   * <span data-ttu-id="fc351-143">**-i (or --public-ip-name)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="fc351-144">將要使用的公用 IP hello hello VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc351-144">Name of hello public IP hello VM will use.</span></span>
   * <span data-ttu-id="fc351-145">**-F (or --vnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="fc351-146">Hello hello VM 將會建立的 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc351-146">Name of hello VNet where hello VM will be created.</span></span>
   * <span data-ttu-id="fc351-147">**-j (or --vnet-subnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="fc351-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="fc351-148">Hello VM 將會建立 hello 子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc351-148">Name of hello subnet where hello VM will be created.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="fc351-149">如何 tooretrieve 靜態私人 IP 位址適用於 VM 的資訊</span><span class="sxs-lookup"><span data-stu-id="fc351-149">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="fc351-150">tooview hello 靜態私人 IP 位址建立 VM 與 hello 指令碼，請執行下列 Azure CLI 命令的 hello hello 資訊，並觀察 hello 值*私用 IP 配置方法*和*的私用IP位址*:</span><span class="sxs-lookup"><span data-stu-id="fc351-150">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="fc351-151">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="fc351-151">Expected output:</span></span>

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="fc351-152">如何 tooremove 靜態私人 IP 位址從 VM</span><span class="sxs-lookup"><span data-stu-id="fc351-152">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="fc351-153">您無法從 Azure CLI 的 NIC 移除資源管理員的靜態私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fc351-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="fc351-154">您必須建立新的 NIC，它會使用動態 IP、 移除 hello hello VM，從上一個 NIC，然後再加入新 NIC toohello hello VM。</span><span class="sxs-lookup"><span data-stu-id="fc351-154">You must create a new NIC that uses a dynamic IP, remove hello previous NIC from hello VM, and then add hello new NIC toohello VM.</span></span> <span data-ttu-id="fc351-155">toochange hello NIC hello VM 使用 int eh 上述命令，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="fc351-155">toochange hello NIC for hello VM used int eh commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="fc351-156">執行 hello **azure 網路的 nic 建立**命令 toocreate 使用動態 IP 配置的新 NIC。</span><span class="sxs-lookup"><span data-stu-id="fc351-156">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="fc351-157">請注意如何您不需要 toospecify hello IP 位址目前。</span><span class="sxs-lookup"><span data-stu-id="fc351-157">Notice how you do not need toospecify hello IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="fc351-158">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="fc351-158">Expected output:</span></span>
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. <span data-ttu-id="fc351-159">執行 hello **azure vm 集**命令 toochange hello hello VM 所使用的 NIC。</span><span class="sxs-lookup"><span data-stu-id="fc351-159">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="fc351-160">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="fc351-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="fc351-161">如果想，執行 hello **azure 網路的 nic 刪除**命令 toodelete hello 舊 nic。</span><span class="sxs-lookup"><span data-stu-id="fc351-161">If wanted, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="fc351-162">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="fc351-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="fc351-163">Tooadd 靜態私人 IP 定址 tooan 現有 VM 的方式</span><span class="sxs-lookup"><span data-stu-id="fc351-163">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="fc351-164">tooadd 靜態私人 IP 位址 toohello NIC，供 VM 使用 hello 指令碼，請建立會執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc351-164">tooadd a static private IP address toohello NIC used by teh VM created using hello script above, run hello following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="fc351-165">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="fc351-165">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a><span data-ttu-id="fc351-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc351-166">Next steps</span></span>
* <span data-ttu-id="fc351-167">深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="fc351-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="fc351-168">深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="fc351-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="fc351-169">請參閱 hello[保留 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fc351-169">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

