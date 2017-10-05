---
title: "建立具有多個 NIC 的 VM (傳統) - Azure PowerShell | Microsoft Docs"
description: "了解如何使用 PowerShell 建立具有多個 NIC 的 VM (傳統)。"
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
ms.openlocfilehash: 923d4817d96399fc423b0a89cbf88f8d397f1af0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="93933-103">使用 PowerShell 建立具有多個 NIC 的 VM (傳統)</span><span class="sxs-lookup"><span data-stu-id="93933-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="93933-104">您可以在 Azure 中建立虛擬機器 (VM) 並將多個網路介面 (NIC) 連接至每個 VM。</span><span class="sxs-lookup"><span data-stu-id="93933-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="93933-105">有多個 NIC 時，可透過各個 NIC 分隔不同的流量類型。</span><span class="sxs-lookup"><span data-stu-id="93933-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="93933-106">例如，一個 NIC 可能與網際網路進行通訊，而另一個 NIC 則只與未連線到網際網路的內部資源進行通訊。</span><span class="sxs-lookup"><span data-stu-id="93933-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="93933-107">透過多個 NIC 分隔網路流量是許多網路虛擬設備 (例如應用程式交付和 WAN 最佳化解決方案) 所需的功能。</span><span class="sxs-lookup"><span data-stu-id="93933-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93933-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="93933-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="93933-109">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="93933-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="93933-110">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="93933-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="93933-111">了解如何使用 [Resource Manager 部署模型](virtual-network-deploy-multinic-arm-ps.md)執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="93933-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="93933-112">在下列步驟中，WEB 伺服器使用名為 *IaaSStory* 的資源群組，而 DB 伺服器使用名為 *IaaSStory-BackEnd* 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="93933-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93933-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="93933-113">Prerequisites</span></span>

