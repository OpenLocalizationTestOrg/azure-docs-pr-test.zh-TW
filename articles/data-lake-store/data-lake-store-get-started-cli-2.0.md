---
title: "使用 Azure 命令列介面 2.0 來開始使用 Azure Data Lake Store | Microsoft Docs"
description: "使用 Azure 跨平台命令列 2.0 建立 Data Lake Store 帳戶並執行基本作業"
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
ms.openlocfilehash: ed78d25f2bac0a9996f1796ee503f31a36940977
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="d65f7-103">使用 Azure CLI 2.0 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d65f7-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d65f7-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="d65f7-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="d65f7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d65f7-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="d65f7-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="d65f7-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="d65f7-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="d65f7-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="d65f7-108">REST API</span><span class="sxs-lookup"><span data-stu-id="d65f7-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="d65f7-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d65f7-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="d65f7-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="d65f7-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="d65f7-111">Python</span><span class="sxs-lookup"><span data-stu-id="d65f7-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="d65f7-112">了解如何使用 Azure CLI 2.0 建立 Azure Data Lake Store 帳戶並執行基本作業，例如建立資料夾、上傳和下載資料檔案、刪除您的帳戶等等。如需有關 Data Lake Store 的詳細資訊，請參閱 [Data Lake Store 概觀](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d65f7-112">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="d65f7-113">Azure CLI 2.0 是管理 Azure 資源的 Azure 新命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="d65f7-113">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="d65f7-114">它可以用於 macOS、Linux 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="d65f7-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="d65f7-115">如需詳細資訊，請參閱 [Azure CLI 2.0 概觀](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="d65f7-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="d65f7-116">您也可以查看 [Azure Data Lake Store CLI 2.0 參考](https://docs.microsoft.com/cli/azure/dls)以取得命令和語法的完整清單。</span><span class="sxs-lookup"><span data-stu-id="d65f7-116">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d65f7-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="d65f7-117">Prerequisites</span></span>
<span data-ttu-id="d65f7-118">開始閱讀本文之前，您必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="d65f7-118">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="d65f7-119">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="d65f7-119">**An Azure subscription**.</span></span> <span data-ttu-id="d65f7-120">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d65f7-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="d65f7-121">**Azure CLI 2.0** - 如需相關指示，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d65f7-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="d65f7-122">驗證</span><span class="sxs-lookup"><span data-stu-id="d65f7-122">Authentication</span></span>

<span data-ttu-id="d65f7-123">本文使用簡單的驗證方法搭配 Data Lake Store (您以使用者身分登入其中)。</span><span class="sxs-lookup"><span data-stu-id="d65f7-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="d65f7-124">Data Lake Store 帳戶和檔案系統的存取層級則由已登入使用者的存取層級所控管。</span><span class="sxs-lookup"><span data-stu-id="d65f7-124">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="d65f7-125">不過，還有其他方法可向 Data Lake Store 進行驗證：**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="d65f7-125">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="d65f7-126">如需有關如何驗證的指示和詳細資訊，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="d65f7-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="d65f7-127">登入您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d65f7-127">Log in to your Azure subscription</span></span>

1. <span data-ttu-id="d65f7-128">登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d65f7-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="d65f7-129">您會在下一個步驟中取得要使用的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d65f7-129">You get a code to use in the next step.</span></span> <span data-ttu-id="d65f7-130">使用網頁瀏覽器開啟 https://aka.ms/devicelogin 頁面並輸入要驗證的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d65f7-130">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span></span> <span data-ttu-id="d65f7-131">系統會提示您使用您的認證登入。</span><span class="sxs-lookup"><span data-stu-id="d65f7-131">You are prompted to log in using your credentials.</span></span>

2. <span data-ttu-id="d65f7-132">一旦您登入後，視窗會列出與您帳戶相關聯的所有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d65f7-132">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="d65f7-133">使用下列命令可使用特定訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d65f7-133">Use the following command to use a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="d65f7-134">建立 Azure Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="d65f7-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="d65f7-135">建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d65f7-135">Create a new resource group.</span></span> <span data-ttu-id="d65f7-136">在下列命令中，提供您想要使用的參數值。</span><span class="sxs-lookup"><span data-stu-id="d65f7-136">In the following command, provide the parameter values you want to use.</span></span> <span data-ttu-id="d65f7-137">如果位置名稱包含空格，請將它放在引號中。</span><span class="sxs-lookup"><span data-stu-id="d65f7-137">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="d65f7-138">例如 "East US 2"。</span><span class="sxs-lookup"><span data-stu-id="d65f7-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="d65f7-139">建立 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d65f7-139">Create the Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="d65f7-140">在 Data Lake Store 帳戶中建立資料夾</span><span class="sxs-lookup"><span data-stu-id="d65f7-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="d65f7-141">您可以在您的 Azure Data Lake Store 帳戶下建立資料夾，用於管理與存放資料。</span><span class="sxs-lookup"><span data-stu-id="d65f7-141">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="d65f7-142">使用下列命令在 Data Lake Store 的根目錄建立名為 **mynewfolder**的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d65f7-142">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="d65f7-143">`--folder` 參數可確保命令會建立一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="d65f7-143">The `--folder` parameter ensures that the command creates a folder.</span></span> <span data-ttu-id="d65f7-144">如果這個參數不存在，命令會在 Data Lake Store 帳戶的根目錄中建立稱為 mynewfolder 的空白檔案。</span><span class="sxs-lookup"><span data-stu-id="d65f7-144">If this parameter is not present, the command creates an empty file called mynewfolder at the root of the Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-to-a-data-lake-store-account"></a><span data-ttu-id="d65f7-145">將資料上傳至 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="d65f7-145">Upload data to a Data Lake Store account</span></span>

<span data-ttu-id="d65f7-146">您可以在根層級直接將資料上傳至 Data Lake Store，或上傳至您在帳戶內建立的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d65f7-146">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="d65f7-147">下列程式碼片段示範如何將一些範例資料上傳至您在上一節中建立的資料夾 (**mynewfolder**)。</span><span class="sxs-lookup"><span data-stu-id="d65f7-147">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="d65f7-148">如果您正在尋找一些可上傳的範例資料，您可以從 **Azure Data Lake Git 存放庫** 取得 [Ambulance Data](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)資料夾。</span><span class="sxs-lookup"><span data-stu-id="d65f7-148">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="d65f7-149">下載檔案並將它儲存在電腦的本機目錄上，例如 C:\sampledata\。</span><span class="sxs-lookup"><span data-stu-id="d65f7-149">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="d65f7-150">針對目的地，您必須指定包含檔案名稱的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="d65f7-150">For the destination, you must specify the complete path including the file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="d65f7-151">在 Data Lake Store 帳戶中列出檔案</span><span class="sxs-lookup"><span data-stu-id="d65f7-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="d65f7-152">使用下列命令列出 Data Lake Store 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="d65f7-152">Use the following command to list the files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="d65f7-153">此命令的輸出應類似這樣：</span><span class="sxs-lookup"><span data-stu-id="d65f7-153">The output of this should be similar to the following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="d65f7-154">重新命名、下載與刪除 Data Lake Store 帳戶中的資料</span><span class="sxs-lookup"><span data-stu-id="d65f7-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="d65f7-155">**若要重新命名檔案**，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="d65f7-155">**To rename a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="d65f7-156">**若要下載檔案**，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="d65f7-156">**To download a file**, use the following command.</span></span> <span data-ttu-id="d65f7-157">請確定您指定的目的地路徑已存在。</span><span class="sxs-lookup"><span data-stu-id="d65f7-157">Make sure the destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="d65f7-158">如果不存在，命令就會建立目的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d65f7-158">The command creates the destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="d65f7-159">**若要刪除檔案**，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="d65f7-159">**To delete a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="d65f7-160">如果您想要在單一命令中一起刪除 **mynewfolder** 資料夾和 **vehicle1_09142014_copy.csv** 檔案，請使用 --recurse 參數</span><span class="sxs-lookup"><span data-stu-id="d65f7-160">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="d65f7-161">處理 Data Lake Store 帳戶的權限和 ACL</span><span class="sxs-lookup"><span data-stu-id="d65f7-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="d65f7-162">在本節中，您將了解如何管理 ACL 和使用 Azure CLI 2.0 的權限。</span><span class="sxs-lookup"><span data-stu-id="d65f7-162">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="d65f7-163">如需 ACL 如何在 Azure Data Lake Store 中實作的詳細討論，請參閱 [Azure Data Lake Store 中的存取控制](data-lake-store-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="d65f7-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="d65f7-164">**若要更新檔案/資料夾的擁有者**，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d65f7-164">**To update the owner of a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="d65f7-165">**若要更新檔案/資料夾的權限**，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d65f7-165">**To update the permissions for a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="d65f7-166">**若要取得指定路徑中的 ACL**，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d65f7-166">**To get the ACLs for a given path**, use the following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="d65f7-167">輸出應該類似如下範例：</span><span class="sxs-lookup"><span data-stu-id="d65f7-167">The output should be similar to the following:</span></span>

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

* <span data-ttu-id="d65f7-168">**若要設定 ACL 的項目**，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d65f7-168">**To set an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="d65f7-169">**若要移除 ACL 的項目**，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d65f7-169">**To remove an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="d65f7-170">**若要移除整個預設的 ACL**，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d65f7-170">**To remove an entire default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="d65f7-171">**若要移除整個非預設的 ACL**，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d65f7-171">**To remove an entire non-default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="d65f7-172">刪除 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="d65f7-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="d65f7-173">使用下列命令刪除 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d65f7-173">Use the following command to delete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="d65f7-174">出現提示時，請輸入 **Y** 刪除帳戶。</span><span class="sxs-lookup"><span data-stu-id="d65f7-174">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d65f7-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d65f7-175">Next steps</span></span>

* [<span data-ttu-id="d65f7-176">Azure Data Lake Store CLI 2.0 參考</span><span class="sxs-lookup"><span data-stu-id="d65f7-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="d65f7-177">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="d65f7-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="d65f7-178">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d65f7-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d65f7-179">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d65f7-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
