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
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="dce98-103">在 Azure 檔案共用中建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="dce98-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="dce98-104">您可以使用 [Azure 入口網站](https://portal.azure.com/)、Azure 儲存體 PowerShell Cmdlet、Azure 儲存體用戶端程式庫或 Azure 儲存體 REST API 來建立 Azure 檔案共用。在本教學課程中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="dce98-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), the Azure Storage PowerShell cmdlets, the Azure Storage client libraries, or the Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="dce98-105">如何使用 Azure 入口網站建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="dce98-105">How to create an Azure File share using the Azure portal</span></span>](#Create file share through the Portal)
* [<span data-ttu-id="dce98-106">如何使用 Powershell 建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="dce98-106">How to create an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="dce98-107">如何使用 CLI 建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="dce98-107">How to create an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="dce98-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="dce98-108">Prerequisites</span></span>
<span data-ttu-id="dce98-109">若要建立 Azure 檔案共用，您可以使用已經存在的儲存體帳戶，或[建立新的 Azure 儲存體帳戶](storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="dce98-109">To create an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](storage-create-storage-account.md).</span></span> <span data-ttu-id="dce98-110">若要使用 PowerShell 建立 Azure 檔案共用，您需要儲存體帳戶的名稱與帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="dce98-110">To create an Azure File share with PowerShell, you will need the account key and name of your storage account..</span></span> <span data-ttu-id="dce98-111">如果您打算使用 Powershell 或 CLI，您將需要儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="dce98-111">You will need Storage account key if you plan to use Powershell or CLI.</span></span>

## <a name="create-file-share-through-the-portal"></a><span data-ttu-id="dce98-112">透過入口網站建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="dce98-112">Create file share through the Portal</span></span>
1. <span data-ttu-id="dce98-113">**前往 Azure 入口網站中的儲存體帳戶刀鋒視窗**：</span><span class="sxs-lookup"><span data-stu-id="dce98-113">**Go to Storage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="dce98-114">![儲存體帳戶刀鋒視窗](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="dce98-114">![Storage Account Blade](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="dce98-115">**按一下 [新增檔案共用] 按鈕**：</span><span class="sxs-lookup"><span data-stu-id="dce98-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="dce98-116">![按一下 [新增檔案共用] 按鈕](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="dce98-116">![Click the add file share button](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="dce98-117">**提供名稱和配額。配額目前上限可以是 5TB**：</span><span class="sxs-lookup"><span data-stu-id="dce98-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="dce98-118">![提供新檔案共用的名稱和所需的配額](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="dce98-118">![Provide a name and a desired quota for the new file share](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="dce98-119">**檢視新的檔案共用**：![檢視新的檔案共用](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="dce98-119">**View your new file share**:  ![View your new file share](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="dce98-120">**上傳檔案**![上傳檔案](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="dce98-120">**Upload a file**:  ![Upload a file](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="dce98-121">**瀏覽至檔案共用並管理您的目錄和檔案**：![瀏覽檔案共用](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="dce98-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="dce98-122">透過 PowerShell 建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="dce98-122">Create file share through PowerShell</span></span>
<span data-ttu-id="dce98-123">若要準備使用 PowerShell，請下載並安裝 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dce98-123">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="dce98-124">如需安裝點和安裝指示的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) 。</span><span class="sxs-lookup"><span data-stu-id="dce98-124">See [How to install and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for the install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="dce98-125">建議您下載和安裝或升級至最新的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="dce98-125">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="dce98-126">**建立儲存體帳戶和金鑰的內容** 內容包含儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="dce98-126">**Create a context for your storage account and key** The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="dce98-127">如需從 [Azure 入口網站](https://portal.azure.com/)複製帳戶金鑰的指示，請參閱[檢視和複製儲存體存取金鑰](storage-create-storage-account.md#view-and-copy-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="dce98-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="dce98-128">**建立新的檔案共用**：</span><span class="sxs-lookup"><span data-stu-id="dce98-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="dce98-129">您的檔案共用名稱必須是全部小寫。</span><span class="sxs-lookup"><span data-stu-id="dce98-129">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="dce98-130">如需有關為檔案共用與檔案命名的完整詳細資料，請參閱 [命名和參考共用、目錄、檔案及中繼資料](https://msdn.microsoft.com/library/azure/dn167011.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dce98-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="dce98-131">透過命令列介面 (CLI) 建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="dce98-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="dce98-132">**若要準備使用命令列介面 (CLI)，請下載並安裝 Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="dce98-132">**To prepare to use a Command Line Interface (CLI), download and install the Azure CLI.**</span></span>  
    <span data-ttu-id="dce98-133">請參閱[安裝 Azure CLI 2.0](/cli/azure/install-az-cli2.md) 和[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="dce98-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="dce98-134">**在您要建立共用的儲存體帳戶中，建立儲存體帳戶的連接字串。**</span><span class="sxs-lookup"><span data-stu-id="dce98-134">**Create a connection string to the storage account where you want to create the share.**</span></span>  
    <span data-ttu-id="dce98-135">使用下列範例中的儲存體帳戶名稱和資源群組來取代 ```<storage-account>``` 和 ```<resource_group>```。</span><span class="sxs-lookup"><span data-stu-id="dce98-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in the following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve the connection string."
    fi
    ```

3. <span data-ttu-id="dce98-136">**建立檔案共用**</span><span class="sxs-lookup"><span data-stu-id="dce98-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="dce98-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dce98-137">Next steps</span></span>
* [<span data-ttu-id="dce98-138">連線並掛接檔案共用 - Windows</span><span class="sxs-lookup"><span data-stu-id="dce98-138">Connect and Mount File Share - Windows</span></span>](storage-file-how-to-use-files-windows.md)
* [<span data-ttu-id="dce98-139">連線並掛接檔案共用 - Linux</span><span class="sxs-lookup"><span data-stu-id="dce98-139">Connect and Mount File Share - Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="dce98-140">連線並掛接檔案共用 - macOS</span><span class="sxs-lookup"><span data-stu-id="dce98-140">Connect and Mount File Share - macOS</span></span>](storage-file-how-to-use-files-mac.md)

<span data-ttu-id="dce98-141">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dce98-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="dce98-142">常見問題集</span><span class="sxs-lookup"><span data-stu-id="dce98-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="dce98-143">疑難排解</span><span class="sxs-lookup"><span data-stu-id="dce98-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)