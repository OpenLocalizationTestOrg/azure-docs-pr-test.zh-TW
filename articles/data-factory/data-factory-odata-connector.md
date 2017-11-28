---
title: "從 OData 來源 aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從 OData toomove 資料來源使用 Azure Data Factory。"
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
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="4c3da-103">使用 Azure Data Factory 來移動 OData 來源的資料</span><span class="sxs-lookup"><span data-stu-id="4c3da-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="4c3da-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從 OData 來源中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="4c3da-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an OData source.</span></span> <span data-ttu-id="4c3da-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="4c3da-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="4c3da-106">您可以從 OData 來源 tooany 支援接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="4c3da-106">You can copy data from an OData source tooany supported sink data store.</span></span> <span data-ttu-id="4c3da-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="4c3da-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4c3da-108">資料處理站目前只支援移動資料從 OData 來源 tooother 資料存放區，但對於將資料從其他資料會儲存 tooan OData 來源。</span><span class="sxs-lookup"><span data-stu-id="4c3da-108">Data factory currently supports only moving data from an OData source tooother data stores, but not for moving data from other data stores tooan OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="4c3da-109">支援的版本和驗證類型</span><span class="sxs-lookup"><span data-stu-id="4c3da-109">Supported versions and authentication types</span></span>
<span data-ttu-id="4c3da-110">此 OData 連接器支援 OData 版本 3.0 和 4.0，而您可以從雲端 OData 和內部部署 OData 來源複製資料。</span><span class="sxs-lookup"><span data-stu-id="4c3da-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="4c3da-111">Hello 後者，您需要 tooinstall hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="4c3da-111">For hello latter, you need tooinstall hello Data Management Gateway.</span></span> <span data-ttu-id="4c3da-112">如需資料管理閘道的詳細資訊，請參閱 [在內部部署和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="4c3da-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="4c3da-113">支援下列驗證類型：</span><span class="sxs-lookup"><span data-stu-id="4c3da-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="4c3da-114">tooaccess**雲端**OData 摘要，您可以使用匿名、 基本 （使用者名稱和密碼） 或 Azure Active Directory 架構 OAuth 驗證。</span><span class="sxs-lookup"><span data-stu-id="4c3da-114">tooaccess **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="4c3da-115">tooaccess**內部**OData 摘要中，您可以使用匿名、 基本 （使用者名稱和密碼） 或 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="4c3da-115">tooaccess **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4c3da-116">開始使用</span><span class="sxs-lookup"><span data-stu-id="4c3da-116">Getting started</span></span>
<span data-ttu-id="4c3da-117">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 OData 來源移動資料。</span><span class="sxs-lookup"><span data-stu-id="4c3da-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="4c3da-118">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="4c3da-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="4c3da-119">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="4c3da-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="4c3da-120">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="4c3da-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4c3da-121">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="4c3da-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="4c3da-122">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c3da-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="4c3da-123">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="4c3da-123">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="4c3da-124">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="4c3da-124">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="4c3da-125">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="4c3da-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="4c3da-126">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="4c3da-126">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4c3da-127">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="4c3da-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="4c3da-128">使用 Data Factory 實體的 OData 來源的使用的 toocopy 資料的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 OData 來源 tooAzure Blob 複製](#json-example-copy-data-from-odata-source-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="4c3da-128">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an OData source, see [JSON example: Copy data from OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="4c3da-129">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooOData 來源的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="4c3da-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooOData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4c3da-130">已連結的服務屬性</span><span class="sxs-lookup"><span data-stu-id="4c3da-130">Linked Service properties</span></span>
<span data-ttu-id="4c3da-131">下表中的 hello 提供 JSON 項目特定 tooOData 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="4c3da-131">hello following table provides description for JSON elements specific tooOData linked service.</span></span>

