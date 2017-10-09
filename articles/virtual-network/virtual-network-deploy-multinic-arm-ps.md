---
title: "具有多個 Nic 的 Azure PowerShell 的 VM aaaCreate |Microsoft 文件"
description: "深入了解如何 toocreate 具有使用 PowerShell 將多個 Nic 的 VM。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="0165a-103">使用 PowerShell 建立具有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="0165a-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0165a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0165a-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="0165a-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0165a-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="0165a-106">範本</span><span class="sxs-lookup"><span data-stu-id="0165a-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="0165a-107">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="0165a-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="0165a-108">Azure CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="0165a-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="0165a-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="0165a-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="0165a-110">本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](virtual-network-deploy-multinic-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="0165a-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="0165a-111">hello 下列步驟使用的資源群組名稱為*IaaSStory* hello 網頁伺服器和資源群組名稱為*IaaSStory 後端*hello DB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0165a-111">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0165a-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="0165a-112">Prerequisites</span></span>
<span data-ttu-id="0165a-113">您可以建立 hello DB 伺服器之前，您需要 toocreate hello *IaaSStory*此案例中的 hello 必要資源與資源群組。</span><span class="sxs-lookup"><span data-stu-id="0165a-113">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="0165a-114">toocreate 這些資源，完成下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="0165a-114">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="0165a-115">瀏覽過[hello 範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)。</span><span class="sxs-lookup"><span data-stu-id="0165a-115">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="0165a-116">在 hello 範本頁面中，右邊 toohello**父資源群組**，按一下 **部署 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="0165a-116">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="0165a-117">如有需要變更為 hello 參數值，然後遵循 hello hello Azure 預覽入口網站 toodeploy hello 資源群組中的步驟。</span><span class="sxs-lookup"><span data-stu-id="0165a-117">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0165a-118">請確定您的儲存體帳戶名稱是唯一的。</span><span class="sxs-lookup"><span data-stu-id="0165a-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="0165a-119">在 Auzre 中不能有重複的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="0165a-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="0165a-120">後端 Vm 建立 hello</span><span class="sxs-lookup"><span data-stu-id="0165a-120">Create hello back-end VMs</span></span>
<span data-ttu-id="0165a-121">後端 Vm 相依於下列資源的 hello hello 建立 hello:</span><span class="sxs-lookup"><span data-stu-id="0165a-121">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="0165a-122">**資料磁碟的儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="0165a-122">**Storage account for data disks**.</span></span> <span data-ttu-id="0165a-123">為提升效能，hello hello 資料庫伺服器上的資料磁碟會使用固態硬碟 (SSD) 技術，需要進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0165a-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="0165a-124">請確定 hello 部署 toosupport 高階儲存體的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="0165a-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="0165a-125">**NIC**。</span><span class="sxs-lookup"><span data-stu-id="0165a-125">**NICs**.</span></span> <span data-ttu-id="0165a-126">每部 VM 都會有兩個 NIC，一個用於資料庫存取，另一個用於管理。</span><span class="sxs-lookup"><span data-stu-id="0165a-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="0165a-127">**可用性設定組**。</span><span class="sxs-lookup"><span data-stu-id="0165a-127">**Availability set**.</span></span> <span data-ttu-id="0165a-128">所有資料庫伺服器將會都加入 tooa 一個可用性設定組，其中至少一個 hello Vm tooensure 已啟動並執行在維護期間。</span><span class="sxs-lookup"><span data-stu-id="0165a-128">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="0165a-129">步驟 1：啟動指令碼</span><span class="sxs-lookup"><span data-stu-id="0165a-129">Step 1 - Start your script</span></span>
<span data-ttu-id="0165a-130">您可以下載用 hello 完整 PowerShell 指令碼[這裡](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1)。</span><span class="sxs-lookup"><span data-stu-id="0165a-130">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="0165a-131">請遵循下列 toochange hello 指令碼 toowork 您環境中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="0165a-131">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="0165a-132">變更 hello hello 變數值以下根據您現有的資源群組，在上面部署[必要條件](#Prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="0165a-132">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="0165a-133">變更 hello 值 hello 變數的下列根據 hello 值要 toouse 後端部署。</span><span class="sxs-lookup"><span data-stu-id="0165a-133">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="0165a-134">擷取您的部署所需的 hello 現有資源。</span><span class="sxs-lookup"><span data-stu-id="0165a-134">Retrieve hello existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="0165a-135">步驟 2：為 VM 建立必要的資源</span><span class="sxs-lookup"><span data-stu-id="0165a-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="0165a-136">您需要 toocreate 新資源群組、 hello 資料磁碟的儲存體帳戶，而且所有 Vm 的可用性都集合。</span><span class="sxs-lookup"><span data-stu-id="0165a-136">You need toocreate a new resource group, a storage account for hello data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="0165a-137">您 alos 需要每個 VM hello 本機系統管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="0165a-137">You alos need hello local administrator account credentials for each VM.</span></span> <span data-ttu-id="0165a-138">toocreate 這些資源，執行下列步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="0165a-138">toocreate these resources, execute hello following steps.</span></span>

1. <span data-ttu-id="0165a-139">建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0165a-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="0165a-140">在上面所建立的 hello 資源群組中建立新的進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0165a-140">Create a new premium storage account in hello resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="0165a-141">建立新的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="0165a-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="0165a-142">收到 hello 本機系統管理員帳戶認證 toobe 用於每個 VM。</span><span class="sxs-lookup"><span data-stu-id="0165a-142">Get hello local administrator account credentials toobe used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="0165a-143">步驟 3-建立 hello Nic 與後端 Vm</span><span class="sxs-lookup"><span data-stu-id="0165a-143">Step 3 - Create hello NICs and back-end VMs</span></span>
<span data-ttu-id="0165a-144">您需要 toouse 迴圈 toocreate 因為許多 Vm，並建立 hello 所需的 Nic 和 Vm hello 迴圈內。</span><span class="sxs-lookup"><span data-stu-id="0165a-144">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="0165a-145">toocreate hello Nic 和 Vm，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="0165a-145">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="0165a-146">啟動`for`迴圈 toorepeat hello 命令 toocreate VM 和兩個 Nic 如有必要，次數根據 hello hello 值`$numberOfVMs`變數。</span><span class="sxs-lookup"><span data-stu-id="0165a-146">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="0165a-147">建立的 hello NIC 用來進行資料庫存取。</span><span class="sxs-lookup"><span data-stu-id="0165a-147">Create hello NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="0165a-148">建立的 hello NIC 用於遠端存取。</span><span class="sxs-lookup"><span data-stu-id="0165a-148">Create hello NIC used for remote access.</span></span> <span data-ttu-id="0165a-149">請注意此 NIC 有相關聯的 NSG tooit 的方式。</span><span class="sxs-lookup"><span data-stu-id="0165a-149">Notice how this NIC has an NSG associated tooit.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="0165a-150">建立 `vmConfig` 物件。</span><span class="sxs-lookup"><span data-stu-id="0165a-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="0165a-151">每部 VM 建立兩個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="0165a-151">Create two data disks per VM.</span></span> <span data-ttu-id="0165a-152">請注意，hello 資料磁碟 hello 稍早建立的 premium 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="0165a-152">Notice that hello data disks are in hello premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="0165a-153">設定 hello 作業系統，以及用於 hello VM 映像 toobe。</span><span class="sxs-lookup"><span data-stu-id="0165a-153">Configure hello operating system, and image toobe used for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="0165a-154">新增 toohello 上面所建立的 hello 兩個 Nic`vmConfig`物件。</span><span class="sxs-lookup"><span data-stu-id="0165a-154">Add hello two NICs created above toohello `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="0165a-155">建立 hello 作業系統磁碟，並建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="0165a-155">Create hello OS disk and create hello VM.</span></span> <span data-ttu-id="0165a-156">請注意 hello`}`結束 hello`for`迴圈。</span><span class="sxs-lookup"><span data-stu-id="0165a-156">Notice hello `}` ending hello `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="0165a-157">步驟 4-執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="0165a-157">Step 4 - Run hello script</span></span>
<span data-ttu-id="0165a-158">既然您已下載並變更 hello 指令碼，根據您的需求，runt 他指令碼 toocreate hello 後端資料庫具有多個 Nic Vm。</span><span class="sxs-lookup"><span data-stu-id="0165a-158">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="0165a-159">儲存您的指令碼，並從 hello 執行**PowerShell**命令提示字元，或**PowerShell ISE**。</span><span class="sxs-lookup"><span data-stu-id="0165a-159">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="0165a-160">您會看到 hello 初始輸出，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0165a-160">You will see hello initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="0165a-161">請稍候幾分鐘，填寫 hello 認證提示，並按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="0165a-161">After a few minutes, fill out hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="0165a-162">以下的 hello 輸出代表單一 VM。</span><span class="sxs-lookup"><span data-stu-id="0165a-162">hello output below represents a single VM.</span></span> <span data-ttu-id="0165a-163">請注意 hello 整個程序所花費 8 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="0165a-163">Notice hello entire process took 8 minutes toocomplete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
