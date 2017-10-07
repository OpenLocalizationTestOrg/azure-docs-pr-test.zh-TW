---
title: "aaaTools 堆疊 Azure 儲存體"
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
ms.date: 8/16/2017
ms.author: xiaofmao
ms.openlocfilehash: 184a1a51b4267e913aae823df31df3704d8e7b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tools-for-azure-stack-storage"></a><span data-ttu-id="689b6-103">Azure Stack 儲存體適用的工具</span><span class="sxs-lookup"><span data-stu-id="689b6-103">Tools for Azure Stack Storage</span></span>

<span data-ttu-id="689b6-104">Microsoft Azure 堆疊提供一組 hello 儲存體服務，如磁碟、 blob、 資料表、 佇列和帳戶管理功能。</span><span class="sxs-lookup"><span data-stu-id="689b6-104">Microsoft Azure Stack provides a set of hello storage services for disks, blobs, tables, queues, and account management functionality.</span></span> <span data-ttu-id="689b6-105">如果您想 toomanage 或移動資料 tooor 從 Azure 堆疊儲存體，您可以使用一組 Azure 儲存體工具。</span><span class="sxs-lookup"><span data-stu-id="689b6-105">You can use a set of Azure Storage tools if you want toomanage or move data tooor from Azure Stack Storage.</span></span> <span data-ttu-id="689b6-106">本文章提供可用的 hello 工具的快速概觀。</span><span class="sxs-lookup"><span data-stu-id="689b6-106">This article provides a quick overview of hello tools available.</span></span>