| <span data-ttu-id="4c3da-132">屬性</span><span class="sxs-lookup"><span data-stu-id="4c3da-132">Property</span></span> | <span data-ttu-id="4c3da-133">說明</span><span class="sxs-lookup"><span data-stu-id="4c3da-133">Description</span></span> | <span data-ttu-id="4c3da-134">必要</span><span class="sxs-lookup"><span data-stu-id="4c3da-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c3da-135">類型</span><span class="sxs-lookup"><span data-stu-id="4c3da-135">type</span></span> |<span data-ttu-id="4c3da-136">hello 類型屬性必須設定為： **OData**</span><span class="sxs-lookup"><span data-stu-id="4c3da-136">hello type property must be set to: **OData**</span></span> |<span data-ttu-id="4c3da-137">是</span><span class="sxs-lookup"><span data-stu-id="4c3da-137">Yes</span></span> |
| <span data-ttu-id="4c3da-138">url</span><span class="sxs-lookup"><span data-stu-id="4c3da-138">url</span></span> |<span data-ttu-id="4c3da-139">Hello OData 服務的 Url。</span><span class="sxs-lookup"><span data-stu-id="4c3da-139">Url of hello OData service.</span></span> |<span data-ttu-id="4c3da-140">是</span><span class="sxs-lookup"><span data-stu-id="4c3da-140">Yes</span></span> |
| <span data-ttu-id="4c3da-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="4c3da-141">authenticationType</span></span> |<span data-ttu-id="4c3da-142">Tooconnect toohello OData 來源使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="4c3da-142">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="4c3da-143">若為雲端 OData，可能的值為 Anonymous、Basic 和 OAuth (請注意，Azure Data Factory 目前僅支援 Azure Active Directory 架構的 OAuth)。</span><span class="sxs-lookup"><span data-stu-id="4c3da-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="4c3da-144">若為內部部署 OData，可能的值為 Anonymous、Basic 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="4c3da-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="4c3da-145">是</span><span class="sxs-lookup"><span data-stu-id="4c3da-145">Yes</span></span> |
| <span data-ttu-id="4c3da-146">username</span><span class="sxs-lookup"><span data-stu-id="4c3da-146">username</span></span> |<span data-ttu-id="4c3da-147">如果您要使用 Basic 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="4c3da-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="4c3da-148">是 (只在您使用基本驗證時)</span><span class="sxs-lookup"><span data-stu-id="4c3da-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="4c3da-149">password</span><span class="sxs-lookup"><span data-stu-id="4c3da-149">password</span></span> |<span data-ttu-id="4c3da-150">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="4c3da-150">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="4c3da-151">是 (只在您使用基本驗證時)</span><span class="sxs-lookup"><span data-stu-id="4c3da-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="4c3da-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="4c3da-152">authorizedCredential</span></span> |<span data-ttu-id="4c3da-153">如果您使用 OAuth 時，按一下**授權**按鈕 hello 資料 Factory 複製精靈或編輯器中，輸入您的認證，然後 hello 這個屬性的值將會自動產生。</span><span class="sxs-lookup"><span data-stu-id="4c3da-153">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="4c3da-154">是 (只有在您使用 OAuth 驗證時)</span><span class="sxs-lookup"><span data-stu-id="4c3da-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="4c3da-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="4c3da-155">gatewayName</span></span> |<span data-ttu-id="4c3da-156">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 OData 服務。</span><span class="sxs-lookup"><span data-stu-id="4c3da-156">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="4c3da-157">只在要從內部部署 OData 來源複製資料時才指定。</span><span class="sxs-lookup"><span data-stu-id="4c3da-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="4c3da-158">否</span><span class="sxs-lookup"><span data-stu-id="4c3da-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="4c3da-159">使用基本驗證</span><span class="sxs-lookup"><span data-stu-id="4c3da-159">Using Basic authentication</span></span>
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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="4c3da-160">使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="4c3da-160">Using Anonymous authentication</span></span>
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

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="4c3da-161">使用存取內部部署 OData 來源的 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="4c3da-161">Using Windows authentication accessing on-premises OData source</span></span>
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

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="4c3da-162">使用 OAuth 驗證存取雲端 OData 來源</span><span class="sxs-lookup"><span data-stu-id="4c3da-162">Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="4c3da-163">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="4c3da-163">Dataset properties</span></span>
<span data-ttu-id="4c3da-164">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="4c3da-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4c3da-165">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="4c3da-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="4c3da-166">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4c3da-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="4c3da-167">hello typeProperties 區段類型的資料集**ODataResource** （包括 OData 資料集） 具有下列屬性的 hello</span><span class="sxs-lookup"><span data-stu-id="4c3da-167">hello typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has hello following properties</span></span>

