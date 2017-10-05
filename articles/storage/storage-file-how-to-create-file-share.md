---
title: "如何建立 Azure 檔案共用 | Microsoft Docs"
description: "如何使用 Azure 入口網站、PowerShell 和 Azure CLI 在 Azure 檔案儲存體中建立 Azure 檔案共用。"
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
ms.openlocfilehash: 10da4d903eaab290a6cca2c4f674548a43a70c53
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>在 Azure 檔案共用中建立檔案共用
您可以使用 [Azure 入口網站](https://portal.azure.com/)、Azure 儲存體 PowerShell Cmdlet、Azure 儲存體用戶端程式庫或 Azure 儲存體 REST API 來建立 Azure 檔案共用。在本教學課程中，您將了解：
* [如何使用 Azure 入口網站建立 Azure 檔案共用](#Create file share through the Portal)
* [如何使用 Powershell 建立 Azure 檔案共用](#Create file share using PowerShell)
* [如何使用 CLI 建立 Azure 檔案共用](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>必要條件
若要建立 Azure 檔案共用，您可以使用已經存在的儲存體帳戶，或[建立新的 Azure 儲存體帳戶](storage-create-storage-account.md)。 若要使用 PowerShell 建立 Azure 檔案共用，您需要儲存體帳戶的名稱與帳戶金鑰。 如果您打算使用 Powershell 或 CLI，您將需要儲存體帳戶金鑰。

## <a name="create-file-share-through-the-portal"></a>透過入口網站建立檔案共用
1. **前往 Azure 入口網站中的儲存體帳戶刀鋒視窗**：    
    ![儲存體帳戶刀鋒視窗](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)

2. **按一下 [新增檔案共用] 按鈕**：    
    ![按一下 [新增檔案共用] 按鈕](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)

3. **提供名稱和配額。配額目前上限可以是 5TB**：    
    ![提供新檔案共用的名稱和所需的配額](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)

4. **檢視新的檔案共用**：![檢視新的檔案共用](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)

5. **上傳檔案**![上傳檔案](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)

6. **瀏覽至檔案共用並管理您的目錄和檔案**：![瀏覽檔案共用](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>透過 PowerShell 建立檔案共用
若要準備使用 PowerShell，請下載並安裝 Azure PowerShell Cmdlet。 如需安裝點和安裝指示的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) 。

> [!Note]  
> 建議您下載和安裝或升級至最新的 Azure PowerShell 模組。

1. **建立儲存體帳戶和金鑰的內容** 內容包含儲存體帳戶名稱和帳戶金鑰。 如需從 [Azure 入口網站](https://portal.azure.com/)複製帳戶金鑰的指示，請參閱[檢視和複製儲存體存取金鑰](storage-create-storage-account.md#view-and-copy-storage-access-keys)。

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **建立新的檔案共用**：    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> 您的檔案共用名稱必須是全部小寫。 如需有關為檔案共用與檔案命名的完整詳細資料，請參閱 [命名和參考共用、目錄、檔案及中繼資料](https://msdn.microsoft.com/library/azure/dn167011.aspx)。

## <a name="create-file-share-through-command-line-interface-cli"></a>透過命令列介面 (CLI) 建立檔案共用
1. **若要準備使用命令列介面 (CLI)，請下載並安裝 Azure CLI**  
    請參閱[安裝 Azure CLI 2.0](/cli/azure/install-az-cli2.md) 和[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md)。

2. **在您要建立共用的儲存體帳戶中，建立儲存體帳戶的連接字串。**  
    使用下列範例中的儲存體帳戶名稱和資源群組來取代 ```<storage-account>``` 和 ```<resource_group>```。

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve the connection string."
    fi
    ```

3. **建立檔案共用**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>後續步驟
* [連線並掛接檔案共用 - Windows](storage-file-how-to-use-files-windows.md)
* [連線並掛接檔案共用 - Linux](storage-how-to-use-files-linux.md)
* [連線並掛接檔案共用 - macOS](storage-file-how-to-use-files-mac.md)

請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。

* [常見問題集](storage-files-faq.md)
* [疑難排解](storage-troubleshoot-file-connection-problems.md)