---
title: "aaaCreate 具有多個 Nic 的 Azure PowerShell 的 VM （傳統） |Microsoft 文件"
description: "深入了解如何 toocreate 具有使用 PowerShell 將多個 Nic 的 VM （傳統）。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="ead09-103">使用 PowerShell 建立具有多個 NIC 的 VM (傳統)</span><span class="sxs-lookup"><span data-stu-id="ead09-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="ead09-104">您可以在 Azure 中建立虛擬機器 (Vm)，並附加多個網路介面 (Nic) tooeach 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="ead09-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="ead09-105">有多個 NIC 時，可透過各個 NIC 分隔不同的流量類型。</span><span class="sxs-lookup"><span data-stu-id="ead09-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="ead09-106">例如，一個 NIC 通訊 hello 網際網路，而另一個不只與內部資源通訊連接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="ead09-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="ead09-107">許多網路虛擬應用裝置，例如應用程式傳遞和 WAN 最佳化解決方案需要 hello 能力 tooseparate 跨多個 Nic 的網路流量。</span><span class="sxs-lookup"><span data-stu-id="ead09-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ead09-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ead09-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ead09-109">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="ead09-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="ead09-110">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="ead09-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ead09-111">深入了解如何 tooperform 這些步驟使用 hello [Resource Manager 部署模型](virtual-network-deploy-multinic-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="ead09-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="ead09-112">hello 下列步驟使用的資源群組名稱為*IaaSStory* hello 網頁伺服器和資源群組名稱為*IaaSStory 後端*hello DB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ead09-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ead09-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="ead09-113">Prerequisites</span></span>

<span data-ttu-id="ead09-114">您可以建立 hello DB 伺服器之前，您需要 toocreate hello *IaaSStory*此案例中的 hello 必要資源與資源群組。</span><span class="sxs-lookup"><span data-stu-id="ead09-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="ead09-115">toocreate 這些資源，完成 hello 遵循的步驟。</span><span class="sxs-lookup"><span data-stu-id="ead09-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="ead09-116">建立虛擬網路中 hello 的 hello 步驟[建立虛擬網路](virtual-networks-create-vnet-classic-netcfg-ps.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ead09-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="ead09-117">後端 Vm 建立 hello</span><span class="sxs-lookup"><span data-stu-id="ead09-117">Create hello back-end VMs</span></span>
<span data-ttu-id="ead09-118">後端 Vm 相依於下列資源的 hello hello 建立 hello:</span><span class="sxs-lookup"><span data-stu-id="ead09-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="ead09-119">**後端子網路**。</span><span class="sxs-lookup"><span data-stu-id="ead09-119">**Backend subnet**.</span></span> <span data-ttu-id="ead09-120">hello 資料庫伺服器都屬於不同的子網路，toosegregate 流量。</span><span class="sxs-lookup"><span data-stu-id="ead09-120">hello database servers will be part of a separate subnet, toosegregate traffic.</span></span> <span data-ttu-id="ead09-121">下列指令碼 hello 預期此子網路 tooexist 中名為 vnet *WTestVnet*。</span><span class="sxs-lookup"><span data-stu-id="ead09-121">hello script below expects this subnet tooexist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="ead09-122">**資料磁碟的儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="ead09-122">**Storage account for data disks**.</span></span> <span data-ttu-id="ead09-123">為提升效能，hello hello 資料庫伺服器上的資料磁碟會使用固態硬碟 (SSD) 技術，需要進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ead09-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="ead09-124">請確定 hello 部署 toosupport 高階儲存體的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="ead09-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="ead09-125">**可用性設定組**。</span><span class="sxs-lookup"><span data-stu-id="ead09-125">**Availability set**.</span></span> <span data-ttu-id="ead09-126">所有資料庫伺服器將會都加入 tooa 一個可用性設定組，其中至少一個 hello Vm tooensure 已啟動並執行在維護期間。</span><span class="sxs-lookup"><span data-stu-id="ead09-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="ead09-127">步驟 1：啟動指令碼</span><span class="sxs-lookup"><span data-stu-id="ead09-127">Step 1 - Start your script</span></span>
<span data-ttu-id="ead09-128">您可以下載用 hello 完整 PowerShell 指令碼[這裡](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1)。</span><span class="sxs-lookup"><span data-stu-id="ead09-128">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="ead09-129">請遵循下列 toochange hello 指令碼 toowork 您環境中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ead09-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="ead09-130">變更 hello hello 變數值以下根據您現有的資源群組，在上面部署[必要條件](#Prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="ead09-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="ead09-131">變更 hello 值 hello 變數的下列根據 hello 值要 toouse 後端部署。</span><span class="sxs-lookup"><span data-stu-id="ead09-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="ead09-132">步驟 2：為 VM 建立必要的資源</span><span class="sxs-lookup"><span data-stu-id="ead09-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="ead09-133">您需要新的雲端服務和儲存體帳戶的所有 vm hello 資料磁碟的 toocreate。</span><span class="sxs-lookup"><span data-stu-id="ead09-133">You need toocreate a new cloud service and a storage account for hello data disks for all VMs.</span></span> <span data-ttu-id="ead09-134">您也需要 toospecify 映像及本機系統管理員帳戶的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="ead09-134">You also need toospecify an image, and a local administrator account for hello VMs.</span></span> <span data-ttu-id="ead09-135">toocreate 這些資源，完成下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="ead09-135">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="ead09-136">建立新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="ead09-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="ead09-137">建立新的進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ead09-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="ead09-138">上面所建立與 hello 目前儲存體帳戶訂用帳戶集 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ead09-138">Set hello storage account created above as hello current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="ead09-139">選取 hello VM 映像。</span><span class="sxs-lookup"><span data-stu-id="ead09-139">Select an image for hello VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="ead09-140">設定 hello 本機系統管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="ead09-140">Set hello local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="ead09-141">步驟 3：建立 VM</span><span class="sxs-lookup"><span data-stu-id="ead09-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="ead09-142">您需要 toouse 迴圈 toocreate 因為許多 Vm，並建立 hello 所需的 Nic 和 Vm hello 迴圈內。</span><span class="sxs-lookup"><span data-stu-id="ead09-142">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="ead09-143">toocreate hello Nic 和 Vm，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="ead09-143">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="ead09-144">啟動`for`迴圈 toorepeat hello 命令 toocreate VM 和兩個 Nic 如有必要，次數根據 hello hello 值`$numberOfVMs`變數。</span><span class="sxs-lookup"><span data-stu-id="ead09-144">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="ead09-145">建立`VMConfig`指定 hello 映像、 大小和可用性設定組 hello VM 的物件。</span><span class="sxs-lookup"><span data-stu-id="ead09-145">Create a `VMConfig` object specifying hello image, size, and availability set for hello VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="ead09-146">佈建 hello 做為 Windows VM 的 VM。</span><span class="sxs-lookup"><span data-stu-id="ead09-146">Provision hello VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="ead09-147">設定 hello 預設 NIC，並將其指派靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ead09-147">Set hello default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="ead09-148">為每部 VM 加入第二個 NIC。</span><span class="sxs-lookup"><span data-stu-id="ead09-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="ead09-149">每個 VM 建立 toodata 磁碟。</span><span class="sxs-lookup"><span data-stu-id="ead09-149">Create toodata disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="ead09-150">建立每個 VM，以及結束 hello 迴圈。</span><span class="sxs-lookup"><span data-stu-id="ead09-150">Create each VM, and end hello loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="ead09-151">步驟 4-執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="ead09-151">Step 4 - Run hello script</span></span>
<span data-ttu-id="ead09-152">既然您已下載並變更 hello 指令碼，根據您的需求，runt 他指令碼 toocreate hello 後端資料庫具有多個 Nic Vm。</span><span class="sxs-lookup"><span data-stu-id="ead09-152">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="ead09-153">儲存您的指令碼，並從 hello 執行**PowerShell**命令提示字元，或**PowerShell ISE**。</span><span class="sxs-lookup"><span data-stu-id="ead09-153">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="ead09-154">您會看到 hello 初始輸出，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ead09-154">You will see hello initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="ead09-155">填寫在 hello 認證提示，並按一下所需的 hello 資訊**確定**。</span><span class="sxs-lookup"><span data-stu-id="ead09-155">Fill out hello information needed in hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="ead09-156">會傳回以下 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="ead09-156">hello output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
