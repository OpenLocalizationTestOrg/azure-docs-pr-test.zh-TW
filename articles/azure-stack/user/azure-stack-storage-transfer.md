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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="tools-for-azure-stack-storage"></a>Azure Stack 儲存體適用的工具

適用於：Azure Stack 整合系統和 Azure Stack 開發套件

Microsoft Azure Stack 提供磁碟、Blob、資料表、佇列和帳戶管理功能適用的一組儲存體服務。 如果您要管理資料、將資料移動至 Azure Stack 儲存體，或從 Azure Stack 儲存體移動資料，就可以使用一組 Azure 儲存體工具。 本文提供可用工具的快速概觀。

最適合您的工具取決於您的需求：
* [AzCopy](#azcopy)

    可下載的儲存體專用命令列公用程式，能夠從儲存體帳戶內或是在儲存體帳戶之間，從一個物件複製資料到另一個物件。

* [Azure PowerShell](#azure-powershell)

    工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。

* [Azure CLI](#azure-cli)

    開放原始碼、跨平台的工具，可提供一組運用在 Azure 和 Azure Stack 平台上的命令。

* [Microsoft 儲存體總管 (預覽)](#microsoft-azure-storage-explorer)

    具有使用者介面且易於使用的獨立應用程式。

由於 Azure 和 Azure Stack 的儲存體服務有所不同，因此下列各節所述的各項工具可能會有一些特定的需求。 如需 Azure Stack 儲存體和 Azure 儲存體之間的比較，請參閱 [Azure Stack 儲存體：差異與注意事項](azure-stack-acs-differences.md)。


## <a name="azcopy"></a>AzCopy
AzCopy 是一個命令列公用程式，可以使用簡單命令高效率地將資料複製到和複製自 Microsoft Azure Blob 和資料表儲存體。 您可以從儲存體帳戶內或是在儲存體帳戶之間，從一個物件複製資料到另一個物件。 AzCopy 有兩個版本：Windows 上的 AzCopy 和 Linux 上的 AzCopy。 Azure Stack 僅支援 Windows 版本。 
 
### <a name="download-and-install-azcopy"></a>下載並安裝 AzCopy 
[下載](https://aka.ms/azcopyforazurestack) Azure Stack 支援的 Windows 版 AzCopy。 在 Azure Stack 和在 Azure 上安裝與使用 AzCopy 的方式一樣。 若要深入了解，請參閱[使用 AzCopy 命令列公用程式傳輸資料](../../storage/common/storage-use-azcopy.md)。 

### <a name="azcopy-command-examples-for-data-transfer"></a>資料傳輸適用的 AzCopy 命令範例
下列範例會示範一些將資料複製至 Azure Stack Blob 以及從 Azure Stack Blob 複製資料的典型案例。 若要深入了解，請參閱[使用 AzCopy 命令列公用程式傳輸資料](../../storage/storage-use-azcopy.md)。 
#### <a name="download-all-blobs-to-local-disk"></a>將所有 Blob 下載至本機磁碟
```azcopy
AzCopy.exe /source:https://myaccount.blob.local.azurestack.external/mycontainer /dest:C:\myfolder /sourcekey:<key> /S
```
#### <a name="upload-single-file-to-virtual-directory"></a>上傳單一檔案到虛擬目錄 
```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.local.azurestack.external/mycontainer/vd /DestKey:key /Pattern:abc.txt
```
#### <a name="move-data-between-azure-and-azure-stack-storage"></a>在 Azure 和 Azure Stack 儲存體之間移動資料 
不支援在 Azure 儲存體和 Azure Stack 之間的非同步資料傳輸。 您必須使用 `/SyncCopy` 選項來指定傳輸。 
```azcopy 
Azcopy /Source:https://myaccount.blob.local.azurestack.external/mycontainer /Dest:https://myaccount2.blob.core.windows.net/mycontainer2 /SourceKey:AzSKey /DestKey:Azurekey /S /SyncCopy
```

### <a name="azcopy-known-issues"></a>Azcopy 的已知問題
* 檔案儲存體還無法在 Azure Stack 中使用，因此檔案儲存體上沒有任何可用的 AzCopy 作業。
* 不支援在 Azure 儲存體和 Azure Stack 之間的非同步資料傳輸。 您可以使用 `/SyncCopy` 選項指定傳輸來複製資料。
* Azure Stack 儲存體不支援 Linux 版本的 Azcopy。 

## <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell 是一個模組，可提供管理 Azure 和 Azure Stack 上服務的 Cmdlet。 此模組為工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。

### <a name="install-and-configure-powershell-for-azure-stack"></a>安裝及設定用於 Azure Stack 的 PowerShell
您需要與 Azure Stack 相容的 Azure PowerShell 模組，才能搭配 Azure Stack 使用。 如需詳細資訊，請參閱[安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md) 和[設定 Azure Stack 使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md)以深入了解。

### <a name="powershell-sample-script-for-azure-stack"></a>適用於 Azure Stack 的 PowerShell 範例指令碼 
此範例假設您已成功[安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)。 此指令碼將協助您完成設定，並要求您的 Azure Stack 租用戶認證，以便將帳戶新增至本機 PowerShell 環境。 接著，指令碼將設定預設的 Azure 訂用帳戶、在 Azure 中建立新的儲存體帳戶、在這個新的儲存體帳戶中建立新容器，並將現有的映像檔案 (Blob) 上傳至該容器。 指令碼列出該容器中的所有 Blob 之後，它會在本機電腦中建立新的目的地目錄並下載映像檔。

1. 安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。  
2. 下載[與 Azure Stack 搭配運作所需的工具](azure-stack-powershell-download.md)。  
3. 開啟 [Windows PowerShell ISE] 和 [以系統管理員​​身分執行]，按一下 **[檔案]** > **[新增]**，以建立新的指令碼檔案。
4. 複製下列指令碼並貼到新的指令碼檔案中。
5. 根據您的組態設定，更新指令碼變數。 
6. 注意：此指令碼必須在下載的 **AzureStack_Tools** 根目錄下執行。 

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

### <a name="powershell-known-issues"></a>PowerShell 的已知問題 
Azure Stack 目前相容的 Azure PowerShell 模組版本是 1.2.10。 此版本與最新版的 Azure PowerShell 不同。 此差異會影響儲存體服務作業：

* `Get-AzureRmStorageAccountKey` 在 1.2.10 版的傳回值格式有兩個屬性：`Key1` 和 `Key2`，而目前的 Azure 版本則會傳回包含所有帳戶金鑰的陣列。
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
   如需詳細資訊，請參閱 [Get-AzureRmStorageAccountKey](https://docs.microsoft.com/powershell/module/azurerm.storage/Get-AzureRmStorageAccountKey?view=azurermps-4.1.0)。

## <a name="azure-cli"></a>Azure CLI
Azure CLI 是管理 Azure 資源的 Azure 命令列體驗。 您可以將它安裝在 macOS、Linux 及 Windows 上，並從命令列來執行。 

Azure CLI 已針對以下作業進行最佳化：從命令列管理 Azure 資源進行，以及建置可用於 Azure Resource Manager 的自動化指令碼。 它提供許多與 Azure Stack 入口網站相同的功能，包括眾多資料存取功能。

Azure Stack 需要有 Azure CLI 2.0 版。 如需有關安裝和設定用於 Azure Stack 的 Azure CLI 詳細資訊，請參閱[安裝和設定 Azure Stack CLI](azure-stack-connect-cli.md)。 如需有關如何搭配 Azure Stack 儲存體帳戶中的資源使用 Azure CLI 2.0 執行多種工作的詳細資訊，請參閱[使用 Azure CLI2.0 搭配 Azure 儲存體](../../storage/storage-azure-cli.md)

### <a name="azure-cli-sample-script-for-azure-stack"></a>適用於 Azure Stack 的 Azure CLI 範例指令碼 
完成 CLI 的安裝和設定之後，您就可以嘗試下列步驟，使用一個小殼層範例指令碼來與 Azure Stack 儲存體資源進行互動。 此指令碼會先在您的儲存體帳戶中建立一個新容器，然後將現有的檔案 (以 Blob 的形式) 上傳至該容器、列出容器中的所有 Blob，最後再將檔案下載到本機電腦上您指定的目的地。 執行此指令碼之前，請確定您已成功連線並登入目標 Azure Stack。 
1. 開啟您喜愛的文字編輯器，然後複製上述指令碼並貼入編輯器中。
2. 更新指令碼的變數以反映您的組態設定。 
3. 在您更新必要變數之後，請儲存指令碼並結束編輯器。 後續步驟假設您已將指令碼命名為 my_storage_sample.sh。
4. 如有必要，請將指令碼標示為可執行檔︰`chmod +x my_storage_sample.sh`
5. 執行指令碼。 例如，在 Bash 中：`./my_storage_sample.sh`

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

## <a name="microsoft-azure-storage-explorer"></a>Microsoft Azure 儲存體總管

Microsoft Azure 儲存體總管是 Windows 提供的獨立應用程式。 此工具可讓您在 Windows、MacOS 和 Linux 上輕鬆處理 Azure 儲存體和 Azure Stack 儲存體的資料。 如果想要輕鬆地管理您的 Azure Stack 儲存體資料，請考慮使用 Microsoft Azure 儲存體總管。

如需有關設定 Azure 儲存體總管來處理 Azure Stack 的詳細資訊，請參閱[將儲存體總管連線到 Azure Stack 訂用帳戶](azure-stack-storage-connect-se.md)。

如需有關 Microsoft Azure 儲存體總管的詳細資訊，請參閱[開始使用儲存體總管 (預覽)](../../vs-azure-tools-storage-manage-with-storage-explorer.md)

## <a name="next-steps"></a>後續步驟
* [將儲存體總管連線到 Azure Stack 訂用帳戶](azure-stack-storage-connect-se.md)
* [開始使用儲存體總管 (預覽)](../../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [與 Azure 一致的儲存體：差異與注意事項](azure-stack-acs-differences.md)
* [Microsoft Azure 儲存體簡介](../../storage/common/storage-introduction.md)

