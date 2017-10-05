---
title: "使用 Azure CLI 2.0 開始使用 Azure Data Lake Analytics | Microsoft Docs"
description: "了解如何透過 Azure 命令列介面 2.0 建立 Data Lake Analytics 帳戶、使用 U-SQL 建立 Data Lake Analytics 作業，以及提交作業。 "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: fe2b84aac718ff5eddd4d73b5dc2120362952c1e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="7d430-103">使用 Azure CLI 2.0 開始使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7d430-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="7d430-104">在本教學課程中，您會開發一個作業可讀取定位字元分隔值 (TSV) 檔案，並將該檔案轉換為逗點分隔值 (CSV) 檔案。</span><span class="sxs-lookup"><span data-stu-id="7d430-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="7d430-105">若要使用其他支援的工具進行同一個教學課程，請使用此區段最上方的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="7d430-105">To go through the same tutorial using other supported tools, use the dropdown list on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d430-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="7d430-106">Prerequisites</span></span>
<span data-ttu-id="7d430-107">開始進行本教學課程之前，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="7d430-107">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="7d430-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7d430-108">**An Azure subscription**.</span></span> <span data-ttu-id="7d430-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7d430-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7d430-110">**Azure CLI 2.0**.</span><span class="sxs-lookup"><span data-stu-id="7d430-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="7d430-111">請參閱 [安裝和設定 Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="7d430-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="7d430-112">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="7d430-112">Log in to Azure</span></span>

<span data-ttu-id="7d430-113">若要登入您的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="7d430-113">To log in to your Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="7d430-114">系統會要求您瀏覽至 URL，然後輸入驗證碼。</span><span class="sxs-lookup"><span data-stu-id="7d430-114">You are requested to browse to a URL, and enter an authentication code.</span></span>  <span data-ttu-id="7d430-115">然後遵循指示輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="7d430-115">And then follow the instructions to enter your credentials.</span></span>

<span data-ttu-id="7d430-116">一旦您已登入後，登入命令會列出您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7d430-116">Once you have logged in, the login command lists your subscriptions.</span></span>

<span data-ttu-id="7d430-117">若要使用特定的訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="7d430-117">To use a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="7d430-118">建立 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="7d430-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="7d430-119">您需要 Data Lake Analytics 帳戶，才能執行作業。</span><span class="sxs-lookup"><span data-stu-id="7d430-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="7d430-120">若要建立 Data Lake Analytics 帳戶，您必須指定下列項目：</span><span class="sxs-lookup"><span data-stu-id="7d430-120">To create a Data Lake Analytics account, you must specify the following items:</span></span>

* <span data-ttu-id="7d430-121">**Azure 資源群組**。</span><span class="sxs-lookup"><span data-stu-id="7d430-121">**Azure Resource Group**.</span></span> <span data-ttu-id="7d430-122">Data Lake Analytics 帳戶必須建立在 Azure 資源群組內。</span><span class="sxs-lookup"><span data-stu-id="7d430-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="7d430-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 可讓您將應用程式中的資源做為群組使用。</span><span class="sxs-lookup"><span data-stu-id="7d430-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="7d430-124">您可以透過單一、協調的作業，將應用程式的所有資源進行部署、更新或刪除。</span><span class="sxs-lookup"><span data-stu-id="7d430-124">You can deploy, update, or delete all of the resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="7d430-125">若要列出訂用帳戶下的現有資源群組：</span><span class="sxs-lookup"><span data-stu-id="7d430-125">To list the existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="7d430-126">若要建立新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="7d430-126">To create a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="7d430-127">**Data Lake Analytics 帳戶名稱**。</span><span class="sxs-lookup"><span data-stu-id="7d430-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="7d430-128">每一個 Data Lake Analytics 帳戶都有名稱。</span><span class="sxs-lookup"><span data-stu-id="7d430-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="7d430-129">**位置**。</span><span class="sxs-lookup"><span data-stu-id="7d430-129">**Location**.</span></span> <span data-ttu-id="7d430-130">使用其中一個支援 Data Lake Analytics 的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="7d430-130">Use one of the Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="7d430-131">**預設 Data Lake Store 帳戶**：每個 Data Lake Analytics 帳戶都有一個預設的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7d430-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="7d430-132">若要列出現有的 Data Lake Store 帳戶：</span><span class="sxs-lookup"><span data-stu-id="7d430-132">To list the existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="7d430-133">建立新的 Data Lake Store 帳戶：</span><span class="sxs-lookup"><span data-stu-id="7d430-133">To create a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="7d430-134">使用下列語法建立 Data Lake Analytics 帳戶：</span><span class="sxs-lookup"><span data-stu-id="7d430-134">Use the following syntax to create a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="7d430-135">建立帳戶後，您可以使用下列命令列出帳戶，並顯示帳戶詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="7d430-135">After creating an account, you can use the following commands to list the accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-to-data-lake-store"></a><span data-ttu-id="7d430-136">將資料上傳至 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7d430-136">Upload data to Data Lake Store</span></span>
<span data-ttu-id="7d430-137">在本教學課程中，您會處理一些搜尋記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7d430-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="7d430-138">搜尋記錄檔可以儲存在 Data Lake Store 或 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="7d430-138">The search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="7d430-139">Azure 入口網站會提供使用者介面，可將範例資料檔案複製到預設的 Data Lake Store 存放區帳戶，其中包括搜尋記錄檔案。</span><span class="sxs-lookup"><span data-stu-id="7d430-139">The Azure portal provides a user interface for copying some sample data files to the default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="7d430-140">若要將資料上傳至預設 Data Lake Store 帳戶，請參閱 [準備來源資料](data-lake-analytics-get-started-portal.md) 。</span><span class="sxs-lookup"><span data-stu-id="7d430-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) to upload the data to the default Data Lake Store account.</span></span>

