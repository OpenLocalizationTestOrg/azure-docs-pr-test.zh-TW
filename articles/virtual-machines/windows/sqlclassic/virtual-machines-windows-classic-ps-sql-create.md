---
title: "在 Azure PowerShell （傳統） 中的 SQL Server 虛擬機器 aaaCreate |Microsoft 文件"
description: "提供使用 SQL Server 虛擬機器資源庫映像建立 Azure VM 的步驟和 PowerShell 指令碼。 本主題使用 hello 傳統部署模式。"
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
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="a318b-104">使用 Azure PowerShell 佈建 SQL Server 虛擬機器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="a318b-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="a318b-105">這篇文章提供如何在 Azure 中使用 SQL Server 虛擬機器 toocreate hello PowerShell 指令程式的步驟。</span><span class="sxs-lookup"><span data-stu-id="a318b-105">This article provides steps for how toocreate a SQL Server virtual machine in Azure by using hello PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a318b-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="a318b-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a318b-107">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="a318b-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a318b-108">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="a318b-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="a318b-109">本主題的 hello 資源管理員版本，請參閱[佈建 SQL Server 虛擬機器使用 Azure PowerShell 資源管理員](../sql/virtual-machines-windows-ps-sql-create.md)。</span><span class="sxs-lookup"><span data-stu-id="a318b-109">For hello Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="a318b-110">安裝並設定 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="a318b-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="a318b-111">如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a318b-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="a318b-112">[下載並安裝最新 Azure PowerShell 命令 hello](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a318b-112">[Download and install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="a318b-113">啟動 Windows PowerShell，並將它連接 tooyour Azure 訂用帳戶以 hello **Add-azureaccount**命令。</span><span class="sxs-lookup"><span data-stu-id="a318b-113">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="a318b-114">決定您的目標 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="a318b-114">Determine your target Azure region</span></span>

<span data-ttu-id="a318b-115">您的 SQL Server 虛擬機器將託管於存放在特定 Azure 區域的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="a318b-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="a318b-116">hello 下列步驟幫助您 toodetermine 您地區、 儲存體帳戶和雲端服務，用於 hello hello 教學課程的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="a318b-116">hello following steps help you toodetermine your region, storage account, and cloud service that will be used for hello rest of hello tutorial.</span></span>

1. <span data-ttu-id="a318b-117">決定您想 toouse toohost SQL Server VM 的 hello 資料中心。</span><span class="sxs-lookup"><span data-stu-id="a318b-117">Determine hello data center that you want toouse toohost your SQL Server VM.</span></span> <span data-ttu-id="a318b-118">hello 下列 PowerShell 命令會顯示一份可用的地區名稱。</span><span class="sxs-lookup"><span data-stu-id="a318b-118">hello following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="a318b-119">一旦您已經識別您想要的位置，設定變數，名為**$dcLocation** toothat 區域。</span><span class="sxs-lookup"><span data-stu-id="a318b-119">Once you've identified your preferred location, set a variable named **$dcLocation** toothat region.</span></span> <span data-ttu-id="a318b-120">比方說，hello 下列命令集 hello 區太 「 美國東部":</span><span class="sxs-lookup"><span data-stu-id="a318b-120">For example, hello following command sets hello region too"East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="a318b-121">設定您的訂閱和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a318b-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="a318b-122">判斷 hello hello 新虛擬機器，您將使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a318b-122">Determine hello Azure subscription you will use for hello new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="a318b-123">指定您的目標 Azure 訂用帳戶 toohello **$subscr**變數。</span><span class="sxs-lookup"><span data-stu-id="a318b-123">Assign your target Azure subscription toohello **$subscr** variable.</span></span> <span data-ttu-id="a318b-124">然後將此設為目前的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a318b-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="a318b-125">然後檢查現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a318b-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="a318b-126">hello 下列指令碼會顯示存在於您所選擇的地區中的所有儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="a318b-126">hello following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="a318b-127">如果您需要新的儲存體帳戶，請先使用如 hello 下列範例所示的 hello 新增 AzureStorageAccount 命令建立全部小寫的儲存體帳戶名稱：`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="a318b-127">If you require a new storage account, first create an all-lower-case storage account name with hello New-AzureStorageAccount command as in hello following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="a318b-128">指派 hello 目標儲存體帳戶名稱 toohello **$staccount**。</span><span class="sxs-lookup"><span data-stu-id="a318b-128">Assign hello target storage account name toohello **$staccount**.</span></span> <span data-ttu-id="a318b-129">然後使用**組 AzureSubscription** tooset hello 訂用帳戶和目前的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a318b-129">Then use **Set-AzureSubscription** tooset hello subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="a318b-130">選取 SQL Server 虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="a318b-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="a318b-131">找出可用的 SQL Server 虛擬機器映像從 hello 組件庫的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="a318b-131">Find out hello list of available SQL Server virtual machines images from hello gallery.</span></span> <span data-ttu-id="a318b-132">這些映像都有以「SQL」開頭的 **ImageFamily** 屬性。</span><span class="sxs-lookup"><span data-stu-id="a318b-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="a318b-133">hello 下列查詢會顯示 hello 映像系列可用 tooyou 具有預先安裝的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="a318b-133">hello following query displays hello image family available tooyou that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="a318b-134">當您找到 hello 虛擬機器映像系列時，此系列中可能有多個已發行的映像。</span><span class="sxs-lookup"><span data-stu-id="a318b-134">When you find hello  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="a318b-135">使用 hello 下列指令碼 toofind hello 最新發行的虛擬機器映像您選取的映像系列名稱 (例如**SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="a318b-135">Use hello following script toofind hello latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a><span data-ttu-id="a318b-136">建立 hello 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a318b-136">Create hello virtual machine</span></span>

<span data-ttu-id="a318b-137">最後，使用 PowerShell 建立 hello 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="a318b-137">Finally, create hello virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="a318b-138">建立雲端服務 toohost hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="a318b-138">Create a cloud service toohost hello new VM.</span></span> <span data-ttu-id="a318b-139">請注意，它也可能 toouse 現有的雲端服務而。</span><span class="sxs-lookup"><span data-stu-id="a318b-139">Note that it is also possible toouse an existing cloud service instead.</span></span> <span data-ttu-id="a318b-140">建立新的變數**$svcname** hello hello 雲端服務的簡短名稱。</span><span class="sxs-lookup"><span data-stu-id="a318b-140">Create a new variable **$svcname** with hello short name of hello cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="a318b-141">指定 hello 虛擬機器名稱和大小。</span><span class="sxs-lookup"><span data-stu-id="a318b-141">Specify hello virtual machine name and a size.</span></span> <span data-ttu-id="a318b-142">如需關於虛擬機器大小的詳細資訊，請參閱 [Azure 的虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a318b-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="a318b-143">指定 hello 本機系統管理員帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="a318b-143">Specify hello local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="a318b-144">執行下列指令碼 toocreate hello 虛擬機器的 hello。</span><span class="sxs-lookup"><span data-stu-id="a318b-144">Run hello following script toocreate hello virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="a318b-145">其他說明及組態選項，請參閱 hello**建置命令集**一節中[使用 Azure PowerShell toocreate 並預先設定 Windows 型虛擬機器](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a318b-145">For additional explanation and configuration options, see hello **Build your command set** section in [Use Azure PowerShell toocreate and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="a318b-146">PowerShell 指令碼範例</span><span class="sxs-lookup"><span data-stu-id="a318b-146">Example PowerShell script</span></span>

<span data-ttu-id="a318b-147">hello 下列指令碼提供一個範例的完整的指令碼會建立**SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a318b-147">hello following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="a318b-148">如果您使用此指令碼，您必須自訂 hello hello 本主題中的上一個步驟為基礎的初始變數。</span><span class="sxs-lookup"><span data-stu-id="a318b-148">If you use this script, you must customize hello initial variables based on hello previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="a318b-149">使用遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="a318b-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="a318b-150">建立 hello RDP 檔案中 hello 目前使用者的文件資料夾 toolaunch 這些虛擬機器 toocomplete 安裝程式：</span><span class="sxs-lookup"><span data-stu-id="a318b-150">Create hello RDP files in hello current user's document folder toolaunch these virtual machines toocomplete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="a318b-151">在 hello 文件目錄中，啟動 hello RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="a318b-151">In hello documents directory, launch hello RDP file.</span></span> <span data-ttu-id="a318b-152">連接 hello 系統管理員使用者名稱與先前提供的密碼 （例如，如果您的使用者名稱是 VMAdmin，指定"\VMAdmin"hello 使用者身分，並提供 hello 密碼）。</span><span class="sxs-lookup"><span data-stu-id="a318b-152">Connect with hello administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as hello user and provide hello password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a><span data-ttu-id="a318b-153">Hello 遠端存取的 SQL Server 電腦的完整 hello 組態</span><span class="sxs-lookup"><span data-stu-id="a318b-153">Complete hello configuration of hello SQL Server Machine for remote access</span></span>

<span data-ttu-id="a318b-154">登入與遠端桌面 toohello 機器之後，設定 SQL Server 中的 hello 指示[Azure VM 中設定 SQL Server 連接的步驟](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)。</span><span class="sxs-lookup"><span data-stu-id="a318b-154">After logging on toohello machine with remote desktop, configure SQL Server based on hello instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a318b-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a318b-155">Next steps</span></span>

<span data-ttu-id="a318b-156">您可以找到的佈建 hello 中的虛擬機器使用 PowerShell 的其他指示[虛擬機器文件](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a318b-156">You can find additional instructions for provisioning virtual machines with PowerShell in hello [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="a318b-157">在許多情況下，hello 下一個步驟是 toomigrate 資料庫 toothis 新的 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="a318b-157">In many cases, hello next step is toomigrate your databases toothis new SQL Server VM.</span></span> <span data-ttu-id="a318b-158">如需資料庫移轉指引，請參閱[移轉資料庫 tooSQL Azure VM 上的 Server](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a318b-158">For database migration guidance, see [Migrating a Database tooSQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="a318b-159">如果您也想使用 hello Azure 入口網站 toocreate SQL 虛擬機器，請參閱[佈建在 Azure 上的 SQL Server 虛擬機器](../sql/virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="a318b-159">If you're also interested in using hello Azure portal toocreate SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="a318b-160">請注意該 hello 教學課程會逐步引導您透過 hello 入口網站建立 Vm 使用 hello 建議的資源管理員模型，而不是使用此 PowerShell 主題中的 hello 傳統模型。</span><span class="sxs-lookup"><span data-stu-id="a318b-160">Note that hello tutorial that walks you through hello portal creates VMs using hello recommended Resource Manager model, rather than hello classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="a318b-161">此外 toothese 資源，我們建議您檢閱[相關 toorunning Azure 虛擬機器中 SQL Server 的其他主題](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a318b-161">In addition toothese resources, we recommend that you review [other topics related toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
