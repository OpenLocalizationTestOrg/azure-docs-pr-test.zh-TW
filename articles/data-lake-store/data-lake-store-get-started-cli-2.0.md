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
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="62c26-103">使用 Azure CLI 2.0 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="62c26-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62c26-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="62c26-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="62c26-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="62c26-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="62c26-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="62c26-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="62c26-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="62c26-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="62c26-108">REST API</span><span class="sxs-lookup"><span data-stu-id="62c26-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="62c26-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="62c26-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="62c26-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="62c26-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="62c26-111">Python</span><span class="sxs-lookup"><span data-stu-id="62c26-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="62c26-112">了解如何 toouse Azure CLI 2.0 toocreate Azure 資料湖存放區帳戶和執行基本作業，例如建立資料夾、 上傳和下載資料檔，刪除您的帳戶，依此類推。如需有關 Data Lake Store 的詳細資訊，請參閱 [Data Lake Store 概觀](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="62c26-112">Learn how toouse Azure CLI 2.0 toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="62c26-113">hello Azure CLI 2.0 是 Azure 的新命令列的體驗來管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="62c26-113">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="62c26-114">它可以用於 macOS、Linux 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="62c26-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="62c26-115">如需詳細資訊，請參閱 [Azure CLI 2.0 概觀](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="62c26-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="62c26-116">您也可以查看 hello [Azure 資料湖存放區 CLI 2.0 參考](https://docs.microsoft.com/cli/azure/dls)的命令和語法的完整清單。</span><span class="sxs-lookup"><span data-stu-id="62c26-116">You can also look at hello [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="62c26-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="62c26-117">Prerequisites</span></span>
<span data-ttu-id="62c26-118">在開始這份文件之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="62c26-118">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="62c26-119">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="62c26-119">**An Azure subscription**.</span></span> <span data-ttu-id="62c26-120">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="62c26-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="62c26-121">**Azure CLI 2.0** - 如需相關指示，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="62c26-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="62c26-122">驗證</span><span class="sxs-lookup"><span data-stu-id="62c26-122">Authentication</span></span>

<span data-ttu-id="62c26-123">本文使用簡單的驗證方法搭配 Data Lake Store (您以使用者身分登入其中)。</span><span class="sxs-lookup"><span data-stu-id="62c26-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="62c26-124">hello 存取層級 tooData Lake Store 帳戶和檔案系統，然後係由 hello hello 登入的使用者存取層級。</span><span class="sxs-lookup"><span data-stu-id="62c26-124">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="62c26-125">不過，有一些其他方法為以及 tooauthenticate 與資料湖存放區，也就是**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="62c26-125">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="62c26-126">如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="62c26-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="62c26-127">登入 tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="62c26-127">Log in tooyour Azure subscription</span></span>

1. <span data-ttu-id="62c26-128">登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="62c26-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="62c26-129">您可以取得程式碼 toouse hello 下一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="62c26-129">You get a code toouse in hello next step.</span></span> <span data-ttu-id="62c26-130">使用 web 瀏覽器 tooopen hello 頁面 https://aka.ms/devicelogin，然後輸入 hello 程式碼 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="62c26-130">Use a web browser tooopen hello page https://aka.ms/devicelogin and enter hello code tooauthenticate.</span></span> <span data-ttu-id="62c26-131">您已在使用您的認證提示的 toolog。</span><span class="sxs-lookup"><span data-stu-id="62c26-131">You are prompted toolog in using your credentials.</span></span>

2. <span data-ttu-id="62c26-132">一旦您登入 視窗列出所有 hello hello 與您的帳戶相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="62c26-132">Once you log in, hello window lists all hello Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="62c26-133">使用下列命令 toouse 特定訂閱 hello。</span><span class="sxs-lookup"><span data-stu-id="62c26-133">Use hello following command toouse a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="62c26-134">建立 Azure 資料湖存放區帳戶</span><span class="sxs-lookup"><span data-stu-id="62c26-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="62c26-135">建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="62c26-135">Create a new resource group.</span></span> <span data-ttu-id="62c26-136">在 hello 下列命令，提供 hello 想 toouse 的參數值。</span><span class="sxs-lookup"><span data-stu-id="62c26-136">In hello following command, provide hello parameter values you want toouse.</span></span> <span data-ttu-id="62c26-137">如果 hello 位置名稱包含空格，請將它放在引號中。</span><span class="sxs-lookup"><span data-stu-id="62c26-137">If hello location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="62c26-138">例如 "East US 2"。</span><span class="sxs-lookup"><span data-stu-id="62c26-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="62c26-139">建立 hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="62c26-139">Create hello Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="62c26-140">在 Data Lake Store 帳戶中建立資料夾</span><span class="sxs-lookup"><span data-stu-id="62c26-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="62c26-141">您可以在您的 Azure Data Lake Store 帳戶 toomanage 下建立資料夾，並儲存資料。</span><span class="sxs-lookup"><span data-stu-id="62c26-141">You can create folders under your Azure Data Lake Store account toomanage and store data.</span></span> <span data-ttu-id="62c26-142">使用下列命令 toocreate 資料夾稱為的 hello **mynewfolder**根目錄 hello hello 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="62c26-142">Use hello following command toocreate a folder called **mynewfolder** at hello root of hello Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="62c26-143">hello`--folder`參數可確保 hello 命令會建立一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="62c26-143">hello `--folder` parameter ensures that hello command creates a folder.</span></span> <span data-ttu-id="62c26-144">如果這個參數不存在，hello 命令會建立空的檔案稱為 mynewfolder 根目錄 hello hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="62c26-144">If this parameter is not present, hello command creates an empty file called mynewfolder at hello root of hello Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a><span data-ttu-id="62c26-145">上傳資料 tooa Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="62c26-145">Upload data tooa Data Lake Store account</span></span>

<span data-ttu-id="62c26-146">您可以上傳資料 tooData 湖存放區，直接在 hello 根層級或 tooa 資料夾 hello 帳戶中建立。</span><span class="sxs-lookup"><span data-stu-id="62c26-146">You can upload data tooData Lake Store directly at hello root level or tooa folder that you created within hello account.</span></span> <span data-ttu-id="62c26-147">下列的 hello 片段會示範如何 tooupload 某些範例資料 toohello 資料夾 (**mynewfolder**) 您建立 hello 前一節中。</span><span class="sxs-lookup"><span data-stu-id="62c26-147">hello snippets below demonstrate how tooupload some sample data toohello folder (**mynewfolder**) you created in hello previous section.</span></span>

<span data-ttu-id="62c26-148">如果您要尋找的一些範例資料 tooupload，您可以取得 hello**政策救護車資料**資料夾從 hello [Azure 資料湖 Git 儲存機制](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)。</span><span class="sxs-lookup"><span data-stu-id="62c26-148">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="62c26-149">下載 hello 檔案，並將它儲存在您的電腦，例如 C:\sampledata\ 上的本機目錄。</span><span class="sxs-lookup"><span data-stu-id="62c26-149">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="62c26-150">Hello 目的地，您必須指定 hello 包括 hello 檔案名稱的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="62c26-150">For hello destination, you must specify hello complete path including hello file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="62c26-151">在 Data Lake Store 帳戶中列出檔案</span><span class="sxs-lookup"><span data-stu-id="62c26-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="62c26-152">使用下列命令 toolist hello 檔案 Data Lake Store 帳戶中的 hello。</span><span class="sxs-lookup"><span data-stu-id="62c26-152">Use hello following command toolist hello files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="62c26-153">這個 hello 輸出應該類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="62c26-153">hello output of this should be similar toohello following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="62c26-154">重新命名、下載與刪除 Data Lake Store 帳戶中的資料</span><span class="sxs-lookup"><span data-stu-id="62c26-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="62c26-155">**toorename 檔案**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="62c26-155">**toorename a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="62c26-156">**toodownload 檔案**，使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="62c26-156">**toodownload a file**, use hello following command.</span></span> <span data-ttu-id="62c26-157">請確定您已經指定 hello 目的地路徑存在。</span><span class="sxs-lookup"><span data-stu-id="62c26-157">Make sure hello destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="62c26-158">如果不存在，hello 命令會建立 hello 目的地資料夾。</span><span class="sxs-lookup"><span data-stu-id="62c26-158">hello command creates hello destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="62c26-159">**toodelete 檔案**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="62c26-159">**toodelete a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="62c26-160">如果您想 toodelete hello 資料夾**mynewfolder**和 hello 檔案**vehicle1_09142014_copy.csv**一起在一個命令中，使用 hello-recurse 參數</span><span class="sxs-lookup"><span data-stu-id="62c26-160">If you want toodelete hello folder **mynewfolder** and hello file **vehicle1_09142014_copy.csv** together in one command, use hello --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="62c26-161">處理 Data Lake Store 帳戶的權限和 ACL</span><span class="sxs-lookup"><span data-stu-id="62c26-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="62c26-162">本節中您了解如何 toomanage Acl 和使用 Azure CLI 2.0 的權限。</span><span class="sxs-lookup"><span data-stu-id="62c26-162">In this section you learn about how toomanage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="62c26-163">如需 ACL 如何在 Azure Data Lake Store 中實作的詳細討論，請參閱 [Azure Data Lake Store 中的存取控制](data-lake-store-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="62c26-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="62c26-164">**tooupdate hello 的擁有者的檔案/資料夾**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="62c26-164">**tooupdate hello owner of a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="62c26-165">**tooupdate hello 檔案/資料夾權限**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="62c26-165">**tooupdate hello permissions for a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="62c26-166">**指定路徑的 tooget hello Acl**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="62c26-166">**tooget hello ACLs for a given path**, use hello following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="62c26-167">hello 輸出應類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="62c26-167">hello output should be similar toohello following:</span></span>

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

* <span data-ttu-id="62c26-168">**tooset 的 acl 項目**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="62c26-168">**tooset an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="62c26-169">**tooremove 的 acl 項目**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="62c26-169">**tooremove an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="62c26-170">**tooremove 整份預設 ACL**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="62c26-170">**tooremove an entire default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="62c26-171">**整個非預設 ACL tooremove**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="62c26-171">**tooremove an entire non-default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="62c26-172">刪除 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="62c26-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="62c26-173">使用下列命令 toodelete Data Lake Store 帳戶的 hello。</span><span class="sxs-lookup"><span data-stu-id="62c26-173">Use hello following command toodelete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="62c26-174">出現提示時，輸入**Y** toodelete hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="62c26-174">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62c26-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62c26-175">Next steps</span></span>

* [<span data-ttu-id="62c26-176">Azure Data Lake Store CLI 2.0 參考</span><span class="sxs-lookup"><span data-stu-id="62c26-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="62c26-177">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="62c26-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="62c26-178">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="62c26-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="62c26-179">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="62c26-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