<span data-ttu-id="689b6-107">最適合您的 hello 工具取決於您的需求：</span><span class="sxs-lookup"><span data-stu-id="689b6-107">hello tool that works best for you depends on your requirements:</span></span>
* [<span data-ttu-id="689b6-108">AzCopy</span><span class="sxs-lookup"><span data-stu-id="689b6-108">AzCopy</span></span>](#azcopy)

    <span data-ttu-id="689b6-109">儲存區特定命令列公用程式，您可以下載 toocopy 資料從一個物件 tooanother 儲存體帳戶內或之間的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="689b6-109">A storage-specific command-line utility that you can download toocopy data from one object tooanother within your storage account, or between storage accounts.</span></span>

* [<span data-ttu-id="689b6-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="689b6-110">Azure PowerShell</span></span>](#azure-powershell)

    <span data-ttu-id="689b6-111">工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。</span><span class="sxs-lookup"><span data-stu-id="689b6-111">A task-based command-line shell and scripting language designed especially for system administration.</span></span>

* [<span data-ttu-id="689b6-112">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="689b6-112">Azure CLI</span></span>](#azure-cli)

    <span data-ttu-id="689b6-113">可提供一組命令使用 hello Azure 和 Azure 堆疊平台的開放原始碼、 跨平台工具。</span><span class="sxs-lookup"><span data-stu-id="689b6-113">An open-source, cross-platform tool that provides a set of commands for working with hello Azure and Azure Stack platforms.</span></span>

* [<span data-ttu-id="689b6-114">Microsoft 儲存體總管 (預覽)</span><span class="sxs-lookup"><span data-stu-id="689b6-114">Microsoft Storage Explorer (Preview)</span></span>](#microsoft-azure-storage-explorer)

    <span data-ttu-id="689b6-115">輕鬆 toouse 獨立應用程式，但使用者介面。</span><span class="sxs-lookup"><span data-stu-id="689b6-115">An easy toouse standalone app with a user interface.</span></span>

<span data-ttu-id="689b6-116">由於 toohello Azure 和 Azure 堆疊之間的儲存體服務存在差異，可能會有一些特定的需求，每個工具 hello 下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="689b6-116">Due toohello Storage services differences between Azure and Azure Stack, there might be some specific requirements for each tool described in hello following sections.</span></span> <span data-ttu-id="689b6-117">如需 Azure Stack 儲存體和 Azure 儲存體之間的比較，請參閱 [Azure Stack 儲存體：差異與注意事項](azure-stack-acs-differences.md)。</span><span class="sxs-lookup"><span data-stu-id="689b6-117">For a comparison between Azure Stack storage and Azure storage, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>


## <a name="azcopy"></a><span data-ttu-id="689b6-118">AzCopy</span><span class="sxs-lookup"><span data-stu-id="689b6-118">AzCopy</span></span>
<span data-ttu-id="689b6-119">AzCopy 是從 Microsoft Azure Blob 和資料表儲存體使用簡單的命令，以獲得最佳效能的設計的命令列公用程式 toocopy 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="689b6-119">AzCopy is a command-line utility designed toocopy data tooand from Microsoft Azure Blob and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="689b6-120">儲存體帳戶內或之間的儲存體帳戶，您可以從一個物件 tooanother 複製資料。</span><span class="sxs-lookup"><span data-stu-id="689b6-120">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span> <span data-ttu-id="689b6-121">有兩個版本的 hello AzCopy： 在 Windows 和 Linux 上的 AzCopy 上 AzCopy。</span><span class="sxs-lookup"><span data-stu-id="689b6-121">There are two version of hello AzCopy: AzCopy on Windows and AzCopy on Linux.</span></span> <span data-ttu-id="689b6-122">Azure 堆疊只支援 Windows hello 的版本。</span><span class="sxs-lookup"><span data-stu-id="689b6-122">Azure Stack only supports hello Windows version.</span></span> 
 
### <a name="download-and-install-azcopy"></a><span data-ttu-id="689b6-123">下載並安裝 AzCopy</span><span class="sxs-lookup"><span data-stu-id="689b6-123">Download and install AzCopy</span></span> 
<span data-ttu-id="689b6-124">[下載](https://aka.ms/azcopyforazurestack)Azure 堆疊的 AzCopy hello 支援 Windows 版本。</span><span class="sxs-lookup"><span data-stu-id="689b6-124">[Download](https://aka.ms/azcopyforazurestack) hello supported Windows version of AzCopy for Azure Stack.</span></span> <span data-ttu-id="689b6-125">您可以安裝和使用 AzCopy 上 Azure 堆疊 hello Azure 與相同的方式。</span><span class="sxs-lookup"><span data-stu-id="689b6-125">You can install and use AzCopy on Azure Stack hello same way as Azure.</span></span> <span data-ttu-id="689b6-126">詳細資訊，請參閱 toolearn [hello AzCopy 命令列公用程式使用傳輸資料](../storage/common/storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="689b6-126">toolearn more, see [Transfer data with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="azcopy-command-examples-for-data-transfer"></a><span data-ttu-id="689b6-127">資料傳輸適用的 AzCopy 命令範例</span><span class="sxs-lookup"><span data-stu-id="689b6-127">AzCopy command examples for data transfer</span></span>
<span data-ttu-id="689b6-128">hello 遵循範例示範如何從 Azure 堆疊 blob 複製資料 tooand 的一些典型狀況。</span><span class="sxs-lookup"><span data-stu-id="689b6-128">hello following examples demonstrate a few typical scenarios for copying data tooand from Azure Stack blobs.</span></span> <span data-ttu-id="689b6-129">詳細資訊，請參閱 toolearn [hello AzCopy 命令列公用程式使用傳輸資料](../storage/storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="689b6-129">toolearn more, see [Transfer data with hello AzCopy Command-Line Utility](../storage/storage-use-azcopy.md).</span></span> 
#### <a name="download-all-blobs-toolocal-disk"></a><span data-ttu-id="689b6-130">下載所有 blob toolocal 磁碟</span><span class="sxs-lookup"><span data-stu-id="689b6-130">Download all blobs toolocal disk</span></span>
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="689b6-131">單一檔案上傳 toovirtual 目錄</span><span class="sxs-lookup"><span data-stu-id="689b6-131">Upload single file toovirtual directory</span></span> 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a><span data-ttu-id="689b6-132">在 Azure 和 Azure Stack 儲存體之間移動資料</span><span class="sxs-lookup"><span data-stu-id="689b6-132">Move data between Azure and Azure Stack Storage</span></span> 
<span data-ttu-id="689b6-133">不支援在 Azure 儲存體和 Azure Stack 之間的非同步資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="689b6-133">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="689b6-134">您需要 toospecify hello 傳輸以 hello`/SyncCopy`選項。</span><span class="sxs-lookup"><span data-stu-id="689b6-134">you need toospecify hello transfer with hello `/SyncCopy` option.</span></span> 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a><span data-ttu-id="689b6-135">Azcopy 的已知問題</span><span class="sxs-lookup"><span data-stu-id="689b6-135">Azcopy Known issues</span></span>
* <span data-ttu-id="689b6-136">檔案儲存體還無法在 Azure Stack 中使用，因此檔案儲存體上沒有任何可用的 AzCopy 作業。</span><span class="sxs-lookup"><span data-stu-id="689b6-136">Any AzCopy operation on File storage is not available because File Storage is not yet available in Azure Stack.</span></span>
* <span data-ttu-id="689b6-137">不支援在 Azure 儲存體和 Azure Stack 之間的非同步資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="689b6-137">Asynchronous data transfer between Azure Storage and Azure Stack is not supported.</span></span> <span data-ttu-id="689b6-138">您可以指定 hello 傳輸以 hello`/SyncCopy`選項 toocopy hello 資料。</span><span class="sxs-lookup"><span data-stu-id="689b6-138">You can specify hello transfer with hello `/SyncCopy` option toocopy hello data.</span></span>
* <span data-ttu-id="689b6-139">Azcopy hello Linux 版本不支援 Azure 堆疊儲存體。</span><span class="sxs-lookup"><span data-stu-id="689b6-139">hello Linux version of Azcopy is not supported for Azure Stack Storage.</span></span> 

## <a name="azure-powershell"></a><span data-ttu-id="689b6-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="689b6-140">Azure PowerShell</span></span>
<span data-ttu-id="689b6-141">Azure PowerShell 是一個模組，可提供管理 Azure 和 Azure Stack 上服務的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="689b6-141">Azure PowerShell is a module that provides cmdlets for managing services on both Azure and Azure Stack.</span></span> <span data-ttu-id="689b6-142">此模組為工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。</span><span class="sxs-lookup"><span data-stu-id="689b6-142">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

### <a name="install-and-configure-powershell-for-azure-stack"></a><span data-ttu-id="689b6-143">安裝及設定用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="689b6-143">Install and Configure PowerShell for Azure Stack</span></span>
<span data-ttu-id="689b6-144">Azure 堆疊相容 Azure PowerShell 模組是與 Azure 堆疊的必要的 toowork。</span><span class="sxs-lookup"><span data-stu-id="689b6-144">Azure Stack compatible Azure PowerShell modules are required toowork with Azure Stack.</span></span> <span data-ttu-id="689b6-145">如需詳細資訊，請參閱[安裝 PowerShell Azure 堆疊以](azure-stack-powershell-install.md)和[設定 hello Azure 堆疊使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="689b6-145">For more information, see [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) and [Configure hello Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) toolearn more.</span></span>

### <a name="powershell-sample-script-for-azure-stack"></a><span data-ttu-id="689b6-146">適用於 Azure Stack 的 PowerShell 範例指令碼</span><span class="sxs-lookup"><span data-stu-id="689b6-146">PowerShell Sample script for Azure Stack</span></span> 
<span data-ttu-id="689b6-147">此範例假設您已成功[安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="689b6-147">This sample assume you have successfully [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> <span data-ttu-id="689b6-148">此指令碼會協助您 conplete hello 組態，並要求您的 Azure 堆疊租用戶認證 tooadd 您帳戶 toohello 本機 PowerShell environemnt。</span><span class="sxs-lookup"><span data-stu-id="689b6-148">This script will help you conplete hello configuration and ask your Azure Stack tenant credentials tooadd your account toohello local PowerShell environemnt.</span></span> <span data-ttu-id="689b6-149">然後，hello 指令碼會設定 hello 預設 Azure 訂用帳戶，在 Azure 中建立新的儲存體帳戶，在這個新的儲存體帳戶中建立新的容器並上傳現有的映像檔案 (blob) toothat 容器。</span><span class="sxs-lookup"><span data-stu-id="689b6-149">Then, hello script will set hello default Azure subscription, create a new storage account in Azure, create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="689b6-150">Hello 指令碼會列出該容器中的所有 blob 之後，它會在本機電腦中建立新的目的地目錄，並下載 hello 映像檔案。</span><span class="sxs-lookup"><span data-stu-id="689b6-150">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>

1. <span data-ttu-id="689b6-151">安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="689b6-151">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
2. <span data-ttu-id="689b6-152">下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="689b6-152">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  
3. <span data-ttu-id="689b6-153">開啟**Windows PowerShell ISE**和**系統管理員身分執行**，按一下 **檔案** > **新增**toocreate 新的指令碼檔。</span><span class="sxs-lookup"><span data-stu-id="689b6-153">Open **Windows PowerShell ISE** and **Run as Administrator**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="689b6-154">複製下列 hello 指令碼並貼上 toohello 新指令碼檔。</span><span class="sxs-lookup"><span data-stu-id="689b6-154">Copy hello script below and paste toohello new script file.</span></span>
5. <span data-ttu-id="689b6-155">更新您的組態設定為基礎的 hello 指令碼變數。</span><span class="sxs-lookup"><span data-stu-id="689b6-155">Update hello script variables based on your configuration settings.</span></span> 
6. <span data-ttu-id="689b6-156">注意： 此指令碼有執行 hello 根目錄下的 toobe 下載**AzureStack_Tools**。</span><span class="sxs-lookup"><span data-stu-id="689b6-156">Note: this script has toobe run under hello root of downloaded **AzureStack_Tools**.</span></span> 

```PowerShell 
# begin

$ARMEvnName = "AzureStackUser" # set AzureStackUser as your Azure Stack environemnt name
$ARMEndPoint = "https://management.local.azurestack.external" 
$GraphAudiance = "https://graph.windows.net/" 
$AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com" 

$SubscriptionName = "basic" # Update with hello name of your subscription.
$ResourceGroupName = "myTestRG" # Give a name tooyour new resource group.
$StorageAccountName = "azsblobcontainer" # Give a name tooyour new storage account. It must be lowercase!
$Location = "Local" # Choose "Local" as an example.
$ContainerName = "photo" # Give a name tooyour new container.
$ImageToUpload = "C:\temp\Hello.jpg" # Prepare an image file and a source directory in your local computer.
$DestinationFolder = "C:\temp\downlaod" # A destination directory in your local computer.

# Import hello Connect PowerShell module"
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Import-Module .\Connect\AzureStack.Connect.psm1

# Configure hello PowerShell environment
# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRmEnvironment -Name $ARMEvnName -ARMEndpoint $ARMEndPoint 

# Set hello GraphEndpointResourceId value
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

# Download blobs from hello container:
# Get a reference tooa list of all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName

# Create hello destination directory.
New-Item -Path $DestinationFolder -ItemType Directory -Force  

# Download blobs into hello local destination directory.
$blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder

# end
```

### <a name="powershell-known-issues"></a><span data-ttu-id="689b6-157">PowerShell 的已知問題</span><span class="sxs-lookup"><span data-stu-id="689b6-157">PowerShell Known Issues</span></span> 
<span data-ttu-id="689b6-158">hello 目前相容 Azure PowerShell 模組版本的 Azure 堆疊是 1.2.10。</span><span class="sxs-lookup"><span data-stu-id="689b6-158">hello current compatible Azure PowerShell module version for Azure Stack is 1.2.10.</span></span> <span data-ttu-id="689b6-159">它與不同的 Azure PowerShell hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="689b6-159">It’s different from hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="689b6-160">此差異會影響儲存體服務作業：</span><span class="sxs-lookup"><span data-stu-id="689b6-160">This difference impacts storage services operation:</span></span>

* <span data-ttu-id="689b6-161">hello 的傳回值格式`Get-AzureRmStorageAccountKey`版本 1.2.10 有兩個屬性：`Key1`和`Key2`，而目前 Azure 版本以 hello 傳回陣列，其中包含所有 hello account 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="689b6-161">hello return value format of `Get-AzureRmStorageAccountKey` in version 1.2.10 has two properties: `Key1` and `Key2`, while hello current Azure version returns an array containing all hello account keys.</span></span>
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
   <span data-ttu-id="689b6-162">如需詳細資訊，請參閱 [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0)。</span><span class="sxs-lookup"><span data-stu-id="689b6-162">For more information, see [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0).</span></span>

## <a name="azure-cli"></a><span data-ttu-id="689b6-163">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="689b6-163">Azure CLI</span></span>
<span data-ttu-id="689b6-164">hello Azure CLI 是 Azure 的命令列體驗來管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="689b6-164">hello Azure CLI is Azure’s command-line experience for managing Azure resources.</span></span> <span data-ttu-id="689b6-165">您可以將它安裝在 macOS、 Linux 及 Windows，並從 hello 命令列執行。</span><span class="sxs-lookup"><span data-stu-id="689b6-165">You can install it on macOS, Linux, and Windows and run it from hello command line.</span></span> 

<span data-ttu-id="689b6-166">Azure CLI 最適合用於與從 hello 命令列管理 Azure 資源和建置工作針對 hello Azure 資源管理員的自動化指令碼。</span><span class="sxs-lookup"><span data-stu-id="689b6-166">Azure CLI is optimized for managing and administering Azure resources from hello command line, and for building automation scripts that work against hello Azure Resource Manager.</span></span> <span data-ttu-id="689b6-167">它會提供許多 hello hello Azure 堆疊入口網站，包括存取大量資料中找到的相同函式。</span><span class="sxs-lookup"><span data-stu-id="689b6-167">It provides many of hello same functions found in hello Azure Stack portal, including rich data access.</span></span>

<span data-ttu-id="689b6-168">Azure Stack 需要有 Azure CLI 2.0 版。</span><span class="sxs-lookup"><span data-stu-id="689b6-168">Azure Stack requires Azure CLI version 2.0.</span></span> <span data-ttu-id="689b6-169">如需有關安裝和設定用於 Azure Stack 的 Azure CLI 詳細資訊，請參閱[安裝和設定 Azure Stack CLI](azure-stack-connect-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="689b6-169">For more information about installing and configuring Azure CLI with Azure Stack, see [Install and configure Azure Stack CLI](azure-stack-connect-cli.md).</span></span> <span data-ttu-id="689b6-170">如需有關如何 toouse hello Azure CLI 2.0 tooperform 數個工作使用您的 Azure 堆疊儲存體帳戶中的資源，請參閱[使用 hello Azure CLI2.0 與 Azure 儲存體](../storage/storage-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="689b6-170">For more information about how toouse hello Azure CLI 2.0 tooperform several tasks working with resources in your Azure Stack Storage account, see [Using hello Azure CLI2.0 with Azure Storage](../storage/storage-azure-cli.md)</span></span>

### <a name="azure-cli-sample-script-for-azure-stack"></a><span data-ttu-id="689b6-171">適用於 Azure Stack 的 Azure CLI 範例指令碼</span><span class="sxs-lookup"><span data-stu-id="689b6-171">Azure CLI sample script for Azure Stack</span></span> 
<span data-ttu-id="689b6-172">一旦您完成 hello CLI 安裝與設定，您可以嘗試下列與使用 Azure 堆疊儲存體資源的小殼層範例指令碼 toointeract 步驟 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="689b6-172">Once you complete hello CLI installation and configuration, you can try hello following steps toowork with a small shell sample script toointeract with Azure Stack Storage resources.</span></span> <span data-ttu-id="689b6-173">hello 指令碼會在儲存體帳戶，會先建立新的容器，然後上傳現有的檔案 （以 blob 的形式） toothat 容器、 列出 hello 容器中的所有 blob 和最後，下載 hello 檔案 tooa 目的地，您指定在本機電腦上的資料。</span><span class="sxs-lookup"><span data-stu-id="689b6-173">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container, lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span> <span data-ttu-id="689b6-174">執行這個指令碼之前，請確定您已成功連接和登入 toohello 目標 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="689b6-174">Before you run this script, make sure you successfully connect and login toohello target Azure Stack.</span></span> 
1. <span data-ttu-id="689b6-175">開啟您偏好的文字編輯器 中，然後複製並貼到 hello 編輯器上述指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="689b6-175">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>
2. <span data-ttu-id="689b6-176">更新 hello 指令碼變數 tooreflect 組態設定。</span><span class="sxs-lookup"><span data-stu-id="689b6-176">Update hello script's variables tooreflect your configuration settings.</span></span> 
3. <span data-ttu-id="689b6-177">更新 hello 必要變數之後，儲存 hello 指令碼，並結束編輯器。</span><span class="sxs-lookup"><span data-stu-id="689b6-177">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="689b6-178">hello 接下來的步驟假設您已為指令碼 my_storage_sample.sh 命名。</span><span class="sxs-lookup"><span data-stu-id="689b6-178">hello next steps assume you've named your script my_storage_sample.sh.</span></span>
4. <span data-ttu-id="689b6-179">如有必要，請標示 hello 做為可執行檔的指令碼：`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="689b6-179">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>
5. <span data-ttu-id="689b6-180">執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="689b6-180">Execute hello script.</span></span> <span data-ttu-id="689b6-181">例如，在 Bash 中：`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="689b6-181">For example, in Bash: `./my_storage_sample.sh`</span></span>

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

echo "Creating hello resource group..."
az group create --name $AZURESTACK_RESOURCE_GROUP --location $AZURESTACK_RG_LOCATION

echo "Creating hello storage account..."
az storage account create --name $AZURESTACK_STORAGE_ACCOUNT_NAME --resource-group $AZURESTACK_RESOURCE_GROUP --account-type Standard_LRS

echo "Creating hello blob container..."
az storage container create --name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Uploading hello file..."
az storage blob upload --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --file $FILE_TO_UPLOAD --name $AZURESTACK_STORAGE_BLOB_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME

echo "Listing hello blobs..."
az storage blob list --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --output table

echo "Downloading hello file..."
az storage blob download --container-name $AZURESTACK_STORAGE_CONTAINER_NAME --account-name $AZURESTACK_STORAGE_ACCOUNT_NAME --name $AZURESTACK_STORAGE_BLOB_NAME --file $DESTINATION_FILE --output table

echo "Done"
```

## <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="689b6-182">Microsoft Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="689b6-182">Microsoft Azure Storage Explorer</span></span>

<span data-ttu-id="689b6-183">Microsoft Azure 儲存體總管是 Windows 提供的獨立應用程式。</span><span class="sxs-lookup"><span data-stu-id="689b6-183">Microsoft Azure Storage Explorer is a standalone app from Microsoft.</span></span> <span data-ttu-id="689b6-184">它可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 儲存體和 Azure 堆疊儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="689b6-184">It allows you tooeasily work with both Azure Storage and Azure Stack Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="689b6-185">如果您想要輕鬆 toomanage Azure 堆疊儲存資料，請考慮使用 Microsoft Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="689b6-185">If you want an easy way toomanage your Azure Stack Storage data, then consider using Microsoft Azure Storage Explorer.</span></span>

<span data-ttu-id="689b6-186">如需設定 Azure 儲存體總管 toowork Azure 堆疊的詳細資訊，請參閱[連接儲存體總管 tooan 堆疊 Azure 訂用帳戶](azure-stack-storage-connect-se.md)。</span><span class="sxs-lookup"><span data-stu-id="689b6-186">For more information about configuring Azure Storage Explorer toowork with Azure Stack, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack-storage-connect-se.md).</span></span>

<span data-ttu-id="689b6-187">如需有關 Microsoft Azure 儲存體總管的詳細資訊，請參閱[開始使用儲存體總管 (預覽)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="689b6-187">For more information about Microsoft Azure Storage Explorer, see [Get started with Storage Explorer (Preview)](../vs-azure-tools-storage-manage-with-storage-explorer.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="689b6-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="689b6-188">Next steps</span></span>
* [<span data-ttu-id="689b6-189">連接儲存體總管 tooan 堆疊 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="689b6-189">Connect Storage Explorer tooan Azure Stack subscription</span></span>](azure-stack-storage-connect-se.md)
* [<span data-ttu-id="689b6-190">開始使用儲存體總管 (預覽)</span><span class="sxs-lookup"><span data-stu-id="689b6-190">Get started with Storage Explorer (Preview)</span></span>](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [<span data-ttu-id="689b6-191">與 Azure 一致的儲存體：差異與注意事項</span><span class="sxs-lookup"><span data-stu-id="689b6-191">Azure-consistent storage: differences and considerations</span></span>](azure-stack-acs-differences.md)
* [<span data-ttu-id="689b6-192">簡介 tooMicrosoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="689b6-192">Introduction tooMicrosoft Azure Storage</span></span>](../storage/common/storage-introduction.md)

