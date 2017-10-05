---
title: "在 Azure 入口網站中啟用儲存體計量功能 | Microsoft Docs"
description: "如何啟用 Blob、佇列、表格和檔案服務的儲存體度量"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4d6065597a41372ea6d320ab318b0c71d6a48b2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="9ca67-103">啟用儲存體度量和檢視度量資料</span><span class="sxs-lookup"><span data-stu-id="9ca67-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="9ca67-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9ca67-104">Overview</span></span>
<span data-ttu-id="9ca67-105">當您建立新的儲存體帳戶時，預設會啟用「儲存體計量」。</span><span class="sxs-lookup"><span data-stu-id="9ca67-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="9ca67-106">若要設定監視，可以使用 [Azure 傳統入口網站](https://manage.windowsazure.com)、Windows PowerShell，或透過儲存體 API 以程式設計方式進行。</span><span class="sxs-lookup"><span data-stu-id="9ca67-106">You can configure monitoring using either the [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="9ca67-107">當您啟用儲存體度量時，必須選擇資料的保留期限：這段期間會決定儲存體服務用來保存度量的時間長度，以及該空間儲存它們所需的費用。</span><span class="sxs-lookup"><span data-stu-id="9ca67-107">When you enable Storage Metrics, you must choose a retention period for the data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="9ca67-108">一般而言，您應該針對每分鐘度量使用比每小時度量還短的保留期限，因為每分鐘度量明顯需要額外的空間。</span><span class="sxs-lookup"><span data-stu-id="9ca67-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="9ca67-109">您應該選擇保留期限，讓您擁有足夠的時間來分析資料，並下載任何您想要保留以供離線分析或報告使用的度量。</span><span class="sxs-lookup"><span data-stu-id="9ca67-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="9ca67-110">請記住，您還是必須支付從儲存體帳戶下載度量資料的費用。</span><span class="sxs-lookup"><span data-stu-id="9ca67-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-storage-metrics-using-the-azure-classic-portal"></a><span data-ttu-id="9ca67-111">如何使用 Azure 傳統入口網站啟用儲存體度量</span><span class="sxs-lookup"><span data-stu-id="9ca67-111">How to enable Storage metrics using the Azure Classic Portal</span></span>
<span data-ttu-id="9ca67-112">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，您可以使用儲存體帳戶的 [設定] 頁面來控制儲存體度量。</span><span class="sxs-lookup"><span data-stu-id="9ca67-112">In the [Azure Classic Portal](https://manage.windowsazure.com), you use the Configure page for a storage account to control Storage Metrics.</span></span> <span data-ttu-id="9ca67-113">如需監視，您可以針對每個 Blob、資料表和佇列設定層級和保留期限 (以天為單位)。</span><span class="sxs-lookup"><span data-stu-id="9ca67-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="9ca67-114">在各個案例中，層級會是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="9ca67-114">In each case, the level is one of the following:</span></span>

* <span data-ttu-id="9ca67-115">關閉 - 不會收集任何度量。</span><span class="sxs-lookup"><span data-stu-id="9ca67-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="9ca67-116">最小 - 儲存體度量會收集一組針對 Blob、資料表與佇列服務彙總的基本度量 (例如，輸入流量/輸出流量、可用性、延遲和成功百分比)。</span><span class="sxs-lookup"><span data-stu-id="9ca67-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for the Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="9ca67-117">詳細資訊 - 除了服務層級度量之外，儲存體度量會收集一組完整的度量，其中包含每個儲存體 API 作業的相同度量。</span><span class="sxs-lookup"><span data-stu-id="9ca67-117">Verbose — Storage Metrics collects a full set of metrics that includes the same metrics for each storage API operation, in addition to the service-level metrics.</span></span> <span data-ttu-id="9ca67-118">詳細資訊度量可供進一步分析在應用程式運作期間發生的問題。</span><span class="sxs-lookup"><span data-stu-id="9ca67-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="9ca67-119">請注意，Azure 傳統入口網站目前無法讓您在儲存體帳戶中設定每分鐘度量；您必須使用 PowerShell 或以程式設計方式來啟用每分鐘度量。</span><span class="sxs-lookup"><span data-stu-id="9ca67-119">Note that the Azure Classic Portal does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-storage-metrics-using-powershell"></a><span data-ttu-id="9ca67-120">如何使用 PowerShell 啟用儲存體度量</span><span class="sxs-lookup"><span data-stu-id="9ca67-120">How to enable Storage metrics using PowerShell</span></span>
<span data-ttu-id="9ca67-121">您可以在本機電腦上使用 PowerShell 來設定儲存體帳戶中的儲存體度量，做法是使用 Azure PowerShell Cmdlet Get-AzureStorageServiceMetricsProperty 來擷取目前的設定，並使用 Cmdlet Set-AzureStorageServiceMetricsProperty 來變更目前的設定。</span><span class="sxs-lookup"><span data-stu-id="9ca67-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="9ca67-122">控制儲存體度量的 Cmdlet 會使用下列參數：</span><span class="sxs-lookup"><span data-stu-id="9ca67-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="9ca67-123">MetricsType 的可能值為 Hour 和 Minute。</span><span class="sxs-lookup"><span data-stu-id="9ca67-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="9ca67-124">ServiceType 的可能值為 Blob、Queue 及 Table。</span><span class="sxs-lookup"><span data-stu-id="9ca67-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="9ca67-125">MetricsLevel 的可能值為 None (相當於 Azure 傳統入口網站中的「關閉」)、Service (相當於 Azure 傳統入口網站中的「最小」)，以及 ServiceAndApi (相當於 Azure 傳統入口網站中的「詳細資訊」)。</span><span class="sxs-lookup"><span data-stu-id="9ca67-125">MetricsLevel possible values are None (equivalent to Off in the Azure Classic Portal), Service (equivalent to Minimal in the Azure Classic Portal), and ServiceAndApi (equivalent to Verbose in the Azure Classic Portal).</span></span>

<span data-ttu-id="9ca67-126">例如，下列命令會在您的預設儲存體帳戶中，為 Blob 服務開啟每分鐘度量，並將保留期限設為五天：</span><span class="sxs-lookup"><span data-stu-id="9ca67-126">For example, the following command switches on minute metrics for the blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="9ca67-127">下列命令會擷取您預設儲存體帳戶中 Blob 服務的目前每小時度量層級和保留天數：</span><span class="sxs-lookup"><span data-stu-id="9ca67-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="9ca67-128">如需如何設定 Azure PowerShell Cmdlet 以使用您的 Azure 訂用帳戶，以及如何選取要使用的預設儲存體帳戶的相關資訊，請參閱： [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="9ca67-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="9ca67-129">如何以程式設計方式啟用儲存體度量</span><span class="sxs-lookup"><span data-stu-id="9ca67-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="9ca67-130">下列 C# 程式碼片段示範如何使用 .NET 的儲存體用戶端程式庫，為 Blob 服務啟用計量和記錄功能：</span><span class="sxs-lookup"><span data-stu-id="9ca67-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="9ca67-131">檢視儲存體度量</span><span class="sxs-lookup"><span data-stu-id="9ca67-131">Viewing Storage metrics</span></span>
<span data-ttu-id="9ca67-132">設定要監視儲存體帳戶的儲存體度量後，它會在您儲存體帳戶的一組已知資料表中記錄度量。</span><span class="sxs-lookup"><span data-stu-id="9ca67-132">When you have configured Storage Metrics to monitor your storage account, it records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="9ca67-133">您可以在 Azure 傳統入口網站中使用您儲存體帳戶的 [監視] 頁面，當它們出現在圖表上時，檢視每小時度量。</span><span class="sxs-lookup"><span data-stu-id="9ca67-133">You can use the Monitor page for your storage account in the Azure Classic Portal to view the hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="9ca67-134">在 Azure 傳統入口網站的這個頁面上，您可以：</span><span class="sxs-lookup"><span data-stu-id="9ca67-134">On this page in the Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="9ca67-135">選取要在圖表上繪製哪些度量 (可用的度量選項將根據您在 [設定] 頁面上，為服務選擇的是詳細資訊或最小監視而定)。</span><span class="sxs-lookup"><span data-stu-id="9ca67-135">Select which metrics to plot on the chart (the choice of available metrics will depend on whether you chose verbose or minimal monitoring for the service on the Configure page).</span></span>
* <span data-ttu-id="9ca67-136">為圖表上顯示的度量選取時間範圍。</span><span class="sxs-lookup"><span data-stu-id="9ca67-136">Select the time range for the metrics displayed on the chart.</span></span>
* <span data-ttu-id="9ca67-137">選擇使用絕對或相對比例來繪製度量。</span><span class="sxs-lookup"><span data-stu-id="9ca67-137">Choose to use an absolute or relative scale to plot the metrics.</span></span>
* <span data-ttu-id="9ca67-138">設定電子郵件警示，在特定的度量達到特定值時通知您。</span><span class="sxs-lookup"><span data-stu-id="9ca67-138">Configure email alerts to notify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="9ca67-139">如果要下載長期儲存體的度量，或在本機加以分析，您必須使用工具或撰寫程式碼來讀取資料表。</span><span class="sxs-lookup"><span data-stu-id="9ca67-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to use a tool or write some code to read the tables.</span></span> <span data-ttu-id="9ca67-140">您必須下載每分鐘度量以進行分析。</span><span class="sxs-lookup"><span data-stu-id="9ca67-140">You must download the minute metrics for analysis.</span></span> <span data-ttu-id="9ca67-141">如果您在儲存體帳戶中列出所有資料表，則資料表就不會出現，但您可以直接依名稱存取它們。</span><span class="sxs-lookup"><span data-stu-id="9ca67-141">The tables do not appear if you list all the tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="9ca67-142">有許多協力廠商儲存體瀏覽工具可以感知這些資料表，讓您能夠直接檢視它們 (如需可用工具清單，請參閱部落格文章 [Microsoft Azure 儲存體總管](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) )。</span><span class="sxs-lookup"><span data-stu-id="9ca67-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly (see the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="9ca67-143">每小時度量</span><span class="sxs-lookup"><span data-stu-id="9ca67-143">Hourly metrics</span></span>
* <span data-ttu-id="9ca67-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="9ca67-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="9ca67-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="9ca67-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="9ca67-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="9ca67-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="9ca67-147">每分鐘度量</span><span class="sxs-lookup"><span data-stu-id="9ca67-147">Minute metrics</span></span>
* <span data-ttu-id="9ca67-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="9ca67-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="9ca67-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="9ca67-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="9ca67-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="9ca67-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="9ca67-151">容量</span><span class="sxs-lookup"><span data-stu-id="9ca67-151">Capacity</span></span>
* <span data-ttu-id="9ca67-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="9ca67-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="9ca67-153">您可以在 [儲存體分析度量資料表結構描述](https://msdn.microsoft.com/library/azure/hh343264.aspx)上找到這些資料表之結構描述的完整詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9ca67-153">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="9ca67-154">下列資料列範例只會顯示可用的資料行子集，但可說明儲存體度量儲存這些度量資訊之方式的一些重要功能：</span><span class="sxs-lookup"><span data-stu-id="9ca67-154">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="9ca67-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="9ca67-155">PartitionKey</span></span> | <span data-ttu-id="9ca67-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="9ca67-156">RowKey</span></span> | <span data-ttu-id="9ca67-157">Timestamp</span><span class="sxs-lookup"><span data-stu-id="9ca67-157">Timestamp</span></span> | <span data-ttu-id="9ca67-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="9ca67-158">TotalRequests</span></span> | <span data-ttu-id="9ca67-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="9ca67-159">TotalBillableRequests</span></span> | <span data-ttu-id="9ca67-160">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="9ca67-160">TotalIngress</span></span> | <span data-ttu-id="9ca67-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="9ca67-161">TotalEgress</span></span> | <span data-ttu-id="9ca67-162">Availability</span><span class="sxs-lookup"><span data-stu-id="9ca67-162">Availability</span></span> | <span data-ttu-id="9ca67-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="9ca67-163">AverageE2ELatency</span></span> | <span data-ttu-id="9ca67-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="9ca67-164">AverageServerLatency</span></span> | <span data-ttu-id="9ca67-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="9ca67-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="9ca67-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9ca67-166">20140522T1100</span></span> |<span data-ttu-id="9ca67-167">user;All</span><span class="sxs-lookup"><span data-stu-id="9ca67-167">user;All</span></span> |<span data-ttu-id="9ca67-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="9ca67-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="9ca67-169">7</span><span class="sxs-lookup"><span data-stu-id="9ca67-169">7</span></span> |<span data-ttu-id="9ca67-170">7</span><span class="sxs-lookup"><span data-stu-id="9ca67-170">7</span></span> |<span data-ttu-id="9ca67-171">4003</span><span class="sxs-lookup"><span data-stu-id="9ca67-171">4003</span></span> |<span data-ttu-id="9ca67-172">46801</span><span class="sxs-lookup"><span data-stu-id="9ca67-172">46801</span></span> |<span data-ttu-id="9ca67-173">100</span><span class="sxs-lookup"><span data-stu-id="9ca67-173">100</span></span> |<span data-ttu-id="9ca67-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="9ca67-174">104.4286</span></span> |<span data-ttu-id="9ca67-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="9ca67-175">6.857143</span></span> |<span data-ttu-id="9ca67-176">100</span><span class="sxs-lookup"><span data-stu-id="9ca67-176">100</span></span> |
| <span data-ttu-id="9ca67-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9ca67-177">20140522T1100</span></span> |<span data-ttu-id="9ca67-178">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="9ca67-178">user;QueryEntities</span></span> |<span data-ttu-id="9ca67-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="9ca67-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="9ca67-180">5</span><span class="sxs-lookup"><span data-stu-id="9ca67-180">5</span></span> |<span data-ttu-id="9ca67-181">5</span><span class="sxs-lookup"><span data-stu-id="9ca67-181">5</span></span> |<span data-ttu-id="9ca67-182">2694</span><span class="sxs-lookup"><span data-stu-id="9ca67-182">2694</span></span> |<span data-ttu-id="9ca67-183">45951</span><span class="sxs-lookup"><span data-stu-id="9ca67-183">45951</span></span> |<span data-ttu-id="9ca67-184">100</span><span class="sxs-lookup"><span data-stu-id="9ca67-184">100</span></span> |<span data-ttu-id="9ca67-185">143.8</span><span class="sxs-lookup"><span data-stu-id="9ca67-185">143.8</span></span> |<span data-ttu-id="9ca67-186">7.8</span><span class="sxs-lookup"><span data-stu-id="9ca67-186">7.8</span></span> |<span data-ttu-id="9ca67-187">100</span><span class="sxs-lookup"><span data-stu-id="9ca67-187">100</span></span> |
| <span data-ttu-id="9ca67-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9ca67-188">20140522T1100</span></span> |<span data-ttu-id="9ca67-189">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="9ca67-189">user;QueryEntity</span></span> |<span data-ttu-id="9ca67-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="9ca67-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="9ca67-191">1</span><span class="sxs-lookup"><span data-stu-id="9ca67-191">1</span></span> |<span data-ttu-id="9ca67-192">1</span><span class="sxs-lookup"><span data-stu-id="9ca67-192">1</span></span> |<span data-ttu-id="9ca67-193">538</span><span class="sxs-lookup"><span data-stu-id="9ca67-193">538</span></span> |<span data-ttu-id="9ca67-194">633</span><span class="sxs-lookup"><span data-stu-id="9ca67-194">633</span></span> |<span data-ttu-id="9ca67-195">100</span><span class="sxs-lookup"><span data-stu-id="9ca67-195">100</span></span> |<span data-ttu-id="9ca67-196">3</span><span class="sxs-lookup"><span data-stu-id="9ca67-196">3</span></span> |<span data-ttu-id="9ca67-197">3</span><span class="sxs-lookup"><span data-stu-id="9ca67-197">3</span></span> |<span data-ttu-id="9ca67-198">100</span><span class="sxs-lookup"><span data-stu-id="9ca67-198">100</span></span> |
| <span data-ttu-id="9ca67-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9ca67-199">20140522T1100</span></span> |<span data-ttu-id="9ca67-200">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="9ca67-200">user;UpdateEntity</span></span> |<span data-ttu-id="9ca67-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="9ca67-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="9ca67-202">1</span><span class="sxs-lookup"><span data-stu-id="9ca67-202">1</span></span> |<span data-ttu-id="9ca67-203">1</span><span class="sxs-lookup"><span data-stu-id="9ca67-203">1</span></span> |<span data-ttu-id="9ca67-204">771</span><span class="sxs-lookup"><span data-stu-id="9ca67-204">771</span></span> |<span data-ttu-id="9ca67-205">217</span><span class="sxs-lookup"><span data-stu-id="9ca67-205">217</span></span> |<span data-ttu-id="9ca67-206">100</span><span class="sxs-lookup"><span data-stu-id="9ca67-206">100</span></span> |<span data-ttu-id="9ca67-207">9</span><span class="sxs-lookup"><span data-stu-id="9ca67-207">9</span></span> |<span data-ttu-id="9ca67-208">6</span><span class="sxs-lookup"><span data-stu-id="9ca67-208">6</span></span> |<span data-ttu-id="9ca67-209">100</span><span class="sxs-lookup"><span data-stu-id="9ca67-209">100</span></span> |

<span data-ttu-id="9ca67-210">在這個每分鐘度量資料範例中，資料分割索引鍵會在每分鐘解析中使用時間。</span><span class="sxs-lookup"><span data-stu-id="9ca67-210">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="9ca67-211">資料列索引鍵會識別資料列中儲存的資訊類型，而這是由兩部分的資訊 (存取類型及要求類型) 所組成：</span><span class="sxs-lookup"><span data-stu-id="9ca67-211">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="9ca67-212">存取類型是使用者或系統，其中使用者是指對儲存體服務所提出的所有使用者要求，而系統是指對儲存體分析所提出的要求。</span><span class="sxs-lookup"><span data-stu-id="9ca67-212">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="9ca67-213">要求類型就是全部 (在此情況下它是摘要行)，或者它會識別特定的 API，例如 QueryEntity 或 UpdateEntity。</span><span class="sxs-lookup"><span data-stu-id="9ca67-213">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="9ca67-214">上述範例資料會為單一分鐘 (從上午 11:00 開始) 顯示所有記錄，因此 QueryEntities 要求的數目加上 QueryEntity 要求的數目再加上 UpdateEntity 要求的數目最多七個，也就是 user:All 資料列上顯示的總數。</span><span class="sxs-lookup"><span data-stu-id="9ca67-214">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="9ca67-215">同樣地，您可以藉由計算 ((143.8 * 5) + 3 + 9)/7，在 user:All 資料列上衍生平均的端對端延遲 104.4286。</span><span class="sxs-lookup"><span data-stu-id="9ca67-215">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="9ca67-216">您應該考慮在 Azure 傳統入口網站的 [監視] 頁面上設定警示，讓儲存體度量可自動通知您儲存體服務行為的任何重要變更。如果您使用儲存體總管工具來下載這個度量資料 (以分隔的格式)，就可以使用 Microsoft Excel 來分析資料。</span><span class="sxs-lookup"><span data-stu-id="9ca67-216">You should consider setting up alerts in the Azure Classic Portal on the Monitor page so that Storage Metrics can automatically notify you of any important changes in the behavior of your storage services.If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="9ca67-217">如需可用儲存體總管工具的清單，請參閱部落格文章 [Microsoft Azure 儲存體總管](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9ca67-217">See the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="9ca67-218">以程式設計方式存取度量資料</span><span class="sxs-lookup"><span data-stu-id="9ca67-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="9ca67-219">下列清單顯示 C# 程式碼範例，其會針對某個分鐘範圍存取每分鐘度量，並將結果顯示在主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="9ca67-219">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="9ca67-220">它會使用 Azure 儲存體程式庫第 4 版，其中包含可簡化存取儲存體中之度量資料表的 CloudAnalyticsClient 類別。</span><span class="sxs-lookup"><span data-stu-id="9ca67-220">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
    string.Format("Time: {0}, ", entity.Time) +
    string.Format("AccessType: {0}, ", entity.AccessType) +
    string.Format("TransactionType: {0}, ", entity.TransactionType) +
    string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="9ca67-221">當您啟用儲存體度量時，會產生哪些費用？</span><span class="sxs-lookup"><span data-stu-id="9ca67-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="9ca67-222">寫入要求以建立度量的資料表實體，會以適用於所有 Azure 儲存體作業的標準費率來收費。</span><span class="sxs-lookup"><span data-stu-id="9ca67-222">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="9ca67-223">用戶端對於度量資料的讀取和刪除要求也會以標準費率來計費。</span><span class="sxs-lookup"><span data-stu-id="9ca67-223">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="9ca67-224">如果您已設定資料保留原則，就不需要在 Azure 儲存體刪除舊的度量資料時付費。</span><span class="sxs-lookup"><span data-stu-id="9ca67-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="9ca67-225">不過，如果您刪除分析資料，則您的帳戶必須支付刪除作業的費用。</span><span class="sxs-lookup"><span data-stu-id="9ca67-225">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="9ca67-226">度量資料表所使用的容量也會列入計費：您可以使用下列項目來估計儲存計量資料所使用的容量大小：</span><span class="sxs-lookup"><span data-stu-id="9ca67-226">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="9ca67-227">如果服務每小時會使用每個服務中的每一種 API，若您已啟用服務和 API 層級摘要，則每小時大約有 148 KB 的資料將儲存於度量交易資料表中。</span><span class="sxs-lookup"><span data-stu-id="9ca67-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="9ca67-228">如果服務每小時會使用每個服務中的每一種 API，若您只啟用服務層級摘要，則每小時大約有 12 KB 的資料將儲存於度量交易資料表中。</span><span class="sxs-lookup"><span data-stu-id="9ca67-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="9ca67-229">適用於 Blob 的容量資料表每天都會新增兩個資料列 (前提是使用者已選擇記錄檔)：也就是說，這個資料表的大小每天最多大約會增加 300 個位元組。</span><span class="sxs-lookup"><span data-stu-id="9ca67-229">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ca67-230">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="9ca67-230">Next steps:</span></span>
[<span data-ttu-id="9ca67-231">啟用儲存體分析記錄和存取記錄檔資料</span><span class="sxs-lookup"><span data-stu-id="9ca67-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)
