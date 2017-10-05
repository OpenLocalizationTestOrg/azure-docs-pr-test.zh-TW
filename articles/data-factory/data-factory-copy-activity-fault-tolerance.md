---
title: "跳過不相容的資料列以在 Azure Data Factory 複製活動中新增容錯 | Microsoft Docs"
description: "了解如何在複製期間跳過不相容的資料列，以在 Azure Data Factory 複製活動中新增容錯"
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
ms.openlocfilehash: e2a108752259d5da3b401666c6bdbaad13b7ea90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="70d51-103">跳過不相容的資料列以在複製活動中新增容錯</span><span class="sxs-lookup"><span data-stu-id="70d51-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="70d51-104">Azure Data Factory [複製活動](data-factory-data-movement-activities.md)可在來源和接收資料存放區之間複製資料時，提供您兩個方式來處理不相容的資料列：</span><span class="sxs-lookup"><span data-stu-id="70d51-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="70d51-105">遇到不相容的資料時，您可以中止並捨棄複製活動 (預設行為)。</span><span class="sxs-lookup"><span data-stu-id="70d51-105">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="70d51-106">您可以繼續複製所有的資料，方法是新增容錯並跳過不相容的資料列。</span><span class="sxs-lookup"><span data-stu-id="70d51-106">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="70d51-107">此外，您可以在 Azure Blob 儲存體中記錄不相容的資料列。</span><span class="sxs-lookup"><span data-stu-id="70d51-107">In addition, you can log the incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="70d51-108">接著，您可以檢查記錄來了解失敗的原因、修正資料來源上的資料，並重試複製活動。</span><span class="sxs-lookup"><span data-stu-id="70d51-108">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="70d51-109">支援的案例</span><span class="sxs-lookup"><span data-stu-id="70d51-109">Supported scenarios</span></span>
<span data-ttu-id="70d51-110">複製活動支援三種情節，以偵測、跳過並記錄不相容的資料：</span><span class="sxs-lookup"><span data-stu-id="70d51-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="70d51-111">**來源資料類型和接收原生類型之間的不相容**</span><span class="sxs-lookup"><span data-stu-id="70d51-111">**Incompatibility between the source data type and the sink native type**</span></span>

    <span data-ttu-id="70d51-112">例如：使用包含三種 **INT** 類型資料行的結構描述定義，從 Blob 儲存體中的 CSV 檔案將資料複製到 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="70d51-112">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="70d51-113">包含數值資料的 CSV 檔案資料列 (例如 `123,456,789`) 會成功複製到接收存放區。</span><span class="sxs-lookup"><span data-stu-id="70d51-113">The CSV file rows that contain numeric data, such as `123,456,789` are copied successfully to the sink store.</span></span> <span data-ttu-id="70d51-114">不過，包含非數值的資料列 (例如 `123,456,abc`) 會偵測為不相容並加以跳過。</span><span class="sxs-lookup"><span data-stu-id="70d51-114">However, the rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="70d51-115">**來源與接收之間的資料行數目不相符**</span><span class="sxs-lookup"><span data-stu-id="70d51-115">**Mismatch in the number of columns between the source and the sink**</span></span>

    <span data-ttu-id="70d51-116">例如：使用包含六個資料行的結構描述定義，從 Blob 儲存體中的 CSV 檔案將資料複製到 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="70d51-116">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="70d51-117">包含六個資料行的 CSV 檔案資料列會成功複製到接收存放區。</span><span class="sxs-lookup"><span data-stu-id="70d51-117">The CSV file rows that contain six columns are copied successfully to the sink store.</span></span> <span data-ttu-id="70d51-118">包含多於或少於六個資料行的 CSV 檔案資料列會偵測為不相容，並加以跳過。</span><span class="sxs-lookup"><span data-stu-id="70d51-118">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="70d51-119">**寫入關聯式資料庫時發生主索引鍵違規**</span><span class="sxs-lookup"><span data-stu-id="70d51-119">**Primary key violation when writing to a relational database**</span></span>

    <span data-ttu-id="70d51-120">例如：從 SQL Server 將資料複製到 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="70d51-120">For example: Copy data from a SQL server to a SQL database.</span></span> <span data-ttu-id="70d51-121">會在接收 SQL 資料庫中定義主索引鍵，但是在來源 SQL Server 中不會定義這類主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="70d51-121">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span></span> <span data-ttu-id="70d51-122">無法將來源中的重複資料列複製到接收。</span><span class="sxs-lookup"><span data-stu-id="70d51-122">The duplicated rows that exist in the source cannot be copied to the sink.</span></span> <span data-ttu-id="70d51-123">複製活動只會將來源資料中的第一個資料列複製到接收。</span><span class="sxs-lookup"><span data-stu-id="70d51-123">Copy Activity copies only the first row of the source data into the sink.</span></span> <span data-ttu-id="70d51-124">包含重複主索引鍵值的後續來源資料列會偵測為不相容，並加以跳過。</span><span class="sxs-lookup"><span data-stu-id="70d51-124">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="70d51-125">組態</span><span class="sxs-lookup"><span data-stu-id="70d51-125">Configuration</span></span>
