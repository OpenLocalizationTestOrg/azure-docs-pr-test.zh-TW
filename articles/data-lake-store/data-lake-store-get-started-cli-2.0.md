---
title: "開始使用 Azure Data Lake Store 的 aaaUse Azure 命令列 2.0 介面 tooget |Microsoft 文件"
description: "使用 Azure 跨平台命令列 2.0 toocreate Data Lake Store 帳戶以及執行基本作業"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a>使用 Azure CLI 2.0 開始使用 Azure Data Lake Store
> [!div class="op_single_selector"]
> * [入口網站](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

了解如何 toouse Azure CLI 2.0 toocreate Azure 資料湖存放區帳戶和執行基本作業，例如建立資料夾、 上傳和下載資料檔，刪除您的帳戶，依此類推。如需有關 Data Lake Store 的詳細資訊，請參閱 [Data Lake Store 概觀](data-lake-store-overview.md)。

hello Azure CLI 2.0 是 Azure 的新命令列的體驗來管理 Azure 資源。 它可以用於 macOS、Linux 和 Windows。 如需詳細資訊，請參閱 [Azure CLI 2.0 概觀](https://docs.microsoft.com/cli/azure/overview)。 您也可以查看 hello [Azure 資料湖存放區 CLI 2.0 參考](https://docs.microsoft.com/cli/azure/dls)的命令和語法的完整清單。


## <a name="prerequisites"></a>必要條件
在開始這份文件之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

* **Azure CLI 2.0** - 如需相關指示，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。

## <a name="authentication"></a>驗證

本文使用簡單的驗證方法搭配 Data Lake Store (您以使用者身分登入其中)。 hello 存取層級 tooData Lake Store 帳戶和檔案系統，然後係由 hello hello 登入的使用者存取層級。 不過，有一些其他方法為以及 tooauthenticate 與資料湖存放區，也就是**使用者驗證**或**服務對服務驗證**。 如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。


## <a name="log-in-tooyour-azure-subscription"></a>登入 tooyour Azure 訂用帳戶

1. 登入您的 Azure 訂用帳戶。

    ```azurecli
    az login
    ```

    您可以取得程式碼 toouse hello 下一個步驟中。 使用 web 瀏覽器 tooopen hello 頁面 https://aka.ms/devicelogin，然後輸入 hello 程式碼 tooauthenticate。 您已在使用您的認證提示的 toolog。

2. 一旦您登入 視窗列出所有 hello hello 與您的帳戶相關聯的 Azure 訂用帳戶。 使用下列命令 toouse 特定訂閱 hello。
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a>建立 Azure 資料湖存放區帳戶

1. 建立新的資源群組。 在 hello 下列命令，提供 hello 想 toouse 的參數值。 如果 hello 位置名稱包含空格，請將它放在引號中。 例如 "East US 2"。 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. 建立 hello Data Lake Store 帳戶。
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a>在 Data Lake Store 帳戶中建立資料夾

您可以在您的 Azure Data Lake Store 帳戶 toomanage 下建立資料夾，並儲存資料。 使用下列命令 toocreate 資料夾稱為的 hello **mynewfolder**根目錄 hello hello 資料湖存放區。

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> hello`--folder`參數可確保 hello 命令會建立一個資料夾。 如果這個參數不存在，hello 命令會建立空的檔案稱為 mynewfolder 根目錄 hello hello Data Lake Store 帳戶。
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a>上傳資料 tooa Data Lake Store 帳戶

您可以上傳資料 tooData 湖存放區，直接在 hello 根層級或 tooa 資料夾 hello 帳戶中建立。 下列的 hello 片段會示範如何 tooupload 某些範例資料 toohello 資料夾 (**mynewfolder**) 您建立 hello 前一節中。

如果您要尋找的一些範例資料 tooupload，您可以取得 hello**政策救護車資料**資料夾從 hello [Azure 資料湖 Git 儲存機制](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)。 下載 hello 檔案，並將它儲存在您的電腦，例如 C:\sampledata\ 上的本機目錄。

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> Hello 目的地，您必須指定 hello 包括 hello 檔案名稱的完整路徑。
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a>在 Data Lake Store 帳戶中列出檔案

使用下列命令 toolist hello 檔案 Data Lake Store 帳戶中的 hello。

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

這個 hello 輸出應該類似 toohello 下列：

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a>重新命名、下載與刪除 Data Lake Store 帳戶中的資料 

* **toorename 檔案**，使用下列命令的 hello:
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* **toodownload 檔案**，使用下列命令的 hello。 請確定您已經指定 hello 目的地路徑存在。
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > 如果不存在，hello 命令會建立 hello 目的地資料夾。
    > 
    >

* **toodelete 檔案**，使用下列命令的 hello:
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    如果您想 toodelete hello 資料夾**mynewfolder**和 hello 檔案**vehicle1_09142014_copy.csv**一起在一個命令中，使用 hello-recurse 參數

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a>處理 Data Lake Store 帳戶的權限和 ACL

本節中您了解如何 toomanage Acl 和使用 Azure CLI 2.0 的權限。 如需 ACL 如何在 Azure Data Lake Store 中實作的詳細討論，請參閱 [Azure Data Lake Store 中的存取控制](data-lake-store-access-control.md)。

* **tooupdate hello 的擁有者的檔案/資料夾**，使用下列命令的 hello:

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* **tooupdate hello 檔案/資料夾權限**，使用下列命令的 hello:

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* **指定路徑的 tooget hello Acl**，使用下列命令的 hello:

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    hello 輸出應類似 toohello 下列：

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* **tooset 的 acl 項目**，使用下列命令的 hello:

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* **tooremove 的 acl 項目**，使用下列命令的 hello:

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* **tooremove 整份預設 ACL**，使用下列命令的 hello:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* **整個非預設 ACL tooremove**，使用下列命令的 hello:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a>刪除 Data Lake Store 帳戶
使用下列命令 toodelete Data Lake Store 帳戶的 hello。

```azurecli
az dls account delete --account mydatalakestore
```

出現提示時，輸入**Y** toodelete hello 帳戶。

## <a name="next-steps"></a>後續步驟

* [Azure Data Lake Store CLI 2.0 參考](https://docs.microsoft.com/cli/azure/dls)
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配 Data Lake Store 使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
