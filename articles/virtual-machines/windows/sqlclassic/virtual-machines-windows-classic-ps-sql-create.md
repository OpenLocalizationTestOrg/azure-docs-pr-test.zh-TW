---
title: "以 Azure PowerShell 建立 SQL Server 虛擬機器 (傳統) | Microsoft Docs"
description: "提供使用 SQL Server 虛擬機器資源庫映像建立 Azure VM 的步驟和 PowerShell 指令碼。 本主題使用傳統部署模式。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: c3bd4329e8a22ce8503d6593560d29c2a3135e83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="3fd5c-104">使用 Azure PowerShell 佈建 SQL Server 虛擬機器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="3fd5c-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="3fd5c-105">這篇文章提供如何使用 PowerShell Cmdlet 在 Azure 中建立 SQL Server 虛擬機器的步驟。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-105">This article provides steps for how to create a SQL Server virtual machine in Azure by using the PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3fd5c-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3fd5c-107">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="3fd5c-108">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="3fd5c-109">如果您需要本主題的 Resource Manager 版本，請參閱 [使用 Azure PowerShell Resource Manager 佈建 SQL Server 虛擬機器](../sql/virtual-machines-windows-ps-sql-create.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-109">For the Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="3fd5c-110">安裝並設定 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="3fd5c-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="3fd5c-111">如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="3fd5c-112">[下載及安裝最新的 Azure PowerShell 命令](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-112">[Download and install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="3fd5c-113">啟動 Windows PowerShell，然後使用 **Add-AzureAccount** 命令將它與您的 Azure 訂用帳戶連線。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-113">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="3fd5c-114">決定您的目標 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="3fd5c-114">Determine your target Azure region</span></span>

<span data-ttu-id="3fd5c-115">您的 SQL Server 虛擬機器將託管於存放在特定 Azure 區域的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="3fd5c-116">下列步驟可協助您決定將用於本教學課程其餘部分的服務區域、儲存體帳戶和雲端服務。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-116">The following steps help you to determine your region, storage account, and cloud service that will be used for the rest of the tutorial.</span></span>

1. <span data-ttu-id="3fd5c-117">決定您想要用來託管 SQL Server VM 的資料中心。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-117">Determine the data center that you want to use to host your SQL Server VM.</span></span> <span data-ttu-id="3fd5c-118">下列 PowerShell 命令會顯示可用區域名稱清單。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-118">The following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="3fd5c-119">找到您偏好的位置後，請設定一個名為 **$dcLocation** 的變數至該區域。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-119">Once you've identified your preferred location, set a variable named **$dcLocation** to that region.</span></span> <span data-ttu-id="3fd5c-120">例如，下列命令會將區域設定成「美國東部」：</span><span class="sxs-lookup"><span data-stu-id="3fd5c-120">For example, the following command sets the region to "East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="3fd5c-121">設定您的訂閱和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3fd5c-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="3fd5c-122">決定您將用於新虛擬機器的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-122">Determine the Azure subscription you will use for the new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="3fd5c-123">將您的目標 Azure 訂用帳戶指派至 **$subscr** 變數。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-123">Assign your target Azure subscription to the **$subscr** variable.</span></span> <span data-ttu-id="3fd5c-124">然後將此設為目前的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="3fd5c-125">然後檢查現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="3fd5c-126">下列指令碼會顯示存在於您所選擇區域中的所有儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="3fd5c-126">The following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="3fd5c-127">如果您需要新的儲存體帳戶，請先使用 New-AzureStorageAccount 命令建立全部小寫的儲存體帳戶名稱，如下列範例所示：`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="3fd5c-127">If you require a new storage account, first create an all-lower-case storage account name with the New-AzureStorageAccount command as in the following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="3fd5c-128">將目標儲存體帳戶名稱指派至 **$staccount**。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-128">Assign the target storage account name to the **$staccount**.</span></span> <span data-ttu-id="3fd5c-129">接著，使用 **Set-AzureSubscription** 設定訂用帳戶和目前的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-129">Then use **Set-AzureSubscription** to set the subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="3fd5c-130">選取 SQL Server 虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="3fd5c-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="3fd5c-131">了解 SQL Server 虛擬機器映像庫的可用清單。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-131">Find out the list of available SQL Server virtual machines images from the gallery.</span></span> <span data-ttu-id="3fd5c-132">這些映像都有以「SQL」開頭的 **ImageFamily** 屬性。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="3fd5c-133">下列查詢會顯示可供使用且已預先安裝 SQL Server 的映像系列。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-133">The following query displays the image family available to you that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="3fd5c-134">當您找到虛擬機器映像系列時，此系列中可能有多個已發佈的映像。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-134">When you find the  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="3fd5c-135">使用下列指令碼尋找您所選映像系列中最新發佈的虛擬機器映像名稱 (例如 **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**)：</span><span class="sxs-lookup"><span data-stu-id="3fd5c-135">Use the following script to find the latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-the-virtual-machine"></a><span data-ttu-id="3fd5c-136">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="3fd5c-136">Create the virtual machine</span></span>

<span data-ttu-id="3fd5c-137">最後，使用 PowerShell 建立虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="3fd5c-137">Finally, create the virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="3fd5c-138">建立雲端服務來裝載新的 VM。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-138">Create a cloud service to host the new VM.</span></span> <span data-ttu-id="3fd5c-139">請注意，您也可以使用現有的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-139">Note that it is also possible to use an existing cloud service instead.</span></span> <span data-ttu-id="3fd5c-140">建立新的變數 **$svcname** ，並以雲端服務的簡短名稱命名。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-140">Create a new variable **$svcname** with the short name of the cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="3fd5c-141">指定虛擬機器名稱和大小。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-141">Specify the virtual machine name and a size.</span></span> <span data-ttu-id="3fd5c-142">如需關於虛擬機器大小的詳細資訊，請參閱 [Azure 的虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see the link to the other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="3fd5c-143">指定本機系統管理員帳戶與密碼。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-143">Specify the local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type the name and password of the local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="3fd5c-144">執行下列指令碼來建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-144">Run the following script to create the virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="3fd5c-145">如需其他說明及組態選項，請參閱 **使用 Azure PowerShell 建立和預先設定以 Windows 為基礎的虛擬機器** 中的 [建置命令集](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)一節。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-145">For additional explanation and configuration options, see the **Build your command set** section in [Use Azure PowerShell to create and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="3fd5c-146">PowerShell 指令碼範例</span><span class="sxs-lookup"><span data-stu-id="3fd5c-146">Example PowerShell script</span></span>

<span data-ttu-id="3fd5c-147">下列指令碼提供可建立 **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** 虛擬機器的完整指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-147">The following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="3fd5c-148">如果您使用這個指令碼，您必須根據本主題中先前步驟來自訂初始變數。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-148">If you use this script, you must customize the initial variables based on the previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set the current subscription and storage account
# Comment out the New-AzureStorageAccount line if the account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select the most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create the new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create the VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type the name and password of the local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create the SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="3fd5c-149">使用遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="3fd5c-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="3fd5c-150">在目前使用者的文件資料夾中建立 RDP 檔案以啟動這些虛擬機器並完成安裝：</span><span class="sxs-lookup"><span data-stu-id="3fd5c-150">Create the RDP files in the current user's document folder to launch these virtual machines to complete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="3fd5c-151">在文件目錄中，啟動 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-151">In the documents directory, launch the RDP file.</span></span> <span data-ttu-id="3fd5c-152">連接先前提供的管理員使用者名稱與密碼 (例如，如果您的使用者名稱是 VMAdmin，請指定「\VMAdmin」為使用者並提供密碼)。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-152">Connect with the administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as the user and provide the password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-the-configuration-of-the-sql-server-machine-for-remote-access"></a><span data-ttu-id="3fd5c-153">完成 SQL Server Machine 的遠端存取組態設定</span><span class="sxs-lookup"><span data-stu-id="3fd5c-153">Complete the configuration of the SQL Server Machine for remote access</span></span>

<span data-ttu-id="3fd5c-154">透過遠端桌面登入該機器之後，根據 [Azure VM 中設定 SQL Server 連線的步驟](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)內的指示設定 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-154">After logging on to the machine with remote desktop, configure SQL Server based on the instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fd5c-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fd5c-155">Next steps</span></span>

<span data-ttu-id="3fd5c-156">您可以在 [虛擬機器文件](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)中找到其他使用 PowerShell 佈建虛擬機器的指示。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-156">You can find additional instructions for provisioning virtual machines with PowerShell in the [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="3fd5c-157">在許多情況下下，下一個步驟是將資料庫移轉到這個新的 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-157">In many cases, the next step is to migrate your databases to this new SQL Server VM.</span></span> <span data-ttu-id="3fd5c-158">如需資料庫移轉的指引，請參閱 [將資料庫移轉至 Azure VM 上的 SQL Server](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-158">For database migration guidance, see [Migrating a Database to SQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="3fd5c-159">如果您也想了解如何使用 Azure 入口網站建立 SQL 虛擬機器，請參閱 [在 Azure 入口網站中佈建 SQL Server 虛擬機器](../sql/virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-159">If you're also interested in using the Azure portal to create SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="3fd5c-160">請注意，本教學課程將逐步說明從入口網站利用建議的資源管理員模型建立 VM，而不是利用本 PowerShell 主題中所使用的傳統模型建立 VM。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-160">Note that the tutorial that walks you through the portal creates VMs using the recommended Resource Manager model, rather than the classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="3fd5c-161">除了上述資源，我們也建議您檢閱 [在 Azure 虛擬機器中執行 SQL Server 的其他相關主題](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd5c-161">In addition to these resources, we recommend that you review [other topics related to running SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
