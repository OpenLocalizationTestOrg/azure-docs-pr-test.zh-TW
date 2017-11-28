---
title: "從 Azure Data Lake Store 來回複製資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 Azure Data Lake Store 來回複製資料"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 11629fbc83f0554e2097eb4322701654c0bc2028
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="62e03-103">了解如何使用 Data Factory 從 Data Lake Store 來回複製資料</span><span class="sxs-lookup"><span data-stu-id="62e03-103">Copy data to and from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="62e03-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，將資料移進與移出 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="62e03-104">This article explains how to use Copy Activity in Azure Data Factory to move data to and from Azure Data Lake Store.</span></span> <span data-ttu-id="62e03-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文概述使用「複製活動」移動資料。</span><span class="sxs-lookup"><span data-stu-id="62e03-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="62e03-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="62e03-106">Supported scenarios</span></span>
<span data-ttu-id="62e03-107">您可以將資料從 Azure Data Lake Store 複製到下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="62e03-107">You can copy data **from Azure Data Lake Store** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="62e03-108">您可以從下列資料存放區將資料複製到 Azure Data Lake Store：</span><span class="sxs-lookup"><span data-stu-id="62e03-108">You can copy data from the following data stores **to Azure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="62e03-109">先建立 Data Lake Store 帳戶，再使用「複製活動」建立管線。</span><span class="sxs-lookup"><span data-stu-id="62e03-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="62e03-110">如需詳細資訊，請參閱[開始使用 Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="62e03-111">支援的驗證類型</span><span class="sxs-lookup"><span data-stu-id="62e03-111">Supported authentication types</span></span>
<span data-ttu-id="62e03-112">Data Lake Store 連接器支援這些驗證類型：</span><span class="sxs-lookup"><span data-stu-id="62e03-112">The Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="62e03-113">服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="62e03-113">Service principal authentication</span></span>
* <span data-ttu-id="62e03-114">使用者認證 (OAuth) 驗證</span><span class="sxs-lookup"><span data-stu-id="62e03-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="62e03-115">我們建議您使用服務主體驗證，特別是針對排程的資料複本。</span><span class="sxs-lookup"><span data-stu-id="62e03-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="62e03-116">權杖到期行為會連同使用者認證驗證發生。</span><span class="sxs-lookup"><span data-stu-id="62e03-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="62e03-117">如需組態詳細資料，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="62e03-117">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="62e03-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="62e03-118">Get started</span></span>
<span data-ttu-id="62e03-119">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="62e03-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="62e03-120">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="62e03-120">The easiest way to create a pipeline to copy data is to use the **Copy Wizard**.</span></span> <span data-ttu-id="62e03-121">如需使用「複製精靈」建立管線的教學課程，請參閱[教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-121">For a tutorial on creating a pipeline by using the Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="62e03-122">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="62e03-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="62e03-123">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="62e03-124">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="62e03-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="62e03-125">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="62e03-125">Create a **data factory**.</span></span> <span data-ttu-id="62e03-126">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="62e03-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="62e03-127">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="62e03-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="62e03-128">例如，如果您將資料從 Azure Blob 儲存體複製到 Azure Data Lake Store，您會建立兩個連結服務，可將 Azure 儲存體帳戶和 Azure Data Lake Store 連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="62e03-128">For example, if you are copying data from an Azure blob storage to an Azure Data Lake Store, you create two linked services to link your Azure storage account and Azure Data Lake store to your data factory.</span></span> <span data-ttu-id="62e03-129">針對 Azure Data Lake Store 專屬的連結服務屬性，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="62e03-129">For linked service properties that are specific to Azure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="62e03-130">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="62e03-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="62e03-131">在上一個步驟所述的範例中，您可以建立資料集來指定包含輸入資料的 Blob 容器與資料夾。</span><span class="sxs-lookup"><span data-stu-id="62e03-131">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="62e03-132">同時並建立另一個資料集，以指定在 Data Lake Store 中保存從 Blob 儲存體複製之資料的資料夾和檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="62e03-132">And, you create another dataset to specify the folder and file path in the Data Lake store that holds the data copied from the blob storage.</span></span> <span data-ttu-id="62e03-133">如需 Azure Data Lake Store 專屬的資料集屬性，請參閱[資料集屬性](#dataset-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="62e03-133">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="62e03-134">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="62e03-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="62e03-135">在稍早所述的範例中，您使用 BlobSource 作為來源，以及使用 AzureDataLakeStoreSink 作為複製活動的接收器。</span><span class="sxs-lookup"><span data-stu-id="62e03-135">In the example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for the copy activity.</span></span> <span data-ttu-id="62e03-136">同樣地，如果您正從 Azure Data Lake Store 複製到 Azure Blob 儲存體，則會在複製活動中使用 AzureDataLakeStoreSource 與 BlobSink。</span><span class="sxs-lookup"><span data-stu-id="62e03-136">Similarly, if you are copying from Azure Data Lake Store to Azure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in the copy activity.</span></span> <span data-ttu-id="62e03-137">針對 Azure Data Lake Store 專屬的複製活動屬性，請參閱[複製活動屬性](#copy-activity-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="62e03-137">For copy activity properties that are specific to Azure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="62e03-138">如需有關如何使用資料存放區作為來源或接收器的詳細資訊，請按一下上一節中資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="62e03-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="62e03-139">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="62e03-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="62e03-140">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="62e03-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="62e03-141">如需相關範例，其中含有用來將資料複製到 Azure Data Lake Store (或從 Azure Data Lake Store 複製資料) 之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例](#json-examples-for-copying-data-to-and-from-data-lake-store)一節。</span><span class="sxs-lookup"><span data-stu-id="62e03-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="62e03-142">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 Data Lake Store 特定的 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="62e03-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Data Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="62e03-143">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="62e03-143">Linked service properties</span></span>
<span data-ttu-id="62e03-144">已連結的服務會將資料存放區連結到 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="62e03-144">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="62e03-145">您建立類型為 **AzureDataLakeStore** 的連結服務，以將 Data Lake Store 資料連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="62e03-145">You create a linked service of type **AzureDataLakeStore** to link your Data Lake Store data to your data factory.</span></span> <span data-ttu-id="62e03-146">下表提供 Data Lake Store 連結服務專屬的 JSON 元素說明。</span><span class="sxs-lookup"><span data-stu-id="62e03-146">The following table describes JSON elements specific to Data Lake Store linked services.</span></span> <span data-ttu-id="62e03-147">您可以在服務主體與使用者認證驗證之間選擇。</span><span class="sxs-lookup"><span data-stu-id="62e03-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="62e03-148">屬性</span><span class="sxs-lookup"><span data-stu-id="62e03-148">Property</span></span> | <span data-ttu-id="62e03-149">說明</span><span class="sxs-lookup"><span data-stu-id="62e03-149">Description</span></span> | <span data-ttu-id="62e03-150">必要</span><span class="sxs-lookup"><span data-stu-id="62e03-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="62e03-151">**type**</span><span class="sxs-lookup"><span data-stu-id="62e03-151">**type**</span></span> | <span data-ttu-id="62e03-152">類型屬性必須設定為 **AzureDataLakeStore**。</span><span class="sxs-lookup"><span data-stu-id="62e03-152">The type property must be set to **AzureDataLakeStore**.</span></span> | <span data-ttu-id="62e03-153">是</span><span class="sxs-lookup"><span data-stu-id="62e03-153">Yes</span></span> |
| <span data-ttu-id="62e03-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="62e03-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="62e03-155">Azure Data Lake Store 帳戶相關資訊。</span><span class="sxs-lookup"><span data-stu-id="62e03-155">Information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="62e03-156">此資訊會採用下列其中一種格式：`https://[accountname].azuredatalakestore.net/webhdfs/v1` 或 `adl://[accountname].azuredatalakestore.net/`。</span><span class="sxs-lookup"><span data-stu-id="62e03-156">This information takes one of the following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="62e03-157">是</span><span class="sxs-lookup"><span data-stu-id="62e03-157">Yes</span></span> |
| <span data-ttu-id="62e03-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="62e03-158">**subscriptionId**</span></span> | <span data-ttu-id="62e03-159">Data Lake Store 帳戶所屬的 Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="62e03-159">Azure subscription ID to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="62e03-160">接收 (Sink) 的必要項目</span><span class="sxs-lookup"><span data-stu-id="62e03-160">Required for sink</span></span> |
| <span data-ttu-id="62e03-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="62e03-161">**resourceGroupName**</span></span> | <span data-ttu-id="62e03-162">Data Lake Store 帳戶所屬的 Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="62e03-162">Azure resource group name to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="62e03-163">接收 (Sink) 的必要項目</span><span class="sxs-lookup"><span data-stu-id="62e03-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="62e03-164">服務主體驗證 (建議)</span><span class="sxs-lookup"><span data-stu-id="62e03-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="62e03-165">若要使用服務主體驗證，請在 Azure Active Directory (Azure AD) 中註冊應用程式實體，並授與其 Data Lake Store 存取權。</span><span class="sxs-lookup"><span data-stu-id="62e03-165">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="62e03-166">如需詳細的步驟，請參閱[服務對服務驗證](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="62e03-167">請記下以下的值，您可以使用這些值來定義連結服務：</span><span class="sxs-lookup"><span data-stu-id="62e03-167">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="62e03-168">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="62e03-168">Application ID</span></span>
* <span data-ttu-id="62e03-169">應用程式金鑰</span><span class="sxs-lookup"><span data-stu-id="62e03-169">Application key</span></span> 
* <span data-ttu-id="62e03-170">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="62e03-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62e03-171">如果您使用「複製精靈」來撰寫資料管線，請確定您至少將 Data Lake Store 帳戶其存取控制 (識別與存取管理) 中的「讀取者」角色授與服務主體。</span><span class="sxs-lookup"><span data-stu-id="62e03-171">If you are using the Copy Wizard to author data pipelines, make sure that you grant the service principal at least a **Reader** role in access control (identity and access management) for the Data Lake Store account.</span></span> <span data-ttu-id="62e03-172">此外，至少將 Data Lake Store 根目錄 ("/") 及其子系的「讀取+執行」權限授與服務主體。</span><span class="sxs-lookup"><span data-stu-id="62e03-172">Also, grant the service principal at least **Read + Execute** permission to your Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="62e03-173">否則，您可能會看到「提供的認證無效」訊息。</span><span class="sxs-lookup"><span data-stu-id="62e03-173">Otherwise you might see the message "The credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="62e03-174">當您建立或更新 Azure AD 中的服務主體之後，變更可能需要幾分鐘才會生效。</span><span class="sxs-lookup"><span data-stu-id="62e03-174">After you create or update a service principal in Azure AD, it can take a few minutes for the changes to take effect.</span></span> <span data-ttu-id="62e03-175">檢查服務主體和 Data Lake Store 存取控制清單 (ACL) 組態。</span><span class="sxs-lookup"><span data-stu-id="62e03-175">Check the service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="62e03-176">如果您仍然看見「提供的認證無效」訊息，請稍候片刻並再試一次。</span><span class="sxs-lookup"><span data-stu-id="62e03-176">If you still see the message "The credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="62e03-177">指定下列屬性以使用服務主體驗證：</span><span class="sxs-lookup"><span data-stu-id="62e03-177">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="62e03-178">屬性</span><span class="sxs-lookup"><span data-stu-id="62e03-178">Property</span></span> | <span data-ttu-id="62e03-179">說明</span><span class="sxs-lookup"><span data-stu-id="62e03-179">Description</span></span> | <span data-ttu-id="62e03-180">必要</span><span class="sxs-lookup"><span data-stu-id="62e03-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="62e03-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="62e03-181">**servicePrincipalId**</span></span> | <span data-ttu-id="62e03-182">指定應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="62e03-182">Specify the application's client ID.</span></span> | <span data-ttu-id="62e03-183">是</span><span class="sxs-lookup"><span data-stu-id="62e03-183">Yes</span></span> |
| <span data-ttu-id="62e03-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="62e03-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="62e03-185">指定應用程式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="62e03-185">Specify the application's key.</span></span> | <span data-ttu-id="62e03-186">是</span><span class="sxs-lookup"><span data-stu-id="62e03-186">Yes</span></span> |
| <span data-ttu-id="62e03-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="62e03-187">**tenant**</span></span> | <span data-ttu-id="62e03-188">指定您的應用程式所在租用戶的資訊 (網域名稱或租用戶識別碼)。</span><span class="sxs-lookup"><span data-stu-id="62e03-188">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="62e03-189">將滑鼠游標暫留在 Azure 入口網站右上角，即可擷取它。</span><span class="sxs-lookup"><span data-stu-id="62e03-189">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="62e03-190">是</span><span class="sxs-lookup"><span data-stu-id="62e03-190">Yes</span></span> |

<span data-ttu-id="62e03-191">**範例：服務主體驗證**</span><span class="sxs-lookup"><span data-stu-id="62e03-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="62e03-192">使用者認證驗證</span><span class="sxs-lookup"><span data-stu-id="62e03-192">User credential authentication</span></span>
<span data-ttu-id="62e03-193">或者，您也可以藉由指定下列屬性，使用使用者認證驗證從 Data Lake Store 複製，或是複製到 Data Lake Store：</span><span class="sxs-lookup"><span data-stu-id="62e03-193">Alternatively, you can use user credential authentication to copy from or to Data Lake Store by specifying the following properties:</span></span>

| <span data-ttu-id="62e03-194">屬性</span><span class="sxs-lookup"><span data-stu-id="62e03-194">Property</span></span> | <span data-ttu-id="62e03-195">說明</span><span class="sxs-lookup"><span data-stu-id="62e03-195">Description</span></span> | <span data-ttu-id="62e03-196">必要</span><span class="sxs-lookup"><span data-stu-id="62e03-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="62e03-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="62e03-197">**authorization**</span></span> | <span data-ttu-id="62e03-198">按一下「資料處理站編輯器」中的 [授權] 按鈕，然後輸入您的認證，此動作會將自動產生的授權 URL 指派給此屬性。</span><span class="sxs-lookup"><span data-stu-id="62e03-198">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="62e03-199">是</span><span class="sxs-lookup"><span data-stu-id="62e03-199">Yes</span></span> |
| <span data-ttu-id="62e03-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="62e03-200">**sessionId**</span></span> | <span data-ttu-id="62e03-201">OAuth 授權工作階段的 OAuth 工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="62e03-201">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="62e03-202">每個工作階段識別碼都是唯一的，只能使用一次。</span><span class="sxs-lookup"><span data-stu-id="62e03-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="62e03-203">當您使用「資料處理站編輯器」時便會自動產生此設定。</span><span class="sxs-lookup"><span data-stu-id="62e03-203">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="62e03-204">是</span><span class="sxs-lookup"><span data-stu-id="62e03-204">Yes</span></span> |

<span data-ttu-id="62e03-205">**範例：使用者認證授權**</span><span class="sxs-lookup"><span data-stu-id="62e03-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="62e03-206">權杖到期</span><span class="sxs-lookup"><span data-stu-id="62e03-206">Token expiration</span></span>
<span data-ttu-id="62e03-207">您使用 [授權] 按鈕所產生的授權碼在一段時間後會到期。</span><span class="sxs-lookup"><span data-stu-id="62e03-207">The authorization code that you generate by using the **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="62e03-208">下列訊息表示驗證權杖已過期：</span><span class="sxs-lookup"><span data-stu-id="62e03-208">The following message means that the authentication token has expired:</span></span>

<span data-ttu-id="62e03-209">認證作業錯誤：invalid_grant - AADSTS70002：驗證認證時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="62e03-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="62e03-210">AADSTS70008：提供的存取授權已過期或撤銷。</span><span class="sxs-lookup"><span data-stu-id="62e03-210">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="62e03-211">追蹤識別碼：d18629e8-af88-43c5-88e3-d8419eb1fca1 相互關連識別碼：fac30a0c-6be6-4e02-8d69-a776d2ffefd7 時間戳記：2015-12-15 21-09-31Z。</span><span class="sxs-lookup"><span data-stu-id="62e03-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="62e03-212">下表顯示不同類型使用者帳戶的到期時間：</span><span class="sxs-lookup"><span data-stu-id="62e03-212">The following table shows the expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="62e03-213">使用者類型</span><span class="sxs-lookup"><span data-stu-id="62e03-213">User type</span></span> | <span data-ttu-id="62e03-214">到期時間</span><span class="sxs-lookup"><span data-stu-id="62e03-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="62e03-215">「不」受 Azure Active Directory 管理的使用者帳戶 (例如 @hotmail.com 或 @live.com)</span><span class="sxs-lookup"><span data-stu-id="62e03-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="62e03-216">12 小時</span><span class="sxs-lookup"><span data-stu-id="62e03-216">12 hours</span></span> |
| <span data-ttu-id="62e03-217">受 Azure Active Directory 管理的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="62e03-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="62e03-218">最後一個配量執行後的 14 天</span><span class="sxs-lookup"><span data-stu-id="62e03-218">14 days after the last slice run</span></span> <br/><br/><span data-ttu-id="62e03-219">如果以 OAuth 式連結服務為基礎的配量至少每 14 天執行一次，則為 90 天</span><span class="sxs-lookup"><span data-stu-id="62e03-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="62e03-220">如果您在此權杖的到期時間之前變更密碼，權杖會立即到期。</span><span class="sxs-lookup"><span data-stu-id="62e03-220">If you change your password before the token expiration time, the token expires immediately.</span></span> <span data-ttu-id="62e03-221">您將會看到本節稍早所提到的訊息。</span><span class="sxs-lookup"><span data-stu-id="62e03-221">You will see the message mentioned earlier in this section.</span></span>

<span data-ttu-id="62e03-222">當權杖到期時，您可以使用 [授權] 按鈕重新授權帳戶，以重新部署連結服務。</span><span class="sxs-lookup"><span data-stu-id="62e03-222">You can reauthorize the account by using the **Authorize** button when the token expires to redeploy the linked service.</span></span> <span data-ttu-id="62e03-223">您也可以使用下列程式碼，以程式設計方式產生 sessionId  和 authorization 屬性的值：</span><span class="sxs-lookup"><span data-stu-id="62e03-223">You can also generate values for the **sessionId** and **authorization** properties programmatically by using the following code:</span></span>


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
<span data-ttu-id="62e03-224">如需程式碼中所使用 Data Factory 類別的詳細資料，請參閱 [AzureDataLakeStoreLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)、[AzureDataLakeAnalyticsLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)和 [AuthorizationSessionGetResponse 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="62e03-224">For details about the Data Factory classes used in the code, see the [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="62e03-225">新增程式碼中所使用 `WindowsFormsWebAuthenticationDialog` 類別的 `2.9.10826.1824` 版 `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` 參考。</span><span class="sxs-lookup"><span data-stu-id="62e03-225">Add a reference to version `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for the `WindowsFormsWebAuthenticationDialog` class used in the code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="62e03-226">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="62e03-226">Dataset properties</span></span>
<span data-ttu-id="62e03-227">若要指定資料集以代表 Data Lake Store 中的輸入資料，請將資料集的 type 屬性設定成 AzureDataLakeStore。</span><span class="sxs-lookup"><span data-stu-id="62e03-227">To specify a dataset to represent input data in a Data Lake Store, you set the **type** property of the dataset to **AzureDataLakeStore**.</span></span> <span data-ttu-id="62e03-228">請將資料集的 linkedServiceName 屬性設定成 Data Lake Store 連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="62e03-228">Set the **linkedServiceName** property of the dataset to the name of the Data Lake Store linked service.</span></span> <span data-ttu-id="62e03-229">如需定義資料集的 JSON 區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="62e03-229">For a full list of JSON sections and properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="62e03-230">所有資料集類型 (例如 Azure SQL 資料庫、Azure Blob 及 Azure 資料表) 其 JSON 中如結構、可用性及原則等資料集區段都相似。</span><span class="sxs-lookup"><span data-stu-id="62e03-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="62e03-231">每個資料集類型的 typeProperties 區段都不同，並提供如資料存放區中資料位置與格式等相關資訊。</span><span class="sxs-lookup"><span data-stu-id="62e03-231">The **typeProperties** section is different for each type of dataset and provides information such as location and format of the data in the data store.</span></span> 

<span data-ttu-id="62e03-232">類型為 AzureDataLakeStore  的資料集其 typeProperties 區段包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="62e03-232">The **typeProperties** section for a dataset of type **AzureDataLakeStore** contains the following properties:</span></span>

| <span data-ttu-id="62e03-233">屬性</span><span class="sxs-lookup"><span data-stu-id="62e03-233">Property</span></span> | <span data-ttu-id="62e03-234">說明</span><span class="sxs-lookup"><span data-stu-id="62e03-234">Description</span></span> | <span data-ttu-id="62e03-235">必要</span><span class="sxs-lookup"><span data-stu-id="62e03-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="62e03-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="62e03-236">**folderPath**</span></span> |<span data-ttu-id="62e03-237">Data Lake Store 中容器與資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="62e03-237">Path to the container and folder in Data Lake Store.</span></span> |<span data-ttu-id="62e03-238">是</span><span class="sxs-lookup"><span data-stu-id="62e03-238">Yes</span></span> |
| <span data-ttu-id="62e03-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="62e03-239">**fileName**</span></span> |<span data-ttu-id="62e03-240">Azure Data Lake Store 中的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="62e03-240">Name of the file in Azure Data Lake Store.</span></span> <span data-ttu-id="62e03-241">fileName 屬性是選擇性的，而且區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="62e03-241">The **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="62e03-242">如果您指定 fileName，活動 (包括複製) 適用於特定的檔案。</span><span class="sxs-lookup"><span data-stu-id="62e03-242">If you specify **fileName**, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="62e03-243">如果您未指定 fileName，複製會在輸入資料集中包含 folderPath 中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="62e03-243">When **fileName** is not specified, Copy includes all files in **folderPath** in the input dataset.</span></span><br/><br/><span data-ttu-id="62e03-244">當未指定輸出資料集的 fileName，且在活動接收中未指定 preserveHierarchy 時，所產生檔案的名稱格式為 Data._Guid_.txt\`。</span><span class="sxs-lookup"><span data-stu-id="62e03-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the format Data._Guid_.txt\`.</span></span> <span data-ttu-id="62e03-245">例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt。</span><span class="sxs-lookup"><span data-stu-id="62e03-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="62e03-246">否</span><span class="sxs-lookup"><span data-stu-id="62e03-246">No</span></span> |
| <span data-ttu-id="62e03-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="62e03-247">**partitionedBy**</span></span> |<span data-ttu-id="62e03-248">partitionedBy 屬性為選擇性。</span><span class="sxs-lookup"><span data-stu-id="62e03-248">The **partitionedBy** property is optional.</span></span> <span data-ttu-id="62e03-249">您可以用來指定時間序列資料的動態路徑與檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="62e03-249">You can use it to specify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="62e03-250">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="62e03-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="62e03-251">如需詳細資料和範例，請參閱 [partitionedBy 屬性](#using-partitionedby-property)一節。</span><span class="sxs-lookup"><span data-stu-id="62e03-251">For details and examples, see [The partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="62e03-252">否</span><span class="sxs-lookup"><span data-stu-id="62e03-252">No</span></span> |
| <span data-ttu-id="62e03-253">**format**</span><span class="sxs-lookup"><span data-stu-id="62e03-253">**format**</span></span> | <span data-ttu-id="62e03-254">支援下列格式類型：TextFormat、JsonFormat、AvroFormat、OrcFormat 和 ParquetFormat。</span><span class="sxs-lookup"><span data-stu-id="62e03-254">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="62e03-255">將 [format] 下的 [type] 屬性設定為下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="62e03-255">Set the **type** property under **format** to one of these values.</span></span> <span data-ttu-id="62e03-256">如需詳細資訊，請參閱 [Azure Data Factory 支援的檔案與壓縮格式](data-factory-supported-file-and-compression-formats.md)一文中[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[JSON 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[ORC 格式](data-factory-supported-file-and-compression-formats.md#orc-format)及 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)各節。</span><span class="sxs-lookup"><span data-stu-id="62e03-256">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in the [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="62e03-257">如果您想要在以檔案為基礎的存放區之間「依原樣」複製檔案 (二進位複本)，請略過輸入和輸出資料集定義中的 `format` 區段。</span><span class="sxs-lookup"><span data-stu-id="62e03-257">If you want to copy files "as-is" between file-based stores (binary copy), skip the `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="62e03-258">否</span><span class="sxs-lookup"><span data-stu-id="62e03-258">No</span></span> |
| <span data-ttu-id="62e03-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="62e03-259">**compression**</span></span> | <span data-ttu-id="62e03-260">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="62e03-260">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="62e03-261">支援的類型為：GZip、Deflate、BZip2 及 ZipDeflate。</span><span class="sxs-lookup"><span data-stu-id="62e03-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="62e03-262">支援的層級為 **Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="62e03-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="62e03-263">如需詳細資訊，請參閱 [Azure Data Factory 支援的檔案與壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="62e03-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="62e03-264">否</span><span class="sxs-lookup"><span data-stu-id="62e03-264">No</span></span> |

### <a name="the-partitionedby-property"></a><span data-ttu-id="62e03-265">partitionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="62e03-265">The partitionedBy property</span></span>
<span data-ttu-id="62e03-266">您可以使用 partitionedBy 屬性、Data Factory 函式及系統變數，來指定時間序列資料的動態 folderPath 和 fileName 屬性。</span><span class="sxs-lookup"><span data-stu-id="62e03-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with the **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="62e03-267">如需詳細資料，請參閱 [Azure Data Factory - 函式與系統變數](data-factory-functions-variables.md)一文。</span><span class="sxs-lookup"><span data-stu-id="62e03-267">For details, see the [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="62e03-268">在下列範例中，`{Slice}` 會取代成 Data Factory 系統變數 `SliceStart` 的值，並採用指定的格式 (`yyyyMMddHH`)。</span><span class="sxs-lookup"><span data-stu-id="62e03-268">In the following example, `{Slice}` is replaced with the value of the Data Factory system variable `SliceStart` in the format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="62e03-269">`SliceStart` 名稱是指配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="62e03-269">The name `SliceStart` refers to the start time of the slice.</span></span> <span data-ttu-id="62e03-270">每個配量的 `folderPath` 屬性皆不同，如 `wikidatagateway/wikisampledataout/2014100103` 或 `wikidatagateway/wikisampledataout/2014100104`。</span><span class="sxs-lookup"><span data-stu-id="62e03-270">The `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="62e03-271">在下列範例中，會將 `SliceStart` 的年、月、日和時間擷取至由 `folderPath` 與 `fileName` 屬性使用的個別變數：</span><span class="sxs-lookup"><span data-stu-id="62e03-271">In the following example, the year, month, day, and time of `SliceStart` are extracted into separate variables that are used by the `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="62e03-272">如需時間序列資料集、排程及配量的詳細資料，請參閱 [Azure Data Factory 中的資料集](data-factory-create-datasets.md)與 [Data Factory 排程與執行](data-factory-scheduling-and-execution.md)文章。</span><span class="sxs-lookup"><span data-stu-id="62e03-272">For more details on time-series datasets, scheduling, and slices, see the [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="62e03-273">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="62e03-273">Copy activity properties</span></span>
<span data-ttu-id="62e03-274">如需定義活動的可用區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="62e03-274">For a full list of sections and properties available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="62e03-275">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="62e03-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="62e03-276">活動之 [typeProperties] 區段中的可用屬性，會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="62e03-276">The properties available in the **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="62e03-277">就複製活動而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="62e03-277">For a copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="62e03-278">AzureDataLakeStoreSource 支援 [typeProperties] 區段中的下列屬性：</span><span class="sxs-lookup"><span data-stu-id="62e03-278">**AzureDataLakeStoreSource** supports the following property in the **typeProperties** section:</span></span>

| <span data-ttu-id="62e03-279">屬性</span><span class="sxs-lookup"><span data-stu-id="62e03-279">Property</span></span> | <span data-ttu-id="62e03-280">說明</span><span class="sxs-lookup"><span data-stu-id="62e03-280">Description</span></span> | <span data-ttu-id="62e03-281">允許的值</span><span class="sxs-lookup"><span data-stu-id="62e03-281">Allowed values</span></span> | <span data-ttu-id="62e03-282">必要</span><span class="sxs-lookup"><span data-stu-id="62e03-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62e03-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="62e03-283">**recursive**</span></span> |<span data-ttu-id="62e03-284">指出是否從子資料夾、或只有從指定的資料夾，以遞迴方式讀取資料。</span><span class="sxs-lookup"><span data-stu-id="62e03-284">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="62e03-285">True (預設值)、False</span><span class="sxs-lookup"><span data-stu-id="62e03-285">True (default value), False</span></span> |<span data-ttu-id="62e03-286">否</span><span class="sxs-lookup"><span data-stu-id="62e03-286">No</span></span> |


<span data-ttu-id="62e03-287">AzureDataLakeStoreSink 支援 [typeProperties] 區段中的下列屬性：</span><span class="sxs-lookup"><span data-stu-id="62e03-287">**AzureDataLakeStoreSink** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="62e03-288">屬性</span><span class="sxs-lookup"><span data-stu-id="62e03-288">Property</span></span> | <span data-ttu-id="62e03-289">說明</span><span class="sxs-lookup"><span data-stu-id="62e03-289">Description</span></span> | <span data-ttu-id="62e03-290">允許的值</span><span class="sxs-lookup"><span data-stu-id="62e03-290">Allowed values</span></span> | <span data-ttu-id="62e03-291">必要</span><span class="sxs-lookup"><span data-stu-id="62e03-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62e03-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="62e03-292">**copyBehavior**</span></span> |<span data-ttu-id="62e03-293">指定複製行為。</span><span class="sxs-lookup"><span data-stu-id="62e03-293">Specifies the copy behavior.</span></span> |<span data-ttu-id="62e03-294"><b>PreserveHierarchy</b>：保留目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="62e03-294"><b>PreserveHierarchy</b>: Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="62e03-295">來源檔案到來源資料夾的相對路徑，與目標檔案到目標資料夾的相對路徑相同。</span><span class="sxs-lookup"><span data-stu-id="62e03-295">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="62e03-296"><b>FlattenHierarchy</b>：來源資料夾的中所有檔案都會建立在目標資料夾的第一層中。</span><span class="sxs-lookup"><span data-stu-id="62e03-296"><b>FlattenHierarchy</b>: All files from the source folder are created in the first level of the target folder.</span></span> <span data-ttu-id="62e03-297">建立的目標檔案會具有自動產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="62e03-297">The target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="62e03-298"><b>MergeFiles</b>：將來源資料夾的所有檔案合併為一個檔案。</span><span class="sxs-lookup"><span data-stu-id="62e03-298"><b>MergeFiles</b>: Merges all files from the source folder to one file.</span></span> <span data-ttu-id="62e03-299">如果有指定檔案或 Blob 名稱，合併檔案的名稱會是指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="62e03-299">If the file or blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="62e03-300">否則，會自動產生檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="62e03-300">Otherwise, the file name is autogenerated.</span></span> |<span data-ttu-id="62e03-301">否</span><span class="sxs-lookup"><span data-stu-id="62e03-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="62e03-302">遞迴和 copyBehavior 範例</span><span class="sxs-lookup"><span data-stu-id="62e03-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="62e03-303">本節說明遞迴和 copyBehavior 值在不同組合的情況下，複製作業所產生的行為。</span><span class="sxs-lookup"><span data-stu-id="62e03-303">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="62e03-304">遞迴</span><span class="sxs-lookup"><span data-stu-id="62e03-304">recursive</span></span> | <span data-ttu-id="62e03-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="62e03-305">copyBehavior</span></span> | <span data-ttu-id="62e03-306">產生的行為</span><span class="sxs-lookup"><span data-stu-id="62e03-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62e03-307">true</span><span class="sxs-lookup"><span data-stu-id="62e03-307">true</span></span> |<span data-ttu-id="62e03-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="62e03-308">preserveHierarchy</span></span> |<span data-ttu-id="62e03-309">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="62e03-309">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="62e03-310">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-310">Folder1</span></span><br/><span data-ttu-id="62e03-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="62e03-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="62e03-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="62e03-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="62e03-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="62e03-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="62e03-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="62e03-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="62e03-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="62e03-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="62e03-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="62e03-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="62e03-317">會以與來源相同的結構，建立目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-317">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="62e03-318">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-318">Folder1</span></span><br/><span data-ttu-id="62e03-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="62e03-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="62e03-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="62e03-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="62e03-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="62e03-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="62e03-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="62e03-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="62e03-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="62e03-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="62e03-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="62e03-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="62e03-325">true</span><span class="sxs-lookup"><span data-stu-id="62e03-325">true</span></span> |<span data-ttu-id="62e03-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="62e03-326">flattenHierarchy</span></span> |<span data-ttu-id="62e03-327">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="62e03-327">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="62e03-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-328">Folder1</span></span><br/><span data-ttu-id="62e03-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="62e03-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="62e03-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="62e03-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="62e03-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="62e03-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="62e03-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="62e03-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="62e03-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="62e03-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="62e03-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="62e03-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="62e03-335">會以下列結構建立目標資料夾 1：</span><span class="sxs-lookup"><span data-stu-id="62e03-335">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="62e03-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-336">Folder1</span></span><br/><span data-ttu-id="62e03-337">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="62e03-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="62e03-338">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="62e03-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="62e03-339">&nbsp;&nbsp;&nbsp;&nbsp;File3 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="62e03-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="62e03-340">&nbsp;&nbsp;&nbsp;&nbsp;File4 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="62e03-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="62e03-341">&nbsp;&nbsp;&nbsp;&nbsp;File5 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="62e03-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="62e03-342">true</span><span class="sxs-lookup"><span data-stu-id="62e03-342">true</span></span> |<span data-ttu-id="62e03-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="62e03-343">mergeFiles</span></span> |<span data-ttu-id="62e03-344">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="62e03-344">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="62e03-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-345">Folder1</span></span><br/><span data-ttu-id="62e03-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="62e03-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="62e03-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="62e03-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="62e03-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="62e03-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="62e03-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="62e03-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="62e03-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="62e03-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="62e03-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="62e03-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="62e03-352">會以下列結構建立目標資料夾 1：</span><span class="sxs-lookup"><span data-stu-id="62e03-352">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="62e03-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-353">Folder1</span></span><br/><span data-ttu-id="62e03-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 的內容會合併成一個檔案，並有自動產生的檔案名稱</span><span class="sxs-lookup"><span data-stu-id="62e03-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="62e03-355">false</span><span class="sxs-lookup"><span data-stu-id="62e03-355">false</span></span> |<span data-ttu-id="62e03-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="62e03-356">preserveHierarchy</span></span> |<span data-ttu-id="62e03-357">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="62e03-357">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="62e03-358">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-358">Folder1</span></span><br/><span data-ttu-id="62e03-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="62e03-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="62e03-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="62e03-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="62e03-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="62e03-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="62e03-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="62e03-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="62e03-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="62e03-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="62e03-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="62e03-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="62e03-365">會以下列結構建立目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-365">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="62e03-366">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-366">Folder1</span></span><br/><span data-ttu-id="62e03-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="62e03-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="62e03-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="62e03-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="62e03-369">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="62e03-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="62e03-370">false</span><span class="sxs-lookup"><span data-stu-id="62e03-370">false</span></span> |<span data-ttu-id="62e03-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="62e03-371">flattenHierarchy</span></span> |<span data-ttu-id="62e03-372">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="62e03-372">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="62e03-373">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-373">Folder1</span></span><br/><span data-ttu-id="62e03-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="62e03-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="62e03-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="62e03-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="62e03-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="62e03-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="62e03-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="62e03-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="62e03-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="62e03-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="62e03-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="62e03-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="62e03-380">會以下列結構建立目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-380">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="62e03-381">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-381">Folder1</span></span><br/><span data-ttu-id="62e03-382">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="62e03-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="62e03-383">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="62e03-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="62e03-384">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="62e03-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="62e03-385">false</span><span class="sxs-lookup"><span data-stu-id="62e03-385">false</span></span> |<span data-ttu-id="62e03-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="62e03-386">mergeFiles</span></span> |<span data-ttu-id="62e03-387">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="62e03-387">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="62e03-388">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-388">Folder1</span></span><br/><span data-ttu-id="62e03-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="62e03-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="62e03-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="62e03-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="62e03-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="62e03-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="62e03-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="62e03-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="62e03-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="62e03-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="62e03-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="62e03-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="62e03-395">會以下列結構建立目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-395">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="62e03-396">Folder1</span><span class="sxs-lookup"><span data-stu-id="62e03-396">Folder1</span></span><br/><span data-ttu-id="62e03-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 的內容會合併成一個檔案，並有自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="62e03-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="62e03-398">File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="62e03-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="62e03-399">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="62e03-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="62e03-400">支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="62e03-400">Supported file and compression formats</span></span>
<span data-ttu-id="62e03-401">如需詳細資料，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)一文。</span><span class="sxs-lookup"><span data-stu-id="62e03-401">For details, see the [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-data-lake-store"></a><span data-ttu-id="62e03-402">從 Data Lake Store 來回複製資料的 JSON 範例</span><span class="sxs-lookup"><span data-stu-id="62e03-402">JSON examples for copying data to and from Data Lake Store</span></span>
<span data-ttu-id="62e03-403">下列範例提供範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="62e03-403">The following examples provide sample JSON definitions.</span></span> <span data-ttu-id="62e03-404">您可以使用這些範例定義，透過使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線。</span><span class="sxs-lookup"><span data-stu-id="62e03-404">You can use these sample definitions to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="62e03-405">這些範例會示範如何從 Data Lake Store 與 Azure Blob 儲存體來回複製資料。</span><span class="sxs-lookup"><span data-stu-id="62e03-405">The examples show how to copy data to and from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="62e03-406">不過，您可以將資料從任何來源_直接_複製到任何支援的接收器。</span><span class="sxs-lookup"><span data-stu-id="62e03-406">However, data can be copied _directly_ from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="62e03-407">如需詳細資訊，請參閱[使用複製活動來移動資料](data-factory-data-movement-activities.md)中的＜支援的資料存放區和格式＞一節。</span><span class="sxs-lookup"><span data-stu-id="62e03-407">For more information, see the section "Supported data stores and formats" in the [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-to-azure-data-lake-store"></a><span data-ttu-id="62e03-408">範例：將資料從 Azure Blob 儲存體複製到 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="62e03-408">Example: Copy data from Azure Blob Storage to Azure Data Lake Store</span></span>
<span data-ttu-id="62e03-409">本節中的範例程式碼顯示︰</span><span class="sxs-lookup"><span data-stu-id="62e03-409">The example code in this section shows:</span></span>

* <span data-ttu-id="62e03-410">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="62e03-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="62e03-411">[AzureDataLakeStore](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="62e03-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="62e03-412">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="62e03-413">[AzureDataLakeStore](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="62e03-414">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [AzureDataLakeStoreSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="62e03-415">此範例示範如何每小時將時間序列資料從 Azure Blob 儲存體複製到 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="62e03-415">The examples show how time-series data from Azure Blob Storage is copied to Data Lake Store every hour.</span></span> 

<span data-ttu-id="62e03-416">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="62e03-416">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="62e03-417">**Azure Data Lake Store 已連結的服務**</span><span class="sxs-lookup"><span data-stu-id="62e03-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="62e03-418">如需組態詳細資料，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="62e03-418">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="62e03-419">**Azure Blob 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="62e03-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="62e03-420">在下列範例中，每小時 (`"frequency": "Hour", "interval": 1`) 會從新的 Blob 中挑選資料。</span><span class="sxs-lookup"><span data-stu-id="62e03-420">In the following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="62e03-421">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="62e03-421">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="62e03-422">資料夾路徑會使用開始時間的年、月和日部分。</span><span class="sxs-lookup"><span data-stu-id="62e03-422">The folder path uses the year, month, and day portion of the start time.</span></span> <span data-ttu-id="62e03-423">檔案名稱會使用開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="62e03-423">The file name uses the hour portion of the start time.</span></span> <span data-ttu-id="62e03-424">`"external": true` 設定會通知 Data Factory 服務：這是資料處理站外部的資料表，且不是由資料處理站中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="62e03-424">The `"external": true` setting informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="62e03-425">**Azure Data Lake Store 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="62e03-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="62e03-426">下列範例會將資料複製到 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="62e03-426">The following example copies data to Data Lake Store.</span></span> <span data-ttu-id="62e03-427">每個小時會將新資料複製到 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="62e03-427">New data is copied to Data Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="62e03-428">**具有 Blob 來源和 Data Lake Store 接收器的管線中的複製活動**</span><span class="sxs-lookup"><span data-stu-id="62e03-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="62e03-429">在下列範例中，管線包含複製活動，該活動已設定為使用輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="62e03-429">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="62e03-430">複製活動排程為每小時執行一次。</span><span class="sxs-lookup"><span data-stu-id="62e03-430">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="62e03-431">在管線 JSON 定義中，`source` 類型設為 `BlobSource`，`sink` 類型設為 `AzureDataLakeStoreSink`。</span><span class="sxs-lookup"><span data-stu-id="62e03-431">In the pipeline JSON definition, the `source` type is set to `BlobSource`, and the `sink` type is set to `AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
        ]
    }
}
```

### <a name="example-copy-data-from-azure-data-lake-store-to-an-azure-blob"></a><span data-ttu-id="62e03-432">範例：將資料從 Azure Data Lake Store 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="62e03-432">Example: Copy data from Azure Data Lake Store to an Azure blob</span></span>
<span data-ttu-id="62e03-433">本節中的範例程式碼顯示︰</span><span class="sxs-lookup"><span data-stu-id="62e03-433">The example code in this section shows:</span></span>

* <span data-ttu-id="62e03-434">[AzureDataLakeStore](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="62e03-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="62e03-435">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="62e03-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="62e03-436">[AzureDataLakeStore](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="62e03-437">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="62e03-438">具有使用 [AzureDataLakeStoreSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="62e03-439">該程式碼每小時會將時間序列資料從 Data Lake Store 複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="62e03-439">The code copies time-series data from Data Lake Store to an Azure blob every hour.</span></span> 

<span data-ttu-id="62e03-440">**Azure Data Lake Store 已連結的服務**</span><span class="sxs-lookup"><span data-stu-id="62e03-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="62e03-441">如需組態詳細資料，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="62e03-441">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="62e03-442">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="62e03-442">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="62e03-443">**Azure Data Lake 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="62e03-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="62e03-444">在此範例中，將 `"external"` 設定為 `true` 會通知 Data Factory 服務：這是資料處理站外部的資料表，而不是由資料處理站中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="62e03-444">In this example, setting `"external"` to `true` informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
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
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
        "policy": {
              "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
              }
        }
      }
}
```
<span data-ttu-id="62e03-445">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="62e03-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="62e03-446">在下列範例中，每小時 (`"frequency": "Hour", "interval": 1`) 會將資料寫入新的 Blob。</span><span class="sxs-lookup"><span data-stu-id="62e03-446">In the following example, data is written to a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="62e03-447">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="62e03-447">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="62e03-448">此資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="62e03-448">The folder path uses the year, month, day, and hours portion of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="62e03-449">**具有 Azure Data Lake Store 來源和 Blob 接收器的管線中的複製活動**</span><span class="sxs-lookup"><span data-stu-id="62e03-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="62e03-450">在下列範例中，管線包含複製活動，該活動已設定為使用輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="62e03-450">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="62e03-451">複製活動排程為每小時執行一次。</span><span class="sxs-lookup"><span data-stu-id="62e03-451">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="62e03-452">在管線 JSON 定義中，`source` 類型設為 `AzureDataLakeStoreSource`，`sink` 類型設為 `BlobSink`。</span><span class="sxs-lookup"><span data-stu-id="62e03-452">In the pipeline JSON definition, the `source` type is set to `AzureDataLakeStoreSource`, and the `sink` type is set to `BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

<span data-ttu-id="62e03-453">在複製活動定義中，您也可以將來源資料集的資料行對應至接收資料集中的資料行。</span><span class="sxs-lookup"><span data-stu-id="62e03-453">In the copy activity definition, you can also map columns from the source dataset to columns in the sink dataset.</span></span> <span data-ttu-id="62e03-454">如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="62e03-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="62e03-455">效能和微調</span><span class="sxs-lookup"><span data-stu-id="62e03-455">Performance and tuning</span></span>
<span data-ttu-id="62e03-456">若要了解影響「複製活動」效能的因素，以及最佳化的方法，請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文。</span><span class="sxs-lookup"><span data-stu-id="62e03-456">To learn about the factors that affect Copy Activity performance and how to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
