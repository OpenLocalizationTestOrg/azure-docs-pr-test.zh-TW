---
title: "使用 Node.js 的 Azure SDK 開始使用 Azure Data Lake Store | Microsoft Docs"
description: "了解如何利用 Node.js 來與 Data Lake Store 帳戶及檔案系統搭配使用。"
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
ms.openlocfilehash: 8c7a2e6ca061bbfa077592efb73d592906c3d070
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="1c44b-103">使用 Node.js 的 Azure SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1c44b-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c44b-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="1c44b-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="1c44b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c44b-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="1c44b-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="1c44b-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="1c44b-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="1c44b-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="1c44b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="1c44b-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="1c44b-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1c44b-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="1c44b-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="1c44b-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="1c44b-111">Python</span><span class="sxs-lookup"><span data-stu-id="1c44b-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="1c44b-112">若要上傳和下載大量資料 (大型檔案、大量檔案或兩者)，建議您使用 [Python SDK](data-lake-store-get-started-python.md)、[.NET SDK](data-lake-store-get-started-net-sdk.md)、[Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md) 或 [Azure PowerShell](data-lake-store-get-started-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="1c44b-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="1c44b-113">這些選項擁有較佳的效能，因為它們會使用多個執行緒平行處理資料移動。</span><span class="sxs-lookup"><span data-stu-id="1c44b-113">These options have better performance as they use multiple threads to parallelize the data movement.</span></span>
> 
> 

<span data-ttu-id="1c44b-114">了解如何使用 Node.js 的 Azure SDK 建立 Azure Data Lake Store 帳戶並執行基本作業，例如建立資料夾、上傳和下載資料檔案、刪除您的帳戶等等。如需有關 Data Lake Store 的詳細資訊，請參閱 [Data Lake Store 概觀](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1c44b-114">Learn how to use the Azure SDK for Node.js to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="1c44b-115">SDK 目前支援</span><span class="sxs-lookup"><span data-stu-id="1c44b-115">Currently, the SDK supports</span></span>

* <span data-ttu-id="1c44b-116">**Node.js 版本：0.10.0 或更高版本**</span><span class="sxs-lookup"><span data-stu-id="1c44b-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="1c44b-117">**帳戶的 REST API 版本：2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="1c44b-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="1c44b-118">**檔案系統的 REST API 版本：2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="1c44b-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c44b-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="1c44b-119">Prerequisites</span></span>
<span data-ttu-id="1c44b-120">開始閱讀本文之前，您必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="1c44b-120">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="1c44b-121">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="1c44b-121">**An Azure subscription**.</span></span> <span data-ttu-id="1c44b-122">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1c44b-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1c44b-123">**建立 Azure Active Directory 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1c44b-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="1c44b-124">您必須使用 Azure AD 應用程式來向 Azure AD 驗證 Data Lake Store 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c44b-124">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="1c44b-125">有不同的方法可向 Azure AD 進行驗證：**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="1c44b-125">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="1c44b-126">如需有關如何驗證的指示和詳細資訊，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="1c44b-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-to-install"></a><span data-ttu-id="1c44b-127">如何安裝</span><span class="sxs-lookup"><span data-stu-id="1c44b-127">How to Install</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="1c44b-128">使用 Azure Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="1c44b-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="1c44b-129">下列程式碼片段顯示兩個不同的方式來利用 Azure AD 驗證 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="1c44b-129">The snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="1c44b-130">如需驗證 Data Lake Store 各種方法的詳細討論，請參閱[使用 Azure Active Directory 驗證 Data Lake Store](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="1c44b-130">For a detailed discussion on various methods to use for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="1c44b-131">下列程式碼片段也需要類似 Azure AD 網域名稱、Azure AD 應用程式的用戶端 ID 等等的輸入。所有這些詳細資料都可從您必須建立的 Azure AD 應用程式擷取，這些詳細資料也包含在上面的連結中。</span><span class="sxs-lookup"><span data-stu-id="1c44b-131">The snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, the details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-store-clients"></a><span data-ttu-id="1c44b-132">建立 Data Lake Store 用戶端</span><span class="sxs-lookup"><span data-stu-id="1c44b-132">Create the Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="1c44b-133">建立 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="1c44b-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object to create
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
    /*err has reference to the actual request and response, so you can see what was sent and received on the wire.
      The structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'The response body if any',
        request: reference to a stripped version of http request
        response: reference to a stripped version of the response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="1c44b-134">建立具有內容的檔案</span><span class="sxs-lookup"><span data-stu-id="1c44b-134">Create a file with content</span></span>
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

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="1c44b-135">取得檔案和資料夾的清單</span><span class="sxs-lookup"><span data-stu-id="1c44b-135">Get a list of files and folders</span></span>
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

## <a name="see-also"></a><span data-ttu-id="1c44b-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1c44b-136">See also</span></span>
* [<span data-ttu-id="1c44b-137">Microsoft Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="1c44b-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="1c44b-138">Microsoft Azure SDK for Node.js - Data Lake Analytics 管理</span><span class="sxs-lookup"><span data-stu-id="1c44b-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

