---
title: "使用 U-SQL 指令碼轉換資料 - Azure | Microsoft Docs"
description: "了解如何在 Azure Data Lake Analytics 計算服務上執行 U-SQL 指令碼來處理或轉換資料。"
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
ms.openlocfilehash: 49a809af92ed1bc6664fbdd3bf1aabf36afb8180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="11205-103">在 Azure Data Lake Analytics 上執行 U-SQL 指令碼來轉換資料</span><span class="sxs-lookup"><span data-stu-id="11205-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="11205-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="11205-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="11205-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="11205-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="11205-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="11205-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="11205-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="11205-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="11205-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="11205-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="11205-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="11205-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="11205-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="11205-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="11205-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="11205-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="11205-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="11205-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="11205-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="11205-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="11205-114">Azure Data Factory 中的「管線」會使用連結的計算服務，來處理連結的儲存體服務中的資料。</span><span class="sxs-lookup"><span data-stu-id="11205-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="11205-115">它包含一系列活動，其中每個活動都會執行特定的處理作業。</span><span class="sxs-lookup"><span data-stu-id="11205-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="11205-116">本文將說明 **Data Lake Analytics U-SQL 活動**，它在 **Azure Data Lake Analytics** 計算連結的服務上執行 **U-SQL** 指令碼。</span><span class="sxs-lookup"><span data-stu-id="11205-116">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="11205-117">使用 Data Lake Analytics「U-SQL 活動」來建立管線之前，請先建立 Azure Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11205-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="11205-118">若要了解 Azure Data Lake Analytics，請參閱 [開始使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="11205-118">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="11205-119">請檢閱 [建置您的第一個管線教學課程](data-factory-build-your-first-pipeline.md) ，以了解建立 Data Factory、連結服務、資料集和管線的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="11205-119">Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="11205-120">您可以搭配「Data Factory 編輯器」、Visual Studio 或 Azure PowerShell 使用 JSON 程式碼片段來建立 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="11205-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="11205-121">支援的驗證類型</span><span class="sxs-lookup"><span data-stu-id="11205-121">Supported authentication types</span></span>
<span data-ttu-id="11205-122">U-SQL 活動支援以下針對 Data Lake Analytics 的驗證類型：</span><span class="sxs-lookup"><span data-stu-id="11205-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="11205-123">服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="11205-123">Service principal authentication</span></span>
* <span data-ttu-id="11205-124">使用者認證 (OAuth) 驗證</span><span class="sxs-lookup"><span data-stu-id="11205-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="11205-125">我們建議您使用服務主體驗證，特別是針對排程的 U-SQL 執行。</span><span class="sxs-lookup"><span data-stu-id="11205-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="11205-126">權杖到期行為會連同使用者認證驗證發生。</span><span class="sxs-lookup"><span data-stu-id="11205-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="11205-127">如需組態詳細資料，請參閱[連結服務屬性](#azure-data-lake-analytics-linked-service)一節。</span><span class="sxs-lookup"><span data-stu-id="11205-127">For configuration details, see the [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="11205-128">Azure Data Lake Analytics 連結服務</span><span class="sxs-lookup"><span data-stu-id="11205-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="11205-129">您需建立 **Azure Data Lake Analytics** 連結服務，來將 Azure Data Lake Analytics 計算服務連結到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="11205-129">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="11205-130">管線中的 Data Lake Analytics U-SQL 活動會參考此連結服務。</span><span class="sxs-lookup"><span data-stu-id="11205-130">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="11205-131">下表提供 JSON 定義中所使用之一般屬性的描述。</span><span class="sxs-lookup"><span data-stu-id="11205-131">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="11205-132">您可以在服務主體與使用者認證驗證之間進一步選擇。</span><span class="sxs-lookup"><span data-stu-id="11205-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="11205-133">屬性</span><span class="sxs-lookup"><span data-stu-id="11205-133">Property</span></span> | <span data-ttu-id="11205-134">說明</span><span class="sxs-lookup"><span data-stu-id="11205-134">Description</span></span> | <span data-ttu-id="11205-135">必要</span><span class="sxs-lookup"><span data-stu-id="11205-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11205-136">**type**</span><span class="sxs-lookup"><span data-stu-id="11205-136">**type**</span></span> |<span data-ttu-id="11205-137">type 屬性應設為： **AzureDataLakeAnalytics**。</span><span class="sxs-lookup"><span data-stu-id="11205-137">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="11205-138">是</span><span class="sxs-lookup"><span data-stu-id="11205-138">Yes</span></span> |
| <span data-ttu-id="11205-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="11205-139">**accountName**</span></span> |<span data-ttu-id="11205-140">Azure Data Lake Analytics 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="11205-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="11205-141">是</span><span class="sxs-lookup"><span data-stu-id="11205-141">Yes</span></span> |
| <span data-ttu-id="11205-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="11205-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="11205-143">Azure Data Lake Analytics URI。</span><span class="sxs-lookup"><span data-stu-id="11205-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="11205-144">否</span><span class="sxs-lookup"><span data-stu-id="11205-144">No</span></span> |
| <span data-ttu-id="11205-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="11205-145">**subscriptionId**</span></span> |<span data-ttu-id="11205-146">Azure 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="11205-146">Azure subscription id</span></span> |<span data-ttu-id="11205-147">否 (如果未指定，便會使用 Data Factory 的訂用帳戶)。</span><span class="sxs-lookup"><span data-stu-id="11205-147">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="11205-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="11205-148">**resourceGroupName**</span></span> |<span data-ttu-id="11205-149">Azure 資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="11205-149">Azure resource group name</span></span> |<span data-ttu-id="11205-150">否 (若未指定，便會使用 Data Factory 的資源群組)。</span><span class="sxs-lookup"><span data-stu-id="11205-150">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="11205-151">服務主體驗證 (建議)</span><span class="sxs-lookup"><span data-stu-id="11205-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="11205-152">若要使用服務主體驗證，請在 Azure Active Directory (Azure AD) 中註冊應用程式實體，並授與其 Data Lake Store 存取權。</span><span class="sxs-lookup"><span data-stu-id="11205-152">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="11205-153">如需詳細的步驟，請參閱[服務對服務驗證](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="11205-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="11205-154">請記下以下的值，您可以使用這些值來定義連結服務：</span><span class="sxs-lookup"><span data-stu-id="11205-154">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="11205-155">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="11205-155">Application ID</span></span>
* <span data-ttu-id="11205-156">應用程式金鑰</span><span class="sxs-lookup"><span data-stu-id="11205-156">Application key</span></span> 
* <span data-ttu-id="11205-157">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="11205-157">Tenant ID</span></span>

