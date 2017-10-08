---
title: "從 SQL Server aaaMove 資料 tooand |Microsoft 文件"
description: "了解有關如何 toomove 資料至 azure 或從 SQL Server 資料庫也就是在內部部署或 Azure VM 使用 Azure Data Factory 中。"
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
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="eccc6-103">移動資料 tooand 從 SQL Server 內部或 IaaS (Azure VM) 上使用 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="eccc6-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="eccc6-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 SQL Server 資料庫中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="eccc6-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="eccc6-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="eccc6-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="eccc6-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="eccc6-106">Supported scenarios</span></span>
<span data-ttu-id="eccc6-107">您可以將資料複製**從 SQL Server 資料庫**toohello 下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="eccc6-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="eccc6-108">您可以將資料複製下列資料存放區的 hello **tooa SQL Server 資料庫**:</span><span class="sxs-lookup"><span data-stu-id="eccc6-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="eccc6-109">支援的 SQL Server 版本</span><span class="sxs-lookup"><span data-stu-id="eccc6-109">Supported SQL Server versions</span></span>
<span data-ttu-id="eccc6-110">複製資料，從這個 SQL Server 連接器支援 / toohello 下列版本的執行個體裝載內部或在使用 SQL 驗證和 Windows 驗證的 Azure IaaS 中： SQL Server 2016、 SQL Server 2014、 SQL Server 2012、 SQL Server 2008 R2、 SQLServer 2008、 SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="eccc6-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="eccc6-111">啟用連線</span><span class="sxs-lookup"><span data-stu-id="eccc6-111">Enabling connectivity</span></span>
<span data-ttu-id="eccc6-112">hello 概念及所需的 Vm （基礎結構做為服務） 連線與 SQL Server 裝載內部或在 Azure IaaS 中的步驟是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="eccc6-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="eccc6-113">在這兩種情況下，您需要連線 toouse 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="eccc6-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="eccc6-114">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="eccc6-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="eccc6-115">設定閘道器執行個體是與 SQL Server 連線的必要條件。</span><span class="sxs-lookup"><span data-stu-id="eccc6-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="eccc6-116">您可以安裝閘道時 hello 相同上內部機器或雲端的 VM 執行個體為 SQL Server hello 以提升效能，我們建議您安裝它們在不同電腦上。</span><span class="sxs-lookup"><span data-stu-id="eccc6-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="eccc6-117">在不同電腦上擁有 hello 閘道和 SQL Server 會減少資源競爭。</span><span class="sxs-lookup"><span data-stu-id="eccc6-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="eccc6-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="eccc6-118">Getting started</span></span>
<span data-ttu-id="eccc6-119">您可以建立內含複製活動的管線，使用不同的工具/API 將資料移進/移出內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="eccc6-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="eccc6-120">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="eccc6-121">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="eccc6-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="eccc6-122">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="eccc6-123">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="eccc6-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="eccc6-124">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="eccc6-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="eccc6-125">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-125">Create a **data factory**.</span></span> <span data-ttu-id="eccc6-126">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="eccc6-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="eccc6-127">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="eccc6-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="eccc6-128">例如，如果您從 Azure blob 儲存體的 SQL Server 資料庫 tooan 複製資料，您建立兩個連結的服務 toolink 您 SQL Server 資料庫和 Azure 儲存體帳戶 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="eccc6-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="eccc6-129">對於特定 tooSQL Server 資料庫的連結的服務屬性，請參閱[連結服務屬性](#linked-service-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="eccc6-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="eccc6-130">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="eccc6-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="eccc6-131">在 hello hello 最後一個步驟中所述的範例，您可以建立資料集 toospecify hello SQL 資料表包含 hello 輸入的資料在 SQL Server 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="eccc6-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="eccc6-132">建立另一個資料集 toospecify hello blob 容器及保存 hello 資料 hello 資料夾 hello 從 SQL Server 資料庫複製。</span><span class="sxs-lookup"><span data-stu-id="eccc6-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="eccc6-133">對於特定 tooSQL Server 資料庫的資料集屬性，請參閱[資料集屬性](#dataset-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="eccc6-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="eccc6-134">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="eccc6-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="eccc6-135">在先前所述 hello 範例中，您使用 SqlSource 作為來源和 BlobSink 做為接收器 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="eccc6-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="eccc6-136">同樣地，如果您要從 Azure Blob 儲存體 tooSQL 伺服器資料庫複製，則使用 BlobSource 和 SqlSink 的 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="eccc6-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="eccc6-137">複製活動是特定 tooSQL 伺服器資料庫的內容，請參閱[複製活動屬性](#copy-activity-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="eccc6-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="eccc6-138">如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。</span><span class="sxs-lookup"><span data-stu-id="eccc6-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="eccc6-139">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="eccc6-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="eccc6-140">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="eccc6-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="eccc6-141">如需使用的 toocopy 資料，從內部部署 SQL Server 資料庫的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-from-and-to-sql-server)本文一節。</span><span class="sxs-lookup"><span data-stu-id="eccc6-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="eccc6-142">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooSQL 伺服器的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="eccc6-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="eccc6-143">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="eccc6-143">Linked service properties</span></span>
<span data-ttu-id="eccc6-144">您建立連結的服務型別的**OnPremisesSqlServer** toolink 在內部部署 SQL Server 資料庫 tooa 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="eccc6-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="eccc6-145">下表中的 hello 提供 JSON 項目特定 tooon 內部部署 SQL Server 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="eccc6-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="eccc6-146">下表中的 hello 提供 JSON 項目特定 tooSQL 連結的伺服器服務的描述。</span><span class="sxs-lookup"><span data-stu-id="eccc6-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="eccc6-147">屬性</span><span class="sxs-lookup"><span data-stu-id="eccc6-147">Property</span></span> | <span data-ttu-id="eccc6-148">說明</span><span class="sxs-lookup"><span data-stu-id="eccc6-148">Description</span></span> | <span data-ttu-id="eccc6-149">必要</span><span class="sxs-lookup"><span data-stu-id="eccc6-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eccc6-150">類型</span><span class="sxs-lookup"><span data-stu-id="eccc6-150">type</span></span> |<span data-ttu-id="eccc6-151">hello 類型屬性應該設定為： **OnPremisesSqlServer**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="eccc6-152">是</span><span class="sxs-lookup"><span data-stu-id="eccc6-152">Yes</span></span> |
| <span data-ttu-id="eccc6-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="eccc6-153">connectionString</span></span> |<span data-ttu-id="eccc6-154">指定所需的 connectionString 資訊 tooconnect toohello 在內部部署 SQL Server 資料庫使用 SQL 驗證或 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="eccc6-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="eccc6-155">是</span><span class="sxs-lookup"><span data-stu-id="eccc6-155">Yes</span></span> |
| <span data-ttu-id="eccc6-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="eccc6-156">gatewayName</span></span> |<span data-ttu-id="eccc6-157">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="eccc6-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="eccc6-158">是</span><span class="sxs-lookup"><span data-stu-id="eccc6-158">Yes</span></span> |
| <span data-ttu-id="eccc6-159">username</span><span class="sxs-lookup"><span data-stu-id="eccc6-159">username</span></span> |<span data-ttu-id="eccc6-160">如果您使用「Windows 驗證」，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="eccc6-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="eccc6-161">範例︰**domainname\\username**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="eccc6-162">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-162">No</span></span> |
| <span data-ttu-id="eccc6-163">password</span><span class="sxs-lookup"><span data-stu-id="eccc6-163">password</span></span> |<span data-ttu-id="eccc6-164">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="eccc6-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="eccc6-165">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-165">No</span></span> |

<span data-ttu-id="eccc6-166">您可以加密認證使用 hello**新增 AzureRmDataFactoryEncryptValue** cmdlet 並將其用於 hello 連接字串 hello 下列範例所示 (**EncryptedCredential**屬性):</span><span class="sxs-lookup"><span data-stu-id="eccc6-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="eccc6-167">範例</span><span class="sxs-lookup"><span data-stu-id="eccc6-167">Samples</span></span>
<span data-ttu-id="eccc6-168">**使用 SQL 驗證的 JSON**</span><span class="sxs-lookup"><span data-stu-id="eccc6-168">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="eccc6-169">**使用 Windows 驗證的 JSON**</span><span class="sxs-lookup"><span data-stu-id="eccc6-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="eccc6-170">資料管理閘道會模擬 hello 指定使用者帳戶 tooconnect toohello 在內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="eccc6-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="eccc6-171">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="eccc6-171">Dataset properties</span></span>
<span data-ttu-id="eccc6-172">在 hello 範例中，您已使用的型別資料集**SqlServerTable** toorepresent SQL Server 資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="eccc6-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="eccc6-173">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="eccc6-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="eccc6-174">所有資料集類型 (SQL Server、Azure Blob、Azure 資料表等) 的資料集 JSON 區段 (例如 structure、availability 及 policy) 都相似。</span><span class="sxs-lookup"><span data-stu-id="eccc6-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="eccc6-175">hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="eccc6-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="eccc6-176">hello **typeProperties** hello 資料集的類型 > 一節**SqlServerTable**具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="eccc6-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="eccc6-177">屬性</span><span class="sxs-lookup"><span data-stu-id="eccc6-177">Property</span></span> | <span data-ttu-id="eccc6-178">說明</span><span class="sxs-lookup"><span data-stu-id="eccc6-178">Description</span></span> | <span data-ttu-id="eccc6-179">必要</span><span class="sxs-lookup"><span data-stu-id="eccc6-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eccc6-180">tableName</span><span class="sxs-lookup"><span data-stu-id="eccc6-180">tableName</span></span> |<span data-ttu-id="eccc6-181">參照 hello 資料表或檢視中的連結服務的 hello 的 SQL Server 資料庫執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="eccc6-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="eccc6-182">是</span><span class="sxs-lookup"><span data-stu-id="eccc6-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="eccc6-183">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="eccc6-183">Copy activity properties</span></span>
<span data-ttu-id="eccc6-184">如果您要移動的資料從 SQL Server 資料庫，您設定 hello 來源類型 hello 複製活動中太**SqlSource**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="eccc6-185">同樣地，如果您要移動資料 tooa SQL Server 資料庫，您設定 hello 接收器類型 hello 複製活動中太**SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="eccc6-186">本節提供 SqlSource 和 SqlSink 支援的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="eccc6-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="eccc6-187">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="eccc6-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="eccc6-188">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="eccc6-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="eccc6-189">hello 複製活動會採用只有 1 個輸入，並產生一個輸出。</span><span class="sxs-lookup"><span data-stu-id="eccc6-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="eccc6-190">而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="eccc6-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="eccc6-191">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="eccc6-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="eccc6-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="eccc6-192">SqlSource</span></span>
<span data-ttu-id="eccc6-193">複製活動中的來源時的型別**SqlSource**中的下列屬性的 hello 可用**typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="eccc6-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="eccc6-194">屬性</span><span class="sxs-lookup"><span data-stu-id="eccc6-194">Property</span></span> | <span data-ttu-id="eccc6-195">說明</span><span class="sxs-lookup"><span data-stu-id="eccc6-195">Description</span></span> | <span data-ttu-id="eccc6-196">允許的值</span><span class="sxs-lookup"><span data-stu-id="eccc6-196">Allowed values</span></span> | <span data-ttu-id="eccc6-197">必要</span><span class="sxs-lookup"><span data-stu-id="eccc6-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eccc6-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="eccc6-198">sqlReaderQuery</span></span> |<span data-ttu-id="eccc6-199">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="eccc6-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="eccc6-200">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="eccc6-200">SQL query string.</span></span> <span data-ttu-id="eccc6-201">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="eccc6-201">For example: select * from MyTable.</span></span> <span data-ttu-id="eccc6-202">從 hello hello 輸入資料集所參考的資料庫，可以參考多個資料表。</span><span class="sxs-lookup"><span data-stu-id="eccc6-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="eccc6-203">如果未指定，hello 執行的 SQL 陳述式： select from MyTable。</span><span class="sxs-lookup"><span data-stu-id="eccc6-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="eccc6-204">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-204">No</span></span> |
| <span data-ttu-id="eccc6-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="eccc6-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="eccc6-206">名稱的 hello 預存程序會從 hello 來源資料表讀取資料。</span><span class="sxs-lookup"><span data-stu-id="eccc6-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="eccc6-207">名稱的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="eccc6-207">Name of hello stored procedure.</span></span> <span data-ttu-id="eccc6-208">hello 最後一個 SQL 陳述式必須在 hello 預存程序中的 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="eccc6-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="eccc6-209">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-209">No</span></span> |
| <span data-ttu-id="eccc6-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="eccc6-210">storedProcedureParameters</span></span> |<span data-ttu-id="eccc6-211">Hello 參數，預存程序。</span><span class="sxs-lookup"><span data-stu-id="eccc6-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="eccc6-212">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="eccc6-212">Name/value pairs.</span></span> <span data-ttu-id="eccc6-213">名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。</span><span class="sxs-lookup"><span data-stu-id="eccc6-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="eccc6-214">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-214">No</span></span> |

<span data-ttu-id="eccc6-215">如果 hello **sqlReaderQuery**指定 hello SqlSource，hello 複製活動會針對 hello 的 SQL Server 資料庫來源 tooget hello 資料執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="eccc6-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="eccc6-216">或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。</span><span class="sxs-lookup"><span data-stu-id="eccc6-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="eccc6-217">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 結構區段中定義的資料行是使用的 toobuild select 查詢 toorun 針對 hello 的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="eccc6-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="eccc6-218">如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="eccc6-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="eccc6-219">當您使用**sqlReaderStoredProcedureName**，您仍然需要 toospecify 值 hello **tableName** hello 資料集 JSON 中的屬性。</span><span class="sxs-lookup"><span data-stu-id="eccc6-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="eccc6-220">雖然目前尚未針對此資料表來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="eccc6-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="eccc6-221">管線</span><span class="sxs-lookup"><span data-stu-id="eccc6-221">SqlSink</span></span>
<span data-ttu-id="eccc6-222">**SqlSink**支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="eccc6-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="eccc6-223">屬性</span><span class="sxs-lookup"><span data-stu-id="eccc6-223">Property</span></span> | <span data-ttu-id="eccc6-224">說明</span><span class="sxs-lookup"><span data-stu-id="eccc6-224">Description</span></span> | <span data-ttu-id="eccc6-225">允許的值</span><span class="sxs-lookup"><span data-stu-id="eccc6-225">Allowed values</span></span> | <span data-ttu-id="eccc6-226">必要</span><span class="sxs-lookup"><span data-stu-id="eccc6-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eccc6-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="eccc6-227">writeBatchTimeout</span></span> |<span data-ttu-id="eccc6-228">在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。</span><span class="sxs-lookup"><span data-stu-id="eccc6-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="eccc6-229">時間範圍</span><span class="sxs-lookup"><span data-stu-id="eccc6-229">timespan</span></span><br/><br/> <span data-ttu-id="eccc6-230">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="eccc6-231">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-231">No</span></span> |
| <span data-ttu-id="eccc6-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="eccc6-232">writeBatchSize</span></span> |<span data-ttu-id="eccc6-233">當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="eccc6-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="eccc6-234">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="eccc6-234">Integer (number of rows)</span></span> |<span data-ttu-id="eccc6-235">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="eccc6-235">No (default: 10000)</span></span> |
| <span data-ttu-id="eccc6-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="eccc6-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="eccc6-237">複製活動 tooexecute 查詢指定的特定配量的資料清除。</span><span class="sxs-lookup"><span data-stu-id="eccc6-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="eccc6-238">如需詳細資訊，請參閱[可重複複製](#repeatable-copy)一節。</span><span class="sxs-lookup"><span data-stu-id="eccc6-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="eccc6-239">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="eccc6-239">A query statement.</span></span> |<span data-ttu-id="eccc6-240">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-240">No</span></span> |
| <span data-ttu-id="eccc6-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="eccc6-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="eccc6-242">指定資料行名稱複製活動 toofill 與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。</span><span class="sxs-lookup"><span data-stu-id="eccc6-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="eccc6-243">如需詳細資訊，請參閱[可重複複製](#repeatable-copy)一節。</span><span class="sxs-lookup"><span data-stu-id="eccc6-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="eccc6-244">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="eccc6-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="eccc6-245">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-245">No</span></span> |
| <span data-ttu-id="eccc6-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="eccc6-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="eccc6-247">名稱的 hello 預存程序 upserts （更新/插入） 資料到 hello 目標資料表。</span><span class="sxs-lookup"><span data-stu-id="eccc6-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="eccc6-248">名稱的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="eccc6-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="eccc6-249">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-249">No</span></span> |
| <span data-ttu-id="eccc6-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="eccc6-250">storedProcedureParameters</span></span> |<span data-ttu-id="eccc6-251">Hello 參數，預存程序。</span><span class="sxs-lookup"><span data-stu-id="eccc6-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="eccc6-252">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="eccc6-252">Name/value pairs.</span></span> <span data-ttu-id="eccc6-253">名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。</span><span class="sxs-lookup"><span data-stu-id="eccc6-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="eccc6-254">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-254">No</span></span> |
| <span data-ttu-id="eccc6-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="eccc6-255">sqlWriterTableType</span></span> |<span data-ttu-id="eccc6-256">指定資料表類型名稱 toobe hello 預存程序中使用。</span><span class="sxs-lookup"><span data-stu-id="eccc6-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="eccc6-257">複製活動移動 hello 資料可讓在暫存資料表與此資料表類型。</span><span class="sxs-lookup"><span data-stu-id="eccc6-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="eccc6-258">預存程序程式碼可以再合併 hello 資料會被複製現有的資料。</span><span class="sxs-lookup"><span data-stu-id="eccc6-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="eccc6-259">資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="eccc6-259">A table type name.</span></span> |<span data-ttu-id="eccc6-260">否</span><span class="sxs-lookup"><span data-stu-id="eccc6-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="eccc6-261">用來複製資料與 tooSQL 伺服器 JSON 範例</span><span class="sxs-lookup"><span data-stu-id="eccc6-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="eccc6-262">hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="eccc6-263">hello 下列範例顯示如何從 SQL Server 和 Azure Blob 儲存體 toocopy 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="eccc6-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="eccc6-264">不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="eccc6-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="eccc6-265">範例： 從 SQL Server tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="eccc6-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="eccc6-266">下列範例會示範 hello:</span><span class="sxs-lookup"><span data-stu-id="eccc6-266">hello following sample shows:</span></span>

1. <span data-ttu-id="eccc6-267">[OnPremisesSqlServer](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="eccc6-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="eccc6-268">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="eccc6-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="eccc6-269">[SqlServerTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="eccc6-270">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="eccc6-271">hello[管線](data-factory-create-pipelines.md)與使用複製活動[SqlSource](#copy-activity-properties)和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="eccc6-272">hello 範例將時間序列資料從 SQL Server 資料表 tooan Azure blob 的每個小時。</span><span class="sxs-lookup"><span data-stu-id="eccc6-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="eccc6-273">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="eccc6-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="eccc6-274">第一個步驟中，安裝程式 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="eccc6-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="eccc6-275">hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="eccc6-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="eccc6-276">**SQL Server 連結服務**</span><span class="sxs-lookup"><span data-stu-id="eccc6-276">**SQL Server linked service**</span></span>
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
<span data-ttu-id="eccc6-277">**Azure Blob 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="eccc6-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="eccc6-278">**SQL Server 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="eccc6-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="eccc6-279">hello 範例假設您已建立資料表"MyTable"SQL Server 中，而且包含稱為"timestampcolumn 「 時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="eccc6-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="eccc6-280">您可以透過 hello hello 資料集的 tableName typeProperty 必須使用相同的資料庫，使用單一資料集，但單一資料表內的多個資料表進行查詢。</span><span class="sxs-lookup"><span data-stu-id="eccc6-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="eccc6-281">設定"external":"true"會通知 Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="eccc6-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="eccc6-282">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="eccc6-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="eccc6-283">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="eccc6-284">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="eccc6-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="eccc6-285">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="eccc6-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="eccc6-286">**具有複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="eccc6-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="eccc6-287">hello 管線包含複製活動的設定的 toouse 這些輸入和輸出資料集，而排程的 toorun 每小時。</span><span class="sxs-lookup"><span data-stu-id="eccc6-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="eccc6-288">在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="eccc6-289">指定 hello SQL 查詢**SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="eccc6-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
<span data-ttu-id="eccc6-290">在此範例中， **sqlReaderQuery** hello SqlSource 指定。</span><span class="sxs-lookup"><span data-stu-id="eccc6-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="eccc6-291">hello 複製活動會針對 hello 的 SQL Server 資料庫來源 tooget hello 資料執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="eccc6-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="eccc6-292">或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。</span><span class="sxs-lookup"><span data-stu-id="eccc6-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="eccc6-293">hello sqlReaderQuery 參考 hello hello 輸入資料集所參考的資料庫內的多個資料表。</span><span class="sxs-lookup"><span data-stu-id="eccc6-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="eccc6-294">它不是設定為 hello 資料集的 tableName typeProperty 有限的 tooonly hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="eccc6-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="eccc6-295">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 結構區段中定義的資料行是使用的 toobuild select 查詢 toorun 針對 hello 的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="eccc6-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="eccc6-296">如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="eccc6-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="eccc6-297">請參閱 hello [Sql 來源](#sqlsource)區段和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello 支援 SqlSource 和 BlobSink 屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="eccc6-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="eccc6-298">範例： 將資料從 Azure Blob tooSQL Server 複製</span><span class="sxs-lookup"><span data-stu-id="eccc6-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="eccc6-299">下列範例會示範 hello:</span><span class="sxs-lookup"><span data-stu-id="eccc6-299">hello following sample shows:</span></span>

1. <span data-ttu-id="eccc6-300">hello 連結類型的服務[OnPremisesSqlServer](#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="eccc6-301">hello 連結類型的服務[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="eccc6-302">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="eccc6-303">[SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="eccc6-304">hello[管線](data-factory-create-pipelines.md)與使用複製活動[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties)和[SqlSink](#sql-server-copy-activity-type-properties)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="eccc6-305">hello 範例複製時間序列資料從 Azure blob tooa SQL Server 資料表的每個小時。</span><span class="sxs-lookup"><span data-stu-id="eccc6-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="eccc6-306">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="eccc6-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="eccc6-307">**SQL Server 連結服務**</span><span class="sxs-lookup"><span data-stu-id="eccc6-307">**SQL Server linked service**</span></span>

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
<span data-ttu-id="eccc6-308">**Azure Blob 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="eccc6-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="eccc6-309">**Azure Blob 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="eccc6-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="eccc6-310">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="eccc6-311">hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="eccc6-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="eccc6-312">年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="eccc6-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="eccc6-313">"external":"true"的設定會在該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="eccc6-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="eccc6-314">**SQL Server 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="eccc6-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="eccc6-315">hello 範例會將名為"MyTable"SQL Server 中的資料 tooa 資料表複製。</span><span class="sxs-lookup"><span data-stu-id="eccc6-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="eccc6-316">建立與 SQL Server 中的 hello 資料表如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。</span><span class="sxs-lookup"><span data-stu-id="eccc6-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="eccc6-317">新的資料列會加入 toohello 資料表的每個小時。</span><span class="sxs-lookup"><span data-stu-id="eccc6-317">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="eccc6-318">**具有複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="eccc6-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="eccc6-319">hello 管線包含複製活動的設定的 toouse 這些輸入和輸出資料集，而排程的 toorun 每小時。</span><span class="sxs-lookup"><span data-stu-id="eccc6-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="eccc6-320">在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="eccc6-321">疑難排解連線問題</span><span class="sxs-lookup"><span data-stu-id="eccc6-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="eccc6-322">設定 SQL Server tooaccept 的遠端連線。</span><span class="sxs-lookup"><span data-stu-id="eccc6-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="eccc6-323">啟動 [SQL Server Management Studio]、用滑鼠右鍵按一下 [伺服器]，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="eccc6-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="eccc6-324">選取**連線**hello 清單和核取**允許遠端連接 toohello 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![啟用遠端連線](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="eccc6-326">請參閱[設定 hello remote access 伺服器組態選項](https://msdn.microsoft.com/library/ms191464.aspx)如需詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="eccc6-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="eccc6-327">啟動 [SQL Server 組態管理員] 。</span><span class="sxs-lookup"><span data-stu-id="eccc6-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="eccc6-328">展開**SQL Server 網路組態**hello 的執行個體和選取**MSSQLSERVER 的通訊協定**。</span><span class="sxs-lookup"><span data-stu-id="eccc6-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="eccc6-329">您應該會看到 hello 右窗格中的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="eccc6-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="eccc6-330">用滑鼠右鍵按一下 [TCP/IP]，然後按一下 [啟用] 來啟用 TCP/IP。</span><span class="sxs-lookup"><span data-stu-id="eccc6-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![啟用 TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="eccc6-332">如需啟用 TCP/IP 通訊協定的詳細資料及替代方式，請參閱 [啟用或停用伺服器網路通訊協定](https://msdn.microsoft.com/library/ms191294.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="eccc6-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="eccc6-333">在 hello 相同的視窗中按兩下**TCP/IP** toolaunch **TCP/IP 內容**視窗。</span><span class="sxs-lookup"><span data-stu-id="eccc6-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="eccc6-334">切換 toohello **IP 位址** 索引標籤。捲動 toosee **IPAll** > 一節。</span><span class="sxs-lookup"><span data-stu-id="eccc6-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="eccc6-335">記下 hello * * TCP 連接埠 * * (預設值是**1433年**)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="eccc6-336">建立**hello Windows 防火牆規則**上透過此連接埠的 hello 機器 tooallow 連入流量。</span><span class="sxs-lookup"><span data-stu-id="eccc6-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="eccc6-337">**請確認連接**: tooconnect toohello 使用完整限定的名稱，SQL Server 使用 SQL Server Management Studio 從不同的電腦。</span><span class="sxs-lookup"><span data-stu-id="eccc6-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="eccc6-338">例如："<machine><domain>.corp<company>.com,1433"。</span><span class="sxs-lookup"><span data-stu-id="eccc6-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="eccc6-339">請參閱[在內部部署來源和資料管理閘道與 hello 雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="eccc6-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="eccc6-340">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="eccc6-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="eccc6-341">Hello 目標資料庫中的識別資料行</span><span class="sxs-lookup"><span data-stu-id="eccc6-341">Identity columns in hello target database</span></span>
<span data-ttu-id="eccc6-342">本章節提供的範例，但沒有識別資料行 tooa 目的地資料表之 identity 資料行的來源資料表中的資料複製。</span><span class="sxs-lookup"><span data-stu-id="eccc6-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="eccc6-343">**來源資料表：**</span><span class="sxs-lookup"><span data-stu-id="eccc6-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="eccc6-344">**目的地資料表：**</span><span class="sxs-lookup"><span data-stu-id="eccc6-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="eccc6-345">請注意該 hello 目標資料表有識別資料行。</span><span class="sxs-lookup"><span data-stu-id="eccc6-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="eccc6-346">**來源資料集 JSON 定義**</span><span class="sxs-lookup"><span data-stu-id="eccc6-346">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="eccc6-347">**目的地資料集 JSON 定義**</span><span class="sxs-lookup"><span data-stu-id="eccc6-347">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="eccc6-348">請注意，您的來源資料表與目標資料表的結構描述不同 (目標資料表有一個具有身分識別的額外資料行)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="eccc6-349">在此案例中，您需要 toospecify**結構**hello 目標資料集定義，其中不包括 hello 識別資料行中的屬性。</span><span class="sxs-lookup"><span data-stu-id="eccc6-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="eccc6-350">從 SQL 接收器叫用預存程序</span><span class="sxs-lookup"><span data-stu-id="eccc6-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="eccc6-351">如需在管線的複製活動中從 SQL 接收器叫用預存程序的範例，請參閱[在複製活動中叫用 SQL 接收器的預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)一文。</span><span class="sxs-lookup"><span data-stu-id="eccc6-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="eccc6-352">SQL Server 的類型對應</span><span class="sxs-lookup"><span data-stu-id="eccc6-352">Type mapping for SQL server</span></span>
<span data-ttu-id="eccc6-353">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會執行自動類型轉換來源類型 toosink 類型以 hello 遵循 2 步驟方法：</span><span class="sxs-lookup"><span data-stu-id="eccc6-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="eccc6-354">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="eccc6-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="eccc6-355">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="eccc6-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="eccc6-356">當資料移動太 & 從 SQL server hello 從 SQL 型別 too.NET 類型，反之亦然，會使用下列的對應。</span><span class="sxs-lookup"><span data-stu-id="eccc6-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="eccc6-357">hello 對應是相同 hello ADO.NET 的 SQL Server 資料類型對應。</span><span class="sxs-lookup"><span data-stu-id="eccc6-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="eccc6-358">SQL Server Database Engine 類型</span><span class="sxs-lookup"><span data-stu-id="eccc6-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="eccc6-359">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="eccc6-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="eccc6-360">bigint</span><span class="sxs-lookup"><span data-stu-id="eccc6-360">bigint</span></span> |<span data-ttu-id="eccc6-361">Int64</span><span class="sxs-lookup"><span data-stu-id="eccc6-361">Int64</span></span> |
| <span data-ttu-id="eccc6-362">binary</span><span class="sxs-lookup"><span data-stu-id="eccc6-362">binary</span></span> |<span data-ttu-id="eccc6-363">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-363">Byte[]</span></span> |
| <span data-ttu-id="eccc6-364">bit</span><span class="sxs-lookup"><span data-stu-id="eccc6-364">bit</span></span> |<span data-ttu-id="eccc6-365">Boolean</span><span class="sxs-lookup"><span data-stu-id="eccc6-365">Boolean</span></span> |
| <span data-ttu-id="eccc6-366">char</span><span class="sxs-lookup"><span data-stu-id="eccc6-366">char</span></span> |<span data-ttu-id="eccc6-367">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-367">String, Char[]</span></span> |
| <span data-ttu-id="eccc6-368">日期</span><span class="sxs-lookup"><span data-stu-id="eccc6-368">date</span></span> |<span data-ttu-id="eccc6-369">DateTime</span><span class="sxs-lookup"><span data-stu-id="eccc6-369">DateTime</span></span> |
| <span data-ttu-id="eccc6-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="eccc6-370">Datetime</span></span> |<span data-ttu-id="eccc6-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="eccc6-371">DateTime</span></span> |
| <span data-ttu-id="eccc6-372">datetime2</span><span class="sxs-lookup"><span data-stu-id="eccc6-372">datetime2</span></span> |<span data-ttu-id="eccc6-373">DateTime</span><span class="sxs-lookup"><span data-stu-id="eccc6-373">DateTime</span></span> |
| <span data-ttu-id="eccc6-374">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="eccc6-374">Datetimeoffset</span></span> |<span data-ttu-id="eccc6-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="eccc6-375">DateTimeOffset</span></span> |
| <span data-ttu-id="eccc6-376">十進位</span><span class="sxs-lookup"><span data-stu-id="eccc6-376">Decimal</span></span> |<span data-ttu-id="eccc6-377">十進位</span><span class="sxs-lookup"><span data-stu-id="eccc6-377">Decimal</span></span> |
| <span data-ttu-id="eccc6-378">FILESTREAM 屬性 (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="eccc6-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="eccc6-379">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-379">Byte[]</span></span> |
| <span data-ttu-id="eccc6-380">Float</span><span class="sxs-lookup"><span data-stu-id="eccc6-380">Float</span></span> |<span data-ttu-id="eccc6-381">兩倍</span><span class="sxs-lookup"><span data-stu-id="eccc6-381">Double</span></span> |
| <span data-ttu-id="eccc6-382">image</span><span class="sxs-lookup"><span data-stu-id="eccc6-382">image</span></span> |<span data-ttu-id="eccc6-383">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-383">Byte[]</span></span> |
| <span data-ttu-id="eccc6-384">int</span><span class="sxs-lookup"><span data-stu-id="eccc6-384">int</span></span> |<span data-ttu-id="eccc6-385">Int32</span><span class="sxs-lookup"><span data-stu-id="eccc6-385">Int32</span></span> |
| <span data-ttu-id="eccc6-386">money</span><span class="sxs-lookup"><span data-stu-id="eccc6-386">money</span></span> |<span data-ttu-id="eccc6-387">十進位</span><span class="sxs-lookup"><span data-stu-id="eccc6-387">Decimal</span></span> |
| <span data-ttu-id="eccc6-388">nchar</span><span class="sxs-lookup"><span data-stu-id="eccc6-388">nchar</span></span> |<span data-ttu-id="eccc6-389">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-389">String, Char[]</span></span> |
| <span data-ttu-id="eccc6-390">ntext</span><span class="sxs-lookup"><span data-stu-id="eccc6-390">ntext</span></span> |<span data-ttu-id="eccc6-391">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-391">String, Char[]</span></span> |
| <span data-ttu-id="eccc6-392">numeric</span><span class="sxs-lookup"><span data-stu-id="eccc6-392">numeric</span></span> |<span data-ttu-id="eccc6-393">十進位</span><span class="sxs-lookup"><span data-stu-id="eccc6-393">Decimal</span></span> |
| <span data-ttu-id="eccc6-394">nvarchar</span><span class="sxs-lookup"><span data-stu-id="eccc6-394">nvarchar</span></span> |<span data-ttu-id="eccc6-395">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-395">String, Char[]</span></span> |
| <span data-ttu-id="eccc6-396">real</span><span class="sxs-lookup"><span data-stu-id="eccc6-396">real</span></span> |<span data-ttu-id="eccc6-397">單一</span><span class="sxs-lookup"><span data-stu-id="eccc6-397">Single</span></span> |
| <span data-ttu-id="eccc6-398">rowversion</span><span class="sxs-lookup"><span data-stu-id="eccc6-398">rowversion</span></span> |<span data-ttu-id="eccc6-399">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-399">Byte[]</span></span> |
| <span data-ttu-id="eccc6-400">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="eccc6-400">smalldatetime</span></span> |<span data-ttu-id="eccc6-401">DateTime</span><span class="sxs-lookup"><span data-stu-id="eccc6-401">DateTime</span></span> |
| <span data-ttu-id="eccc6-402">smallint</span><span class="sxs-lookup"><span data-stu-id="eccc6-402">smallint</span></span> |<span data-ttu-id="eccc6-403">Int16</span><span class="sxs-lookup"><span data-stu-id="eccc6-403">Int16</span></span> |
| <span data-ttu-id="eccc6-404">smallmoney</span><span class="sxs-lookup"><span data-stu-id="eccc6-404">smallmoney</span></span> |<span data-ttu-id="eccc6-405">十進位</span><span class="sxs-lookup"><span data-stu-id="eccc6-405">Decimal</span></span> |
| <span data-ttu-id="eccc6-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="eccc6-406">sql_variant</span></span> |<span data-ttu-id="eccc6-407">物件 *</span><span class="sxs-lookup"><span data-stu-id="eccc6-407">Object *</span></span> |
| <span data-ttu-id="eccc6-408">文字</span><span class="sxs-lookup"><span data-stu-id="eccc6-408">text</span></span> |<span data-ttu-id="eccc6-409">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-409">String, Char[]</span></span> |
| <span data-ttu-id="eccc6-410">分析</span><span class="sxs-lookup"><span data-stu-id="eccc6-410">time</span></span> |<span data-ttu-id="eccc6-411">時間範圍</span><span class="sxs-lookup"><span data-stu-id="eccc6-411">TimeSpan</span></span> |
| <span data-ttu-id="eccc6-412">timestamp</span><span class="sxs-lookup"><span data-stu-id="eccc6-412">timestamp</span></span> |<span data-ttu-id="eccc6-413">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-413">Byte[]</span></span> |
| <span data-ttu-id="eccc6-414">tinyint</span><span class="sxs-lookup"><span data-stu-id="eccc6-414">tinyint</span></span> |<span data-ttu-id="eccc6-415">位元組</span><span class="sxs-lookup"><span data-stu-id="eccc6-415">Byte</span></span> |
| <span data-ttu-id="eccc6-416">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="eccc6-416">uniqueidentifier</span></span> |<span data-ttu-id="eccc6-417">Guid</span><span class="sxs-lookup"><span data-stu-id="eccc6-417">Guid</span></span> |
| <span data-ttu-id="eccc6-418">varbinary</span><span class="sxs-lookup"><span data-stu-id="eccc6-418">varbinary</span></span> |<span data-ttu-id="eccc6-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-419">Byte[]</span></span> |
| <span data-ttu-id="eccc6-420">varchar</span><span class="sxs-lookup"><span data-stu-id="eccc6-420">varchar</span></span> |<span data-ttu-id="eccc6-421">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="eccc6-421">String, Char[]</span></span> |
| <span data-ttu-id="eccc6-422">xml</span><span class="sxs-lookup"><span data-stu-id="eccc6-422">xml</span></span> |<span data-ttu-id="eccc6-423">xml</span><span class="sxs-lookup"><span data-stu-id="eccc6-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="eccc6-424">對應來源 toosink 資料行</span><span class="sxs-lookup"><span data-stu-id="eccc6-424">Mapping source toosink columns</span></span>
<span data-ttu-id="eccc6-425">toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="eccc6-426">可重複複製</span><span class="sxs-lookup"><span data-stu-id="eccc6-426">Repeatable copy</span></span>
<span data-ttu-id="eccc6-427">當複製資料 tooSQL 伺服器資料庫，hello 複製活動將預設附加 toohello 接收資料表。</span><span class="sxs-lookup"><span data-stu-id="eccc6-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="eccc6-428">相反地，請參閱 tooperform UPSERT[可重複寫入 tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink)發行項。</span><span class="sxs-lookup"><span data-stu-id="eccc6-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="eccc6-429">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="eccc6-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="eccc6-430">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="eccc6-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="eccc6-431">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="eccc6-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="eccc6-432">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="eccc6-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="eccc6-433">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="eccc6-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="eccc6-434">效能和微調</span><span class="sxs-lookup"><span data-stu-id="eccc6-434">Performance and Tuning</span></span>
<span data-ttu-id="eccc6-435">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="eccc6-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
