---
title: "從 ODBC 資料存放區移動資料 | Microsoft Docs"
description: "深入了解如何使用 Azure Data Factory 從 ODBC 資料存放區移動資料"
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
ms.openlocfilehash: 269d9802ca4a6a16dbf9021929fe21104cb431f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="21c50-103">使用 Azure Data Factory 從 ODBC 資料存放區移動資料</span><span class="sxs-lookup"><span data-stu-id="21c50-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="21c50-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從內部部署的 ODBC 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="21c50-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="21c50-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="21c50-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="21c50-106">您可以將資料從 ODBC 資料存放區複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="21c50-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="21c50-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格。</span><span class="sxs-lookup"><span data-stu-id="21c50-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="21c50-108">Data Factory 目前只支援將資料從 ODBC 資料存放區移到其他資料存放區，而不支援將資料從其他資料存放區移到 ODBC 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="21c50-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="21c50-109">啟用連線</span><span class="sxs-lookup"><span data-stu-id="21c50-109">Enabling connectivity</span></span>
<span data-ttu-id="21c50-110">Data Factory 服務支援使用資料管理閘道器連接至內部部署 ODBC 來源。</span><span class="sxs-lookup"><span data-stu-id="21c50-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="21c50-111">請參閱 [在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文來了解資料管理閘道和設定閘道的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="21c50-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="21c50-112">即使 ODBC 資料存放區裝載於 Azure IaaS VM 中，仍請使用閘道來與其連接。</span><span class="sxs-lookup"><span data-stu-id="21c50-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="21c50-113">您可以將閘道安裝在與 ODBC 資料存放區相同的內部部署機器或 Azure VM 上。</span><span class="sxs-lookup"><span data-stu-id="21c50-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="21c50-114">不過，建議您將閘道安裝在個別的機器/Azure IaaS VM 上，除了可避免發生資源爭用的情況之外，也可獲得較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="21c50-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="21c50-115">當您在不同機器上安裝閘道器時，機器應該能夠存取具有 ODBC 資料存放區的機器。</span><span class="sxs-lookup"><span data-stu-id="21c50-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="21c50-116">除了資料管理閘道器，您也需要在閘道器機器上的資料存放區安裝 ODBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="21c50-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="21c50-117">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="21c50-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="21c50-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="21c50-118">Getting started</span></span>
<span data-ttu-id="21c50-119">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 ODBC 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="21c50-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="21c50-120">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="21c50-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="21c50-121">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="21c50-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="21c50-122">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="21c50-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="21c50-123">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="21c50-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="21c50-124">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="21c50-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="21c50-125">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="21c50-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="21c50-126">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="21c50-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="21c50-127">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="21c50-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="21c50-128">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="21c50-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="21c50-129">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="21c50-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="21c50-130">如需相關範例，其中含有用來從 ODBC 資料存放區複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 ODBC 資料存放區複製到 Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="21c50-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="21c50-131">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 ODBC 資料存放區特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="21c50-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="21c50-132">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="21c50-132">Linked service properties</span></span>
<span data-ttu-id="21c50-133">下表提供 ODBC 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="21c50-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="21c50-134">屬性</span><span class="sxs-lookup"><span data-stu-id="21c50-134">Property</span></span> | <span data-ttu-id="21c50-135">說明</span><span class="sxs-lookup"><span data-stu-id="21c50-135">Description</span></span> | <span data-ttu-id="21c50-136">必要</span><span class="sxs-lookup"><span data-stu-id="21c50-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21c50-137">類型</span><span class="sxs-lookup"><span data-stu-id="21c50-137">type</span></span> |<span data-ttu-id="21c50-138">類型屬性必須設為： **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="21c50-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="21c50-139">是</span><span class="sxs-lookup"><span data-stu-id="21c50-139">Yes</span></span> |
| <span data-ttu-id="21c50-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="21c50-140">connectionString</span></span> |<span data-ttu-id="21c50-141">連接字串的非存取認證部分和選擇性的加密認證。</span><span class="sxs-lookup"><span data-stu-id="21c50-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="21c50-142">請參閱下列幾節中的範例。</span><span class="sxs-lookup"><span data-stu-id="21c50-142">See examples in the following sections.</span></span> |<span data-ttu-id="21c50-143">是</span><span class="sxs-lookup"><span data-stu-id="21c50-143">Yes</span></span> |
| <span data-ttu-id="21c50-144">認證</span><span class="sxs-lookup"><span data-stu-id="21c50-144">credential</span></span> |<span data-ttu-id="21c50-145">以驅動程式特定「屬性-值」格式指定之連接字串的存取認證部分。</span><span class="sxs-lookup"><span data-stu-id="21c50-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="21c50-146">範例：“Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”。</span><span class="sxs-lookup"><span data-stu-id="21c50-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="21c50-147">否</span><span class="sxs-lookup"><span data-stu-id="21c50-147">No</span></span> |
| <span data-ttu-id="21c50-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21c50-148">authenticationType</span></span> |<span data-ttu-id="21c50-149">用來連接到 ODBC 資料存放區的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="21c50-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="21c50-150">可能的值為：Anonymous 和 Basic。</span><span class="sxs-lookup"><span data-stu-id="21c50-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="21c50-151">是</span><span class="sxs-lookup"><span data-stu-id="21c50-151">Yes</span></span> |
| <span data-ttu-id="21c50-152">username</span><span class="sxs-lookup"><span data-stu-id="21c50-152">username</span></span> |<span data-ttu-id="21c50-153">如果您要使用 Basic 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="21c50-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="21c50-154">否</span><span class="sxs-lookup"><span data-stu-id="21c50-154">No</span></span> |
| <span data-ttu-id="21c50-155">password</span><span class="sxs-lookup"><span data-stu-id="21c50-155">password</span></span> |<span data-ttu-id="21c50-156">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="21c50-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="21c50-157">否</span><span class="sxs-lookup"><span data-stu-id="21c50-157">No</span></span> |
| <span data-ttu-id="21c50-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21c50-158">gatewayName</span></span> |<span data-ttu-id="21c50-159">Data Factory 服務應該用來連接到 ODBC 資料存放區的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="21c50-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="21c50-160">是</span><span class="sxs-lookup"><span data-stu-id="21c50-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="21c50-161">使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="21c50-161">Using Basic authentication</span></span>

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
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="21c50-162">使用基本驗證與加密認證</span><span class="sxs-lookup"><span data-stu-id="21c50-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="21c50-163">您可以使用 [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 版的 Azure PowerShell) Cmdlet 或 [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 或更舊版的 Azure PowerShell) 來加密認證。</span><span class="sxs-lookup"><span data-stu-id="21c50-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="21c50-164">使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="21c50-164">Using Anonymous authentication</span></span>

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


