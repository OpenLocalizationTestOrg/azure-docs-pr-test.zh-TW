---
title: "aaaUsing hello Azure CLI 1.0 搭配 Azure 儲存體 |Microsoft 文件"
description: "了解 toouse hello Azure 命令列介面 (Azure CLI) 1.0 與 Azure 儲存體 toocreate 和管理儲存體帳戶和使用 Azure blob 及檔案的方式。 hello Azure CLI 是跨平台工具"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 786f2be64875f5094f09fd6e4a47532889c3a82f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a>使用 Azure CLI 1.0 hello 與 Azure 儲存體

## <a name="overview"></a>概觀

hello Azure CLI 提供一組的開放原始碼跨平台命令來處理 hello Azure 平台。 它可提供許多相同的功能位於 hello hello [Azure 入口網站](https://portal.azure.com)也為豐富的資料存取功能。

本指南中，我們將探討如何 toouse [Azure 命令列介面 (Azure CLI)](../cli-install-nodejs.md) tooperform 各種開發和管理工作與 Azure 儲存體。 我們建議您下載並安裝或升級 toohello 使用本指南之前的最新 Azure CLI。

本指南假設您已了解 hello 的 Azure 儲存體的基本概念。 hello 指南提供的指令碼數目的 hello 與 Azure 儲存體的 Azure CLI toodemonstrate hello 使用量。 為確定 tooupdate hello 指令碼變數，根據您的設定，才能執行每個指令碼。

> [!NOTE]
> hello 指南提供傳統儲存體帳戶的 hello Azure CLI 命令和指令碼範例。 請參閱[使用 hello Mac、 Linux 和 Windows Azure 資源管理與 Azure CLI](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)資源管理員的儲存體帳戶的 Azure CLI 命令。
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a>開始使用 Azure 儲存體和 hello Azure CLI 在 5 分鐘內
本指南使用 Ubuntu 作為範例，但其他作業系統平台也同樣能夠執行。

**新 tooAzure:**取得 Microsoft Azure 訂用帳戶和該訂用帳戶相關聯的 Microsoft 帳戶。 如需 Azure 購買選項的資訊，請參閱[免費試用](https://azure.microsoft.com/pricing/free-trial/)、[購買選項](https://azure.microsoft.com/pricing/purchase-options/)和[會員優惠](https://azure.microsoft.com/pricing/member-offers/) (適用於 MSDN、Microsoft 合作夥伴網路、BizSpark 和其他 Microsoft 方案的成員)。

如需 Azure 訂用帳戶的詳細資訊，請參閱 [在 Azure Active Directory (Azure AD) 中指派系統管理員角色](https://msdn.microsoft.com/library/azure/hh531793.aspx) 。

**建立 Microsoft Azure 訂用帳戶和帳戶之後：**

1. 下載並安裝 Azure CLI hello 指示中所述的 hello[安裝 hello Azure CLI](../cli-install-nodejs.md)。
2. 一旦 hello Azure CLI 安裝之後，您將無法 toouse hello azure 命令列介面 （Bash，終端機，命令提示字元） tooaccess hello Azure CLI 命令的命令。 型別 hello _azure_命令，而且您應該會看到下列輸出的 hello。

    ![Azure 命令輸出][Image1]
3. 在 hello 命令列介面中，輸入`azure storage`所有 toolist hello azure 儲存體命令，並取得 hello 功能 hello Azure CLI 提供第一印象。 您可以輸入命令名稱**-h**參數 (例如， `azure storage share create -h`) toosee 的命令語法的詳細資料。
4. 現在，我們會提供簡單的指令碼會顯示基本 Azure CLI 命令 tooaccess Azure 儲存體。 hello 指令碼會先要求您 tooset 兩個變數提供您的儲存體帳戶和金鑰。 然後，hello 指令碼會在這個新的儲存體帳戶中建立新的容器，並上傳現有的映像檔案 (blob) toothat 容器。 Hello 指令碼會列出該容器中的所有 blob 之後，它會下載 hello 映像檔案 toohello 目的地目錄已存在 hello 本機電腦上。

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. 在您的本機電腦上，開啟您慣用的文字編輯器 (例如 vim)。 在文字編輯器中輸入 hello 上述指令碼。
6. 現在，您必須根據您的組態設定 tooupdate hello 指令碼變數。

   * **< Storage_account_name >**使用給定名稱 hello 指令碼中的 hello 或輸入您的儲存體帳戶的新名稱。 **重要事項：** hello hello 儲存體帳戶名稱必須是唯一在 Azure 中。 而且必須是小寫字母！
   * **< storage_account_key >** hello 的儲存體帳戶的存取金鑰。
   * **< Container_name >**使用給定名稱 hello 指令碼中的 hello 或輸入您的容器的新名稱。
   * **< Image_to_upload >**您本機電腦上，輸入路徑 tooa 圖片，例如:"~ / images/HelloWorld.png"。
   * **< Destination_folder >** Enter 路徑 tooa 本機目錄 toostore 下載檔案，從 Azure 儲存體，例如:"~/downloadImages"。
7. 更新 vim 中的 hello 必要變數之後，按下按鍵組合`ESC`， `:`， `wq!` toosave hello 指令碼。
8. toorun 此指令碼，只要類型 hello 指令碼檔案名稱 hello bash 主控台中。 執行這個指令碼之後，您應該有包含 hello 下載映像檔的本機目的資料夾。 下列螢幕擷取畫面的 hello 顯示範例輸出：

Hello 指令碼執行之後，您應該有包含 hello 下載映像檔的本機目的資料夾。

## <a name="manage-storage-accounts-with-hello-azure-cli"></a>管理儲存體帳戶以 hello Azure CLI
### <a name="connect-tooyour-azure-subscription"></a>連接 tooyour Azure 訂用帳戶
雖然大部分 hello 儲存命令的運作時不會具有 Azure 訂用帳戶，但建議您從 hello Azure CLI tooconnect tooyour 訂用帳戶。 tooconfigure hello Azure CLI toowork 與您的訂用帳戶，請依照下列中的 hello 步驟[tooan Azure 訂用帳戶連線從 hello Azure CLI](../xplat-cli-connect.md)。

### <a name="create-a-new-storage-account"></a>建立新的儲存體帳戶
toouse Azure 儲存體，您需要儲存體帳戶。 設定您的電腦 tooconnect tooyour 訂用帳戶之後，您可以建立新的 Azure 儲存體帳戶。

```azurecli
azure storage account create <account_name>
```

hello 您的儲存體帳戶名稱必須介於 3 到 24 個字元的長度，並使用數字和小寫的字母。

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a>在環境變數中設定預設 Azure 儲存體帳戶
您可以在訂用帳戶中有多個儲存體帳戶。 您可以選擇其中一個，並將它設定在 hello 環境變數的所有 hello 存放裝置中的都命令 hello 相同工作階段。 這可讓您 toorun hello Azure CLI 儲存命令，而不指定 hello 儲存體帳戶，以及明確金鑰。

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

另一個方式 tooset 預設儲存體帳戶正在使用連接字串。 首先命令以取得 hello 連接字串：

```azurecli
azure storage account connectionstring show <account_name>
```

然後將複製 hello 輸出連接字串，並將它設定 tooenvironment 變數：

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a>建立和管理 Blob
Azure Blob 儲存體是用於儲存大量非結構化資料，例如文字或二進位資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。 本節假設您已熟悉 hello Azure Blob 儲存體概念。 如需詳細資訊，請參閱[使用 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)和 [Blob 服務概念](http://msdn.microsoft.com/library/azure/dd179376.aspx)。

### <a name="create-a-container"></a>建立容器
Azure 儲存體中的每個 Blob 必須位於一個容器中。 您可以建立私用容器使用 hello`azure storage container create`命令：

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> 匿名讀取權限有三個層級：**Off**、**Blob** 和 **Container**。 tooprevent 匿名存取 tooblobs，集 hello 權限的參數太**關閉**。 根據預設，hello 新容器是私人的而且只有 hello 帳戶擁有者可存取。 tooallow 匿名公用讀取存取 tooblob 資源，但不是 toocontainer 中繼資料或 toohello 清單 hello 容器中的 blob、 設定 hello 權限的參數太**Blob**。 tooallow 完整公用讀取存取 tooblob 資源、 容器中繼資料及 hello hello 容器中的 blob 清單中，設定 hello 權限的參數太**容器**。 如需詳細資訊，請參閱[管理匿名讀取權限 toocontainers 和 blob](storage-manage-access-to-resources.md)。
>
>

### <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。 如需詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。

tooupload tooa 容器中的 blob，您可以使用 hello `azure storage blob upload`。 根據預設，此命令會將 hello 本機檔案 tooa 區塊 blob 上傳。 toospecify hello hello blob 類型，您可以使用 hello`--blobtype`參數。

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a>從容器下載 Blob
下列範例中的 hello 示範 toodownload 從容器的 blob。

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a>複製 Blob
您可以在儲存體帳戶內或在不同儲存體帳戶和區域之間，以非同步方式複製 Blob。

hello 下列範例示範如何從一個儲存體 toocopy blob 帳戶 tooanother。 在此範例中，我們建立 Blob 為公開，可匿名存取的容器。

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

此範例會執行非同步複製。 您可以監視每個複製作業的 hello 狀態執行 hello`azure storage blob copy show`作業。

請注意，hello 複製作業所提供的 hello 來源 URL 必須可公開存取，或包含 SAS （共用的存取簽章） 權杖。

### <a name="delete-a-blob"></a>刪除 Blob
toodelete blob，使用下列命令 hello:

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a>建立和管理檔案共用
Azure 檔案儲存體提供共用存放裝置使用 hello 標準 SMB 通訊協定的應用程式。 Microsoft Azure 虛擬機器和雲端服務，以及內部部署應用程式，可以透過掛接共用，共用檔案資料。 您可以管理檔案共用和檔案資料，透過 hello Azure CLI。 如需 Azure 檔案儲存體的詳細資訊，請參閱[開始使用 Azure 檔案儲存在 Windows 上](storage-dotnet-how-to-use-files.md)或[如何 toouse Linux 的 Azure 檔案儲存體](storage-how-to-use-files-linux.md)。

### <a name="create-a-file-share"></a>建立檔案共用
Azure 檔案共用是 Azure 中的 SMB 檔案共用。 所有目錄和檔案都必須在檔案共用中建立。 帳戶可以包含無限的數目的共用，並共用可以存放無限的數量的檔案，向上 toohello hello 儲存體帳戶的容量限制。 hello 下列範例會建立名為的檔案共用**myshare**。

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a>建立目錄
目錄會提供 Azure 檔案共用選擇性的階層式結構。 hello 下列範例會建立一個名為目錄**myDir** hello 檔案共用中。

```azurecli
azure storage directory create myshare myDir
```

請注意，目錄路徑可包含多個層級，例如 **a/b**。 不過，您必須確定所有父目錄都存在。 例如，如果路徑是 **a/b**，您必須先建立目錄 **a**，然後再建立目錄 **b**。

### <a name="upload-a-local-file-toodirectory"></a>上傳本機檔案 toodirectory
hello 例會將檔案上傳從**~/temp/samplefile.txt** toohello **myDir**目錄。 編輯 hello 檔案路徑，使它所指 tooa 有效的檔案在本機電腦上：

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

請注意，在 hello 共用的檔案可以是 up too1 TB 的大小。

### <a name="list-hello-files-in-hello-share-root-or-directory"></a>列出 hello 共用根目錄或目錄中的 hello 檔案
您可以列出 hello 檔案和子目錄的共用根目錄或使用下列命令的 hello 目錄中：

```azurecli
azure storage file list myshare myDir
```

請注意該 hello 目錄名稱是選擇性的 hello 列出作業。 如果省略，則 hello 命令會列出 hello hello 根目錄 hello 共用的內容。

### <a name="copy-files"></a>複製檔案
開始使用 Azure CLI 0.9.8 版，您可以複製檔案 tooanother 檔案、 檔案 tooa blob 或 blob tooa 檔案。 下面我們將示範如何 tooperform 這些複製使用 CLI 命令的作業。 toocopy toohello 新檔案的目錄：

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

toocopy blob tooa 檔案目錄：

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a>後續步驟

您可以在下列網頁找到可與「儲存體」資源搭配運作的 Azure CLI 1.0 命令參考資料：

* [Resource Manager 模式中的 Azure CLI 命令](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [Azure 服務管理模式中的 Azure CLI 命令](../cli-install-nodejs.md)

您可能也要 tootry hello [Azure CLI 2.0](storage-azure-cli.md)、 撰寫搭配 hello Resource Manager 部署模型使用 Python，我們下一代 CLI。

[Image1]: ./media/storage-azure-cli/azure_command.png