<span data-ttu-id="11205-158">指定下列屬性以使用服務主體驗證：</span><span class="sxs-lookup"><span data-stu-id="11205-158">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="11205-159">屬性</span><span class="sxs-lookup"><span data-stu-id="11205-159">Property</span></span> | <span data-ttu-id="11205-160">說明</span><span class="sxs-lookup"><span data-stu-id="11205-160">Description</span></span> | <span data-ttu-id="11205-161">必要</span><span class="sxs-lookup"><span data-stu-id="11205-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="11205-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="11205-162">**servicePrincipalId**</span></span> | <span data-ttu-id="11205-163">指定應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="11205-163">Specify the application's client ID.</span></span> | <span data-ttu-id="11205-164">是</span><span class="sxs-lookup"><span data-stu-id="11205-164">Yes</span></span> |
| <span data-ttu-id="11205-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="11205-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="11205-166">指定應用程式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="11205-166">Specify the application's key.</span></span> | <span data-ttu-id="11205-167">是</span><span class="sxs-lookup"><span data-stu-id="11205-167">Yes</span></span> |
| <span data-ttu-id="11205-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="11205-168">**tenant**</span></span> | <span data-ttu-id="11205-169">指定您的應用程式所在租用戶的資訊 (網域名稱或租用戶識別碼)。</span><span class="sxs-lookup"><span data-stu-id="11205-169">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="11205-170">將滑鼠游標暫留在 Azure 入口網站右上角，即可擷取它。</span><span class="sxs-lookup"><span data-stu-id="11205-170">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="11205-171">是</span><span class="sxs-lookup"><span data-stu-id="11205-171">Yes</span></span> |

