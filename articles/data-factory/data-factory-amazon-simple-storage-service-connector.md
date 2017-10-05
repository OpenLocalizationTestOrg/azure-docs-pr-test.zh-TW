---
title: "使用 Data Factory 從 Amazon Simple Storage Service 移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 Amazon Simple Storage Service (S3) 移動資料。"
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
ms.openlocfilehash: 3e21f7dfccc3b235071344a28c7d94f65e6bf9ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="5f10b-103">使用 Azure Data Factory 從 Amazon Simple Storage Service 移動資料</span><span class="sxs-lookup"><span data-stu-id="5f10b-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="5f10b-104">本文說明如何使用 Azure Data Factory 中的複製活動，從 Amazon Simple Storage Service (S3) 移動資料。</span><span class="sxs-lookup"><span data-stu-id="5f10b-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="5f10b-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="5f10b-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="5f10b-106">您可以將資料從 Amazon S3 複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5f10b-106">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="5f10b-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格。</span><span class="sxs-lookup"><span data-stu-id="5f10b-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="5f10b-108">Data Factory 目前只支援將資料從 Amazon S3 移到其他資料存放區，而不支援將資料從其他資料存放區移到 Amazon S3。</span><span class="sxs-lookup"><span data-stu-id="5f10b-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="5f10b-109">所需的權限</span><span class="sxs-lookup"><span data-stu-id="5f10b-109">Required permissions</span></span>
<span data-ttu-id="5f10b-110">若要從 Amazon S3 複製資料，請確定您已獲得下列權限︰</span><span class="sxs-lookup"><span data-stu-id="5f10b-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="5f10b-111">適用於 Amazon S3 物件作業的 `s3:GetObject` 和 `s3:GetObjectVersion`。</span><span class="sxs-lookup"><span data-stu-id="5f10b-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="5f10b-112">適用於 Amazon S3 貯體作業的 `s3:ListBucket`。</span><span class="sxs-lookup"><span data-stu-id="5f10b-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="5f10b-113">如果您要使用「Data Factory 複製精靈」，則也需要 `s3:ListAllMyBuckets`。</span><span class="sxs-lookup"><span data-stu-id="5f10b-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="5f10b-114">如需有關完整 Amazon S3 權限清單的詳細資料，請參閱[在原則中指定權限 (英文)](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="5f10b-115">開始使用</span><span class="sxs-lookup"><span data-stu-id="5f10b-115">Getting started</span></span>
<span data-ttu-id="5f10b-116">您可以藉由使用不同的工具或 API，建立內含複製活動的管線，以從 Amazon S3 來源移動資料。</span><span class="sxs-lookup"><span data-stu-id="5f10b-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="5f10b-117">若要建立管線，最簡單的方式就是使用**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="5f10b-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="5f10b-118">如需快速逐步解說，請參閱[教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="5f10b-119">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="5f10b-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5f10b-120">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="5f10b-121">不論您是使用工具還是 API，都需執行下列步驟，以建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="5f10b-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="5f10b-122">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="5f10b-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="5f10b-123">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="5f10b-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="5f10b-124">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="5f10b-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="5f10b-125">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="5f10b-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="5f10b-126">使用工具或 API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="5f10b-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="5f10b-127">如需相關範例，其中含有用來從 Amazon S3 資料存放區複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 Amazon S3 複製到 Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="5f10b-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="5f10b-128">如需有關針對複製活動支援的檔案和壓縮格式的詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="5f10b-129">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 Amazon S3 特定的 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="5f10b-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5f10b-130">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="5f10b-130">Linked service properties</span></span>
<span data-ttu-id="5f10b-131">已連結的服務會將資料存放區連結到 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="5f10b-131">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="5f10b-132">您需建立 **AwsAccessKey** 類型的已連結服務，以將 Amazon S3 資料存放區連結到 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="5f10b-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="5f10b-133">下表提供 Amazon S3 (AwsAccessKey) 已連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="5f10b-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="5f10b-134">屬性</span><span class="sxs-lookup"><span data-stu-id="5f10b-134">Property</span></span> | <span data-ttu-id="5f10b-135">說明</span><span class="sxs-lookup"><span data-stu-id="5f10b-135">Description</span></span> | <span data-ttu-id="5f10b-136">允許的值</span><span class="sxs-lookup"><span data-stu-id="5f10b-136">Allowed values</span></span> | <span data-ttu-id="5f10b-137">必要</span><span class="sxs-lookup"><span data-stu-id="5f10b-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f10b-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="5f10b-138">accessKeyID</span></span> |<span data-ttu-id="5f10b-139">密碼存取金鑰的識別碼。</span><span class="sxs-lookup"><span data-stu-id="5f10b-139">ID of the secret access key.</span></span> |<span data-ttu-id="5f10b-140">string</span><span class="sxs-lookup"><span data-stu-id="5f10b-140">string</span></span> |<span data-ttu-id="5f10b-141">是</span><span class="sxs-lookup"><span data-stu-id="5f10b-141">Yes</span></span> |
| <span data-ttu-id="5f10b-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="5f10b-142">secretAccessKey</span></span> |<span data-ttu-id="5f10b-143">密碼存取金鑰本身。</span><span class="sxs-lookup"><span data-stu-id="5f10b-143">The secret access key itself.</span></span> |<span data-ttu-id="5f10b-144">加密的密碼字串</span><span class="sxs-lookup"><span data-stu-id="5f10b-144">Encrypted secret string</span></span> |<span data-ttu-id="5f10b-145">是</span><span class="sxs-lookup"><span data-stu-id="5f10b-145">Yes</span></span> |

<span data-ttu-id="5f10b-146">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="5f10b-146">Here is an example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="5f10b-147">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="5f10b-147">Dataset properties</span></span>
<span data-ttu-id="5f10b-148">若要指定資料集以代表 Azure Blob 儲存體中的輸入資料，請將資料集的類型屬性設定成 **AmazonS3**。</span><span class="sxs-lookup"><span data-stu-id="5f10b-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="5f10b-149">請將資料集的 **linkedServiceName** 屬性設定成 Amazon S3 已連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="5f10b-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="5f10b-150">如需可供定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="5f10b-151">所有資料集類型 (例如 SQL 資料庫、Azure Blob 及 Azure 資料表) 的結構、可用性及原則等區段都相似。</span><span class="sxs-lookup"><span data-stu-id="5f10b-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="5f10b-152">每個類型之資料集的 **typeProperties** 區段都不同，可提供資料存放區中資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5f10b-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="5f10b-153">**AmazonS3** 類型之資料集 (包括 Amazon S3 資料集) 的 **typeProperties** 區段具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="5f10b-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="5f10b-154">屬性</span><span class="sxs-lookup"><span data-stu-id="5f10b-154">Property</span></span> | <span data-ttu-id="5f10b-155">說明</span><span class="sxs-lookup"><span data-stu-id="5f10b-155">Description</span></span> | <span data-ttu-id="5f10b-156">允許的值</span><span class="sxs-lookup"><span data-stu-id="5f10b-156">Allowed values</span></span> | <span data-ttu-id="5f10b-157">必要</span><span class="sxs-lookup"><span data-stu-id="5f10b-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f10b-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="5f10b-158">bucketName</span></span> |<span data-ttu-id="5f10b-159">S3 貯體名稱。</span><span class="sxs-lookup"><span data-stu-id="5f10b-159">The S3 bucket name.</span></span> |<span data-ttu-id="5f10b-160">string</span><span class="sxs-lookup"><span data-stu-id="5f10b-160">String</span></span> |<span data-ttu-id="5f10b-161">是</span><span class="sxs-lookup"><span data-stu-id="5f10b-161">Yes</span></span> |
| <span data-ttu-id="5f10b-162">key</span><span class="sxs-lookup"><span data-stu-id="5f10b-162">key</span></span> |<span data-ttu-id="5f10b-163">S3 物件索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5f10b-163">The S3 object key.</span></span> |<span data-ttu-id="5f10b-164">string</span><span class="sxs-lookup"><span data-stu-id="5f10b-164">String</span></span> |<span data-ttu-id="5f10b-165">否</span><span class="sxs-lookup"><span data-stu-id="5f10b-165">No</span></span> |
| <span data-ttu-id="5f10b-166">prefix</span><span class="sxs-lookup"><span data-stu-id="5f10b-166">prefix</span></span> |<span data-ttu-id="5f10b-167">S3 物件索引鍵的前置詞。</span><span class="sxs-lookup"><span data-stu-id="5f10b-167">Prefix for the S3 object key.</span></span> <span data-ttu-id="5f10b-168">系統會選取索引鍵以此前置詞開頭的物件。</span><span class="sxs-lookup"><span data-stu-id="5f10b-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="5f10b-169">只有當索引鍵空白時才適用。</span><span class="sxs-lookup"><span data-stu-id="5f10b-169">Applies only when key is empty.</span></span> |<span data-ttu-id="5f10b-170">string</span><span class="sxs-lookup"><span data-stu-id="5f10b-170">String</span></span> |<span data-ttu-id="5f10b-171">否</span><span class="sxs-lookup"><span data-stu-id="5f10b-171">No</span></span> |
| <span data-ttu-id="5f10b-172">version</span><span class="sxs-lookup"><span data-stu-id="5f10b-172">version</span></span> |<span data-ttu-id="5f10b-173">如果已啟用 S3 版本設定功能，則為 S3 物件的版本。</span><span class="sxs-lookup"><span data-stu-id="5f10b-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="5f10b-174">String</span><span class="sxs-lookup"><span data-stu-id="5f10b-174">String</span></span> |<span data-ttu-id="5f10b-175">否</span><span class="sxs-lookup"><span data-stu-id="5f10b-175">No</span></span> |
| <span data-ttu-id="5f10b-176">format</span><span class="sxs-lookup"><span data-stu-id="5f10b-176">format</span></span> | <span data-ttu-id="5f10b-177">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="5f10b-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="5f10b-178">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="5f10b-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="5f10b-179">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[JSON 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)小節。</span><span class="sxs-lookup"><span data-stu-id="5f10b-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="5f10b-180">如果您想要在檔案型存放區之間依原樣複製檔案 (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="5f10b-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="5f10b-181">否</span><span class="sxs-lookup"><span data-stu-id="5f10b-181">No</span></span> | |
| <span data-ttu-id="5f10b-182">compression</span><span class="sxs-lookup"><span data-stu-id="5f10b-182">compression</span></span> | <span data-ttu-id="5f10b-183">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="5f10b-183">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="5f10b-184">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="5f10b-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="5f10b-185">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="5f10b-185">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="5f10b-186">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="5f10b-187">否</span><span class="sxs-lookup"><span data-stu-id="5f10b-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="5f10b-188">**bucketName + key** 可指定 S3 物件的位置，其中 bucket (貯體) 是 S3 物件的根容器，而 key 是 S3 物件的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="5f10b-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="5f10b-189">prefix 的相關範例資料集</span><span class="sxs-lookup"><span data-stu-id="5f10b-189">Sample dataset with prefix</span></span>

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
### <a name="sample-dataset-with-version"></a><span data-ttu-id="5f10b-190">範例資料集 (含版本)</span><span class="sxs-lookup"><span data-stu-id="5f10b-190">Sample dataset (with version)</span></span>

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

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="5f10b-191">S3 的動態路徑</span><span class="sxs-lookup"><span data-stu-id="5f10b-191">Dynamic paths for S3</span></span>
<span data-ttu-id="5f10b-192">上述範例針對 Amazon S3 資料集內的 **key** 和 **bucketName** 屬性使用固定的值。</span><span class="sxs-lookup"><span data-stu-id="5f10b-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="5f10b-193">您可以藉由使用系統變數 (例如 SliceStart)，讓 Data Factory 在執行階段動態地計算這些屬性。</span><span class="sxs-lookup"><span data-stu-id="5f10b-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="5f10b-194">您也可以對 Amazon S3 資料集的 **prefix** 屬性執行相同的操作。</span><span class="sxs-lookup"><span data-stu-id="5f10b-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="5f10b-195">如需支援的函式和變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="5f10b-196">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="5f10b-196">Copy activity properties</span></span>
<span data-ttu-id="5f10b-197">如需可用來定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="5f10b-198">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="5f10b-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="5f10b-199">活動的 **typeProperties** 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="5f10b-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="5f10b-200">就複製活動而言，屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="5f10b-200">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="5f10b-201">當複製活動中的來源類型為 **FileSystemSource** (其中包括 Azure S3) 時，**typeProperties** 區段中會有下列可用屬性：</span><span class="sxs-lookup"><span data-stu-id="5f10b-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="5f10b-202">屬性</span><span class="sxs-lookup"><span data-stu-id="5f10b-202">Property</span></span> | <span data-ttu-id="5f10b-203">說明</span><span class="sxs-lookup"><span data-stu-id="5f10b-203">Description</span></span> | <span data-ttu-id="5f10b-204">允許的值</span><span class="sxs-lookup"><span data-stu-id="5f10b-204">Allowed values</span></span> | <span data-ttu-id="5f10b-205">必要</span><span class="sxs-lookup"><span data-stu-id="5f10b-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f10b-206">遞迴</span><span class="sxs-lookup"><span data-stu-id="5f10b-206">recursive</span></span> |<span data-ttu-id="5f10b-207">指定是否要以遞迴方式列出目錄下的 S3 物件。</span><span class="sxs-lookup"><span data-stu-id="5f10b-207">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="5f10b-208">true/false</span><span class="sxs-lookup"><span data-stu-id="5f10b-208">true/false</span></span> |<span data-ttu-id="5f10b-209">否</span><span class="sxs-lookup"><span data-stu-id="5f10b-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="5f10b-210">JSON 範例：將資料從 Amazon S3 複製到 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="5f10b-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="5f10b-211">此範例示範如何將資料從 Amazon S3 複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f10b-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="5f10b-212">不過，您可以使用 Data Factory 中的複製活動，將資料直接複製到[任何支援的接收器](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="5f10b-213">此範例提供下列 Data Factory 實體的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="5f10b-213">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="5f10b-214">您可以透過 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)，使用這些定義來建立管線，以將資料從 Amazon S3 複製到 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f10b-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="5f10b-215">[AwsAccessKey](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="5f10b-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="5f10b-216">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="5f10b-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="5f10b-217">[AmazonS3](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="5f10b-218">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="5f10b-219">具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5f10b-220">此範例會每小時將資料從 Amazon S3 複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="5f10b-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="5f10b-221">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="5f10b-221">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="5f10b-222">Amazon S3 已連結的服務</span><span class="sxs-lookup"><span data-stu-id="5f10b-222">Amazon S3 linked service</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="5f10b-223">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="5f10b-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="5f10b-224">Amazon S3 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="5f10b-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="5f10b-225">設定 **"external": true** 會通知 Data Factory 服務該資料集是 Data Factory 外部的資料集。</span><span class="sxs-lookup"><span data-stu-id="5f10b-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="5f10b-226">在不是由管線中的活動所產生的輸入資料集上，請將此屬性設定為 true。</span><span class="sxs-lookup"><span data-stu-id="5f10b-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="5f10b-227">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="5f10b-227">Azure Blob output dataset</span></span>

<span data-ttu-id="5f10b-228">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5f10b-229">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="5f10b-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="5f10b-230">此資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="5f10b-230">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="5f10b-231">具有 Amazon S3 來源和 Blob 接收器的管線中複製活動</span><span class="sxs-lookup"><span data-stu-id="5f10b-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="5f10b-232">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="5f10b-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="5f10b-233">在管線 JSON 定義中，**source** 類型設為 **FileSystemSource**，而 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="5f10b-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="5f10b-234">若要將來自來源資料集的資料行與來自接收資料集的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="5f10b-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f10b-235">Next steps</span></span>
<span data-ttu-id="5f10b-236">請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="5f10b-236">See the following articles:</span></span>

* <span data-ttu-id="5f10b-237">若要了解影響 Data Factory 中資料移動 (複製活動) 效能的關鍵因素，以及各種最佳化的方法，請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="5f10b-238">如需使用複製活動來建立管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="5f10b-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
