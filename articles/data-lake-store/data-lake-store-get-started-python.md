---
title: "透過 Python SDK 開始使用 Azure Data Lake Store | Microsoft Docs"
description: "了解如何利用 Python SDK 來與 Data Lake Store 帳戶及檔案系統搭配使用。"
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
ms.openlocfilehash: 375a603360ac249fc1b08923a94c85652390a3fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="f46ff-103">透過 Python 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f46ff-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f46ff-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="f46ff-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="f46ff-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f46ff-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="f46ff-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="f46ff-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="f46ff-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="f46ff-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="f46ff-108">REST API</span><span class="sxs-lookup"><span data-stu-id="f46ff-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="f46ff-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f46ff-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="f46ff-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="f46ff-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="f46ff-111">Python</span><span class="sxs-lookup"><span data-stu-id="f46ff-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="f46ff-112">了解如何使用適用於 Azure 和 Azure Data Lake Store 的 Python SDK 來執行基本作業，例如建立資料夾、上傳和下載資料檔案等等。如需有關 Data Lake 的詳細資訊，請參閱 [Azure Data Lake Store](data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-112">Learn how to use the Python SDK for Azure and Azure Data Lake Store to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f46ff-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="f46ff-113">Prerequisites</span></span>

* <span data-ttu-id="f46ff-114">**Python**。</span><span class="sxs-lookup"><span data-stu-id="f46ff-114">**Python**.</span></span> <span data-ttu-id="f46ff-115">您可以從[這裡](https://www.python.org/downloads/)下載 Python。</span><span class="sxs-lookup"><span data-stu-id="f46ff-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="f46ff-116">本文章使用 Python 3.5.2。</span><span class="sxs-lookup"><span data-stu-id="f46ff-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="f46ff-117">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f46ff-117">**An Azure subscription**.</span></span> <span data-ttu-id="f46ff-118">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="f46ff-119">**建立 Azure Active Directory 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f46ff-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="f46ff-120">您必須使用 Azure AD 應用程式來向 Azure AD 驗證 Data Lake Store 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="f46ff-121">有不同的方法可向 Azure AD 進行驗證：**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="f46ff-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="f46ff-122">如需有關如何驗證的指示和詳細資訊，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="f46ff-123">安裝模組</span><span class="sxs-lookup"><span data-stu-id="f46ff-123">Install the modules</span></span>

<span data-ttu-id="f46ff-124">若要透過 Python 使用 Data Lake Store，您需要安裝三個模組。</span><span class="sxs-lookup"><span data-stu-id="f46ff-124">To work with Data Lake Store using Python, you need to install three modules.</span></span>

* <span data-ttu-id="f46ff-125">`azure-mgmt-resource` 模組。</span><span class="sxs-lookup"><span data-stu-id="f46ff-125">The `azure-mgmt-resource` module.</span></span> <span data-ttu-id="f46ff-126">這包括適用於 Active Directory 等等的 Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="f46ff-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="f46ff-127">`azure-mgmt-datalake-store` 模組。</span><span class="sxs-lookup"><span data-stu-id="f46ff-127">The `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="f46ff-128">這包括 Azure Data Lake Store 帳戶管理作業。</span><span class="sxs-lookup"><span data-stu-id="f46ff-128">This includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="f46ff-129">如需關於此模組的詳細資訊，請參閱 [Azure Data Lake Store Management module reference (Azure Data Lake Store 管理模組參考)](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="f46ff-130">`azure-datalake-store` 模組。</span><span class="sxs-lookup"><span data-stu-id="f46ff-130">The `azure-datalake-store` module.</span></span> <span data-ttu-id="f46ff-131">這包括 Azure Data Lake Store 檔案系統作業。</span><span class="sxs-lookup"><span data-stu-id="f46ff-131">This includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="f46ff-132">如需關於此模組的詳細資訊，請參閱 [Azure Data Lake Store Filesystem module reference (Azure Data Lake Store 檔案系統模組參考)](http://azure-datalake-store.readthedocs.io/en/latest/)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="f46ff-133">使用下列命令來安裝新模組。</span><span class="sxs-lookup"><span data-stu-id="f46ff-133">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="f46ff-134">建立新的 Python 應用程式</span><span class="sxs-lookup"><span data-stu-id="f46ff-134">Create a new Python application</span></span>

1. <span data-ttu-id="f46ff-135">在您選定的整合式開發環境 (IDE) 中建立新的 Python 應用程式，例如 **mysample.py**。</span><span class="sxs-lookup"><span data-stu-id="f46ff-135">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="f46ff-136">加入以下文字行以匯入必要模組</span><span class="sxs-lookup"><span data-stu-id="f46ff-136">Add the following lines to import the required modules</span></span>

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

3. <span data-ttu-id="f46ff-137">將變更儲存至 mysample.py。</span><span class="sxs-lookup"><span data-stu-id="f46ff-137">Save changes to mysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="f46ff-138">驗證</span><span class="sxs-lookup"><span data-stu-id="f46ff-138">Authentication</span></span>

<span data-ttu-id="f46ff-139">在本節中，我們會討論向 Azure AD 進行驗證的各種方式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-139">In this section, we talk about the different ways to authenticate with Azure AD.</span></span> <span data-ttu-id="f46ff-140">可用的選項如下︰</span><span class="sxs-lookup"><span data-stu-id="f46ff-140">The options available are:</span></span>

* <span data-ttu-id="f46ff-141">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="f46ff-141">End-user authentication</span></span>
* <span data-ttu-id="f46ff-142">服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="f46ff-142">Service-to-service authentication</span></span>
* <span data-ttu-id="f46ff-143">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f46ff-143">Multi-factor authentication</span></span>

<span data-ttu-id="f46ff-144">您必須對帳戶管理和檔案系統管理模組使用這些驗證選項。</span><span class="sxs-lookup"><span data-stu-id="f46ff-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="f46ff-145">適用於帳戶管理的使用者驗證</span><span class="sxs-lookup"><span data-stu-id="f46ff-145">End-user authentication for account management</span></span>

<span data-ttu-id="f46ff-146">使用這個方法來向 Azure AD 驗證，以便進行帳戶管理作業 (建立/刪除 Data Lake Store 帳戶等等)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-146">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="f46ff-147">您必須提供 Azure AD 使用者的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f46ff-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="f46ff-148">請注意，使用者不應設定使用多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="f46ff-148">Note that the user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="f46ff-149">檔案系統作業的使用者驗證</span><span class="sxs-lookup"><span data-stu-id="f46ff-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="f46ff-150">使用這個方法來向 Azure AD 驗證，以便進行檔案系統作業 (建立資料夾、上傳檔案等等)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-150">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="f46ff-151">請將此方法用於現有的 Azure AD「原生用戶端」應用程式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="f46ff-152">您提供認證的 Azure AD 使用者不應設定使用多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="f46ff-152">The Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="f46ff-153">適用於帳戶管理的用戶端密碼服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="f46ff-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="f46ff-154">使用這個方法來向 Azure AD 驗證，以便進行帳戶管理作業 (建立/刪除 Data Lake Store 帳戶等等)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-154">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="f46ff-155">下列程式碼片段可供使用應用程式/服務主體的用戶端密碼，以非互動方式驗證您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-155">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="f46ff-156">請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="f46ff-157">適用於檔案系統作業的用戶端密碼服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="f46ff-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="f46ff-158">使用這個方法來向 Azure AD 驗證，以便進行檔案系統作業 (建立資料夾、上傳檔案等等)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-158">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="f46ff-159">下列程式碼片段可供使用應用程式/服務主體的用戶端密碼，以非互動方式驗證您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-159">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="f46ff-160">請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="f46ff-161">適用於帳戶管理的 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f46ff-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="f46ff-162">使用這個方法來向 Azure AD 驗證，以便進行帳戶管理作業 (建立/刪除 Data Lake Store 帳戶等等)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-162">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="f46ff-163">下列程式碼片段可供使用 Multi-Factor Authentication 來驗證您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-163">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="f46ff-164">請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-164">Use this with an existing Azure AD "Web App" application.</span></span>

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

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="f46ff-165">適用於檔案系統管理的 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f46ff-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="f46ff-166">使用這個方法來向 Azure AD 驗證，以便進行檔案系統作業 (建立資料夾、上傳檔案等等)。</span><span class="sxs-lookup"><span data-stu-id="f46ff-166">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="f46ff-167">下列程式碼片段可供使用 Multi-Factor Authentication 來驗證您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-167">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="f46ff-168">請將此方法用於現有的 Azure AD「Web 應用程式」應用程式。</span><span class="sxs-lookup"><span data-stu-id="f46ff-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="f46ff-169">建立 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="f46ff-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="f46ff-170">使用下列程式碼片段來建立 Azure 資源群組︰</span><span class="sxs-lookup"><span data-stu-id="f46ff-170">Use the following code snippet to create an Azure Resource Group:</span></span>

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

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="f46ff-171">建立用戶端與 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="f46ff-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="f46ff-172">以下程式碼片段會先建立 Data Lake Store 帳戶用戶端。</span><span class="sxs-lookup"><span data-stu-id="f46ff-172">The following snippet first creates the Data Lake Store account client.</span></span> <span data-ttu-id="f46ff-173">它會使用用戶端物件來建立 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f46ff-173">It uses the client object to create a Data Lake Store account.</span></span> <span data-ttu-id="f46ff-174">最後，程式碼片段會建立檔案系統用戶端物件。</span><span class="sxs-lookup"><span data-stu-id="f46ff-174">Finally, the snippet creates a filesystem client object.</span></span>

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

## <a name="list-the-data-lake-store-accounts"></a><span data-ttu-id="f46ff-175">列出 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="f46ff-175">List the Data Lake Store accounts</span></span>

    ## List the existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="f46ff-176">建立目錄</span><span class="sxs-lookup"><span data-stu-id="f46ff-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="f46ff-177">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="f46ff-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="f46ff-178">下載檔案</span><span class="sxs-lookup"><span data-stu-id="f46ff-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="f46ff-179">刪除目錄</span><span class="sxs-lookup"><span data-stu-id="f46ff-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="f46ff-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f46ff-180">See also</span></span>

- [<span data-ttu-id="f46ff-181">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="f46ff-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="f46ff-182">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f46ff-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="f46ff-183">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f46ff-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="f46ff-184">Data Lake Store .NET SDK 參考</span><span class="sxs-lookup"><span data-stu-id="f46ff-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="f46ff-185">Data Lake Store REST 參考</span><span class="sxs-lookup"><span data-stu-id="f46ff-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
