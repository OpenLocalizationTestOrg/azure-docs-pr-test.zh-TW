---
title: "從 OData 來源移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory，來移動 OData 來源的資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 624b6c8f317477d83539392c6c2f15c2dc69d401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="e959d-103">使用 Azure Data Factory 來移動 OData 來源的資料</span><span class="sxs-lookup"><span data-stu-id="e959d-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="e959d-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從內部部署的 OData 來源移動資料。</span><span class="sxs-lookup"><span data-stu-id="e959d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="e959d-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="e959d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="e959d-106">您可以將資料從 OData 來源複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="e959d-106">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="e959d-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格。</span><span class="sxs-lookup"><span data-stu-id="e959d-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="e959d-108">Data Factory 目前只支援將資料從 OData 來源移到其他資料存放區，而不支援將資料從其他資料存放區移到 OData 來源。</span><span class="sxs-lookup"><span data-stu-id="e959d-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="e959d-109">支援的版本和驗證類型</span><span class="sxs-lookup"><span data-stu-id="e959d-109">Supported versions and authentication types</span></span>
<span data-ttu-id="e959d-110">此 OData 連接器支援 OData 版本 3.0 和 4.0，而您可以從雲端 OData 和內部部署 OData 來源複製資料。</span><span class="sxs-lookup"><span data-stu-id="e959d-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="e959d-111">若為後者，您必須安裝資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="e959d-111">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="e959d-112">如需資料管理閘道的詳細資訊，請參閱 [在內部部署和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="e959d-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="e959d-113">支援下列驗證類型：</span><span class="sxs-lookup"><span data-stu-id="e959d-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="e959d-114">若要存取**雲端** OData 摘要，您可以使用匿名、基本 (使用者名稱和密碼) 或 Azure Active Directory 架構的 OAuth 驗證。</span><span class="sxs-lookup"><span data-stu-id="e959d-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="e959d-115">若要存取**內部部署** OData 摘要，您可以使用匿名、基本 (使用者名稱和密碼) 或 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="e959d-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e959d-116">開始使用</span><span class="sxs-lookup"><span data-stu-id="e959d-116">Getting started</span></span>
<span data-ttu-id="e959d-117">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 OData 來源移動資料。</span><span class="sxs-lookup"><span data-stu-id="e959d-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="e959d-118">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="e959d-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="e959d-119">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="e959d-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="e959d-120">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="e959d-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e959d-121">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="e959d-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e959d-122">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="e959d-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="e959d-123">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="e959d-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="e959d-124">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="e959d-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="e959d-125">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="e959d-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e959d-126">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="e959d-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="e959d-127">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="e959d-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="e959d-128">如需相關範例，其中含有用來從 OData 來源複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 OData 來源複製到 Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="e959d-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="e959d-129">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 OData 來源特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="e959d-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e959d-130">已連結的服務屬性</span><span class="sxs-lookup"><span data-stu-id="e959d-130">Linked Service properties</span></span>
<span data-ttu-id="e959d-131">下表提供 OData 連結服務專屬 JSON 元素的說明。</span><span class="sxs-lookup"><span data-stu-id="e959d-131">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="e959d-132">屬性</span><span class="sxs-lookup"><span data-stu-id="e959d-132">Property</span></span> | <span data-ttu-id="e959d-133">說明</span><span class="sxs-lookup"><span data-stu-id="e959d-133">Description</span></span> | <span data-ttu-id="e959d-134">必要</span><span class="sxs-lookup"><span data-stu-id="e959d-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e959d-135">類型</span><span class="sxs-lookup"><span data-stu-id="e959d-135">type</span></span> |<span data-ttu-id="e959d-136">類型屬性必須設為： **OData**</span><span class="sxs-lookup"><span data-stu-id="e959d-136">The type property must be set to: **OData**</span></span> |<span data-ttu-id="e959d-137">是</span><span class="sxs-lookup"><span data-stu-id="e959d-137">Yes</span></span> |
| <span data-ttu-id="e959d-138">URL</span><span class="sxs-lookup"><span data-stu-id="e959d-138">url</span></span> |<span data-ttu-id="e959d-139">OData 服務的 URL。</span><span class="sxs-lookup"><span data-stu-id="e959d-139">Url of the OData service.</span></span> |<span data-ttu-id="e959d-140">是</span><span class="sxs-lookup"><span data-stu-id="e959d-140">Yes</span></span> |
| <span data-ttu-id="e959d-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e959d-141">authenticationType</span></span> |<span data-ttu-id="e959d-142">用來連線到 OData 來源的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="e959d-142">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="e959d-143">若為雲端 OData，可能的值為 Anonymous、Basic 和 OAuth (請注意，Azure Data Factory 目前僅支援 Azure Active Directory 架構的 OAuth)。</span><span class="sxs-lookup"><span data-stu-id="e959d-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="e959d-144">若為內部部署 OData，可能的值為 Anonymous、Basic 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="e959d-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="e959d-145">是</span><span class="sxs-lookup"><span data-stu-id="e959d-145">Yes</span></span> |
| <span data-ttu-id="e959d-146">username</span><span class="sxs-lookup"><span data-stu-id="e959d-146">username</span></span> |<span data-ttu-id="e959d-147">如果您要使用 Basic 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="e959d-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="e959d-148">是 (只在您使用基本驗證時)</span><span class="sxs-lookup"><span data-stu-id="e959d-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="e959d-149">password</span><span class="sxs-lookup"><span data-stu-id="e959d-149">password</span></span> |<span data-ttu-id="e959d-150">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="e959d-150">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="e959d-151">是 (只在您使用基本驗證時)</span><span class="sxs-lookup"><span data-stu-id="e959d-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="e959d-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="e959d-152">authorizedCredential</span></span> |<span data-ttu-id="e959d-153">如果您使用 OAuth，按一下 Data Factory 複製精靈或編輯器中的 [授權] 按鈕，然後輸入您的認證，接著將會自動產生這個屬性的值。</span><span class="sxs-lookup"><span data-stu-id="e959d-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="e959d-154">是 (只有在您使用 OAuth 驗證時)</span><span class="sxs-lookup"><span data-stu-id="e959d-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="e959d-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e959d-155">gatewayName</span></span> |<span data-ttu-id="e959d-156">Data Factory 服務應該用來連接到內部部署 OData 服務的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="e959d-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="e959d-157">只在要從內部部署 OData 來源複製資料時才指定。</span><span class="sxs-lookup"><span data-stu-id="e959d-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="e959d-158">否</span><span class="sxs-lookup"><span data-stu-id="e959d-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="e959d-159">使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="e959d-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="e959d-160">使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="e959d-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="e959d-161">使用存取內部部署 OData 來源的 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="e959d-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="e959d-162">使用 OAuth 驗證存取雲端 OData 來源</span><span class="sxs-lookup"><span data-stu-id="e959d-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="e959d-163">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="e959d-163">Dataset properties</span></span>
<span data-ttu-id="e959d-164">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="e959d-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e959d-165">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="e959d-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e959d-166">每個資料集類型的 **typeProperties** 區段都不同，可提供資料存放區中的資料位置資訊。</span><span class="sxs-lookup"><span data-stu-id="e959d-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="e959d-167">**ODataResource** (包含 OData 資料集) 類型資料集的 typeProperties 區段有下列屬性</span><span class="sxs-lookup"><span data-stu-id="e959d-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="e959d-168">屬性</span><span class="sxs-lookup"><span data-stu-id="e959d-168">Property</span></span> | <span data-ttu-id="e959d-169">說明</span><span class="sxs-lookup"><span data-stu-id="e959d-169">Description</span></span> | <span data-ttu-id="e959d-170">必要</span><span class="sxs-lookup"><span data-stu-id="e959d-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e959d-171">path</span><span class="sxs-lookup"><span data-stu-id="e959d-171">path</span></span> |<span data-ttu-id="e959d-172">OData 資源的路徑</span><span class="sxs-lookup"><span data-stu-id="e959d-172">Path to the OData resource</span></span> |<span data-ttu-id="e959d-173">否</span><span class="sxs-lookup"><span data-stu-id="e959d-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="e959d-174">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="e959d-174">Copy activity properties</span></span>
<span data-ttu-id="e959d-175">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="e959d-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e959d-176">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="e959d-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="e959d-177">另一方面，活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e959d-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="e959d-178">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e959d-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="e959d-179">如果來源類型為 **RelationalSource** (包含 OData)，則 typeProperties 區段可使用下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e959d-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="e959d-180">屬性</span><span class="sxs-lookup"><span data-stu-id="e959d-180">Property</span></span> | <span data-ttu-id="e959d-181">說明</span><span class="sxs-lookup"><span data-stu-id="e959d-181">Description</span></span> | <span data-ttu-id="e959d-182">範例</span><span class="sxs-lookup"><span data-stu-id="e959d-182">Example</span></span> | <span data-ttu-id="e959d-183">必要</span><span class="sxs-lookup"><span data-stu-id="e959d-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e959d-184">query</span><span class="sxs-lookup"><span data-stu-id="e959d-184">query</span></span> |<span data-ttu-id="e959d-185">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="e959d-185">Use the custom query to read data.</span></span> |<span data-ttu-id="e959d-186">「?$select=Name, Description&$top=5」</span><span class="sxs-lookup"><span data-stu-id="e959d-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="e959d-187">否</span><span class="sxs-lookup"><span data-stu-id="e959d-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="e959d-188">OData 的類型對應</span><span class="sxs-lookup"><span data-stu-id="e959d-188">Type Mapping for OData</span></span>
<span data-ttu-id="e959d-189">如 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會藉由下列含有兩個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換。</span><span class="sxs-lookup"><span data-stu-id="e959d-189">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="e959d-190">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="e959d-190">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="e959d-191">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="e959d-191">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="e959d-192">從 OData 移動資料時，OData 類型至 .NET 類型會使用下列對應。</span><span class="sxs-lookup"><span data-stu-id="e959d-192">When moving data from OData, the following mappings are used from OData types to .NET type.</span></span>

