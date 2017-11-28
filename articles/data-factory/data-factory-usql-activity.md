---
title: "使用 U-SQL 指令碼-Azure aaaTransform 資料 |Microsoft 文件"
description: "了解如何藉由執行在 Azure Data Lake Analytics U-SQL 指令碼 tooprocess 或轉換資料計算服務。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="fcc61-103">在 Azure Data Lake Analytics 上執行 U-SQL 指令碼來轉換資料</span><span class="sxs-lookup"><span data-stu-id="fcc61-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="fcc61-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="fcc61-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="fcc61-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="fcc61-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="fcc61-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="fcc61-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="fcc61-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="fcc61-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="fcc61-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="fcc61-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="fcc61-114">Azure Data Factory 中的「管線」會使用連結的計算服務，來處理連結的儲存體服務中的資料。</span><span class="sxs-lookup"><span data-stu-id="fcc61-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="fcc61-115">它包含一系列活動，其中每個活動都會執行特定的處理作業。</span><span class="sxs-lookup"><span data-stu-id="fcc61-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="fcc61-116">本文說明 hello**資料 Lake Analytics U-SQL 活動**執行**U-SQL**上的指令碼**Azure Data Lake Analytics**計算連結的服務。</span><span class="sxs-lookup"><span data-stu-id="fcc61-116">This article describes hello **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="fcc61-117">使用 Data Lake Analytics「U-SQL 活動」來建立管線之前，請先建立 Azure Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fcc61-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="fcc61-118">toolearn 有關 Azure Data Lake Analytics，請參閱[開始使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc61-118">toolearn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="fcc61-119">檢閱 hello[建置您的第一個管線教學課程](data-factory-build-your-first-pipeline.md)的詳細的步驟 toocreate data factory，連結的服務、 資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="fcc61-119">Review hello [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps toocreate a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="fcc61-120">使用 Data Factory 編輯器或 Visual Studio 或 Azure PowerShell toocreate Data Factory 實體的 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="fcc61-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell toocreate Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="fcc61-121">支援的驗證類型</span><span class="sxs-lookup"><span data-stu-id="fcc61-121">Supported authentication types</span></span>
<span data-ttu-id="fcc61-122">U-SQL 活動支援以下針對 Data Lake Analytics 的驗證類型：</span><span class="sxs-lookup"><span data-stu-id="fcc61-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="fcc61-123">服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="fcc61-123">Service principal authentication</span></span>
* <span data-ttu-id="fcc61-124">使用者認證 (OAuth) 驗證</span><span class="sxs-lookup"><span data-stu-id="fcc61-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="fcc61-125">我們建議您使用服務主體驗證，特別是針對排程的 U-SQL 執行。</span><span class="sxs-lookup"><span data-stu-id="fcc61-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="fcc61-126">權杖到期行為會連同使用者認證驗證發生。</span><span class="sxs-lookup"><span data-stu-id="fcc61-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="fcc61-127">設定詳細資料，請參閱 hello[連結服務屬性](#azure-data-lake-analytics-linked-service)> 一節。</span><span class="sxs-lookup"><span data-stu-id="fcc61-127">For configuration details, see hello [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="fcc61-128">Azure Data Lake Analytics 連結服務</span><span class="sxs-lookup"><span data-stu-id="fcc61-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="fcc61-129">您建立**Azure Data Lake Analytics**連結服務 toolink Azure Data Lake Analytics 計算服務 tooan Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="fcc61-129">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="fcc61-130">hello hello 管線中的資料 Lake Analytics U-SQL 活動指的是 toothis 連結服務。</span><span class="sxs-lookup"><span data-stu-id="fcc61-130">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="fcc61-131">hello 下表提供說明 hello hello JSON 定義中使用的一般內容。</span><span class="sxs-lookup"><span data-stu-id="fcc61-131">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="fcc61-132">您可以在服務主體與使用者認證驗證之間進一步選擇。</span><span class="sxs-lookup"><span data-stu-id="fcc61-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="fcc61-133">屬性</span><span class="sxs-lookup"><span data-stu-id="fcc61-133">Property</span></span> | <span data-ttu-id="fcc61-134">說明</span><span class="sxs-lookup"><span data-stu-id="fcc61-134">Description</span></span> | <span data-ttu-id="fcc61-135">必要</span><span class="sxs-lookup"><span data-stu-id="fcc61-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fcc61-136">**type**</span><span class="sxs-lookup"><span data-stu-id="fcc61-136">**type**</span></span> |<span data-ttu-id="fcc61-137">hello 類型屬性應該設定為： **AzureDataLakeAnalytics**。</span><span class="sxs-lookup"><span data-stu-id="fcc61-137">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="fcc61-138">是</span><span class="sxs-lookup"><span data-stu-id="fcc61-138">Yes</span></span> |
| <span data-ttu-id="fcc61-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="fcc61-139">**accountName**</span></span> |<span data-ttu-id="fcc61-140">Azure Data Lake Analytics 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="fcc61-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="fcc61-141">是</span><span class="sxs-lookup"><span data-stu-id="fcc61-141">Yes</span></span> |
| <span data-ttu-id="fcc61-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="fcc61-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="fcc61-143">Azure Data Lake Analytics URI。</span><span class="sxs-lookup"><span data-stu-id="fcc61-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="fcc61-144">否</span><span class="sxs-lookup"><span data-stu-id="fcc61-144">No</span></span> |
| <span data-ttu-id="fcc61-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="fcc61-145">**subscriptionId**</span></span> |<span data-ttu-id="fcc61-146">Azure 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="fcc61-146">Azure subscription id</span></span> |<span data-ttu-id="fcc61-147">否 （如果未指定，訂用帳戶的資料處理站可用的 hello）。</span><span class="sxs-lookup"><span data-stu-id="fcc61-147">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="fcc61-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="fcc61-148">**resourceGroupName**</span></span> |<span data-ttu-id="fcc61-149">Azure 資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="fcc61-149">Azure resource group name</span></span> |<span data-ttu-id="fcc61-150">否 （如果未指定，資源群組的資料處理站可用的 hello）。</span><span class="sxs-lookup"><span data-stu-id="fcc61-150">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="fcc61-151">服務主體驗證 (建議)</span><span class="sxs-lookup"><span data-stu-id="fcc61-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="fcc61-152">服務主體驗證 toouse，註冊在 Azure Active Directory (Azure AD) 和授與它 hello 應用程式的實體存取 tooData 湖存放區。</span><span class="sxs-lookup"><span data-stu-id="fcc61-152">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="fcc61-153">如需詳細的步驟，請參閱[服務對服務驗證](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc61-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="fcc61-154">請記下的下列值，您使用的 hello toodefine hello 連結服務：</span><span class="sxs-lookup"><span data-stu-id="fcc61-154">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="fcc61-155">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="fcc61-155">Application ID</span></span>
* <span data-ttu-id="fcc61-156">應用程式金鑰</span><span class="sxs-lookup"><span data-stu-id="fcc61-156">Application key</span></span> 
* <span data-ttu-id="fcc61-157">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="fcc61-157">Tenant ID</span></span>

<span data-ttu-id="fcc61-158">您可以使用服務主體的驗證方法是指定 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="fcc61-158">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="fcc61-159">屬性</span><span class="sxs-lookup"><span data-stu-id="fcc61-159">Property</span></span> | <span data-ttu-id="fcc61-160">說明</span><span class="sxs-lookup"><span data-stu-id="fcc61-160">Description</span></span> | <span data-ttu-id="fcc61-161">必要</span><span class="sxs-lookup"><span data-stu-id="fcc61-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fcc61-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="fcc61-162">**servicePrincipalId**</span></span> | <span data-ttu-id="fcc61-163">指定 hello 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="fcc61-163">Specify hello application's client ID.</span></span> | <span data-ttu-id="fcc61-164">是</span><span class="sxs-lookup"><span data-stu-id="fcc61-164">Yes</span></span> |
| <span data-ttu-id="fcc61-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="fcc61-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="fcc61-166">指定 hello 應用程式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="fcc61-166">Specify hello application's key.</span></span> | <span data-ttu-id="fcc61-167">是</span><span class="sxs-lookup"><span data-stu-id="fcc61-167">Yes</span></span> |
| <span data-ttu-id="fcc61-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="fcc61-168">**tenant**</span></span> | <span data-ttu-id="fcc61-169">指定在您的應用程式所在的 hello 租用戶資訊 (網域名稱或租用戶 ID)。</span><span class="sxs-lookup"><span data-stu-id="fcc61-169">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="fcc61-170">您可以透過暫留在 hello 右上角的 hello Azure 入口網站中的 hello 滑鼠擷取它。</span><span class="sxs-lookup"><span data-stu-id="fcc61-170">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="fcc61-171">是</span><span class="sxs-lookup"><span data-stu-id="fcc61-171">Yes</span></span> |

<span data-ttu-id="fcc61-172">**範例：服務主體驗證**</span><span class="sxs-lookup"><span data-stu-id="fcc61-172">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="fcc61-173">使用者認證驗證</span><span class="sxs-lookup"><span data-stu-id="fcc61-173">User credential authentication</span></span>
<span data-ttu-id="fcc61-174">或者，您可以使用使用者認證驗證的 Data Lake Analytics 藉由指定下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="fcc61-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="fcc61-175">屬性</span><span class="sxs-lookup"><span data-stu-id="fcc61-175">Property</span></span> | <span data-ttu-id="fcc61-176">說明</span><span class="sxs-lookup"><span data-stu-id="fcc61-176">Description</span></span> | <span data-ttu-id="fcc61-177">必要</span><span class="sxs-lookup"><span data-stu-id="fcc61-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fcc61-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="fcc61-178">**authorization**</span></span> | <span data-ttu-id="fcc61-179">按一下 hello**授權**按鈕 hello Data Factory 編輯器中，並輸入您 hello 自動產生的授權 URL toothis 屬性指派的認證。</span><span class="sxs-lookup"><span data-stu-id="fcc61-179">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="fcc61-180">是</span><span class="sxs-lookup"><span data-stu-id="fcc61-180">Yes</span></span> |
| <span data-ttu-id="fcc61-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="fcc61-181">**sessionId**</span></span> | <span data-ttu-id="fcc61-182">從 hello OAuth 授權工作階段的 OAuth 工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="fcc61-182">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="fcc61-183">每個工作階段識別碼都是唯一的，只能使用一次。</span><span class="sxs-lookup"><span data-stu-id="fcc61-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="fcc61-184">當您使用 hello Data Factory 編輯器時，此設定會自動產生。</span><span class="sxs-lookup"><span data-stu-id="fcc61-184">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="fcc61-185">是</span><span class="sxs-lookup"><span data-stu-id="fcc61-185">Yes</span></span> |

<span data-ttu-id="fcc61-186">**範例：使用者認證授權**</span><span class="sxs-lookup"><span data-stu-id="fcc61-186">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="fcc61-187">權杖到期</span><span class="sxs-lookup"><span data-stu-id="fcc61-187">Token expiration</span></span>
<span data-ttu-id="fcc61-188">hello 您使用 hello 所產生的授權碼**授權**一段時間後到期 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcc61-188">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="fcc61-189">請參閱下表針對不同類型的使用者帳戶的 hello 逾期時間的 hello。</span><span class="sxs-lookup"><span data-stu-id="fcc61-189">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="fcc61-190">您可能會看到下列錯誤訊息的 hello 當 hello 驗證**權杖到期**： 認證作業發生錯誤： invalid_grant-AADSTS70002： 驗證認證時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="fcc61-190">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="fcc61-191">AADSTS70008: hello 提供存取權限已過期或撤銷。</span><span class="sxs-lookup"><span data-stu-id="fcc61-191">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="fcc61-192">追蹤識別碼：d18629e8-af88-43c5-88e3-d8419eb1fca1 相互關連識別碼：fac30a0c-6be6-4e02-8d69-a776d2ffefd7 時間戳記：2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="fcc61-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="fcc61-193">使用者類型</span><span class="sxs-lookup"><span data-stu-id="fcc61-193">User type</span></span> | <span data-ttu-id="fcc61-194">到期時間</span><span class="sxs-lookup"><span data-stu-id="fcc61-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="fcc61-195">不受 Azure Active Directory 管理的使用者帳戶 (@hotmail.com、@live.com 等)</span><span class="sxs-lookup"><span data-stu-id="fcc61-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="fcc61-196">12 小時</span><span class="sxs-lookup"><span data-stu-id="fcc61-196">12 hours</span></span> |
| <span data-ttu-id="fcc61-197">受 Azure Active Directory (AAD) 管理的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="fcc61-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="fcc61-198">14 天之後 hello 最後一個配量執行。</span><span class="sxs-lookup"><span data-stu-id="fcc61-198">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="fcc61-199">如果以 OAuth 式連結服務為基礎的配量至少每 14 天執行一次，則為 90 天。</span><span class="sxs-lookup"><span data-stu-id="fcc61-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="fcc61-200">tooavoid/解決這個錯誤，重新授權使用 hello**授權**按鈕時 hello**權杖到期**然後重新部署 hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="fcc61-200">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="fcc61-201">您也可以如下使用程式碼，以程式設計方式產生 **sessionId** 和 **authorization** 屬性的值：</span><span class="sxs-lookup"><span data-stu-id="fcc61-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

<span data-ttu-id="fcc61-202">請參閱[AzureDataLakeStoreLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)， [AzureDataLakeAnalyticsLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)，和[AuthorizationSessionGetResponse 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx)主題的詳細資訊關於 hello hello 程式碼中使用的 Data Factory 類別。</span><span class="sxs-lookup"><span data-stu-id="fcc61-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="fcc61-203">加入的參考： Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll hello WindowsFormsWebAuthenticationDialog 類別。</span><span class="sxs-lookup"><span data-stu-id="fcc61-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="fcc61-204">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="fcc61-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="fcc61-205">hello 下列 JSON 片段會定義具有資料 Lake Analytics U-SQL 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="fcc61-205">hello following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="fcc61-206">hello 活動定義具有參考 toohello 您稍早建立的連結的 Azure 資料湖分析服務。</span><span class="sxs-lookup"><span data-stu-id="fcc61-206">hello activity definition has a reference toohello Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="fcc61-207">hello 下表描述之特定 toothis 活動的屬性名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="fcc61-207">hello following table describes names and descriptions of properties that are specific toothis activity.</span></span> 

| <span data-ttu-id="fcc61-208">屬性</span><span class="sxs-lookup"><span data-stu-id="fcc61-208">Property</span></span> | <span data-ttu-id="fcc61-209">說明</span><span class="sxs-lookup"><span data-stu-id="fcc61-209">Description</span></span> | <span data-ttu-id="fcc61-210">必要</span><span class="sxs-lookup"><span data-stu-id="fcc61-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fcc61-211">類型</span><span class="sxs-lookup"><span data-stu-id="fcc61-211">type</span></span> |<span data-ttu-id="fcc61-212">hello type 屬性必須設定得**DataLakeAnalyticsU SQL**。</span><span class="sxs-lookup"><span data-stu-id="fcc61-212">hello type property must be set too**DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="fcc61-213">是</span><span class="sxs-lookup"><span data-stu-id="fcc61-213">Yes</span></span> |
| <span data-ttu-id="fcc61-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="fcc61-214">scriptPath</span></span> |<span data-ttu-id="fcc61-215">路徑 toofolder 包含 hello U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="fcc61-215">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="fcc61-216">Hello 檔案的名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="fcc61-216">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="fcc61-217">否 (如果您使用指令碼)</span><span class="sxs-lookup"><span data-stu-id="fcc61-217">No (if you use script)</span></span> |
| <span data-ttu-id="fcc61-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="fcc61-218">scriptLinkedService</span></span> |<span data-ttu-id="fcc61-219">連結包含 hello 指令碼 toohello 資料 factory 的 hello 儲存體連結的服務</span><span class="sxs-lookup"><span data-stu-id="fcc61-219">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="fcc61-220">否 (如果您使用指令碼)</span><span class="sxs-lookup"><span data-stu-id="fcc61-220">No (if you use script)</span></span> |
| <span data-ttu-id="fcc61-221">script</span><span class="sxs-lookup"><span data-stu-id="fcc61-221">script</span></span> |<span data-ttu-id="fcc61-222">指定內嵌指令碼而不是指定 scriptPath 和 scriptLinkedService。</span><span class="sxs-lookup"><span data-stu-id="fcc61-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="fcc61-223">例如： `"script": "CREATE DATABASE test"`。</span><span class="sxs-lookup"><span data-stu-id="fcc61-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="fcc61-224">否 (如果您使用 scriptPath 和 scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="fcc61-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="fcc61-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="fcc61-225">degreeOfParallelism</span></span> |<span data-ttu-id="fcc61-226">hello 的節點數目上限，同時使用 toorun hello 作業。</span><span class="sxs-lookup"><span data-stu-id="fcc61-226">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="fcc61-227">否</span><span class="sxs-lookup"><span data-stu-id="fcc61-227">No</span></span> |
| <span data-ttu-id="fcc61-228">優先順序</span><span class="sxs-lookup"><span data-stu-id="fcc61-228">priority</span></span> |<span data-ttu-id="fcc61-229">決定從所有已排入佇列的作業應該選取的 toorun 第一次。</span><span class="sxs-lookup"><span data-stu-id="fcc61-229">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="fcc61-230">hello 低 hello 數字，hello hello 優先順序越高。</span><span class="sxs-lookup"><span data-stu-id="fcc61-230">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="fcc61-231">否</span><span class="sxs-lookup"><span data-stu-id="fcc61-231">No</span></span> |
| <span data-ttu-id="fcc61-232">參數</span><span class="sxs-lookup"><span data-stu-id="fcc61-232">parameters</span></span> |<span data-ttu-id="fcc61-233">Hello U-SQL 指令碼的參數</span><span class="sxs-lookup"><span data-stu-id="fcc61-233">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="fcc61-234">否</span><span class="sxs-lookup"><span data-stu-id="fcc61-234">No</span></span> |
| <span data-ttu-id="fcc61-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="fcc61-235">runtimeVersion</span></span> | <span data-ttu-id="fcc61-236">Hello U-SQL 引擎 toouse 執行階段版本</span><span class="sxs-lookup"><span data-stu-id="fcc61-236">Runtime version of hello U-SQL engine toouse</span></span> | <span data-ttu-id="fcc61-237">否</span><span class="sxs-lookup"><span data-stu-id="fcc61-237">No</span></span> | 
| <span data-ttu-id="fcc61-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="fcc61-238">compilationMode</span></span> | <p><span data-ttu-id="fcc61-239">U-SQL 的編譯模式。</span><span class="sxs-lookup"><span data-stu-id="fcc61-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="fcc61-240">必須是下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="fcc61-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="fcc61-241">**Semantic：**僅執行語意檢查和必要的例行性檢查。</span><span class="sxs-lookup"><span data-stu-id="fcc61-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="fcc61-242">**完整：**執行 hello 完整編譯，包括語法檢查、 最佳化，程式碼產生、 等等。</span><span class="sxs-lookup"><span data-stu-id="fcc61-242">**Full:** Perform hello full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="fcc61-243">**SingleBox:**執行 hello 完整的編譯，TargetType 設定 tooSingleBox。</span><span class="sxs-lookup"><span data-stu-id="fcc61-243">**SingleBox:** Perform hello full compilation, with TargetType setting tooSingleBox.</span></span></li></ul><p><span data-ttu-id="fcc61-244">如果您未指定此屬性的值，hello 伺服器會決定 hello 最佳編譯模式。</span><span class="sxs-lookup"><span data-stu-id="fcc61-244">If you don't specify a value for this property, hello server determines hello optimal compilation mode.</span></span> </p>| <span data-ttu-id="fcc61-245">否</span><span class="sxs-lookup"><span data-stu-id="fcc61-245">No</span></span> | 

<span data-ttu-id="fcc61-246">請參閱[SearchLogProcessing.txt 指令碼定義](#sample-u-sql-script)hello 指令碼定義。</span><span class="sxs-lookup"><span data-stu-id="fcc61-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for hello script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="fcc61-247">建立輸入和輸出資料集</span><span class="sxs-lookup"><span data-stu-id="fcc61-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="fcc61-248">輸入資料集</span><span class="sxs-lookup"><span data-stu-id="fcc61-248">Input dataset</span></span>
<span data-ttu-id="fcc61-249">在此範例中，hello 輸入的資料位於 Azure 資料湖存放區 （SearchLog.tsv 檔案 hello datalake/輸入資料夾中）。</span><span class="sxs-lookup"><span data-stu-id="fcc61-249">In this example, hello input data resides in an Azure Data Lake Store (SearchLog.tsv file in hello datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="fcc61-250">輸出資料集</span><span class="sxs-lookup"><span data-stu-id="fcc61-250">Output dataset</span></span>
<span data-ttu-id="fcc61-251">在此範例中，hello hello U-SQL 指令碼所產生的輸出資料會儲存在 Azure Data Lake Store （datalake/輸出資料夾）。</span><span class="sxs-lookup"><span data-stu-id="fcc61-251">In this example, hello output data produced by hello U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="fcc61-252">Data Lake Store 連結服務範例</span><span class="sxs-lookup"><span data-stu-id="fcc61-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="fcc61-253">以下是 hello 定義 Azure Data Lake Store 連結 hello 輸入/輸出資料集所使用的服務的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="fcc61-253">Here is hello definition of hello sample Azure Data Lake Store linked service used by hello input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="fcc61-254">請參閱[從 Azure 資料湖存放區移動資料 tooand](data-factory-azure-datalake-connector.md) JSON 屬性的說明文章。</span><span class="sxs-lookup"><span data-stu-id="fcc61-254">See [Move data tooand from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="fcc61-255">U-SQL 指令碼範例</span><span class="sxs-lookup"><span data-stu-id="fcc61-255">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="fcc61-256">hello 值 **@in** 和 **@out**  hello U-SQL 指令碼中的參數傳遞以動態方式的 ADF 使用 hello 'parameters' 區段。</span><span class="sxs-lookup"><span data-stu-id="fcc61-256">hello values for **@in** and **@out** parameters in hello U-SQL script are passed dynamically by ADF using hello ‘parameters’ section.</span></span> <span data-ttu-id="fcc61-257">請參閱 hello 管線定義中的 hello 'parameters' 區段。</span><span class="sxs-lookup"><span data-stu-id="fcc61-257">See hello ‘parameters’ section in hello pipeline definition.</span></span>

<span data-ttu-id="fcc61-258">您可以在管線定義中的 hello hello Azure 資料湖分析服務執行的作業以及指定其他屬性，例如 degreeOfParallelism 和優先順序。</span><span class="sxs-lookup"><span data-stu-id="fcc61-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for hello jobs that run on hello Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="fcc61-259">動態參數</span><span class="sxs-lookup"><span data-stu-id="fcc61-259">Dynamic parameters</span></span>
<span data-ttu-id="fcc61-260">往返在 hello 範例管線定義中，參數會指派以硬式編碼值。</span><span class="sxs-lookup"><span data-stu-id="fcc61-260">In hello sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="fcc61-261">相反地，它是可能 toouse 動態參數。</span><span class="sxs-lookup"><span data-stu-id="fcc61-261">It is possible toouse dynamic parameters instead.</span></span> <span data-ttu-id="fcc61-262">例如：</span><span class="sxs-lookup"><span data-stu-id="fcc61-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="fcc61-263">在此情況下，輸入的檔案仍然從挑選 hello /datalake/input 資料夾和 hello /datalake/output 資料夾中產生輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc61-263">In this case, input files are still picked up from hello /datalake/input folder and output files are generated in hello /datalake/output folder.</span></span> <span data-ttu-id="fcc61-264">hello 檔案名稱是動態的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="fcc61-264">hello file names are dynamic based on hello slice start time.</span></span>  

