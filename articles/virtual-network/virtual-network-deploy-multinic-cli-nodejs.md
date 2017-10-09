---
title: "具有多個 Nic-Azure CLI 1.0 VM aaaCreate |Microsoft 文件"
description: "了解與使用多個 Nic VM toocreate hello Azure CLI 1.0 的方式。"
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
ms.openlocfilehash: 07c660b632bcdc004365a6f910ecf8a5c13cbc6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="369f7-103">建立與使用 Azure CLI 1.0 hello 的多個 Nic VM</span><span class="sxs-lookup"><span data-stu-id="369f7-103">Create a VM with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="369f7-104">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="369f7-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="369f7-105">本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](virtual-network-deploy-multinic-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="369f7-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="369f7-106">hello 下列步驟使用的資源群組名稱為*IaaSStory* hello 網頁伺服器和資源群組名稱為*IaaSStory 後端*hello DB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="369f7-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span> <span data-ttu-id="369f7-107">您可以完成這項工作中使用 Azure CLI 1.0 （即本文） hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="369f7-107">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="369f7-108">hello 中的值""hello 遵循的步驟中的 hello 變數被 hello 案例的設定建立資源。</span><span class="sxs-lookup"><span data-stu-id="369f7-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="369f7-109">變更為適用於您環境的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="369f7-109">Change hello values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="369f7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="369f7-110">Prerequisites</span></span>
<span data-ttu-id="369f7-111">您可以建立 hello DB 伺服器之前，您需要 toocreate hello *IaaSStory*此案例中的 hello 必要資源與資源群組。</span><span class="sxs-lookup"><span data-stu-id="369f7-111">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="369f7-112">toocreate 這些資源，完成下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="369f7-112">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="369f7-113">瀏覽過[hello 範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)。</span><span class="sxs-lookup"><span data-stu-id="369f7-113">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="369f7-114">在 hello 範本頁面中，右邊 toohello**父資源群組**，按一下 **部署 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="369f7-114">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="369f7-115">如有需要變更為 hello 參數值，然後遵循 hello hello Azure 預覽入口網站 toodeploy hello 資源群組中的步驟。</span><span class="sxs-lookup"><span data-stu-id="369f7-115">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="369f7-116">請確定您的儲存體帳戶名稱是唯一的。</span><span class="sxs-lookup"><span data-stu-id="369f7-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="369f7-117">在 Auzre 中不能有重複的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="369f7-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="369f7-118">後端 Vm 建立 hello</span><span class="sxs-lookup"><span data-stu-id="369f7-118">Create hello back-end VMs</span></span>
<span data-ttu-id="369f7-119">後端 Vm 相依於下列資源的 hello hello 建立 hello:</span><span class="sxs-lookup"><span data-stu-id="369f7-119">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="369f7-120">**資料磁碟的儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="369f7-120">**Storage account for data disks**.</span></span> <span data-ttu-id="369f7-121">為提升效能，hello hello 資料庫伺服器上的資料磁碟會使用固態硬碟 (SSD) 技術，需要進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="369f7-121">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="369f7-122">請確定 hello 部署 toosupport 高階儲存體的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="369f7-122">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="369f7-123">**NIC**。</span><span class="sxs-lookup"><span data-stu-id="369f7-123">**NICs**.</span></span> <span data-ttu-id="369f7-124">每部 VM 都會有兩個 NIC，一個用於資料庫存取，另一個用於管理。</span><span class="sxs-lookup"><span data-stu-id="369f7-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="369f7-125">**可用性設定組**。</span><span class="sxs-lookup"><span data-stu-id="369f7-125">**Availability set**.</span></span> <span data-ttu-id="369f7-126">所有資料庫伺服器將會都加入 tooa 一個可用性設定組，其中至少一個 hello Vm tooensure 已啟動並執行在維護期間。</span><span class="sxs-lookup"><span data-stu-id="369f7-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="369f7-127">步驟 1：啟動指令碼</span><span class="sxs-lookup"><span data-stu-id="369f7-127">Step 1 - Start your script</span></span>
<span data-ttu-id="369f7-128">您可以下載 hello 完整 bash 指令碼使用[這裡](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh)。</span><span class="sxs-lookup"><span data-stu-id="369f7-128">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="369f7-129">請遵循下列 toochange hello 指令碼 toowork 您環境中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="369f7-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="369f7-130">變更 hello hello 變數值以下根據您現有的資源群組，在上面部署[必要條件](#Prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="369f7-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="369f7-131">變更 hello 值 hello 變數的下列根據 hello 值要 toouse 後端部署。</span><span class="sxs-lookup"><span data-stu-id="369f7-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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