| <span data-ttu-id="4c3da-168">屬性</span><span class="sxs-lookup"><span data-stu-id="4c3da-168">Property</span></span> | <span data-ttu-id="4c3da-169">說明</span><span class="sxs-lookup"><span data-stu-id="4c3da-169">Description</span></span> | <span data-ttu-id="4c3da-170">必要</span><span class="sxs-lookup"><span data-stu-id="4c3da-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c3da-171">路徑</span><span class="sxs-lookup"><span data-stu-id="4c3da-171">path</span></span> |<span data-ttu-id="4c3da-172">路徑 toohello OData 資源</span><span class="sxs-lookup"><span data-stu-id="4c3da-172">Path toohello OData resource</span></span> |<span data-ttu-id="4c3da-173">否</span><span class="sxs-lookup"><span data-stu-id="4c3da-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="4c3da-174">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="4c3da-174">Copy activity properties</span></span>
<span data-ttu-id="4c3da-175">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="4c3da-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4c3da-176">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="4c3da-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="4c3da-177">屬性中的 hello hello 活動 hello typeProperties 區段可用另一方面會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="4c3da-177">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="4c3da-178">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="4c3da-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="4c3da-179">當來源屬於型別**RelationalSource** （包括 OData） typeProperties 節中會使用下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c3da-179">When source is of type **RelationalSource** (which includes OData) hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="4c3da-180">屬性</span><span class="sxs-lookup"><span data-stu-id="4c3da-180">Property</span></span> | <span data-ttu-id="4c3da-181">說明</span><span class="sxs-lookup"><span data-stu-id="4c3da-181">Description</span></span> | <span data-ttu-id="4c3da-182">範例</span><span class="sxs-lookup"><span data-stu-id="4c3da-182">Example</span></span> | <span data-ttu-id="4c3da-183">必要</span><span class="sxs-lookup"><span data-stu-id="4c3da-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4c3da-184">query</span><span class="sxs-lookup"><span data-stu-id="4c3da-184">query</span></span> |<span data-ttu-id="4c3da-185">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="4c3da-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="4c3da-186">「?$select=Name, Description&$top=5」</span><span class="sxs-lookup"><span data-stu-id="4c3da-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="4c3da-187">否</span><span class="sxs-lookup"><span data-stu-id="4c3da-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="4c3da-188">OData 的類型對應</span><span class="sxs-lookup"><span data-stu-id="4c3da-188">Type Mapping for OData</span></span>
<span data-ttu-id="4c3da-189">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello。</span><span class="sxs-lookup"><span data-stu-id="4c3da-189">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="4c3da-190">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="4c3da-190">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="4c3da-191">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="4c3da-191">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="4c3da-192">從 OData 資料時，hello 下列會使用對應從 OData 類型 too.NET 型別。</span><span class="sxs-lookup"><span data-stu-id="4c3da-192">When moving data from OData, hello following mappings are used from OData types too.NET type.</span></span>

