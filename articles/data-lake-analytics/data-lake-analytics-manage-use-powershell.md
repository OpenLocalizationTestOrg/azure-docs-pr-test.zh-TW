---
title: "使用 Azure PowerShell 的 Azure Data Lake Analytics aaaManage |Microsoft 文件"
description: "了解 toomanage Data Lake Analytics 帳戶，資料來源的工作，以及類別目錄項目。 "
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
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>使用 Azure PowerShell 管理 Azure Data Lake Analytics
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

了解如何 toomanage Azure Data Lake Analytics 帳戶，資料來源的工作，以及使用 Azure PowerShell 的類別目錄項目。 

## <a name="prerequisites"></a>必要條件

建立 Data Lake Analytics 帳戶時，您會需要 tooknow:

* **訂用帳戶 ID**: hello Data Lake Analytics 帳戶所在的 Azure 訂用帳戶 ID。
* **資源群組**: hello hello 包含 Data Lake Analytics 帳戶的 Azure 資源群組名稱。
* **Data Lake Analytics 帳戶名稱**: hello 帳戶名稱只能包含小寫字母和數字。
* **預設 Data Lake Store 帳戶**：每個 Data Lake Analytics 帳戶都有一個預設的 Data Lake Store 帳戶。 這些帳戶必須是 hello 中相同的位置。
* **位置**: hello 位置，您的 Data Lake Analytics 帳戶，例如 「 美國東部 2 」 或其他支援的位置。 您可以在我們的[價格頁面](https://azure.microsoft.com/pricing/details/data-lake-analytics/)上看到支援的位置。

在此教學課程中的 hello PowerShell 程式碼片段會使用這些變數 toostore 這項資訊

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>登入

使用訂用帳戶 ID 來登入。

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

使用訂用帳戶名稱來登入。

```
Login-AzureRmAccount -SubscriptionName $subname 
```

hello `Login-AzureRmAccount` cmdlet 永遠提示輸入認證。 您可以避免使用下列 cmdlet 的 hello 提示：

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>管理帳戶

### <a name="create-a-data-lake-analytics-account"></a>建立 Data Lake Analytics 帳戶

如果您還沒有[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)toouse，建立一個。 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

每個 Data Lake Analytics 帳戶都需要預設 Data Lake Store 帳戶，用於儲存記錄。 您可以重複使用現有的帳戶，或建立一個帳戶。 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

資源群組和 Data Lake Store 帳戶一旦可用，請建立 Data Lake Analytics 帳戶。

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>取得帳戶的相關資訊

取得帳戶的相關詳細資料。

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

請檢查特定的資料湖分析帳戶 hello 存在。 hello cmdlet 會傳回`True`或`False`。

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

請檢查特定的 Data Lake Store 帳戶 hello 存在。 hello cmdlet 會傳回`True`或`False`。

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>列出帳戶

清單資料湖分析帳戶 hello 目前訂用帳戶內。

```powershell
Get-AdlAnalyticsAccount
```

列出特定資源群組內的 Data Lake Analytics 帳戶。

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>管理防火牆規則

列出防火牆規則。

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

新增防火牆規則。

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

變更防火牆規則。

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

移除防火牆規則。

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



允許 Azure IP 位址。

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>管理資料來源
Azure Data Lake Analytics 目前支援下列資料來源的 hello:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure 儲存體](../storage/common/storage-introduction.md)

當您建立 Analytics 帳戶時，您必須指定 Data Lake Store 帳戶 toobe hello 預設資料來源。 hello 資料湖存放區會使用預設帳戶 toostore 工作中繼資料和作業的稽核記錄檔。 建立 Data Lake Analytics 帳戶之後，您可以新增其他 Data Lake Store 帳戶和/或儲存體帳戶。 

### <a name="find-hello-default-data-lake-store-account"></a>找不到 hello 預設 Data Lake Store 帳戶

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

您可以依 hello 篩選的資料來源的 hello 清單來尋找 hello 預設 Data Lake Store 帳戶`IsDefault`屬性：

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>建立資料來源

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>列出資料來源

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>提交 U-SQL 作業

### <a name="submit-a-string-as-a-u-sql-script"></a>以 U-SQL 指令碼形式提交字串

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a>以 U-SQL 指令碼形式提交檔案

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>列出帳戶中的作業

### <a name="list-all-hello-jobs-in-hello-account"></a>列出所有 hello 帳戶中的 hello 作業。 

hello 輸出會包含目前正在執行工作和最近完成這些工作的 hello。

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>列出特定數目的作業

預設排序工作 hello 清單在送出時間。 因此最近送出 hello 作業會先出現。 預設為 180 天，hello ADLA 帳戶會記住的工作，但只 hello hello Ge AdlJob cmdlet 預設傳回的前 500 個。 使用-最上層參數 toolist 特定數量的作業。

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>根據 hello 工作屬性值的清單作業

使用 hello`-State`參數。 您可以結合以下這些值：

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
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

使用 hello`-Result`參數 toodetect 結束的作業是否已順利完成。 它有下列值：

* Cancelled
* Failed
* None
* Succeeded

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


hello`-Submitter`參數可協助您識別誰送出工作。

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

