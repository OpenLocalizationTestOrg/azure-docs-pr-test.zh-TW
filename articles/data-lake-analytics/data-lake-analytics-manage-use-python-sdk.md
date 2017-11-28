---
title: "Azure Data Lake Analytics aaaManage 使用 Python |Microsoft 文件"
description: "了解如何 toouse Python toocreate 資料湖存放區帳戶，並提交工作。 "
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
ms.openlocfilehash: 3c0fff155db7c4fd4e84c2562816995eb156be16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="6823e-103">使用 Python 來管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6823e-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="6823e-104">Python 版本</span><span class="sxs-lookup"><span data-stu-id="6823e-104">Python versions</span></span>

* <span data-ttu-id="6823e-105">使用 64 位元版 Python。</span><span class="sxs-lookup"><span data-stu-id="6823e-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="6823e-106">您可以使用 hello 位於標準 Python 發佈 **[Python.org 下載](https://www.python.org/downloads/)**。</span><span class="sxs-lookup"><span data-stu-id="6823e-106">You can use hello standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="6823e-107">許多開發人員認為它方便 toouse hello  **[Anaconda Python 發佈](https://www.continuum.io/downloads)**。</span><span class="sxs-lookup"><span data-stu-id="6823e-107">Many developers find it convenient toouse hello **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="6823e-108">使用 Python 版本 3.6 hello 標準 Python 發佈撰寫本文時</span><span class="sxs-lookup"><span data-stu-id="6823e-108">This article was written using Python version 3.6 from hello standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="6823e-109">安裝 Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="6823e-109">Install Azure Python SDK</span></span>

<span data-ttu-id="6823e-110">安裝 hello 下列模組：</span><span class="sxs-lookup"><span data-stu-id="6823e-110">Install hello following modules:</span></span>

* <span data-ttu-id="6823e-111">hello **azure mgmt 資源**模組包含 Active Directory 等其他 Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="6823e-111">hello **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="6823e-112">hello **azure mgmt-datalake 市集**模組包含 hello Azure Data Lake Store 帳戶的管理作業。</span><span class="sxs-lookup"><span data-stu-id="6823e-112">hello **azure-mgmt-datalake-store** module includes hello Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="6823e-113">hello **azure datalake 市集**模組包含 hello Azure Data Lake Store 檔案系統作業。</span><span class="sxs-lookup"><span data-stu-id="6823e-113">hello **azure-datalake-store** module includes hello Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="6823e-114">hello **azure datalake 分析**模組包含 hello Azure Data Lake Analytics 的作業。</span><span class="sxs-lookup"><span data-stu-id="6823e-114">hello **azure-datalake-analytics** module includes hello Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="6823e-115">首先，請確定您有最新的 hello`pip`藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6823e-115">First, ensure you have hello latest `pip` by running hello following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="6823e-116">本文件是使用 `pip version 9.0.1` 撰寫的。</span><span class="sxs-lookup"><span data-stu-id="6823e-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="6823e-117">使用下列 hello`pip`命令 tooinstall hello 模組從 hello commandline:</span><span class="sxs-lookup"><span data-stu-id="6823e-117">Use hello following `pip` commands tooinstall hello modules from hello commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="6823e-118">建立新的 Python 指令碼</span><span class="sxs-lookup"><span data-stu-id="6823e-118">Create a new Python script</span></span>

<span data-ttu-id="6823e-119">貼上下列程式碼到 hello 指令碼中的 hello:</span><span class="sxs-lookup"><span data-stu-id="6823e-119">Paste hello following code into hello script:</span></span>

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