3. <span data-ttu-id="369f7-132">擷取 hello 識別碼 hello `BackEnd` hello Vm 將會建立子網路。</span><span class="sxs-lookup"><span data-stu-id="369f7-132">Retrieve hello ID for hello `BackEnd` subnet where hello VMs will be created.</span></span> <span data-ttu-id="369f7-133">您需要 toodo 此因為 hello Nic 相關聯的 toobe toothis 子網路是不同資源群組中。</span><span class="sxs-lookup"><span data-stu-id="369f7-133">You need toodo this since hello NICs toobe associated toothis subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="369f7-134">hello 第一個命令會使用上述[grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html)和[字串操作](http://tldp.org/LDP/abs/html/string-manipulation.html)（更具體來說，子字串移除項目）。</span><span class="sxs-lookup"><span data-stu-id="369f7-134">hello first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="369f7-135">擷取 hello 識別碼 hello `NSG-RemoteAccess` NSG。</span><span class="sxs-lookup"><span data-stu-id="369f7-135">Retrieve hello ID for hello `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="369f7-136">您需要 toodo 此因為 hello Nic toobe 關聯的 toothis NSG 是不同資源群組中。</span><span class="sxs-lookup"><span data-stu-id="369f7-136">You need toodo this since hello NICs toobe associated toothis NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="369f7-137">步驟 2：為 VM 建立必要的資源</span><span class="sxs-lookup"><span data-stu-id="369f7-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="369f7-138">為所有後端資源建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="369f7-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="369f7-139">請注意 hello 使用 hello `$backendRGName` hello 資源群組名稱 中的變數和`$location`hello Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="369f7-139">Notice hello use of hello `$backendRGName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="369f7-140">建立 hello OS 的進階儲存體帳戶和您的 Vm 所使用的資料磁碟 toobe。</span><span class="sxs-lookup"><span data-stu-id="369f7-140">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="369f7-141">建立可用性設定組 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="369f7-141">Create an availability set for hello VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="369f7-142">步驟 3-建立 hello Nic 與後端 Vm</span><span class="sxs-lookup"><span data-stu-id="369f7-142">Step 3 - Create hello NICs and back-end VMs</span></span>

1. <span data-ttu-id="369f7-143">啟動多個 Vm，根據 hello 迴圈 toocreate`numberOfVMs`變數。</span><span class="sxs-lookup"><span data-stu-id="369f7-143">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="369f7-144">針對每部 VM，建立 NIC 以用於資料庫存取。</span><span class="sxs-lookup"><span data-stu-id="369f7-144">For each VM, create a NIC for database access.</span></span>

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

3. <span data-ttu-id="369f7-145">針對每部 VM，建立 NIC 以用於遠端存取。</span><span class="sxs-lookup"><span data-stu-id="369f7-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="369f7-146">請注意 hello`--network-security-group`參數，使用的 tooassociate hello NIC tooan NSG。</span><span class="sxs-lookup"><span data-stu-id="369f7-146">Notice hello `--network-security-group` parameter, used tooassociate hello NIC tooan NSG.</span></span>

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

4. <span data-ttu-id="369f7-147">建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="369f7-147">Create hello VM.</span></span>

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

5. <span data-ttu-id="369f7-148">針對每個 VM，建立兩個資料磁碟和結束 hello 迴圈以 hello`done`命令。</span><span class="sxs-lookup"><span data-stu-id="369f7-148">For each VM, create two data disks, and end hello loop with hello `done` command.</span></span>

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

### <a name="step-4---run-hello-script"></a><span data-ttu-id="369f7-149">步驟 4-執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="369f7-149">Step 4 - Run hello script</span></span>
<span data-ttu-id="369f7-150">既然您已下載並變更您的需求，執行 hello 指令碼 toocreate hello 備份為基礎的 hello 指令碼會結束資料庫具有多個 Nic 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="369f7-150">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="369f7-151">儲存您的指令碼並從 **Bash** 終端機執行。</span><span class="sxs-lookup"><span data-stu-id="369f7-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="369f7-152">您會看到 hello 初始輸出，如下所示。</span><span class="sxs-lookup"><span data-stu-id="369f7-152">You will see hello initial output, as shown below.</span></span>
   
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
        info:    Looking up hello availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up hello network interface "NICDB1-DA"
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
        info:    Looking up hello network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up hello network interface "NICDB1-RA"
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
        info:    Looking up hello VM "DB1"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB1-DA"
        info:    Looking up hello NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="369f7-153">請稍候幾分鐘 hello 執行將結束，您會看到 hello 其餘 hello 輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="369f7-153">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up hello network interface "NICDB2-DA"
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
        info:    Looking up hello network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up hello network interface "NICDB2-RA"
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
        info:    Looking up hello VM "DB2"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB2-DA"
        info:    Looking up hello NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

