---
title: "在 Azure 資料 Factory 複製活動中藉由略過不相容的資料列的 aaaAdd 容錯功能 |Microsoft 文件"
description: "了解如何 tooadd 容錯藉由在複製期間略過不相容的資料列的 Azure 資料 Factory 複製活動中的功能"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="e7ea7-103">跳過不相容的資料列以在複製活動中新增容錯</span><span class="sxs-lookup"><span data-stu-id="e7ea7-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="e7ea7-104">Azure Data Factory[複製活動](data-factory-data-movement-activities.md)來源和接收的資料存放區之間複製資料時將您提供兩種方式 toohandle 不相容的資料列：</span><span class="sxs-lookup"><span data-stu-id="e7ea7-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="e7ea7-105">您可以中止和失敗 hello 複製活動不相容的資料時遇到 （預設行為）。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="e7ea7-106">您可以繼續 toocopy 所有 hello 加入容錯，並略過不相容的資料列的資料。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="e7ea7-107">此外，您可以在 Azure Blob 儲存體記錄 hello 不相容的資料列。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="e7ea7-108">您可以接著檢查 hello 記錄 toolearn hello hello 失敗原因、 修正 hello 資料 hello 的資料來源，再重試 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="e7ea7-109">支援的案例</span><span class="sxs-lookup"><span data-stu-id="e7ea7-109">Supported scenarios</span></span>
<span data-ttu-id="e7ea7-110">複製活動支援三種情節，以偵測、跳過並記錄不相容的資料：</span><span class="sxs-lookup"><span data-stu-id="e7ea7-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="e7ea7-111">**Hello 來源資料類型與 hello 接收原生型別之間的不相容**</span><span class="sxs-lookup"><span data-stu-id="e7ea7-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="e7ea7-112">例如： 複製資料，從 CSV 檔案中的 Blob 儲存體 tooa SQL 資料庫的結構描述定義，包含三種**INT**類型資料行。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="e7ea7-113">hello CSV 檔案資料列包含數值資料，例如`123,456,789`成功複製 toohello 接收存放區。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="e7ea7-114">不過，hello 資料列包含非數字的值，例如`123,456,abc`被偵測為不相容，所以會略過。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="e7ea7-115">**Hello hello 來源與 hello 接收器之間的資料行數不相符**</span><span class="sxs-lookup"><span data-stu-id="e7ea7-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="e7ea7-116">例如： 複製資料，從 CSV 檔案中的 Blob 儲存體 tooa SQL 資料庫的結構描述定義，包含六個資料行。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="e7ea7-117">hello CSV 檔案包含六個資料行的資料列成功地複製 toohello 接收存放區。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="e7ea7-118">hello CSV 檔案包含的資料列更多或少於六個資料行被偵測為不相容，並略過。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="e7ea7-119">**撰寫 tooa 關聯式資料庫時的主索引鍵違規**</span><span class="sxs-lookup"><span data-stu-id="e7ea7-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="e7ea7-120">例如： 將資料從 SQL server tooa SQL 資料庫複製。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="e7ea7-121">在 hello 接收 SQL 資料庫中，定義主索引鍵，但是沒有這類主索引鍵會定義在 hello 來源 SQL server。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="e7ea7-122">hello 來源檔案中的 hello 重複資料列不能複製的 toohello 接收。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="e7ea7-123">複製活動會將只 hello 第一個資料列的 hello 來源資料複製到 hello 接收。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="e7ea7-124">hello 後續的來源資料列包含重複的 hello 主索引鍵值被偵測為不相容且會略過。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="e7ea7-125">組態</span><span class="sxs-lookup"><span data-stu-id="e7ea7-125">Configuration</span></span>
<span data-ttu-id="e7ea7-126">hello 下列範例提供 JSON 定義 tooconfigure 略過複製活動在 hello 不相容的資料列：</span><span class="sxs-lookup"><span data-stu-id="e7ea7-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="e7ea7-127">屬性</span><span class="sxs-lookup"><span data-stu-id="e7ea7-127">Property</span></span> | <span data-ttu-id="e7ea7-128">說明</span><span class="sxs-lookup"><span data-stu-id="e7ea7-128">Description</span></span> | <span data-ttu-id="e7ea7-129">允許的值</span><span class="sxs-lookup"><span data-stu-id="e7ea7-129">Allowed values</span></span> | <span data-ttu-id="e7ea7-130">必要</span><span class="sxs-lookup"><span data-stu-id="e7ea7-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e7ea7-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="e7ea7-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="e7ea7-132">啟用或停用在複製期間略過不相容的資料列。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="e7ea7-133">True</span><span class="sxs-lookup"><span data-stu-id="e7ea7-133">True</span></span><br/><span data-ttu-id="e7ea7-134">FALSE (預設值)</span><span class="sxs-lookup"><span data-stu-id="e7ea7-134">False (default)</span></span> | <span data-ttu-id="e7ea7-135">否</span><span class="sxs-lookup"><span data-stu-id="e7ea7-135">No</span></span> |
| <span data-ttu-id="e7ea7-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="e7ea7-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="e7ea7-137">一組屬性可指定當您想 toolog hello 不相容的資料列。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="e7ea7-138">否</span><span class="sxs-lookup"><span data-stu-id="e7ea7-138">No</span></span> |
| <span data-ttu-id="e7ea7-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="e7ea7-139">**linkedServiceName**</span></span> | <span data-ttu-id="e7ea7-140">hello 連結服務的 Azure 儲存體 toostore hello 記錄，其中包含 hello 略過資料列。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="e7ea7-141">hello 名稱[AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service)或[AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service)連結服務，也就是您想 toouse toostore hello 記錄檔的 toohello 儲存執行個體。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="e7ea7-142">否</span><span class="sxs-lookup"><span data-stu-id="e7ea7-142">No</span></span> |
| <span data-ttu-id="e7ea7-143">**路徑**</span><span class="sxs-lookup"><span data-stu-id="e7ea7-143">**path**</span></span> | <span data-ttu-id="e7ea7-144">hello 記錄檔，其中包含 hello hello 路徑略過資料列。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="e7ea7-145">指定您想 toouse toolog hello 不相容的資料 hello Blob 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="e7ea7-146">如果您未提供路徑，hello 服務會為您建立的容器。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="e7ea7-147">否</span><span class="sxs-lookup"><span data-stu-id="e7ea7-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="e7ea7-148">監視</span><span class="sxs-lookup"><span data-stu-id="e7ea7-148">Monitoring</span></span>
<span data-ttu-id="e7ea7-149">Hello 複製活動執行完成之後，您可以看到 hello hello [監視] 區段中略過資料列數目：</span><span class="sxs-lookup"><span data-stu-id="e7ea7-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![監視跳過的不相容資料列](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="e7ea7-151">如果您設定 toolog hello 不相容的資料列時，您可以找到 hello 記錄檔，在這個路徑： `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` hello 記錄檔，您可以查看 hello 略過的資料列並 hello hello 不相容問題的根本原因。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="e7ea7-152">Hello 原始資料和 hello 對應的錯誤會記錄在 hello 檔。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="e7ea7-153">Hello 記錄檔案內容的範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="e7ea7-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="e7ea7-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7ea7-154">Next steps</span></span>
<span data-ttu-id="e7ea7-155">toolearn 進一步了解 Azure 資料 Factory 複製活動時，請參閱[使用複製活動移動資料](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="e7ea7-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
