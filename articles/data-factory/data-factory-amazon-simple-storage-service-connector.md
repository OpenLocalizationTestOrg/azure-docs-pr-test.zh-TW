---
title: "使用 Data Factory 的 aaaMove 資料從 Amazon 簡單的儲存體服務 |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 toomove 資料從 Amazon 簡單儲存體服務 (S3)。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="3ae30-103">使用 Azure Data Factory 從 Amazon Simple Storage Service 移動資料</span><span class="sxs-lookup"><span data-stu-id="3ae30-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="3ae30-104">本文說明如何 toouse hello 複製在 Azure Data Factory toomove 資料從 Amazon 簡單儲存體服務 (S3) 活動。</span><span class="sxs-lookup"><span data-stu-id="3ae30-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="3ae30-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="3ae30-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="3ae30-106">您可以從 Amazon S3 tooany 支援接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="3ae30-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="3ae30-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="3ae30-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="3ae30-108">Data Factory 目前支援從 Amazon S3 tooother 資料存放區的唯一移動資料，但不是將資料從其他資料會儲存 tooAmazon S3。</span><span class="sxs-lookup"><span data-stu-id="3ae30-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="3ae30-109">所需的權限</span><span class="sxs-lookup"><span data-stu-id="3ae30-109">Required permissions</span></span>
<span data-ttu-id="3ae30-110">toocopy 資料從 Amazon S3，請確定您已獲得下列權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="3ae30-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="3ae30-111">適用於 Amazon S3 物件作業的 `s3:GetObject` 和 `s3:GetObjectVersion`。</span><span class="sxs-lookup"><span data-stu-id="3ae30-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="3ae30-112">適用於 Amazon S3 貯體作業的 `s3:ListBucket`。</span><span class="sxs-lookup"><span data-stu-id="3ae30-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="3ae30-113">如果您使用 Data Factory 複製精靈中，hello`s3:ListAllMyBuckets`也是必要欄位。</span><span class="sxs-lookup"><span data-stu-id="3ae30-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="3ae30-114">如需 hello 的 Amazon S3 權限的完整清單的詳細資訊，請參閱[原則中指定的權限](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="3ae30-115">開始使用</span><span class="sxs-lookup"><span data-stu-id="3ae30-115">Getting started</span></span>
<span data-ttu-id="3ae30-116">您可以藉由使用不同的工具或 API，建立內含複製活動的管線，以從 Amazon S3 來源移動資料。</span><span class="sxs-lookup"><span data-stu-id="3ae30-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="3ae30-117">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="3ae30-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="3ae30-118">如需快速逐步解說，請參閱[教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="3ae30-119">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="3ae30-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3ae30-120">如需逐步指示 toocreate 具有複製活動的管線，請參閱 hello[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="3ae30-121">無論您是使用工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="3ae30-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="3ae30-122">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="3ae30-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="3ae30-123">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="3ae30-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="3ae30-124">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="3ae30-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="3ae30-125">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="3ae30-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="3ae30-126">當您使用工具或 Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="3ae30-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="3ae30-127">使用 Data Factory 實體的 Amazon S3 資料存放區中的使用的 toocopy 資料的 JSON 定義中的範例，請參閱 hello [JSON 範例： 將資料從 Amazon S3 tooAzure Blob 複製](#json-example-copy-data-from-amazon-s3-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="3ae30-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="3ae30-128">如需有關針對複製活動支援的檔案和壓縮格式的詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="3ae30-129">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAmazon S3 的 JSON 屬性的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3ae30-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3ae30-130">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="3ae30-130">Linked service properties</span></span>
<span data-ttu-id="3ae30-131">連結的服務連結資料儲存區 tooa data factory。</span><span class="sxs-lookup"><span data-stu-id="3ae30-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="3ae30-132">您建立連結的服務型別的**AwsAccessKey** toolink Amazon S3 資料儲存 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="3ae30-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="3ae30-133">下表中的 hello 提供描述的 JSON 元素特定 tooAmazon S3 (AwsAccessKey) 連結服務。</span><span class="sxs-lookup"><span data-stu-id="3ae30-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="3ae30-134">屬性</span><span class="sxs-lookup"><span data-stu-id="3ae30-134">Property</span></span> | <span data-ttu-id="3ae30-135">說明</span><span class="sxs-lookup"><span data-stu-id="3ae30-135">Description</span></span> | <span data-ttu-id="3ae30-136">允許的值</span><span class="sxs-lookup"><span data-stu-id="3ae30-136">Allowed values</span></span> | <span data-ttu-id="3ae30-137">必要</span><span class="sxs-lookup"><span data-stu-id="3ae30-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ae30-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="3ae30-138">accessKeyID</span></span> |<span data-ttu-id="3ae30-139">Hello 密碼的存取金鑰的識別碼。</span><span class="sxs-lookup"><span data-stu-id="3ae30-139">ID of hello secret access key.</span></span> |<span data-ttu-id="3ae30-140">字串</span><span class="sxs-lookup"><span data-stu-id="3ae30-140">string</span></span> |<span data-ttu-id="3ae30-141">是</span><span class="sxs-lookup"><span data-stu-id="3ae30-141">Yes</span></span> |
| <span data-ttu-id="3ae30-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="3ae30-142">secretAccessKey</span></span> |<span data-ttu-id="3ae30-143">hello 密碼存取金鑰本身。</span><span class="sxs-lookup"><span data-stu-id="3ae30-143">hello secret access key itself.</span></span> |<span data-ttu-id="3ae30-144">加密的密碼字串</span><span class="sxs-lookup"><span data-stu-id="3ae30-144">Encrypted secret string</span></span> |<span data-ttu-id="3ae30-145">是</span><span class="sxs-lookup"><span data-stu-id="3ae30-145">Yes</span></span> |

<span data-ttu-id="3ae30-146">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="3ae30-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="3ae30-147">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="3ae30-147">Dataset properties</span></span>
<span data-ttu-id="3ae30-148">資料集 toorepresent toospecify 輸入 Azure Blob 儲存體，hello 類型的屬性設定 hello 資料集的資料太**AmazonS3**。</span><span class="sxs-lookup"><span data-stu-id="3ae30-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="3ae30-149">設定 hello **linkedServiceName**連結服務的 hello Amazon S3 hello 資料集 toohello 名稱的內容。</span><span class="sxs-lookup"><span data-stu-id="3ae30-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="3ae30-150">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="3ae30-151">所有資料集類型 (例如 SQL 資料庫、Azure Blob 及 Azure 資料表) 的結構、可用性及原則等區段都相似。</span><span class="sxs-lookup"><span data-stu-id="3ae30-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="3ae30-152">hello **typeProperties**章節是不同的每種類型的資料集，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3ae30-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="3ae30-153">hello **typeProperties**類型的資料集區段**AmazonS3** （包括 hello Amazon S3 資料集） 具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="3ae30-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="3ae30-154">屬性</span><span class="sxs-lookup"><span data-stu-id="3ae30-154">Property</span></span> | <span data-ttu-id="3ae30-155">說明</span><span class="sxs-lookup"><span data-stu-id="3ae30-155">Description</span></span> | <span data-ttu-id="3ae30-156">允許的值</span><span class="sxs-lookup"><span data-stu-id="3ae30-156">Allowed values</span></span> | <span data-ttu-id="3ae30-157">必要</span><span class="sxs-lookup"><span data-stu-id="3ae30-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ae30-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="3ae30-158">bucketName</span></span> |<span data-ttu-id="3ae30-159">hello S3 值區的名稱。</span><span class="sxs-lookup"><span data-stu-id="3ae30-159">hello S3 bucket name.</span></span> |<span data-ttu-id="3ae30-160">String</span><span class="sxs-lookup"><span data-stu-id="3ae30-160">String</span></span> |<span data-ttu-id="3ae30-161">是</span><span class="sxs-lookup"><span data-stu-id="3ae30-161">Yes</span></span> |
| <span data-ttu-id="3ae30-162">key</span><span class="sxs-lookup"><span data-stu-id="3ae30-162">key</span></span> |<span data-ttu-id="3ae30-163">hello S3 物件索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3ae30-163">hello S3 object key.</span></span> |<span data-ttu-id="3ae30-164">String</span><span class="sxs-lookup"><span data-stu-id="3ae30-164">String</span></span> |<span data-ttu-id="3ae30-165">否</span><span class="sxs-lookup"><span data-stu-id="3ae30-165">No</span></span> |
| <span data-ttu-id="3ae30-166">prefix</span><span class="sxs-lookup"><span data-stu-id="3ae30-166">prefix</span></span> |<span data-ttu-id="3ae30-167">Hello S3 物件索引鍵的前置詞。</span><span class="sxs-lookup"><span data-stu-id="3ae30-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="3ae30-168">系統會選取索引鍵以此前置詞開頭的物件。</span><span class="sxs-lookup"><span data-stu-id="3ae30-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="3ae30-169">只有當索引鍵空白時才適用。</span><span class="sxs-lookup"><span data-stu-id="3ae30-169">Applies only when key is empty.</span></span> |<span data-ttu-id="3ae30-170">string</span><span class="sxs-lookup"><span data-stu-id="3ae30-170">String</span></span> |<span data-ttu-id="3ae30-171">否</span><span class="sxs-lookup"><span data-stu-id="3ae30-171">No</span></span> |
| <span data-ttu-id="3ae30-172">版本</span><span class="sxs-lookup"><span data-stu-id="3ae30-172">version</span></span> |<span data-ttu-id="3ae30-173">hello 的 hello S3 物件，如果已啟用 S3 版本控制的版本。</span><span class="sxs-lookup"><span data-stu-id="3ae30-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="3ae30-174">String</span><span class="sxs-lookup"><span data-stu-id="3ae30-174">String</span></span> |<span data-ttu-id="3ae30-175">否</span><span class="sxs-lookup"><span data-stu-id="3ae30-175">No</span></span> |
| <span data-ttu-id="3ae30-176">format</span><span class="sxs-lookup"><span data-stu-id="3ae30-176">format</span></span> | <span data-ttu-id="3ae30-177">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="3ae30-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3ae30-178">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="3ae30-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="3ae30-179">如需詳細資訊，請參閱 hello[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)， [JSON 格式](data-factory-supported-file-and-compression-formats.md#json-format)， [Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)， [Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)，和[Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)區段。</span><span class="sxs-lookup"><span data-stu-id="3ae30-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="3ae30-180">如果您想要為 toocopy 檔案-之間以檔案為基礎存放區 （二進位複製），略過 hello 格式 > 一節中這兩個輸入和輸出資料集定義。</span><span class="sxs-lookup"><span data-stu-id="3ae30-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3ae30-181">否</span><span class="sxs-lookup"><span data-stu-id="3ae30-181">No</span></span> | |
| <span data-ttu-id="3ae30-182">compression</span><span class="sxs-lookup"><span data-stu-id="3ae30-182">compression</span></span> | <span data-ttu-id="3ae30-183">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="3ae30-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="3ae30-184">hello 支援型別： **GZip**， **Deflate**， **BZip2**，和**ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="3ae30-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="3ae30-185">hello 支援層級為：**最佳**和**最快**。</span><span class="sxs-lookup"><span data-stu-id="3ae30-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3ae30-186">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3ae30-187">否</span><span class="sxs-lookup"><span data-stu-id="3ae30-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="3ae30-188">**bucketName + 鍵**指定 hello hello S3 物件，其中值區是 hello S3 物件的根容器，而索引鍵是 hello 完整路徑 toohello S3 物件位置。</span><span class="sxs-lookup"><span data-stu-id="3ae30-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="3ae30-189">prefix 的相關範例資料集</span><span class="sxs-lookup"><span data-stu-id="3ae30-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="3ae30-190">範例資料集 (含版本)</span><span class="sxs-lookup"><span data-stu-id="3ae30-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="3ae30-191">S3 的動態路徑</span><span class="sxs-lookup"><span data-stu-id="3ae30-191">Dynamic paths for S3</span></span>
<span data-ttu-id="3ae30-192">hello 上述範例會使用固定的值為 hello**金鑰**和**bucketName** hello Amazon S3 資料集中的屬性。</span><span class="sxs-lookup"><span data-stu-id="3ae30-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="3ae30-193">您可以藉由使用系統變數 (例如 SliceStart)，讓 Data Factory 在執行階段動態地計算這些屬性。</span><span class="sxs-lookup"><span data-stu-id="3ae30-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="3ae30-194">您可以相同 hello hello**前置詞**Amazon S3 資料集的屬性。</span><span class="sxs-lookup"><span data-stu-id="3ae30-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="3ae30-195">如需支援的函式和變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="3ae30-196">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="3ae30-196">Copy activity properties</span></span>
<span data-ttu-id="3ae30-197">如需可用來定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="3ae30-198">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="3ae30-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="3ae30-199">屬性用於 hello **typeProperties** hello 活動的區段會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="3ae30-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="3ae30-200">Hello 複製活動，根據 hello 類型的來源與接收屬性而有所不同。</span><span class="sxs-lookup"><span data-stu-id="3ae30-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="3ae30-201">Hello 複製活動中的來源時的型別**FileSystemSource** （包括 Amazon S3），下列屬性的 hello 位於**typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="3ae30-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="3ae30-202">屬性</span><span class="sxs-lookup"><span data-stu-id="3ae30-202">Property</span></span> | <span data-ttu-id="3ae30-203">說明</span><span class="sxs-lookup"><span data-stu-id="3ae30-203">Description</span></span> | <span data-ttu-id="3ae30-204">允許的值</span><span class="sxs-lookup"><span data-stu-id="3ae30-204">Allowed values</span></span> | <span data-ttu-id="3ae30-205">必要</span><span class="sxs-lookup"><span data-stu-id="3ae30-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ae30-206">遞迴</span><span class="sxs-lookup"><span data-stu-id="3ae30-206">recursive</span></span> |<span data-ttu-id="3ae30-207">指定是否 toorecursively 清單 S3 物件 hello 目錄下。</span><span class="sxs-lookup"><span data-stu-id="3ae30-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="3ae30-208">true/false</span><span class="sxs-lookup"><span data-stu-id="3ae30-208">true/false</span></span> |<span data-ttu-id="3ae30-209">否</span><span class="sxs-lookup"><span data-stu-id="3ae30-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="3ae30-210">JSON 範例： 從 Amazon S3 tooAzure Blob 儲存體複製資料</span><span class="sxs-lookup"><span data-stu-id="3ae30-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="3ae30-211">這個範例示範如何從 Azure Blob 儲存體的 Amazon S3 tooan toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="3ae30-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="3ae30-212">不過，資料可以複製直接太[任何支援的 hello 接收](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 Data Factory 中的 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="3ae30-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="3ae30-213">hello 範例提供下列 Data Factory 實體的 hello 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="3ae30-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="3ae30-214">您可以使用這些定義 toocreate 管線 toocopy 資料從 Amazon S3 tooBlob 儲存體，使用 hello [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="3ae30-215">[AwsAccessKey](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="3ae30-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="3ae30-216">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="3ae30-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="3ae30-217">[AmazonS3](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="3ae30-218">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="3ae30-219">具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3ae30-220">hello 範例將資料從 Azure blob 的 Amazon S3 tooan 每小時。</span><span class="sxs-lookup"><span data-stu-id="3ae30-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="3ae30-221">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="3ae30-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="3ae30-222">Amazon S3 已連結的服務</span><span class="sxs-lookup"><span data-stu-id="3ae30-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="3ae30-223">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="3ae30-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="3ae30-224">Amazon S3 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="3ae30-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="3ae30-225">設定**"external": true**通知 hello Data Factory 服務該 hello 資料集是外部 toohello 資料處理站。</span><span class="sxs-lookup"><span data-stu-id="3ae30-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="3ae30-226">設定此屬性 tootrue 上就不會產生 hello 管線中活動的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="3ae30-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="3ae30-227">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="3ae30-227">Azure Blob output dataset</span></span>

<span data-ttu-id="3ae30-228">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3ae30-229">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="3ae30-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="3ae30-230">hello 資料夾路徑會使用 hello 的 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="3ae30-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="3ae30-231">具有 Amazon S3 來源和 Blob 接收器的管線中複製活動</span><span class="sxs-lookup"><span data-stu-id="3ae30-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="3ae30-232">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="3ae30-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="3ae30-233">在 hello 管線 JSON 定義中，hello**來源**類型設定得**FileSystemSource**，和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="3ae30-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="3ae30-234">請參閱 < 從接收的資料集、 來源資料集 toocolumns toomap 資料行[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="3ae30-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ae30-235">Next steps</span></span>
<span data-ttu-id="3ae30-236">請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="3ae30-236">See hello following articles:</span></span>

* <span data-ttu-id="3ae30-237">關於金鑰 toolearn 因素影響效能的 Data Factory 中的資料移動 （複製活動） 和各種方式 toooptimize 的請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="3ae30-238">複製活動與建立管線的逐步指示，請參閱 hello[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae30-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
