---
title: "使用 Azure PowerShell 管理 Azure Data Lake Analytics | Microsoft Docs"
description: "了解如何管理 Data Lake Analytics 帳戶、資料來源、作業及目錄項目。 "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 862e9551f1e129b7bba06651fbae94e337c92dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="5b664-103">使用 Azure PowerShell 管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5b664-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="5b664-104">了解如何使用 Azure PowerShell 來管理 Azure Data Lake Analytics 帳戶、資料來源、作業及目錄項目。</span><span class="sxs-lookup"><span data-stu-id="5b664-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5b664-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="5b664-105">Prerequisites</span></span>

<span data-ttu-id="5b664-106">建立 Data Lake Analytics 帳戶時，您必須知道：</span><span class="sxs-lookup"><span data-stu-id="5b664-106">When creating a Data Lake Analytics account, you need to know:</span></span>

* <span data-ttu-id="5b664-107">**訂用帳戶 ID**：您 Data Lake Analytics 帳戶所在的 Azure 訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="5b664-107">**Subscription ID**: The Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="5b664-108">**資源群組**：包含您 Data Lake Analytics 帳戶的 Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="5b664-108">**Resource group**: The name of the Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="5b664-109">**Data Lake Analytics 帳戶名稱**：此帳戶名稱只能包含小寫字母和數字。</span><span class="sxs-lookup"><span data-stu-id="5b664-109">**Data Lake Analytics account name**: The account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="5b664-110">**預設 Data Lake Store 帳戶**：每個 Data Lake Analytics 帳戶都有一個預設的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b664-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="5b664-111">這些帳戶必須位於相同的位置。</span><span class="sxs-lookup"><span data-stu-id="5b664-111">These accounts must be in the same location.</span></span>
* <span data-ttu-id="5b664-112">**位置**：您 Data Lake Analytics 帳戶的位置，例如「美國東部 2」或其他支援的位置。</span><span class="sxs-lookup"><span data-stu-id="5b664-112">**Location**: The location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="5b664-113">您可以在我們的[價格頁面](https://azure.microsoft.com/pricing/details/data-lake-analytics/)上看到支援的位置。</span><span class="sxs-lookup"><span data-stu-id="5b664-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="5b664-114">本教學課程中的 PowerShell 程式碼片段會使用這些變數來儲存此資訊</span><span class="sxs-lookup"><span data-stu-id="5b664-114">The PowerShell snippets in this tutorial use these variables to store this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="5b664-115">登入</span><span class="sxs-lookup"><span data-stu-id="5b664-115">Log in</span></span>

<span data-ttu-id="5b664-116">使用訂用帳戶 ID 來登入。</span><span class="sxs-lookup"><span data-stu-id="5b664-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="5b664-117">使用訂用帳戶名稱來登入。</span><span class="sxs-lookup"><span data-stu-id="5b664-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="5b664-118">`Login-AzureRmAccount` Cmdlet 一律會提示輸入認證。</span><span class="sxs-lookup"><span data-stu-id="5b664-118">The `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="5b664-119">您可以使用下列 Cmdlet 來避免出現提示：</span><span class="sxs-lookup"><span data-stu-id="5b664-119">You can avoid being prompted by using the following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="5b664-120">管理帳戶</span><span class="sxs-lookup"><span data-stu-id="5b664-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="5b664-121">建立 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="5b664-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="5b664-122">如果您還沒有可使用的[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="5b664-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) to use, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="5b664-123">每個 Data Lake Analytics 帳戶都需要預設 Data Lake Store 帳戶，用於儲存記錄。</span><span class="sxs-lookup"><span data-stu-id="5b664-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="5b664-124">您可以重複使用現有的帳戶，或建立一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b664-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="5b664-125">資源群組和 Data Lake Store 帳戶一旦可用，請建立 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b664-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="5b664-126">取得帳戶的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5b664-126">Get information about an account</span></span>

<span data-ttu-id="5b664-127">取得帳戶的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5b664-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="5b664-128">檢查特定的 Data Lake Analytics 帳戶是否存在。</span><span class="sxs-lookup"><span data-stu-id="5b664-128">Check the existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="5b664-129">此 Cmdlet 會傳回 `True` 或 `False`。</span><span class="sxs-lookup"><span data-stu-id="5b664-129">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="5b664-130">檢查特定的 Data Lake Store account 帳戶是否存在。</span><span class="sxs-lookup"><span data-stu-id="5b664-130">Check the existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="5b664-131">此 Cmdlet 會傳回 `True` 或 `False`。</span><span class="sxs-lookup"><span data-stu-id="5b664-131">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="5b664-132">列出帳戶</span><span class="sxs-lookup"><span data-stu-id="5b664-132">Listing accounts</span></span>

<span data-ttu-id="5b664-133">列出目前訂用帳戶內的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b664-133">List Data Lake Analytics accounts within the current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="5b664-134">列出特定資源群組內的 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b664-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="5b664-135">管理防火牆規則</span><span class="sxs-lookup"><span data-stu-id="5b664-135">Managing firewall rules</span></span>

<span data-ttu-id="5b664-136">列出防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="5b664-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="5b664-137">新增防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="5b664-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="5b664-138">變更防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="5b664-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="5b664-139">移除防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="5b664-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="5b664-140">允許 Azure IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5b664-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="5b664-141">管理資料來源</span><span class="sxs-lookup"><span data-stu-id="5b664-141">Managing data sources</span></span>
<span data-ttu-id="5b664-142">Azure Data Lake Analytics 目前支援下列資料來源：</span><span class="sxs-lookup"><span data-stu-id="5b664-142">Azure Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="5b664-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5b664-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="5b664-144">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="5b664-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="5b664-145">當您建立 Analytics 帳戶時，必須指定一個 Data Lake Store 帳戶作為預設的資料來源。</span><span class="sxs-lookup"><span data-stu-id="5b664-145">When you create an Analytics account, you must designate a Data Lake Store account to be the default data source.</span></span> <span data-ttu-id="5b664-146">預設的 Data Lake Store 帳戶是用來儲存工作中繼資料與工作稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="5b664-146">The default Data Lake Store account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="5b664-147">建立 Data Lake Analytics 帳戶之後，您可以新增其他 Data Lake Store 帳戶和/或儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b664-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-the-default-data-lake-store-account"></a><span data-ttu-id="5b664-148">尋找預設的 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="5b664-148">Find the default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="5b664-149">您可以用 `IsDefault` 屬性篩選資料來源清單，藉此方式尋找預設的 Data Lake Store 帳戶：</span><span class="sxs-lookup"><span data-stu-id="5b664-149">You can find the default Data Lake Store account by filtering the list of datasources by the `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="5b664-150">建立資料來源</span><span class="sxs-lookup"><span data-stu-id="5b664-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="5b664-151">列出資料來源</span><span class="sxs-lookup"><span data-stu-id="5b664-151">List data sources</span></span>

```powershell
# List all the data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="5b664-152">提交 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="5b664-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="5b664-153">以 U-SQL 指令碼形式提交字串</span><span class="sxs-lookup"><span data-stu-id="5b664-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="5b664-154">以 U-SQL 指令碼形式提交檔案</span><span class="sxs-lookup"><span data-stu-id="5b664-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="5b664-155">列出帳戶中的作業</span><span class="sxs-lookup"><span data-stu-id="5b664-155">List jobs in an account</span></span>

### <a name="list-all-the-jobs-in-the-account"></a><span data-ttu-id="5b664-156">列出帳戶中的所有作業。</span><span class="sxs-lookup"><span data-stu-id="5b664-156">List all the jobs in the account.</span></span> 

<span data-ttu-id="5b664-157">輸出包含目前執行中作業和最近完成的作業。</span><span class="sxs-lookup"><span data-stu-id="5b664-157">The output includes the currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="5b664-158">列出特定數目的作業</span><span class="sxs-lookup"><span data-stu-id="5b664-158">List a specific number of jobs</span></span>

<span data-ttu-id="5b664-159">預設會在提交時排序作業清單。</span><span class="sxs-lookup"><span data-stu-id="5b664-159">By default the list of jobs is sorted on submit time.</span></span> <span data-ttu-id="5b664-160">因此，最新提交的作業會顯示在最前面。</span><span class="sxs-lookup"><span data-stu-id="5b664-160">So the most recently submitted jobs appear first.</span></span> <span data-ttu-id="5b664-161">ADLA 帳戶預設會記住 180 天內的作業，但 Ge-AdlJob Cmdlet 預設只會傳回前 500 個作業。</span><span class="sxs-lookup"><span data-stu-id="5b664-161">By default, The ADLA account remembers jobs for 180 days, but the Ge-AdlJob  cmdlet by default returns only the first 500.</span></span> <span data-ttu-id="5b664-162">請使用 -Top 參數來列出特定數目的作業。</span><span class="sxs-lookup"><span data-stu-id="5b664-162">Use -Top parameter to list a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-the-value-of-job-property"></a><span data-ttu-id="5b664-163">根據作業屬性的值列出作業</span><span class="sxs-lookup"><span data-stu-id="5b664-163">List jobs based on the value of job property</span></span>

<span data-ttu-id="5b664-164">使用 `-State` 參數。</span><span class="sxs-lookup"><span data-stu-id="5b664-164">Using the `-State` parameter.</span></span> <span data-ttu-id="5b664-165">您可以結合以下這些值：</span><span class="sxs-lookup"><span data-stu-id="5b664-165">You can combine any of these values:</span></span>

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List the running jobs
Get-AdlJob -Account $adla -State Running

# List the jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List the jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="5b664-166">使用 `-Result` 參數來偵測已結束的工作是否順利完成。</span><span class="sxs-lookup"><span data-stu-id="5b664-166">Use the `-Result` parameter to detect whether ended jobs completed successfully.</span></span> <span data-ttu-id="5b664-167">它有下列值：</span><span class="sxs-lookup"><span data-stu-id="5b664-167">It has these values:</span></span>

* <span data-ttu-id="5b664-168">Cancelled</span><span class="sxs-lookup"><span data-stu-id="5b664-168">Cancelled</span></span>
* <span data-ttu-id="5b664-169">Failed</span><span class="sxs-lookup"><span data-stu-id="5b664-169">Failed</span></span>
* <span data-ttu-id="5b664-170">None</span><span class="sxs-lookup"><span data-stu-id="5b664-170">None</span></span>
* <span data-ttu-id="5b664-171">Succeeded</span><span class="sxs-lookup"><span data-stu-id="5b664-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="5b664-172">`-Submitter` 參數可協助您識別由誰提交工作。</span><span class="sxs-lookup"><span data-stu-id="5b664-172">The `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="5b664-173">`-SubmittedAfter` 用於篩選時間範圍。</span><span class="sxs-lookup"><span data-stu-id="5b664-173">The `-SubmittedAfter` is useful in filtering to a time range.</span></span>


```powershell
# List  jobs submitted in the last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in the last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="5b664-174">列出作業的常見案例</span><span class="sxs-lookup"><span data-stu-id="5b664-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in the last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within the past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="5b664-175">篩選作業清單</span><span class="sxs-lookup"><span data-stu-id="5b664-175">Filtering a list of jobs</span></span>

<span data-ttu-id="5b664-176">在您取得目前 PowerShell 工作階段中的作業清單之後，</span><span class="sxs-lookup"><span data-stu-id="5b664-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="5b664-177">您可以使用標準 PowerShell Cmdlet 來篩選該清單。</span><span class="sxs-lookup"><span data-stu-id="5b664-177">You can use normal PowerShell cmdlets to filter the list.</span></span>

<span data-ttu-id="5b664-178">將作業清單篩選成顯示過去 24 小時提交的作業</span><span class="sxs-lookup"><span data-stu-id="5b664-178">Filter a list of jobs to the jobs submitted in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="5b664-179">將作業清單篩選成顯示過去 24 小時結束的作業</span><span class="sxs-lookup"><span data-stu-id="5b664-179">Filter a list of jobs to the jobs that ended in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="5b664-180">將作業清單篩選成顯示已開始執行的作業。</span><span class="sxs-lookup"><span data-stu-id="5b664-180">Filter a list of jobs to the jobs that started running.</span></span> <span data-ttu-id="5b664-181">作業有可能在編譯階段即發生失敗，因而永遠不會開始。</span><span class="sxs-lookup"><span data-stu-id="5b664-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="5b664-182">讓我們看看已實際開始執行然後發生失敗的失敗作業。</span><span class="sxs-lookup"><span data-stu-id="5b664-182">Let's look at the failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="5b664-183">分析作業清單</span><span class="sxs-lookup"><span data-stu-id="5b664-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="5b664-184">使用 `Group-Object` Cmdlet 來分析作業清單。</span><span class="sxs-lookup"><span data-stu-id="5b664-184">Use the `Group-Object` cmdlet to analyze a list of jobs.</span></span>

```
# Count the number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count the number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count the number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count the number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="5b664-185">執行分析時，將屬性新增到作業物件可能會相當有用，這可讓您更容易進行篩選和分組。</span><span class="sxs-lookup"><span data-stu-id="5b664-185">When performing an analysis, it can be useful to add properties to the Job objects to make filtering and grouping simpler.</span></span> <span data-ttu-id="5b664-186">下列程式碼片段說明如何使用計算的屬性來標註 JobInfo。</span><span class="sxs-lookup"><span data-stu-id="5b664-186">The following  snippet shows how to annotate a JobInfo with calculated properties.</span></span>

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="5b664-187">取得管線和週期的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5b664-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="5b664-188">使用 `Get-AdlJobPipeline` Cmdlet 來查看先前提交作業的管線資訊。</span><span class="sxs-lookup"><span data-stu-id="5b664-188">Use the `Get-AdlJobPipeline` cmdlet to see the pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="5b664-189">使用 `Get-AdlJobRecurrence` Cmdlet 來查看先前提交作業的週期資訊。</span><span class="sxs-lookup"><span data-stu-id="5b664-189">Use the `Get-AdlJobRecurrence` cmdlet to see the recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="5b664-190">取得作業的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5b664-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="5b664-191">取得作業狀態</span><span class="sxs-lookup"><span data-stu-id="5b664-191">Get job status</span></span>

<span data-ttu-id="5b664-192">取得特定作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="5b664-192">Get the status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-the-job-outputs"></a><span data-ttu-id="5b664-193">檢查作業輸出</span><span class="sxs-lookup"><span data-stu-id="5b664-193">Examine the job outputs</span></span>

<span data-ttu-id="5b664-194">在作業結束之後，請列出資料夾中的檔案，來檢查輸出檔案是否存在。</span><span class="sxs-lookup"><span data-stu-id="5b664-194">After the job has ended, check if the output file exists by listing the files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="5b664-195">管理執行中的作業</span><span class="sxs-lookup"><span data-stu-id="5b664-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="5b664-196">取消工作</span><span class="sxs-lookup"><span data-stu-id="5b664-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-to-finish"></a><span data-ttu-id="5b664-197">等候作業結束</span><span class="sxs-lookup"><span data-stu-id="5b664-197">Wait for a job to finish</span></span>

<span data-ttu-id="5b664-198">您可以不重複執行 `Get-AdlAnalyticsJob` 直到作業結束，而是使用 `Wait-AdlJob` Cmdlet 來等候作業結束。</span><span class="sxs-lookup"><span data-stu-id="5b664-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use the `Wait-AdlJob` cmdlet to wait for the job to end.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="5b664-199">管理計算原則</span><span class="sxs-lookup"><span data-stu-id="5b664-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="5b664-200">列出現有的計算原則</span><span class="sxs-lookup"><span data-stu-id="5b664-200">List existing compute policies</span></span>

<span data-ttu-id="5b664-201">`Get-AdlAnalyticsComputePolicy` Cmdlet 會擷取 Data Lake Analytics 帳戶的計算原則清單。</span><span class="sxs-lookup"><span data-stu-id="5b664-201">The `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="5b664-202">建立計算原則</span><span class="sxs-lookup"><span data-stu-id="5b664-202">Create a compute policy</span></span>

<span data-ttu-id="5b664-203">`New-AdlAnalyticsComputePolicy` Cmdlet 會為 Data Lake Analytics 帳戶建立新的計算原則。</span><span class="sxs-lookup"><span data-stu-id="5b664-203">The `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="5b664-204">這個範例會將指定使用者的可用 AU 上限設定為 50，將最低作業優先權設為 250。</span><span class="sxs-lookup"><span data-stu-id="5b664-204">This example sets  the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-the-existence-of-a-file"></a><span data-ttu-id="5b664-205">檢查檔案是否存在。</span><span class="sxs-lookup"><span data-stu-id="5b664-205">Check for the existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="5b664-206">上傳和下載</span><span class="sxs-lookup"><span data-stu-id="5b664-206">Uploading and downloading</span></span>

<span data-ttu-id="5b664-207">上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="5b664-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="5b664-208">以遞迴方式上傳整個資料夾。</span><span class="sxs-lookup"><span data-stu-id="5b664-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="5b664-209">下載檔案。</span><span class="sxs-lookup"><span data-stu-id="5b664-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="5b664-210">以遞迴方式下載整個資料夾。</span><span class="sxs-lookup"><span data-stu-id="5b664-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="5b664-211">如果上傳或下載程序中斷，您可以搭配 ``-Resume`` 旗標來重新執行該 Cmdlet，以嘗試繼續該程序。</span><span class="sxs-lookup"><span data-stu-id="5b664-211">If the upload or download process is interrupted, you can attempt to resume the process by running the cmdlet again with the ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="5b664-212">管理目錄項目</span><span class="sxs-lookup"><span data-stu-id="5b664-212">Manage catalog items</span></span>

<span data-ttu-id="5b664-213">U-SQL 目錄是用來建構資料和程式碼，讓 U-SQL 指令碼可以共用它們。</span><span class="sxs-lookup"><span data-stu-id="5b664-213">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="5b664-214">目錄可以讓 Azure Data Lake 中的資料具有可能的最高效能。</span><span class="sxs-lookup"><span data-stu-id="5b664-214">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="5b664-215">如需詳細資訊，請參閱 [使用 U-SQL 目錄](data-lake-analytics-use-u-sql-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="5b664-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-the-u-sql-catalog"></a><span data-ttu-id="5b664-216">列出 U-SQL 目錄中的項目</span><span class="sxs-lookup"><span data-stu-id="5b664-216">List items in the U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="5b664-217">列出 ADLA 帳戶中所有資料庫的所有組件。</span><span class="sxs-lookup"><span data-stu-id="5b664-217">List all the assemblies in all the databases in an ADLA Account.</span></span>

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="5b664-218">取得目錄項目的相關詳細資料</span><span class="sxs-lookup"><span data-stu-id="5b664-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="5b664-219">在目錄中建立認證</span><span class="sxs-lookup"><span data-stu-id="5b664-219">Create credentials in a catalog</span></span>

<span data-ttu-id="5b664-220">在 U-SQL 資料庫內，為裝載於 Azure 中的資料庫建立認證物件。</span><span class="sxs-lookup"><span data-stu-id="5b664-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="5b664-221">目前，U-SQL 認證是您可以透過 PowerShell 建立的唯一目錄項目類型。</span><span class="sxs-lookup"><span data-stu-id="5b664-221">Currently, U-SQL credentials are the only type of catalog item that you can create through PowerShell.</span></span>

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="5b664-222">取得 ADLA 帳戶的相關基本資訊</span><span class="sxs-lookup"><span data-stu-id="5b664-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="5b664-223">只要指定帳戶名稱，下列程式碼就會查詢該帳戶的相關基本資訊</span><span class="sxs-lookup"><span data-stu-id="5b664-223">Given an account name, the following code looks up basic information about the account</span></span>

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a><span data-ttu-id="5b664-224">使用 Azure</span><span class="sxs-lookup"><span data-stu-id="5b664-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="5b664-225">取得 AzureRm 錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="5b664-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="5b664-226">確認您是否是以系統管理員身分執行</span><span class="sxs-lookup"><span data-stu-id="5b664-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="5b664-227">尋找 TenantID</span><span class="sxs-lookup"><span data-stu-id="5b664-227">Find a TenantID</span></span>

<span data-ttu-id="5b664-228">從訂用帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="5b664-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="5b664-229">從訂用帳戶 ID：</span><span class="sxs-lookup"><span data-stu-id="5b664-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="5b664-230">從網域位址 (例如 "contoso.com")</span><span class="sxs-lookup"><span data-stu-id="5b664-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="5b664-231">列出您的所有訂用帳戶和租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="5b664-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="5b664-232">使用範本建立 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="5b664-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="5b664-233">您也可以運用下列 PowerShell 指令碼來使用「Azure 資源群組」範本：</span><span class="sxs-lookup"><span data-stu-id="5b664-233">You can also use an Azure Resource Group template using the following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update the JSON template path 

# Log in to Azure
Login-AzureRmAccount -SubscriptionId $subId

# Create the resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create the Data Lake Analytics account with the default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="5b664-234">如需詳細資訊，請參閱[使用 Azure Resource Manager 範本來部署應用程式](../azure-resource-manager/resource-group-template-deploy.md)和[編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="5b664-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5b664-235">**範例範本**</span><span class="sxs-lookup"><span data-stu-id="5b664-235">**Example template**</span></span>

<span data-ttu-id="5b664-236">請將下列文字儲存成 `.json` 檔案，然後運用上面的 PowerShell 指令碼來使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5b664-236">Save the following text as a `.json` file, and then use the preceding PowerShell script to use the template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Analytics account to create."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Store account to create."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="5b664-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b664-237">Next steps</span></span>
* [<span data-ttu-id="5b664-238">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="5b664-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="5b664-239">運用 [Azure 入口網站](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md) 來開始使用 Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5b664-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="5b664-240">運用 [Azure 入口網站](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) 來管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5b664-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
