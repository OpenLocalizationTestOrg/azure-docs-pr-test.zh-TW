---
title: "適用於 Vm （傳統）-Azure CLI 1.0 aaaConfigure 私人 IP 位址 |Microsoft 文件"
description: "了解 tooconfigure 私人 IP 位址的虛擬機器 （傳統） 使用 hello Azure 命令列介面 (CLI) 1.0 的方式。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a><span data-ttu-id="dcc2c-103">設定私人 IP 位址使用 hello Azure CLI 1.0 為虛擬機器 （傳統）</span><span class="sxs-lookup"><span data-stu-id="dcc2c-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="dcc2c-104">本文涵蓋 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="dcc2c-105">您也可以[管理 hello Resource Manager 部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="dcc2c-106">下列的 hello 範例 Azure CLI 命令預期簡單的環境中已經建立。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-106">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="dcc2c-107">如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境中所述[建立 vnet](virtual-networks-create-vnet-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="dcc2c-108">如何 toospecify 靜態私人 IP 位址建立 VM 時</span><span class="sxs-lookup"><span data-stu-id="dcc2c-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="dcc2c-109">名為的新 VM toocreate *DNS01*新的雲端服務中名為*TestService*根據上面的 hello 案例，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dcc2c-109">toocreate a new VM named *DNS01* in a new cloud service named *TestService* based on hello scenario above, follow these steps:</span></span>

1. <span data-ttu-id="dcc2c-110">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="dcc2c-111">執行 hello **azure 服務建立**命令 toocreate hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-111">Run hello **azure service create** command toocreate hello cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="dcc2c-112">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="dcc2c-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="dcc2c-113">執行 hello **azure 建立的 vm**命令 toocreate hello VM。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-113">Run hello **azure create vm** command toocreate hello VM.</span></span> <span data-ttu-id="dcc2c-114">請注意 hello 靜態私人 IP 位址的值。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-114">Notice hello value for a static private IP address.</span></span> <span data-ttu-id="dcc2c-115">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-115">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="dcc2c-116">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="dcc2c-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="dcc2c-117">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-117">**-l (or --location)**.</span></span> <span data-ttu-id="dcc2c-118">將會建立 hello VM 的 azure 區域。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-118">Azure region where hello VM will be created.</span></span> <span data-ttu-id="dcc2c-119">在本文案例中為 *centralus*。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="dcc2c-120">**-n (或 --vm-name)**。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="dcc2c-121">建立 hello VM toobe 的名稱。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-121">Name of hello VM toobe created.</span></span>
   * <span data-ttu-id="dcc2c-122">**-w (或 --virtual-network-name)**。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="dcc2c-123">Hello hello VM 將會建立的 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-123">Name of hello VNet where hello VM will be created.</span></span> 
   * <span data-ttu-id="dcc2c-124">**-S (或 --static-ip)**。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="dcc2c-125">私用的靜態 IP 位址 hello VM。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-125">Static private IP address for hello VM.</span></span>
   * <span data-ttu-id="dcc2c-126">**TestService**。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-126">**TestService**.</span></span> <span data-ttu-id="dcc2c-127">Hello VM 將會建立 hello 雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-127">Name of hello cloud service where hello VM will be created.</span></span>
   * <span data-ttu-id="dcc2c-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="dcc2c-129">使用 toocreate hello VM 映像。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-129">Image used toocreate hello VM.</span></span>
   * <span data-ttu-id="dcc2c-130">**adminuser**。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-130">**adminuser**.</span></span> <span data-ttu-id="dcc2c-131">Hello Windows VM 的本機系統管理員。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-131">Local administrator for hello Windows VM.</span></span>
   * <span data-ttu-id="dcc2c-132">**AdminP@ssw0rd**。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="dcc2c-133">Hello Windows VM 的本機系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-133">Local administrator password for hello Windows VM.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="dcc2c-134">如何 tooretrieve 靜態私人 IP 位址適用於 VM 的資訊</span><span class="sxs-lookup"><span data-stu-id="dcc2c-134">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="dcc2c-135">tooview hello 靜態私人 IP 位址建立 VM 與 hello 指令碼，請執行下列 Azure CLI 命令的 hello hello 資訊，並觀察 hello 值*網路 StaticIP*:</span><span class="sxs-lookup"><span data-stu-id="dcc2c-135">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="dcc2c-136">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="dcc2c-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="dcc2c-137">如何 tooremove 靜態私人 IP 位址從 VM</span><span class="sxs-lookup"><span data-stu-id="dcc2c-137">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="dcc2c-138">tooremove hello 靜態私人 IP 位址執行下列 Azure CLI 命令的 hello 上方的 hello 指令碼中加入 toohello VM:</span><span class="sxs-lookup"><span data-stu-id="dcc2c-138">tooremove hello static private IP address added toohello VM in hello script above, run hello following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="dcc2c-139">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="dcc2c-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a><span data-ttu-id="dcc2c-140">如何 tooadd 靜態的私用 IP tooan 現有的 VM</span><span class="sxs-lookup"><span data-stu-id="dcc2c-140">How tooadd a static private IP tooan existing VM</span></span>
<span data-ttu-id="dcc2c-141">tooadd 靜態私人 IP 位址 toohello 下命令使用上述 runt hello 指令碼建立 VM:</span><span class="sxs-lookup"><span data-stu-id="dcc2c-141">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="dcc2c-142">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="dcc2c-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="dcc2c-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dcc2c-143">Next steps</span></span>
* <span data-ttu-id="dcc2c-144">深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="dcc2c-145">深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="dcc2c-146">請參閱 hello[保留 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dcc2c-146">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

