---
title: "開始使用 Data Lake Store 的 aaaUse hello REST API tooget |Microsoft 文件"
description: "您可以使用 Data Lake store WebHDFS REST Api tooperform 作業"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="3b1b9-103">使用 REST API 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3b1b9-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b1b9-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="3b1b9-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="3b1b9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b1b9-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="3b1b9-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="3b1b9-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="3b1b9-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="3b1b9-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="3b1b9-108">REST API</span><span class="sxs-lookup"><span data-stu-id="3b1b9-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="3b1b9-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3b1b9-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="3b1b9-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="3b1b9-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="3b1b9-111">Python</span><span class="sxs-lookup"><span data-stu-id="3b1b9-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="3b1b9-112">在本文中，您將學習如何 toouse WebHDFS REST Api 和資料湖存放區 REST Api tooperform 帳戶管理，以及 Azure Data Lake Store 上的檔案系統作業。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-112">In this article, you will learn how toouse WebHDFS REST APIs and Data Lake Store REST APIs tooperform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="3b1b9-113">Azure Data Lake Store 會公開自己的 REST API 以進行帳戶管理作業。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="3b1b9-114">不過，因為 Data Lake Store 與 HDFS 和 Hadoop 生態系統相容，所以它支援使用 WebHDFS REST API 進行檔案系統作業。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="3b1b9-115">Data Lake Store 的 hello REST API 支援的詳細資訊，請參閱[Azure 資料湖存放區 REST API 參考](https://msdn.microsoft.com/library/mt693424.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-115">For detailed information on hello REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3b1b9-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="3b1b9-116">Prerequisites</span></span>
* <span data-ttu-id="3b1b9-117">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-117">**An Azure subscription**.</span></span> <span data-ttu-id="3b1b9-118">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3b1b9-119">**建立 Azure Active Directory 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="3b1b9-120">您可以使用 hello Azure AD 應用程式 tooauthenticate hello Data Lake Store 應用程式與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="3b1b9-121">有不同的方法 tooauthenticate 與 Azure AD，這是**使用者驗證**或**服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="3b1b9-122">如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="3b1b9-123">[cURL](http://curl.haxx.se/)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="3b1b9-124">本文使用 cURL toodemonstrate 如何 toomake REST API 呼叫針對 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-124">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="3b1b9-125">如何使用 Azure Active Directory 驗證？</span><span class="sxs-lookup"><span data-stu-id="3b1b9-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="3b1b9-126">您可以使用兩個方法 tooauthenticate 使用 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-126">You can use two approaches tooauthenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="3b1b9-127">使用者驗證 (互動式)</span><span class="sxs-lookup"><span data-stu-id="3b1b9-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="3b1b9-128">在此案例中，hello 應用程式會提示中的 hello 使用者 toolog 和 hello hello 使用者內容中執行所有的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-128">In this scenario, hello application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> <span data-ttu-id="3b1b9-129">執行 hello 互動式驗證步驟。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-129">Perform hello following steps for interactive authentication.</span></span>

1. <span data-ttu-id="3b1b9-130">您的應用程式，透過重新導向 hello 使用者 toohello 下列 URL:</span><span class="sxs-lookup"><span data-stu-id="3b1b9-130">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="3b1b9-131">\<重新導向 URI > 需要 toobe 編碼 URL 中使用。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-131">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="3b1b9-132">因此，針對 https://localhost，使用 `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="3b1b9-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="3b1b9-133">為了 hello 本教學課程，您可以取代上述 hello URL 中的 hello 預留位置值，並將它貼在網頁瀏覽器的網址列中。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-133">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="3b1b9-134">您將會重新導向的 tooauthenticate 使用您的 Azure 登入。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-134">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="3b1b9-135">一旦您已成功登入，hello 回應會顯示 hello 瀏覽器的網址列中。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-135">Once you successfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="3b1b9-136">hello 回應 hello 遵循格式會是：</span><span class="sxs-lookup"><span data-stu-id="3b1b9-136">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="3b1b9-137">擷取 hello 回應 hello 授權碼。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-137">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="3b1b9-138">此教學課程中，您可以複製 hello hello web 瀏覽器網址列中的 hello 授權碼，並將它傳遞 hello POST 要求 toohello 權杖端點，在如下所示：</span><span class="sxs-lookup"><span data-stu-id="3b1b9-138">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="3b1b9-139">在此情況下，hello\<重新導向 URI > 不需要進行編碼。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-139">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="3b1b9-140">hello 回應是包含存取權杖的 JSON 物件 (例如`"access_token": "<ACCESS_TOKEN>"`) 和重新整理權杖 (例如`"refresh_token": "<REFRESH_TOKEN>"`)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-140">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="3b1b9-141">您的應用程式使用 hello 存取權杖時存取 Azure 資料湖存放區和 hello 重新整理語彙基元 tooget 另一個存取權杖的存取權杖到期時。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-141">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="3b1b9-142">Hello 存取權杖過期時，您可以要求新的存取權杖使用 hello 重新整理權杖，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3b1b9-142">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="3b1b9-143">如需互動使用者驗證的詳細資料，請參閱 [授權碼授與流程](https://msdn.microsoft.com/library/azure/dn645542.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="3b1b9-144">服務對服務驗證 (非互動式)</span><span class="sxs-lookup"><span data-stu-id="3b1b9-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="3b1b9-145">在此案例中，hello hello 應用程式會提供自己的認證 tooperform hello 作業。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-145">In this scenario, hello hello application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="3b1b9-146">這麼做，您必須發出 POST 要求像 hello 一個如下所示。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-146">For this, you must issue a POST request like hello one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="3b1b9-147">這項要求的 hello 輸出將包括授權權杖 (表示`access-token`hello 以下的輸出中)，您接下來將會傳遞 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-147">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="3b1b9-148">將此驗證權杖儲存在文字檔中；您將在本文稍後需要此權杖。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="3b1b9-149">本文使用 hello**非互動式**方法。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-149">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="3b1b9-150">如需有關非互動式 （服務對服務呼叫） 的詳細資訊，請參閱[服務會使用認證 tooservice 呼叫](https://msdn.microsoft.com/library/azure/dn645543.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-150">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="3b1b9-151">建立 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="3b1b9-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="3b1b9-152">這項作業根據定義的 hello REST API 呼叫[這裡](https://msdn.microsoft.com/library/mt694078.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-152">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="3b1b9-153">使用下列 cURL 命令 hello。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-153">Use hello following cURL command.</span></span> <span data-ttu-id="3b1b9-154">以 Data Lake Store 名稱取代 **\<yourstorename>**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="3b1b9-155">在上述命令 hello，取代\< `REDACTED` \> hello 授權權杖與先前擷取。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-155">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="3b1b9-156">此命令的 hello 要求承載包含在 hello **input.json**提供 hello 檔案`-d`上述的參數。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-156">hello request payload for this command is contained in hello **input.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="3b1b9-157">hello hello input.json 檔內容看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="3b1b9-157">hello contents of hello input.json file resemble hello following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="3b1b9-158">在 Data Lake Store 帳戶中建立資料夾</span><span class="sxs-lookup"><span data-stu-id="3b1b9-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="3b1b9-159">這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-159">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="3b1b9-160">使用下列 cURL 命令 hello。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-160">Use hello following cURL command.</span></span> <span data-ttu-id="3b1b9-161">以 Data Lake Store 名稱取代 **\<yourstorename>**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="3b1b9-162">在上述命令 hello，取代\< `REDACTED` \> hello 授權權杖與先前擷取。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-162">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="3b1b9-163">此命令會建立名為目錄**mytempdir** hello 的 Data Lake Store 帳戶的根資料夾下。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-163">This command creates a directory called **mytempdir** under hello root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="3b1b9-164">如果 hello 作業順利完成，您會看到如下的回應：</span><span class="sxs-lookup"><span data-stu-id="3b1b9-164">You should see a response like this if hello operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="3b1b9-165">在 Data Lake Store 帳戶中列入資料夾</span><span class="sxs-lookup"><span data-stu-id="3b1b9-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="3b1b9-166">這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-166">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="3b1b9-167">使用下列 cURL 命令 hello。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-167">Use hello following cURL command.</span></span> <span data-ttu-id="3b1b9-168">以 Data Lake Store 名稱取代 **\<yourstorename>**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="3b1b9-169">在上述命令 hello，取代\< `REDACTED` \> hello 授權權杖與先前擷取。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-169">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span>

<span data-ttu-id="3b1b9-170">如果 hello 作業順利完成，您會看到如下的回應：</span><span class="sxs-lookup"><span data-stu-id="3b1b9-170">You should see a response like this if hello operation completes successfully:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="3b1b9-171">將資料上傳至 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="3b1b9-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="3b1b9-172">這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-172">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="3b1b9-173">使用下列 cURL 命令 hello。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-173">Use hello following cURL command.</span></span> <span data-ttu-id="3b1b9-174">以 Data Lake Store 名稱取代 **\<yourstorename>**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="3b1b9-175">在上述語法 hello **-T**參數是您要上傳的 hello 檔案 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-175">In hello above syntax **-T** parameter is hello location of hello file you are uploading.</span></span>

<span data-ttu-id="3b1b9-176">hello 輸出是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="3b1b9-176">hello output is similar toohello following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="3b1b9-177">從 Data Lake Store 帳戶讀取資料</span><span class="sxs-lookup"><span data-stu-id="3b1b9-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="3b1b9-178">這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-178">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="3b1b9-179">從 Data Lake Store 帳戶讀取資料是兩個步驟的程序。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="3b1b9-180">您第一次提交的 GET 要求針對 hello 端點`https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-180">You first submit a GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="3b1b9-181">這會傳回要求的位置 toosubmit hello 下一個 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-181">This will return a location toosubmit hello next GET request to.</span></span>
* <span data-ttu-id="3b1b9-182">然後送出 hello GET 要求，針對 hello 端點`https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-182">You then submit hello GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="3b1b9-183">這會顯示 hello hello 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-183">This will display hello contents of hello file.</span></span>

<span data-ttu-id="3b1b9-184">不過，因為沒有任何差異在 hello hello 個輸入的參數先和 hello 的第二個步驟，您可以使用 hello`-L`參數 toosubmit hello 第一個要求。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-184">However, because there is no difference in hello input parameters between hello first and hello second step, you can use hello `-L` parameter toosubmit hello first request.</span></span> <span data-ttu-id="3b1b9-185">`-L`選項基本上結合成一個兩個要求，並將 cURL 重做 hello hello 新位置上的要求。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-185">`-L` option essentially combines two requests into one and will make cURL redo hello request on hello new location.</span></span> <span data-ttu-id="3b1b9-186">最後，hello hello 之所有要求呼叫就會顯示輸出，例如如下所示。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-186">Finally, hello output from all hello request calls is displayed, like shown below.</span></span> <span data-ttu-id="3b1b9-187">以 Data Lake Store 名稱取代 **\<yourstorename>**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="3b1b9-188">您應該會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="3b1b9-188">You should see an output similar toohello following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="3b1b9-189">在 Data Lake Store 帳戶中重新命名檔案</span><span class="sxs-lookup"><span data-stu-id="3b1b9-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="3b1b9-190">這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-190">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="3b1b9-191">使用 hello 下列 cURL 命令 toorename 檔案。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-191">Use hello following cURL command toorename a file.</span></span> <span data-ttu-id="3b1b9-192">以 Data Lake Store 名稱取代 **\<yourstorename>**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="3b1b9-193">您應該會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="3b1b9-193">You should see an output similar toohello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="3b1b9-194">從 Data Lake Store 帳戶刪除檔案</span><span class="sxs-lookup"><span data-stu-id="3b1b9-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="3b1b9-195">這項作業根據定義的 hello WebHDFS REST API 呼叫[這裡](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-195">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="3b1b9-196">使用 hello 下列 cURL 命令 toodelete 檔案。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-196">Use hello following cURL command toodelete a file.</span></span> <span data-ttu-id="3b1b9-197">以 Data Lake Store 名稱取代 **\<yourstorename>**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="3b1b9-198">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="3b1b9-198">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="3b1b9-199">刪除 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="3b1b9-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="3b1b9-200">這項作業根據定義的 hello REST API 呼叫[這裡](https://msdn.microsoft.com/library/mt694075.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-200">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="3b1b9-201">使用 hello 下列 cURL 命令 toodelete Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-201">Use hello following cURL command toodelete a Data Lake Store account.</span></span> <span data-ttu-id="3b1b9-202">以 Data Lake Store 名稱取代 **\<yourstorename>**。</span><span class="sxs-lookup"><span data-stu-id="3b1b9-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="3b1b9-203">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="3b1b9-203">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="3b1b9-204">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3b1b9-204">See also</span></span>
* [<span data-ttu-id="3b1b9-205">與 Azure Data Lake Store 相容的開放原始碼巨量資料應用程式</span><span class="sxs-lookup"><span data-stu-id="3b1b9-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

