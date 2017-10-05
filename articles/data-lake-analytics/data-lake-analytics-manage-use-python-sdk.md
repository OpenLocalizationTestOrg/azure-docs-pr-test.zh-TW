---
title: "使用 Python 來管理 Azure Data Lake Analytics | Microsoft Docs"
description: "了解如何使用 Python 來建立 Data Lake Store 帳戶及提交作業。 "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 31326a32f8748e6cfb8bfe24cda46c511ab59352
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="78571-103">使用 Python 來管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="78571-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="78571-104">Python 版本</span><span class="sxs-lookup"><span data-stu-id="78571-104">Python versions</span></span>

* <span data-ttu-id="78571-105">使用 64 位元版 Python。</span><span class="sxs-lookup"><span data-stu-id="78571-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="78571-106">您可以使用在 **[Python.org 下載](https://www.python.org/downloads/)** \(英文\) 找到的標準 Python 散發套件。</span><span class="sxs-lookup"><span data-stu-id="78571-106">You can use the standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="78571-107">許多開發人員發現使用 **[Anaconda Python 散發套件](https://www.continuum.io/downloads)** \(英文\) 相當便利。</span><span class="sxs-lookup"><span data-stu-id="78571-107">Many developers find it convenient to use the **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="78571-108">本文是使用來自標準 Python 散發套件的 Python 3.6 版來撰寫的</span><span class="sxs-lookup"><span data-stu-id="78571-108">This article was written using Python version 3.6 from the standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="78571-109">安裝 Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="78571-109">Install Azure Python SDK</span></span>

<span data-ttu-id="78571-110">請安裝下列模組：</span><span class="sxs-lookup"><span data-stu-id="78571-110">Install the following modules:</span></span>

* <span data-ttu-id="78571-111">**azure-mgmt-resource** 模組包含適用於 Active Directory 等等的其他 Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="78571-111">The **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="78571-112">**azure-mgmt-datalake-store** 模組包含 Azure Data Lake Store 帳戶管理作業。</span><span class="sxs-lookup"><span data-stu-id="78571-112">The **azure-mgmt-datalake-store** module includes the Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="78571-113">**azure-datalake-store** 模組包含 Azure Data Lake Store 檔案系統作業。</span><span class="sxs-lookup"><span data-stu-id="78571-113">The **azure-datalake-store** module includes the Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="78571-114">**azure-datalake-analytics** 模組包含 Azure Data Lake Analytics 作業。</span><span class="sxs-lookup"><span data-stu-id="78571-114">The **azure-datalake-analytics** module includes the Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="78571-115">請先執行下列命令，以確保您擁有最新的 `pip`：</span><span class="sxs-lookup"><span data-stu-id="78571-115">First, ensure you have the latest `pip` by running the following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="78571-116">本文件是使用 `pip version 9.0.1` 撰寫的。</span><span class="sxs-lookup"><span data-stu-id="78571-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="78571-117">使用下列 `pip` 命令以從命令列安裝新模組：</span><span class="sxs-lookup"><span data-stu-id="78571-117">Use the following `pip` commands to install the modules from the commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="78571-118">建立新的 Python 指令碼</span><span class="sxs-lookup"><span data-stu-id="78571-118">Create a new Python script</span></span>

<span data-ttu-id="78571-119">將下列程式碼貼到指令碼中：</span><span class="sxs-lookup"><span data-stu-id="78571-119">Paste the following code into the script:</span></span>

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

<span data-ttu-id="78571-120">請執行此指令碼以確認可將模組匯入。</span><span class="sxs-lookup"><span data-stu-id="78571-120">Run this script to verify that the modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="78571-121">驗證</span><span class="sxs-lookup"><span data-stu-id="78571-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="78571-122">使用快顯視窗進行互動式使用者驗證</span><span class="sxs-lookup"><span data-stu-id="78571-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="78571-123">不支援此方法。</span><span class="sxs-lookup"><span data-stu-id="78571-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="78571-124">使用裝置代碼進行互動式使用者驗證</span><span class="sxs-lookup"><span data-stu-id="78571-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter the user to authenticate with that has permission to subscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="78571-125">使用 SPI 和祕密進行非互動式驗證</span><span class="sxs-lookup"><span data-stu-id="78571-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="78571-126">使用 API 和憑證進行非互動式驗證</span><span class="sxs-lookup"><span data-stu-id="78571-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="78571-127">不支援此方法。</span><span class="sxs-lookup"><span data-stu-id="78571-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="78571-128">通用指令碼變數</span><span class="sxs-lookup"><span data-stu-id="78571-128">Common script variables</span></span>

<span data-ttu-id="78571-129">以下是範例中使用的變數。</span><span class="sxs-lookup"><span data-stu-id="78571-129">These variables are used in the samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-the-clients"></a><span data-ttu-id="78571-130">建立用戶端</span><span class="sxs-lookup"><span data-stu-id="78571-130">Create the clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="78571-131">建立 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="78571-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="78571-132">建立 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="78571-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="78571-133">首先，建立一個存放區帳戶。</span><span class="sxs-lookup"><span data-stu-id="78571-133">First create a store account.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```
<span data-ttu-id="78571-134">接著，建立一個使用該存放區的 ADLA 帳戶。</span><span class="sxs-lookup"><span data-stu-id="78571-134">Then create an ADLA account that uses that store.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a><span data-ttu-id="78571-135">提交作業</span><span class="sxs-lookup"><span data-stu-id="78571-135">Submit a job</span></span>

```python
script = """
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
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-to-end"></a><span data-ttu-id="78571-136">等候工作結束</span><span class="sxs-lookup"><span data-stu-id="78571-136">Wait for a job to end</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="78571-137">列出管線和週期</span><span class="sxs-lookup"><span data-stu-id="78571-137">List pipelines and recurrences</span></span>
<span data-ttu-id="78571-138">視您作業是否有附加的管線或週期中繼資料而定，您可以列出管線和週期。</span><span class="sxs-lookup"><span data-stu-id="78571-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="78571-139">管理計算原則</span><span class="sxs-lookup"><span data-stu-id="78571-139">Manage compute policies</span></span>

<span data-ttu-id="78571-140">DataLakeAnalyticsAccountManagementClient 物件會提供方法，用以管理 Data Lake Analytics 帳戶的計算原則。</span><span class="sxs-lookup"><span data-stu-id="78571-140">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="78571-141">列出計算原則</span><span class="sxs-lookup"><span data-stu-id="78571-141">List compute policies</span></span>

<span data-ttu-id="78571-142">下列程式碼會擷取 Data Lake Analytics 帳戶的計算原則清單。</span><span class="sxs-lookup"><span data-stu-id="78571-142">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="78571-143">建立新的計算原則</span><span class="sxs-lookup"><span data-stu-id="78571-143">Create a new compute policy</span></span>

<span data-ttu-id="78571-144">下列程式碼會為 Data Lake Analytics 帳戶建立新的計算原則，其中是將指定使用者可用的 AU 上限設定為 50，而將作業最低優先順序設定為 250。</span><span class="sxs-lookup"><span data-stu-id="78571-144">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="78571-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="78571-145">Next steps</span></span>

- <span data-ttu-id="78571-146">若要使用其他工具檢視同一個教學課程，請按一下頁面最上方的索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="78571-146">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
- <span data-ttu-id="78571-147">若要了解 U-SQL，請參閱 [開始使用 Azure Data Lake Analytics U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="78571-147">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="78571-148">針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="78571-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

