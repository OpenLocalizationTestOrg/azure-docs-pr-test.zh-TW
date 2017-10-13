---
title: "Azure Stack 儲存體適用的工具"
description: "了解 Azure Stack 儲存體資料傳輸工具"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: 9799498a11449a9ed496d0fdb40312603eda064e
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="tools-for-azure-stack-storage"></a><span data-ttu-id="2ffab-103">Azure Stack 儲存體適用的工具</span><span class="sxs-lookup"><span data-stu-id="2ffab-103">Tools for Azure Stack Storage</span></span>

<span data-ttu-id="2ffab-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="2ffab-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="2ffab-105">Microsoft Azure Stack 提供磁碟、Blob、資料表、佇列和帳戶管理功能適用的一組儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="2ffab-105">Microsoft Azure Stack provides a set of the storage services for disks, blobs, tables, queues, and account management functionality.</span></span> <span data-ttu-id="2ffab-106">如果您要管理資料、將資料移動至 Azure Stack 儲存體，或從 Azure Stack 儲存體移動資料，就可以使用一組 Azure 儲存體工具。</span><span class="sxs-lookup"><span data-stu-id="2ffab-106">You can use a set of Azure Storage tools if you want to manage or move data to or from Azure Stack Storage.</span></span> <span data-ttu-id="2ffab-107">本文提供可用工具的快速概觀。</span><span class="sxs-lookup"><span data-stu-id="2ffab-107">This article provides a quick overview of the tools available.</span></span>

