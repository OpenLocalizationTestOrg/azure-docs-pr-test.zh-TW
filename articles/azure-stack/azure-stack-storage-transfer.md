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
# <a name="tools-for-azure-stack-storage"></a>Azure Stack 儲存體適用的工具

Microsoft Azure 堆疊提供一組 hello 儲存體服務，如磁碟、 blob、 資料表、 佇列和帳戶管理功能。 如果您想 toomanage 或移動資料 tooor 從 Azure 堆疊儲存體，您可以使用一組 Azure 儲存體工具。 本文章提供可用的 hello 工具的快速概觀。

最適合您的 hello 工具取決於您的需求：
* [AzCopy](#azcopy)

    儲存區特定命令列公用程式，您可以下載 toocopy 資料從一個物件 tooanother 儲存體帳戶內或之間的儲存體帳戶。

* [Azure PowerShell](#azure-powershell)

    工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。

* [Azure CLI](#azure-cli)

    可提供一組命令使用 hello Azure 和 Azure 堆疊平台的開放原始碼、 跨平台工具。

* [Microsoft 儲存體總管 (預覽)](#microsoft-azure-storage-explorer)

    輕鬆 toouse 獨立應用程式，但使用者介面。

由於 toohello Azure 和 Azure 堆疊之間的儲存體服務存在差異，可能會有一些特定的需求，每個工具 hello 下列各節中所述。 如需 Azure Stack 儲存體和 Azure 儲存體之間的比較，請參閱 [Azure Stack 儲存體：差異與注意事項](azure-stack-acs-differences.md)。


## <a name="azcopy"></a>AzCopy
AzCopy 是從 Microsoft Azure Blob 和資料表儲存體使用簡單的命令，以獲得最佳效能的設計的命令列公用程式 toocopy 資料 tooand。 儲存體帳戶內或之間的儲存體帳戶，您可以從一個物件 tooanother 複製資料。 有兩個版本的 hello AzCopy： 在 Windows 和 Linux 上的 AzCopy 上 AzCopy。 Azure 堆疊只支援 Windows hello 的版本。 
 
### <a name="download-and-install-azcopy"></a>下載並安裝 AzCopy 
[下載](https://aka.ms/azcopyforazurestack)Azure 堆疊的 AzCopy hello 支援 Windows 版本。 您可以安裝和使用 AzCopy 上 Azure 堆疊 hello Azure 與相同的方式。 詳細資訊，請參閱 toolearn [hello AzCopy 命令列公用程式使用傳輸資料](../storage/common/storage-use-azcopy.md)。 

### <a name="azcopy-command-examples-for-data-transfer"></a>資料傳輸適用的 AzCopy 命令範例
hello 遵循範例示範如何從 Azure 堆疊 blob 複製資料 tooand 的一些典型狀況。 詳細資訊，請參閱 toolearn [hello AzCopy 命令列公用程式使用傳輸資料](../storage/storage-use-azcopy.md)。 
#### <a name="download-all-blobs-toolocal-disk"></a>下載所有 blob toolocal 磁碟
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-toovirtual-directory"></a>單一檔案上傳 toovirtual 目錄 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a>在 Azure 和 Azure Stack 儲存體之間移動資料 
不支援在 Azure 儲存體和 Azure Stack 之間的非同步資料傳輸。 您需要 toospecify hello 傳輸以 hello`/SyncCopy`選項。 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a>Azcopy 的已知問題
* 檔案儲存體還無法在 Azure Stack 中使用，因此檔案儲存體上沒有任何可用的 AzCopy 作業。
* 不支援在 Azure 儲存體和 Azure Stack 之間的非同步資料傳輸。 您可以指定 hello 傳輸以 hello`/SyncCopy`選項 toocopy hello 資料。
* Azcopy hello Linux 版本不支援 Azure 堆疊儲存體。 

## <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell 是一個模組，可提供管理 Azure 和 Azure Stack 上服務的 Cmdlet。 此模組為工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。

### <a name="install-and-configure-powershell-for-azure-stack"></a>安裝及設定用於 Azure Stack 的 PowerShell
Azure 堆疊相容 Azure PowerShell 模組是與 Azure 堆疊的必要的 toowork。 如需詳細資訊，請參閱[安裝 PowerShell Azure 堆疊以](azure-stack-powershell-install.md)和[設定 hello Azure 堆疊使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md)toolearn 更多。

### <a name="powershell-sample-script-for-azure-stack"></a>適用於 Azure Stack 的 PowerShell 範例指令碼 
此範例假設您已成功[安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)。 此指令碼會協助您 conplete hello 組態，並要求您的 Azure 堆疊租用戶認證 tooadd 您帳戶 toohello 本機 PowerShell environemnt。 然後，hello 指令碼會設定 hello 預設 Azure 訂用帳戶，在 Azure 中建立新的儲存體帳戶，在這個新的儲存體帳戶中建立新的容器並上傳現有的映像檔案 (blob) toothat 容器。 Hello 指令碼會列出該容器中的所有 blob 之後，它會在本機電腦中建立新的目的地目錄，並下載 hello 映像檔案。

1. 安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。  
2. 下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。  
3. 開啟**Windows PowerShell ISE**和**系統管理員身分執行**，按一下 **檔案** > **新增**toocreate 新的指令碼檔。
4. 複製下列 hello 指令碼並貼上 toohello 新指令碼檔。
5. 更新您的組態設定為基礎的 hello 指令碼變數。 
6. 注意： 此指令碼有執行 hello 根目錄下的 toobe 下載**AzureStack_Tools**。 

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

### <a name="powershell-known-issues"></a>PowerShell 的已知問題 
hello 目前相容 Azure PowerShell 模組版本的 Azure 堆疊是 1.2.10。 它與不同的 Azure PowerShell hello 最新版本。 此差異會影響儲存體服務作業：

* hello 的傳回值格式`Get-AzureRmStorageAccountKey`版本 1.2.10 有兩個屬性：`Key1`和`Key2`，而目前 Azure 版本以 hello 傳回陣列，其中包含所有 hello account 索引鍵。
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
   如需詳細資訊，請參閱 [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0)。

## <a name="azure-cli"></a>Azure CLI
hello Azure CLI 是 Azure 的命令列體驗來管理 Azure 資源。 您可以將它安裝在 macOS、 Linux 及 Windows，並從 hello 命令列執行。 

Azure CLI 最適合用於與從 hello 命令列管理 Azure 資源和建置工作針對 hello Azure 資源管理員的自動化指令碼。 它會提供許多 hello hello Azure 堆疊入口網站，包括存取大量資料中找到的相同函式。

Azure Stack 需要有 Azure CLI 2.0 版。 如需有關安裝和設定用於 Azure Stack 的 Azure CLI 詳細資訊，請參閱[安裝和設定 Azure Stack CLI](azure-stack-connect-cli.md)。 如需有關如何 toouse hello Azure CLI 2.0 tooperform 數個工作使用您的 Azure 堆疊儲存體帳戶中的資源，請參閱[使用 hello Azure CLI2.0 與 Azure 儲存體](../storage/storage-azure-cli.md)

### <a name="azure-cli-sample-script-for-azure-stack"></a>適用於 Azure Stack 的 Azure CLI 範例指令碼 
一旦您完成 hello CLI 安裝與設定，您可以嘗試下列與使用 Azure 堆疊儲存體資源的小殼層範例指令碼 toointeract 步驟 toowork hello。 hello 指令碼會在儲存體帳戶，會先建立新的容器，然後上傳現有的檔案 （以 blob 的形式） toothat 容器、 列出 hello 容器中的所有 blob 和最後，下載 hello 檔案 tooa 目的地，您指定在本機電腦上的資料。 執行這個指令碼之前，請確定您已成功連接和登入 toohello 目標 Azure 堆疊。 
1. 開啟您偏好的文字編輯器 中，然後複製並貼到 hello 編輯器上述指令碼的 hello。
2. 更新 hello 指令碼變數 tooreflect 組態設定。 
3. 更新 hello 必要變數之後，儲存 hello 指令碼，並結束編輯器。 hello 接下來的步驟假設您已為指令碼 my_storage_sample.sh 命名。
4. 如有必要，請標示 hello 做為可執行檔的指令碼：`chmod +x my_storage_sample.sh`
5. 執行 hello 指令碼。 例如，在 Bash 中：`./my_storage_sample.sh`

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

## <a name="microsoft-azure-storage-explorer"></a>Microsoft Azure 儲存體總管

Microsoft Azure 儲存體總管是 Windows 提供的獨立應用程式。 它可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 儲存體和 Azure 堆疊儲存體資料。 如果您想要輕鬆 toomanage Azure 堆疊儲存資料，請考慮使用 Microsoft Azure 儲存體總管。

如需設定 Azure 儲存體總管 toowork Azure 堆疊的詳細資訊，請參閱[連接儲存體總管 tooan 堆疊 Azure 訂用帳戶](azure-stack-storage-connect-se.md)。

如需有關 Microsoft Azure 儲存體總管的詳細資訊，請參閱[開始使用儲存體總管 (預覽)](../vs-azure-tools-storage-manage-with-storage-explorer.md)

## <a name="next-steps"></a>後續步驟
* [連接儲存體總管 tooan 堆疊 Azure 訂用帳戶](azure-stack-storage-connect-se.md)
* [開始使用儲存體總管 (預覽)](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [與 Azure 一致的儲存體：差異與注意事項](azure-stack-acs-differences.md)
* [簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)

