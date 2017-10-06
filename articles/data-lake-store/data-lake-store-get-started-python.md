---
title: "開始使用 Azure Data Lake Store 的 aaaUse hello Python SDK tooget |Microsoft 文件"
description: "了解如何使用 Data Lake Store 帳戶和 hello toouse Python SDK toowork 檔案系統。"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a>透過 Python 開始使用 Azure Data Lake Store

> [!div class="op_single_selector"]
> * [入口網站](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

了解如何 toouse hello Azure 的 Python SDK 和 Azure Data Lake Store tooperform 基本作業，例如建立資料夾、 上傳和下載資料檔等。如需有關 Data Lake 的詳細資訊，請參閱 [Azure Data Lake Store](data-lake-store-overview.md)。

## <a name="prerequisites"></a>必要條件

* **Python**。 您可以從[這裡](https://www.python.org/downloads/)下載 Python。 本文章使用 Python 3.5.2。

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

* **建立 Azure Active Directory 應用程式**。 您可以使用 hello Azure AD 應用程式 tooauthenticate hello Data Lake Store 應用程式與 Azure AD。 有不同的方法 tooauthenticate 與 Azure AD，這是**使用者驗證**或**服務對服務驗證**。 如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。

## <a name="install-hello-modules"></a>安裝 hello 模組

toowork 與資料湖存放區使用 Python，您需要 tooinstall 三個模組。

* hello`azure-mgmt-resource`模組。 這包括適用於 Active Directory 等等的 Azure 模組。
* hello`azure-mgmt-datalake-store`模組。 這包括 hello Azure Data Lake Store 帳戶的管理作業。 如需關於此模組的詳細資訊，請參閱 [Azure Data Lake Store Management module reference (Azure Data Lake Store 管理模組參考)](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html)。
* hello`azure-datalake-store`模組。 這包括 hello Azure Data Lake Store 檔案系統作業。 如需關於此模組的詳細資訊，請參閱 [Azure Data Lake Store Filesystem module reference (Azure Data Lake Store 檔案系統模組參考)](http://azure-datalake-store.readthedocs.io/en/latest/)。

使用下列命令 tooinstall hello 模組 hello。

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>建立新的 Python 應用程式

1. Hello 您選擇的 IDE 中建立新的 Python 應用程式，例如**mysample.py**。

2. 新增下列幾行 tooimport hello 所需模組的 hello

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. 儲存變更 toomysample.py。

## <a name="authentication"></a>驗證

在本節中，我們討論 hello 不同的方式 tooauthenticate 與 Azure AD。 hello 選項如下：

* 使用者驗證
* 服務對服務驗證
* Multi-Factor Authentication

您必須對帳戶管理和檔案系統管理模組使用這些驗證選項。

### <a name="end-user-authentication-for-account-management"></a>適用於帳戶管理的使用者驗證

使用此 tooauthenticate 和 Azure AD 的帳戶管理操作 （建立/刪除 Data Lake Store 帳戶等。）。 您必須提供 Azure AD 使用者的使用者名稱和密碼。 請注意該 hello 使用者不應該設定多重要素驗證。

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a>檔案系統作業的使用者驗證

使用此 tooauthenticate 和 Azure AD （建立資料夾、 上傳的檔案等） 的檔案系統作業。 請將此方法用於現有的 Azure AD「原生用戶端」應用程式。 您提供認證的 hello Azure AD 使用者不應該設定多重要素驗證。

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a>適用於帳戶管理的用戶端密碼服務對服務驗證

使用此 tooauthenticate 和 Azure AD 的帳戶管理操作 （建立/刪除 Data Lake Store 帳戶等。）。 下列程式碼片段 hello 可以是使用的 tooauthenticate 您的應用程式非互動方式，應用程式 / 服務主體使用 hello 用戶端密碼。 請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a>適用於檔案系統作業的用戶端密碼服務對服務驗證

使用此 tooauthenticate 和 Azure AD （建立資料夾、 上傳的檔案等） 的檔案系統作業。 下列程式碼片段 hello 可以是使用的 tooauthenticate 您的應用程式非互動方式，應用程式 / 服務主體使用 hello 用戶端密碼。 請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a>適用於帳戶管理的 Multi-Factor Authentication

使用此 tooauthenticate 和 Azure AD 的帳戶管理操作 （建立/刪除 Data Lake Store 帳戶等。）。 hello 下列程式碼片段可以是使用 tooauthenticate 使用多因素驗證應用程式。 請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a>適用於檔案系統管理的 Multi-Factor Authentication

使用此 tooauthenticate 和 Azure AD （建立資料夾、 上傳的檔案等） 的檔案系統作業。 hello 下列程式碼片段可以是使用 tooauthenticate 使用多因素驗證應用程式。 請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a>建立 Azure 資源群組

使用下列程式碼片段 toocreate Azure 資源群組的 hello:

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a>建立用戶端與 Data Lake Store 帳戶

下列程式碼片段的第一次的 hello 建立 hello Data Lake Store 帳戶用戶端。 它會使用 hello 用戶端物件 toocreate Data Lake Store 帳戶。 最後，hello 片段會建立檔案系統的用戶端物件。

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-hello-data-lake-store-accounts"></a>列出 hello Data Lake Store 帳戶

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a>建立目錄

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>上傳檔案


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>下載檔案

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>刪除目錄

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a>另請參閱

- [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
- [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [搭配 Data Lake Store 使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)
- [Data Lake Store .NET SDK 參考](https://msdn.microsoft.com/library/mt581387.aspx)
- [Data Lake Store REST 參考](https://msdn.microsoft.com/library/mt693424.aspx)
