---
title: "aaaEnabling hello Azure 入口網站中的儲存體度量 |Microsoft 文件"
description: "如何儲存體度量 tooenable hello Blob、 佇列、 表格和檔案服務"
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
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="4c29b-103">啟用儲存體度量和檢視度量資料</span><span class="sxs-lookup"><span data-stu-id="4c29b-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="4c29b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4c29b-104">Overview</span></span>
<span data-ttu-id="4c29b-105">當您建立新的儲存體帳戶時，預設會啟用「儲存體計量」。</span><span class="sxs-lookup"><span data-stu-id="4c29b-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="4c29b-106">您可以設定監視使用任一 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，Windows PowerShell 或透過儲存體 API 以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="4c29b-106">You can configure monitoring using either hello [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="4c29b-107">當您啟用儲存體度量時，您必須選擇 hello 資料的保留期限： 此期間決定多久 hello 儲存體服務可以維持 hello 度量，並且您 hello 空間需要的 toostore 費用它們。</span><span class="sxs-lookup"><span data-stu-id="4c29b-107">When you enable Storage Metrics, you must choose a retention period for hello data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="4c29b-108">一般而言，您應該於每小時度量的每分鐘度量使用較短的保留期限因為 hello 重大的額外空間所需的每分鐘度量。</span><span class="sxs-lookup"><span data-stu-id="4c29b-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="4c29b-109">您應該選擇的保留期限，您有足夠時間 tooanalyze hello 資料，並下載您想 tookeep 供離線分析或報告之用的任何度量。</span><span class="sxs-lookup"><span data-stu-id="4c29b-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="4c29b-110">請記住，您還是必須支付從儲存體帳戶下載度量資料的費用。</span><span class="sxs-lookup"><span data-stu-id="4c29b-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a><span data-ttu-id="4c29b-111">如何使用 tooenable 儲存體度量 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="4c29b-111">How tooenable Storage metrics using hello Azure Classic Portal</span></span>
<span data-ttu-id="4c29b-112">在 [hello [Azure 傳統入口網站](https://manage.windowsazure.com)，您用於儲存體度量的儲存體帳戶 toocontrol hello 設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4c29b-112">In hello [Azure Classic Portal](https://manage.windowsazure.com), you use hello Configure page for a storage account toocontrol Storage Metrics.</span></span> <span data-ttu-id="4c29b-113">如需監視，您可以針對每個 Blob、資料表和佇列設定層級和保留期限 (以天為單位)。</span><span class="sxs-lookup"><span data-stu-id="4c29b-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="4c29b-114">在每個案例中，hello 層級是 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="4c29b-114">In each case, hello level is one of hello following:</span></span>

* <span data-ttu-id="4c29b-115">關閉 - 不會收集任何度量。</span><span class="sxs-lookup"><span data-stu-id="4c29b-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="4c29b-116">最少 — 儲存體度量 」 會收集一組基本度量，例如輸入/輸出、 可用性、 延遲和成功百分比 hello Blob、 資料表和佇列服務彙總。</span><span class="sxs-lookup"><span data-stu-id="4c29b-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for hello Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="4c29b-117">詳細資訊，完整設定的度量，包括儲存體度量收集 hello 每個儲存體程式開發介面作業的相同度量資訊，除了 toohello 服務等級度量。</span><span class="sxs-lookup"><span data-stu-id="4c29b-117">Verbose — Storage Metrics collects a full set of metrics that includes hello same metrics for each storage API operation, in addition toohello service-level metrics.</span></span> <span data-ttu-id="4c29b-118">詳細資訊度量可供進一步分析在應用程式運作期間發生的問題。</span><span class="sxs-lookup"><span data-stu-id="4c29b-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="4c29b-119">請注意，hello Azure 傳統入口網站目前無法讓您 tooconfigure 分鐘度量，在儲存體帳戶。您必須啟用分鐘度量使用 PowerShell 或以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="4c29b-119">Note that hello Azure Classic Portal does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-storage-metrics-using-powershell"></a><span data-ttu-id="4c29b-120">如何使用 PowerShell tooenable 儲存體度量</span><span class="sxs-lookup"><span data-stu-id="4c29b-120">How tooenable Storage metrics using PowerShell</span></span>
<span data-ttu-id="4c29b-121">您可以使用 hello Azure PowerShell cmdlet Get-azurestorageservicemetricsproperty tooretrieve hello 目前的設定，儲存體帳戶中使用 PowerShell 在您本機電腦 tooconfigure 儲存體度量和 hello cmdletSet-azurestorageservicemetricsproperty toochange hello 目前設定。</span><span class="sxs-lookup"><span data-stu-id="4c29b-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="4c29b-122">控制儲存體度量的 hello cmdlet 使用下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c29b-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="4c29b-123">MetricsType 的可能值為 Hour 和 Minute。</span><span class="sxs-lookup"><span data-stu-id="4c29b-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="4c29b-124">ServiceType 的可能值為 Blob、Queue 及 Table。</span><span class="sxs-lookup"><span data-stu-id="4c29b-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="4c29b-125">MetricsLevel 可能的值為 None (hello Azure 傳統入口網站中的對等 tooOff)，服務 (hello Azure 傳統入口網站中的對等 tooMinimal) 和 ServiceAndApi (hello Azure 傳統入口網站中的對等 tooVerbose)。</span><span class="sxs-lookup"><span data-stu-id="4c29b-125">MetricsLevel possible values are None (equivalent tooOff in hello Azure Classic Portal), Service (equivalent tooMinimal in hello Azure Classic Portal), and ServiceAndApi (equivalent tooVerbose in hello Azure Classic Portal).</span></span>

<span data-ttu-id="4c29b-126">例如，hello 下列命令會開啟分鐘 hello hello 保留期限預設儲存體帳戶中的 blob 服務的度量設定 toofive 天：</span><span class="sxs-lookup"><span data-stu-id="4c29b-126">For example, hello following command switches on minute metrics for hello blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="4c29b-127">hello comando siguiente recupera hello 目前每小時度量層級和保留天數的預設儲存體帳戶中的 hello blob 服務：</span><span class="sxs-lookup"><span data-stu-id="4c29b-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="4c29b-128">如需如何 tooconfigure hello Azure PowerShell cmdlet toowork 您 Azure 訂用帳戶及如何 tooselect hello 預設儲存體帳戶 toouse 資訊，請參閱：[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4c29b-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="4c29b-129">如何 tooenable 儲存體度量以程式設計的方式</span><span class="sxs-lookup"><span data-stu-id="4c29b-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="4c29b-130">hello 下列 C# 程式碼片段顯示如何 tooenable 度量和記錄 hello Blob 服務使用 hello 儲存體用戶端程式庫適用於.NET:</span><span class="sxs-lookup"><span data-stu-id="4c29b-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="4c29b-131">檢視儲存體度量</span><span class="sxs-lookup"><span data-stu-id="4c29b-131">Viewing Storage metrics</span></span>
<span data-ttu-id="4c29b-132">當您已設定儲存體度量 toomonitor 儲存體帳戶時，它會記錄一組已知資料表中儲存體帳戶中的 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="4c29b-132">When you have configured Storage Metrics toomonitor your storage account, it records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="4c29b-133">可供在圖表上，您可以使用儲存體帳戶中 hello Azure 傳統入口網站 tooview hello 每小時度量 hello [監視] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4c29b-133">You can use hello Monitor page for your storage account in hello Azure Classic Portal tooview hello hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="4c29b-134">這個頁面上 hello Azure 傳統入口網站中，您可以：</span><span class="sxs-lookup"><span data-stu-id="4c29b-134">On this page in hello Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="4c29b-135">選取 hello 圖表上的度量 tooplot （可用度量的 hello 選擇將取決於您選擇了 hello hello 設定 頁面上的服務的詳細資訊還是最小監控）。</span><span class="sxs-lookup"><span data-stu-id="4c29b-135">Select which metrics tooplot on hello chart (hello choice of available metrics will depend on whether you chose verbose or minimal monitoring for hello service on hello Configure page).</span></span>
* <span data-ttu-id="4c29b-136">選取 hello hello 度量 hello 圖表上顯示的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="4c29b-136">Select hello time range for hello metrics displayed on hello chart.</span></span>
* <span data-ttu-id="4c29b-137">選擇 toouse 絕對或相對比例 tooplot hello 度量資訊。</span><span class="sxs-lookup"><span data-stu-id="4c29b-137">Choose toouse an absolute or relative scale tooplot hello metrics.</span></span>
* <span data-ttu-id="4c29b-138">設定電子郵件警示 toonotify 時的特定度量達到特定的值。</span><span class="sxs-lookup"><span data-stu-id="4c29b-138">Configure email alerts toonotify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="4c29b-139">如果您想要 toodownload hello 度量長期的儲存體或 tooanalyze 它們在本機，您將需要 toouse 工具或撰寫一些程式碼 tooread hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="4c29b-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need toouse a tool or write some code tooread hello tables.</span></span> <span data-ttu-id="4c29b-140">您必須下載 hello 分鐘度量以供分析。</span><span class="sxs-lookup"><span data-stu-id="4c29b-140">You must download hello minute metrics for analysis.</span></span> <span data-ttu-id="4c29b-141">如果您列出所有 hello 資料表儲存體帳戶中，但您可以直接透過名稱存取這些 hello 資料表不會出現。</span><span class="sxs-lookup"><span data-stu-id="4c29b-141">hello tables do not appear if you list all hello tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="4c29b-142">許多協力廠商儲存體瀏覽工具會察覺這些資料表，並讓您 tooview 它們直接 (請參閱 hello 部落格文章[Microsoft Azure 儲存體總管](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)取得一份可用的工具)。</span><span class="sxs-lookup"><span data-stu-id="4c29b-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly (see hello blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="4c29b-143">每小時度量</span><span class="sxs-lookup"><span data-stu-id="4c29b-143">Hourly metrics</span></span>
* <span data-ttu-id="4c29b-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="4c29b-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="4c29b-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="4c29b-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="4c29b-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="4c29b-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="4c29b-147">每分鐘度量</span><span class="sxs-lookup"><span data-stu-id="4c29b-147">Minute metrics</span></span>
* <span data-ttu-id="4c29b-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="4c29b-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="4c29b-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="4c29b-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="4c29b-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="4c29b-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="4c29b-151">容量</span><span class="sxs-lookup"><span data-stu-id="4c29b-151">Capacity</span></span>
* <span data-ttu-id="4c29b-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="4c29b-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="4c29b-153">您可以找到 hello 結構描述的完整詳細資料，在這些資料表[儲存體分析度量資料表結構描述](https://msdn.microsoft.com/library/azure/hh343264.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4c29b-153">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="4c29b-154">以下的 hello 範例資料列僅顯示部分 hello 可用的資料行，但說明 hello 方式儲存體度量會儲存這些度量的一些重要功能：</span><span class="sxs-lookup"><span data-stu-id="4c29b-154">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="4c29b-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="4c29b-155">PartitionKey</span></span> | <span data-ttu-id="4c29b-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="4c29b-156">RowKey</span></span> | <span data-ttu-id="4c29b-157">Timestamp</span><span class="sxs-lookup"><span data-stu-id="4c29b-157">Timestamp</span></span> | <span data-ttu-id="4c29b-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="4c29b-158">TotalRequests</span></span> | <span data-ttu-id="4c29b-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="4c29b-159">TotalBillableRequests</span></span> | <span data-ttu-id="4c29b-160">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="4c29b-160">TotalIngress</span></span> | <span data-ttu-id="4c29b-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="4c29b-161">TotalEgress</span></span> | <span data-ttu-id="4c29b-162">Availability</span><span class="sxs-lookup"><span data-stu-id="4c29b-162">Availability</span></span> | <span data-ttu-id="4c29b-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="4c29b-163">AverageE2ELatency</span></span> | <span data-ttu-id="4c29b-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="4c29b-164">AverageServerLatency</span></span> | <span data-ttu-id="4c29b-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="4c29b-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4c29b-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="4c29b-166">20140522T1100</span></span> |<span data-ttu-id="4c29b-167">user;All</span><span class="sxs-lookup"><span data-stu-id="4c29b-167">user;All</span></span> |<span data-ttu-id="4c29b-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="4c29b-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="4c29b-169">7</span><span class="sxs-lookup"><span data-stu-id="4c29b-169">7</span></span> |<span data-ttu-id="4c29b-170">7</span><span class="sxs-lookup"><span data-stu-id="4c29b-170">7</span></span> |<span data-ttu-id="4c29b-171">4003</span><span class="sxs-lookup"><span data-stu-id="4c29b-171">4003</span></span> |<span data-ttu-id="4c29b-172">46801</span><span class="sxs-lookup"><span data-stu-id="4c29b-172">46801</span></span> |<span data-ttu-id="4c29b-173">100</span><span class="sxs-lookup"><span data-stu-id="4c29b-173">100</span></span> |<span data-ttu-id="4c29b-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="4c29b-174">104.4286</span></span> |<span data-ttu-id="4c29b-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="4c29b-175">6.857143</span></span> |<span data-ttu-id="4c29b-176">100</span><span class="sxs-lookup"><span data-stu-id="4c29b-176">100</span></span> |
| <span data-ttu-id="4c29b-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="4c29b-177">20140522T1100</span></span> |<span data-ttu-id="4c29b-178">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="4c29b-178">user;QueryEntities</span></span> |<span data-ttu-id="4c29b-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="4c29b-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="4c29b-180">5</span><span class="sxs-lookup"><span data-stu-id="4c29b-180">5</span></span> |<span data-ttu-id="4c29b-181">5</span><span class="sxs-lookup"><span data-stu-id="4c29b-181">5</span></span> |<span data-ttu-id="4c29b-182">2694</span><span class="sxs-lookup"><span data-stu-id="4c29b-182">2694</span></span> |<span data-ttu-id="4c29b-183">45951</span><span class="sxs-lookup"><span data-stu-id="4c29b-183">45951</span></span> |<span data-ttu-id="4c29b-184">100</span><span class="sxs-lookup"><span data-stu-id="4c29b-184">100</span></span> |<span data-ttu-id="4c29b-185">143.8</span><span class="sxs-lookup"><span data-stu-id="4c29b-185">143.8</span></span> |<span data-ttu-id="4c29b-186">7.8</span><span class="sxs-lookup"><span data-stu-id="4c29b-186">7.8</span></span> |<span data-ttu-id="4c29b-187">100</span><span class="sxs-lookup"><span data-stu-id="4c29b-187">100</span></span> |
| <span data-ttu-id="4c29b-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="4c29b-188">20140522T1100</span></span> |<span data-ttu-id="4c29b-189">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="4c29b-189">user;QueryEntity</span></span> |<span data-ttu-id="4c29b-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="4c29b-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="4c29b-191">1</span><span class="sxs-lookup"><span data-stu-id="4c29b-191">1</span></span> |<span data-ttu-id="4c29b-192">1</span><span class="sxs-lookup"><span data-stu-id="4c29b-192">1</span></span> |<span data-ttu-id="4c29b-193">538</span><span class="sxs-lookup"><span data-stu-id="4c29b-193">538</span></span> |<span data-ttu-id="4c29b-194">633</span><span class="sxs-lookup"><span data-stu-id="4c29b-194">633</span></span> |<span data-ttu-id="4c29b-195">100</span><span class="sxs-lookup"><span data-stu-id="4c29b-195">100</span></span> |<span data-ttu-id="4c29b-196">3</span><span class="sxs-lookup"><span data-stu-id="4c29b-196">3</span></span> |<span data-ttu-id="4c29b-197">3</span><span class="sxs-lookup"><span data-stu-id="4c29b-197">3</span></span> |<span data-ttu-id="4c29b-198">100</span><span class="sxs-lookup"><span data-stu-id="4c29b-198">100</span></span> |
| <span data-ttu-id="4c29b-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="4c29b-199">20140522T1100</span></span> |<span data-ttu-id="4c29b-200">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="4c29b-200">user;UpdateEntity</span></span> |<span data-ttu-id="4c29b-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="4c29b-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="4c29b-202">1</span><span class="sxs-lookup"><span data-stu-id="4c29b-202">1</span></span> |<span data-ttu-id="4c29b-203">1</span><span class="sxs-lookup"><span data-stu-id="4c29b-203">1</span></span> |<span data-ttu-id="4c29b-204">771</span><span class="sxs-lookup"><span data-stu-id="4c29b-204">771</span></span> |<span data-ttu-id="4c29b-205">217</span><span class="sxs-lookup"><span data-stu-id="4c29b-205">217</span></span> |<span data-ttu-id="4c29b-206">100</span><span class="sxs-lookup"><span data-stu-id="4c29b-206">100</span></span> |<span data-ttu-id="4c29b-207">9</span><span class="sxs-lookup"><span data-stu-id="4c29b-207">9</span></span> |<span data-ttu-id="4c29b-208">6</span><span class="sxs-lookup"><span data-stu-id="4c29b-208">6</span></span> |<span data-ttu-id="4c29b-209">100</span><span class="sxs-lookup"><span data-stu-id="4c29b-209">100</span></span> |

<span data-ttu-id="4c29b-210">此範例中的每分鐘度量資料，hello 資料分割索引鍵會使用分鐘解析 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="4c29b-210">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="4c29b-211">hello 資料列索引鍵識別 hello hello 資料列中儲存的資訊類型，這資訊、 hello 存取類型和 hello 要求類型之兩個部分所組成：</span><span class="sxs-lookup"><span data-stu-id="4c29b-211">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="4c29b-212">使用者或系統，其中使用者是指 tooall 使用者要求 toohello 儲存體服務，而系統會參考儲存體分析所做的 toorequests hello 存取類型。</span><span class="sxs-lookup"><span data-stu-id="4c29b-212">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="4c29b-213">hello 要求類型是所有在此情況下它可能摘要行，或者它會識別例如 QueryEntity 或 UpdateEntity hello 特定 API。</span><span class="sxs-lookup"><span data-stu-id="4c29b-213">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="4c29b-214">所有 hello 如上 hello 範例資料記錄 （從上午 11:00 開始） 的一分鐘，QueryEntities 要求因此 hello 數目加上 hello QueryEntity 要求數目加上 hello UpdateEntity 要求數目加總 tooseven，是 hello 總上所顯示hello user: All 資料列。</span><span class="sxs-lookup"><span data-stu-id="4c29b-214">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="4c29b-215">同樣地，您可以藉由計算衍生 hello 平均端對端延遲 104.4286 hello user: All 資料列上的 ((143.8 * 5) + 3 + 9) / 7。</span><span class="sxs-lookup"><span data-stu-id="4c29b-215">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="4c29b-216">您應該考慮 hello [監視] 頁面上的 hello Azure 傳統入口網站中的警示設定儲存體度量自動通知您任何的儲存體服務的 hello 行為的重要變更。如果您使用儲存體總管工具 toodownload 此度量資料分隔的格式，您可以使用 Microsoft Excel tooanalyze hello 資料。</span><span class="sxs-lookup"><span data-stu-id="4c29b-216">You should consider setting up alerts in hello Azure Classic Portal on hello Monitor page so that Storage Metrics can automatically notify you of any important changes in hello behavior of your storage services.If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="4c29b-217">請參閱 hello 部落格文章[Microsoft Azure 儲存體總管](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)取得一份可用的儲存體總管工具。</span><span class="sxs-lookup"><span data-stu-id="4c29b-217">See hello blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="4c29b-218">以程式設計方式存取度量資料</span><span class="sxs-lookup"><span data-stu-id="4c29b-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="4c29b-219">hello 下列清單顯示範例 C# 程式碼可存取某幾分鐘的 hello 分鐘度量，並且會顯示在主控台視窗中的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="4c29b-219">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="4c29b-220">它會使用 hello Azure 儲存體程式庫第 4 版包含 hello CloudAnalyticsClient 類別，可簡化存取儲存體中的 hello 度量資料表。</span><span class="sxs-lookup"><span data-stu-id="4c29b-220">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="4c29b-221">當您啟用儲存體度量時，會產生哪些費用？</span><span class="sxs-lookup"><span data-stu-id="4c29b-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="4c29b-222">寫入要求 toocreate 資料表實體的度量資訊會收費 hello 標準費率適用 tooall Azure 儲存體作業。</span><span class="sxs-lookup"><span data-stu-id="4c29b-222">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="4c29b-223">由用戶端 toometrics 資料的讀取與刪除要求也是標準費率計費。</span><span class="sxs-lookup"><span data-stu-id="4c29b-223">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="4c29b-224">如果您已設定資料保留原則，就不需要在 Azure 儲存體刪除舊的度量資料時付費。</span><span class="sxs-lookup"><span data-stu-id="4c29b-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="4c29b-225">不過，如果您刪除分析資料，您的帳戶則需支付 hello 刪除作業。</span><span class="sxs-lookup"><span data-stu-id="4c29b-225">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="4c29b-226">hello 度量資料表所使用的 hello 容量也會列入計費： 您可以使用下列用來儲存度量資料的容量 tooestimate hello 數量的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c29b-226">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="4c29b-227">如果每小時的服務會利用每項服務中的每個 API，大約 148KB 的資料將儲存 hello 度量交易資料表中每個小時，如果您已啟用服務和應用程式開發介面層級摘要。</span><span class="sxs-lookup"><span data-stu-id="4c29b-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="4c29b-228">如果每小時的服務會利用每項服務中的每個 API，大約 12KB 的資料將儲存 hello 度量交易資料表中每個小時，如果您已啟用只服務層級摘要。</span><span class="sxs-lookup"><span data-stu-id="4c29b-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="4c29b-229">hello blob 的容量資料表有兩個資料列加入每一天 （提供的記錄檔的使用者已選擇加入）： 這表示，此資料表的每日 hello 大小增加總 tooapproximately 300 個位元組。</span><span class="sxs-lookup"><span data-stu-id="4c29b-229">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c29b-230">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="4c29b-230">Next steps:</span></span>
[<span data-ttu-id="4c29b-231">啟用儲存體分析記錄和存取記錄檔資料</span><span class="sxs-lookup"><span data-stu-id="4c29b-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)
