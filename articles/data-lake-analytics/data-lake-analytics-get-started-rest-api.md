---
title: "開始使用 Data Lake Analytics 使用 REST API 的 aaaGet |Microsoft 文件"
description: "使用 Data Lake Analytics tooperform WebHDFS REST Api 作業"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="688dd-103">使用 REST API 開始使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="688dd-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="688dd-104">了解 toouse WebHDFS REST Api 和資料湖分析 REST Api toomanage Data Lake Analytics 帳戶、 作業、 和目錄的方式。</span><span class="sxs-lookup"><span data-stu-id="688dd-104">Learn how toouse WebHDFS REST APIs and Data Lake Analytics REST APIs toomanage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="688dd-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="688dd-105">Prerequisites</span></span>
* <span data-ttu-id="688dd-106">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="688dd-106">**An Azure subscription**.</span></span> <span data-ttu-id="688dd-107">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="688dd-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="688dd-108">**建立 Azure Active Directory 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="688dd-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="688dd-109">您可以使用 hello Azure AD 應用程式 tooauthenticate hello Data Lake Analytics 應用程式與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="688dd-109">You use hello Azure AD application tooauthenticate hello Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="688dd-110">有不同的方法 tooauthenticate 與 Azure AD，這是**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="688dd-110">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="688dd-111">如需指示和詳細資訊 tooauthenticate，請參閱[驗證與使用 Azure Active Directory 的 Data Lake Analytics](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="688dd-111">For instructions and more information on how tooauthenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="688dd-112">[cURL](http://curl.haxx.se/)。</span><span class="sxs-lookup"><span data-stu-id="688dd-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="688dd-113">本文使用 cURL toodemonstrate 如何 toomake REST API 呼叫針對 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="688dd-113">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="688dd-114">向 Azure Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="688dd-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="688dd-115">向 Azure Active Directory 進行驗證的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="688dd-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="688dd-116">使用者驗證 (互動式)</span><span class="sxs-lookup"><span data-stu-id="688dd-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="688dd-117">使用此方法時，應用程式會提示中的 hello 使用者 toolog 和 hello hello 使用者內容中執行所有的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="688dd-117">Using this method, application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> 

<span data-ttu-id="688dd-118">遵循下列步驟進行互動式驗證：</span><span class="sxs-lookup"><span data-stu-id="688dd-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="688dd-119">您的應用程式，透過重新導向 hello 使用者 toohello 下列 URL:</span><span class="sxs-lookup"><span data-stu-id="688dd-119">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="688dd-120">\<重新導向 URI > 需要 toobe 編碼 URL 中使用。</span><span class="sxs-lookup"><span data-stu-id="688dd-120">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="688dd-121">因此，針對 https://localhost，使用 `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="688dd-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="688dd-122">為了 hello 本教學課程，您可以取代上述 hello URL 中的 hello 預留位置值，並將它貼在網頁瀏覽器的網址列中。</span><span class="sxs-lookup"><span data-stu-id="688dd-122">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="688dd-123">您將會重新導向的 tooauthenticate 使用您的 Azure 登入。</span><span class="sxs-lookup"><span data-stu-id="688dd-123">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="688dd-124">一旦您已成功登入，hello 回應會顯示 hello 瀏覽器的網址列中。</span><span class="sxs-lookup"><span data-stu-id="688dd-124">Once you succesfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="688dd-125">hello 回應 hello 遵循格式會是：</span><span class="sxs-lookup"><span data-stu-id="688dd-125">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="688dd-126">擷取 hello 回應 hello 授權碼。</span><span class="sxs-lookup"><span data-stu-id="688dd-126">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="688dd-127">此教學課程中，您可以複製 hello hello web 瀏覽器網址列中的 hello 授權碼，並將它傳遞 hello POST 要求 toohello 權杖端點，在如下所示：</span><span class="sxs-lookup"><span data-stu-id="688dd-127">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="688dd-128">在此情況下，hello\<重新導向 URI > 不需要進行編碼。</span><span class="sxs-lookup"><span data-stu-id="688dd-128">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="688dd-129">hello 回應是包含存取權杖的 JSON 物件 (例如`"access_token": "<ACCESS_TOKEN>"`) 和重新整理權杖 (例如`"refresh_token": "<REFRESH_TOKEN>"`)。</span><span class="sxs-lookup"><span data-stu-id="688dd-129">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="688dd-130">您的應用程式使用 hello 存取權杖時存取 Azure 資料湖存放區和 hello 重新整理語彙基元 tooget 另一個存取權杖的存取權杖到期時。</span><span class="sxs-lookup"><span data-stu-id="688dd-130">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="688dd-131">Hello 存取權杖過期時，您可以要求新的存取權杖使用 hello 重新整理權杖，如下所示：</span><span class="sxs-lookup"><span data-stu-id="688dd-131">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="688dd-132">如需互動使用者驗證的詳細資料，請參閱 [授權碼授與流程](https://msdn.microsoft.com/library/azure/dn645542.aspx)。</span><span class="sxs-lookup"><span data-stu-id="688dd-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="688dd-133">服務對服務驗證 (非互動式)</span><span class="sxs-lookup"><span data-stu-id="688dd-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="688dd-134">使用此方法時，應用程式會提供自己的認證 tooperform hello 作業。</span><span class="sxs-lookup"><span data-stu-id="688dd-134">Using this method, application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="688dd-135">這麼做，您必須發出 POST 要求像 hello 一個如下所示：</span><span class="sxs-lookup"><span data-stu-id="688dd-135">For this, you must issue a POST request like hello one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="688dd-136">這項要求的 hello 輸出將包括授權權杖 (表示`access-token`hello 以下的輸出中)，您接下來將會傳遞 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="688dd-136">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="688dd-137">將此驗證權杖儲存在文字檔中；您將在本文稍後需要此權杖。</span><span class="sxs-lookup"><span data-stu-id="688dd-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="688dd-138">本文使用 hello**非互動式**方法。</span><span class="sxs-lookup"><span data-stu-id="688dd-138">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="688dd-139">如需有關非互動式 （服務對服務呼叫） 的詳細資訊，請參閱[服務會使用認證 tooservice 呼叫](https://msdn.microsoft.com/library/azure/dn645543.aspx)。</span><span class="sxs-lookup"><span data-stu-id="688dd-139">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="688dd-140">建立 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="688dd-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="688dd-141">您必須先建立 Azure 資源群組和 Data Lake Store 帳戶，才可以建立 Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="688dd-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="688dd-142">請參閱[建立 Data Lake Store 帳戶](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account)。</span><span class="sxs-lookup"><span data-stu-id="688dd-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="688dd-143">hello 遵循 Curl 命令顯示如何 toocreate 帳戶：</span><span class="sxs-lookup"><span data-stu-id="688dd-143">hello following Curl command shows how toocreate an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="688dd-144">取代\< `REDACTED` \>與 hello 授權權杖， \< `AzureSubscriptionID` \>以您的訂用帳戶 ID， \< `AzureResourceGroupName` \>與現有的 Azure 資源群組名稱和\< `NewAzureDataLakeAnalyticsAccountName` \>以新的資料湖分析帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="688dd-144">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="688dd-145">此命令的 hello 要求承載包含在 hello **CreateDatalakeAnalyticsAccountRequest.json**提供 hello 檔案`-d`上述的參數。</span><span class="sxs-lookup"><span data-stu-id="688dd-145">hello request payload for this command is contained in hello **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="688dd-146">hello hello input.json 檔內容看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="688dd-146">hello contents of hello input.json file resemble hello following:</span></span>

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="688dd-147">列出訂用帳戶中的 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="688dd-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="688dd-148">hello 下列 Curl 命令顯示如何 toolist 帳戶的訂用帳戶中：</span><span class="sxs-lookup"><span data-stu-id="688dd-148">hello following Curl command shows how toolist accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="688dd-149">取代\< `REDACTED` \>與 hello 授權權杖， \< `AzureSubscriptionID` \>與您的訂用帳戶 id。</span><span class="sxs-lookup"><span data-stu-id="688dd-149">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="688dd-150">hello 輸出如下：</span><span class="sxs-lookup"><span data-stu-id="688dd-150">hello output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="688dd-151">取得 Data Lake Analytics 帳戶的相關資訊</span><span class="sxs-lookup"><span data-stu-id="688dd-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="688dd-152">hello 遵循 Curl 命令顯示如何 tooget 帳戶資訊：</span><span class="sxs-lookup"><span data-stu-id="688dd-152">hello following Curl command shows how tooget an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="688dd-153">取代\< `REDACTED` \>與 hello 授權權杖， \< `AzureSubscriptionID` \>以您的訂用帳戶 ID， \< `AzureResourceGroupName` \>與現有的 Azure 資源群組名稱和\< `DataLakeAnalyticsAccountName` \> hello 現有的資料湖分析帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="688dd-153">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="688dd-154">hello 輸出如下：</span><span class="sxs-lookup"><span data-stu-id="688dd-154">hello output is similar to:</span></span>

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="688dd-155">列出 Data Lake Analytics 帳戶的 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="688dd-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="688dd-156">hello 下列 Curl 命令顯示如何 toolist 資料湖存放的帳戶：</span><span class="sxs-lookup"><span data-stu-id="688dd-156">hello following Curl command shows how toolist Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="688dd-157">取代\< `REDACTED` \>與 hello 授權權杖， \< `AzureSubscriptionID` \>以您的訂用帳戶 ID， \< `AzureResourceGroupName` \>與現有的 Azure 資源群組名稱和\< `DataLakeAnalyticsAccountName` \> hello 現有的資料湖分析帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="688dd-157">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="688dd-158">hello 輸出如下：</span><span class="sxs-lookup"><span data-stu-id="688dd-158">hello output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="688dd-159">提交 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="688dd-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="688dd-160">hello 遵循 Curl 命令顯示如何 toosubmit U SQL 工作：</span><span class="sxs-lookup"><span data-stu-id="688dd-160">hello following Curl command shows how toosubmit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="688dd-161">取代\< `REDACTED` \>與 hello 授權權杖， \< `DataLakeAnalyticsAccountName` \> hello 現有的資料湖分析帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="688dd-161">Replace \<`REDACTED`\> with hello authorization token, \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="688dd-162">此命令的 hello 要求承載包含在 hello **SubmitADLAJob.json**提供 hello 檔案`-d`上述的參數。</span><span class="sxs-lookup"><span data-stu-id="688dd-162">hello request payload for this command is contained in hello **SubmitADLAJob.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="688dd-163">hello hello input.json 檔內容看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="688dd-163">hello contents of hello input.json file resemble hello following:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="688dd-164">hello 輸出如下：</span><span class="sxs-lookup"><span data-stu-id="688dd-164">hello output is similar to:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a><span data-ttu-id="688dd-165">列出 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="688dd-165">List U-SQL jobs</span></span>
<span data-ttu-id="688dd-166">hello 遵循 Curl 命令顯示如何 toolist U-SQL 作業：</span><span class="sxs-lookup"><span data-stu-id="688dd-166">hello following Curl command shows how toolist U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="688dd-167">取代\< `REDACTED` \>與 hello 授權權杖，並\< `DataLakeAnalyticsAccountName` \> hello 現有的資料湖分析帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="688dd-167">Replace \<`REDACTED`\> with hello authorization token, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="688dd-168">hello 輸出如下：</span><span class="sxs-lookup"><span data-stu-id="688dd-168">hello output is similar to:</span></span>

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a><span data-ttu-id="688dd-169">取得目錄項目</span><span class="sxs-lookup"><span data-stu-id="688dd-169">Get catalog items</span></span>
<span data-ttu-id="688dd-170">hello 下列 Curl 命令顯示如何從 tooget hello 資料庫 hello 目錄：</span><span class="sxs-lookup"><span data-stu-id="688dd-170">hello following Curl command shows how tooget hello databases from hello catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="688dd-171">hello 輸出如下：</span><span class="sxs-lookup"><span data-stu-id="688dd-171">hello output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="688dd-172">另請參閱</span><span class="sxs-lookup"><span data-stu-id="688dd-172">See also</span></span>
* <span data-ttu-id="688dd-173">toosee 更複雜的查詢，請參閱[使用 Azure Data Lake Analytics 分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。</span><span class="sxs-lookup"><span data-stu-id="688dd-173">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="688dd-174">tooget 開始開發 U-SQL 應用程式，請參閱[使用 Data Lake Tools for Visual Studio 的開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="688dd-174">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="688dd-175">toolearn U-SQL，請參閱[開始使用 Azure 資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="688dd-175">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="688dd-176">針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="688dd-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="688dd-177">tooget 的概觀的 Data Lake Analytics，請參閱[Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="688dd-177">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="688dd-178">toosee hello 相同教學課程中使用其他工具中，按一下在 hello hello 頁面最上方的 hello 索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="688dd-178">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>