<span data-ttu-id="11205-172">**範例：服務主體驗證**</span><span class="sxs-lookup"><span data-stu-id="11205-172">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="11205-173">使用者認證驗證</span><span class="sxs-lookup"><span data-stu-id="11205-173">User credential authentication</span></span>
<span data-ttu-id="11205-174">或者，您也可以藉由指定下列屬性，使用 Data Lake Analytics 的使用者認證驗證：</span><span class="sxs-lookup"><span data-stu-id="11205-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="11205-175">屬性</span><span class="sxs-lookup"><span data-stu-id="11205-175">Property</span></span> | <span data-ttu-id="11205-176">說明</span><span class="sxs-lookup"><span data-stu-id="11205-176">Description</span></span> | <span data-ttu-id="11205-177">必要</span><span class="sxs-lookup"><span data-stu-id="11205-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="11205-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="11205-178">**authorization**</span></span> | <span data-ttu-id="11205-179">按一下「資料處理站編輯器」中的 [授權] 按鈕，然後輸入您的認證，此動作會將自動產生的授權 URL 指派給此屬性。</span><span class="sxs-lookup"><span data-stu-id="11205-179">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="11205-180">是</span><span class="sxs-lookup"><span data-stu-id="11205-180">Yes</span></span> |
| <span data-ttu-id="11205-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="11205-181">**sessionId**</span></span> | <span data-ttu-id="11205-182">OAuth 授權工作階段的 OAuth 工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="11205-182">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="11205-183">每個工作階段識別碼都是唯一的，只能使用一次。</span><span class="sxs-lookup"><span data-stu-id="11205-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="11205-184">當您使用「資料處理站編輯器」時便會自動產生此設定。</span><span class="sxs-lookup"><span data-stu-id="11205-184">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="11205-185">是</span><span class="sxs-lookup"><span data-stu-id="11205-185">Yes</span></span> |

<span data-ttu-id="11205-186">**範例：使用者認證授權**</span><span class="sxs-lookup"><span data-stu-id="11205-186">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="11205-187">權杖到期</span><span class="sxs-lookup"><span data-stu-id="11205-187">Token expiration</span></span>
<span data-ttu-id="11205-188">您使用 [授權] 按鈕所產生的授權碼在一段時間後會到期。</span><span class="sxs-lookup"><span data-stu-id="11205-188">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="11205-189">請參閱下表以了解不同類型的使用者帳戶的到期時間。</span><span class="sxs-lookup"><span data-stu-id="11205-189">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="11205-190">當驗證**權杖到期**時，您可能會看到下列錯誤訊息：認證作業發生錯誤：invalid_grant - AADSTS70002：驗證認證時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="11205-190">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="11205-191">AADSTS70008：提供的存取授權已過期或撤銷。</span><span class="sxs-lookup"><span data-stu-id="11205-191">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="11205-192">追蹤識別碼：d18629e8-af88-43c5-88e3-d8419eb1fca1 相互關連識別碼：fac30a0c-6be6-4e02-8d69-a776d2ffefd7 時間戳記：2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="11205-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="11205-193">使用者類型</span><span class="sxs-lookup"><span data-stu-id="11205-193">User type</span></span> | <span data-ttu-id="11205-194">到期時間</span><span class="sxs-lookup"><span data-stu-id="11205-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="11205-195">不受 Azure Active Directory 管理的使用者帳戶 (@hotmail.com、@live.com 等)</span><span class="sxs-lookup"><span data-stu-id="11205-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="11205-196">12 小時</span><span class="sxs-lookup"><span data-stu-id="11205-196">12 hours</span></span> |
| <span data-ttu-id="11205-197">受 Azure Active Directory (AAD) 管理的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="11205-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="11205-198">最後一次執行配量後的 14 天。</span><span class="sxs-lookup"><span data-stu-id="11205-198">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="11205-199">如果以 OAuth 式連結服務為基礎的配量至少每 14 天執行一次，則為 90 天。</span><span class="sxs-lookup"><span data-stu-id="11205-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="11205-200">如果要避免/解決此錯誤，請在**權杖到期**時使用 [授權] 按鈕重新授權，然後重新部署連結服務。</span><span class="sxs-lookup"><span data-stu-id="11205-200">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="11205-201">您也可以如下使用程式碼，以程式設計方式產生 **sessionId** 和 **authorization** 屬性的值：</span><span class="sxs-lookup"><span data-stu-id="11205-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="11205-202">請參閱 [AzureDataLakeStoreLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)、[AzureDataLakeAnalyticsLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)和 [AuthorizationSessionGetResponse 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx)主題，以取得在程式碼中使用的 Data Factory 類別的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="11205-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="11205-203">請針對 WindowsFormsWebAuthenticationDialog 類別，新增對下列項目的參考：Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll。</span><span class="sxs-lookup"><span data-stu-id="11205-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="11205-204">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="11205-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="11205-205">下列 JSON 片段會定義具有 Data Lake Analytics U-SQL 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="11205-205">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="11205-206">活動定義具有您稍早建立的 Azure Data Lake Analytics 連結服務的參考。</span><span class="sxs-lookup"><span data-stu-id="11205-206">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline to compute events for en-gb locale and date less than 2012/02/19.",
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

