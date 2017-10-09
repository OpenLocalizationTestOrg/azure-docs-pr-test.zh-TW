---
title: "從 Azure Data Lake Store aaaCopy 資料 tooand |Microsoft 文件"
description: "深入了解如何從資料湖存放區使用 Azure Data Factory 的 toocopy 資料 tooand"
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
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="db707-103">複製資料湖存放區中的資料 tooand，使用 Data Factory</span><span class="sxs-lookup"><span data-stu-id="db707-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="db707-104">這篇文章說明如何在 Azure 資料湖存放區從 Azure Data Factory toomove 資料 tooand toouse 複製活動。</span><span class="sxs-lookup"><span data-stu-id="db707-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="db707-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)發行項的資料移動，複製活動的概觀。</span><span class="sxs-lookup"><span data-stu-id="db707-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="db707-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="db707-106">Supported scenarios</span></span>
<span data-ttu-id="db707-107">您可以將資料複製**從 Azure Data Lake Store** toohello 下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="db707-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="db707-108">您可以將資料複製下列資料存放區的 hello **tooAzure Data Lake Store**:</span><span class="sxs-lookup"><span data-stu-id="db707-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="db707-109">先建立 Data Lake Store 帳戶，再使用「複製活動」建立管線。</span><span class="sxs-lookup"><span data-stu-id="db707-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="db707-110">如需詳細資訊，請參閱[開始使用 Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="db707-111">支援的驗證類型</span><span class="sxs-lookup"><span data-stu-id="db707-111">Supported authentication types</span></span>
<span data-ttu-id="db707-112">hello Data Lake Store 連接器支援這些驗證類型：</span><span class="sxs-lookup"><span data-stu-id="db707-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="db707-113">服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="db707-113">Service principal authentication</span></span>
* <span data-ttu-id="db707-114">使用者認證 (OAuth) 驗證</span><span class="sxs-lookup"><span data-stu-id="db707-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="db707-115">我們建議您使用服務主體驗證，特別是針對排程的資料複本。</span><span class="sxs-lookup"><span data-stu-id="db707-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="db707-116">權杖到期行為會連同使用者認證驗證發生。</span><span class="sxs-lookup"><span data-stu-id="db707-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="db707-117">設定詳細資料，請參閱 hello[連結服務屬性](#linked-service-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="db707-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="db707-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="db707-118">Get started</span></span>
<span data-ttu-id="db707-119">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="db707-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="db707-120">最簡單方式 toocreate hello 管線 toocopy 資料為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="db707-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="db707-121">如需使用 hello 複製精靈建立管線的教學課程，請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="db707-122">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="db707-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="db707-123">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="db707-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="db707-124">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="db707-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="db707-125">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="db707-125">Create a **data factory**.</span></span> <span data-ttu-id="db707-126">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="db707-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="db707-127">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="db707-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="db707-128">例如，如果您要從 Azure blob 儲存體 tooan Azure 資料湖存放區來複製資料，您建立兩個連結的服務 toolink 您的 Azure 儲存體帳戶和 Azure 資料湖存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="db707-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="db707-129">連結的服務是特定 tooAzure 資料湖存放區的內容，請參閱[連結服務屬性](#linked-service-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="db707-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="db707-130">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="db707-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="db707-131">在 hello hello 最後一個步驟中所述的範例中，您可以建立資料集 toospecify hello blob 容器和包含 hello 輸入的資料的資料夾。</span><span class="sxs-lookup"><span data-stu-id="db707-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="db707-132">而且，您保存 hello 資料從 hello blob 儲存體複製 hello 資料湖存放區中建立另一個資料集 toospecify hello 資料夾和檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="db707-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="db707-133">資料集是特定 tooAzure 資料湖存放區的屬性，請參閱[資料集屬性](#dataset-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="db707-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="db707-134">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="db707-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="db707-135">在先前所述 hello 範例中，您使用 BlobSource 作為來源和 AzureDataLakeStoreSink 做為接收器 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="db707-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="db707-136">同樣地，如果您要從 Azure Data Lake Store tooAzure Blob 儲存體複製，則使用 AzureDataLakeStoreSource 和 BlobSink 的 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="db707-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="db707-137">特定 tooAzure 資料湖存放區複製活動內容，請參閱[複製活動屬性](#copy-activity-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="db707-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="db707-138">如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。</span><span class="sxs-lookup"><span data-stu-id="db707-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="db707-139">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="db707-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="db707-140">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="db707-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="db707-141">如需使用的 toocopy 資料至 azure 或從 Azure Data Lake Store 的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-data-lake-store)本文一節。</span><span class="sxs-lookup"><span data-stu-id="db707-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="db707-142">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooData Lake Store 的 JSON 屬性的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="db707-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="db707-143">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="db707-143">Linked service properties</span></span>
<span data-ttu-id="db707-144">連結的服務連結資料儲存區 tooa data factory。</span><span class="sxs-lookup"><span data-stu-id="db707-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="db707-145">您建立連結的服務型別的**AzureDataLakeStore** toolink 您 Data Lake Store 資料 tooyour 的 data factory。</span><span class="sxs-lookup"><span data-stu-id="db707-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="db707-146">hello 下表描述的 JSON 元素特定 tooData Lake Store 連結服務。</span><span class="sxs-lookup"><span data-stu-id="db707-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="db707-147">您可以在服務主體與使用者認證驗證之間選擇。</span><span class="sxs-lookup"><span data-stu-id="db707-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="db707-148">屬性</span><span class="sxs-lookup"><span data-stu-id="db707-148">Property</span></span> | <span data-ttu-id="db707-149">說明</span><span class="sxs-lookup"><span data-stu-id="db707-149">Description</span></span> | <span data-ttu-id="db707-150">必要</span><span class="sxs-lookup"><span data-stu-id="db707-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="db707-151">**type**</span><span class="sxs-lookup"><span data-stu-id="db707-151">**type**</span></span> | <span data-ttu-id="db707-152">hello type 屬性必須設定得**AzureDataLakeStore**。</span><span class="sxs-lookup"><span data-stu-id="db707-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="db707-153">是</span><span class="sxs-lookup"><span data-stu-id="db707-153">Yes</span></span> |
| <span data-ttu-id="db707-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="db707-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="db707-155">Hello Azure Data Lake Store 帳戶的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="db707-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="db707-156">這項資訊會使用其中一個 hello 下列格式：`https://[accountname].azuredatalakestore.net/webhdfs/v1`或`adl://[accountname].azuredatalakestore.net/`。</span><span class="sxs-lookup"><span data-stu-id="db707-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="db707-157">是</span><span class="sxs-lookup"><span data-stu-id="db707-157">Yes</span></span> |
| <span data-ttu-id="db707-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="db707-158">**subscriptionId**</span></span> | <span data-ttu-id="db707-159">所屬的 azure 訂用帳戶 ID toowhich hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="db707-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="db707-160">接收 (Sink) 的必要項目</span><span class="sxs-lookup"><span data-stu-id="db707-160">Required for sink</span></span> |
| <span data-ttu-id="db707-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="db707-161">**resourceGroupName**</span></span> | <span data-ttu-id="db707-162">所屬的 azure 資源群組名稱 toowhich hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="db707-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="db707-163">接收 (Sink) 的必要項目</span><span class="sxs-lookup"><span data-stu-id="db707-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="db707-164">服務主體驗證 (建議)</span><span class="sxs-lookup"><span data-stu-id="db707-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="db707-165">服務主體驗證 toouse，註冊在 Azure Active Directory (Azure AD) 和授與它 hello 應用程式的實體存取 tooData 湖存放區。</span><span class="sxs-lookup"><span data-stu-id="db707-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="db707-166">如需詳細的步驟，請參閱[服務對服務驗證](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="db707-167">請記下的下列值，您使用的 hello toodefine hello 連結服務：</span><span class="sxs-lookup"><span data-stu-id="db707-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="db707-168">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="db707-168">Application ID</span></span>
* <span data-ttu-id="db707-169">應用程式金鑰</span><span class="sxs-lookup"><span data-stu-id="db707-169">Application key</span></span> 
* <span data-ttu-id="db707-170">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="db707-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db707-171">如果您使用 hello 複製精靈 tooauthor 資料管線，請確定您授與 hello 服務主體至少**讀取器**hello Data Lake Store 帳戶的存取控制 （身分識別和存取管理） 中的角色。</span><span class="sxs-lookup"><span data-stu-id="db707-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="db707-172">此外，至少授與 hello 服務主體**讀取 + Execute**權限 tooyour Data Lake Store 根 （"/"） 和其子系。</span><span class="sxs-lookup"><span data-stu-id="db707-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="db707-173">否則，您可能會看到 hello 訊息"hello 提供的認證無效。"</span><span class="sxs-lookup"><span data-stu-id="db707-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="db707-174">您建立或更新 Azure AD 中的服務主體之後，可能需要幾分鐘，讓 hello 變更 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="db707-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="db707-175">請檢查 hello 服務主體以及資料湖存放區的存取控制清單 (ACL) 設定。</span><span class="sxs-lookup"><span data-stu-id="db707-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="db707-176">如果您仍然看到 hello 訊息"提供的認證不正確的 hello"，請稍待片刻，然後再試。</span><span class="sxs-lookup"><span data-stu-id="db707-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="db707-177">您可以使用服務主體的驗證方法是指定 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="db707-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="db707-178">屬性</span><span class="sxs-lookup"><span data-stu-id="db707-178">Property</span></span> | <span data-ttu-id="db707-179">說明</span><span class="sxs-lookup"><span data-stu-id="db707-179">Description</span></span> | <span data-ttu-id="db707-180">必要</span><span class="sxs-lookup"><span data-stu-id="db707-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="db707-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="db707-181">**servicePrincipalId**</span></span> | <span data-ttu-id="db707-182">指定 hello 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="db707-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="db707-183">是</span><span class="sxs-lookup"><span data-stu-id="db707-183">Yes</span></span> |
| <span data-ttu-id="db707-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="db707-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="db707-185">指定 hello 應用程式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="db707-185">Specify hello application's key.</span></span> | <span data-ttu-id="db707-186">是</span><span class="sxs-lookup"><span data-stu-id="db707-186">Yes</span></span> |
| <span data-ttu-id="db707-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="db707-187">**tenant**</span></span> | <span data-ttu-id="db707-188">指定在您的應用程式所在的 hello 租用戶資訊 (網域名稱或租用戶 ID)。</span><span class="sxs-lookup"><span data-stu-id="db707-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="db707-189">您可以透過暫留在 hello 右上角的 hello Azure 入口網站中的 hello 滑鼠擷取它。</span><span class="sxs-lookup"><span data-stu-id="db707-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="db707-190">是</span><span class="sxs-lookup"><span data-stu-id="db707-190">Yes</span></span> |

<span data-ttu-id="db707-191">**範例：服務主體驗證**</span><span class="sxs-lookup"><span data-stu-id="db707-191">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="db707-192">使用者認證驗證</span><span class="sxs-lookup"><span data-stu-id="db707-192">User credential authentication</span></span>
<span data-ttu-id="db707-193">或者，您可以使用從使用者認證驗證 toocopy 或 tooData 湖存放區，藉由指定下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="db707-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="db707-194">屬性</span><span class="sxs-lookup"><span data-stu-id="db707-194">Property</span></span> | <span data-ttu-id="db707-195">說明</span><span class="sxs-lookup"><span data-stu-id="db707-195">Description</span></span> | <span data-ttu-id="db707-196">必要</span><span class="sxs-lookup"><span data-stu-id="db707-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="db707-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="db707-197">**authorization**</span></span> | <span data-ttu-id="db707-198">按一下 hello**授權**按鈕 hello Data Factory 編輯器中，並輸入您 hello 自動產生的授權 URL toothis 屬性指派的認證。</span><span class="sxs-lookup"><span data-stu-id="db707-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="db707-199">是</span><span class="sxs-lookup"><span data-stu-id="db707-199">Yes</span></span> |
| <span data-ttu-id="db707-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="db707-200">**sessionId**</span></span> | <span data-ttu-id="db707-201">從 hello OAuth 授權工作階段的 OAuth 工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="db707-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="db707-202">每個工作階段識別碼都是唯一的，只能使用一次。</span><span class="sxs-lookup"><span data-stu-id="db707-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="db707-203">當您使用 hello Data Factory 編輯器時，此設定會自動產生。</span><span class="sxs-lookup"><span data-stu-id="db707-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="db707-204">是</span><span class="sxs-lookup"><span data-stu-id="db707-204">Yes</span></span> |

<span data-ttu-id="db707-205">**範例：使用者認證授權**</span><span class="sxs-lookup"><span data-stu-id="db707-205">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="db707-206">權杖到期</span><span class="sxs-lookup"><span data-stu-id="db707-206">Token expiration</span></span>
<span data-ttu-id="db707-207">hello 您使用 hello 產生的授權碼**授權**一段時間之後過期的按鈕。</span><span class="sxs-lookup"><span data-stu-id="db707-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="db707-208">hello 下訊息，表示該 hello 驗證權杖已過期：</span><span class="sxs-lookup"><span data-stu-id="db707-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="db707-209">認證作業錯誤：invalid_grant - AADSTS70002：驗證認證時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="db707-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="db707-210">AADSTS70008: hello 提供存取權限已過期或撤銷。</span><span class="sxs-lookup"><span data-stu-id="db707-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="db707-211">追蹤識別碼：d18629e8-af88-43c5-88e3-d8419eb1fca1 相互關連識別碼：fac30a0c-6be6-4e02-8d69-a776d2ffefd7 時間戳記：2015-12-15 21-09-31Z。</span><span class="sxs-lookup"><span data-stu-id="db707-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="db707-212">hello 下表顯示 hello 逾期時間的不同類型的使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="db707-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="db707-213">使用者類型</span><span class="sxs-lookup"><span data-stu-id="db707-213">User type</span></span> | <span data-ttu-id="db707-214">到期時間</span><span class="sxs-lookup"><span data-stu-id="db707-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="db707-215">「不」受 Azure Active Directory 管理的使用者帳戶 (例如 @hotmail.com 或 @live.com)</span><span class="sxs-lookup"><span data-stu-id="db707-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="db707-216">12 小時</span><span class="sxs-lookup"><span data-stu-id="db707-216">12 hours</span></span> |
| <span data-ttu-id="db707-217">受 Azure Active Directory 管理的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="db707-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="db707-218">14 天之後執行 hello 最後一個配量</span><span class="sxs-lookup"><span data-stu-id="db707-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="db707-219">如果以 OAuth 式連結服務為基礎的配量至少每 14 天執行一次，則為 90 天</span><span class="sxs-lookup"><span data-stu-id="db707-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="db707-220">如果您變更您的密碼 hello 權杖到期時間之前，hello 語彙基元就會立即到期。</span><span class="sxs-lookup"><span data-stu-id="db707-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="db707-221">您會看見 hello 訊息本節先前所述。</span><span class="sxs-lookup"><span data-stu-id="db707-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="db707-222">您可以重新 hello 帳戶授權使用 hello**授權**按鈕時 hello 權杖到期 tooredeploy hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="db707-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="db707-223">您也可以產生值 hello **sessionId**和**授權**屬性以程式設計方式利用 hello 下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="db707-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


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
<span data-ttu-id="db707-224">如需 hello 程式碼中使用的 hello Data Factory 類別的詳細資訊，請參閱 hello [AzureDataLakeStoreLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)， [AzureDataLakeAnalyticsLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)，和[AuthorizationSessionGetResponse 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="db707-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="db707-225">新增參考 tooversion`2.9.10826.1824`的`Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll`hello `WindowsFormsWebAuthenticationDialog` hello 程式碼中使用的類別。</span><span class="sxs-lookup"><span data-stu-id="db707-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="db707-226">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="db707-226">Dataset properties</span></span>
<span data-ttu-id="db707-227">toospecify 資料湖存放區中的資料集 toorepresent 輸入資料，設定 hello**類型**hello 資料集的屬性太**AzureDataLakeStore**。</span><span class="sxs-lookup"><span data-stu-id="db707-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="db707-228">設定 hello **linkedServiceName** hello Data Lake Store 的 hello 資料集 toohello 名稱的屬性連結服務。</span><span class="sxs-lookup"><span data-stu-id="db707-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="db707-229">如需 JSON 區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="db707-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="db707-230">所有資料集類型 (例如 Azure SQL 資料庫、Azure Blob 及 Azure 資料表) 其 JSON 中如結構、可用性及原則等資料集區段都相似。</span><span class="sxs-lookup"><span data-stu-id="db707-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="db707-231">hello **typeProperties**章節是不同的資料集的每個型別，並提供資訊，例如位置和 hello 資料存放區中的 hello 資料格式。</span><span class="sxs-lookup"><span data-stu-id="db707-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="db707-232">hello **typeProperties**類型的資料集區段**AzureDataLakeStore**包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="db707-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="db707-233">屬性</span><span class="sxs-lookup"><span data-stu-id="db707-233">Property</span></span> | <span data-ttu-id="db707-234">說明</span><span class="sxs-lookup"><span data-stu-id="db707-234">Description</span></span> | <span data-ttu-id="db707-235">必要</span><span class="sxs-lookup"><span data-stu-id="db707-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="db707-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="db707-236">**folderPath**</span></span> |<span data-ttu-id="db707-237">路徑 toohello 容器，並在資料湖存放區中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="db707-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="db707-238">是</span><span class="sxs-lookup"><span data-stu-id="db707-238">Yes</span></span> |
| <span data-ttu-id="db707-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="db707-239">**fileName**</span></span> |<span data-ttu-id="db707-240">在 Azure 資料湖存放區中的 hello 檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="db707-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="db707-241">hello **fileName**屬性是選擇性的區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="db707-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="db707-242">如果您指定**fileName**，hello 活動 （包括複製） 的運作方式 hello 特定檔案。</span><span class="sxs-lookup"><span data-stu-id="db707-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="db707-243">當**fileName**未指定，複本會包含中的所有檔案**folderPath** hello 輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="db707-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="db707-244">當**fileName**未指定輸出資料集和**preserveHierarchy**中未指定活動接收 hello hello 產生檔案名稱的資料格式 hello。_Guid_.txt'。</span><span class="sxs-lookup"><span data-stu-id="db707-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="db707-245">例如：Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt。</span><span class="sxs-lookup"><span data-stu-id="db707-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="db707-246">否</span><span class="sxs-lookup"><span data-stu-id="db707-246">No</span></span> |
| <span data-ttu-id="db707-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="db707-247">**partitionedBy**</span></span> |<span data-ttu-id="db707-248">hello **partitionedBy**是選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="db707-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="db707-249">Toospecify 動態的路徑和檔名，時間序列資料，您可以使用它。</span><span class="sxs-lookup"><span data-stu-id="db707-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="db707-250">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="db707-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="db707-251">如需詳細資訊和範例，請參閱[hello partitionedBy 屬性](#using-partitionedby-property)。</span><span class="sxs-lookup"><span data-stu-id="db707-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="db707-252">否</span><span class="sxs-lookup"><span data-stu-id="db707-252">No</span></span> |
| <span data-ttu-id="db707-253">**format**</span><span class="sxs-lookup"><span data-stu-id="db707-253">**format**</span></span> | <span data-ttu-id="db707-254">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**，和**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="db707-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="db707-255">設定 hello**類型**下的屬性**格式**tooone 這些值。</span><span class="sxs-lookup"><span data-stu-id="db707-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="db707-256">如需詳細資訊，請參閱 hello[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)， [JSON 格式](data-factory-supported-file-and-compression-formats.md#json-format)， [Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)， [ORC 格式](data-factory-supported-file-and-compression-formats.md#orc-format)，和[Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節 hello [Azure Data Factory 支援的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="db707-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="db707-257">如果您想要 toocopy 檔案 」 做為-是 「 檔案型存放區之間 （二進位複製），略過 hello`format`這兩個輸入和輸出資料集定義中的區段。</span><span class="sxs-lookup"><span data-stu-id="db707-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="db707-258">否</span><span class="sxs-lookup"><span data-stu-id="db707-258">No</span></span> |
| <span data-ttu-id="db707-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="db707-259">**compression**</span></span> | <span data-ttu-id="db707-260">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="db707-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="db707-261">支援的類型為：GZip、Deflate、BZip2 及 ZipDeflate。</span><span class="sxs-lookup"><span data-stu-id="db707-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="db707-262">支援的層級為 **Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="db707-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="db707-263">如需詳細資訊，請參閱 [Azure Data Factory 支援的檔案與壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="db707-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="db707-264">否</span><span class="sxs-lookup"><span data-stu-id="db707-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="db707-265">hello partitionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="db707-265">hello partitionedBy property</span></span>
<span data-ttu-id="db707-266">您可以指定動態**folderPath**和**fileName**屬性時間序列資料以 hello **partitionedBy**屬性、 Data Factory 函數和系統變數。</span><span class="sxs-lookup"><span data-stu-id="db707-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="db707-267">如需詳細資訊，請參閱 hello [Azure Data Factory-函式和系統變數](data-factory-functions-variables.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="db707-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="db707-268">在下列範例，hello `{Slice}` hello hello Data Factory 系統變數值會取代`SliceStart`hello 格式指定 (`yyyyMMddHH`)。</span><span class="sxs-lookup"><span data-stu-id="db707-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="db707-269">hello 名稱`SliceStart`參考 toohello hello 配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="db707-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="db707-270">hello`folderPath`屬性是不同的每個配量，如下所示`wikidatagateway/wikisampledataout/2014100103`或`wikidatagateway/wikisampledataout/2014100104`。</span><span class="sxs-lookup"><span data-stu-id="db707-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="db707-271">在下列範例、 hello 年、 月、 日和時間的 hello`SliceStart`會擷取至不同的變數所使用的 hello`folderPath`和`fileName`屬性：</span><span class="sxs-lookup"><span data-stu-id="db707-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
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
<span data-ttu-id="db707-272">如需有關時間序列資料集的詳細資訊，排程，以及配量，請參閱 hello [Azure Data Factory 中的資料集](data-factory-create-datasets.md)和[Data Factory 排程和執行](data-factory-scheduling-and-execution.md)文件。</span><span class="sxs-lookup"><span data-stu-id="db707-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="db707-273">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="db707-273">Copy activity properties</span></span>
<span data-ttu-id="db707-274">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="db707-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="db707-275">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="db707-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="db707-276">hello hello 中可用屬性**typeProperties** > 一節的活動會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="db707-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="db707-277">複製活動，它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="db707-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="db707-278">**AzureDataLakeStoreSource**支援下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="db707-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="db707-279">屬性</span><span class="sxs-lookup"><span data-stu-id="db707-279">Property</span></span> | <span data-ttu-id="db707-280">說明</span><span class="sxs-lookup"><span data-stu-id="db707-280">Description</span></span> | <span data-ttu-id="db707-281">允許的值</span><span class="sxs-lookup"><span data-stu-id="db707-281">Allowed values</span></span> | <span data-ttu-id="db707-282">必要</span><span class="sxs-lookup"><span data-stu-id="db707-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db707-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="db707-283">**recursive**</span></span> |<span data-ttu-id="db707-284">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="db707-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="db707-285">True (預設值)、False</span><span class="sxs-lookup"><span data-stu-id="db707-285">True (default value), False</span></span> |<span data-ttu-id="db707-286">否</span><span class="sxs-lookup"><span data-stu-id="db707-286">No</span></span> |


<span data-ttu-id="db707-287">**AzureDataLakeStoreSink**支援下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="db707-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="db707-288">屬性</span><span class="sxs-lookup"><span data-stu-id="db707-288">Property</span></span> | <span data-ttu-id="db707-289">說明</span><span class="sxs-lookup"><span data-stu-id="db707-289">Description</span></span> | <span data-ttu-id="db707-290">允許的值</span><span class="sxs-lookup"><span data-stu-id="db707-290">Allowed values</span></span> | <span data-ttu-id="db707-291">必要</span><span class="sxs-lookup"><span data-stu-id="db707-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db707-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="db707-292">**copyBehavior**</span></span> |<span data-ttu-id="db707-293">指定 hello 複製行為。</span><span class="sxs-lookup"><span data-stu-id="db707-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="db707-294"><b>PreserveHierarchy</b>： 保留 hello hello 目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="db707-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="db707-295">hello 的來源檔案 toosource 資料夾的相對路徑會是相同 toohello 的目標檔案 tootarget 資料夾的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="db707-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="db707-296"><b>FlattenHierarchy</b>: hello 第一個層級的 hello 目標資料夾中建立 hello 來源資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="db707-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="db707-297">會使用自動產生名稱建立 hello 目標檔案。</span><span class="sxs-lookup"><span data-stu-id="db707-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="db707-298"><b>MergeFiles</b>： 合併 hello 來源資料夾 tooone 檔案中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="db707-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="db707-299">如果 hello 檔案或 blob 名稱指定，則 hello 合併的檔案名稱是 hello 指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="db707-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="db707-300">否則，hello 檔案名稱是自動產生。</span><span class="sxs-lookup"><span data-stu-id="db707-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="db707-301">否</span><span class="sxs-lookup"><span data-stu-id="db707-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="db707-302">遞迴和 copyBehavior 範例</span><span class="sxs-lookup"><span data-stu-id="db707-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="db707-303">本章節描述 hello hello 複製作業，針對遞迴和 copyBehavior 值的不同組合產生的行為。</span><span class="sxs-lookup"><span data-stu-id="db707-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="db707-304">遞迴</span><span class="sxs-lookup"><span data-stu-id="db707-304">recursive</span></span> | <span data-ttu-id="db707-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="db707-305">copyBehavior</span></span> | <span data-ttu-id="db707-306">產生的行為</span><span class="sxs-lookup"><span data-stu-id="db707-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db707-307">true</span><span class="sxs-lookup"><span data-stu-id="db707-307">true</span></span> |<span data-ttu-id="db707-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="db707-308">preserveHierarchy</span></span> |<span data-ttu-id="db707-309">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="db707-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="db707-310">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-310">Folder1</span></span><br/><span data-ttu-id="db707-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="db707-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="db707-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="db707-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="db707-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="db707-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="db707-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="db707-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="db707-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="db707-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="db707-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="db707-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="db707-317">hello 目標資料夾 Folder1 建立以相同結構為 hello 來源 hello</span><span class="sxs-lookup"><span data-stu-id="db707-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="db707-318">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-318">Folder1</span></span><br/><span data-ttu-id="db707-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="db707-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="db707-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="db707-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="db707-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="db707-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="db707-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="db707-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="db707-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="db707-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="db707-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="db707-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="db707-325">true</span><span class="sxs-lookup"><span data-stu-id="db707-325">true</span></span> |<span data-ttu-id="db707-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="db707-326">flattenHierarchy</span></span> |<span data-ttu-id="db707-327">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="db707-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="db707-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-328">Folder1</span></span><br/><span data-ttu-id="db707-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="db707-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="db707-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="db707-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="db707-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="db707-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="db707-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="db707-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="db707-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="db707-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="db707-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="db707-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="db707-335">使用下列結構的 hello 建立 hello 目標 Folder1:</span><span class="sxs-lookup"><span data-stu-id="db707-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="db707-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-336">Folder1</span></span><br/><span data-ttu-id="db707-337">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="db707-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="db707-338">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="db707-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="db707-339">&nbsp;&nbsp;&nbsp;&nbsp;File3 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="db707-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="db707-340">&nbsp;&nbsp;&nbsp;&nbsp;File4 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="db707-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="db707-341">&nbsp;&nbsp;&nbsp;&nbsp;File5 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="db707-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="db707-342">true</span><span class="sxs-lookup"><span data-stu-id="db707-342">true</span></span> |<span data-ttu-id="db707-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="db707-343">mergeFiles</span></span> |<span data-ttu-id="db707-344">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="db707-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="db707-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-345">Folder1</span></span><br/><span data-ttu-id="db707-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="db707-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="db707-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="db707-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="db707-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="db707-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="db707-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="db707-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="db707-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="db707-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="db707-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="db707-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="db707-352">使用下列結構的 hello 建立 hello 目標 Folder1:</span><span class="sxs-lookup"><span data-stu-id="db707-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="db707-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-353">Folder1</span></span><br/><span data-ttu-id="db707-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 的內容會合併成一個檔案，並有自動產生的檔案名稱</span><span class="sxs-lookup"><span data-stu-id="db707-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="db707-355">false</span><span class="sxs-lookup"><span data-stu-id="db707-355">false</span></span> |<span data-ttu-id="db707-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="db707-356">preserveHierarchy</span></span> |<span data-ttu-id="db707-357">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="db707-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="db707-358">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-358">Folder1</span></span><br/><span data-ttu-id="db707-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="db707-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="db707-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="db707-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="db707-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="db707-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="db707-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="db707-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="db707-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="db707-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="db707-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="db707-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="db707-365">使用下列結構的 hello 建立 hello 目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="db707-366">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-366">Folder1</span></span><br/><span data-ttu-id="db707-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="db707-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="db707-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="db707-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="db707-369">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="db707-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="db707-370">false</span><span class="sxs-lookup"><span data-stu-id="db707-370">false</span></span> |<span data-ttu-id="db707-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="db707-371">flattenHierarchy</span></span> |<span data-ttu-id="db707-372">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="db707-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="db707-373">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-373">Folder1</span></span><br/><span data-ttu-id="db707-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="db707-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="db707-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="db707-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="db707-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="db707-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="db707-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="db707-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="db707-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="db707-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="db707-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="db707-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="db707-380">使用下列結構的 hello 建立 hello 目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="db707-381">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-381">Folder1</span></span><br/><span data-ttu-id="db707-382">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="db707-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="db707-383">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="db707-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="db707-384">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="db707-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="db707-385">false</span><span class="sxs-lookup"><span data-stu-id="db707-385">false</span></span> |<span data-ttu-id="db707-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="db707-386">mergeFiles</span></span> |<span data-ttu-id="db707-387">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="db707-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="db707-388">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-388">Folder1</span></span><br/><span data-ttu-id="db707-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="db707-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="db707-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="db707-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="db707-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="db707-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="db707-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="db707-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="db707-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="db707-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="db707-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="db707-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="db707-395">使用下列結構的 hello 建立 hello 目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="db707-396">Folder1</span><span class="sxs-lookup"><span data-stu-id="db707-396">Folder1</span></span><br/><span data-ttu-id="db707-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 的內容會合併成一個檔案，並有自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="db707-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="db707-398">File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="db707-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="db707-399">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="db707-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="db707-400">支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="db707-400">Supported file and compression formats</span></span>
<span data-ttu-id="db707-401">如需詳細資訊，請參閱 hello [Azure Data Factory 中的檔案及壓縮格式](data-factory-supported-file-and-compression-formats.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="db707-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="db707-402">從資料湖存放區複製資料 tooand JSON 範例</span><span class="sxs-lookup"><span data-stu-id="db707-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="db707-403">下列範例中的 hello 提供範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="db707-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="db707-404">您可以使用這些範例定義 toocreate 管線使用 hello [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="db707-405">hello 範例顯示如何從資料湖存放區和 Azure Blob 儲存體 toocopy 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="db707-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="db707-406">不過，資料可以複製_直接_從任何支援的 hello 接收的 hello 來源 tooany。</span><span class="sxs-lookup"><span data-stu-id="db707-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="db707-407">如需詳細資訊，請參閱"支援資料存放區和格式 」 的 hello 一節中 hello[使用複製活動移動資料](data-factory-data-movement-activities.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="db707-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="db707-408">範例： 將資料從 Azure Blob 儲存體 tooAzure 資料湖存放區複製</span><span class="sxs-lookup"><span data-stu-id="db707-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="db707-409">本節中的 hello 範例程式碼顯示：</span><span class="sxs-lookup"><span data-stu-id="db707-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="db707-410">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="db707-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="db707-411">[AzureDataLakeStore](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="db707-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="db707-412">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="db707-413">[AzureDataLakeStore](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="db707-414">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [AzureDataLakeStoreSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="db707-415">hello 範例顯示時間序列資料從 Azure Blob 儲存體的方式複製 tooData 湖存放區的每個小時。</span><span class="sxs-lookup"><span data-stu-id="db707-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="db707-416">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="db707-416">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="db707-417">**Azure Data Lake Store 已連結的服務**</span><span class="sxs-lookup"><span data-stu-id="db707-417">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="db707-418">設定詳細資料，請參閱 hello[連結服務屬性](#linked-service-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="db707-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="db707-419">**Azure Blob 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="db707-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="db707-420">在下列範例的 hello，資料從挑選新的 blob 每小時 (`"frequency": "Hour", "interval": 1`)。</span><span class="sxs-lookup"><span data-stu-id="db707-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="db707-421">hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="db707-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="db707-422">hello 年、 月和日數部分的 hello 開始時間，則會使用 hello 資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="db707-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="db707-423">hello 檔案名稱會使用 hello hello 部分開始時間的小時。</span><span class="sxs-lookup"><span data-stu-id="db707-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="db707-424">hello `"external": true` hello 資料表是外部 toohello 資料處理站並不產生 hello data factory 中的活動時，設定會通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="db707-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="db707-425">**Azure Data Lake Store 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="db707-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="db707-426">下列範例複製資料 tooData 湖存放區的 hello。</span><span class="sxs-lookup"><span data-stu-id="db707-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="db707-427">會複製新的資料湖存放區 tooData 每小時。</span><span class="sxs-lookup"><span data-stu-id="db707-427">New data is copied tooData Lake Store every hour.</span></span>

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


<span data-ttu-id="db707-428">**具有 Blob 來源和 Data Lake Store 接收器的管線中的複製活動**</span><span class="sxs-lookup"><span data-stu-id="db707-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="db707-429">在下列範例的 hello，hello 管線包含設定的複製活動 toouse hello 輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="db707-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="db707-430">hello 複製活動會排定的 toorun 每小時。</span><span class="sxs-lookup"><span data-stu-id="db707-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="db707-431">在 hello 管線 JSON 定義中，hello`source`類型設定得`BlobSource`，和 hello`sink`類型設定得`AzureDataLakeStoreSink`。</span><span class="sxs-lookup"><span data-stu-id="db707-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="db707-432">範例： 將資料從 Azure Data Lake Store tooan Azure blob 複製</span><span class="sxs-lookup"><span data-stu-id="db707-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="db707-433">本節中的 hello 範例程式碼顯示：</span><span class="sxs-lookup"><span data-stu-id="db707-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="db707-434">[AzureDataLakeStore](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="db707-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="db707-435">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="db707-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="db707-436">[AzureDataLakeStore](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="db707-437">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="db707-438">具有使用 [AzureDataLakeStoreSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="db707-439">hello 程式碼會複製時間序列資料從 Azure blob 的資料湖存放區 tooan 每小時。</span><span class="sxs-lookup"><span data-stu-id="db707-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="db707-440">**Azure Data Lake Store 已連結的服務**</span><span class="sxs-lookup"><span data-stu-id="db707-440">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="db707-441">設定詳細資料，請參閱 hello[連結服務屬性](#linked-service-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="db707-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="db707-442">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="db707-442">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="db707-443">**Azure Data Lake 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="db707-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="db707-444">在此範例中，設定`"external"`太`true`hello 資料表是外部 toohello 資料處理站並不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="db707-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="db707-445">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="db707-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="db707-446">在下列範例的 hello，資料會寫入 tooa 新 blob 的每個小時 (`"frequency": "Hour", "interval": 1`)。</span><span class="sxs-lookup"><span data-stu-id="db707-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="db707-447">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="db707-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="db707-448">hello 年、 月、 日和 hello 開始時間的小時部分，則會使用 hello 資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="db707-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

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

<span data-ttu-id="db707-449">**具有 Azure Data Lake Store 來源和 Blob 接收器的管線中的複製活動**</span><span class="sxs-lookup"><span data-stu-id="db707-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="db707-450">在下列範例的 hello，hello 管線包含設定的複製活動 toouse hello 輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="db707-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="db707-451">hello 複製活動會排定的 toorun 每小時。</span><span class="sxs-lookup"><span data-stu-id="db707-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="db707-452">在 hello 管線 JSON 定義中，hello`source`類型設定得`AzureDataLakeStoreSource`，和 hello`sink`類型設定得`BlobSink`。</span><span class="sxs-lookup"><span data-stu-id="db707-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

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

<span data-ttu-id="db707-453">您也可以在 hello 複製活動定義中，對應 hello 來源資料集 toocolumns hello 接收資料集中的資料行。</span><span class="sxs-lookup"><span data-stu-id="db707-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="db707-454">如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="db707-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="db707-455">效能和微調</span><span class="sxs-lookup"><span data-stu-id="db707-455">Performance and tuning</span></span>
<span data-ttu-id="db707-456">toolearn 有關 hello 因素會影響複製活動效能以及如何 toooptimize，請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="db707-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
