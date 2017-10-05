---
title: "從 SQL Server 來回移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory，從內部部署或 Azure VM 中的 SQL Server 資料庫來回移動資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: 9cd2077d897631457925cda5ef5e6df3c0c33177
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="e5481-103">使用 Azure Data Factory 從 SQL Server 內部部署或 IaaS (Azure VM) 上來回移動資料</span><span class="sxs-lookup"><span data-stu-id="e5481-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="e5481-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，將資料移進/移出內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e5481-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="e5481-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="e5481-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="e5481-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="e5481-106">Supported scenarios</span></span>
<span data-ttu-id="e5481-107">您可以**從 SQL Server 資料庫**將資料複製到下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="e5481-107">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="e5481-108">您可以從下列資料存放區將資料複製**到 SQL Server 資料庫**：</span><span class="sxs-lookup"><span data-stu-id="e5481-108">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="e5481-109">支援的 SQL Server 版本</span><span class="sxs-lookup"><span data-stu-id="e5481-109">Supported SQL Server versions</span></span>
<span data-ttu-id="e5481-110">這個 SQL Server 連接器支援使用 SQL 驗證和 Windows 驗證，在裝載於內部部署或在 Azure IaaS 中的下列版本個體間往返複製資料︰SQL Server 2016、SQL Server 2014、SQL Server 2012、SQL Server 2008 R2、SQL Server 2008、SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="e5481-110">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="e5481-111">啟用連線</span><span class="sxs-lookup"><span data-stu-id="e5481-111">Enabling connectivity</span></span>
<span data-ttu-id="e5481-112">與裝載於內部部署或 Azure IaaS (基礎結構即為服務) VM 中的 SQL Server 連線所需的概念和步驟都相同。</span><span class="sxs-lookup"><span data-stu-id="e5481-112">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="e5481-113">在這兩種情況下，您都需要使用「資料管理閘道」來進行連線。</span><span class="sxs-lookup"><span data-stu-id="e5481-113">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="e5481-114">請參閱 [在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文來了解資料管理閘道和設定閘道的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="e5481-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="e5481-115">設定閘道器執行個體是與 SQL Server 連線的必要條件。</span><span class="sxs-lookup"><span data-stu-id="e5481-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="e5481-116">雖然您可以將閘道安裝在與 SQL Server 相同的內部部署機器或雲端 VM 執行個體上來獲得較佳的效能，但仍建議您將它們安裝在個別的機器上。</span><span class="sxs-lookup"><span data-stu-id="e5481-116">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="e5481-117">將閘道與 SQL Server 置於個別的機器上可降低發生資源競爭的情況。</span><span class="sxs-lookup"><span data-stu-id="e5481-117">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e5481-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="e5481-118">Getting started</span></span>
<span data-ttu-id="e5481-119">您可以建立內含複製活動的管線，使用不同的工具/API 將資料移進/移出內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e5481-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="e5481-120">若要建立管線，最簡單的方式就是使用**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="e5481-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="e5481-121">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="e5481-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="e5481-122">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="e5481-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e5481-123">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="e5481-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e5481-124">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="e5481-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="e5481-125">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="e5481-125">Create a **data factory**.</span></span> <span data-ttu-id="e5481-126">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="e5481-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="e5481-127">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="e5481-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="e5481-128">例如，如果您從 SQL Server 資料庫將資料複製到 Azure Blob 儲存體，您會建立兩個連結服務，將 SQL Server 資料庫和 Azure 儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="e5481-128">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="e5481-129">有關 SQL Server 資料庫專屬的連結服務屬性，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="e5481-129">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="e5481-130">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="e5481-131">在上一個步驟所述的範例中，您會建立資料集來指定 SQL Server 資料庫中包含輸入資料的 SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-131">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="e5481-132">您還會建立另一個資料集來指定 blob 容器和資料夾，以保存從 SQL Server 資料庫複製的資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-132">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="e5481-133">有關 SQL Server 資料庫專屬的資料集屬性，請參閱[資料集屬性](#dataset-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="e5481-133">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="e5481-134">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="e5481-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="e5481-135">在稍早所述的範例中，您使用 SqlSource 作為來源，以及使用 BlobSink 作為複製活動的接收器。</span><span class="sxs-lookup"><span data-stu-id="e5481-135">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="e5481-136">同樣地，如果您是從 Azure Blob 儲存體複製到 SQL Server 資料庫，則需要在複製活動中使用 BlobSource 和 SqlSink。</span><span class="sxs-lookup"><span data-stu-id="e5481-136">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="e5481-137">有關 SQL Server 資料庫專屬的複製活動屬性，請參閱[複製活動屬性](#copy-activity-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="e5481-137">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="e5481-138">如需有關如何使用資料存放區作為來源或接收器的詳細資訊，請在上一節按一下適用於您的資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="e5481-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="e5481-139">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="e5481-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="e5481-140">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="e5481-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="e5481-141">如需相關範例，其中含有用來將資料複製到內部部署 SQL Server 資料庫 (或從內部部署 SQL Server 資料庫複製資料) 之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例](#json-examples-for-copying-data-from-and-to-sql-server)一節。</span><span class="sxs-lookup"><span data-stu-id="e5481-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="e5481-142">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 SQL Server 特有的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="e5481-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="e5481-143">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="e5481-143">Linked service properties</span></span>
<span data-ttu-id="e5481-144">您可以建立 **OnPremisesSqlServer** 類型的連結服務，以將內部部署 SQL Server 資料庫連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="e5481-144">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="e5481-145">下表提供內部部署 SQL Server 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="e5481-145">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="e5481-146">下表提供 SQL Server 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="e5481-146">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="e5481-147">屬性</span><span class="sxs-lookup"><span data-stu-id="e5481-147">Property</span></span> | <span data-ttu-id="e5481-148">說明</span><span class="sxs-lookup"><span data-stu-id="e5481-148">Description</span></span> | <span data-ttu-id="e5481-149">必要</span><span class="sxs-lookup"><span data-stu-id="e5481-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5481-150">類型</span><span class="sxs-lookup"><span data-stu-id="e5481-150">type</span></span> |<span data-ttu-id="e5481-151">類型屬性應設為： **OnPremisesSqlServer**。</span><span class="sxs-lookup"><span data-stu-id="e5481-151">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="e5481-152">是</span><span class="sxs-lookup"><span data-stu-id="e5481-152">Yes</span></span> |
| <span data-ttu-id="e5481-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="e5481-153">connectionString</span></span> |<span data-ttu-id="e5481-154">指定使用 SQL 驗證或 Windows 驗證連接至內部部署 SQL Server 資料庫所需的 connectionString 資訊。</span><span class="sxs-lookup"><span data-stu-id="e5481-154">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="e5481-155">是</span><span class="sxs-lookup"><span data-stu-id="e5481-155">Yes</span></span> |
| <span data-ttu-id="e5481-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e5481-156">gatewayName</span></span> |<span data-ttu-id="e5481-157">Data Factory 服務應該用來連接到內部部署 SQL Server 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-157">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="e5481-158">是</span><span class="sxs-lookup"><span data-stu-id="e5481-158">Yes</span></span> |
| <span data-ttu-id="e5481-159">username</span><span class="sxs-lookup"><span data-stu-id="e5481-159">username</span></span> |<span data-ttu-id="e5481-160">如果您使用「Windows 驗證」，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="e5481-161">範例︰**domainname\\username**。</span><span class="sxs-lookup"><span data-stu-id="e5481-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="e5481-162">否</span><span class="sxs-lookup"><span data-stu-id="e5481-162">No</span></span> |
| <span data-ttu-id="e5481-163">password</span><span class="sxs-lookup"><span data-stu-id="e5481-163">password</span></span> |<span data-ttu-id="e5481-164">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="e5481-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="e5481-165">否</span><span class="sxs-lookup"><span data-stu-id="e5481-165">No</span></span> |

<span data-ttu-id="e5481-166">您可以使用 **New-AzureRmDataFactoryEncryptValue** Cmdlet 加密認證，並在連接字串中使用這些認證，如下列範例所示 (**EncryptedCredential** 屬性)：</span><span class="sxs-lookup"><span data-stu-id="e5481-166">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="e5481-167">範例</span><span class="sxs-lookup"><span data-stu-id="e5481-167">Samples</span></span>
<span data-ttu-id="e5481-168">**使用 SQL 驗證的 JSON**</span><span class="sxs-lookup"><span data-stu-id="e5481-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="e5481-169">**使用 Windows 驗證的 JSON**</span><span class="sxs-lookup"><span data-stu-id="e5481-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="e5481-170">資料管理閘道會模擬指定的使用者帳戶，以連線到內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e5481-170">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="e5481-171">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="e5481-171">Dataset properties</span></span>
<span data-ttu-id="e5481-172">範例中使用使用 **SqlServerTable** 類型的資料集來表示 SQL Server 資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-172">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="e5481-173">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="e5481-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e5481-174">所有資料集類型 (SQL Server、Azure Blob、Azure 資料表等) 的資料集 JSON 區段 (例如 structure、availability 及 policy) 都相似。</span><span class="sxs-lookup"><span data-stu-id="e5481-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e5481-175">每個資料集類型的 typeProperties 區段都不同，可提供資料存放區中資料的位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e5481-175">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="e5481-176">**SqlServerTable** 類型資料集的 **typeProperties** 區段有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e5481-176">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="e5481-177">屬性</span><span class="sxs-lookup"><span data-stu-id="e5481-177">Property</span></span> | <span data-ttu-id="e5481-178">說明</span><span class="sxs-lookup"><span data-stu-id="e5481-178">Description</span></span> | <span data-ttu-id="e5481-179">必要</span><span class="sxs-lookup"><span data-stu-id="e5481-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5481-180">tableName</span><span class="sxs-lookup"><span data-stu-id="e5481-180">tableName</span></span> |<span data-ttu-id="e5481-181">SQL Server Database 執行個體中連結服務所參照的資料表或檢視名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-181">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="e5481-182">是</span><span class="sxs-lookup"><span data-stu-id="e5481-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="e5481-183">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="e5481-183">Copy activity properties</span></span>
<span data-ttu-id="e5481-184">如果您要將資料從 SQL Server 資料庫移出，請將複製活動中的來源類型設定為 **SqlSource**。</span><span class="sxs-lookup"><span data-stu-id="e5481-184">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="e5481-185">同樣的，如果您要將資料移進 SQL Server 資料庫，請將複製活動中的接收器類型設定為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="e5481-185">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="e5481-186">本節提供 SqlSource 和 SqlSink 支援的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="e5481-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="e5481-187">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="e5481-187">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e5481-188">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="e5481-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="e5481-189">複製活動只會採用一個輸入，而且只產生一個輸出。</span><span class="sxs-lookup"><span data-stu-id="e5481-189">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="e5481-190">而活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e5481-190">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="e5481-191">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e5481-191">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="e5481-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="e5481-192">SqlSource</span></span>
<span data-ttu-id="e5481-193">當複製活動中的來源類型為 **SqlSource** 時，**typeProperties** 區段會有下列可用屬性：</span><span class="sxs-lookup"><span data-stu-id="e5481-193">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="e5481-194">屬性</span><span class="sxs-lookup"><span data-stu-id="e5481-194">Property</span></span> | <span data-ttu-id="e5481-195">說明</span><span class="sxs-lookup"><span data-stu-id="e5481-195">Description</span></span> | <span data-ttu-id="e5481-196">允許的值</span><span class="sxs-lookup"><span data-stu-id="e5481-196">Allowed values</span></span> | <span data-ttu-id="e5481-197">必要</span><span class="sxs-lookup"><span data-stu-id="e5481-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e5481-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="e5481-198">sqlReaderQuery</span></span> |<span data-ttu-id="e5481-199">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-199">Use the custom query to read data.</span></span> |<span data-ttu-id="e5481-200">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="e5481-200">SQL query string.</span></span> <span data-ttu-id="e5481-201">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="e5481-201">For example: select * from MyTable.</span></span> <span data-ttu-id="e5481-202">可以參考輸入資料集所參考資料庫中的多個資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-202">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="e5481-203">如果未指定，執行的 SQL 陳述式：select from MyTable。</span><span class="sxs-lookup"><span data-stu-id="e5481-203">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="e5481-204">否</span><span class="sxs-lookup"><span data-stu-id="e5481-204">No</span></span> |
| <span data-ttu-id="e5481-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="e5481-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="e5481-206">從來源資料表讀取資料的預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-206">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="e5481-207">預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-207">Name of the stored procedure.</span></span> <span data-ttu-id="e5481-208">最後一個 SQL 陳述式必須是預存程序中的 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="e5481-208">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="e5481-209">否</span><span class="sxs-lookup"><span data-stu-id="e5481-209">No</span></span> |
| <span data-ttu-id="e5481-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e5481-210">storedProcedureParameters</span></span> |<span data-ttu-id="e5481-211">預存程序的參數。</span><span class="sxs-lookup"><span data-stu-id="e5481-211">Parameters for the stored procedure.</span></span> |<span data-ttu-id="e5481-212">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="e5481-212">Name/value pairs.</span></span> <span data-ttu-id="e5481-213">參數的名稱和大小寫必須符合預存程序參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="e5481-213">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="e5481-214">否</span><span class="sxs-lookup"><span data-stu-id="e5481-214">No</span></span> |

<span data-ttu-id="e5481-215">如果已為 SqlSource 指定 **sqlReaderQuery** ，複製活動會針對 SQL Server 資料庫來源執行這項查詢以取得資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-215">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="e5481-216">或者，您可以藉由指定 **sqlReaderStoredProcedureName** 和 **storedProcedureParameters** (如果預存程序接受參數) 來指定預存程序。</span><span class="sxs-lookup"><span data-stu-id="e5481-216">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="e5481-217">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，系統就會使用 structure 區段中定義的資料行來建立一個要對「SQL Server 資料庫」執行的 select 查詢。</span><span class="sxs-lookup"><span data-stu-id="e5481-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="e5481-218">如果資料集定義沒有結構，則會從資料表中選取所有資料行。</span><span class="sxs-lookup"><span data-stu-id="e5481-218">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="e5481-219">當您使用 **sqlReaderStoredProcedureName** 時，仍必須為資料集 JSON 中的 **tableName** 屬性指定值。</span><span class="sxs-lookup"><span data-stu-id="e5481-219">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="e5481-220">雖然目前尚未針對此資料表來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="e5481-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="e5481-221">管線</span><span class="sxs-lookup"><span data-stu-id="e5481-221">SqlSink</span></span>
<span data-ttu-id="e5481-222">**SqlSink** 支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e5481-222">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="e5481-223">屬性</span><span class="sxs-lookup"><span data-stu-id="e5481-223">Property</span></span> | <span data-ttu-id="e5481-224">說明</span><span class="sxs-lookup"><span data-stu-id="e5481-224">Description</span></span> | <span data-ttu-id="e5481-225">允許的值</span><span class="sxs-lookup"><span data-stu-id="e5481-225">Allowed values</span></span> | <span data-ttu-id="e5481-226">必要</span><span class="sxs-lookup"><span data-stu-id="e5481-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e5481-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e5481-227">writeBatchTimeout</span></span> |<span data-ttu-id="e5481-228">在逾時前等待批次插入作業完成的時間。</span><span class="sxs-lookup"><span data-stu-id="e5481-228">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="e5481-229">時間範圍</span><span class="sxs-lookup"><span data-stu-id="e5481-229">timespan</span></span><br/><br/> <span data-ttu-id="e5481-230">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="e5481-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="e5481-231">否</span><span class="sxs-lookup"><span data-stu-id="e5481-231">No</span></span> |
| <span data-ttu-id="e5481-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e5481-232">writeBatchSize</span></span> |<span data-ttu-id="e5481-233">當緩衝區大小達到 writeBatchSize 時，將資料插入 SQL 資料表中</span><span class="sxs-lookup"><span data-stu-id="e5481-233">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="e5481-234">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="e5481-234">Integer (number of rows)</span></span> |<span data-ttu-id="e5481-235">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="e5481-235">No (default: 10000)</span></span> |
| <span data-ttu-id="e5481-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="e5481-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="e5481-237">指定要讓「複製活動」執行的查詢，以便清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-237">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="e5481-238">如需詳細資訊，請參閱[可重複複製](#repeatable-copy)一節。</span><span class="sxs-lookup"><span data-stu-id="e5481-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="e5481-239">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="e5481-239">A query statement.</span></span> |<span data-ttu-id="e5481-240">否</span><span class="sxs-lookup"><span data-stu-id="e5481-240">No</span></span> |
| <span data-ttu-id="e5481-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="e5481-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="e5481-242">指定要讓「複製活動」以自動產生的分割識別碼填入的資料行名稱，這可在重新執行時用來清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-242">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="e5481-243">如需詳細資訊，請參閱[可重複複製](#repeatable-copy)一節。</span><span class="sxs-lookup"><span data-stu-id="e5481-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="e5481-244">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="e5481-245">否</span><span class="sxs-lookup"><span data-stu-id="e5481-245">No</span></span> |
| <span data-ttu-id="e5481-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="e5481-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="e5481-247">將資料更新插入 (更新/插入) 目標資料表中的預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-247">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="e5481-248">預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-248">Name of the stored procedure.</span></span> |<span data-ttu-id="e5481-249">否</span><span class="sxs-lookup"><span data-stu-id="e5481-249">No</span></span> |
| <span data-ttu-id="e5481-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e5481-250">storedProcedureParameters</span></span> |<span data-ttu-id="e5481-251">預存程序的參數。</span><span class="sxs-lookup"><span data-stu-id="e5481-251">Parameters for the stored procedure.</span></span> |<span data-ttu-id="e5481-252">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="e5481-252">Name/value pairs.</span></span> <span data-ttu-id="e5481-253">參數的名稱和大小寫必須符合預存程序參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="e5481-253">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="e5481-254">否</span><span class="sxs-lookup"><span data-stu-id="e5481-254">No</span></span> |
| <span data-ttu-id="e5481-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="e5481-255">sqlWriterTableType</span></span> |<span data-ttu-id="e5481-256">指定要在預存程序中使用的資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-256">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="e5481-257">複製活動可讓正在移動的資料可用於此資料表類型的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-257">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="e5481-258">然後，預存程序程式碼可以合併正在複製的資料與現有的資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-258">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="e5481-259">資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-259">A table type name.</span></span> |<span data-ttu-id="e5481-260">否</span><span class="sxs-lookup"><span data-stu-id="e5481-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="e5481-261">往返 SQL Server 複製資料的 JSON 範例</span><span class="sxs-lookup"><span data-stu-id="e5481-261">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="e5481-262">以下範例提供可用來使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 建立管線的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="e5481-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e5481-263">下列範例說明如何將資料複製到 SQL Server 和「Azure Blob 儲存體」，以及從這兩處複製資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-263">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="e5481-264">不過，您可以在 Azure Data Factory 中使用複製活動，從任何來源 **直接** 將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="e5481-264">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="e5481-265">範例：將資料從 SQL Server 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e5481-265">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="e5481-266">下列範例顯示︰</span><span class="sxs-lookup"><span data-stu-id="e5481-266">The following sample shows:</span></span>

1. <span data-ttu-id="e5481-267">[OnPremisesSqlServer](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="e5481-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="e5481-268">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="e5481-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e5481-269">[SqlServerTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="e5481-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="e5481-270">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="e5481-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e5481-271">具有使用 [SqlSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="e5481-271">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e5481-272">此範例會每小時將時間序列資料從 SQL Server 資料表複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="e5481-272">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="e5481-273">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="e5481-273">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="e5481-274">第一步是設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="e5481-274">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="e5481-275">如需相關指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="e5481-275">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="e5481-276">**SQL Server 連結服務**</span><span class="sxs-lookup"><span data-stu-id="e5481-276">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="e5481-277">**Azure Blob 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="e5481-277">**Azure Blob storage linked service**</span></span>

```json
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
<span data-ttu-id="e5481-278">**SQL Server 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="e5481-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="e5481-279">此範例假設您已在 SQL Server 中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestampcolumn")。</span><span class="sxs-lookup"><span data-stu-id="e5481-279">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="e5481-280">您可以使用單一資料集來查詢相同資料庫內的多個資料表，但針對資料集的 tableName typeProperty 必須使用單一資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-280">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="e5481-281">設定 “external”: ”true” 可讓 Data Factory 服務知道資料集是在 Data Factory 外部，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="e5481-281">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
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
<span data-ttu-id="e5481-282">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="e5481-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="e5481-283">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="e5481-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e5481-284">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="e5481-284">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="e5481-285">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="e5481-285">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
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
<span data-ttu-id="e5481-286">**具有複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="e5481-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="e5481-287">此管線包含「複製活動」，該活動已設定為使用這些輸入和輸出資料集，並且排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="e5481-287">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="e5481-288">在管線 JSON 定義中，**source** 類型設為 **SqlSource**，而 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="e5481-288">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="e5481-289">針對 **SqlReaderQuery** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-289">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="e5481-290">在此範例中，已為 SqlSource 指定 **sqlReaderQuery** 。</span><span class="sxs-lookup"><span data-stu-id="e5481-290">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="e5481-291">複製活動會針對 SQL Server 資料庫來源執行這項查詢以取得資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-291">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="e5481-292">或者，您可以藉由指定 **sqlReaderStoredProcedureName** 和 **storedProcedureParameters** (如果預存程序接受參數) 來指定預存程序。</span><span class="sxs-lookup"><span data-stu-id="e5481-292">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="e5481-293">sqlReaderQuery 可以參考輸入資料集所參考之資料庫內的多個資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-293">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="e5481-294">這不限於只有設定為資料集之 tableName typeProperty 的資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-294">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="e5481-295">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，系統就會使用 structure 區段中定義的資料行來建立一個要對「SQL Server 資料庫」執行的 select 查詢。</span><span class="sxs-lookup"><span data-stu-id="e5481-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="e5481-296">如果資料集定義沒有結構，則會從資料表中選取所有資料行。</span><span class="sxs-lookup"><span data-stu-id="e5481-296">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="e5481-297">如需 SqlSource 和 BlobSink 所支援屬性的清單，請參閱 [SQL 來源](#sqlsource)小節和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="e5481-297">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="e5481-298">範例：將資料從 Azure Blob 複製到 SQL Server</span><span class="sxs-lookup"><span data-stu-id="e5481-298">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="e5481-299">下列範例顯示︰</span><span class="sxs-lookup"><span data-stu-id="e5481-299">The following sample shows:</span></span>

1. <span data-ttu-id="e5481-300">[OnPremisesSqlServer](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="e5481-300">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="e5481-301">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="e5481-301">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e5481-302">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="e5481-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e5481-303">[SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="e5481-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e5481-304">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [SqlSink](#sql-server-copy-activity-type-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="e5481-304">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="e5481-305">此範例會每小時將時間序列資料從 Azure Blob 複製到 SQL Server 資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-305">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="e5481-306">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="e5481-306">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="e5481-307">**SQL Server 連結服務**</span><span class="sxs-lookup"><span data-stu-id="e5481-307">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="e5481-308">**Azure Blob 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="e5481-308">**Azure Blob storage linked service**</span></span>

```json
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
<span data-ttu-id="e5481-309">**Azure Blob 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="e5481-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="e5481-310">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="e5481-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e5481-311">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="e5481-311">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="e5481-312">資料夾路徑會使用開始時間的年、月及日部分，而檔案名稱則使用開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="e5481-312">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="e5481-313">“external”: “true” 設定可讓 Data Factory 服務知道資料集是在 Data Factory 外部，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="e5481-313">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
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
<span data-ttu-id="e5481-314">**SQL Server 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="e5481-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="e5481-315">此範例會將資料複製到 SQL Server 中名為 "MyTable" 的資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-315">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="e5481-316">請在 SQL Server 中建立此資料表，其資料行的數目須與您預期 Blob CSV 檔案要包含的數目相同。</span><span class="sxs-lookup"><span data-stu-id="e5481-316">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="e5481-317">此資料表會每小時加入新的資料列。</span><span class="sxs-lookup"><span data-stu-id="e5481-317">New rows are added to the table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="e5481-318">**具有複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="e5481-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="e5481-319">此管線包含「複製活動」，該活動已設定為使用這些輸入和輸出資料集，並且排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="e5481-319">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="e5481-320">在管線 JSON 定義中，**source** 類型設為 **BlobSource**，而 **sink** 類型設為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="e5481-320">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="e5481-321">疑難排解連線問題</span><span class="sxs-lookup"><span data-stu-id="e5481-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="e5481-322">將 SQL Server 設定成接受遠端連線。</span><span class="sxs-lookup"><span data-stu-id="e5481-322">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="e5481-323">啟動 [SQL Server Management Studio]、用滑鼠右鍵按一下 [伺服器]，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="e5481-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="e5481-324">選取清單中 [連接]，然後核取 [允許此伺服器的遠端連接]。</span><span class="sxs-lookup"><span data-stu-id="e5481-324">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![啟用遠端連線](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="e5481-326">如需詳細步驟，請參閱 [設定 remote access 伺服器組態選項](https://msdn.microsoft.com/library/ms191464.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="e5481-326">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="e5481-327">啟動 [SQL Server 組態管理員] 。</span><span class="sxs-lookup"><span data-stu-id="e5481-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="e5481-328">展開您想要之執行個體的 [SQL Server 網路組態]，然後選取 [MSSQLSERVER 的通訊協定]。</span><span class="sxs-lookup"><span data-stu-id="e5481-328">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="e5481-329">您應該會在右窗格中看到通訊協定。</span><span class="sxs-lookup"><span data-stu-id="e5481-329">You should see protocols in the right-pane.</span></span> <span data-ttu-id="e5481-330">用滑鼠右鍵按一下 [TCP/IP]，然後按一下 [啟用] 來啟用 TCP/IP。</span><span class="sxs-lookup"><span data-stu-id="e5481-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![啟用 TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="e5481-332">如需啟用 TCP/IP 通訊協定的詳細資料及替代方式，請參閱 [啟用或停用伺服器網路通訊協定](https://msdn.microsoft.com/library/ms191294.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="e5481-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="e5481-333">在相同的視窗中，按兩下 [TCP/IP] 來啟動 [TCP/IP 屬性] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e5481-333">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="e5481-334">切換到 [IP 位址] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e5481-334">Switch to the **IP Addresses** tab.</span></span> <span data-ttu-id="e5481-335">向下捲動到 [IPAll] 區段。</span><span class="sxs-lookup"><span data-stu-id="e5481-335">Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="e5481-336">記下 **TCP 通訊埠** (預設值是 **1433**)。</span><span class="sxs-lookup"><span data-stu-id="e5481-336">Note down the **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="e5481-337">在電腦上建立 **Windows 防火牆規則** ，來允許透過此連接埠的連入流量。</span><span class="sxs-lookup"><span data-stu-id="e5481-337">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="e5481-338">**確認連線**：若要使用完整名稱來連線到 SQL Server，請使用來自不同機器的 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="e5481-338">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="e5481-339">例如："<machine><domain>.corp<company>.com,1433"。</span><span class="sxs-lookup"><span data-stu-id="e5481-339">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="e5481-340">如需詳細資訊，請參閱[利用資料管理閘道在內部部署來源和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="e5481-340">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="e5481-341">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="e5481-341">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="e5481-342">目標資料庫中的身分識別資料行</span><span class="sxs-lookup"><span data-stu-id="e5481-342">Identity columns in the target database</span></span>
<span data-ttu-id="e5481-343">本節提供一個範例，此範例會將資料從沒有身分識別資料行的來源資料表，複製到具有身分識別資料行的目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-343">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="e5481-344">**來源資料表：**</span><span class="sxs-lookup"><span data-stu-id="e5481-344">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="e5481-345">**目的地資料表：**</span><span class="sxs-lookup"><span data-stu-id="e5481-345">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="e5481-346">請注意，目標資料表具有身分識別資料行。</span><span class="sxs-lookup"><span data-stu-id="e5481-346">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="e5481-347">**來源資料集 JSON 定義**</span><span class="sxs-lookup"><span data-stu-id="e5481-347">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="e5481-348">**目的地資料集 JSON 定義**</span><span class="sxs-lookup"><span data-stu-id="e5481-348">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="e5481-349">請注意，您的來源資料表與目標資料表的結構描述不同 (目標資料表有一個具有身分識別的額外資料行)。</span><span class="sxs-lookup"><span data-stu-id="e5481-349">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="e5481-350">在此案例中，您必須在目標資料集定義中指定 **structure** 屬性，這不包含身分識別資料行。</span><span class="sxs-lookup"><span data-stu-id="e5481-350">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="e5481-351">從 SQL 接收器叫用預存程序</span><span class="sxs-lookup"><span data-stu-id="e5481-351">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="e5481-352">如需在管線的複製活動中從 SQL 接收器叫用預存程序的範例，請參閱[在複製活動中叫用 SQL 接收器的預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)一文。</span><span class="sxs-lookup"><span data-stu-id="e5481-352">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="e5481-353">SQL Server 的類型對應</span><span class="sxs-lookup"><span data-stu-id="e5481-353">Type mapping for SQL server</span></span>
<span data-ttu-id="e5481-354">如同 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，「複製活動」會藉由含有下列 2 個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="e5481-354">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="e5481-355">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="e5481-355">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="e5481-356">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="e5481-356">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="e5481-357">從 SQL Server 來回移動資料時，會使用下列從 SQL 類型到 .NET 類型的對應，以及反向的對應。</span><span class="sxs-lookup"><span data-stu-id="e5481-357">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="e5481-358">此對應與 ADO.NET 的 SQL Server 資料類型對應相同。</span><span class="sxs-lookup"><span data-stu-id="e5481-358">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="e5481-359">SQL Server Database Engine 類型</span><span class="sxs-lookup"><span data-stu-id="e5481-359">SQL Server Database Engine type</span></span> | <span data-ttu-id="e5481-360">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="e5481-360">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="e5481-361">bigint</span><span class="sxs-lookup"><span data-stu-id="e5481-361">bigint</span></span> |<span data-ttu-id="e5481-362">Int64</span><span class="sxs-lookup"><span data-stu-id="e5481-362">Int64</span></span> |
| <span data-ttu-id="e5481-363">binary</span><span class="sxs-lookup"><span data-stu-id="e5481-363">binary</span></span> |<span data-ttu-id="e5481-364">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e5481-364">Byte[]</span></span> |
| <span data-ttu-id="e5481-365">bit</span><span class="sxs-lookup"><span data-stu-id="e5481-365">bit</span></span> |<span data-ttu-id="e5481-366">Boolean</span><span class="sxs-lookup"><span data-stu-id="e5481-366">Boolean</span></span> |
| <span data-ttu-id="e5481-367">char</span><span class="sxs-lookup"><span data-stu-id="e5481-367">char</span></span> |<span data-ttu-id="e5481-368">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="e5481-368">String, Char[]</span></span> |
| <span data-ttu-id="e5481-369">日期</span><span class="sxs-lookup"><span data-stu-id="e5481-369">date</span></span> |<span data-ttu-id="e5481-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="e5481-370">DateTime</span></span> |
| <span data-ttu-id="e5481-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="e5481-371">Datetime</span></span> |<span data-ttu-id="e5481-372">DateTime</span><span class="sxs-lookup"><span data-stu-id="e5481-372">DateTime</span></span> |
| <span data-ttu-id="e5481-373">datetime2</span><span class="sxs-lookup"><span data-stu-id="e5481-373">datetime2</span></span> |<span data-ttu-id="e5481-374">DateTime</span><span class="sxs-lookup"><span data-stu-id="e5481-374">DateTime</span></span> |
| <span data-ttu-id="e5481-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="e5481-375">Datetimeoffset</span></span> |<span data-ttu-id="e5481-376">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="e5481-376">DateTimeOffset</span></span> |
| <span data-ttu-id="e5481-377">十進位</span><span class="sxs-lookup"><span data-stu-id="e5481-377">Decimal</span></span> |<span data-ttu-id="e5481-378">十進位</span><span class="sxs-lookup"><span data-stu-id="e5481-378">Decimal</span></span> |
| <span data-ttu-id="e5481-379">FILESTREAM 屬性 (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="e5481-379">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="e5481-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e5481-380">Byte[]</span></span> |
| <span data-ttu-id="e5481-381">Float</span><span class="sxs-lookup"><span data-stu-id="e5481-381">Float</span></span> |<span data-ttu-id="e5481-382">兩倍</span><span class="sxs-lookup"><span data-stu-id="e5481-382">Double</span></span> |
| <span data-ttu-id="e5481-383">image</span><span class="sxs-lookup"><span data-stu-id="e5481-383">image</span></span> |<span data-ttu-id="e5481-384">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e5481-384">Byte[]</span></span> |
| <span data-ttu-id="e5481-385">int</span><span class="sxs-lookup"><span data-stu-id="e5481-385">int</span></span> |<span data-ttu-id="e5481-386">Int32</span><span class="sxs-lookup"><span data-stu-id="e5481-386">Int32</span></span> |
| <span data-ttu-id="e5481-387">money</span><span class="sxs-lookup"><span data-stu-id="e5481-387">money</span></span> |<span data-ttu-id="e5481-388">十進位</span><span class="sxs-lookup"><span data-stu-id="e5481-388">Decimal</span></span> |
| <span data-ttu-id="e5481-389">nchar</span><span class="sxs-lookup"><span data-stu-id="e5481-389">nchar</span></span> |<span data-ttu-id="e5481-390">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="e5481-390">String, Char[]</span></span> |
| <span data-ttu-id="e5481-391">ntext</span><span class="sxs-lookup"><span data-stu-id="e5481-391">ntext</span></span> |<span data-ttu-id="e5481-392">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="e5481-392">String, Char[]</span></span> |
| <span data-ttu-id="e5481-393">numeric</span><span class="sxs-lookup"><span data-stu-id="e5481-393">numeric</span></span> |<span data-ttu-id="e5481-394">十進位</span><span class="sxs-lookup"><span data-stu-id="e5481-394">Decimal</span></span> |
| <span data-ttu-id="e5481-395">nvarchar</span><span class="sxs-lookup"><span data-stu-id="e5481-395">nvarchar</span></span> |<span data-ttu-id="e5481-396">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="e5481-396">String, Char[]</span></span> |
| <span data-ttu-id="e5481-397">real</span><span class="sxs-lookup"><span data-stu-id="e5481-397">real</span></span> |<span data-ttu-id="e5481-398">單一</span><span class="sxs-lookup"><span data-stu-id="e5481-398">Single</span></span> |
| <span data-ttu-id="e5481-399">rowversion</span><span class="sxs-lookup"><span data-stu-id="e5481-399">rowversion</span></span> |<span data-ttu-id="e5481-400">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e5481-400">Byte[]</span></span> |
| <span data-ttu-id="e5481-401">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="e5481-401">smalldatetime</span></span> |<span data-ttu-id="e5481-402">DateTime</span><span class="sxs-lookup"><span data-stu-id="e5481-402">DateTime</span></span> |
| <span data-ttu-id="e5481-403">smallint</span><span class="sxs-lookup"><span data-stu-id="e5481-403">smallint</span></span> |<span data-ttu-id="e5481-404">Int16</span><span class="sxs-lookup"><span data-stu-id="e5481-404">Int16</span></span> |
| <span data-ttu-id="e5481-405">smallmoney</span><span class="sxs-lookup"><span data-stu-id="e5481-405">smallmoney</span></span> |<span data-ttu-id="e5481-406">十進位</span><span class="sxs-lookup"><span data-stu-id="e5481-406">Decimal</span></span> |
| <span data-ttu-id="e5481-407">sql_variant</span><span class="sxs-lookup"><span data-stu-id="e5481-407">sql_variant</span></span> |<span data-ttu-id="e5481-408">物件 *</span><span class="sxs-lookup"><span data-stu-id="e5481-408">Object *</span></span> |
| <span data-ttu-id="e5481-409">文字</span><span class="sxs-lookup"><span data-stu-id="e5481-409">text</span></span> |<span data-ttu-id="e5481-410">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="e5481-410">String, Char[]</span></span> |
| <span data-ttu-id="e5481-411">分析</span><span class="sxs-lookup"><span data-stu-id="e5481-411">time</span></span> |<span data-ttu-id="e5481-412">時間範圍</span><span class="sxs-lookup"><span data-stu-id="e5481-412">TimeSpan</span></span> |
| <span data-ttu-id="e5481-413">timestamp</span><span class="sxs-lookup"><span data-stu-id="e5481-413">timestamp</span></span> |<span data-ttu-id="e5481-414">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e5481-414">Byte[]</span></span> |
| <span data-ttu-id="e5481-415">tinyint</span><span class="sxs-lookup"><span data-stu-id="e5481-415">tinyint</span></span> |<span data-ttu-id="e5481-416">位元組</span><span class="sxs-lookup"><span data-stu-id="e5481-416">Byte</span></span> |
| <span data-ttu-id="e5481-417">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="e5481-417">uniqueidentifier</span></span> |<span data-ttu-id="e5481-418">Guid</span><span class="sxs-lookup"><span data-stu-id="e5481-418">Guid</span></span> |
| <span data-ttu-id="e5481-419">varbinary</span><span class="sxs-lookup"><span data-stu-id="e5481-419">varbinary</span></span> |<span data-ttu-id="e5481-420">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e5481-420">Byte[]</span></span> |
| <span data-ttu-id="e5481-421">varchar</span><span class="sxs-lookup"><span data-stu-id="e5481-421">varchar</span></span> |<span data-ttu-id="e5481-422">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="e5481-422">String, Char[]</span></span> |
| <span data-ttu-id="e5481-423">xml</span><span class="sxs-lookup"><span data-stu-id="e5481-423">xml</span></span> |<span data-ttu-id="e5481-424">xml</span><span class="sxs-lookup"><span data-stu-id="e5481-424">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="e5481-425">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="e5481-425">Mapping source to sink columns</span></span>
<span data-ttu-id="e5481-426">若要將來自來源資料集的資料行與來自接收資料集的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="e5481-426">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="e5481-427">可重複複製</span><span class="sxs-lookup"><span data-stu-id="e5481-427">Repeatable copy</span></span>
<span data-ttu-id="e5481-428">將資料複製到 SQL Server 資料庫時，複製活動預設會將資料附加至接收資料表。</span><span class="sxs-lookup"><span data-stu-id="e5481-428">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="e5481-429">若要改為執行 UPSERT，請參閱[對 SqlSink 進行可重複的寫入](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink)一文。</span><span class="sxs-lookup"><span data-stu-id="e5481-429">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="e5481-430">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="e5481-430">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="e5481-431">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="e5481-431">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e5481-432">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="e5481-432">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e5481-433">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="e5481-433">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e5481-434">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="e5481-434">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e5481-435">效能和微調</span><span class="sxs-lookup"><span data-stu-id="e5481-435">Performance and Tuning</span></span>
<span data-ttu-id="e5481-436">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="e5481-436">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