<span data-ttu-id="11205-207">下表描述此活動特有的屬性之名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="11205-207">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="11205-208">屬性</span><span class="sxs-lookup"><span data-stu-id="11205-208">Property</span></span> | <span data-ttu-id="11205-209">說明</span><span class="sxs-lookup"><span data-stu-id="11205-209">Description</span></span> | <span data-ttu-id="11205-210">必要</span><span class="sxs-lookup"><span data-stu-id="11205-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="11205-211">類型</span><span class="sxs-lookup"><span data-stu-id="11205-211">type</span></span> |<span data-ttu-id="11205-212">類型屬性必須設為 DataLakeAnalyticsU-SQL 。</span><span class="sxs-lookup"><span data-stu-id="11205-212">The type property must be set to **DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="11205-213">是</span><span class="sxs-lookup"><span data-stu-id="11205-213">Yes</span></span> |
| <span data-ttu-id="11205-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="11205-214">scriptPath</span></span> |<span data-ttu-id="11205-215">包含 U-SQL 指令碼的資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="11205-215">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="11205-216">檔案的名稱有區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="11205-216">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="11205-217">否 (如果您使用指令碼)</span><span class="sxs-lookup"><span data-stu-id="11205-217">No (if you use script)</span></span> |
| <span data-ttu-id="11205-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="11205-218">scriptLinkedService</span></span> |<span data-ttu-id="11205-219">連結服務會連結包含 Data Factory 的指令碼的儲存體</span><span class="sxs-lookup"><span data-stu-id="11205-219">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="11205-220">否 (如果您使用指令碼)</span><span class="sxs-lookup"><span data-stu-id="11205-220">No (if you use script)</span></span> |
| <span data-ttu-id="11205-221">script</span><span class="sxs-lookup"><span data-stu-id="11205-221">script</span></span> |<span data-ttu-id="11205-222">指定內嵌指令碼而不是指定 scriptPath 和 scriptLinkedService。</span><span class="sxs-lookup"><span data-stu-id="11205-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="11205-223">例如： `"script": "CREATE DATABASE test"`。</span><span class="sxs-lookup"><span data-stu-id="11205-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="11205-224">否 (如果您使用 scriptPath 和 scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="11205-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="11205-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="11205-225">degreeOfParallelism</span></span> |<span data-ttu-id="11205-226">同時用來執行作業的節點數目上限。</span><span class="sxs-lookup"><span data-stu-id="11205-226">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="11205-227">否</span><span class="sxs-lookup"><span data-stu-id="11205-227">No</span></span> |
| <span data-ttu-id="11205-228">優先順序</span><span class="sxs-lookup"><span data-stu-id="11205-228">priority</span></span> |<span data-ttu-id="11205-229">判斷應該選取排入佇列的哪些工作首先執行。</span><span class="sxs-lookup"><span data-stu-id="11205-229">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="11205-230">編號愈低，優先順序愈高。</span><span class="sxs-lookup"><span data-stu-id="11205-230">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="11205-231">否</span><span class="sxs-lookup"><span data-stu-id="11205-231">No</span></span> |
| <span data-ttu-id="11205-232">參數</span><span class="sxs-lookup"><span data-stu-id="11205-232">parameters</span></span> |<span data-ttu-id="11205-233">U-SQL 指令碼的參數</span><span class="sxs-lookup"><span data-stu-id="11205-233">Parameters for the U-SQL script</span></span> |<span data-ttu-id="11205-234">否</span><span class="sxs-lookup"><span data-stu-id="11205-234">No</span></span> |
| <span data-ttu-id="11205-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="11205-235">runtimeVersion</span></span> | <span data-ttu-id="11205-236">所要使用之 U-SQL 引擎的執行階段版本</span><span class="sxs-lookup"><span data-stu-id="11205-236">Runtime version of the U-SQL engine to use</span></span> | <span data-ttu-id="11205-237">否</span><span class="sxs-lookup"><span data-stu-id="11205-237">No</span></span> | 
| <span data-ttu-id="11205-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="11205-238">compilationMode</span></span> | <p><span data-ttu-id="11205-239">U-SQL 的編譯模式。</span><span class="sxs-lookup"><span data-stu-id="11205-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="11205-240">必須是下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="11205-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="11205-241">**Semantic：**僅執行語意檢查和必要的例行性檢查。</span><span class="sxs-lookup"><span data-stu-id="11205-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="11205-242">**Full：**執行完整編譯，包括語法檢查、最佳化、程式碼產生等。</span><span class="sxs-lookup"><span data-stu-id="11205-242">**Full:** Perform the full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="11205-243">**SingleBox：**在將 TargetType 設定為 SingleBox 的情況下，執行完整編譯。</span><span class="sxs-lookup"><span data-stu-id="11205-243">**SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span></span></li></ul><p><span data-ttu-id="11205-244">如果您沒有為此屬性指定值，伺服器將會判斷最佳的編譯模式。</span><span class="sxs-lookup"><span data-stu-id="11205-244">If you don't specify a value for this property, the server determines the optimal compilation mode.</span></span> </p>| <span data-ttu-id="11205-245">否</span><span class="sxs-lookup"><span data-stu-id="11205-245">No</span></span> | 

<span data-ttu-id="11205-246">指令碼定義請參閱 [SearchLogProcessing.txt 指令碼定義](#sample-u-sql-script) 。</span><span class="sxs-lookup"><span data-stu-id="11205-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="11205-247">建立輸入和輸出資料集</span><span class="sxs-lookup"><span data-stu-id="11205-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="11205-248">輸入資料集</span><span class="sxs-lookup"><span data-stu-id="11205-248">Input dataset</span></span>
<span data-ttu-id="11205-249">在此範例中，輸入的資料是位於 Azure Data Lake Store (datalake/input 資料夾中的 SearchLog.tsv 檔案)。</span><span class="sxs-lookup"><span data-stu-id="11205-249">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span></span> 

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

### <a name="output-dataset"></a><span data-ttu-id="11205-250">輸出資料集</span><span class="sxs-lookup"><span data-stu-id="11205-250">Output dataset</span></span>
<span data-ttu-id="11205-251">在此範例中，U-SQL 指令碼所產生的輸出資料會儲存在 Azure Data Lake Store (datalake/output 資料夾)。</span><span class="sxs-lookup"><span data-stu-id="11205-251">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

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

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="11205-252">Data Lake Store 連結服務範例</span><span class="sxs-lookup"><span data-stu-id="11205-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="11205-253">以下是輸入/輸出資料集所使用的範例 Azure Data Lake Store 連結服務的定義。</span><span class="sxs-lookup"><span data-stu-id="11205-253">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span></span> 

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

<span data-ttu-id="11205-254">如需 JSON 屬性的描述，請參閱 [將資料移入和移除 Azure Data Lake Store](data-factory-azure-datalake-connector.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="11205-254">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="11205-255">U-SQL 指令碼範例</span><span class="sxs-lookup"><span data-stu-id="11205-255">Sample U-SQL Script</span></span>

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
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="11205-256">ADF 會使用 ‘parameters’ 區段來動態傳遞 U-SQL 指令碼中 **@in** 和 **@out** 參數的值。</span><span class="sxs-lookup"><span data-stu-id="11205-256">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span></span> <span data-ttu-id="11205-257">請參閱管線定義中的 ‘parameters’ 區段。</span><span class="sxs-lookup"><span data-stu-id="11205-257">See the ‘parameters’ section in the pipeline definition.</span></span>

<span data-ttu-id="11205-258">您也可以在管線定義中，針對在 Azure Data Lake Analytics 服務上執行的作業，指定其他屬性 (例如 degreeOfParallelism 和 priority)。</span><span class="sxs-lookup"><span data-stu-id="11205-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="11205-259">動態參數</span><span class="sxs-lookup"><span data-stu-id="11205-259">Dynamic parameters</span></span>
<span data-ttu-id="11205-260">在範例管線定義中，in 和 out 參數都被指派了硬式編碼值。</span><span class="sxs-lookup"><span data-stu-id="11205-260">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="11205-261">您可改為使用動態參數。</span><span class="sxs-lookup"><span data-stu-id="11205-261">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="11205-262">例如：</span><span class="sxs-lookup"><span data-stu-id="11205-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="11205-263">在此例中，系統仍然會從 /datalake/input 資料夾挑選輸入檔，並在 /datalake/output 資料夾中產生輸出檔。</span><span class="sxs-lookup"><span data-stu-id="11205-263">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="11205-264">檔案名稱則是根據配量開始時間動態產生。</span><span class="sxs-lookup"><span data-stu-id="11205-264">The file names are dynamic based on the slice start time.</span></span>  

