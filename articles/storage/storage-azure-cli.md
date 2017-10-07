---
title: "aaaUsing hello 與 Azure 儲存體的 Azure CLI 2.0 |Microsoft 文件"
description: "了解 toouse hello Azure 命令列介面 (Azure CLI) 2.0 與 Azure 儲存體 toocreate 和管理儲存體帳戶和使用 Azure blob 及檔案的方式。 hello Azure CLI 2.0 是以 Python 撰寫的跨平台工具。"
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 38402373dcd87f1ef05471a02353c77d58f1a9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a>使用 Azure CLI 2.0 hello 與 Azure 儲存體

hello 開放原始碼、 跨平台 Azure CLI 2.0 提供一組命令使用 hello Azure 平台。 它可提供許多相同的功能位於 hello hello [Azure 入口網站](https://portal.azure.com)，包括豐富的資料存取。

在本指南中，我們會示範如何 toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform 幾項工作使用您的 Azure 儲存體帳戶中的資源。 我們建議您下載並安裝或升級使用本指南之前的 hello CLI 2.0 toohello 最新版本。

hello 指南中的 hello 範例假設 hello hello Bash 殼層 Ubuntu 上, 使用，但其他平台應該同樣地執行。 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a>必要條件
本指南假設您已了解 hello 的 Azure 儲存體的基本概念。 它也假設您使用的是可以 toosatisfy hello 帳戶建立需求下方指定的 Azure 與 hello 儲存體服務。

### <a name="accounts"></a>帳戶
* **Azure 帳戶**：如果您沒有 Azure 訂用帳戶，請[建立免費的 Azure 帳戶](https://azure.microsoft.com/free/)。
* **儲存體帳戶**：請參閱[關於 Azure 儲存體帳戶](../storage/storage-create-storage-account.md)中的[建立儲存體帳戶](../storage/storage-create-storage-account.md#create-a-storage-account)。

### <a name="install-hello-azure-cli-20"></a>安裝 hello Azure CLI 2.0

下載並安裝 hello 指示中所述的 hello Azure CLI 2.0[安裝 Azure CLI 2.0](/cli/azure/install-az-cli2)。

> [!TIP]
> 如果您有 hello 安裝問題，請參閱 hello[安裝疑難排解](/cli/azure/install-az-cli2#installation-troubleshooting)hello 文件： hello 的區段[安裝疑難排解](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md)GitHub 上的指南。
>

## <a name="working-with-hello-cli"></a>使用 CLI hello

一旦您已安裝 hello CLI，您可以使用 hello`az`命令 Bash、 終端機 （命令提示字元） 的命令列介面 tooaccess hello Azure CLI 命令。 型別 hello`az`命令 toosee hello （下列範例輸出的 hello 已截斷） 的基底命令的完整清單：

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

在命令列介面中，執行 hello 命令`az storage --help`toolist hello`storage`命令子群組。 hello 描述 hello 子群組提供 hello 功能 hello Azure CLI 提供使用儲存體資源的概觀。

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a>連接 hello CLI tooyour Azure 訂用帳戶

與您 Azure 訂用帳戶中的 hello 資源 toowork，您必須先登入 tooyour Azure 帳戶`az login`。 登入的方法有數種：

* **互動式登入**：`az login`
* **以使用者名稱和密碼登入**：`az login -u johndoe@contoso.com -p VerySecret`
  * 這不適用於 Microsoft 帳戶或使用 Multi-Factor Authentication 的帳戶。
* **登入服務主體**：`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`

## <a name="azure-cli-20-sample-script"></a>Azure CLI 2.0 範例指令碼

接下來，我們將使用一些基本 Azure CLI 2.0 命令 toointeract 發出與 Azure 儲存體資源的小型的殼層指令碼。 hello 指令碼會先在儲存體帳戶中建立新的容器，然後上傳現有的檔案 （以 blob 的形式） toothat 容器。 它接著會列出 hello 容器中的所有 blob，和最後，下載 hello 檔案 tooa 目的地，您指定在本機電腦上。

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

**設定及執行 hello 指令碼**

1. 開啟您偏好的文字編輯器 中，然後複製並貼到 hello 編輯器上述指令碼的 hello。

2. 接著，更新 hello 指令碼變數 tooreflect 組態設定。 取代為下列指定的值的 hello:

   * **\<storage_account_name\>**  hello 您的儲存體帳戶名稱。
   * **\<storage_account_key\>**  hello 儲存體帳戶的主要或次要存取金鑰。
   * **\<container_name\>** 名稱 hello 新容器 toocreate，例如"azure cli-範例-容器 」。
   * **\<blob_name\>**  hello 容器中的 hello 目的地 blob 的名稱。
   * **\<file_to_upload\>**  hello 路徑 toosmall 檔案儲存在本機電腦，例如"~ / images/HelloWorld.png"。
   * **\<destination_file\>**  hello 目的地檔案路徑，例如"~ / downloadedImage.png"。

3. 更新 hello 必要變數之後，儲存 hello 指令碼，並結束編輯器。 hello 接下來的步驟假設您已命名為您的指令碼**my_storage_sample.sh**。

4. 如有必要，請標示 hello 做為可執行檔的指令碼：`chmod +x my_storage_sample.sh`

5. 執行 hello 指令碼。 例如，在 Bash 中：`./my_storage_sample.sh`

您應看到類似 toohello 下列程式碼輸出，及 hello  **\<destination_file\>**  hello 中所指定指令碼應該會出現在本機電腦上。

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> hello 上述輸出會**資料表**格式。 您可以指定哪一個輸出格式 toouse 藉由指定 hello`--output`在 CLI 命令中的引數，或將它全域使用`az configure`。
>

## <a name="manage-storage-accounts"></a>管理儲存體帳戶

### <a name="create-a-new-storage-account"></a>建立新的儲存體帳戶
toouse Azure 儲存體，您需要儲存體帳戶。 您可以建立新的 Azure 儲存體帳戶之後您已設定您的電腦太,[連接 tooyour 訂閱](#connect-to-your-azure-subscription)。

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* `--location` [必要]：位置。 例如，「美國西部」。
* `--name`[必要]: hello 儲存體帳戶名稱。 hello 名稱必須 3 too24 個字元的長度，且只使用小寫英數字元。
* `--resource-group` [必要]：資源群組的名稱。
* `--sku`[必要]: hello SKU 的儲存體帳戶。 允許的值：
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a>設定預設 Azure 儲存體帳戶環境變數
您可以在 Azure 訂用帳戶中有多個儲存體帳戶。 其中一個 tooselect 所有後續的存放裝置的 toouse 命令，您可以設定這些環境變數：

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

另一個方式 tooset 預設儲存體帳戶是使用連接字串。 首先，取得 hello 連接字串以 hello`show-connection-string`命令：

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

複製 hello 輸出連接字串，然後設定 hello `AZURE_STORAGE_CONNECTION_STRING` （您可能需要以引號括住 tooenclose hello 連接字串） 的環境變數：

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> Hello 下列各節的這篇文章中的所有範例都假設您已設定 hello`AZURE_STORAGE_ACCOUNT`和`AZURE_STORAGE_ACCESS_KEY`環境變數。
>

## <a name="create-and-manage-blobs"></a>建立和管理 Blob
Azure Blob 儲存體是用於儲存大量非結構化資料，例如文字或二進位資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。 本節假設您已熟悉 Azure Blob 儲存體的概念。 如需詳細資訊，請參閱[使用 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)和 [Blob 服務概念](/rest/api/storageservices/blob-service-concepts)。

### <a name="create-a-container"></a>建立容器
Azure 儲存體中的每個 Blob 必須位於一個容器中。 您可以建立容器使用 hello`az storage container create`命令：

```azurecli
az storage container create --name <container_name>
```

您可以為新的容器中設定的讀取權限的三個層級的其中一個，藉由指定選擇性的 hello`--public-access`引數：

* `off`（預設值）： 容器資料為私用 toohello 帳戶擁有者。
* `blob`：Blob 的公用讀取權限。
* `container`： 公用讀取和清單存取 toohello 整個容器。

如需詳細資訊，請參閱[管理匿名讀取權限 toocontainers 和 blob](storage-manage-access-to-resources.md)。

### <a name="upload-a-blob-tooa-container"></a>上傳 blob tooa 容器
Azure Blob 儲存體支援區塊、附加和分頁 Blob。 上傳 blob tooa 容器使用 hello`blob upload`命令：

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 根據預設，hello `blob upload` *.vhd 檔案 toopage blob 或區塊 blob 否則命令將上傳。 另一個時輸入 toospecify 上傳 blob，您可以使用 hello`--type`引數--允許的值是`append`， `block`，和`page`。

 如需有關 hello 不同的 blob 類型的詳細資訊，請參閱[了解區塊 Blob、 附加 Blob 和分頁 Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs)。


### <a name="download-a-blob-from-a-container"></a>從容器下載 Blob
這個範例會示範如何 toodownload 從容器的 blob:

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a>列出容器中的 hello blob

列出在 hello 與容器中的 hello blob [az 儲存體 blob 清單](/cli/azure/storage/blob#list)命令。

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a>複製 Blob
您可以在儲存體帳戶內或在不同儲存體帳戶和區域之間，以非同步方式複製 Blob。

hello 下列範例示範如何從一個儲存體 toocopy blob 帳戶 tooanother。 我們會先建立容器 hello 來源儲存體帳戶中，指定對其 blob 的公用讀取權。 接下來，我們會將檔案 toohello 容器和最後，從該容器的複製 hello blob 上載到 hello 目的地儲存體帳戶中的容器。

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

在上述範例中的 hello，hello 目的地容器必須已存在於 hello 複製作業 toosucceed hello 目的地儲存體帳戶。 此外，hello 來源 blob 中 hello 指定`--source-uri`引數必須包含共用的存取簽章 (SAS) 權杖，或為可公開存取，如此範例所示。

### <a name="delete-a-blob"></a>刪除 Blob
toodelete blob，使用 hello`blob delete`命令：

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a>建立和管理檔案共用
Azure 檔案儲存體提供共用存放裝置使用 hello 伺服器訊息區塊 (SMB) 通訊協定的應用程式。 Microsoft Azure 虛擬機器和雲端服務，以及內部部署應用程式，可以透過掛接共用，共用檔案資料。 您可以管理檔案共用和檔案資料，透過 hello Azure CLI。 如需 Azure 檔案儲存體的詳細資訊，請參閱[開始使用 Azure 檔案儲存在 Windows 上](storage-dotnet-how-to-use-files.md)或[如何 toouse Linux 的 Azure 檔案儲存體](storage-how-to-use-files-linux.md)。

### <a name="create-a-file-share"></a>建立檔案共用
Azure 檔案共用是 Azure 中的 SMB 檔案共用。 所有目錄和檔案都必須在檔案共用中建立。 帳戶可以包含無限的數目的共用，並共用可以存放無限的數量的檔案，向上 toohello hello 儲存體帳戶的容量限制。 hello 下列範例會建立名為的檔案共用**myshare**。

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a>建立目錄
目錄會提供 Azure 檔案共用的階層式結構。 hello 下列範例會建立一個名為目錄**myDir** hello 檔案共用中。

```azurecli
az storage directory create --name myDir --share-name myshare
```

目錄路徑可包含多個層級，例如 **dir1/dir2**。 不過，您必須先確定所有父目錄都存在，才能建立子目錄。 例如，如果路徑是 **dir1/dir2**，您必須先建立目錄 **dir1**，然後再建立目錄 **dir2**。

### <a name="upload-a-local-file-tooa-share"></a>上傳本機檔案 tooa 共用
hello 例會將檔案上傳從**~/temp/samplefile.txt**的 hello tooroot **myshare**檔案共用。 hello`--source`引數指定的現有本機檔案 tooupload hello。

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

如同目錄建立時，您可以指定 hello 共用 tooupload hello 檔案 tooan 現有目錄內 hello 共用內的目錄路徑：

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

Hello 共用中的檔案可以是 up too1 TB 的大小。

### <a name="list-hello-files-in-a-share"></a>列出的共用中的 hello 檔案
您可以使用 hello 列出中共用檔案和目錄`az storage file list`命令：

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a>複製檔案      
您可以複製檔案 tooanother 檔案、 檔案 tooa blob 或 blob tooa 檔案。 例如，toocopy 中不同的共用檔案 tooa 目錄：        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a>後續步驟
以下是進一步了解使用 Azure CLI 2.0 hello 一些額外的資源。

* [開始使用 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Azure CLI 2.0 命令參考](/cli/azure)
* [GitHub 上的 Azure CLI 2.0](https://github.com/Azure/azure-cli)