<span data-ttu-id="70d51-126">下列範例提供的 JSON 定義，可設定在複製活動中跳過不相容資料列：</span><span class="sxs-lookup"><span data-stu-id="70d51-126">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span></span>

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

| <span data-ttu-id="70d51-127">屬性</span><span class="sxs-lookup"><span data-stu-id="70d51-127">Property</span></span> | <span data-ttu-id="70d51-128">說明</span><span class="sxs-lookup"><span data-stu-id="70d51-128">Description</span></span> | <span data-ttu-id="70d51-129">允許的值</span><span class="sxs-lookup"><span data-stu-id="70d51-129">Allowed values</span></span> | <span data-ttu-id="70d51-130">必要</span><span class="sxs-lookup"><span data-stu-id="70d51-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="70d51-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="70d51-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="70d51-132">啟用或停用在複製期間略過不相容的資料列。</span><span class="sxs-lookup"><span data-stu-id="70d51-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="70d51-133">True</span><span class="sxs-lookup"><span data-stu-id="70d51-133">True</span></span><br/><span data-ttu-id="70d51-134">FALSE (預設值)</span><span class="sxs-lookup"><span data-stu-id="70d51-134">False (default)</span></span> | <span data-ttu-id="70d51-135">否</span><span class="sxs-lookup"><span data-stu-id="70d51-135">No</span></span> |
| <span data-ttu-id="70d51-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="70d51-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="70d51-137">當您想要記錄不相容的資料列時，可指定的一組屬性。</span><span class="sxs-lookup"><span data-stu-id="70d51-137">A group of properties that can be specified when you want to log the incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="70d51-138">否</span><span class="sxs-lookup"><span data-stu-id="70d51-138">No</span></span> |
| <span data-ttu-id="70d51-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="70d51-139">**linkedServiceName**</span></span> | <span data-ttu-id="70d51-140">Azure 儲存體的連結服務，儲存包含跳過資料列的記錄。</span><span class="sxs-lookup"><span data-stu-id="70d51-140">The linked service of Azure Storage to store the log that contains the skipped rows.</span></span> | <span data-ttu-id="70d51-141">[AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) 或 [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) 連結服務的名稱，以代表您需要用來儲存記錄檔的儲存體執行個體。</span><span class="sxs-lookup"><span data-stu-id="70d51-141">The name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers to the storage instance that you want to use to store the log file.</span></span> | <span data-ttu-id="70d51-142">否</span><span class="sxs-lookup"><span data-stu-id="70d51-142">No</span></span> |
| <span data-ttu-id="70d51-143">**路徑**</span><span class="sxs-lookup"><span data-stu-id="70d51-143">**path**</span></span> | <span data-ttu-id="70d51-144">包含跳過之資料列的記錄檔路徑。</span><span class="sxs-lookup"><span data-stu-id="70d51-144">The path of the log file that contains the skipped rows.</span></span> | <span data-ttu-id="70d51-145">指定需要用來記錄不相容資料的 Blob 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="70d51-145">Specify the Blob storage path that you want to use to log the incompatible data.</span></span> <span data-ttu-id="70d51-146">如不提供路徑，服務會為您建立容器。</span><span class="sxs-lookup"><span data-stu-id="70d51-146">If you do not provide a path, the service creates a container for you.</span></span> | <span data-ttu-id="70d51-147">否</span><span class="sxs-lookup"><span data-stu-id="70d51-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="70d51-148">監視</span><span class="sxs-lookup"><span data-stu-id="70d51-148">Monitoring</span></span>
<span data-ttu-id="70d51-149">複製活動執行完成之後，您會在 [監視] 區段中看到跳過的資料列數目：</span><span class="sxs-lookup"><span data-stu-id="70d51-149">After the copy activity run completes, you can see the number of skipped rows in the monitoring section:</span></span>

![監視跳過的不相容資料列](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="70d51-151">如果設定記錄不相容的資料列，您可在此路徑找到記錄檔：`https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` 在記錄檔中，您會看到跳過的資料列和不相容的根本原因。</span><span class="sxs-lookup"><span data-stu-id="70d51-151">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In the log file, you can see the rows that were skipped and the root cause of the incompatibility.</span></span>

<span data-ttu-id="70d51-152">原始資料和對應的錯誤都會記錄在檔案中。</span><span class="sxs-lookup"><span data-stu-id="70d51-152">Both the original data and the corresponding error are logged in the file.</span></span> <span data-ttu-id="70d51-153">記錄檔內容範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="70d51-153">An example of the log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="70d51-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70d51-154">Next steps</span></span>
<span data-ttu-id="70d51-155">若要深入了解 Azure Data Factory 複製活動，請參閱[使用複製活動來移動資料](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="70d51-155">To learn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>