| <span data-ttu-id="4c3da-193">OData 資料類型</span><span class="sxs-lookup"><span data-stu-id="4c3da-193">OData Data Type</span></span> | <span data-ttu-id="4c3da-194">.NET 類型</span><span class="sxs-lookup"><span data-stu-id="4c3da-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="4c3da-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="4c3da-195">Edm.Binary</span></span> |<span data-ttu-id="4c3da-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4c3da-196">Byte[]</span></span> |
| <span data-ttu-id="4c3da-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="4c3da-197">Edm.Boolean</span></span> |<span data-ttu-id="4c3da-198">Bool</span><span class="sxs-lookup"><span data-stu-id="4c3da-198">Bool</span></span> |
| <span data-ttu-id="4c3da-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="4c3da-199">Edm.Byte</span></span> |<span data-ttu-id="4c3da-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4c3da-200">Byte[]</span></span> |
| <span data-ttu-id="4c3da-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="4c3da-201">Edm.DateTime</span></span> |<span data-ttu-id="4c3da-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="4c3da-202">DateTime</span></span> |
| <span data-ttu-id="4c3da-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="4c3da-203">Edm.Decimal</span></span> |<span data-ttu-id="4c3da-204">十進位</span><span class="sxs-lookup"><span data-stu-id="4c3da-204">Decimal</span></span> |
| <span data-ttu-id="4c3da-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="4c3da-205">Edm.Double</span></span> |<span data-ttu-id="4c3da-206">兩倍</span><span class="sxs-lookup"><span data-stu-id="4c3da-206">Double</span></span> |
| <span data-ttu-id="4c3da-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="4c3da-207">Edm.Single</span></span> |<span data-ttu-id="4c3da-208">單一</span><span class="sxs-lookup"><span data-stu-id="4c3da-208">Single</span></span> |
| <span data-ttu-id="4c3da-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="4c3da-209">Edm.Guid</span></span> |<span data-ttu-id="4c3da-210">Guid</span><span class="sxs-lookup"><span data-stu-id="4c3da-210">Guid</span></span> |
| <span data-ttu-id="4c3da-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="4c3da-211">Edm.Int16</span></span> |<span data-ttu-id="4c3da-212">Int16</span><span class="sxs-lookup"><span data-stu-id="4c3da-212">Int16</span></span> |
| <span data-ttu-id="4c3da-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="4c3da-213">Edm.Int32</span></span> |<span data-ttu-id="4c3da-214">Int32</span><span class="sxs-lookup"><span data-stu-id="4c3da-214">Int32</span></span> |
| <span data-ttu-id="4c3da-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="4c3da-215">Edm.Int64</span></span> |<span data-ttu-id="4c3da-216">Int64</span><span class="sxs-lookup"><span data-stu-id="4c3da-216">Int64</span></span> |
| <span data-ttu-id="4c3da-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="4c3da-217">Edm.SByte</span></span> |<span data-ttu-id="4c3da-218">Int16</span><span class="sxs-lookup"><span data-stu-id="4c3da-218">Int16</span></span> |
| <span data-ttu-id="4c3da-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="4c3da-219">Edm.String</span></span> |<span data-ttu-id="4c3da-220">String</span><span class="sxs-lookup"><span data-stu-id="4c3da-220">String</span></span> |
| <span data-ttu-id="4c3da-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="4c3da-221">Edm.Time</span></span> |<span data-ttu-id="4c3da-222">時間範圍</span><span class="sxs-lookup"><span data-stu-id="4c3da-222">TimeSpan</span></span> |
| <span data-ttu-id="4c3da-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="4c3da-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="4c3da-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="4c3da-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="4c3da-225">不支援 OData 複雜資料類型，例如，物件。</span><span class="sxs-lookup"><span data-stu-id="4c3da-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a><span data-ttu-id="4c3da-226">JSON 範例： 從 OData 來源 tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="4c3da-226">JSON example: Copy data from OData source tooAzure Blob</span></span>
<span data-ttu-id="4c3da-227">此範例中提供的範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="4c3da-227">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="4c3da-228">它們會顯示如何 toocopy 資料從 OData 來源 tooan Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4c3da-228">They show how toocopy data from an OData source tooan Azure Blob Storage.</span></span> <span data-ttu-id="4c3da-229">不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="4c3da-229">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="4c3da-230">hello 範例有下列 Data Factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c3da-230">hello sample has hello following Data Factory entities:</span></span>

