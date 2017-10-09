---
title: "aaaCreate 具有多個 Nic-Azure CLI 1.0 的 VM （傳統） |Microsoft 文件"
description: "了解 toocreate 具有使用多個 Nic 的 VM （傳統） hello Azure 命令列介面 (CLI) 1.0 的方式。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="5112f-103">建立與使用 Azure CLI 1.0 hello 的多個 Nic VM （傳統）</span><span class="sxs-lookup"><span data-stu-id="5112f-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="5112f-104">您可以在 Azure 中建立虛擬機器 (Vm)，並附加多個網路介面 (Nic) tooeach 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="5112f-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="5112f-105">有多個 NIC 時，可透過各個 NIC 分隔不同的流量類型。</span><span class="sxs-lookup"><span data-stu-id="5112f-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="5112f-106">例如，一個 NIC 通訊 hello 網際網路，而另一個不只與內部資源通訊連接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="5112f-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="5112f-107">許多網路虛擬應用裝置，例如應用程式傳遞和 WAN 最佳化解決方案需要 hello 能力 tooseparate 跨多個 Nic 的網路流量。</span><span class="sxs-lookup"><span data-stu-id="5112f-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5112f-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="5112f-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5112f-109">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="5112f-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="5112f-110">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="5112f-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5112f-111">深入了解如何 tooperform 這些步驟使用 hello [Resource Manager 部署模型](virtual-network-deploy-multinic-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="5112f-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="5112f-112">hello 下列步驟使用的資源群組名稱為*IaaSStory* hello 網頁伺服器和資源群組名稱為*IaaSStory 後端*hello DB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5112f-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5112f-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="5112f-113">Prerequisites</span></span>
<span data-ttu-id="5112f-114">您可以建立 hello DB 伺服器之前，您需要 toocreate hello *IaaSStory*此案例中的 hello 必要資源與資源群組。</span><span class="sxs-lookup"><span data-stu-id="5112f-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="5112f-115">toocreate 這些資源，完成 hello 遵循的步驟。</span><span class="sxs-lookup"><span data-stu-id="5112f-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="5112f-116">建立虛擬網路中 hello 的 hello 步驟[建立虛擬網路](virtual-networks-create-vnet-classic-cli.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="5112f-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="5112f-117">部署 hello 後端 Vm</span><span class="sxs-lookup"><span data-stu-id="5112f-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="5112f-118">後端 Vm 相依於下列資源的 hello hello 建立 hello:</span><span class="sxs-lookup"><span data-stu-id="5112f-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="5112f-119">**資料磁碟的儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="5112f-119">**Storage account for data disks**.</span></span> <span data-ttu-id="5112f-120">為提升效能，hello hello 資料庫伺服器上的資料磁碟會使用固態硬碟 (SSD) 技術，需要進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5112f-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="5112f-121">請確定 hello 部署 toosupport 高階儲存體的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="5112f-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="5112f-122">**NIC**。</span><span class="sxs-lookup"><span data-stu-id="5112f-122">**NICs**.</span></span> <span data-ttu-id="5112f-123">每部 VM 都會有兩個 NIC，一個用於資料庫存取，另一個用於管理。</span><span class="sxs-lookup"><span data-stu-id="5112f-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="5112f-124">**可用性設定組**。</span><span class="sxs-lookup"><span data-stu-id="5112f-124">**Availability set**.</span></span> <span data-ttu-id="5112f-125">所有資料庫伺服器將會都加入 tooa 一個可用性設定組，其中至少一個 hello Vm tooensure 已啟動並執行在維護期間。</span><span class="sxs-lookup"><span data-stu-id="5112f-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="5112f-126">步驟 1：啟動指令碼</span><span class="sxs-lookup"><span data-stu-id="5112f-126">Step 1 - Start your script</span></span>
<span data-ttu-id="5112f-127">您可以下載 hello 完整 bash 指令碼使用[這裡](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh)。</span><span class="sxs-lookup"><span data-stu-id="5112f-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="5112f-128">完成下列步驟 toochange hello 指令碼 toowork 您環境中的 hello:</span><span class="sxs-lookup"><span data-stu-id="5112f-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="5112f-129">變更 hello hello 變數值以下根據您現有的資源群組，在上面部署[必要條件](#Prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="5112f-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="5112f-130">變更 hello 值 hello 變數的下列根據 hello 值要 toouse 後端部署。</span><span class="sxs-lookup"><span data-stu-id="5112f-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="5112f-131">步驟 2：為 VM 建立必要的資源</span><span class="sxs-lookup"><span data-stu-id="5112f-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="5112f-132">為所有後端 VM 建立新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5112f-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="5112f-133">請注意 hello 使用 hello `$backendCSName` hello 資源群組名稱 中的變數和`$location`hello Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="5112f-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="5112f-134">建立 hello OS 的進階儲存體帳戶和您的 Vm 所使用的資料磁碟 toobe。</span><span class="sxs-lookup"><span data-stu-id="5112f-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="5112f-135">步驟 3：建立具有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="5112f-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="5112f-136">啟動多個 Vm，根據 hello 迴圈 toocreate`numberOfVMs`變數。</span><span class="sxs-lookup"><span data-stu-id="5112f-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="5112f-137">針對每個 VM 中，指定 hello 名稱和每個 hello 兩個 Nic 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5112f-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="5112f-138">建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="5112f-138">Create hello VM.</span></span> <span data-ttu-id="5112f-139">請注意 hello 使用量的 hello`--nic-config`參數，其中包含所有 Nic 具有名稱、 子網路和 IP 位址的清單。</span><span class="sxs-lookup"><span data-stu-id="5112f-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="5112f-140">針對每個 VM，請建立兩個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="5112f-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="5112f-141">步驟 4-執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="5112f-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="5112f-142">既然您已下載並變更您的需求，執行 hello 指令碼 toocreate hello 備份為基礎的 hello 指令碼會結束資料庫具有多個 Nic 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="5112f-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="5112f-143">儲存您的指令碼並從 **Bash** 終端機執行。</span><span class="sxs-lookup"><span data-stu-id="5112f-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="5112f-144">您會看到 hello 初始輸出，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5112f-144">You will see hello initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="5112f-145">請稍候幾分鐘 hello 執行將結束，您會看到 hello 其餘 hello 輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="5112f-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
