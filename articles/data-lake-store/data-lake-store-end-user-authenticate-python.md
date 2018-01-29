---
title: "使用者驗證︰使用 Python 利用 Azure Active Directory 向 Data Lake Store 進行 | Microsoft Docs"
description: "了解如何使用 Python，利用 Azure Active Directory 向 Data Lake Store 完成使用者驗證"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/09/2018
ms.author: nitinme
ms.openlocfilehash: 1fa8df760ac22ae915765895b498f21d628eea76
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2018
---
# <a name="end-user-authentication-with-data-lake-store-using-python"></a>使用 Python 向 Data Lake Store 進行使用者驗證
> [!div class="op_single_selector"]
> * [使用 Java](data-lake-store-end-user-authenticate-java-sdk.md)
> * [使用 .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md)
> * [使用 Python](data-lake-store-end-user-authenticate-python.md)
> * [使用 REST API](data-lake-store-end-user-authenticate-rest-api.md)
> 
> 

在本文中，您會了解如何使用 Python SDK 向 Azure Data Lake Store 進行使用者驗證。 使用者驗證可以進一步分成兩個類別：

* 沒有多重要素驗證的使用者驗證
* 有多重要素驗證的使用者驗證

本文中討論這兩個選項。 如需使用 Python 向 Data Lake Store 進行服務對服務驗證，請參閱[使用 Python 向 Data Lake Store 進行服務對服務驗證](data-lake-store-service-to-service-authenticate-python.md)。

## <a name="prerequisites"></a>必要條件

* **Python**。 您可以從[這裡](https://www.python.org/downloads/)下載 Python。 本文使用 Python 3.6.2。

* **Azure 訂用帳戶**。 請參閱[取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

* **建立 Active Directory 「原生」應用程式**。 您必須已經完成[使用 Azure Active Directory 向 Data Lake Store 進行使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)中的步驟。

## <a name="install-the-modules"></a>安裝模組

若要透過 Python 使用 Data Lake Store，您需要安裝三個模組。

* `azure-mgmt-resource` 模組，這包括適用於 Active Directory 等等的 Azure 模組。
* `azure-mgmt-datalake-store` 模組，這包括 Azure Data Lake Store 帳戶管理作業。 如需關於此模組的詳細資訊，請參閱 [Azure Data Lake Store Management module reference (Azure Data Lake Store 管理模組參考)](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html)。
* `azure-datalake-store` 模組，這包括 Azure Data Lake Store 檔案系統作業。 如需關於此模組的詳細資訊，請參閱 [Azure Data Lake Store Filesystem module reference (Azure Data Lake Store 檔案系統模組參考)](http://azure-datalake-store.readthedocs.io/en/latest/)。

使用下列命令來安裝新模組。

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>建立新的 Python 應用程式

1. 在您選定的整合式開發環境 (IDE) 中建立新的 Python 應用程式，例如 **mysample.py**。

2. 新增以下程式碼片段以匯入必要模組

    ```
    ## Use this for Azure AD authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    import adal
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, pprint, uuid, time
    ```

3. 將變更儲存至 mysample.py。

## <a name="end-user-authentication-with-multi-factor-authentication"></a>有多重要素驗證的使用者驗證

### <a name="for-account-management"></a>對於帳戶管理

使用下列程式碼片段向 Azure AD 驗證，以便對 Data Lake Store 帳戶進行帳戶管理作業。 下列程式碼片段可供使用 Multi-Factor Authentication 來驗證您的應用程式。 對現有的 Azure AD **原生**應用程式提供下列值。

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
    armCreds = AADTokenCredentials(mgmt_token, client_id, resource = RESOURCE)

### <a name="for-filesystem-operations"></a>對於檔案系統作業

使用這個指令向 Azure AD 驗證，以便對 Data Lake Store 進行檔案系統作業。 下列程式碼片段可供使用 Multi-Factor Authentication 來驗證您的應用程式。 對現有的 Azure AD **原生**應用程式提供下列值。

    adlCreds = lib.auth(tenant_id='FILL-IN-HERE', resource = 'https://datalake.azure.net/')

## <a name="end-user-authentication-without-multi-factor-authentication"></a>沒有多重要素驗證的使用者驗證

這已被取代。 如需詳細資訊，請參閱[使用 Python SDK 進行 Azure 驗證](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate?view=azure-python#mgmt-auth-token)。
   
## <a name="next-steps"></a>後續步驟
在本文中，您已了解如何使用 Python，使用使用者驗證向 Azure Data Lake Store 進行驗證。 您現在可以看看下列文章，了解如何使用 Python 與 Azure Data Lake Store 搭配。

* [使用 Python 對 Data Lake Store 進行帳戶管理作業](data-lake-store-get-started-python.md)
* [使用 Python 對 Data Lake Store 進行資料作業](data-lake-store-data-operations-python.md)

