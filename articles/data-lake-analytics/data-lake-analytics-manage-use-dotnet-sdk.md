---
title: "使用 Azure.NET SDK 的 Azure Data Lake Analytics aaaManage |Microsoft 文件"
description: "了解如何 toomanage Data Lake Analytics 作業、 資料來源的使用者。 "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 811d172d-9873-4ce9-a6d5-c1a26b374c79
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 98630ba411823644a8bce1f1b0c1331f689cbb0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="cbc5e-103">使用 Azure .NET SDK 管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cbc5e-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="cbc5e-104">了解 toomanage Azure Data Lake Analytics 帳戶、 資料來源、 使用者和工作使用 hello Azure.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cbc5e-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="cbc5e-105">Prerequisites</span></span>

* <span data-ttu-id="cbc5e-106">**已安裝 Visual Studio 2015、Visual Studio 2013 更新 4，或具有 Visual C++ 的 Visual Studio 2012**。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="cbc5e-107">**Microsoft Azure SDK for .NET 2.5 版或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="cbc5e-108">安裝使用 hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-108">Install it using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="cbc5e-109">**必要的 NuGet 套件**</span><span class="sxs-lookup"><span data-stu-id="cbc5e-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="cbc5e-110">安裝 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="cbc5e-110">Install NuGet packages</span></span>

