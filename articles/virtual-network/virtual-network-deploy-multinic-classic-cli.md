---
title: "建立具有多個 NIC 的 VM (傳統) - Azure CLI 1.0 | Microsoft Docs"
description: "了解如何使用 Azure 命令列介面 (CLI) 1.0 建立具有多個 NIC 的 VM (傳統)。"
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
ms.openlocfilehash: b62421b7289650818748d0016dccfdf42ef0a768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="cc52e-103">使用 Azure CLI 1.0 建立具有多個 NIC 的 VM (傳統)</span><span class="sxs-lookup"><span data-stu-id="cc52e-103">Create a VM (Classic) with multiple NICs using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="cc52e-104">您可以在 Azure 中建立虛擬機器 (VM) 並將多個網路介面 (NIC) 連接至每個 VM。</span><span class="sxs-lookup"><span data-stu-id="cc52e-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="cc52e-105">有多個 NIC 時，可透過各個 NIC 分隔不同的流量類型。</span><span class="sxs-lookup"><span data-stu-id="cc52e-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="cc52e-106">例如，一個 NIC 可能與網際網路進行通訊，而另一個 NIC 則只與未連線到網際網路的內部資源進行通訊。</span><span class="sxs-lookup"><span data-stu-id="cc52e-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="cc52e-107">透過多個 NIC 分隔網路流量是許多網路虛擬設備 (例如應用程式交付和 WAN 最佳化解決方案) 所需的功能。</span><span class="sxs-lookup"><span data-stu-id="cc52e-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc52e-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="cc52e-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cc52e-109">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="cc52e-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="cc52e-110">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="cc52e-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="cc52e-111">了解如何使用 [Resource Manager 部署模型](virtual-network-deploy-multinic-arm-cli.md)執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="cc52e-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="cc52e-112">在下列步驟中，WEB 伺服器使用名為 *IaaSStory* 的資源群組，而 DB 伺服器使用名為 *IaaSStory-BackEnd* 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="cc52e-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc52e-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="cc52e-113">Prerequisites</span></span>
<span data-ttu-id="cc52e-114">您需要建立 *IaaSStory* 資源群組，其中含有此案例的所有必要資源，才能建立 DB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cc52e-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="cc52e-115">若要建立這些資源，請完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="cc52e-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="cc52e-116">依照[建立虛擬網路](virtual-networks-create-vnet-classic-cli.md)文章中的步驟建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="cc52e-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-the-back-end-vms"></a><span data-ttu-id="cc52e-117">部署後端 VM</span><span class="sxs-lookup"><span data-stu-id="cc52e-117">Deploy the back-end VMs</span></span>
<span data-ttu-id="cc52e-118">後端 VM 有賴於建立下列資源：</span><span class="sxs-lookup"><span data-stu-id="cc52e-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="cc52e-119">**資料磁碟的儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="cc52e-119">**Storage account for data disks**.</span></span> <span data-ttu-id="cc52e-120">為取得更佳的效能，資料庫伺服器上的資料磁碟會使用需要進階儲存體帳戶的固態硬碟 (SSD) 技術。</span><span class="sxs-lookup"><span data-stu-id="cc52e-120">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="cc52e-121">請確定 Azure 的部署位置，以支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="cc52e-121">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="cc52e-122">**NIC**。</span><span class="sxs-lookup"><span data-stu-id="cc52e-122">**NICs**.</span></span> <span data-ttu-id="cc52e-123">每部 VM 都會有兩個 NIC，一個用於資料庫存取，另一個用於管理。</span><span class="sxs-lookup"><span data-stu-id="cc52e-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="cc52e-124">**可用性設定組**。</span><span class="sxs-lookup"><span data-stu-id="cc52e-124">**Availability set**.</span></span> <span data-ttu-id="cc52e-125">所有的資料庫伺服器都會加入單一的可用性設定組，確保在維護期間至少有一部 VM 啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="cc52e-125">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="cc52e-126">步驟 1：啟動指令碼</span><span class="sxs-lookup"><span data-stu-id="cc52e-126">Step 1 - Start your script</span></span>
<span data-ttu-id="cc52e-127">[這裡](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh)可以下載所使用的完整 Bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="cc52e-127">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="cc52e-128">請完成下列步驟來變更指令碼，讓指令碼可在您的環境中運作：</span><span class="sxs-lookup"><span data-stu-id="cc52e-128">Complete the following steps to change the script to work in your environment:</span></span>

1. <span data-ttu-id="cc52e-129">根據上述 [必要條件](#Prerequisites)中已部署的現有資源群組來變更下列變數的值。</span><span class="sxs-lookup"><span data-stu-id="cc52e-129">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="cc52e-130">根據後端部署要使用的值，變更下列變數值。</span><span class="sxs-lookup"><span data-stu-id="cc52e-130">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="cc52e-131">步驟 2：為 VM 建立必要的資源</span><span class="sxs-lookup"><span data-stu-id="cc52e-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="cc52e-132">為所有後端 VM 建立新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="cc52e-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="cc52e-133">請注意，資源群組名稱的 `$backendCSName` 變數，以及 Azure 區域之 `$location` 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="cc52e-133">Notice the use of the `$backendCSName` variable for the resource group name, and `$location` for the Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="cc52e-134">為您的 VM 要使用的作業系統和資料磁碟建立進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc52e-134">Create a premium storage account for the OS and data disks to be used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="cc52e-135">步驟 3：建立具有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="cc52e-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="cc52e-136">根據 `numberOfVMs` 變數，啟動迴圈以建立多部 VM。</span><span class="sxs-lookup"><span data-stu-id="cc52e-136">Start a loop to create multiple VMs, based on the `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="cc52e-137">對於每個 VM，請分別為這兩個 NIC 的個別指定名稱和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cc52e-137">For each VM, specify the name and IP address of each of the two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="cc52e-138">建立 VM。</span><span class="sxs-lookup"><span data-stu-id="cc52e-138">Create the VM.</span></span> <span data-ttu-id="cc52e-139">請注意使用 `--nic-config` 參數，其中包含具有名稱、子網路和 IP 位址的所有 NIC 清單。</span><span class="sxs-lookup"><span data-stu-id="cc52e-139">Notice the usage of the `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

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

4. <span data-ttu-id="cc52e-140">針對每個 VM，請建立兩個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="cc52e-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="cc52e-141">步驟 4：執行指令碼</span><span class="sxs-lookup"><span data-stu-id="cc52e-141">Step 4 - Run the script</span></span>
<span data-ttu-id="cc52e-142">現在您已根據需求下載並變更了指令碼，請執行指令碼來建立具有多個 NIC 的後端資料庫 VM。</span><span class="sxs-lookup"><span data-stu-id="cc52e-142">Now that you downloaded and changed the script based on your needs, run the script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="cc52e-143">儲存您的指令碼並從 **Bash** 終端機執行。</span><span class="sxs-lookup"><span data-stu-id="cc52e-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="cc52e-144">您會看到初始的輸出，如下所示。</span><span class="sxs-lookup"><span data-stu-id="cc52e-144">You will see the initial output, as shown below.</span></span>

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

2. <span data-ttu-id="cc52e-145">幾分鐘後，執行將會結束，且您將會看到其餘的輸出，如下所示。</span><span class="sxs-lookup"><span data-stu-id="cc52e-145">After a few minutes, the execution will end and you will see the rest of the output as shown below.</span></span>

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
