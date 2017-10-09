---
title: "aaaHow toocreate Azure 檔案共用 |Microsoft 文件"
description: "如何 toocreate Azure 的檔案共用使用 hello Azure 入口網站、 PowerShell 和 hello Azure CLI Azure 檔案儲存體中。"
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>在 Azure 檔案共用中建立檔案共用
您可以建立使用 Azure 檔案共用[Azure 入口網站](https://portal.azure.com/)hello Azure 儲存體 PowerShell cmdlet、 hello Azure 儲存體用戶端程式庫，或 hello Azure 儲存體的 REST API。在本教學課程中，您將學習：
* [Toocreate Azure 檔案共用使用 hello Azure 入口網站](#Create file share through hello Portal)
* [如何 toocreate Azure 檔案共用使用 Powershell](#Create file share using PowerShell)
* [如何 toocreate Azure 檔案共用使用 CLI](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>必要條件
toocreate Azure 檔案共用，您可以使用的儲存體帳戶已經存在，或[建立新的 Azure 儲存體帳戶](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。 toocreate 使用 PowerShell 的 Azure 檔案共用，您將需要 hello 帳號金鑰及儲存體帳戶名稱... 如果您計劃 toouse Powershell 或 CLI，您需要儲存體帳戶金鑰。

## <a name="create-file-share-through-hello-portal"></a>建立檔案共用，透過 hello 入口網站
1. **Azure 入口網站上的 [移 tooStorage 帳戶] 刀鋒視窗**:    
    ![儲存體帳戶刀鋒視窗](./media/storage-how-to-create-file-share/create-file-share-portal1.png)

2. **按一下 [新增檔案共用] 按鈕**：    
    ![按一下 hello 新增檔案共用 按鈕](./media/storage-how-to-create-file-share/create-file-share-portal2.png)

3. **提供名稱和配額。配額目前上限可以是 5TB**：    
    ![提供的名稱和所需的配額的 hello 新檔案共用](./media/storage-how-to-create-file-share/create-file-share-portal3.png)

4. **檢視新的檔案共用**：![檢視新的檔案共用](./media/storage-how-to-create-file-share/create-file-share-portal4.png)

5. **上傳檔案**![上傳檔案](./media/storage-how-to-create-file-share/create-file-share-portal5.png)

6. **瀏覽至檔案共用並管理您的目錄和檔案**：![瀏覽檔案共用](./media/storage-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>透過 PowerShell 建立檔案共用
tooprepare toouse PowerShell 中，下載並安裝 hello Azure PowerShell cmdlet。 請參閱[如何 tooinstall 和設定 Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) hello 安裝點和安裝指示。

> [!Note]  
> 建議您下載並安裝或升級 toohello 最新的 Azure PowerShell 模組。

1. **建立您的儲存體帳戶和金鑰內容**hello 內容封裝 hello 儲存體帳戶名稱和帳戶金鑰。 如需從 [Azure 入口網站](https://portal.azure.com/)複製帳戶金鑰的指示，請參閱[檢視和複製儲存體存取金鑰](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys)。

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **建立新的檔案共用**：    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> 檔案共用的 hello 名稱必須全部小寫。 如需有關為檔案共用與檔案命名的完整詳細資料，請參閱 [命名和參考共用、目錄、檔案及中繼資料](https://msdn.microsoft.com/library/azure/dn167011.aspx)。

## <a name="create-file-share-through-command-line-interface-cli"></a>透過命令列介面 (CLI) 建立檔案共用
1. **tooprepare toouse 命令列介面 (CLI)，下載並安裝 hello Azure CLI。**  
    請參閱[安裝 Azure CLI 2.0](/cli/azure/install-az-cli2.md) 和[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md)。

2. **建立您想要 toocreate hello 共用的連線字串 toohello 儲存體帳戶。**  
    取代```<storage-account>```和```<resource_group>```與儲存體帳戶名稱和資源群組在下列範例中的 hello。

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **建立檔案共用**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>後續步驟
* [連線並掛接檔案共用 - Windows](storage-how-to-use-files-windows.md)
* [連線並掛接檔案共用 - Linux](../storage-how-to-use-files-linux.md)
* [連線並掛接檔案共用 - macOS](storage-how-to-use-files-mac.md)

請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。

* [常見問題集](../storage-files-faq.md)
* [在 Windows 上進行疑難排解](storage-troubleshoot-windows-file-connection-problems.md)      
* [在 Linux 上進行疑難排解](storage-troubleshoot-linux-file-connection-problems.md)   