---
title: "開始使用 Azure Data Lake Store 的 aaaUse PowerShell tooget |Microsoft 文件"
description: "使用 Azure PowerShell toocreate Data Lake Store 帳戶以及執行基本作業"
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
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="8295d-103">使用 Azure PowerShell 開始使用 Azure 資料湖分析存放區</span><span class="sxs-lookup"><span data-stu-id="8295d-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8295d-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="8295d-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="8295d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8295d-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="8295d-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="8295d-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="8295d-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="8295d-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="8295d-108">REST API</span><span class="sxs-lookup"><span data-stu-id="8295d-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="8295d-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8295d-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="8295d-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="8295d-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="8295d-111">Python</span><span class="sxs-lookup"><span data-stu-id="8295d-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="8295d-112">了解如何 toouse Azure PowerShell toocreate Azure 資料湖存放區帳戶和執行基本作業，例如建立資料夾、 上傳和下載資料檔，刪除您的帳戶，依此類推。如需有關 Data Lake Store 的詳細資訊，請參閱 [Data Lake Store 概觀](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8295d-112">Learn how toouse Azure PowerShell toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8295d-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="8295d-113">Prerequisites</span></span>
<span data-ttu-id="8295d-114">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="8295d-114">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="8295d-115">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8295d-115">**An Azure subscription**.</span></span> <span data-ttu-id="8295d-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8295d-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8295d-117">**Azure PowerShell 1.0 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="8295d-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="8295d-118">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="8295d-118">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="8295d-119">驗證</span><span class="sxs-lookup"><span data-stu-id="8295d-119">Authentication</span></span>
<span data-ttu-id="8295d-120">本文使用更簡單的驗證方法提示的 tooenter 所在的資料湖存放區與您的 Azure 帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="8295d-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="8295d-121">hello 存取層級 tooData Lake Store 帳戶和檔案系統，然後係由 hello hello 登入的使用者存取層級。</span><span class="sxs-lookup"><span data-stu-id="8295d-121">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="8295d-122">不過，有一些其他方法為以及 tooauthenticate 與資料湖存放區，也就是**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="8295d-122">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="8295d-123">如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="8295d-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="8295d-124">建立 Azure 資料湖存放區帳戶</span><span class="sxs-lookup"><span data-stu-id="8295d-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="8295d-125">從您的桌面上，開啟新的 Windows PowerShell 視窗中，輸入下列程式碼片段 toolog tooyour Azure 帳戶中的 hello、 設定 hello 訂用帳戶，並註冊 hello 資料湖存放區提供者。</span><span class="sxs-lookup"><span data-stu-id="8295d-125">From your desktop, open a new Windows PowerShell window, and enter hello following snippet toolog in tooyour Azure account, set hello subscription, and register hello Data Lake Store provider.</span></span> <span data-ttu-id="8295d-126">當提示的 toolog 中，請確定您登入做為其中一個 hello 訂用帳戶 admininistrators/擁有者：</span><span class="sxs-lookup"><span data-stu-id="8295d-126">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="8295d-127">Azure Data Lake Store 帳戶與 Azure 資源群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="8295d-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="8295d-128">從建立 Azure 資源群組開始。</span><span class="sxs-lookup"><span data-stu-id="8295d-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="8295d-129">![建立 Azure 資源群組](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "建立 Azure 資源群組")</span><span class="sxs-lookup"><span data-stu-id="8295d-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="8295d-130">建立 Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8295d-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="8295d-131">您指定的 hello 名稱只能包含小寫字母和數字。</span><span class="sxs-lookup"><span data-stu-id="8295d-131">hello name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="8295d-132">![建立 Azure Data Lake Store 帳戶](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "建立 Azure Data Lake Store 帳戶")</span><span class="sxs-lookup"><span data-stu-id="8295d-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="8295d-133">確認已成功建立 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8295d-133">Verify that hello account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="8295d-134">這應該是輸出的 hello **True**。</span><span class="sxs-lookup"><span data-stu-id="8295d-134">hello output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="8295d-135">在您的 Azure 資料湖存放區中建立目錄結構</span><span class="sxs-lookup"><span data-stu-id="8295d-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="8295d-136">您可以在您的 Azure Data Lake Store 帳戶 toomanage 下建立目錄，並儲存資料。</span><span class="sxs-lookup"><span data-stu-id="8295d-136">You can create directories under your Azure Data Lake Store account toomanage and store data.</span></span>

1. <span data-ttu-id="8295d-137">指定根目錄。</span><span class="sxs-lookup"><span data-stu-id="8295d-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="8295d-138">建立新的目錄稱為**mynewdirectory** hello 指定根目錄下。</span><span class="sxs-lookup"><span data-stu-id="8295d-138">Create a new directory called **mynewdirectory** under hello specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="8295d-139">請確認已成功建立該 hello 新目錄。</span><span class="sxs-lookup"><span data-stu-id="8295d-139">Verify that hello new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="8295d-140">它應該會顯示類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="8295d-140">It should show an output like hello following:</span></span>

    <span data-ttu-id="8295d-141">![確認目錄](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "確認目錄")</span><span class="sxs-lookup"><span data-stu-id="8295d-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-tooyour-azure-data-lake-store"></a><span data-ttu-id="8295d-142">上傳資料 tooyour Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8295d-142">Upload data tooyour Azure Data Lake Store</span></span>
<span data-ttu-id="8295d-143">您可以上傳資料 tooData 湖存放區直接在 hello 根層級或 tooa 目錄 hello 帳戶中建立。</span><span class="sxs-lookup"><span data-stu-id="8295d-143">You can upload your data tooData Lake Store directly at hello root level or tooa directory that you created within hello account.</span></span> <span data-ttu-id="8295d-144">下列的 hello 片段會示範如何 tooupload 某些範例資料 toohello 目錄 (**mynewdirectory**) 您建立 hello 前一節中。</span><span class="sxs-lookup"><span data-stu-id="8295d-144">hello snippets below demonstrate how tooupload some sample data toohello directory (**mynewdirectory**) you created in hello previous section.</span></span>

<span data-ttu-id="8295d-145">如果您要尋找的一些範例資料 tooupload，您可以取得 hello**政策救護車資料**資料夾從 hello [Azure 資料湖 Git 儲存機制](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)。</span><span class="sxs-lookup"><span data-stu-id="8295d-145">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="8295d-146">下載 hello 檔案，並將它儲存在您的電腦，例如 C:\sampledata\ 上的本機目錄。</span><span class="sxs-lookup"><span data-stu-id="8295d-146">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="8295d-147">重新命名、下載與刪除資料湖存放區中的資料</span><span class="sxs-lookup"><span data-stu-id="8295d-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="8295d-148">toorename 檔案，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8295d-148">toorename a file, use hello following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="8295d-149">toodownload 檔案，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8295d-149">toodownload a file, use hello following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="8295d-150">toodelete 檔案，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8295d-150">toodelete a file, use hello following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="8295d-151">出現提示時，輸入**Y** toodelete hello 項目。</span><span class="sxs-lookup"><span data-stu-id="8295d-151">When prompted, enter **Y** toodelete hello item.</span></span> <span data-ttu-id="8295d-152">如果您有多個檔案 toodelete，您可以提供以逗號分隔的所有 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="8295d-152">If you have more than one file toodelete, you can provide all hello paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="8295d-153">刪除 Azure 資料湖存放區帳戶</span><span class="sxs-lookup"><span data-stu-id="8295d-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="8295d-154">使用下列命令 toodelete hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8295d-154">Use hello following command toodelete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="8295d-155">出現提示時，輸入**Y** toodelete hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8295d-155">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="8295d-156">使用 PowerShell 時的效能指引</span><span class="sxs-lookup"><span data-stu-id="8295d-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="8295d-157">以下是最重要的設定，可以是微調的 tooget hello 最佳效能，同時使用 Data Lake Store 的 PowerShell toowork hello:</span><span class="sxs-lookup"><span data-stu-id="8295d-157">Below are hello most important settings that can be tuned tooget hello best performance while using PowerShell toowork with Data Lake Store:</span></span>

| <span data-ttu-id="8295d-158">屬性</span><span class="sxs-lookup"><span data-stu-id="8295d-158">Property</span></span>            | <span data-ttu-id="8295d-159">預設值</span><span class="sxs-lookup"><span data-stu-id="8295d-159">Default</span></span> | <span data-ttu-id="8295d-160">說明</span><span class="sxs-lookup"><span data-stu-id="8295d-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="8295d-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="8295d-161">PerFileThreadCount</span></span>  | <span data-ttu-id="8295d-162">10</span><span class="sxs-lookup"><span data-stu-id="8295d-162">10</span></span>      | <span data-ttu-id="8295d-163">這個參數可讓您上傳或下載每個檔案的平行執行緒 toochoose hello 數目。</span><span class="sxs-lookup"><span data-stu-id="8295d-163">This parameter enables you toochoose hello number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="8295d-164">這個數字代表 hello 執行緒數目上限可配置每個檔案，但您可能會收到較少的執行緒，根據您的案例 (例如： 如果您要上傳的 1 KB 的檔案，就會收到一個執行緒，即使您尋求 20 個執行緒)。</span><span class="sxs-lookup"><span data-stu-id="8295d-164">This number represents hello max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="8295d-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="8295d-165">ConcurrentFileCount</span></span> | <span data-ttu-id="8295d-166">10</span><span class="sxs-lookup"><span data-stu-id="8295d-166">10</span></span>      | <span data-ttu-id="8295d-167">這個參數特別用於上傳或下載資料夾。</span><span class="sxs-lookup"><span data-stu-id="8295d-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="8295d-168">這個參數會決定 hello 並行上傳或下載的檔案數目。</span><span class="sxs-lookup"><span data-stu-id="8295d-168">This parameter determines hello number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="8295d-169">這個數字代表 hello 並行的檔案可上傳或下載一次的數目上限，但您可能會收到較少的並行存取，根據您的案例 (例如： 如果您要上傳兩個檔案，您就會取得兩個並行的檔案上傳，即使您要求15)。</span><span class="sxs-lookup"><span data-stu-id="8295d-169">This number represents hello maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="8295d-170">**範例**</span><span class="sxs-lookup"><span data-stu-id="8295d-170">**Example**</span></span>

<span data-ttu-id="8295d-171">此命令會從 Azure Data Lake Store toohello 使用者的本機磁碟機使用 20 個執行緒，每個檔案和 100 個並行的檔案下載檔案。</span><span class="sxs-lookup"><span data-stu-id="8295d-171">This command downloads files from Azure Data Lake Store toohello user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a><span data-ttu-id="8295d-172">我要如何判斷 hello 值 tooset 這些參數的？</span><span class="sxs-lookup"><span data-stu-id="8295d-172">How do I determine hello value tooset for these parameters?</span></span>

<span data-ttu-id="8295d-173">以下是一些您可以使用的指引。</span><span class="sxs-lookup"><span data-stu-id="8295d-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="8295d-174">**步驟 1： 決定 hello 總執行緒計數**-一開始應該計算 hello 總執行緒計數 toouse。</span><span class="sxs-lookup"><span data-stu-id="8295d-174">**Step 1: Determine hello total thread count** - You should start by calculating hello total thread count toouse.</span></span> <span data-ttu-id="8295d-175">一般來說，您應該針對每個實體核心使用 6 個執行緒。</span><span class="sxs-lookup"><span data-stu-id="8295d-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="8295d-176">**範例**</span><span class="sxs-lookup"><span data-stu-id="8295d-176">**Example**</span></span>

    <span data-ttu-id="8295d-177">假設您正在執行 hello PowerShell 命令從 D14 VM，在具有 16 個核心</span><span class="sxs-lookup"><span data-stu-id="8295d-177">Assuming you are running hello PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="8295d-178">**步驟 2： 計算 PerFileThreadCount** -我們 PerFileThreadCount 根據 hello hello 檔案大小來計算。</span><span class="sxs-lookup"><span data-stu-id="8295d-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on hello size of hello files.</span></span> <span data-ttu-id="8295d-179">小於 2.5 GB 的檔案，沒有任何需要 toochange 此參數因為 hello 預設值是 10 已足夠。</span><span class="sxs-lookup"><span data-stu-id="8295d-179">For files smaller than 2.5GB, there is no need toochange this parameter because hello default of 10 is sufficient.</span></span> <span data-ttu-id="8295d-180">大於 2.5 GB 的檔案，您應該使用 10 個執行緒的 hello 基底 hello 第一個有 2.5 GB，並加入 1 個執行緒的每個額外的 256 MB 增加檔案大小。</span><span class="sxs-lookup"><span data-stu-id="8295d-180">For files larger than 2.5GB, you should use 10 threads as hello base for hello first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="8295d-181">如果您要複製包含各種檔案大小的資料夾，請考慮將其分組為相似的檔案大小。</span><span class="sxs-lookup"><span data-stu-id="8295d-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="8295d-182">檔案大小不相近可能會導致非最佳的效能。</span><span class="sxs-lookup"><span data-stu-id="8295d-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="8295d-183">如果不可能 toogroup 類似檔案大小，您應該設定 PerFileThreadCount hello 最大檔案大小為基礎。</span><span class="sxs-lookup"><span data-stu-id="8295d-183">If that's not possible toogroup similar file sizes, you should set PerFileThreadCount based on hello largest file size.</span></span>

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="8295d-184">**範例**</span><span class="sxs-lookup"><span data-stu-id="8295d-184">**Example**</span></span>

    <span data-ttu-id="8295d-185">我們假設您有 100 個檔案，範圍介於 1 GB too10GB，使用的 hello hello 最大為 10 GB 檔案大小的方程式，它會讀取 hello 如下。</span><span class="sxs-lookup"><span data-stu-id="8295d-185">Assuming you have 100 files ranging from 1GB too10GB, we use hello 10GB as hello largest file size for equation, which would read like hello following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="8295d-186">**步驟 3： 計算 ConcurrentFilecount** -使用 hello 總執行緒計數和 PerFileThreadCount toocalculate ConcurrentFileCount 取決於下列方程式 hello。</span><span class="sxs-lookup"><span data-stu-id="8295d-186">**Step 3: Calculate ConcurrentFilecount** - Use hello total thread count and PerFileThreadCount toocalculate ConcurrentFileCount based on hello following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="8295d-187">**範例**</span><span class="sxs-lookup"><span data-stu-id="8295d-187">**Example**</span></span>

    <span data-ttu-id="8295d-188">根據我們使用 hello 範例值</span><span class="sxs-lookup"><span data-stu-id="8295d-188">Based on hello example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="8295d-189">因此， **ConcurrentFileCount**是**2.4**，我們可以藉由四捨五入太其中**2**。</span><span class="sxs-lookup"><span data-stu-id="8295d-189">So, **ConcurrentFileCount** is **2.4**, which we can round off too**2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="8295d-190">進一步微調</span><span class="sxs-lookup"><span data-stu-id="8295d-190">Further tuning</span></span>

<span data-ttu-id="8295d-191">您可能需要進一步調整因為沒有與檔案大小 toowork 的範圍。</span><span class="sxs-lookup"><span data-stu-id="8295d-191">You might require further tuning because there is a range of file sizes toowork with.</span></span> <span data-ttu-id="8295d-192">上述計算 hello 運作 hello 檔案的全部或大部分是較大且更接近 toohello 10 GB 範圍的情況。</span><span class="sxs-lookup"><span data-stu-id="8295d-192">hello above calculation works well if all or most of hello files are larger and closer toohello 10GB range.</span></span> <span data-ttu-id="8295d-193">相反地，如果有許多不同的檔案大小且很多檔案比較小，您可以減少 PerFileThreadCount。</span><span class="sxs-lookup"><span data-stu-id="8295d-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="8295d-194">藉由減少 hello PerFileThreadCount，我們可以增加 ConcurrentFileCount。</span><span class="sxs-lookup"><span data-stu-id="8295d-194">By reducing hello PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="8295d-195">因此，如果我們假設，我們檔案的最小 hello 5 GB 範圍中，我們可以重新執行我們的計算：</span><span class="sxs-lookup"><span data-stu-id="8295d-195">So, if we assume that most of our files are smaller in hello 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="8295d-196">因此， **ConcurrentFileCount**會立即 96/20，也就是 4.8 四捨五入太**4**。</span><span class="sxs-lookup"><span data-stu-id="8295d-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off too**4**.</span></span>

<span data-ttu-id="8295d-197">您可以繼續 tootune 這些設定變更 hello **PerFileThreadCount**向上和向下的檔案大小的 hello 分佈而定。</span><span class="sxs-lookup"><span data-stu-id="8295d-197">You can continue tootune these settings by changing hello **PerFileThreadCount** up and down depending on hello distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="8295d-198">限制</span><span class="sxs-lookup"><span data-stu-id="8295d-198">Limitation</span></span>

* <span data-ttu-id="8295d-199">**檔案數目小於 ConcurrentFileCount**： 如果您要上傳的檔案的 hello 數目小於 hello **ConcurrentFileCount**您計算，然後您應該降低**ConcurrentFileCount**檔案 toobe 等於 toohello 數目。</span><span class="sxs-lookup"><span data-stu-id="8295d-199">**Number of files is less than ConcurrentFileCount**: If hello number of files you are uploading is smaller than hello **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** toobe equal toohello number of files.</span></span> <span data-ttu-id="8295d-200">您可以使用任何剩餘的執行緒 tooincrease **PerFileThreadCount**。</span><span class="sxs-lookup"><span data-stu-id="8295d-200">You can use any remaining threads tooincrease **PerFileThreadCount**.</span></span>

* <span data-ttu-id="8295d-201">**太多執行緒**： 如果您增加執行緒計數太多而不會增加您的叢集大小、 hello 造成效能降低的問題。</span><span class="sxs-lookup"><span data-stu-id="8295d-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run hello risk of degraded performance.</span></span> <span data-ttu-id="8295d-202">內容切換 hello CPU 上時，可以是競爭問題。</span><span class="sxs-lookup"><span data-stu-id="8295d-202">There can be contention issues when context-switching on hello CPU.</span></span>

* <span data-ttu-id="8295d-203">**不足的並行**： 如果 hello 並行處理並不敷使用，則您的叢集可能會太小。</span><span class="sxs-lookup"><span data-stu-id="8295d-203">**Insufficient concurrency**: If hello concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="8295d-204">這樣會提供您多個並行叢集中，您可以增加 hello 節點數目。</span><span class="sxs-lookup"><span data-stu-id="8295d-204">You can increase hello number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="8295d-205">**節流錯誤**︰如果並行處理量太高，您可能會看到節流錯誤。</span><span class="sxs-lookup"><span data-stu-id="8295d-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="8295d-206">如果您看見期間發生節流錯誤，您應該降低 hello 並行或與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="8295d-206">If you are seeing throttling errors, you should either reduce hello concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8295d-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8295d-207">Next steps</span></span>
* [<span data-ttu-id="8295d-208">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="8295d-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="8295d-209">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8295d-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="8295d-210">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8295d-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

