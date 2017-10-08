---
title: "開始使用 Azure SDK for Node.js 的 Azure Data Lake Store aaaGet |Microsoft 文件"
description: "了解如何使用 Data Lake Store 帳戶和 hello toouse Node.js toowork 檔案系統。"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="a34a7-103">使用 Node.js 的 Azure SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a34a7-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a34a7-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="a34a7-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="a34a7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a34a7-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="a34a7-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="a34a7-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="a34a7-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="a34a7-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="a34a7-108">REST API</span><span class="sxs-lookup"><span data-stu-id="a34a7-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="a34a7-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a34a7-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="a34a7-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="a34a7-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="a34a7-111">Python</span><span class="sxs-lookup"><span data-stu-id="a34a7-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="a34a7-112">上傳和下載大量的資料 （大型檔案，大量的檔案，或兩者），我們建議您使用 hello [Python SDK](data-lake-store-get-started-python.md)，hello [.NET SDK](data-lake-store-get-started-net-sdk.md)， [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)，或[Azure PowerShell](data-lake-store-get-started-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="a34a7-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="a34a7-113">這些選項會有較佳的效能，因為它們使用多個執行緒 tooparallelize hello 資料移動。</span><span class="sxs-lookup"><span data-stu-id="a34a7-113">These options have better performance as they use multiple threads tooparallelize hello data movement.</span></span>
> 
> 

<span data-ttu-id="a34a7-114">了解如何 toouse hello Azure SDK for Node.js toocreate Azure Data Lake Store 帳戶和執行基本作業，例如建立資料夾、 上傳和下載資料檔，刪除您的帳戶，依此類推。如需有關 Data Lake Store 的詳細資訊，請參閱 [Data Lake Store 概觀](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a34a7-114">Learn how toouse hello Azure SDK for Node.js toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="a34a7-115">目前，hello SDK 支援</span><span class="sxs-lookup"><span data-stu-id="a34a7-115">Currently, hello SDK supports</span></span>

* <span data-ttu-id="a34a7-116">**Node.js 版本：0.10.0 或更高版本**</span><span class="sxs-lookup"><span data-stu-id="a34a7-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="a34a7-117">**帳戶的 REST API 版本：2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="a34a7-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="a34a7-118">**檔案系統的 REST API 版本：2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="a34a7-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a34a7-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="a34a7-119">Prerequisites</span></span>
<span data-ttu-id="a34a7-120">在開始這份文件之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="a34a7-120">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="a34a7-121">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a34a7-121">**An Azure subscription**.</span></span> <span data-ttu-id="a34a7-122">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a34a7-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a34a7-123">**建立 Azure Active Directory 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a34a7-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="a34a7-124">您可以使用 hello Azure AD 應用程式 tooauthenticate hello Data Lake Store 應用程式與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="a34a7-124">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="a34a7-125">有不同的方法 tooauthenticate 與 Azure AD，這是**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="a34a7-125">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="a34a7-126">如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="a34a7-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="a34a7-127">如何 tooInstall</span><span class="sxs-lookup"><span data-stu-id="a34a7-127">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="a34a7-128">使用 Azure Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="a34a7-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="a34a7-129">下列的 hello 片段將示範使用 Azure AD 驗證與資料湖存放區的兩個不同的方式。</span><span class="sxs-lookup"><span data-stu-id="a34a7-129">hello snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="a34a7-130">驗證的資料湖存放區的各種方法 toouse 的詳細討論，請參閱[驗證資料湖存放區使用 Azure Active Directory](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="a34a7-130">For a detailed discussion on various methods toouse for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="a34a7-131">hello 以下程式碼片段也需要與 Azure AD 網域名稱，Azure AD 應用程式等的用戶端識別碼的輸入。所有這些詳細資料可從擷取的 Azure AD 應用程式，您必須建立 hello 詳細資料，其中也會包含在上面的連結。</span><span class="sxs-lookup"><span data-stu-id="a34a7-131">hello snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, hello details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a><span data-ttu-id="a34a7-132">建立 hello 資料湖存放區的用戶端</span><span class="sxs-lookup"><span data-stu-id="a34a7-132">Create hello Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="a34a7-133">建立 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="a34a7-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="a34a7-134">建立具有內容的檔案</span><span class="sxs-lookup"><span data-stu-id="a34a7-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="a34a7-135">取得檔案和資料夾的清單</span><span class="sxs-lookup"><span data-stu-id="a34a7-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="a34a7-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a34a7-136">See also</span></span>
* [<span data-ttu-id="a34a7-137">Microsoft Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="a34a7-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="a34a7-138">Microsoft Azure SDK for Node.js - Data Lake Analytics 管理</span><span class="sxs-lookup"><span data-stu-id="a34a7-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