|<span data-ttu-id="cbc5e-111">Package</span><span class="sxs-lookup"><span data-stu-id="cbc5e-111">Package</span></span>|<span data-ttu-id="cbc5e-112">版本</span><span class="sxs-lookup"><span data-stu-id="cbc5e-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="cbc5e-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="cbc5e-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="cbc5e-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="cbc5e-114">2.3.1</span></span>|
|[<span data-ttu-id="cbc5e-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="cbc5e-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="cbc5e-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="cbc5e-116">3.0.0</span></span>|
|[<span data-ttu-id="cbc5e-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="cbc5e-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="cbc5e-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="cbc5e-118">2.2.0</span></span>|
|[<span data-ttu-id="cbc5e-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="cbc5e-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="cbc5e-120">1.6.0-preview</span><span class="sxs-lookup"><span data-stu-id="cbc5e-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="cbc5e-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="cbc5e-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="cbc5e-122">3.4.0-preview</span><span class="sxs-lookup"><span data-stu-id="cbc5e-122">3.4.0-preview</span></span>|

<span data-ttu-id="cbc5e-123">您可以安裝這些套件透過 hello NuGet 命令列以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="cbc5e-123">You can install these packages via hello NuGet command line with hello following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="cbc5e-124">常用變數</span><span class="sxs-lookup"><span data-stu-id="cbc5e-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="cbc5e-125">驗證</span><span class="sxs-lookup"><span data-stu-id="cbc5e-125">Authentication</span></span>

<span data-ttu-id="cbc5e-126">您有多個選項的登入 tooAzure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-126">You have multiple options for logging on tooAzure Data Lake Analytics.</span></span> <span data-ttu-id="cbc5e-127">hello 下列程式碼片段顯示使用快顯視窗的互動式使用者驗證與驗證的範例。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-127">hello following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

``` csharp
using System;
using System.IO;
using System.Threading;
using System.Security.Cryptography.X509Certificates;

using Microsoft.Rest;
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.DataLake.Analytics;
using Microsoft.Azure.Management.DataLake.Analytics.Models;
using Microsoft.Azure.Management.DataLake.Store;
using Microsoft.Azure.Management.DataLake.Store.Models;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Azure.Graph.RBAC;

public static Program
{
   public static string TENANT = "microsoft.onmicrosoft.com";
   public static string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
   public static System.Uri ARM_TOKEN_AUDIENCE = new System.Uri( @"https://management.core.windows.net/");
   public static System.Uri ADL_TOKEN_AUDIENCE = new System.Uri( @"https://datalake.azure.net/" );
   public static System.Uri GRAPH_TOKEN_AUDIENCE = new System.Uri( @"https://graph.windows.net/" );

   static void Main(string[] args)
   {
      string MY_DOCUMENTS= System.Environment.GetFolderPath( System.Environment.SpecialFolder.MyDocuments);
      string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");

      var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
      var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var graphCreds = GetCreds_User_Popup(TENANT, GRAPH_TOKEN_AUDIENCE, CLIENTID, tokenCache);
   }
}
```

<span data-ttu-id="cbc5e-128">hello 原始程式碼**GetCreds_User_Popup** hello 的其他驗證選項中涵蓋的程式碼和[資料湖分析.NET 驗證選項](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span><span class="sxs-lookup"><span data-stu-id="cbc5e-128">hello source code for **GetCreds_User_Popup** and hello code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-hello-client-management-objects"></a><span data-ttu-id="cbc5e-129">建立 hello 用戶端管理物件</span><span class="sxs-lookup"><span data-stu-id="cbc5e-129">Create hello client management objects</span></span>

``` csharp
var resourceManagementClient = new ResourceManagementClient(armCreds) { SubscriptionId = subid };

var adlaAccountClient = new DataLakeAnalyticsAccountManagementClient(armCreds);
adlaAccountClient.SubscriptionId = subid;

var adlsAccountClient = new DataLakeStoreAccountManagementClient(armCreds);
adlsAccountClient.SubscriptionId = subid;

var adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClient(adlCreds);
var adlaJobClient = new DataLakeAnalyticsJobManagementClient(adlCreds);

var adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(adlCreds);

var  graphClient = new GraphRbacManagementClient(graphCreds);
graphClient.TenantID = domain;

```

## <a name="manage-accounts"></a><span data-ttu-id="cbc5e-130">管理帳戶</span><span class="sxs-lookup"><span data-stu-id="cbc5e-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="cbc5e-131">建立 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="cbc5e-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="cbc5e-132">如果您尚未建立一個，您必須有 Azure 資源群組 toocreate Data Lake Analytics 元件。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-132">If you haven't already created one, you must have an Azure Resource Group toocreate your Data Lake Analytics components.</span></span> <span data-ttu-id="cbc5e-133">您將需要您的驗證認證、訂用帳戶 ID 及一個位置。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="cbc5e-134">hello 下列程式碼會示範如何 toocreate 資源群組：</span><span class="sxs-lookup"><span data-stu-id="cbc5e-134">hello following code shows how toocreate a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="cbc5e-135">如需詳細資訊，請參閱 [Azure 資源群組和 Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics)。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="cbc5e-136">建立 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="cbc5e-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="cbc5e-137">每個 ADLA 帳戶都需要一個 ADLS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="cbc5e-138">如果您還沒有一個 toouse，您可以建立一個以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbc5e-138">If you don't already have one toouse, you can create one with hello following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="cbc5e-139">建立 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="cbc5e-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="cbc5e-140">下列程式碼的 hello 建立 ADLS 帳戶</span><span class="sxs-lookup"><span data-stu-id="cbc5e-140">hello following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="cbc5e-141">列出 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="cbc5e-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="cbc5e-142">列出 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="cbc5e-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="cbc5e-143">檢查帳戶是否存在</span><span class="sxs-lookup"><span data-stu-id="cbc5e-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="cbc5e-144">取得帳戶的相關資訊</span><span class="sxs-lookup"><span data-stu-id="cbc5e-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="cbc5e-145">刪除帳戶</span><span class="sxs-lookup"><span data-stu-id="cbc5e-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a><span data-ttu-id="cbc5e-146">取得 hello 預設 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="cbc5e-146">Get hello default Data Lake Store account</span></span>

<span data-ttu-id="cbc5e-147">每個 Data Lake Analytics 帳戶都必須擁有預設 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="cbc5e-148">使用此程式碼 toodetermine hello 預設存放區帳戶 Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-148">Use this code toodetermine hello default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="cbc5e-149">管理資料來源</span><span class="sxs-lookup"><span data-stu-id="cbc5e-149">Manage data sources</span></span>

<span data-ttu-id="cbc5e-150">Data Lake Analytics 目前支援下列資料來源的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbc5e-150">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="cbc5e-151">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cbc5e-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="cbc5e-152">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="cbc5e-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a><span data-ttu-id="cbc5e-153">連結 tooan Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="cbc5e-153">Link tooan Azure Storage account</span></span>

<span data-ttu-id="cbc5e-154">您可以建立連結 tooAzure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-154">You can create links tooAzure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="cbc5e-155">列出 Azure 儲存體資料來源</span><span class="sxs-lookup"><span data-stu-id="cbc5e-155">List Azure Storage data sources</span></span>

``` csharp
var stg_accounts = adlaAccountClient.StorageAccounts.ListByAccount(rg, adla);

if (stg_accounts != null)
{
  foreach (var stg_account in stg_accounts)
  {
      Console.WriteLine($"Storage account: {0}", stg_account.Name);
  }
}
```

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="cbc5e-156">列出 Data Lake Store 資料來源</span><span class="sxs-lookup"><span data-stu-id="cbc5e-156">List Data Lake Store data sources</span></span>

``` csharp
var adls_accounts = adlsClient.Account.List();

if (adls_accounts != null)
{
  foreach (var adls_accnt in adls_accounts)
  {
      Console.WriteLine($"ADLS account: {0}", adls_accnt.Name);
  }
}
```

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="cbc5e-157">上傳及下載資料夾和檔案</span><span class="sxs-lookup"><span data-stu-id="cbc5e-157">Upload and download folders and files</span></span>
<span data-ttu-id="cbc5e-158">您可以使用 hello Data Lake Store 檔案系統用戶端管理物件 tooupload 並下載個別檔案或資料夾從 Azure tooyour 本機電腦，使用下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="cbc5e-158">You can use hello Data Lake Store file system client management object tooupload and download individual files or folders from Azure tooyour local computer, using hello following methods:</span></span>

- <span data-ttu-id="cbc5e-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="cbc5e-159">UploadFolder</span></span>
- <span data-ttu-id="cbc5e-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="cbc5e-160">UploadFile</span></span>
- <span data-ttu-id="cbc5e-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="cbc5e-161">DownloadFolder</span></span>
- <span data-ttu-id="cbc5e-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="cbc5e-162">DownloadFile</span></span>

<span data-ttu-id="cbc5e-163">hello 這些方法的第一個參數是 hello hello 資料湖存放區帳戶，後面接著 hello 來源路徑與 hello 目的地路徑的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-163">hello first parameter for these methods is hello name of hello Data Lake Store Account, followed by parameters for hello source path and hello destination path.</span></span>

<span data-ttu-id="cbc5e-164">hello 下列範例顯示如何 toodownload 資料夾中的 hello 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-164">hello following example shows how toodownload a folder in hello Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="cbc5e-165">在 Data Lake Store 帳戶中建立檔案</span><span class="sxs-lookup"><span data-stu-id="cbc5e-165">Create a file in a Data Lake Store account</span></span>

``` csharp
using (var memstream = new MemoryStream())
{
   using (var sw = new StreamWriter(memstream, UTF8Encoding.UTF8))
   {
      sw.WriteLine("Hello World");
      sw.Flush();

      adlsFileSystemClient.FileSystem.Create(adls, "/Samples/Output/randombytes.csv", memstream);
   }
}
```

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="cbc5e-166">確認 Azure 儲存體帳戶路徑</span><span class="sxs-lookup"><span data-stu-id="cbc5e-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="cbc5e-167">hello 下列程式碼會檢查當 Azure 儲存體帳戶 (storageAccntName) 存在於資料湖分析帳戶 (analyticsAccountName)，而且如果 hello Azure 儲存體帳戶中存在的容器 (containerName)。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-167">hello following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in hello Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="cbc5e-168">管理目錄和作業</span><span class="sxs-lookup"><span data-stu-id="cbc5e-168">Manage catalog and jobs</span></span>
<span data-ttu-id="cbc5e-169">hello DataLakeAnalyticsCatalogManagementClient 物件會提供管理 hello SQL database 針對每個 Azure 資料湖分析帳戶提供的方法。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-169">hello DataLakeAnalyticsCatalogManagementClient object provides methods for managing hello SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="cbc5e-170">hello DataLakeAnalyticsJobManagementClient 提供方法 toosubmit 及管理 hello U-SQL 指令碼的資料庫上執行的工作。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-170">hello DataLakeAnalyticsJobManagementClient provides methods toosubmit and manage jobs run on hello database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="cbc5e-171">列出資料庫和結構描述</span><span class="sxs-lookup"><span data-stu-id="cbc5e-171">List databases and schemas</span></span>
<span data-ttu-id="cbc5e-172">Hello 幾件事您可以列出，最常見的 hello 包括資料庫和其結構描述。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-172">Among hello several things you can list, hello most common are databases and their schema.</span></span> <span data-ttu-id="cbc5e-173">hello 下列程式碼取得集合的資料庫，並且然後列舉 hello 每個資料庫的結構描述。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-173">hello following code obtains a collection of databases, and then enumerates hello schema for each database.</span></span>

``` csharp
var databases = adlaCatalogClient.Catalog.ListDatabases(adla);
foreach (var db in databases)
{
  Console.WriteLine($"Database: {db.Name}");
  Console.WriteLine(" - Schemas:");
  var schemas = adlaCatalogClient.Catalog.ListSchemas(adla, db.Name);
  foreach (var schm in schemas)
  {
      Console.WriteLine($"\t{schm.Name}");
  }
}
```

### <a name="list-table-columns"></a><span data-ttu-id="cbc5e-174">列出資料表資料行</span><span class="sxs-lookup"><span data-stu-id="cbc5e-174">List table columns</span></span>
<span data-ttu-id="cbc5e-175">hello 下列程式碼會示範如何 tooaccess hello 與資料湖分析目錄管理用戶端 toolist hello 資料表資料行指定的資料庫。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-175">hello following code shows how tooaccess hello database with a Data Lake Analytics Catalog management client toolist hello columns in a specified table.</span></span>

``` csharp
var tbl = adlaCatalogClient.Catalog.GetTable(adla, "master", "dbo", "MyTableName");
IEnumerable<USqlTableColumn> columns = tbl.ColumnList;

foreach (USqlTableColumn utc in columns)
{
  string scriptPath = "/Samples/Scripts/SearchResults_Wikipedia_Script.txt";
  Stream scriptStrm = adlsFileSystemClient.FileSystem.Open(_adlsAccountName, scriptPath);
  string scriptTxt = string.Empty;
  using (StreamReader sr = new StreamReader(scriptStrm))
  {
      scriptTxt = sr.ReadToEnd();
  }

  var jobName = "SR_Wikipedia";
  var jobId = Guid.NewGuid();
  var properties = new USqlJobProperties(scriptTxt);
  var parameters = new JobInformation(jobName, JobType.USql, properties, priority: 1, degreeOfParallelism: 1, jobId: jobId);
  var jobInfo = adlaJobClient.Job.Create(adla, jobId, parameters);
  Console.WriteLine($"Job {jobName} submitted.");

}
```

### <a name="list-failed-jobs"></a><span data-ttu-id="cbc5e-176">列出失敗的作業</span><span class="sxs-lookup"><span data-stu-id="cbc5e-176">List failed jobs</span></span>
<span data-ttu-id="cbc5e-177">hello 下列程式碼列出作業失敗的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-177">hello following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="cbc5e-178">列出管線</span><span class="sxs-lookup"><span data-stu-id="cbc5e-178">List pipelines</span></span>
<span data-ttu-id="cbc5e-179">hello 下列程式碼列出每個管線的工作提交的 toohello 帳戶的資訊。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-179">hello following code lists information about each pipeline of jobs submitted toohello account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="cbc5e-180">列出週期</span><span class="sxs-lookup"><span data-stu-id="cbc5e-180">List recurrences</span></span>
<span data-ttu-id="cbc5e-181">hello 下列程式碼會列出每個循環中的工作提交的 toohello 帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-181">hello following code lists information about each recurrence of jobs submitted toohello account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="cbc5e-182">常見的圖形案例</span><span class="sxs-lookup"><span data-stu-id="cbc5e-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-hello-aad-directory"></a><span data-ttu-id="cbc5e-183">查閱 hello AAD 目錄中的使用者</span><span class="sxs-lookup"><span data-stu-id="cbc5e-183">Look up user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a><span data-ttu-id="cbc5e-184">Hello AAD 目錄中取得使用者的 ObjectId hello</span><span class="sxs-lookup"><span data-stu-id="cbc5e-184">Get hello ObjectId of a user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="cbc5e-185">管理計算原則</span><span class="sxs-lookup"><span data-stu-id="cbc5e-185">Manage compute policies</span></span>
<span data-ttu-id="cbc5e-186">hello DataLakeAnalyticsAccountManagementClient 物件提供用來管理 hello 方法計算的資料湖分析帳戶原則。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-186">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="cbc5e-187">列出計算原則</span><span class="sxs-lookup"><span data-stu-id="cbc5e-187">List compute policies</span></span>
<span data-ttu-id="cbc5e-188">下列程式碼的 hello 擷取 Data Lake Analytics 帳戶的計算原則的清單。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-188">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="cbc5e-189">建立新的計算原則</span><span class="sxs-lookup"><span data-stu-id="cbc5e-189">Create a new compute policy</span></span>
<span data-ttu-id="cbc5e-190">下列程式碼的 hello 建立 Data Lake Analytics 帳戶的新計算原則，設定 hello 最大澳洲可用 toohello 指定使用者 too50 和 hello 最小的工作優先權 too250。</span><span class="sxs-lookup"><span data-stu-id="cbc5e-190">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="cbc5e-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbc5e-191">Next steps</span></span>
* [<span data-ttu-id="cbc5e-192">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="cbc5e-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="cbc5e-193">使用 Azure 入口網站管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cbc5e-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="cbc5e-194">使用 Azure 入口網站監視和疑難排解 Azure Data Lake Analytics 作業</span><span class="sxs-lookup"><span data-stu-id="cbc5e-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
