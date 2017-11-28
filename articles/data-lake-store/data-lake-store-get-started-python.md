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
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="576a3-103">透過 Python 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="576a3-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="576a3-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="576a3-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="576a3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="576a3-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="576a3-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="576a3-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="576a3-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="576a3-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="576a3-108">REST API</span><span class="sxs-lookup"><span data-stu-id="576a3-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="576a3-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="576a3-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="576a3-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="576a3-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="576a3-111">Python</span><span class="sxs-lookup"><span data-stu-id="576a3-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="576a3-112">了解如何 toouse hello Azure 的 Python SDK 和 Azure Data Lake Store tooperform 基本作業，例如建立資料夾、 上傳和下載資料檔等。如需有關 Data Lake 的詳細資訊，請參閱 [Azure Data Lake Store](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="576a3-112">Learn how toouse hello Python SDK for Azure and Azure Data Lake Store tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="576a3-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="576a3-113">Prerequisites</span></span>

* <span data-ttu-id="576a3-114">**Python**。</span><span class="sxs-lookup"><span data-stu-id="576a3-114">**Python**.</span></span> <span data-ttu-id="576a3-115">您可以從[這裡](https://www.python.org/downloads/)下載 Python。</span><span class="sxs-lookup"><span data-stu-id="576a3-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="576a3-116">本文章使用 Python 3.5.2。</span><span class="sxs-lookup"><span data-stu-id="576a3-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="576a3-117">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="576a3-117">**An Azure subscription**.</span></span> <span data-ttu-id="576a3-118">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="576a3-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="576a3-119">**建立 Azure Active Directory 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="576a3-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="576a3-120">您可以使用 hello Azure AD 應用程式 tooauthenticate hello Data Lake Store 應用程式與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="576a3-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="576a3-121">有不同的方法 tooauthenticate 與 Azure AD，這是**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="576a3-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="576a3-122">如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="576a3-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-hello-modules"></a><span data-ttu-id="576a3-123">安裝 hello 模組</span><span class="sxs-lookup"><span data-stu-id="576a3-123">Install hello modules</span></span>

<span data-ttu-id="576a3-124">toowork 與資料湖存放區使用 Python，您需要 tooinstall 三個模組。</span><span class="sxs-lookup"><span data-stu-id="576a3-124">toowork with Data Lake Store using Python, you need tooinstall three modules.</span></span>

* <span data-ttu-id="576a3-125">hello`azure-mgmt-resource`模組。</span><span class="sxs-lookup"><span data-stu-id="576a3-125">hello `azure-mgmt-resource` module.</span></span> <span data-ttu-id="576a3-126">這包括適用於 Active Directory 等等的 Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="576a3-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="576a3-127">hello`azure-mgmt-datalake-store`模組。</span><span class="sxs-lookup"><span data-stu-id="576a3-127">hello `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="576a3-128">這包括 hello Azure Data Lake Store 帳戶的管理作業。</span><span class="sxs-lookup"><span data-stu-id="576a3-128">This includes hello Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="576a3-129">如需關於此模組的詳細資訊，請參閱 [Azure Data Lake Store Management module reference (Azure Data Lake Store 管理模組參考)](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html)。</span><span class="sxs-lookup"><span data-stu-id="576a3-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="576a3-130">hello`azure-datalake-store`模組。</span><span class="sxs-lookup"><span data-stu-id="576a3-130">hello `azure-datalake-store` module.</span></span> <span data-ttu-id="576a3-131">這包括 hello Azure Data Lake Store 檔案系統作業。</span><span class="sxs-lookup"><span data-stu-id="576a3-131">This includes hello Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="576a3-132">如需關於此模組的詳細資訊，請參閱 [Azure Data Lake Store Filesystem module reference (Azure Data Lake Store 檔案系統模組參考)](http://azure-datalake-store.readthedocs.io/en/latest/)。</span><span class="sxs-lookup"><span data-stu-id="576a3-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="576a3-133">使用下列命令 tooinstall hello 模組 hello。</span><span class="sxs-lookup"><span data-stu-id="576a3-133">Use hello following commands tooinstall hello modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="576a3-134">建立新的 Python 應用程式</span><span class="sxs-lookup"><span data-stu-id="576a3-134">Create a new Python application</span></span>

1. <span data-ttu-id="576a3-135">Hello 您選擇的 IDE 中建立新的 Python 應用程式，例如**mysample.py**。</span><span class="sxs-lookup"><span data-stu-id="576a3-135">In hello IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="576a3-136">新增下列幾行 tooimport hello 所需模組的 hello</span><span class="sxs-lookup"><span data-stu-id="576a3-136">Add hello following lines tooimport hello required modules</span></span>

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

3. <span data-ttu-id="576a3-137">儲存變更 toomysample.py。</span><span class="sxs-lookup"><span data-stu-id="576a3-137">Save changes toomysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="576a3-138">驗證</span><span class="sxs-lookup"><span data-stu-id="576a3-138">Authentication</span></span>

<span data-ttu-id="576a3-139">在本節中，我們討論 hello 不同的方式 tooauthenticate 與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="576a3-139">In this section, we talk about hello different ways tooauthenticate with Azure AD.</span></span> <span data-ttu-id="576a3-140">hello 選項如下：</span><span class="sxs-lookup"><span data-stu-id="576a3-140">hello options available are:</span></span>

* <span data-ttu-id="576a3-141">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="576a3-141">End-user authentication</span></span>
* <span data-ttu-id="576a3-142">服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="576a3-142">Service-to-service authentication</span></span>
* <span data-ttu-id="576a3-143">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="576a3-143">Multi-factor authentication</span></span>

<span data-ttu-id="576a3-144">您必須對帳戶管理和檔案系統管理模組使用這些驗證選項。</span><span class="sxs-lookup"><span data-stu-id="576a3-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="576a3-145">適用於帳戶管理的使用者驗證</span><span class="sxs-lookup"><span data-stu-id="576a3-145">End-user authentication for account management</span></span>

<span data-ttu-id="576a3-146">使用此 tooauthenticate 和 Azure AD 的帳戶管理操作 （建立/刪除 Data Lake Store 帳戶等。）。</span><span class="sxs-lookup"><span data-stu-id="576a3-146">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="576a3-147">您必須提供 Azure AD 使用者的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="576a3-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="576a3-148">請注意該 hello 使用者不應該設定多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="576a3-148">Note that hello user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="576a3-149">檔案系統作業的使用者驗證</span><span class="sxs-lookup"><span data-stu-id="576a3-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="576a3-150">使用此 tooauthenticate 和 Azure AD （建立資料夾、 上傳的檔案等） 的檔案系統作業。</span><span class="sxs-lookup"><span data-stu-id="576a3-150">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="576a3-151">請將此方法用於現有的 Azure AD「原生用戶端」應用程式。</span><span class="sxs-lookup"><span data-stu-id="576a3-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="576a3-152">您提供認證的 hello Azure AD 使用者不應該設定多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="576a3-152">hello Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="576a3-153">適用於帳戶管理的用戶端密碼服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="576a3-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="576a3-154">使用此 tooauthenticate 和 Azure AD 的帳戶管理操作 （建立/刪除 Data Lake Store 帳戶等。）。</span><span class="sxs-lookup"><span data-stu-id="576a3-154">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="576a3-155">下列程式碼片段 hello 可以是使用的 tooauthenticate 您的應用程式非互動方式，應用程式 / 服務主體使用 hello 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="576a3-155">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="576a3-156">請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。</span><span class="sxs-lookup"><span data-stu-id="576a3-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="576a3-157">適用於檔案系統作業的用戶端密碼服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="576a3-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="576a3-158">使用此 tooauthenticate 和 Azure AD （建立資料夾、 上傳的檔案等） 的檔案系統作業。</span><span class="sxs-lookup"><span data-stu-id="576a3-158">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="576a3-159">下列程式碼片段 hello 可以是使用的 tooauthenticate 您的應用程式非互動方式，應用程式 / 服務主體使用 hello 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="576a3-159">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="576a3-160">請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。</span><span class="sxs-lookup"><span data-stu-id="576a3-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="576a3-161">適用於帳戶管理的 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="576a3-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="576a3-162">使用此 tooauthenticate 和 Azure AD 的帳戶管理操作 （建立/刪除 Data Lake Store 帳戶等。）。</span><span class="sxs-lookup"><span data-stu-id="576a3-162">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="576a3-163">hello 下列程式碼片段可以是使用 tooauthenticate 使用多因素驗證應用程式。</span><span class="sxs-lookup"><span data-stu-id="576a3-163">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="576a3-164">請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。</span><span class="sxs-lookup"><span data-stu-id="576a3-164">Use this with an existing Azure AD "Web App" application.</span></span>

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

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="576a3-165">適用於檔案系統管理的 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="576a3-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="576a3-166">使用此 tooauthenticate 和 Azure AD （建立資料夾、 上傳的檔案等） 的檔案系統作業。</span><span class="sxs-lookup"><span data-stu-id="576a3-166">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="576a3-167">hello 下列程式碼片段可以是使用 tooauthenticate 使用多因素驗證應用程式。</span><span class="sxs-lookup"><span data-stu-id="576a3-167">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="576a3-168">請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。</span><span class="sxs-lookup"><span data-stu-id="576a3-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="576a3-169">建立 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="576a3-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="576a3-170">使用下列程式碼片段 toocreate Azure 資源群組的 hello:</span><span class="sxs-lookup"><span data-stu-id="576a3-170">Use hello following code snippet toocreate an Azure Resource Group:</span></span>

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

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="576a3-171">建立用戶端與 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="576a3-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="576a3-172">下列程式碼片段的第一次的 hello 建立 hello Data Lake Store 帳戶用戶端。</span><span class="sxs-lookup"><span data-stu-id="576a3-172">hello following snippet first creates hello Data Lake Store account client.</span></span> <span data-ttu-id="576a3-173">它會使用 hello 用戶端物件 toocreate Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="576a3-173">It uses hello client object toocreate a Data Lake Store account.</span></span> <span data-ttu-id="576a3-174">最後，hello 片段會建立檔案系統的用戶端物件。</span><span class="sxs-lookup"><span data-stu-id="576a3-174">Finally, hello snippet creates a filesystem client object.</span></span>

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

## <a name="list-hello-data-lake-store-accounts"></a><span data-ttu-id="576a3-175">列出 hello Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="576a3-175">List hello Data Lake Store accounts</span></span>

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="576a3-176">建立目錄</span><span class="sxs-lookup"><span data-stu-id="576a3-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="576a3-177">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="576a3-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="576a3-178">下載檔案</span><span class="sxs-lookup"><span data-stu-id="576a3-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="576a3-179">刪除目錄</span><span class="sxs-lookup"><span data-stu-id="576a3-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="576a3-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="576a3-180">See also</span></span>

- [<span data-ttu-id="576a3-181">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="576a3-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="576a3-182">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="576a3-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="576a3-183">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="576a3-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="576a3-184">Data Lake Store .NET SDK 參考</span><span class="sxs-lookup"><span data-stu-id="576a3-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="576a3-185">Data Lake Store REST 參考</span><span class="sxs-lookup"><span data-stu-id="576a3-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