## <a name="dataset-properties"></a><span data-ttu-id="21c50-165">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="21c50-165">Dataset properties</span></span>
<span data-ttu-id="21c50-166">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="21c50-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="21c50-167">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="21c50-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="21c50-168">每個資料集類型的 **typeProperties** 區段都不同，可提供資料存放區中的資料位置資訊。</span><span class="sxs-lookup"><span data-stu-id="21c50-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="21c50-169">**RelationalTable** 資料集類型的 typeProperties 區段 (包含 ODBC 資料集) 具有下列屬性</span><span class="sxs-lookup"><span data-stu-id="21c50-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="21c50-170">屬性</span><span class="sxs-lookup"><span data-stu-id="21c50-170">Property</span></span> | <span data-ttu-id="21c50-171">說明</span><span class="sxs-lookup"><span data-stu-id="21c50-171">Description</span></span> | <span data-ttu-id="21c50-172">必要</span><span class="sxs-lookup"><span data-stu-id="21c50-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21c50-173">tableName</span><span class="sxs-lookup"><span data-stu-id="21c50-173">tableName</span></span> |<span data-ttu-id="21c50-174">ODBC 資料存放區中資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="21c50-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="21c50-175">是</span><span class="sxs-lookup"><span data-stu-id="21c50-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="21c50-176">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="21c50-176">Copy activity properties</span></span>
<span data-ttu-id="21c50-177">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="21c50-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="21c50-178">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="21c50-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="21c50-179">另一方面，活動的 **typeProperties** 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="21c50-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="21c50-180">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="21c50-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="21c50-181">在複製活動中，如果來源的類型為 **RelationalSource** (包括 ODBC)，則 typeProperties 區段中可使用下列屬性：</span><span class="sxs-lookup"><span data-stu-id="21c50-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="21c50-182">屬性</span><span class="sxs-lookup"><span data-stu-id="21c50-182">Property</span></span> | <span data-ttu-id="21c50-183">說明</span><span class="sxs-lookup"><span data-stu-id="21c50-183">Description</span></span> | <span data-ttu-id="21c50-184">允許的值</span><span class="sxs-lookup"><span data-stu-id="21c50-184">Allowed values</span></span> | <span data-ttu-id="21c50-185">必要</span><span class="sxs-lookup"><span data-stu-id="21c50-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21c50-186">query</span><span class="sxs-lookup"><span data-stu-id="21c50-186">query</span></span> |<span data-ttu-id="21c50-187">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="21c50-187">Use the custom query to read data.</span></span> |<span data-ttu-id="21c50-188">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="21c50-188">SQL query string.</span></span> <span data-ttu-id="21c50-189">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="21c50-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="21c50-190">是</span><span class="sxs-lookup"><span data-stu-id="21c50-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="21c50-191">JSON 範例：將資料從 ODBC 資料存放區複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="21c50-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="21c50-192">此範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="21c50-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="21c50-193">它示範如何將資料從 ODBC 來源複製到「Azure Blob 儲存體」。</span><span class="sxs-lookup"><span data-stu-id="21c50-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="21c50-194">不過，您可以在 Azure Data Factory 中使用複製活動，將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="21c50-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="21c50-195">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="21c50-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="21c50-196">[OnPremisesOdbc](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="21c50-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="21c50-197">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="21c50-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="21c50-198">[RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="21c50-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="21c50-199">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="21c50-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="21c50-200">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="21c50-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="21c50-201">此範例會每個小時將資料從 ODBC 資料存放區中的查詢結果複製到 Blob。</span><span class="sxs-lookup"><span data-stu-id="21c50-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="21c50-202">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="21c50-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="21c50-203">第一步是設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="21c50-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="21c50-204">如需相關指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="21c50-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="21c50-205">**ODBC 連結服務** 此範例會使用 Basic 驗證。</span><span class="sxs-lookup"><span data-stu-id="21c50-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="21c50-206">請參閱 [ODBC 連結服務](#linked-service-properties) 章節以了解您可以使用的各種不同類型的驗證。</span><span class="sxs-lookup"><span data-stu-id="21c50-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="21c50-207">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="21c50-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="21c50-208">**ODBC 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="21c50-208">**ODBC input dataset**</span></span>

<span data-ttu-id="21c50-209">此範例假設您已在 ODBC 資料庫中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestampcolumn")。</span><span class="sxs-lookup"><span data-stu-id="21c50-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="21c50-210">設定 “external”: ”true” 會通知 Data Factory 服務：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="21c50-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="21c50-211">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="21c50-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="21c50-212">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="21c50-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="21c50-213">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="21c50-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="21c50-214">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="21c50-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


<span data-ttu-id="21c50-215">**具有 ODBC 來源 (RelationalSource) 和 Blob 接收器 (BlobSink) 的管線中複製活動**</span><span class="sxs-lookup"><span data-stu-id="21c50-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="21c50-216">此管線包含「複製活動」，該活動已設定為使用這些輸入和輸出資料集，並且排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="21c50-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="21c50-217">在管線 JSON 定義中，已將 **source** 類型設為 **RelationalSource**，並將 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="21c50-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="21c50-218">針對 **query** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="21c50-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="21c50-219">ODBC 的類型對應</span><span class="sxs-lookup"><span data-stu-id="21c50-219">Type mapping for ODBC</span></span>
<span data-ttu-id="21c50-220">如 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會藉由下列含有兩個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="21c50-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="21c50-221">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="21c50-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="21c50-222">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="21c50-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="21c50-223">從 ODBC 資料存放區移動資料時，ODBC 資料類型會對應至 .NET 類型，如 [ODBC 資料類型對應](https://msdn.microsoft.com/library/cc668763.aspx) 主題中所述。</span><span class="sxs-lookup"><span data-stu-id="21c50-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="21c50-224">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="21c50-224">Map source to sink columns</span></span>
<span data-ttu-id="21c50-225">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="21c50-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="21c50-226">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="21c50-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="21c50-227">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="21c50-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="21c50-228">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="21c50-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="21c50-229">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="21c50-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="21c50-230">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="21c50-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="21c50-231">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="21c50-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="21c50-232">GE Historian 存放區</span><span class="sxs-lookup"><span data-stu-id="21c50-232">GE Historian store</span></span>
<span data-ttu-id="21c50-233">您建立 ODBC 連結服務，將 [GE Proficy Historian (現為 GE Historian)](http://www.geautomation.com/products/proficy-historian) 資料存放區連結至 Azure Data Factory，如下例所示︰</span><span class="sxs-lookup"><span data-stu-id="21c50-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="21c50-234">將「資料管理閘道」安裝在內部部署機器上，並向入口網站註冊該閘道。</span><span class="sxs-lookup"><span data-stu-id="21c50-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="21c50-235">安裝在內部部署電腦上的閘道會使用適用於 GE Historian 的 ODBC 驅動程式來連接到 GE Historian 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="21c50-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="21c50-236">因此，如果尚未在閘道機器上安裝該驅動程式，請安裝它。</span><span class="sxs-lookup"><span data-stu-id="21c50-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="21c50-237">如需詳細資訊，請參閱 [啟用連線](#enabling-connectivity) 一節。</span><span class="sxs-lookup"><span data-stu-id="21c50-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="21c50-238">使用 Data Factory 方案中的 GE Historian 存放區之前，請先確認閘道器可否使用下節中的指示連接到資料存放區。</span><span class="sxs-lookup"><span data-stu-id="21c50-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="21c50-239">如需在複製作業中將 ODBC 資料存放區用做來源資料存放區的詳細概觀，請從頭閱讀本文。</span><span class="sxs-lookup"><span data-stu-id="21c50-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="21c50-240">疑難排解連線問題</span><span class="sxs-lookup"><span data-stu-id="21c50-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="21c50-241">若要針對連線問題進行疑難排解，請使用 [資料管理閘道器組態管理員] 的 [診斷] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="21c50-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="21c50-242">啟動 **資料管理閘道器組態管理員**。</span><span class="sxs-lookup"><span data-stu-id="21c50-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="21c50-243">您可以直接執行 "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" (或) 搜尋**閘道**，以尋找 **Microsoft 資料管理閘道**應用程式的連結，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="21c50-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![搜尋閘道器](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="21c50-245">切換至 [診斷]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="21c50-245">Switch to the **Diagnostics** tab.</span></span>

    ![閘道診斷](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="21c50-247">選取資料存放區的 **類型** (連結的服務)。</span><span class="sxs-lookup"><span data-stu-id="21c50-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="21c50-248">指定 [驗證]，然後輸入用來連線到資料存放區的**認證** (或) 輸入**連接字串**。</span><span class="sxs-lookup"><span data-stu-id="21c50-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="21c50-249">按一下 [測試連線]  以測試資料存放區連線。</span><span class="sxs-lookup"><span data-stu-id="21c50-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="21c50-250">效能和微調</span><span class="sxs-lookup"><span data-stu-id="21c50-250">Performance and Tuning</span></span>
<span data-ttu-id="21c50-251">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="21c50-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