| <span data-ttu-id="e959d-193">OData 資料類型</span><span class="sxs-lookup"><span data-stu-id="e959d-193">OData Data Type</span></span> | <span data-ttu-id="e959d-194">.NET 類型</span><span class="sxs-lookup"><span data-stu-id="e959d-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="e959d-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="e959d-195">Edm.Binary</span></span> |<span data-ttu-id="e959d-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e959d-196">Byte[]</span></span> |
| <span data-ttu-id="e959d-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="e959d-197">Edm.Boolean</span></span> |<span data-ttu-id="e959d-198">Bool</span><span class="sxs-lookup"><span data-stu-id="e959d-198">Bool</span></span> |
| <span data-ttu-id="e959d-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="e959d-199">Edm.Byte</span></span> |<span data-ttu-id="e959d-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e959d-200">Byte[]</span></span> |
| <span data-ttu-id="e959d-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="e959d-201">Edm.DateTime</span></span> |<span data-ttu-id="e959d-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="e959d-202">DateTime</span></span> |
| <span data-ttu-id="e959d-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="e959d-203">Edm.Decimal</span></span> |<span data-ttu-id="e959d-204">十進位</span><span class="sxs-lookup"><span data-stu-id="e959d-204">Decimal</span></span> |
| <span data-ttu-id="e959d-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="e959d-205">Edm.Double</span></span> |<span data-ttu-id="e959d-206">兩倍</span><span class="sxs-lookup"><span data-stu-id="e959d-206">Double</span></span> |
| <span data-ttu-id="e959d-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="e959d-207">Edm.Single</span></span> |<span data-ttu-id="e959d-208">單一</span><span class="sxs-lookup"><span data-stu-id="e959d-208">Single</span></span> |
| <span data-ttu-id="e959d-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="e959d-209">Edm.Guid</span></span> |<span data-ttu-id="e959d-210">Guid</span><span class="sxs-lookup"><span data-stu-id="e959d-210">Guid</span></span> |
| <span data-ttu-id="e959d-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="e959d-211">Edm.Int16</span></span> |<span data-ttu-id="e959d-212">Int16</span><span class="sxs-lookup"><span data-stu-id="e959d-212">Int16</span></span> |
| <span data-ttu-id="e959d-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="e959d-213">Edm.Int32</span></span> |<span data-ttu-id="e959d-214">Int32</span><span class="sxs-lookup"><span data-stu-id="e959d-214">Int32</span></span> |
| <span data-ttu-id="e959d-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="e959d-215">Edm.Int64</span></span> |<span data-ttu-id="e959d-216">Int64</span><span class="sxs-lookup"><span data-stu-id="e959d-216">Int64</span></span> |
| <span data-ttu-id="e959d-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="e959d-217">Edm.SByte</span></span> |<span data-ttu-id="e959d-218">Int16</span><span class="sxs-lookup"><span data-stu-id="e959d-218">Int16</span></span> |
| <span data-ttu-id="e959d-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="e959d-219">Edm.String</span></span> |<span data-ttu-id="e959d-220">String</span><span class="sxs-lookup"><span data-stu-id="e959d-220">String</span></span> |
| <span data-ttu-id="e959d-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="e959d-221">Edm.Time</span></span> |<span data-ttu-id="e959d-222">時間範圍</span><span class="sxs-lookup"><span data-stu-id="e959d-222">TimeSpan</span></span> |
| <span data-ttu-id="e959d-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="e959d-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="e959d-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="e959d-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="e959d-225">不支援 OData 複雜資料類型，例如，物件。</span><span class="sxs-lookup"><span data-stu-id="e959d-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="e959d-226">JSON 範例：將資料從 OData 來源複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e959d-226">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="e959d-227">此範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="e959d-227">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e959d-228">這些範例示範如何把 OData 來源的資料複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e959d-228">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="e959d-229">不過，您可以在 Azure Data Factory 中使用複製活動，將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="e959d-229">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="e959d-230">範例有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="e959d-230">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="e959d-231">[OData](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="e959d-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="e959d-232">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="e959d-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e959d-233">[ODataResource](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="e959d-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="e959d-234">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="e959d-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e959d-235">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="e959d-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e959d-236">範例會每隔一小時依照 OData 來源，把查詢來的資料複製到 Azure Blob 中。</span><span class="sxs-lookup"><span data-stu-id="e959d-236">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="e959d-237">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="e959d-237">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="e959d-238">**OData 已連結的服務：**此範例會使用匿名驗證。</span><span class="sxs-lookup"><span data-stu-id="e959d-238">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="e959d-239">請參閱 [OData 連結服務](#linked-service-properties) 一節，來了解您可以使用的不同驗證類型。</span><span class="sxs-lookup"><span data-stu-id="e959d-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="e959d-240">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="e959d-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="e959d-241">**OData 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="e959d-241">**OData input dataset:**</span></span>

<span data-ttu-id="e959d-242">設定 “external”: ”true” 會通知 Data Factory 服務：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="e959d-242">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="e959d-243">在資料集定義中指定 **path** 的動作是可以省略的。</span><span class="sxs-lookup"><span data-stu-id="e959d-243">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="e959d-244">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="e959d-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e959d-245">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="e959d-245">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e959d-246">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="e959d-246">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="e959d-247">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="e959d-247">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="e959d-248">**具有 OData 來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="e959d-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="e959d-249">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="e959d-249">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="e959d-250">在管線 JSON 定義中，已將 **source** 類型設為 **RelationalSource**，並將 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="e959d-250">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="e959d-251">針對 **query** 屬性所指定的 SQL 查詢，會從 OData 來源選取最新的資料。</span><span class="sxs-lookup"><span data-stu-id="e959d-251">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="e959d-252">在管線定義中指定 **query** 的動作是可以省略的。</span><span class="sxs-lookup"><span data-stu-id="e959d-252">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="e959d-253">Data Factory 服務用來擷取資料的 **URL** 就是：在連結服務中所指定的 URL (必要) + 在資料集所指定的路徑 (可省略) + 管線中的查詢 (可省略)。</span><span class="sxs-lookup"><span data-stu-id="e959d-253">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="e959d-254">OData 的類型對應</span><span class="sxs-lookup"><span data-stu-id="e959d-254">Type mapping for OData</span></span>
<span data-ttu-id="e959d-255">如同 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會使用下列 2 個步驟的方法，執行自動類型轉換，將來源類型轉換成接收類型：</span><span class="sxs-lookup"><span data-stu-id="e959d-255">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="e959d-256">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="e959d-256">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="e959d-257">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="e959d-257">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="e959d-258">當您移動 OData 資料存放區的資料時，OData 資料類型會對應到 .NET 類型。</span><span class="sxs-lookup"><span data-stu-id="e959d-258">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="e959d-259">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="e959d-259">Map source to sink columns</span></span>
<span data-ttu-id="e959d-260">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="e959d-260">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="e959d-261">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="e959d-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="e959d-262">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="e959d-262">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="e959d-263">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="e959d-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e959d-264">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="e959d-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e959d-265">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="e959d-265">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e959d-266">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="e959d-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e959d-267">效能和微調</span><span class="sxs-lookup"><span data-stu-id="e959d-267">Performance and Tuning</span></span>
<span data-ttu-id="e959d-268">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="e959d-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
