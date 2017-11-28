---
title: "aaaEnabling hello Azure 入口網站中的儲存體度量 |Microsoft 文件"
description: "如何儲存體度量 tooenable hello Blob、 佇列、 表格和檔案服務"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: f157dbdf9a256da7ab186f80db746b91d1a9beb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="6ffb5-103">啟用 Azure 儲存體計量和檢視計量資料</span><span class="sxs-lookup"><span data-stu-id="6ffb5-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="6ffb5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6ffb5-104">Overview</span></span>
<span data-ttu-id="6ffb5-105">當您建立新的儲存體帳戶時，預設會啟用「儲存體計量」。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="6ffb5-106">您可以設定監視透過 hello [Azure 入口網站](https://portal.azure.com)或 Windows PowerShell 或以程式設計方式透過其中一個 hello 儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="6ffb5-107">您可以設定 hello 度量資料的保留期限： 此期間決定多久 hello 儲存體服務可以維持 hello 度量，並且您 hello 空間需要的 toostore 費用它們。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="6ffb5-108">一般而言，您應該於每小時度量的每分鐘度量使用較短的保留期限因為 hello 重大的額外空間所需的每分鐘度量。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="6ffb5-109">您應該選擇的保留期限，您有足夠時間 tooanalyze hello 資料，並下載您想 tookeep 供離線分析或報告之用的任何度量。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="6ffb5-110">請記住，您還是必須支付從儲存體帳戶下載度量資料的費用。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="6ffb5-111">如何使用 tooenable 度量 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6ffb5-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="6ffb5-112">請遵循這些步驟 tooenable 中的計量 hello [Azure 入口網站](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="6ffb5-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="6ffb5-113">瀏覽 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="6ffb5-114">選取**診斷**上 hello**功能表**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="6ffb5-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="6ffb5-115">請確認**狀態**設定得**上**。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="6ffb5-116">選取 hello hello 服務的度量，您需要 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="6ffb5-117">指定保留原則 tooindicate 多久 tooretain 度量和記錄資料。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="6ffb5-118">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-118">Select **Save**.</span></span>

<span data-ttu-id="6ffb5-119">請注意該 hello [Azure 入口網站](https://portal.azure.com)目前無法讓您 tooconfigure 分鐘度量，在儲存體帳戶; 您必須啟用分鐘度量使用 PowerShell 或以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="6ffb5-120">如何使用 PowerShell tooenable 度量</span><span class="sxs-lookup"><span data-stu-id="6ffb5-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="6ffb5-121">您可以使用 hello Azure PowerShell cmdlet Get-azurestorageservicemetricsproperty tooretrieve hello 目前的設定，儲存體帳戶中使用 PowerShell 在您本機電腦 tooconfigure 儲存體度量和 hello cmdletSet-azurestorageservicemetricsproperty toochange hello 目前設定。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="6ffb5-122">控制儲存體度量的 hello cmdlet 使用下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb5-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="6ffb5-123">MetricsType：可能值為 Hour 和 Minute。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="6ffb5-124">ServiceType：可能值為 Blob、Queue 及 Table。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="6ffb5-125">MetricsLevel：可能值為 None、服務，以及 ServiceAndApi。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="6ffb5-126">例如，hello 下列命令會開啟分鐘 hello hello 保留期限預設儲存體帳戶中的 Blob 服務的度量設定 toofive 天：</span><span class="sxs-lookup"><span data-stu-id="6ffb5-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="6ffb5-127">hello comando siguiente recupera hello 目前每小時度量層級和保留天數的預設儲存體帳戶中的 hello blob 服務：</span><span class="sxs-lookup"><span data-stu-id="6ffb5-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="6ffb5-128">如需如何 tooconfigure hello Azure PowerShell cmdlet toowork 您 Azure 訂用帳戶及如何 tooselect hello 預設儲存體帳戶 toouse 資訊，請參閱：[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="6ffb5-129">如何 tooenable 儲存體度量以程式設計的方式</span><span class="sxs-lookup"><span data-stu-id="6ffb5-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="6ffb5-130">hello 下列 C# 程式碼片段顯示如何 tooenable 度量和記錄 hello Blob 服務使用 hello 儲存體用戶端程式庫適用於.NET:</span><span class="sxs-lookup"><span data-stu-id="6ffb5-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

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

## <a name="viewing-storage-metrics"></a><span data-ttu-id="6ffb5-131">檢視儲存體度量</span><span class="sxs-lookup"><span data-stu-id="6ffb5-131">Viewing Storage metrics</span></span>
<span data-ttu-id="6ffb5-132">設定儲存體分析度量 toomonitor 儲存體帳戶之後，儲存體分析會記錄在一組已知資料表儲存體帳戶中的 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="6ffb5-133">您可以在 hello 設定圖表 tooview 每小時度量[Azure 入口網站](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="6ffb5-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="6ffb5-134">瀏覽 tooyour 儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="6ffb5-135">選取**度量**在 hello**功能表**刀鋒視窗中的 hello 服務其計量想 tooview。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="6ffb5-136">選取**編輯**想 tooconfigure hello 圖表上。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="6ffb5-137">在 hello**編輯圖表**刀鋒視窗中，選取 hello**時間範圍**，**圖表類型**，和您想要顯示 hello 圖表中的 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="6ffb5-138">選取 [確定]</span><span class="sxs-lookup"><span data-stu-id="6ffb5-138">Select **OK**</span></span>

<span data-ttu-id="6ffb5-139">如果您想 toodownload hello 度量的長期存放裝置或 tooanalyze 它們在本機，您必須：</span><span class="sxs-lookup"><span data-stu-id="6ffb5-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="6ffb5-140">使用會察覺這些資料表，並將 tooview 可讓您和下載這些工具。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="6ffb5-141">撰寫自訂的應用程式或指令碼 tooread 和 hello 資料表儲存。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="6ffb5-142">許多協力廠商儲存體瀏覽工具會察覺這些資料表，並讓您 tooview 它們直接。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="6ffb5-143">如需可用工具的清單，請參閱 [Azure 儲存體用戶端工具](storage-explorers.md)。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="6ffb5-144">從 0.8.0 版的 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)，您可以檢視和下載 hello 分析度量資料表。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="6ffb5-145">順序 tooaccess hello 分析中的資料表以程式設計的方式，請注意是否您列出儲存體帳戶中的所有 hello 資料表 hello 分析資料表不會出現。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="6ffb5-146">您可以直接透過名稱，存取它們，或使用 hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) hello.NET 用戶端程式庫 tooquery hello 資料表名稱中。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="6ffb5-147">每小時度量</span><span class="sxs-lookup"><span data-stu-id="6ffb5-147">Hourly metrics</span></span>
* <span data-ttu-id="6ffb5-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="6ffb5-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="6ffb5-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="6ffb5-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="6ffb5-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="6ffb5-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="6ffb5-151">每分鐘度量</span><span class="sxs-lookup"><span data-stu-id="6ffb5-151">Minute metrics</span></span>
* <span data-ttu-id="6ffb5-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="6ffb5-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="6ffb5-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="6ffb5-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="6ffb5-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="6ffb5-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="6ffb5-155">容量</span><span class="sxs-lookup"><span data-stu-id="6ffb5-155">Capacity</span></span>
* <span data-ttu-id="6ffb5-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="6ffb5-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="6ffb5-157">您可以找到 hello 結構描述的完整詳細資料，在這些資料表[儲存體分析度量資料表結構描述](https://msdn.microsoft.com/library/azure/hh343264.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="6ffb5-158">以下的 hello 範例資料列僅顯示部分 hello 可用的資料行，但說明 hello 方式儲存體度量會儲存這些度量的一些重要功能：</span><span class="sxs-lookup"><span data-stu-id="6ffb5-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="6ffb5-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="6ffb5-159">PartitionKey</span></span> | <span data-ttu-id="6ffb5-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="6ffb5-160">RowKey</span></span> | <span data-ttu-id="6ffb5-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="6ffb5-161">Timestamp</span></span> | <span data-ttu-id="6ffb5-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="6ffb5-162">TotalRequests</span></span> | <span data-ttu-id="6ffb5-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="6ffb5-163">TotalBillableRequests</span></span> | <span data-ttu-id="6ffb5-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="6ffb5-164">TotalIngress</span></span> | <span data-ttu-id="6ffb5-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="6ffb5-165">TotalEgress</span></span> | <span data-ttu-id="6ffb5-166">Availability</span><span class="sxs-lookup"><span data-stu-id="6ffb5-166">Availability</span></span> | <span data-ttu-id="6ffb5-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="6ffb5-167">AverageE2ELatency</span></span> | <span data-ttu-id="6ffb5-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="6ffb5-168">AverageServerLatency</span></span> | <span data-ttu-id="6ffb5-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="6ffb5-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="6ffb5-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-170">20140522T1100</span></span> |<span data-ttu-id="6ffb5-171">user;All</span><span class="sxs-lookup"><span data-stu-id="6ffb5-171">user;All</span></span> |<span data-ttu-id="6ffb5-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="6ffb5-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="6ffb5-173">7</span><span class="sxs-lookup"><span data-stu-id="6ffb5-173">7</span></span> |<span data-ttu-id="6ffb5-174">7</span><span class="sxs-lookup"><span data-stu-id="6ffb5-174">7</span></span> |<span data-ttu-id="6ffb5-175">4003</span><span class="sxs-lookup"><span data-stu-id="6ffb5-175">4003</span></span> |<span data-ttu-id="6ffb5-176">46801</span><span class="sxs-lookup"><span data-stu-id="6ffb5-176">46801</span></span> |<span data-ttu-id="6ffb5-177">100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-177">100</span></span> |<span data-ttu-id="6ffb5-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="6ffb5-178">104.4286</span></span> |<span data-ttu-id="6ffb5-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="6ffb5-179">6.857143</span></span> |<span data-ttu-id="6ffb5-180">100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-180">100</span></span> |
| <span data-ttu-id="6ffb5-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-181">20140522T1100</span></span> |<span data-ttu-id="6ffb5-182">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="6ffb5-182">user;QueryEntities</span></span> |<span data-ttu-id="6ffb5-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="6ffb5-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="6ffb5-184">5</span><span class="sxs-lookup"><span data-stu-id="6ffb5-184">5</span></span> |<span data-ttu-id="6ffb5-185">5</span><span class="sxs-lookup"><span data-stu-id="6ffb5-185">5</span></span> |<span data-ttu-id="6ffb5-186">2694</span><span class="sxs-lookup"><span data-stu-id="6ffb5-186">2694</span></span> |<span data-ttu-id="6ffb5-187">45951</span><span class="sxs-lookup"><span data-stu-id="6ffb5-187">45951</span></span> |<span data-ttu-id="6ffb5-188">100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-188">100</span></span> |<span data-ttu-id="6ffb5-189">143.8</span><span class="sxs-lookup"><span data-stu-id="6ffb5-189">143.8</span></span> |<span data-ttu-id="6ffb5-190">7.8</span><span class="sxs-lookup"><span data-stu-id="6ffb5-190">7.8</span></span> |<span data-ttu-id="6ffb5-191">100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-191">100</span></span> |
| <span data-ttu-id="6ffb5-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-192">20140522T1100</span></span> |<span data-ttu-id="6ffb5-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="6ffb5-193">user;QueryEntity</span></span> |<span data-ttu-id="6ffb5-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="6ffb5-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="6ffb5-195">1</span><span class="sxs-lookup"><span data-stu-id="6ffb5-195">1</span></span> |<span data-ttu-id="6ffb5-196">1</span><span class="sxs-lookup"><span data-stu-id="6ffb5-196">1</span></span> |<span data-ttu-id="6ffb5-197">538</span><span class="sxs-lookup"><span data-stu-id="6ffb5-197">538</span></span> |<span data-ttu-id="6ffb5-198">633</span><span class="sxs-lookup"><span data-stu-id="6ffb5-198">633</span></span> |<span data-ttu-id="6ffb5-199">100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-199">100</span></span> |<span data-ttu-id="6ffb5-200">3</span><span class="sxs-lookup"><span data-stu-id="6ffb5-200">3</span></span> |<span data-ttu-id="6ffb5-201">3</span><span class="sxs-lookup"><span data-stu-id="6ffb5-201">3</span></span> |<span data-ttu-id="6ffb5-202">100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-202">100</span></span> |
| <span data-ttu-id="6ffb5-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-203">20140522T1100</span></span> |<span data-ttu-id="6ffb5-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="6ffb5-204">user;UpdateEntity</span></span> |<span data-ttu-id="6ffb5-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="6ffb5-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="6ffb5-206">1</span><span class="sxs-lookup"><span data-stu-id="6ffb5-206">1</span></span> |<span data-ttu-id="6ffb5-207">1</span><span class="sxs-lookup"><span data-stu-id="6ffb5-207">1</span></span> |<span data-ttu-id="6ffb5-208">771</span><span class="sxs-lookup"><span data-stu-id="6ffb5-208">771</span></span> |<span data-ttu-id="6ffb5-209">217</span><span class="sxs-lookup"><span data-stu-id="6ffb5-209">217</span></span> |<span data-ttu-id="6ffb5-210">100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-210">100</span></span> |<span data-ttu-id="6ffb5-211">9</span><span class="sxs-lookup"><span data-stu-id="6ffb5-211">9</span></span> |<span data-ttu-id="6ffb5-212">6</span><span class="sxs-lookup"><span data-stu-id="6ffb5-212">6</span></span> |<span data-ttu-id="6ffb5-213">100</span><span class="sxs-lookup"><span data-stu-id="6ffb5-213">100</span></span> |

<span data-ttu-id="6ffb5-214">此範例中的每分鐘度量資料，hello 資料分割索引鍵會使用分鐘解析 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="6ffb5-215">hello 資料列索引鍵識別 hello hello 資料列中儲存的資訊類型，這資訊、 hello 存取類型和 hello 要求類型之兩個部分所組成：</span><span class="sxs-lookup"><span data-stu-id="6ffb5-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="6ffb5-216">使用者或系統，其中使用者是指 tooall 使用者要求 toohello 儲存體服務，而系統會參考儲存體分析所做的 toorequests hello 存取類型。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="6ffb5-217">hello 要求類型是所有在此情況下它可能摘要行，或者它會識別例如 QueryEntity 或 UpdateEntity hello 特定 API。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="6ffb5-218">所有 hello 如上 hello 範例資料記錄 （從上午 11:00 開始） 的一分鐘，QueryEntities 要求因此 hello 數目加上 hello QueryEntity 要求數目加上 hello UpdateEntity 要求數目加總 tooseven，是 hello 總上所顯示hello user: All 資料列。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="6ffb5-219">同樣地，您可以藉由計算衍生 hello 平均端對端延遲 104.4286 hello user: All 資料列上的 ((143.8 * 5) + 3 + 9) / 7。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="6ffb5-220">計量警示</span><span class="sxs-lookup"><span data-stu-id="6ffb5-220">Metrics alerts</span></span>
<span data-ttu-id="6ffb5-221">您應該考慮設定警示 hello [Azure 入口網站](https://portal.azure.com)讓儲存體度量自動通知您重要的儲存體服務的 hello 行為的變更。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="6ffb5-222">如果您使用儲存體總管工具 toodownload 此度量資料分隔的格式，您可以使用 Microsoft Excel tooanalyze hello 資料。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="6ffb5-223">如需可用的儲存體總管工具清單，請參閱 [Azure 儲存體用戶端工具](storage-explorers.md)。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="6ffb5-224">您可以設定警示 hello**警示規則**刀鋒視窗中，存取**監視**hello 儲存體帳戶功能表刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ffb5-225">可能的儲存體事件與 hello 對應每小時或分鐘度量資料時就會記錄之間的延遲。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="6ffb5-226">中的每分鐘度量 hello 案例中，可能會一次寫入幾分鐘的資料。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="6ffb5-227">這會導致 tootransactions 進行彙總 hello 交易 hello 目前的分鐘到幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="6ffb5-228">當發生這種情況時，服務可能沒有 hello 的所有可用的度量資料的 hello 警示設定警示的間隔，可能會導致非預期地引發 tooalerts。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="6ffb5-229">以程式設計方式存取度量資料</span><span class="sxs-lookup"><span data-stu-id="6ffb5-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="6ffb5-230">hello 下列清單顯示範例 C# 程式碼可存取某幾分鐘的 hello 分鐘度量，並且會顯示在主控台視窗中的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="6ffb5-231">它會使用 hello Azure 儲存體程式庫第 4 版包含 hello CloudAnalyticsClient 類別，可簡化存取儲存體中的 hello 度量資料表。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="6ffb5-232">當您啟用儲存體度量時，會產生哪些費用？</span><span class="sxs-lookup"><span data-stu-id="6ffb5-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="6ffb5-233">寫入要求 toocreate 資料表實體的度量資訊會收費 hello 標準費率適用 tooall Azure 儲存體作業。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="6ffb5-234">由用戶端 toometrics 資料的讀取與刪除要求也是標準費率計費。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="6ffb5-235">如果您已設定資料保留原則，就不需要在 Azure 儲存體刪除舊的度量資料時付費。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="6ffb5-236">不過，如果您刪除分析資料，您的帳戶則需支付 hello 刪除作業。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="6ffb5-237">hello 度量資料表所使用的 hello 容量也會列入計費： 您可以使用下列用來儲存度量資料的容量 tooestimate hello 數量的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb5-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="6ffb5-238">如果每小時的服務會利用每項服務中的每個 API，大約 148KB 的資料將儲存 hello 度量交易資料表中每個小時，如果您已啟用服務和應用程式開發介面層級摘要。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="6ffb5-239">如果每小時的服務會利用每項服務中的每個 API，大約 12KB 的資料將儲存 hello 度量交易資料表中每個小時，如果您已啟用只服務層級摘要。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="6ffb5-240">hello blob 的容量資料表有兩個資料列加入每一天 （提供的記錄檔的使用者已選擇加入）： 這表示，此資料表的每日 hello 大小增加總 tooapproximately 300 個位元組。</span><span class="sxs-lookup"><span data-stu-id="6ffb5-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ffb5-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ffb5-241">Next steps</span></span>
[<span data-ttu-id="6ffb5-242">啟用儲存體記錄和存取記錄檔資料</span><span class="sxs-lookup"><span data-stu-id="6ffb5-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