<span data-ttu-id="6823e-120">執行這個指令碼 tooverify 模組匯入該 hello。</span><span class="sxs-lookup"><span data-stu-id="6823e-120">Run this script tooverify that hello modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="6823e-121">驗證</span><span class="sxs-lookup"><span data-stu-id="6823e-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="6823e-122">使用快顯視窗進行互動式使用者驗證</span><span class="sxs-lookup"><span data-stu-id="6823e-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="6823e-123">不支援此方法。</span><span class="sxs-lookup"><span data-stu-id="6823e-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="6823e-124">使用裝置代碼進行互動式使用者驗證</span><span class="sxs-lookup"><span data-stu-id="6823e-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="6823e-125">使用 SPI 和祕密進行非互動式驗證</span><span class="sxs-lookup"><span data-stu-id="6823e-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="6823e-126">使用 API 和憑證進行非互動式驗證</span><span class="sxs-lookup"><span data-stu-id="6823e-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="6823e-127">不支援此方法。</span><span class="sxs-lookup"><span data-stu-id="6823e-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="6823e-128">通用指令碼變數</span><span class="sxs-lookup"><span data-stu-id="6823e-128">Common script variables</span></span>

<span data-ttu-id="6823e-129">Hello 範例中使用這些變數。</span><span class="sxs-lookup"><span data-stu-id="6823e-129">These variables are used in hello samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a><span data-ttu-id="6823e-130">建立 hello 用戶端</span><span class="sxs-lookup"><span data-stu-id="6823e-130">Create hello clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="6823e-131">建立 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="6823e-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="6823e-132">建立 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="6823e-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="6823e-133">首先，建立一個存放區帳戶。</span><span class="sxs-lookup"><span data-stu-id="6823e-133">First create a store account.</span></span>

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
<span data-ttu-id="6823e-134">接著，建立一個使用該存放區的 ADLA 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6823e-134">Then create an ADLA account that uses that store.</span></span>

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

## <a name="submit-a-job"></a><span data-ttu-id="6823e-135">提交作業</span><span class="sxs-lookup"><span data-stu-id="6823e-135">Submit a job</span></span>

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
    too"/data.csv"
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

## <a name="wait-for-a-job-tooend"></a><span data-ttu-id="6823e-136">等候工作 tooend</span><span class="sxs-lookup"><span data-stu-id="6823e-136">Wait for a job tooend</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="6823e-137">列出管線和週期</span><span class="sxs-lookup"><span data-stu-id="6823e-137">List pipelines and recurrences</span></span>
<span data-ttu-id="6823e-138">視您作業是否有附加的管線或週期中繼資料而定，您可以列出管線和週期。</span><span class="sxs-lookup"><span data-stu-id="6823e-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="6823e-139">管理計算原則</span><span class="sxs-lookup"><span data-stu-id="6823e-139">Manage compute policies</span></span>

<span data-ttu-id="6823e-140">hello DataLakeAnalyticsAccountManagementClient 物件提供用來管理 hello 方法計算的資料湖分析帳戶原則。</span><span class="sxs-lookup"><span data-stu-id="6823e-140">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="6823e-141">列出計算原則</span><span class="sxs-lookup"><span data-stu-id="6823e-141">List compute policies</span></span>

<span data-ttu-id="6823e-142">下列程式碼的 hello 擷取 Data Lake Analytics 帳戶的計算原則的清單。</span><span class="sxs-lookup"><span data-stu-id="6823e-142">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="6823e-143">建立新的計算原則</span><span class="sxs-lookup"><span data-stu-id="6823e-143">Create a new compute policy</span></span>

<span data-ttu-id="6823e-144">下列程式碼的 hello 建立 Data Lake Analytics 帳戶的新計算原則，設定 hello 最大澳洲可用 toohello 指定使用者 too50 和 hello 最小的工作優先權 too250。</span><span class="sxs-lookup"><span data-stu-id="6823e-144">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="6823e-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6823e-145">Next steps</span></span>

- <span data-ttu-id="6823e-146">toosee hello 相同教學課程中使用其他工具中，按一下在 hello hello 頁面最上方的 hello 索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="6823e-146">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
- <span data-ttu-id="6823e-147">toolearn U-SQL，請參閱[開始使用 Azure 資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6823e-147">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="6823e-148">針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6823e-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