hello`-SubmittedAfter`篩選 tooa 時間範圍中很有用。


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>列出作業的常見案例


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a>篩選作業清單

在您取得目前 PowerShell 工作階段中的作業清單之後， 您可以使用標準的 PowerShell cmdlet toofilter hello 清單。

篩選器的作業 toohello 工作清單的送出 hello 中過去 24 小時

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

篩選工作結束 hello 過去 24 小時的 toohello 工作的清單

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

篩選的工作 toohello 工作開始執行的清單。 作業有可能在編譯階段即發生失敗，因而永遠不會開始。 讓我們看看實際開始執行，然後失敗的 hello 失敗作業。

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>分析作業清單

使用 hello `Group-Object` cmdlet tooanalyze 工作清單。

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
在執行分析時，可能很有用的 tooadd 屬性 toohello 工作物件 toomake 篩選和群組更簡單。 下列程式碼片段的 hello 顯示 tooannotate a JobInfo 與如何計算屬性。

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

## <a name="get-information-about-pipelines-and-recurrences"></a>取得管線和週期的相關資訊

使用 hello `Get-AdlJobPipeline` cmdlet toosee hello 管線資訊先前已送出的工作。

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

使用 hello `Get-AdlJobRecurrence` cmdlet toosee hello 循環資訊先前已提交的工作。

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>取得作業的相關資訊

### <a name="get-job-status"></a>取得作業狀態

取得 hello 特定作業的狀態。

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>檢查 hello 作業輸出

Hello 工作結束之後，請檢查所列出的資料夾中的 hello 檔案是否存在 hello 輸出檔。

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>管理執行中的作業

### <a name="cancel-a-job"></a>取消工作

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>等候工作 toofinish

而不是重複`Get-AdlAnalyticsJob`直到作業完成時，您可以使用 hello `Wait-AdlJob` hello 作業 tooend 的 cmdlet toowait。

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>管理計算原則

### <a name="list-existing-compute-policies"></a>列出現有的計算原則

hello`Get-AdlAnalyticsComputePolicy`指令程式可抓取 Data Lake Analytics 帳戶的計算原則的相關資訊。

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>建立計算原則

hello `New-AdlAnalyticsComputePolicy` cmdlet 會建立新的計算資料湖分析帳戶原則。 集 hello 最大澳洲可用 toohello 這個範例會指定使用者 too50 和 hello 最小的工作優先權 too250。

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>檢查 hello 的檔案存在。

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>上傳和下載

上傳檔案。

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

以遞迴方式上傳整個資料夾。

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

下載檔案。

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

以遞迴方式下載整個資料夾。

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> 如果 hello 上傳或下載程序將會中斷，您可以嘗試再次以 hello 執行 hello cmdlet tooresume hello 程序``-Resume``旗標。

## <a name="manage-catalog-items"></a>管理目錄項目

hello U-SQL 目錄會是使用的 toostructure 資料和程式碼，因此它們可以共用 U-SQL 指令碼。 hello 類別目錄可讓 hello Azure Data Lake 中的資料可能的最大效能。 如需詳細資訊，請參閱 [使用 U-SQL 目錄](data-lake-analytics-use-u-sql-catalog.md)。

### <a name="list-items-in-hello-u-sql-catalog"></a>Hello U-SQL 類別目錄的清單項目

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

列出所有 ADLA 帳戶中的 hello 資料庫中的所有 hello 組件。

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

### <a name="get-details-about-a-catalog-item"></a>取得目錄項目的相關詳細資料

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>在目錄中建立認證

在 U-SQL 資料庫內，為裝載於 Azure 中的資料庫建立認證物件。 目前，U SQL 認證已 hello 唯一的您可以透過 PowerShell 建立類別目錄項目類型。

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

### <a name="get-basic-information-about-an-adla-account"></a>取得 ADLA 帳戶的相關基本資訊

指定的帳戶名稱，下列程式碼的 hello 查閱 hello 帳戶的基本資訊

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

## <a name="working-with-azure"></a>使用 Azure

### <a name="get-details-of-azurerm-errors"></a>取得 AzureRm 錯誤詳細資料

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>確認您是否是以系統管理員身分執行

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>尋找 TenantID

從訂用帳戶名稱：

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

從訂用帳戶 ID：

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

從網域位址 (例如 "contoso.com")


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>列出您的所有訂用帳戶和租用戶識別碼

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>使用範本建立 Data Lake Analytics 帳戶

您也可以使用 Azure 資源群組範本，使用下列 PowerShell 指令碼的 hello:

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

如需詳細資訊，請參閱[使用 Azure Resource Manager 範本來部署應用程式](../azure-resource-manager/resource-group-template-deploy.md)和[編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。

**範例範本**

儲存下列文字當做 hello`.json`檔案，然後再使用 hello 上述 PowerShell 指令碼 toouse hello 範本。 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
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

## <a name="next-steps"></a>後續步驟
* [Microsoft Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)
* 運用 [Azure 入口網站](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md) 來開始使用 Data Lake Analytics
* 運用 [Azure 入口網站](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) 來管理 Azure Data Lake Analytics 
