---
title: "透過 PowerShell 開始使用 Azure Data Lake Store | Microsoft Docs"
description: "使用 Azure PowerShell 建立資料湖存放區帳戶，並執行基本作業"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 23c9aaa089251bff5132652475f4daadc2c128fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="58333-103">使用 Azure PowerShell 開始使用 Azure 資料湖分析存放區</span><span class="sxs-lookup"><span data-stu-id="58333-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58333-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="58333-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="58333-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="58333-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="58333-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="58333-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="58333-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="58333-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="58333-108">REST API</span><span class="sxs-lookup"><span data-stu-id="58333-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="58333-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="58333-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="58333-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="58333-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="58333-111">Python</span><span class="sxs-lookup"><span data-stu-id="58333-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="58333-112">了解如何使用 Azure PowerShell 建立 Azure 資料湖存放區帳戶並執行基本作業，例如建立資料夾、上傳和下載資料檔案、刪除您的帳戶等等。如需有關 Data Lake Store 的詳細資訊，請參閱 [Data Lake Store 概觀](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="58333-112">Learn how to use Azure PowerShell to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58333-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="58333-113">Prerequisites</span></span>
<span data-ttu-id="58333-114">開始進行本教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="58333-114">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="58333-115">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="58333-115">**An Azure subscription**.</span></span> <span data-ttu-id="58333-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="58333-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="58333-117">**Azure PowerShell 1.0 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="58333-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="58333-118">請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="58333-118">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="58333-119">驗證</span><span class="sxs-lookup"><span data-stu-id="58333-119">Authentication</span></span>
<span data-ttu-id="58333-120">本文搭配使用較簡單的驗證方法與 Data Lake Store，系統會提示您輸入 Azure 帳號認證。</span><span class="sxs-lookup"><span data-stu-id="58333-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="58333-121">Data Lake Store 帳戶和檔案系統的存取層級則由已登入使用者的存取層級所控管。</span><span class="sxs-lookup"><span data-stu-id="58333-121">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="58333-122">不過，還有其他方法可向 Data Lake Store 進行驗證：**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="58333-122">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="58333-123">如需有關如何驗證的指示和詳細資訊，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="58333-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="58333-124">建立 Azure Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="58333-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="58333-125">從您的桌面上開啟新的 Windows PowerShell 視窗，輸入下列程式碼片段登入 Azure 帳戶、設定訂用帳戶，然後註冊 Data Lake Store 提供者。</span><span class="sxs-lookup"><span data-stu-id="58333-125">From your desktop, open a new Windows PowerShell window, and enter the following snippet to log in to your Azure account, set the subscription, and register the Data Lake Store provider.</span></span> <span data-ttu-id="58333-126">系統提示您登入時，請使用其中一個訂用帳戶管理員/擁有者身分登入：</span><span class="sxs-lookup"><span data-stu-id="58333-126">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="58333-127">Azure 資料湖存放區帳戶與 Azure 資源群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="58333-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="58333-128">從建立 Azure 資源群組開始。</span><span class="sxs-lookup"><span data-stu-id="58333-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="58333-129">![建立 Azure 資源群組](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "建立 Azure 資源群組")</span><span class="sxs-lookup"><span data-stu-id="58333-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="58333-130">建立 Azure 資料湖存放區帳戶。</span><span class="sxs-lookup"><span data-stu-id="58333-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="58333-131">您指定的名稱必須只包含小寫字母和數字。</span><span class="sxs-lookup"><span data-stu-id="58333-131">The name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="58333-132">![建立 Azure Data Lake Store 帳戶](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "建立 Azure Data Lake Store 帳戶")</span><span class="sxs-lookup"><span data-stu-id="58333-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="58333-133">確認已成功建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="58333-133">Verify that the account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="58333-134">輸出應為 **True**。</span><span class="sxs-lookup"><span data-stu-id="58333-134">The output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="58333-135">在您的 Azure 資料湖存放區中建立目錄結構</span><span class="sxs-lookup"><span data-stu-id="58333-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="58333-136">您可以在您的 Azure 資料湖存放區帳戶下建立用於管理與儲存資料的目錄。</span><span class="sxs-lookup"><span data-stu-id="58333-136">You can create directories under your Azure Data Lake Store account to manage and store data.</span></span>

1. <span data-ttu-id="58333-137">指定根目錄。</span><span class="sxs-lookup"><span data-stu-id="58333-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="58333-138">在指定的根目錄下建立名為 **mynewdirectory** 的新目錄。</span><span class="sxs-lookup"><span data-stu-id="58333-138">Create a new directory called **mynewdirectory** under the specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="58333-139">確認已成功建立新目錄。</span><span class="sxs-lookup"><span data-stu-id="58333-139">Verify that the new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="58333-140">應該會顯示類似下面的輸出畫面：</span><span class="sxs-lookup"><span data-stu-id="58333-140">It should show an output like the following:</span></span>

    <span data-ttu-id="58333-141">![確認目錄](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "確認目錄")</span><span class="sxs-lookup"><span data-stu-id="58333-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-to-your-azure-data-lake-store"></a><span data-ttu-id="58333-142">將資料上傳至 Azure 資料湖存放區</span><span class="sxs-lookup"><span data-stu-id="58333-142">Upload data to your Azure Data Lake Store</span></span>
<span data-ttu-id="58333-143">您可以在根層級直接將資料上傳至資料湖存放區，或上傳至您在帳戶內建立的目錄。</span><span class="sxs-lookup"><span data-stu-id="58333-143">You can upload your data to Data Lake Store directly at the root level or to a directory that you created within the account.</span></span> <span data-ttu-id="58333-144">下列程式碼範例說明如何將一些範例資料上傳至您在上一節中建立的目錄 (**mynewdirectory**)。</span><span class="sxs-lookup"><span data-stu-id="58333-144">The snippets below demonstrate how to upload some sample data to the directory (**mynewdirectory**) you created in the previous section.</span></span>

<span data-ttu-id="58333-145">如果您正在尋找一些可上傳的範例資料，您可以從 **Azure Data Lake Git 存放庫** 取得 [Ambulance Data](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)資料夾。</span><span class="sxs-lookup"><span data-stu-id="58333-145">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="58333-146">下載檔案並將它儲存在電腦的本機目錄上，例如 C:\sampledata\。</span><span class="sxs-lookup"><span data-stu-id="58333-146">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="58333-147">重新命名、下載與刪除資料湖存放區中的資料</span><span class="sxs-lookup"><span data-stu-id="58333-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="58333-148">若要重新命名檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="58333-148">To rename a file, use the following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="58333-149">若要下載檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="58333-149">To download a file, use the following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="58333-150">若要刪除檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="58333-150">To delete a file, use the following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="58333-151">出現提示時，請輸入 **Y** 刪除項目。</span><span class="sxs-lookup"><span data-stu-id="58333-151">When prompted, enter **Y** to delete the item.</span></span> <span data-ttu-id="58333-152">如果您要刪除多個檔案，可以提供所有的路徑並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="58333-152">If you have more than one file to delete, you can provide all the paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="58333-153">刪除 Azure 資料湖存放區帳戶</span><span class="sxs-lookup"><span data-stu-id="58333-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="58333-154">使用下列命令刪除資料湖存放區帳戶。</span><span class="sxs-lookup"><span data-stu-id="58333-154">Use the following command to delete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="58333-155">出現提示時，請輸入 **Y** 刪除帳戶。</span><span class="sxs-lookup"><span data-stu-id="58333-155">When prompted, enter **Y** to delete the account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="58333-156">使用 PowerShell 時的效能指引</span><span class="sxs-lookup"><span data-stu-id="58333-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="58333-157">以下是可以微調的最重要設定，以在使用 PowerShell 搭配 Data Lake Store 運作時獲得最佳效能︰</span><span class="sxs-lookup"><span data-stu-id="58333-157">Below are the most important settings that can be tuned to get the best performance while using PowerShell to work with Data Lake Store:</span></span>

| <span data-ttu-id="58333-158">屬性</span><span class="sxs-lookup"><span data-stu-id="58333-158">Property</span></span>            | <span data-ttu-id="58333-159">預設值</span><span class="sxs-lookup"><span data-stu-id="58333-159">Default</span></span> | <span data-ttu-id="58333-160">說明</span><span class="sxs-lookup"><span data-stu-id="58333-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="58333-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="58333-161">PerFileThreadCount</span></span>  | <span data-ttu-id="58333-162">10</span><span class="sxs-lookup"><span data-stu-id="58333-162">10</span></span>      | <span data-ttu-id="58333-163">這個參數可讓您選擇可用於上傳或下載每個檔案的平行執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="58333-163">This parameter enables you to choose the number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="58333-164">此數字代表每個檔案可以配置的執行緒數目上限，但視您的案例而定，您可能會收到比較少的執行緒 (例如︰如果您要上傳 1 KB 檔案，即使您要求 20 個執行緒，但您將取得一個執行緒)。</span><span class="sxs-lookup"><span data-stu-id="58333-164">This number represents the max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="58333-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="58333-165">ConcurrentFileCount</span></span> | <span data-ttu-id="58333-166">10</span><span class="sxs-lookup"><span data-stu-id="58333-166">10</span></span>      | <span data-ttu-id="58333-167">這個參數特別用於上傳或下載資料夾。</span><span class="sxs-lookup"><span data-stu-id="58333-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="58333-168">這個參數會決定可以上傳或下載的並行檔案數目。</span><span class="sxs-lookup"><span data-stu-id="58333-168">This parameter determines the number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="58333-169">此數字代表可以一次上傳或下載的並行檔案數目上限，但視您的案例而定，您可能會收到比較少的並行檔案 (例如︰如果您要上傳兩個檔案，即使您要求 15 個檔案，但您將取得兩個並行檔案)。</span><span class="sxs-lookup"><span data-stu-id="58333-169">This number represents the maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="58333-170">**範例**</span><span class="sxs-lookup"><span data-stu-id="58333-170">**Example**</span></span>

<span data-ttu-id="58333-171">此命令會使用每個檔案 20 個執行緒和 100 個並行檔案，將檔案從 Azure Data Lake Store 下載至使用者的本機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="58333-171">This command downloads files from Azure Data Lake Store to the user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-the-value-to-set-for-these-parameters"></a><span data-ttu-id="58333-172">如何判斷要針對這些參數設定的值？</span><span class="sxs-lookup"><span data-stu-id="58333-172">How do I determine the value to set for these parameters?</span></span>

<span data-ttu-id="58333-173">以下是一些您可以使用的指引。</span><span class="sxs-lookup"><span data-stu-id="58333-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="58333-174">**步驟 1︰決定總執行緒計數** - 您應該從計算要使用的總執行緒計數著手。</span><span class="sxs-lookup"><span data-stu-id="58333-174">**Step 1: Determine the total thread count** - You should start by calculating the total thread count to use.</span></span> <span data-ttu-id="58333-175">一般來說，您應該針對每個實體核心使用 6 個執行緒。</span><span class="sxs-lookup"><span data-stu-id="58333-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="58333-176">**範例**</span><span class="sxs-lookup"><span data-stu-id="58333-176">**Example**</span></span>

    <span data-ttu-id="58333-177">假設您正從有 16 個核心的 D14 VM 執行 PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="58333-177">Assuming you are running the PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="58333-178">**步驟 2︰計算 PerFileThreadCount** - 我們會根據檔案的大小計算 PerFileThreadCount。</span><span class="sxs-lookup"><span data-stu-id="58333-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on the size of the files.</span></span> <span data-ttu-id="58333-179">對於小於 2.5 GB 的檔案，不需要變更此參數，因為預設值為 10 就已足夠。</span><span class="sxs-lookup"><span data-stu-id="58333-179">For files smaller than 2.5GB, there is no need to change this parameter because the default of 10 is sufficient.</span></span> <span data-ttu-id="58333-180">對於大於 2.5 GB 的檔案，您應該使用 10 個執行緒做為第一個 2.5 GB 的基底，並且為每增加額外 256 MB 的檔案大小新增 1 個執行緒。</span><span class="sxs-lookup"><span data-stu-id="58333-180">For files larger than 2.5GB, you should use 10 threads as the base for the first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="58333-181">如果您要複製包含各種檔案大小的資料夾，請考慮將其分組為相似的檔案大小。</span><span class="sxs-lookup"><span data-stu-id="58333-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="58333-182">檔案大小不相近可能會導致非最佳的效能。</span><span class="sxs-lookup"><span data-stu-id="58333-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="58333-183">如果不可能分組為相似的檔案大小，您應該根據最大檔案大小設定 PerFileThreadCount。</span><span class="sxs-lookup"><span data-stu-id="58333-183">If that's not possible to group similar file sizes, you should set PerFileThreadCount based on the largest file size.</span></span>

        PerFileThreadCount = 10 threads for the first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="58333-184">**範例**</span><span class="sxs-lookup"><span data-stu-id="58333-184">**Example**</span></span>

    <span data-ttu-id="58333-185">假設您有 100 個 1GB 到 10GB 的檔案，我們使用 10GB 做為等式的最大檔案大小，該等式會如下所示。</span><span class="sxs-lookup"><span data-stu-id="58333-185">Assuming you have 100 files ranging from 1GB to 10GB, we use the 10GB as the largest file size for equation, which would read like the following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="58333-186">**步驟 3︰計算 ConcurrentFilecount** - 使用總執行緒計數和 PerFileThreadCount 來計算以下列等式為基礎的 ConcurrentFileCount。</span><span class="sxs-lookup"><span data-stu-id="58333-186">**Step 3: Calculate ConcurrentFilecount** - Use the total thread count and PerFileThreadCount to calculate ConcurrentFileCount based on the following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="58333-187">**範例**</span><span class="sxs-lookup"><span data-stu-id="58333-187">**Example**</span></span>

    <span data-ttu-id="58333-188">以我們使用的範例值為基礎</span><span class="sxs-lookup"><span data-stu-id="58333-188">Based on the example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="58333-189">因此，**ConcurrentFileCount** 是 **2.4**, ，我們可以四捨五入為 **2**。</span><span class="sxs-lookup"><span data-stu-id="58333-189">So, **ConcurrentFileCount** is **2.4**, which we can round off to **2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="58333-190">進一步微調</span><span class="sxs-lookup"><span data-stu-id="58333-190">Further tuning</span></span>

<span data-ttu-id="58333-191">您可能需要進一步微調，因為有各種檔案大小要處理。</span><span class="sxs-lookup"><span data-stu-id="58333-191">You might require further tuning because there is a range of file sizes to work with.</span></span> <span data-ttu-id="58333-192">如果所有或大部分檔案都比較大且比較接近 10GB 的範圍，就很適合上述的計算。</span><span class="sxs-lookup"><span data-stu-id="58333-192">The above calculation works well if all or most of the files are larger and closer to the 10GB range.</span></span> <span data-ttu-id="58333-193">相反地，如果有許多不同的檔案大小且很多檔案比較小，您可以減少 PerFileThreadCount。</span><span class="sxs-lookup"><span data-stu-id="58333-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="58333-194">藉由減少 PerFileThreadCount，我們即可增加 ConcurrentFileCount。</span><span class="sxs-lookup"><span data-stu-id="58333-194">By reducing the PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="58333-195">所以，如果假設 5GB 範圍中的大部分檔案比較小，我們可以重新進行計算︰</span><span class="sxs-lookup"><span data-stu-id="58333-195">So, if we assume that most of our files are smaller in the 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="58333-196">因此，**ConcurrentFileCount** 現在會是 96/20，也就是 4.8，可四捨五入為 **4**。</span><span class="sxs-lookup"><span data-stu-id="58333-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off to **4**.</span></span>

<span data-ttu-id="58333-197">您可以根據檔案大小的分佈情形，將 **PerFileThreadCount** 變大和變小，繼續微調這些設定。</span><span class="sxs-lookup"><span data-stu-id="58333-197">You can continue to tune these settings by changing the **PerFileThreadCount** up and down depending on the distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="58333-198">限制</span><span class="sxs-lookup"><span data-stu-id="58333-198">Limitation</span></span>

* <span data-ttu-id="58333-199">**檔案數目小於 ConcurrentFileCount**︰如果您要上傳的檔案數目小於您計算的 **ConcurrentFileCount**，則應該減少 **ConcurrentFileCount** 使其等於檔案數目。</span><span class="sxs-lookup"><span data-stu-id="58333-199">**Number of files is less than ConcurrentFileCount**: If the number of files you are uploading is smaller than the **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** to be equal to the number of files.</span></span> <span data-ttu-id="58333-200">您可以使用任何剩餘的執行緒來增加 **PerFileThreadCount**。</span><span class="sxs-lookup"><span data-stu-id="58333-200">You can use any remaining threads to increase **PerFileThreadCount**.</span></span>

* <span data-ttu-id="58333-201">**執行緒太多**︰如果您增加太多執行緒計數，但未增加您的叢集大小，您會有效能降低的風險。</span><span class="sxs-lookup"><span data-stu-id="58333-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run the risk of degraded performance.</span></span> <span data-ttu-id="58333-202">在 CPU 上進行環境切換時，可能會有爭用問題。</span><span class="sxs-lookup"><span data-stu-id="58333-202">There can be contention issues when context-switching on the CPU.</span></span>

* <span data-ttu-id="58333-203">**並行處理量不足**︰如果並行處理量不足，您的叢集可能太小。</span><span class="sxs-lookup"><span data-stu-id="58333-203">**Insufficient concurrency**: If the concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="58333-204">您可以增加叢集中的節點數目，以提供更多的並行處理量。</span><span class="sxs-lookup"><span data-stu-id="58333-204">You can increase the number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="58333-205">**節流錯誤**︰如果並行處理量太高，您可能會看到節流錯誤。</span><span class="sxs-lookup"><span data-stu-id="58333-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="58333-206">如果您看到節流錯誤，則應該減少並行處理量或與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="58333-206">If you are seeing throttling errors, you should either reduce the concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58333-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58333-207">Next steps</span></span>
* [<span data-ttu-id="58333-208">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="58333-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="58333-209">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="58333-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="58333-210">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="58333-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