1. <span data-ttu-id="4c3da-231">[OData](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="4c3da-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="4c3da-232">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="4c3da-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4c3da-233">[ODataResource](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="4c3da-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="4c3da-234">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="4c3da-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4c3da-235">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="4c3da-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="4c3da-236">hello 範例會將資料從查詢的 OData 來源 tooan 針對 Azure blob 的每個小時。</span><span class="sxs-lookup"><span data-stu-id="4c3da-236">hello sample copies data from querying against an OData source tooan Azure blob every hour.</span></span> <span data-ttu-id="4c3da-237">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="4c3da-237">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="4c3da-238">**OData 連結的服務：**本例使用 hello 匿名驗證。</span><span class="sxs-lookup"><span data-stu-id="4c3da-238">**OData linked service:** This example uses hello Anonymous authentication.</span></span> <span data-ttu-id="4c3da-239">請參閱 [OData 連結服務](#linked-service-properties) 一節，來了解您可以使用的不同驗證類型。</span><span class="sxs-lookup"><span data-stu-id="4c3da-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="4c3da-240">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="4c3da-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="4c3da-241">**OData 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="4c3da-241">**OData input dataset:**</span></span>

<span data-ttu-id="4c3da-242">設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="4c3da-242">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="4c3da-243">指定**路徑**hello 資料集定義為選擇性。</span><span class="sxs-lookup"><span data-stu-id="4c3da-243">Specifying **path** in hello dataset definition is optional.</span></span>

<span data-ttu-id="4c3da-244">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="4c3da-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="4c3da-245">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="4c3da-245">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4c3da-246">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="4c3da-246">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4c3da-247">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="4c3da-247">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


<span data-ttu-id="4c3da-248">**具有 OData 來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="4c3da-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="4c3da-249">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="4c3da-249">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="4c3da-250">在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="4c3da-250">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="4c3da-251">指定 hello SQL 查詢**查詢**屬性從 hello OData 來源選取 hello 最新 （最新版） 的資料。</span><span class="sxs-lookup"><span data-stu-id="4c3da-251">hello SQL query specified for hello **query** property selects hello latest (newest) data from hello OData source.</span></span>

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

<span data-ttu-id="4c3da-252">指定**查詢**hello 管線中定義為選擇性。</span><span class="sxs-lookup"><span data-stu-id="4c3da-252">Specifying **query** in hello pipeline definition is optional.</span></span> <span data-ttu-id="4c3da-253">hello **URL** hello Data Factory 服務會使用 tooretrieve 資料是： hello 連結的服務 （必要） + （選擇性） hello 資料集中指定的路徑，+ hello 管線 （選擇性） 在查詢中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="4c3da-253">hello **URL** that hello Data Factory service uses tooretrieve data is: URL specified in hello linked service (required) + path specified in hello dataset (optional) + query in hello pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="4c3da-254">OData 的類型對應</span><span class="sxs-lookup"><span data-stu-id="4c3da-254">Type mapping for OData</span></span>
<span data-ttu-id="4c3da-255">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以 hello 遵循 2 步驟方法：</span><span class="sxs-lookup"><span data-stu-id="4c3da-255">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="4c3da-256">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="4c3da-256">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="4c3da-257">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="4c3da-257">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="4c3da-258">當您從 OData 資料存放區中移動資料，OData 資料類型都是對應的 too.NET 類型。</span><span class="sxs-lookup"><span data-stu-id="4c3da-258">When moving data from OData data stores, OData data types are mapped too.NET types.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="4c3da-259">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="4c3da-259">Map source toosink columns</span></span>
<span data-ttu-id="4c3da-260">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="4c3da-260">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="4c3da-261">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="4c3da-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="4c3da-262">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="4c3da-262">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="4c3da-263">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="4c3da-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="4c3da-264">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="4c3da-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="4c3da-265">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="4c3da-265">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="4c3da-266">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="4c3da-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4c3da-267">效能和微調</span><span class="sxs-lookup"><span data-stu-id="4c3da-267">Performance and Tuning</span></span>
<span data-ttu-id="4c3da-268">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="4c3da-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