<span data-ttu-id="7d430-141">若要使用 CLI 2.0 上傳檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="7d430-141">To upload files using CLI 2.0, use the following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="7d430-142">Data Lake Analytics 也可存取 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7d430-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="7d430-143">若要將資料上傳至 Azure Blob 儲存體，請參閱 [使用 Azure CLI 搭配 Azure 儲存體](../storage/common/storage-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="7d430-143">For uploading data to Azure Blob storage, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="7d430-144">提交 Data Lake Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="7d430-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="7d430-145">Data Lake Analytics 工作是以 U-SQL 語言撰寫。</span><span class="sxs-lookup"><span data-stu-id="7d430-145">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="7d430-146">若要深入了解 U-SQL，請參閱[開始使用 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)和 [U-SQL 語言參考](http://go.microsoft.com/fwlink/?LinkId=691348)。</span><span class="sxs-lookup"><span data-stu-id="7d430-146">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="7d430-147">**建立 Data Lake Analytics 工作指令碼**</span><span class="sxs-lookup"><span data-stu-id="7d430-147">**To create a Data Lake Analytics job script**</span></span>

<span data-ttu-id="7d430-148">使用下列 U-SQL 指令碼建立文字檔，並將該檔案儲存到您的工作站：</span><span class="sxs-lookup"><span data-stu-id="7d430-148">Create a text file with following U-SQL script, and save the text file to your workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="7d430-149">此 U-SQL 指令碼會使用 **Extractors.Tsv()** 讀取來源資料檔案，然後使用 **Outputters.Csv()** 建立 csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="7d430-149">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="7d430-150">除非您將來源檔案複製到其他位置，否則請勿修改這兩個路徑。</span><span class="sxs-lookup"><span data-stu-id="7d430-150">Don't modify the two paths unless you copy the source file into a different location.</span></span>  <span data-ttu-id="7d430-151">Data Lake Analytics 會建立輸出資料夾 (若尚未建立)。</span><span class="sxs-lookup"><span data-stu-id="7d430-151">Data Lake Analytics creates the output folder if it doesn't exist.</span></span>

<span data-ttu-id="7d430-152">使用儲存在預設 Data Lake Store 帳戶中檔案的相對路徑，是比較容易的方法。</span><span class="sxs-lookup"><span data-stu-id="7d430-152">It is simpler to use relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="7d430-153">您也可以使用絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="7d430-153">You can also use absolute paths.</span></span>  <span data-ttu-id="7d430-154">例如：</span><span class="sxs-lookup"><span data-stu-id="7d430-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="7d430-155">您必須使用絕對路徑存取連結儲存體帳戶中的檔案。</span><span class="sxs-lookup"><span data-stu-id="7d430-155">You must use absolute paths to access files in linked Storage accounts.</span></span>  <span data-ttu-id="7d430-156">儲存在連結 Azure 儲存體帳戶中之檔案的語法是：</span><span class="sxs-lookup"><span data-stu-id="7d430-156">The syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="7d430-157">不支援使用公用 blob 的 Azure Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="7d430-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="7d430-158">不支援使用公用容器的 Azure Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="7d430-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="7d430-159">**提交作業**</span><span class="sxs-lookup"><span data-stu-id="7d430-159">**To submit jobs**</span></span>

<span data-ttu-id="7d430-160">使用以下語法提交作業。</span><span class="sxs-lookup"><span data-stu-id="7d430-160">Use the following syntax to submit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="7d430-161">例如：</span><span class="sxs-lookup"><span data-stu-id="7d430-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="7d430-162">**若要列出作業並顯示作業詳細資料**</span><span class="sxs-lookup"><span data-stu-id="7d430-162">**To list jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="7d430-163">**取消作業**</span><span class="sxs-lookup"><span data-stu-id="7d430-163">**To cancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="7d430-164">擷取作業結果</span><span class="sxs-lookup"><span data-stu-id="7d430-164">Retrieve job results</span></span>

<span data-ttu-id="7d430-165">作業完成之後，您可以使用下列命令列出該輸出檔案，並下載檔案：</span><span class="sxs-lookup"><span data-stu-id="7d430-165">After a job is completed, you can use the following commands to list the output files, and download the files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="7d430-166">例如：</span><span class="sxs-lookup"><span data-stu-id="7d430-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="7d430-167">管線和週期</span><span class="sxs-lookup"><span data-stu-id="7d430-167">Pipelines and recurrences</span></span>

<span data-ttu-id="7d430-168">**取得管線和週期的相關資訊**</span><span class="sxs-lookup"><span data-stu-id="7d430-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="7d430-169">使用 `az dla job pipeline` 命令來查看先前提交作業的管線資訊。</span><span class="sxs-lookup"><span data-stu-id="7d430-169">Use the `az dla job pipeline` commands to see the pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="7d430-170">使用 `az dla job recurrence` 命令來查看先前提交作業的週期資訊。</span><span class="sxs-lookup"><span data-stu-id="7d430-170">Use the `az dla job recurrence` commands to see the recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="7d430-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d430-171">Next steps</span></span>

* <span data-ttu-id="7d430-172">若要查看 Data Lake Analytics CLI 2.0 參考文件，請參閱 [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla)。</span><span class="sxs-lookup"><span data-stu-id="7d430-172">To see the Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="7d430-173">若要查看 Data Lake Store CLI 2.0 參考文件，請參閱 [Data Lake Store](https://docs.microsoft.com/cli/azure/dls)。</span><span class="sxs-lookup"><span data-stu-id="7d430-173">To see the Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="7d430-174">若要了解更複雜的查詢，請參閱 [使用 Azure Data Lake Analytics 來分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。</span><span class="sxs-lookup"><span data-stu-id="7d430-174">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
