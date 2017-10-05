---
title: "建立具有多個 NIC 的 VM - Azure CLI 1.0 | Microsoft Docs"
description: "了解如何使用 Azure CLI 1.0 建立具有多個 NIC 的 VM。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b95bcb38664718bf25ec6981c803415790c6da3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="8a1fe-103">使用 Azure CLI 1.0 建立具有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="8a1fe-103">Create a VM with multiple NICs using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="8a1fe-104">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8a1fe-105">本文涵蓋內容包括使用 Resource Manager 部署模型，Microsoft 建議大部分的新部署使用此模型，而不是[傳統部署模型](virtual-network-deploy-multinic-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="8a1fe-106">在下列步驟中，WEB 伺服器使用名為 *IaaSStory* 的資源群組，而 DB 伺服器使用名為 *IaaSStory-BackEnd* 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span> <span data-ttu-id="8a1fe-107">您可以使用 Azure CLI 1.0 (本文) 或 [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md) 完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-107">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="8a1fe-108">後續步驟所含變數之 "" 中的值，會使用案例中的設定建立資源。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-108">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="8a1fe-109">請針對您的環境適當地變更值。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-109">Change the values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a1fe-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8a1fe-110">Prerequisites</span></span>
<span data-ttu-id="8a1fe-111">您需要建立 *IaaSStory* 資源群組，其中含有此案例的所有必要資源，才能建立 DB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-111">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="8a1fe-112">若要建立這些資源，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8a1fe-112">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="8a1fe-113">瀏覽至 [範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-113">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="8a1fe-114">在範本頁面中，按一下 [父資源群組] 右邊的 [部署至 Azure]。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-114">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="8a1fe-115">視需要變更參數值，然後依照 Azure Preview 入口網站中的步驟部署資源群組。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-115">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a1fe-116">請確定您的儲存體帳戶名稱是唯一的。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="8a1fe-117">在 Auzre 中不能有重複的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="8a1fe-118">建立後端 VM</span><span class="sxs-lookup"><span data-stu-id="8a1fe-118">Create the back-end VMs</span></span>
<span data-ttu-id="8a1fe-119">後端 VM 有賴於建立下列資源：</span><span class="sxs-lookup"><span data-stu-id="8a1fe-119">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="8a1fe-120">**資料磁碟的儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-120">**Storage account for data disks**.</span></span> <span data-ttu-id="8a1fe-121">為取得更佳的效能，資料庫伺服器上的資料磁碟會使用需要進階儲存體帳戶的固態硬碟 (SSD) 技術。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-121">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="8a1fe-122">請確定 Azure 的部署位置，以支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-122">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="8a1fe-123">**NIC**。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-123">**NICs**.</span></span> <span data-ttu-id="8a1fe-124">每部 VM 都會有兩個 NIC，一個用於資料庫存取，另一個用於管理。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="8a1fe-125">**可用性設定組**。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-125">**Availability set**.</span></span> <span data-ttu-id="8a1fe-126">所有的資料庫伺服器都會加入單一的可用性設定組，確保在維護期間至少有一部 VM 啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="8a1fe-127">步驟 1：啟動指令碼</span><span class="sxs-lookup"><span data-stu-id="8a1fe-127">Step 1 - Start your script</span></span>
<span data-ttu-id="8a1fe-128">[這裡](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh)可以下載所使用的完整 Bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-128">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="8a1fe-129">請遵循下列步驟來變更指令碼來讓指令碼在環境中運作。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="8a1fe-130">根據上述 [必要條件](#Prerequisites)中已部署的現有資源群組來變更下列變數的值。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="8a1fe-131">根據後端部署要使用的值，變更下列變數值。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```azurecli
    backendRGName="IaaSStory-Backend"
    prmStorageAccountName="wtestvnetstorageprm"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    publisher="Canonical"
    offer="UbuntuServer"
    sku="14.04.2-LTS"
    version="latest"
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskName="datadisk"
    nicNamePrefix="NICDB"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

3. <span data-ttu-id="8a1fe-132">擷取將在其中建立 VM 之 `BackEnd` 子網路的識別碼。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-132">Retrieve the ID for the `BackEnd` subnet where the VMs will be created.</span></span> <span data-ttu-id="8a1fe-133">您需要這麼做，因為要和這個子網路關聯的 NIC 位於不同的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-133">You need to do this since the NICs to be associated to this subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="8a1fe-134">上述的第一個命令會使用 [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) 和[字串操作](http://tldp.org/LDP/abs/html/string-manipulation.html) (更具體來說，是子字串移除)。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-134">The first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="8a1fe-135">擷取 `NSG-RemoteAccess` NSG 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-135">Retrieve the ID for the `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="8a1fe-136">您需要這麼做，因為要和這個 NSG 關聯的 NIC 位於不同的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-136">You need to do this since the NICs to be associated to this NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="8a1fe-137">步驟 2：為 VM 建立必要的資源</span><span class="sxs-lookup"><span data-stu-id="8a1fe-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="8a1fe-138">為所有後端資源建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="8a1fe-139">請注意，資員群組名稱的 `$backendRGName` 變數，以及 Azure 區域之 `$location` 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-139">Notice the use of the `$backendRGName` variable for the resource group name, and `$location` for the Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="8a1fe-140">為您的 VM 要使用的作業系統和資料磁碟建立進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-140">Create a premium storage account for the OS and data disks to be used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="8a1fe-141">為 VM 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-141">Create an availability set for the VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-the-nics-and-back-end-vms"></a><span data-ttu-id="8a1fe-142">步驟 3：建立 NIC 和後端 VM</span><span class="sxs-lookup"><span data-stu-id="8a1fe-142">Step 3 - Create the NICs and back-end VMs</span></span>

1. <span data-ttu-id="8a1fe-143">根據 `numberOfVMs` 變數，啟動迴圈以建立多部 VM。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-143">Start a loop to create multiple VMs, based on the `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="8a1fe-144">針對每部 VM，建立 NIC 以用於資料庫存取。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-144">For each VM, create a NIC for database access.</span></span>

    ```azurecli
    nic1Name=$nicNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x
    azure network nic create --name $nic1Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress1 \
        --subnet-id $subnetId
    ```

3. <span data-ttu-id="8a1fe-145">針對每部 VM，建立 NIC 以用於遠端存取。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="8a1fe-146">請注意用於關聯 NIC 與 NSG 的 `--network-security-group` 參數。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-146">Notice the `--network-security-group` parameter, used to associate the NIC to an NSG.</span></span>

    ```azurecli
    nic2Name=$nicNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    azure network nic create --name $nic2Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress2 \
        --subnet-id $subnetId $vnetName \
        --network-security-group-id $nsgId
    ```

4. <span data-ttu-id="8a1fe-147">建立 VM。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-147">Create the VM.</span></span>

    ```azurecli
    azure vm create --resource-group $backendRGName \
        --name $vmNamePrefix$suffixNumber \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --availset-name $avSetName \
        --nic-names $nic1Name,$nic2Name \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName$suffixNumber.vhd \
        --admin-username $username \
        --admin-password $password
    ```

5. <span data-ttu-id="8a1fe-148">針對每部 VM，建立兩個資料磁碟，並使用 `done` 命令結束迴圈。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-148">For each VM, create two data disks, and end the loop with the `done` command.</span></span>

    ```azurecli
    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-1.vhd \
        --size-in-gb $diskSize \
        --lun 0

    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \        
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-2.vhd \
        --size-in-gb $diskSize \
        --lun 1
        done
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="8a1fe-149">步驟 4：執行指令碼</span><span class="sxs-lookup"><span data-stu-id="8a1fe-149">Step 4 - Run the script</span></span>
<span data-ttu-id="8a1fe-150">現在您已根據需求下載並變更了指令碼，請執行指令碼來建立具有多個 NIC 的後端資料庫 VM。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-150">Now that you downloaded and changed the script based on your needs, run the script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="8a1fe-151">儲存您的指令碼並從 **Bash** 終端機執行。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="8a1fe-152">您會看到初始的輸出，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-152">You will see the initial output, as shown below.</span></span>
   
        info:    Executing command group create
        info:    Getting resource group IaaSStory-Backend
        info:    Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command availset create
        info:    Looking up the availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up the network interface "NICDB1-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-DA
        data:    Name                            : NICDB1-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up the network interface "NICDB1-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-RA
        data:    Name                            : NICDB1-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.54
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up the VM "DB1"
        info:    Using the VM Size "Standard_DS3"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account wtestvnetstorageprm
        info:    Looking up the availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up the NIC "NICDB1-DA"
        info:    Looking up the NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="8a1fe-153">幾分鐘後，執行將會結束，且您將會看到其餘的輸出，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8a1fe-153">After a few minutes, the execution will end and you will see the rest of the output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB1"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB1"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up the network interface "NICDB2-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-DA
        data:    Name                            : NICDB2-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.5
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up the network interface "NICDB2-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-RA
        data:    Name                            : NICDB2-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.55
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up the VM "DB2"
        info:    Using the VM Size "Standard_DS3"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account wtestvnetstorageprm
        info:    Looking up the availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up the NIC "NICDB2-DA"
        info:    Looking up the NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB2"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB2"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

