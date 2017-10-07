---
title: "開始使用 Azure CLI 2.0 的 Azure Data Lake Analytics aaaGet |Microsoft 文件"
description: "了解如何 toouse hello Azure 命令列介面 2.0 toocreate Data Lake Analytics 帳戶中建立使用 U SQL Data Lake Analytics 工作並送出 hello 作業。 "
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
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="6805f-103">使用 Azure CLI 2.0 開始使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6805f-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="6805f-104">在本教學課程中，您會開發一個作業可讀取定位字元分隔值 (TSV) 檔案，並將該檔案轉換為逗點分隔值 (CSV) 檔案。</span><span class="sxs-lookup"><span data-stu-id="6805f-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="6805f-105">透過相同的教學課程使用其他支援的 hello toogo 工具，在這一節的 hello 最上層使用 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="6805f-105">toogo through hello same tutorial using other supported tools, use hello dropdown list on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6805f-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="6805f-106">Prerequisites</span></span>
<span data-ttu-id="6805f-107">開始本教學課程之前，您必須具備下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="6805f-107">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="6805f-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="6805f-108">**An Azure subscription**.</span></span> <span data-ttu-id="6805f-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6805f-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6805f-110">**Azure CLI 2.0**.</span><span class="sxs-lookup"><span data-stu-id="6805f-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="6805f-111">請參閱 [安裝和設定 Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6805f-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="6805f-112">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="6805f-112">Log in tooAzure</span></span>

<span data-ttu-id="6805f-113">toolog tooyour Azure 訂用帳戶中：</span><span class="sxs-lookup"><span data-stu-id="6805f-113">toolog in tooyour Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="6805f-114">您要求的 toobrowse tooa URL，而且輸入驗證碼。</span><span class="sxs-lookup"><span data-stu-id="6805f-114">You are requested toobrowse tooa URL, and enter an authentication code.</span></span>  <span data-ttu-id="6805f-115">然後依照 hello 指示 tooenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="6805f-115">And then follow hello instructions tooenter your credentials.</span></span>

<span data-ttu-id="6805f-116">一旦您登入，hello 登入的命令會列出訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6805f-116">Once you have logged in, hello login command lists your subscriptions.</span></span>

<span data-ttu-id="6805f-117">toouse 特定訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="6805f-117">toouse a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="6805f-118">建立 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="6805f-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="6805f-119">您需要 Data Lake Analytics 帳戶，才能執行作業。</span><span class="sxs-lookup"><span data-stu-id="6805f-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="6805f-120">toocreate Data Lake Analytics 帳戶，您必須指定下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="6805f-120">toocreate a Data Lake Analytics account, you must specify hello following items:</span></span>

* <span data-ttu-id="6805f-121">**Azure 資源群組**。</span><span class="sxs-lookup"><span data-stu-id="6805f-121">**Azure Resource Group**.</span></span> <span data-ttu-id="6805f-122">Data Lake Analytics 帳戶必須建立在 Azure 資源群組內。</span><span class="sxs-lookup"><span data-stu-id="6805f-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="6805f-123">[Azure 資源管理員](../azure-resource-manager/resource-group-overview.md)可讓您與您的應用程式，為群組中的 hello 資源 toowork。</span><span class="sxs-lookup"><span data-stu-id="6805f-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you toowork with hello resources in your application as a group.</span></span> <span data-ttu-id="6805f-124">您可以部署、 更新或刪除 hello 資源的所有應用程式在單一、 協調作業。</span><span class="sxs-lookup"><span data-stu-id="6805f-124">You can deploy, update, or delete all of hello resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="6805f-125">toolist hello 現有資源群組您的訂用帳戶底下：</span><span class="sxs-lookup"><span data-stu-id="6805f-125">toolist hello existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="6805f-126">toocreate 新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="6805f-126">toocreate a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="6805f-127">**Data Lake Analytics 帳戶名稱**。</span><span class="sxs-lookup"><span data-stu-id="6805f-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="6805f-128">每一個 Data Lake Analytics 帳戶都有名稱。</span><span class="sxs-lookup"><span data-stu-id="6805f-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="6805f-129">**位置**。</span><span class="sxs-lookup"><span data-stu-id="6805f-129">**Location**.</span></span> <span data-ttu-id="6805f-130">使用其中一個支援 Data Lake Analytics 的 hello Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="6805f-130">Use one of hello Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="6805f-131">**預設 Data Lake Store 帳戶**：每個 Data Lake Analytics 帳戶都有一個預設的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6805f-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="6805f-132">toolist hello 現有 Data Lake Store 帳戶：</span><span class="sxs-lookup"><span data-stu-id="6805f-132">toolist hello existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="6805f-133">toocreate 新的 Data Lake Store 帳戶：</span><span class="sxs-lookup"><span data-stu-id="6805f-133">toocreate a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="6805f-134">使用下列語法 toocreate Data Lake Analytics 帳戶的 hello:</span><span class="sxs-lookup"><span data-stu-id="6805f-134">Use hello following syntax toocreate a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="6805f-135">建立帳戶後，您可以使用下列命令 toolist hello 帳戶 hello，並顯示 帳戶詳細資料：</span><span class="sxs-lookup"><span data-stu-id="6805f-135">After creating an account, you can use hello following commands toolist hello accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a><span data-ttu-id="6805f-136">上傳資料 tooData 湖存放區</span><span class="sxs-lookup"><span data-stu-id="6805f-136">Upload data tooData Lake Store</span></span>
<span data-ttu-id="6805f-137">在本教學課程中，您會處理一些搜尋記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6805f-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="6805f-138">hello 搜尋記錄檔可以儲存在資料湖存放區或 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="6805f-138">hello search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="6805f-139">hello Azure 入口網站提供使用者介面複製某些範例資料檔案 toohello 預設 Data Lake Store 帳戶，包括搜尋記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6805f-139">hello Azure portal provides a user interface for copying some sample data files toohello default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="6805f-140">請參閱[準備來源資料](data-lake-analytics-get-started-portal.md)tooupload hello 資料 toohello 預設 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6805f-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) tooupload hello data toohello default Data Lake Store account.</span></span>

<span data-ttu-id="6805f-141">使用 CLI 2.0 tooupload 檔案中使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6805f-141">tooupload files using CLI 2.0, use hello following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="6805f-142">Data Lake Analytics 也可存取 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="6805f-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="6805f-143">上傳資料 tooAzure Blob 儲存體，請參閱[使用 hello 與 Azure 儲存體的 Azure CLI](../storage/common/storage-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="6805f-143">For uploading data tooAzure Blob storage, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="6805f-144">提交 Data Lake Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="6805f-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="6805f-145">hello Data Lake Analytics 工作是以 hello U-SQL 語言撰寫。</span><span class="sxs-lookup"><span data-stu-id="6805f-145">hello Data Lake Analytics jobs are written in hello U-SQL language.</span></span> <span data-ttu-id="6805f-146">toolearn 進一步了解 U-SQL，請參閱[開始使用 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)和[U-SQL 語言 eence](http://go.microsoft.com/fwlink/?LinkId=691348)。</span><span class="sxs-lookup"><span data-stu-id="6805f-146">toolearn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="6805f-147">**toocreate Data Lake Analytics 作業指令碼**</span><span class="sxs-lookup"><span data-stu-id="6805f-147">**toocreate a Data Lake Analytics job script**</span></span>

<span data-ttu-id="6805f-148">使用下列的 U-SQL 指令碼，建立文字檔案，並將儲存 hello 文字檔案 tooyour 工作站：</span><span class="sxs-lookup"><span data-stu-id="6805f-148">Create a text file with following U-SQL script, and save hello text file tooyour workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="6805f-149">此 U-SQL 指令碼會讀取 hello 來源資料檔案使用**Extractors.Tsv()**，然後建立使用 csv 檔案**Outputters.Csv()**。</span><span class="sxs-lookup"><span data-stu-id="6805f-149">This U-SQL script reads hello source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="6805f-150">請勿修改 hello 兩個路徑，除非您將 hello 原始程式檔複製到不同的位置。</span><span class="sxs-lookup"><span data-stu-id="6805f-150">Don't modify hello two paths unless you copy hello source file into a different location.</span></span>  <span data-ttu-id="6805f-151">Data Lake Analytics 建立 hello 輸出資料夾，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="6805f-151">Data Lake Analytics creates hello output folder if it doesn't exist.</span></span>

<span data-ttu-id="6805f-152">它是簡單 toouse 預設 Data Lake Store 帳戶中儲存的檔案相對路徑。</span><span class="sxs-lookup"><span data-stu-id="6805f-152">It is simpler toouse relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="6805f-153">您也可以使用絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="6805f-153">You can also use absolute paths.</span></span>  <span data-ttu-id="6805f-154">例如：</span><span class="sxs-lookup"><span data-stu-id="6805f-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="6805f-155">您必須使用連結的儲存體帳戶中的絕對路徑 tooaccess 檔案。</span><span class="sxs-lookup"><span data-stu-id="6805f-155">You must use absolute paths tooaccess files in linked Storage accounts.</span></span>  <span data-ttu-id="6805f-156">檔案儲存在連結的 Azure 儲存體帳戶中的 hello 語法為：</span><span class="sxs-lookup"><span data-stu-id="6805f-156">hello syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="6805f-157">不支援使用公用 blob 的 Azure Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="6805f-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="6805f-158">不支援使用公用容器的 Azure Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="6805f-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="6805f-159">**toosubmit 工作**</span><span class="sxs-lookup"><span data-stu-id="6805f-159">**toosubmit jobs**</span></span>

<span data-ttu-id="6805f-160">使用下列語法 toosubmit 作業 hello。</span><span class="sxs-lookup"><span data-stu-id="6805f-160">Use hello following syntax toosubmit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="6805f-161">例如：</span><span class="sxs-lookup"><span data-stu-id="6805f-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="6805f-162">**toolist 作業與顯示工作詳細資料**</span><span class="sxs-lookup"><span data-stu-id="6805f-162">**toolist jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="6805f-163">**toocancel 工作**</span><span class="sxs-lookup"><span data-stu-id="6805f-163">**toocancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="6805f-164">擷取作業結果</span><span class="sxs-lookup"><span data-stu-id="6805f-164">Retrieve job results</span></span>

<span data-ttu-id="6805f-165">作業完成之後，您可以使用下列命令 toolist hello 輸出檔案的 hello 和下載 hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="6805f-165">After a job is completed, you can use hello following commands toolist hello output files, and download hello files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="6805f-166">例如：</span><span class="sxs-lookup"><span data-stu-id="6805f-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="6805f-167">管線和週期</span><span class="sxs-lookup"><span data-stu-id="6805f-167">Pipelines and recurrences</span></span>

<span data-ttu-id="6805f-168">**取得管線和週期的相關資訊**</span><span class="sxs-lookup"><span data-stu-id="6805f-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="6805f-169">使用 hello `az dla job pipeline` toosee hello 管線資訊先前已送出工作的命令。</span><span class="sxs-lookup"><span data-stu-id="6805f-169">Use hello `az dla job pipeline` commands toosee hello pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="6805f-170">使用 hello`az dla job recurrence`命令 toosee hello 循環資訊，如先前已提交的工作。</span><span class="sxs-lookup"><span data-stu-id="6805f-170">Use hello `az dla job recurrence` commands toosee hello recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="6805f-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6805f-171">Next steps</span></span>

* <span data-ttu-id="6805f-172">toosee hello 資料湖分析 CLI 2.0 參考文件，請參閱[Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla)。</span><span class="sxs-lookup"><span data-stu-id="6805f-172">toosee hello Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="6805f-173">toosee hello 資料湖存放區 CLI 2.0 參考文件，請參閱[Data Lake Store](https://docs.microsoft.com/cli/azure/dls)。</span><span class="sxs-lookup"><span data-stu-id="6805f-173">toosee hello Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="6805f-174">toosee 更複雜的查詢，請參閱[使用 Azure Data Lake Analytics 分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。</span><span class="sxs-lookup"><span data-stu-id="6805f-174">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