<span data-ttu-id="2ffab-108">最適合您的工具取決於您的需求：</span><span class="sxs-lookup"><span data-stu-id="2ffab-108">The tool that works best for you depends on your requirements:</span></span>
* [<span data-ttu-id="2ffab-109">AzCopy</span><span class="sxs-lookup"><span data-stu-id="2ffab-109">AzCopy</span></span>](#azcopy)

    <span data-ttu-id="2ffab-110">可下載的儲存體專用命令列公用程式，能夠從儲存體帳戶內或是在儲存體帳戶之間，從一個物件複製資料到另一個物件。</span><span class="sxs-lookup"><span data-stu-id="2ffab-110">A storage-specific command-line utility that you can download to copy data from one object to another within your storage account, or between storage accounts.</span></span>

* [<span data-ttu-id="2ffab-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ffab-111">Azure PowerShell</span></span>](#azure-powershell)

    <span data-ttu-id="2ffab-112">工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。</span><span class="sxs-lookup"><span data-stu-id="2ffab-112">A task-based command-line shell and scripting language designed especially for system administration.</span></span>

* [<span data-ttu-id="2ffab-113">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2ffab-113">Azure CLI</span></span>](#azure-cli)

    <span data-ttu-id="2ffab-114">開放原始碼、跨平台的工具，可提供一組運用在 Azure 和 Azure Stack 平台上的命令。</span><span class="sxs-lookup"><span data-stu-id="2ffab-114">An open-source, cross-platform tool that provides a set of commands for working with the Azure and Azure Stack platforms.</span></span>

* [<span data-ttu-id="2ffab-115">Microsoft 儲存體總管 (預覽)</span><span class="sxs-lookup"><span data-stu-id="2ffab-115">Microsoft Storage Explorer (Preview)</span></span>](#microsoft-azure-storage-explorer)

    <span data-ttu-id="2ffab-116">具有使用者介面且易於使用的獨立應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ffab-116">An easy to use standalone app with a user interface.</span></span>

<span data-ttu-id="2ffab-117">由於 Azure 和 Azure Stack 的儲存體服務有所不同，因此下列各節所述的各項工具可能會有一些特定的需求。</span><span class="sxs-lookup"><span data-stu-id="2ffab-117">Due to the Storage services differences between Azure and Azure Stack, there might be some specific requirements for each tool described in the following sections.</span></span> <span data-ttu-id="2ffab-118">如需 Azure Stack 儲存體和 Azure 儲存體之間的比較，請參閱 [Azure Stack 儲存體：差異與注意事項](azure-stack-acs-differences.md)。</span><span class="sxs-lookup"><span data-stu-id="2ffab-118">For a comparison between Azure Stack storage and Azure storage, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>


## <a name="azcopy"></a><span data-ttu-id="2ffab-119">AzCopy</span><span class="sxs-lookup"><span data-stu-id="2ffab-119">AzCopy</span></span>
<span data-ttu-id="2ffab-120">AzCopy 是一個命令列公用程式，可以使用簡單命令高效率地將資料複製到和複製自 Microsoft Azure Blob 和資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="2ffab-120">AzCopy is a command-line utility designed to copy data to and from Microsoft Azure Blob and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="2ffab-121">您可以從儲存體帳戶內或是在儲存體帳戶之間，從一個物件複製資料到另一個物件。</span><span class="sxs-lookup"><span data-stu-id="2ffab-121">You can copy data from one object to another within your storage account, or between storage accounts.</span></span> <span data-ttu-id="2ffab-122">AzCopy 有兩個版本：Windows 上的 AzCopy 和 Linux 上的 AzCopy。</span><span class="sxs-lookup"><span data-stu-id="2ffab-122">There are two version of the AzCopy: AzCopy on Windows and AzCopy on Linux.</span></span> <span data-ttu-id="2ffab-123">Azure Stack 僅支援 Windows 版本。</span><span class="sxs-lookup"><span data-stu-id="2ffab-123">Azure Stack only supports the Windows version.</span></span> 
 
### <a name="download-and-install-azcopy"></a><span data-ttu-id="2ffab-124">下載並安裝 AzCopy</span><span class="sxs-lookup"><span data-stu-id="2ffab-124">Download and install AzCopy</span></span> 
<span data-ttu-id="2ffab-125">[下載](https://aka.ms/azcopyforazurestack) Azure Stack 支援的 Windows 版 AzCopy。</span><span class="sxs-lookup"><span data-stu-id="2ffab-125">[Download](https://aka.ms/azcopyforazurestack) the supported Windows version of AzCopy for Azure Stack.</span></span> <span data-ttu-id="2ffab-126">在 Azure Stack 和在 Azure 上安裝與使用 AzCopy 的方式一樣。</span><span class="sxs-lookup"><span data-stu-id="2ffab-126">You can install and use AzCopy on Azure Stack the same way as Azure.</span></span> <span data-ttu-id="2ffab-127">若要深入了解，請參閱[使用 AzCopy 命令列公用程式傳輸資料](../../storage/common/storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="2ffab-127">To learn more, see [Transfer data with the AzCopy Command-Line Utility](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="azcopy-command-examples-for-data-transfer"></a><span data-ttu-id="2ffab-128">資料傳輸適用的 AzCopy 命令範例</span><span class="sxs-lookup"><span data-stu-id="2ffab-128">AzCopy command examples for data transfer</span></span>
<span data-ttu-id="2ffab-129">下列範例會示範一些將資料複製至 Azure Stack Blob 以及從 Azure Stack Blob 複製資料的典型案例。</span><span class="sxs-lookup"><span data-stu-id="2ffab-129">The following examples demonstrate a few typical scenarios for copying data to and from Azure Stack blobs.</span></span> <span data-ttu-id="2ffab-130">若要深入了解，請參閱[使用 AzCopy 命令列公用程式傳輸資料](../../storage/storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="2ffab-130">To learn more, see [Transfer data with the AzCopy Command-Line Utility](../../storage/storage-use-azcopy.md).</span></span> 
#### <a name="download-all-blobs-to-local-disk"></a><span data-ttu-id="2ffab-131">將所有 Blob 下載至本機磁碟</span><span class="sxs-lookup"><span data-stu-id="2ffab-131">Download all blobs to local disk</span></span>
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="2ffab-132">上傳單一檔案到虛擬目錄</span><span class="sxs-lookup"><span data-stu-id="2ffab-132">Upload single file to virtual directory</span></span> 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a><span data-ttu-id="2ffab-133">在 Azure 和 Azure Stack 儲存體之間移動資料</span><span class="sxs-lookup"><span data-stu-id="2ffab-133">Move data between Azure and Azure Stack Storage</span></span> 
<span data-ttu-id="2ffab-134">不支援在 Azure 儲存體和 Azure Stack 之間的非同步資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="2ffab-134">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="2ffab-135">您必須使用 `/SyncCopy` 選項來指定傳輸。</span><span class="sxs-lookup"><span data-stu-id="2ffab-135">you need to specify the transfer with the `/SyncCopy` option.</span></span> 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a><span data-ttu-id="2ffab-136">Azcopy 的已知問題</span><span class="sxs-lookup"><span data-stu-id="2ffab-136">Azcopy Known issues</span></span>
* <span data-ttu-id="2ffab-137">檔案儲存體還無法在 Azure Stack 中使用，因此檔案儲存體上沒有任何可用的 AzCopy 作業。</span><span class="sxs-lookup"><span data-stu-id="2ffab-137">Any AzCopy operation on File storage is not available because File Storage is not yet available in Azure Stack.</span></span>
* <span data-ttu-id="2ffab-138">不支援在 Azure 儲存體和 Azure Stack 之間的非同步資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="2ffab-138">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="2ffab-139">您可以使用 `/SyncCopy` 選項指定傳輸來複製資料。</span><span class="sxs-lookup"><span data-stu-id="2ffab-139">You can specify the transfer with the `/SyncCopy` option to copy the data.</span></span>
* <span data-ttu-id="2ffab-140">Azure Stack 儲存體不支援 Linux 版本的 Azcopy。</span><span class="sxs-lookup"><span data-stu-id="2ffab-140">The Linux version of Azcopy is not supported for Azure Stack Storage.</span></span> 

## <a name="azure-powershell"></a><span data-ttu-id="2ffab-141">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ffab-141">Azure PowerShell</span></span>
<span data-ttu-id="2ffab-142">Azure PowerShell 是一個模組，可提供管理 Azure 和 Azure Stack 上服務的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2ffab-142">Azure PowerShell is a module that provides cmdlets for managing services on both Azure and Azure Stack.</span></span> <span data-ttu-id="2ffab-143">此模組為工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。</span><span class="sxs-lookup"><span data-stu-id="2ffab-143">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

### <a name="install-and-configure-powershell-for-azure-stack"></a><span data-ttu-id="2ffab-144">安裝及設定用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ffab-144">Install and Configure PowerShell for Azure Stack</span></span>
<span data-ttu-id="2ffab-145">您需要與 Azure Stack 相容的 Azure PowerShell 模組，才能搭配 Azure Stack 使用。</span><span class="sxs-lookup"><span data-stu-id="2ffab-145">Azure Stack compatible Azure PowerShell modules are required to work with Azure Stack.</span></span> <span data-ttu-id="2ffab-146">如需詳細資訊，請參閱[安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md) 和[設定 Azure Stack 使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md)以深入了解。</span><span class="sxs-lookup"><span data-stu-id="2ffab-146">For more information, see [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) and [Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) to learn more.</span></span>

### <a name="powershell-sample-script-for-azure-stack"></a><span data-ttu-id="2ffab-147">適用於 Azure Stack 的 PowerShell 範例指令碼</span><span class="sxs-lookup"><span data-stu-id="2ffab-147">PowerShell Sample script for Azure Stack</span></span> 
<span data-ttu-id="2ffab-148">此範例假設您已成功[安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="2ffab-148">This sample assume you have successfully [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> <span data-ttu-id="2ffab-149">此指令碼將協助您完成設定，並要求您的 Azure Stack 租用戶認證，以便將帳戶新增至本機 PowerShell 環境。</span><span class="sxs-lookup"><span data-stu-id="2ffab-149">This script will help you conplete the configuration and ask your Azure Stack tenant credentials to add your account to the local PowerShell environemnt.</span></span> <span data-ttu-id="2ffab-150">接著，指令碼將設定預設的 Azure 訂用帳戶、在 Azure 中建立新的儲存體帳戶、在這個新的儲存體帳戶中建立新容器，並將現有的映像檔案 (Blob) 上傳至該容器。</span><span class="sxs-lookup"><span data-stu-id="2ffab-150">Then, the script will set the default Azure subscription, create a new storage account in Azure, create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="2ffab-151">指令碼列出該容器中的所有 Blob 之後，它會在本機電腦中建立新的目的地目錄並下載映像檔。</span><span class="sxs-lookup"><span data-stu-id="2ffab-151">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>

1. <span data-ttu-id="2ffab-152">安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="2ffab-152">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
2. <span data-ttu-id="2ffab-153">下載[與 Azure Stack 搭配運作所需的工具](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="2ffab-153">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  
3. <span data-ttu-id="2ffab-154">開啟 [Windows PowerShell ISE] 和 [以系統管理員​​身分執行]，按一下 **[檔案]** > **[新增]**，以建立新的指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="2ffab-154">Open **Windows PowerShell ISE** and **Run as Administrator**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="2ffab-155">複製下列指令碼並貼到新的指令碼檔案中。</span><span class="sxs-lookup"><span data-stu-id="2ffab-155">Copy the script below and paste to the new script file.</span></span>
5. <span data-ttu-id="2ffab-156">根據您的組態設定，更新指令碼變數。</span><span class="sxs-lookup"><span data-stu-id="2ffab-156">Update the script variables based on your configuration settings.</span></span> 
6. <span data-ttu-id="2ffab-157">注意：此指令碼必須在下載的 **AzureStack_Tools** 根目錄下執行。</span><span class="sxs-lookup"><span data-stu-id="2ffab-157">Note: this script has to be run under the root of downloaded **AzureStack_Tools**.</span></span> 

```PowerShell 
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with the name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name to your new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name to your new storage account. It must be lowercase!
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name to your new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import the Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure the PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set the GraphEndpointResourceId value
Set-AzureRmEnvironment -Name $ARMEvnName -GraphEndpoint $GraphAudiance

# Login
$TenantID = Get-AzsDirectoryTenantId -AADTenantName $AADTenantName -EnvironmentName $ARMEvnName
Login-AzureRmAccount -EnvironmentName $ARMEvnName -TenantId $TenantID 

# Set a default Azure subscription.
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Create a new Resource Group 
New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

# Create a new storage account.
New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS

# Set a default storage account.
Set-AzureRmCurrentStorageAccount -StorageAccountName $StorageAccountName -ResourceGroupName $ResourceGroupName 

# Create a new container.
New-AzureStorageContainer -Name $ContainerName -Permission Off

# Upload a blob into a container.
Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload

# List all blobs in a container.
Get-AzureStorageBlob -Container $ContainerName

# Download blobs from the container:
# Get a reference to a list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create the destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into the local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
```

### <a name="powershell-known-issues"></a><span data-ttu-id="2ffab-158">PowerShell 的已知問題</span><span class="sxs-lookup"><span data-stu-id="2ffab-158">PowerShell Known Issues</span></span> 
<span data-ttu-id="2ffab-159">Azure Stack 目前相容的 Azure PowerShell 模組版本是 1.2.10。</span><span class="sxs-lookup"><span data-stu-id="2ffab-159">The current compatible Azure PowerShell module version for Azure Stack is 1.2.10.</span></span> <span data-ttu-id="2ffab-160">此版本與最新版的 Azure PowerShell 不同。</span><span class="sxs-lookup"><span data-stu-id="2ffab-160">It’s different from the latest version of Azure PowerShell.</span></span> <span data-ttu-id="2ffab-161">此差異會影響儲存體服務作業：</span><span class="sxs-lookup"><span data-stu-id="2ffab-161">This difference impacts storage services operation:</span></span>

* <span data-ttu-id="2ffab-162">`Get-AzureRmStorageAccountKey` 在 1.2.10 版的傳回值格式有兩個屬性：`Key1` 和 `Key2`，而目前的 Azure 版本則會傳回包含所有帳戶金鑰的陣列。</span><span class="sxs-lookup"><span data-stu-id="2ffab-162">The return value format of `Get-AzureRmStorageAccountKey` in version 1.2.10 has two properties: `Key1` and `Key2`, while the current Azure version returns an array containing all the account keys.</span></span>
   ```
   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.4, and later versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Value[0]

   # This command gets a specific key for a Storage account, 
   # and works for Azure PowerShell version 1.3.2, and previous versions.
   (Get-AzureRmStorageAccountKey -ResourceGroupName "RG01" `
   -AccountName "MyStorageAccount").Key1

   ```
   <span data-ttu-id="2ffab-163">如需詳細資訊，請參閱 [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0)。</span><span class="sxs-lookup"><span data-stu-id="2ffab-163">For more information, see [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span></span>

## <a name="azure-cli"></a><span data-ttu-id="2ffab-164">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2ffab-164">Azure CLI</span></span>
<span data-ttu-id="2ffab-165">Azure CLI 是管理 Azure 資源的 Azure 命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="2ffab-165">The Azure CLI is Azure’s command-line experience for managing Azure resources.</span></span> <span data-ttu-id="2ffab-166">您可以將它安裝在 macOS、Linux 及 Windows 上，並從命令列來執行。</span><span class="sxs-lookup"><span data-stu-id="2ffab-166">You can install it on macOS, Linux, and Windows and run it from the command line.</span></span> 

<span data-ttu-id="2ffab-167">Azure CLI 已針對以下作業進行最佳化：從命令列管理 Azure 資源進行，以及建置可用於 Azure Resource Manager 的自動化指令碼。</span><span class="sxs-lookup"><span data-stu-id="2ffab-167">Azure CLI is optimized for managing and administering Azure resources from the command line, and for building automation scripts that work against the Azure Resource Manager.</span></span> <span data-ttu-id="2ffab-168">它提供許多與 Azure Stack 入口網站相同的功能，包括眾多資料存取功能。</span><span class="sxs-lookup"><span data-stu-id="2ffab-168">It provides many of the same functions found in the Azure Stack portal, including rich data access.</span></span>

<span data-ttu-id="2ffab-169">Azure Stack 需要有 Azure CLI 2.0 版。</span><span class="sxs-lookup"><span data-stu-id="2ffab-169">Azure Stack requires Azure CLI version 2.0.</span></span> <span data-ttu-id="2ffab-170">如需有關安裝和設定用於 Azure Stack 的 Azure CLI 詳細資訊，請參閱[安裝和設定 Azure Stack CLI](azure-stack-connect-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="2ffab-170">For more information about installing and configuring Azure CLI with Azure Stack, see [Install and configure Azure Stack CLI](azure-stack-connect-cli.md).</span></span> <span data-ttu-id="2ffab-171">如需有關如何搭配 Azure Stack 儲存體帳戶中的資源使用 Azure CLI 2.0 執行多種工作的詳細資訊，請參閱[使用 Azure CLI2.0 搭配 Azure 儲存體](../../storage/storage-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2ffab-171">For more information about how to use the Azure CLI 2.0 to perform several tasks working with resources in your Azure Stack Storage account, see [Using the Azure CLI2.0 with Azure Storage](../../storage/storage-azure-cli.md)</span></span>

### <a name="azure-cli-sample-script-for-azure-stack"></a><span data-ttu-id="2ffab-172">適用於 Azure Stack 的 Azure CLI 範例指令碼</span><span class="sxs-lookup"><span data-stu-id="2ffab-172">Azure CLI sample script for Azure Stack</span></span> 
<span data-ttu-id="2ffab-173">完成 CLI 的安裝和設定之後，您就可以嘗試下列步驟，使用一個小殼層範例指令碼來與 Azure Stack 儲存體資源進行互動。</span><span class="sxs-lookup"><span data-stu-id="2ffab-173">Once you complete the CLI installation and configuration, you can try the following steps to work with a small shell sample script to interact with Azure Stack Storage resources.</span></span> <span data-ttu-id="2ffab-174">此指令碼會先在您的儲存體帳戶中建立一個新容器，然後將現有的檔案 (以 Blob 的形式) 上傳至該容器、列出容器中的所有 Blob，最後再將檔案下載到本機電腦上您指定的目的地。</span><span class="sxs-lookup"><span data-stu-id="2ffab-174">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container, lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span> <span data-ttu-id="2ffab-175">執行此指令碼之前，請確定您已成功連線並登入目標 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="2ffab-175">Before you run this script, make sure you successfully connect and login to the target Azure Stack.</span></span> 
1. <span data-ttu-id="2ffab-176">開啟您喜愛的文字編輯器，然後複製上述指令碼並貼入編輯器中。</span><span class="sxs-lookup"><span data-stu-id="2ffab-176">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>
2. <span data-ttu-id="2ffab-177">更新指令碼的變數以反映您的組態設定。</span><span class="sxs-lookup"><span data-stu-id="2ffab-177">Update the script's variables to reflect your configuration settings.</span></span> 
3. <span data-ttu-id="2ffab-178">在您更新必要變數之後，請儲存指令碼並結束編輯器。</span><span class="sxs-lookup"><span data-stu-id="2ffab-178">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="2ffab-179">後續步驟假設您已將指令碼命名為 my_storage_sample.sh。</span><span class="sxs-lookup"><span data-stu-id="2ffab-179">The next steps assume you've named your script my_storage_sample.sh.</span></span>
4. <span data-ttu-id="2ffab-180">如有必要，請將指令碼標示為可執行檔︰`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="2ffab-180">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>
5. <span data-ttu-id="2ffab-181">執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="2ffab-181">Execute the script.</span></span> <span data-ttu-id="2ffab-182">例如，在 Bash 中：`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="2ffab-182">For example, in Bash: `./my_storage_sample.sh`</span></span>

```bash
#!/bin/bash
# A simple Azure Stack Storage example script

export AZURESTACK_RESOURCE_GROUP=<resource_group_name>
export AZURESTACK_RG_LOCATION="local"
export AZURESTACK_STORAGE_ACCOUNT_NAME=<storage_account_name>
export AZURESTACK_STORAGE_CONTAINER_NAME=<container_name>
export AZURESTACK_STORAGE_BLOB_NAME=<blob_name>
export FILE_TO_UPLOAD=<file_to_upload>
export DESTINATION_FILE=<destination_file>

echo "Creating the resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating the storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating the blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading the file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing the blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading the file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
```

## <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="2ffab-183">Microsoft Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="2ffab-183">Microsoft Azure Storage Explorer</span></span>

<span data-ttu-id="2ffab-184">Microsoft Azure 儲存體總管是 Windows 提供的獨立應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ffab-184">Microsoft Azure Storage Explorer is a standalone app from Microsoft.</span></span> <span data-ttu-id="2ffab-185">此工具可讓您在 Windows、MacOS 和 Linux 上輕鬆處理 Azure 儲存體和 Azure Stack 儲存體的資料。</span><span class="sxs-lookup"><span data-stu-id="2ffab-185">It allows you to easily work with both Azure Storage and Azure Stack Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="2ffab-186">如果想要輕鬆地管理您的 Azure Stack 儲存體資料，請考慮使用 Microsoft Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="2ffab-186">If you want an easy way to manage your Azure Stack Storage data, then consider using Microsoft Azure Storage Explorer.</span></span>

<span data-ttu-id="2ffab-187">如需有關設定 Azure 儲存體總管來處理 Azure Stack 的詳細資訊，請參閱[將儲存體總管連線到 Azure Stack 訂用帳戶](azure-stack-storage-connect-se.md)。</span><span class="sxs-lookup"><span data-stu-id="2ffab-187">For more information about configuring Azure Storage Explorer to work with Azure Stack, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack-storage-connect-se.md).</span></span>

<span data-ttu-id="2ffab-188">如需有關 Microsoft Azure 儲存體總管的詳細資訊，請參閱[開始使用儲存體總管 (預覽)](../../vs-azure-tools-storage-manage-with-storage-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="2ffab-188">For more information about Microsoft Azure Storage Explorer, see [Get started with Storage Explorer (Preview)](../../vs-azure-tools-storage-manage-with-storage-explorer.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ffab-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ffab-189">Next steps</span></span>
* [<span data-ttu-id="2ffab-190">將儲存體總管連線到 Azure Stack 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2ffab-190">Connect Storage Explorer to an Azure Stack subscription</span></span>](azure-stack-storage-connect-se.md)
* [<span data-ttu-id="2ffab-191">開始使用儲存體總管 (預覽)</span><span class="sxs-lookup"><span data-stu-id="2ffab-191">Get started with Storage Explorer (Preview)</span></span>](../../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="2ffab-192">與 Azure 一致的儲存體：差異與注意事項</span><span class="sxs-lookup"><span data-stu-id="2ffab-192">Azure-consistent storage: differences and considerations</span></span>](azure-stack-acs-differences.md)
* [<span data-ttu-id="2ffab-193">Microsoft Azure 儲存體簡介</span><span class="sxs-lookup"><span data-stu-id="2ffab-193">Introduction to Microsoft Azure Storage</span></span>](../../storage/common/storage-introduction.md)

