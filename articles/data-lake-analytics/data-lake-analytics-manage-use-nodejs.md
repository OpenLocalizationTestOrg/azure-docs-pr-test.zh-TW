---
title: "使用 Azure SDK for Node.js 的 Azure Data Lake Analytics aaaManage |Microsoft 文件"
description: "了解如何 toomanage Data Lake Analytics 帳戶，資料來源、 工作和使用者使用 Azure SDK for Node.js"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 9de1bcf4-b15b-4d0b-9284-8889ecf0c438
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 07acd058bf252af2fc98c4cfe87a135e0b79900f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a>使用 Node.js 的 Azure SDK 管理 Azure 資料湖分析
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

hello Azure SDK for Node.js 可以用來管理 Azure Data Lake Analytics 帳戶、 工作和類別目錄中。 toosee 管理主題使用其他工具中，按一下 [hello] 索引標籤選取上述。

它目前支援︰

* **Node.js 版本：0.10.0 或更高版本**
* **帳戶的 REST API 版本：2015-10-01-preview**
* **目錄的 REST API 版本：2015-10-01-preview**
* **作業的 REST API 版本：2016-03-20-preview**

## <a name="features"></a>特性
* 帳戶管理：建立、取得、列出、更新及刪除。
* 作業管理︰提交、取得、列出及取消。
* 目錄管理：取得及列出。

## <a name="how-tooinstall"></a>如何 tooInstall
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a>使用 Azure Active Directory 進行驗證
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-analytics-client"></a>建立 hello Data Lake Analytics 用戶端
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a>建立 Data Lake Analytics 帳戶
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlaacct';
var location = 'eastus2';

// A Data Lake Store account must already have been created toocreate
// a Data Lake Analytics account. See hello Data Lake Store readme for
// information on doing so. For now, we assume one exists already.
var datalakeStoreAccountName = 'existingadlsaccount';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location,
  properties: {
    defaultDataLakeStoreAccount: datalakeStoreAccountName,
    dataLakeStoreAccounts: [
      {
        name: datalakeStoreAccountName
      }
    ]
  }
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

## <a name="get-a-list-of-jobs"></a>取得作業清單
```javascript
var util = require('util');
var accountName = 'testadlaacct';
jobClient.job.list(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="get-a-list-of-databases-in-hello-data-lake-analytics-catalog"></a>取得 hello 資料湖分析目錄中的資料庫清單
```javascript
var util = require('util');
var accountName = 'testadlaacct';
catalogClient.catalog.listDatabases(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a>另請參閱
* [Microsoft Azure SDK for Node.js](https://github.com/azure/azure-sdk-for-node)
* [Microsoft Azure SDK for Node.js - Data Lake Store 管理](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

