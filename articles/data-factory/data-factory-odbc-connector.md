---
title: "從 ODBC 資料存放區 aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從 ODBC 資料 toomove 資料存放區使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="44924-103">使用 Azure Data Factory 從 ODBC 資料存放區移動資料</span><span class="sxs-lookup"><span data-stu-id="44924-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="44924-104">本文說明如何儲存在 Azure Data Factory toomove 資料從內部部署 ODBC 資料 toouse hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="44924-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="44924-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="44924-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="44924-106">您可以從 ODBC 資料存放區支援 tooany 接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="44924-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="44924-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="44924-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="44924-108">目前資料處理站都會支援只移動從 ODBC 資料的資料存放區 tooother 資料存放區，但不適用於將資料從其他資料存放區 tooan ODBC 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="44924-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="44924-109">啟用連線</span><span class="sxs-lookup"><span data-stu-id="44924-109">Enabling connectivity</span></span>
<span data-ttu-id="44924-110">資料 Factory 服務支援使用 hello 資料管理閘道的連線 tooon 內部部署 ODBC 來源。</span><span class="sxs-lookup"><span data-stu-id="44924-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="44924-111">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="44924-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="44924-112">使用 hello 閘道 tooconnect tooan ODBC 資料存放區，即使它裝載於 Azure IaaS VM。</span><span class="sxs-lookup"><span data-stu-id="44924-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="44924-113">您可以在 hello 相同的內部部署電腦或 hello 做 hello ODBC 資料存放區的 Azure VM 上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="44924-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="44924-114">不過，我們建議您在個別機器/Azure IaaS VM 上安裝 hello 閘道 tooavoid 資源爭用和較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="44924-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="44924-115">當您在不同電腦上安裝 hello 閘道時，hello 部應該能夠 tooaccess hello 機器 hello ODBC 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="44924-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="44924-116">除了 hello 資料管理閘道器，您也需要 tooinstall hello ODBC 驅動程式 hello hello 閘道機器上的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="44924-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="44924-117">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="44924-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="44924-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="44924-118">Getting started</span></span>
<span data-ttu-id="44924-119">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 ODBC 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="44924-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="44924-120">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="44924-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="44924-121">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="44924-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="44924-122">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="44924-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="44924-123">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="44924-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="44924-124">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="44924-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="44924-125">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="44924-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="44924-126">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="44924-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="44924-127">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="44924-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="44924-128">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="44924-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="44924-129">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="44924-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="44924-130">使用 Data Factory 實體的 ODBC 資料存放區中的使用的 toocopy 資料的 JSON 定義中的範例，請參閱[JSON 範例： 從 ODBC 資料的複本資料存放區 tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="44924-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="44924-131">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooODBC 資料存放區的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="44924-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="44924-132">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="44924-132">Linked service properties</span></span>
<span data-ttu-id="44924-133">下表中的 hello 提供 JSON 項目特定 tooODBC 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="44924-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="44924-134">屬性</span><span class="sxs-lookup"><span data-stu-id="44924-134">Property</span></span> | <span data-ttu-id="44924-135">說明</span><span class="sxs-lookup"><span data-stu-id="44924-135">Description</span></span> | <span data-ttu-id="44924-136">必要</span><span class="sxs-lookup"><span data-stu-id="44924-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44924-137">類型</span><span class="sxs-lookup"><span data-stu-id="44924-137">type</span></span> |<span data-ttu-id="44924-138">hello 類型屬性必須設定為： **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="44924-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="44924-139">是</span><span class="sxs-lookup"><span data-stu-id="44924-139">Yes</span></span> |
| <span data-ttu-id="44924-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="44924-140">connectionString</span></span> |<span data-ttu-id="44924-141">hello 非存取認證部分 hello 連接字串和選擇性的加密認證。</span><span class="sxs-lookup"><span data-stu-id="44924-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="44924-142">請參閱下列各節的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="44924-142">See examples in hello following sections.</span></span> |<span data-ttu-id="44924-143">是</span><span class="sxs-lookup"><span data-stu-id="44924-143">Yes</span></span> |
| <span data-ttu-id="44924-144">認證</span><span class="sxs-lookup"><span data-stu-id="44924-144">credential</span></span> |<span data-ttu-id="44924-145">hello 存取認證的 hello 驅動程式特有的屬性值的格式指定的連接字串部分。</span><span class="sxs-lookup"><span data-stu-id="44924-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="44924-146">範例：“Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”。</span><span class="sxs-lookup"><span data-stu-id="44924-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="44924-147">否</span><span class="sxs-lookup"><span data-stu-id="44924-147">No</span></span> |
| <span data-ttu-id="44924-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="44924-148">authenticationType</span></span> |<span data-ttu-id="44924-149">Tooconnect toohello ODBC 資料存放區使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="44924-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="44924-150">可能的值為：Anonymous 和 Basic。</span><span class="sxs-lookup"><span data-stu-id="44924-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="44924-151">是</span><span class="sxs-lookup"><span data-stu-id="44924-151">Yes</span></span> |
| <span data-ttu-id="44924-152">username</span><span class="sxs-lookup"><span data-stu-id="44924-152">username</span></span> |<span data-ttu-id="44924-153">如果您要使用 Basic 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="44924-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="44924-154">否</span><span class="sxs-lookup"><span data-stu-id="44924-154">No</span></span> |
| <span data-ttu-id="44924-155">password</span><span class="sxs-lookup"><span data-stu-id="44924-155">password</span></span> |<span data-ttu-id="44924-156">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="44924-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="44924-157">否</span><span class="sxs-lookup"><span data-stu-id="44924-157">No</span></span> |
| <span data-ttu-id="44924-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="44924-158">gatewayName</span></span> |<span data-ttu-id="44924-159">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello ODBC 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="44924-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="44924-160">是</span><span class="sxs-lookup"><span data-stu-id="44924-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="44924-161">使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="44924-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="44924-162">使用基本驗證與加密認證</span><span class="sxs-lookup"><span data-stu-id="44924-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="44924-163">您可以加密使用 hello hello 認證[新增 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) （1.0 版本的 Azure PowerShell） 指令程式或[New-azuredatafactoryencryptvalue](https://msdn.microsoft.com/library/dn834940.aspx) （0.9 或更早版本的 helloAzure PowerShell)。</span><span class="sxs-lookup"><span data-stu-id="44924-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="44924-164">使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="44924-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="44924-165">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="44924-165">Dataset properties</span></span>
<span data-ttu-id="44924-166">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="44924-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="44924-167">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="44924-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="44924-168">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="44924-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="44924-169">hello typeProperties 區段類型的資料集**RelationalTable** （包括 ODBC 的資料集） 具有下列屬性的 hello</span><span class="sxs-lookup"><span data-stu-id="44924-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="44924-170">屬性</span><span class="sxs-lookup"><span data-stu-id="44924-170">Property</span></span> | <span data-ttu-id="44924-171">說明</span><span class="sxs-lookup"><span data-stu-id="44924-171">Description</span></span> | <span data-ttu-id="44924-172">必要</span><span class="sxs-lookup"><span data-stu-id="44924-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44924-173">tableName</span><span class="sxs-lookup"><span data-stu-id="44924-173">tableName</span></span> |<span data-ttu-id="44924-174">Hello ODBC 資料存放區中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="44924-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="44924-175">是</span><span class="sxs-lookup"><span data-stu-id="44924-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="44924-176">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="44924-176">Copy activity properties</span></span>
<span data-ttu-id="44924-177">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="44924-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="44924-178">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="44924-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="44924-179">屬性用於 hello **typeProperties** > 一節的 hello hello 活動另一方面會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="44924-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="44924-180">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="44924-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="44924-181">複製活動中，當來源的類型為**RelationalSource** （包括 ODBC），下列屬性的 hello 可用 typeProperties 區段中：</span><span class="sxs-lookup"><span data-stu-id="44924-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="44924-182">屬性</span><span class="sxs-lookup"><span data-stu-id="44924-182">Property</span></span> | <span data-ttu-id="44924-183">說明</span><span class="sxs-lookup"><span data-stu-id="44924-183">Description</span></span> | <span data-ttu-id="44924-184">允許的值</span><span class="sxs-lookup"><span data-stu-id="44924-184">Allowed values</span></span> | <span data-ttu-id="44924-185">必要</span><span class="sxs-lookup"><span data-stu-id="44924-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="44924-186">query</span><span class="sxs-lookup"><span data-stu-id="44924-186">query</span></span> |<span data-ttu-id="44924-187">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="44924-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="44924-188">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="44924-188">SQL query string.</span></span> <span data-ttu-id="44924-189">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="44924-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="44924-190">是</span><span class="sxs-lookup"><span data-stu-id="44924-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="44924-191">JSON 範例： 從 ODBC 資料的複本資料存放區 tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="44924-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="44924-192">此範例中提供的 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="44924-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="44924-193">它會顯示如何從 ODBC toocopy 資料來源 tooan Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="44924-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="44924-194">不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="44924-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="44924-195">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="44924-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="44924-196">[OnPremisesOdbc](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="44924-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="44924-197">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="44924-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="44924-198">[RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="44924-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="44924-199">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="44924-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="44924-200">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="44924-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="44924-201">hello 範例將資料從 ODBC 資料存放區 tooa blob 中的查詢結果的每個小時。</span><span class="sxs-lookup"><span data-stu-id="44924-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="44924-202">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="44924-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="44924-203">第一個步驟中，設定 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="44924-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="44924-204">hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="44924-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="44924-205">**ODBC 的連結服務**本例使用 hello 基本驗證。</span><span class="sxs-lookup"><span data-stu-id="44924-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="44924-206">請參閱 [ODBC 連結服務](#linked-service-properties) 章節以了解您可以使用的各種不同類型的驗證。</span><span class="sxs-lookup"><span data-stu-id="44924-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="44924-207">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="44924-207">**Azure Storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
    }
}
```

<span data-ttu-id="44924-208">**ODBC 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="44924-208">**ODBC input dataset**</span></span>

<span data-ttu-id="44924-209">hello 範例假設您已建立資料表"MyTable"中的 ODBC 資料庫而且包含稱為"timestampcolumn 「 時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="44924-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="44924-210">設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="44924-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="44924-211">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="44924-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="44924-212">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="44924-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="44924-213">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="44924-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="44924-214">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="44924-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


<span data-ttu-id="44924-215">**具有 ODBC 來源 (RelationalSource) 和 Blob 接收器 (BlobSink) 的管線中複製活動**</span><span class="sxs-lookup"><span data-stu-id="44924-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="44924-216">hello 管線包含複製活動的設定的 toouse 這些輸入和輸出資料集，而排程的 toorun 每小時。</span><span class="sxs-lookup"><span data-stu-id="44924-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="44924-217">在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="44924-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="44924-218">指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="44924-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="44924-219">ODBC 的類型對應</span><span class="sxs-lookup"><span data-stu-id="44924-219">Type mapping for ODBC</span></span>
<span data-ttu-id="44924-220">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="44924-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="44924-221">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="44924-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="44924-222">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="44924-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="44924-223">當從 ODBC 資料存放區移動資料時，ODBC 資料類型會對應的 too.NET 類型 hello 中所述[ODBC 資料類型對應](https://msdn.microsoft.com/library/cc668763.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="44924-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="44924-224">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="44924-224">Map source toosink columns</span></span>
<span data-ttu-id="44924-225">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="44924-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="44924-226">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="44924-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="44924-227">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="44924-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="44924-228">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="44924-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="44924-229">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="44924-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="44924-230">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="44924-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="44924-231">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="44924-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="44924-232">GE Historian 存放區</span><span class="sxs-lookup"><span data-stu-id="44924-232">GE Historian store</span></span>
<span data-ttu-id="44924-233">建立連結的 ODBC 服務 toolink [GE Proficy 歷史學家 （現在 GE 歷史學家）](http://www.geautomation.com/products/proficy-historian)資料存放區 tooan 的 Azure data factory 中 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="44924-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="44924-234">在內部部署電腦上安裝資料管理閘道器，並向 hello 入口網站中的 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="44924-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="44924-235">在內部部署電腦上安裝的 hello 閘道 GE 歷史學家 tooconnect toohello GE 歷史學家資料存放區使用 hello ODBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="44924-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="44924-236">因此，如果它尚未安裝 hello 閘道機器上時，才能安裝 hello 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="44924-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="44924-237">如需詳細資訊，請參閱 [啟用連線](#enabling-connectivity) 一節。</span><span class="sxs-lookup"><span data-stu-id="44924-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="44924-238">使用的 hello GE 歷史學家儲存在 Data Factory 方案之前，請確認 hello 閘道是否能連接 toohello 資料存放區使用 hello 下一節中的指示。</span><span class="sxs-lookup"><span data-stu-id="44924-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="44924-239">讀取 hello 的發行項的詳細概觀 hello 從頭使用 ODBC 資料會儲存為複製作業中的來源資料存放區。</span><span class="sxs-lookup"><span data-stu-id="44924-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="44924-240">疑難排解連線問題</span><span class="sxs-lookup"><span data-stu-id="44924-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="44924-241">tootroubleshoot 連接問題，使用 hello**診斷** 索引標籤**資料管理閘道組態管理員**。</span><span class="sxs-lookup"><span data-stu-id="44924-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="44924-242">啟動 **資料管理閘道器組態管理員**。</span><span class="sxs-lookup"><span data-stu-id="44924-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="44924-243">您可以執行"C:\Program Files\Microsoft 資料管理 Gateway\1.0\Shared\ConfigManager.exe 」 直接 （或） 搜尋的**閘道**toofind 連結太**Microsoft 資料管理閘道器**應用程式中 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="44924-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![搜尋閘道器](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="44924-245">切換 toohello**診斷** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="44924-245">Switch toohello **Diagnostics** tab.</span></span>

    ![閘道診斷](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="44924-247">選取 hello**類型**的資料儲存區 （連結的服務）。</span><span class="sxs-lookup"><span data-stu-id="44924-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="44924-248">指定**驗證**輸入**認證**（或） 輸入**連接字串**，是使用的 tooconnect toohello 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="44924-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="44924-249">按一下**測試連接**tootest hello 連接 toohello 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="44924-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="44924-250">效能和微調</span><span class="sxs-lookup"><span data-stu-id="44924-250">Performance and Tuning</span></span>
<span data-ttu-id="44924-251">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="44924-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