<span data-ttu-id="93933-114">您需要建立 *IaaSStory* 資源群組，其中含有此案例的所有必要資源，才能建立 DB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="93933-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="93933-115">若要建立這些資源，請完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="93933-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="93933-116">依照[建立虛擬網路](virtual-networks-create-vnet-classic-netcfg-ps.md)文章中的步驟建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93933-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="93933-117">建立後端 VM</span><span class="sxs-lookup"><span data-stu-id="93933-117">Create the back-end VMs</span></span>
<span data-ttu-id="93933-118">後端 VM 有賴於建立下列資源：</span><span class="sxs-lookup"><span data-stu-id="93933-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="93933-119">**後端子網路**。</span><span class="sxs-lookup"><span data-stu-id="93933-119">**Backend subnet**.</span></span> <span data-ttu-id="93933-120">資料庫伺服器會是另外的子網路的一部分，以隔離流量。</span><span class="sxs-lookup"><span data-stu-id="93933-120">The database servers will be part of a separate subnet, to segregate traffic.</span></span> <span data-ttu-id="93933-121">下面的指令碼需要這個子網路位在名為 *WTestVnet*的 vnet 中。</span><span class="sxs-lookup"><span data-stu-id="93933-121">The script below expects this subnet to exist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="93933-122">**資料磁碟的儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="93933-122">**Storage account for data disks**.</span></span> <span data-ttu-id="93933-123">為取得更佳的效能，資料庫伺服器上的資料磁碟會使用需要進階儲存體帳戶的固態硬碟 (SSD) 技術。</span><span class="sxs-lookup"><span data-stu-id="93933-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="93933-124">請確定 Azure 的部署位置，以支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="93933-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="93933-125">**可用性設定組**。</span><span class="sxs-lookup"><span data-stu-id="93933-125">**Availability set**.</span></span> <span data-ttu-id="93933-126">所有的資料庫伺服器都會加入單一的可用性設定組，確保在維護期間至少有一部 VM 啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="93933-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="93933-127">步驟 1：啟動指令碼</span><span class="sxs-lookup"><span data-stu-id="93933-127">Step 1 - Start your script</span></span>
<span data-ttu-id="93933-128">[這裡](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1)可以下載所使用之完整的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="93933-128">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="93933-129">請遵循下列步驟來變更指令碼來讓指令碼在環境中運作。</span><span class="sxs-lookup"><span data-stu-id="93933-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="93933-130">根據上述 [必要條件](#Prerequisites)中已部署的現有資源群組來變更下列變數的值。</span><span class="sxs-lookup"><span data-stu-id="93933-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="93933-131">根據後端部署要使用的值，變更下列變數值。</span><span class="sxs-lookup"><span data-stu-id="93933-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="93933-132">步驟 2：為 VM 建立必要的資源</span><span class="sxs-lookup"><span data-stu-id="93933-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="93933-133">您需要為所有 VM 的資料磁碟建立新的雲端服務和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="93933-133">You need to create a new cloud service and a storage account for the data disks for all VMs.</span></span> <span data-ttu-id="93933-134">您也需要指定影像及 VM 的本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="93933-134">You also need to specify an image, and a local administrator account for the VMs.</span></span> <span data-ttu-id="93933-135">若要建立這些資源，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="93933-135">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="93933-136">建立新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="93933-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="93933-137">建立新的進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="93933-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="93933-138">設定前文中建立的儲存體帳戶，做為訂用帳戶的目前儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="93933-138">Set the storage account created above as the current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="93933-139">選取 VM 影像。</span><span class="sxs-lookup"><span data-stu-id="93933-139">Select an image for the VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="93933-140">設定本機系統管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="93933-140">Set the local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="93933-141">步驟 3：建立 VM</span><span class="sxs-lookup"><span data-stu-id="93933-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="93933-142">您需要使用迴圈建立所需數量的 VM，並在迴圈中建立必要的 NIC 和 VM。</span><span class="sxs-lookup"><span data-stu-id="93933-142">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="93933-143">若要建立 NIC 和 VM，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="93933-143">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="93933-144">啟動 `for` 迴圈，根據 `$numberOfVMs` 變數值，視需要的次數重複命令來建立一部 VM 和兩個 NIC。</span><span class="sxs-lookup"><span data-stu-id="93933-144">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="93933-145">建立指定 VM 影像、大小和可用性設定組的 `VMConfig` 物件。</span><span class="sxs-lookup"><span data-stu-id="93933-145">Create a `VMConfig` object specifying the image, size, and availability set for the VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="93933-146">將 VM 佈建為 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="93933-146">Provision the VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="93933-147">設定預設 NIC，並指派它一個靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93933-147">Set the default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="93933-148">為每部 VM 加入第二個 NIC。</span><span class="sxs-lookup"><span data-stu-id="93933-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="93933-149">為每部 VM 建立資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="93933-149">Create to data disks for each VM.</span></span>

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

7. <span data-ttu-id="93933-150">建立每部 VM 並結束迴圈。</span><span class="sxs-lookup"><span data-stu-id="93933-150">Create each VM, and end the loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="93933-151">步驟 4：執行指令碼</span><span class="sxs-lookup"><span data-stu-id="93933-151">Step 4 - Run the script</span></span>
<span data-ttu-id="93933-152">既然您已根據需求下載並變更指令碼，請執行指令碼來建立有多個 NIC 的後端資料庫 VM。</span><span class="sxs-lookup"><span data-stu-id="93933-152">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="93933-153">儲存您的指令碼，然後從 **PowerShell** 命令提示字元或 **PowerShell ISE** 執行它。</span><span class="sxs-lookup"><span data-stu-id="93933-153">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="93933-154">您會看到初始的輸出，如下所示。</span><span class="sxs-lookup"><span data-stu-id="93933-154">You will see the initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="93933-155">填寫認證提示中所需的資訊，並按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="93933-155">Fill out the information needed in the credentials prompt and click **OK**.</span></span> <span data-ttu-id="93933-156">會傳回以下的輸出。</span><span class="sxs-lookup"><span data-stu-id="93933-156">The output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
