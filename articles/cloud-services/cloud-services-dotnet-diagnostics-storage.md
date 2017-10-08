---
title: "aaaStore 和檢視診斷資料，在 Azure 儲存體 |Microsoft 文件"
description: "將 Azure 診斷資料放入 Azure 儲存體並加以檢視"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="1cdb3-103">在 Azure 儲存體中儲存和檢視診斷資料</span><span class="sxs-lookup"><span data-stu-id="1cdb3-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="1cdb3-104">除非您傳送 toohello Microsoft Azure 儲存體模擬器或 tooAzure 存放裝置，不會永久儲存診斷資料。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-104">Diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="1cdb3-105">一旦位於儲存體，即可利用其中一個可用的工具進行檢視。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="1cdb3-106">指定儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1cdb3-106">Specify a storage account</span></span>
<span data-ttu-id="1cdb3-107">您指定您想 toouse hello ServiceConfiguration.cscfg 檔案中的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-107">You specify hello storage account that you want toouse in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="1cdb3-108">hello 帳戶資訊定義為組態設定中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-108">hello account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="1cdb3-109">hello 下例示範建立新的雲端服務專案，Visual Studio 中的 hello 預設連接字串：</span><span class="sxs-lookup"><span data-stu-id="1cdb3-109">hello following example shows hello default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="1cdb3-110">您可以變更此連接字串 tooprovide 帳戶資訊的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-110">You can change this connection string tooprovide account information for an Azure storage account.</span></span>

<span data-ttu-id="1cdb3-111">根據 hello 所收集的診斷資料類型，Azure 診斷會使用 hello Blob 服務或 hello 表格服務。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-111">Depending on hello type of diagnostic data that is being collected, Azure Diagnostics uses either hello Blob service or hello Table service.</span></span> <span data-ttu-id="1cdb3-112">hello 下表顯示 hello 會保存的資料來源以及其格式。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-112">hello following table shows hello data sources that are persisted and their format.</span></span>

| <span data-ttu-id="1cdb3-113">資料來源</span><span class="sxs-lookup"><span data-stu-id="1cdb3-113">Data source</span></span> | <span data-ttu-id="1cdb3-114">儲存體格式</span><span class="sxs-lookup"><span data-stu-id="1cdb3-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="1cdb3-115">Azure 記錄檔</span><span class="sxs-lookup"><span data-stu-id="1cdb3-115">Azure logs</span></span> |<span data-ttu-id="1cdb3-116">資料表</span><span class="sxs-lookup"><span data-stu-id="1cdb3-116">Table</span></span> |
| <span data-ttu-id="1cdb3-117">IIS 7.0 記錄檔</span><span class="sxs-lookup"><span data-stu-id="1cdb3-117">IIS 7.0 logs</span></span> |<span data-ttu-id="1cdb3-118">Blob</span><span class="sxs-lookup"><span data-stu-id="1cdb3-118">Blob</span></span> |
| <span data-ttu-id="1cdb3-119">Azure 診斷基礎結構記錄檔</span><span class="sxs-lookup"><span data-stu-id="1cdb3-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="1cdb3-120">資料表</span><span class="sxs-lookup"><span data-stu-id="1cdb3-120">Table</span></span> |
| <span data-ttu-id="1cdb3-121">失敗要求追蹤記錄檔</span><span class="sxs-lookup"><span data-stu-id="1cdb3-121">Failed Request Trace logs</span></span> |<span data-ttu-id="1cdb3-122">Blob</span><span class="sxs-lookup"><span data-stu-id="1cdb3-122">Blob</span></span> |
| <span data-ttu-id="1cdb3-123">Windows 事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="1cdb3-123">Windows Event logs</span></span> |<span data-ttu-id="1cdb3-124">資料表</span><span class="sxs-lookup"><span data-stu-id="1cdb3-124">Table</span></span> |
| <span data-ttu-id="1cdb3-125">效能計數器</span><span class="sxs-lookup"><span data-stu-id="1cdb3-125">Performance counters</span></span> |<span data-ttu-id="1cdb3-126">資料表</span><span class="sxs-lookup"><span data-stu-id="1cdb3-126">Table</span></span> |
| <span data-ttu-id="1cdb3-127">損毀傾印</span><span class="sxs-lookup"><span data-stu-id="1cdb3-127">Crash dumps</span></span> |<span data-ttu-id="1cdb3-128">Blob</span><span class="sxs-lookup"><span data-stu-id="1cdb3-128">Blob</span></span> |
| <span data-ttu-id="1cdb3-129">自訂錯誤記錄檔</span><span class="sxs-lookup"><span data-stu-id="1cdb3-129">Custom error logs</span></span> |<span data-ttu-id="1cdb3-130">Blob</span><span class="sxs-lookup"><span data-stu-id="1cdb3-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="1cdb3-131">傳輸診斷資料</span><span class="sxs-lookup"><span data-stu-id="1cdb3-131">Transfer diagnostic data</span></span>
<span data-ttu-id="1cdb3-132">SDK 2.5 和更新版本、 hello 要求 tootransfer 診斷資料可能透過 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-132">For SDK 2.5 and later, hello request tootransfer diagnostic data can occur through hello configuration file.</span></span> <span data-ttu-id="1cdb3-133">您可以在 hello 組態中所指定的排程間隔傳輸診斷資料。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-133">You can transfer diagnostic data at scheduled intervals as specified in hello configuration.</span></span>

<span data-ttu-id="1cdb3-134">SDK 2.4 和前一個您可以透過 hello 設定檔，以程式設計方式要求 tootransfer hello 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-134">For SDK 2.4 and previous you can request tootransfer hello diagnostic data through hello configuration file as well as programmatically.</span></span> <span data-ttu-id="1cdb3-135">hello 以程式設計的方式也可讓您 toodo 上隨選傳輸。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-135">hello programmatic approach also allows you toodo on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1cdb3-136">當您將傳輸診斷資料 tooan Azure 儲存體帳戶時，就會發生 hello 儲存體資源的診斷資料所使用的成本。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-136">When you transfer diagnostic data tooan Azure storage account, you incur costs for hello storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="1cdb3-137">儲存診斷資料</span><span class="sxs-lookup"><span data-stu-id="1cdb3-137">Store diagnostic data</span></span>
<span data-ttu-id="1cdb3-138">記錄檔資料會儲存在 Blob 或資料表儲存體，以下列名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="1cdb3-138">Log data is stored in either Blob or Table storage with hello following names:</span></span>

<span data-ttu-id="1cdb3-139">**資料表 (英文)**</span><span class="sxs-lookup"><span data-stu-id="1cdb3-139">**Tables**</span></span>

* <span data-ttu-id="1cdb3-140">**WadLogsTable** -以使用 hello 追蹤接聽程式的程式碼撰寫的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-140">**WadLogsTable** - Logs written in code using hello trace listener.</span></span>
* <span data-ttu-id="1cdb3-141">**WADDiagnosticInfrastructureLogsTable** - 診斷監視器和組態變更。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="1cdb3-142">**WADDirectoriesTable** – 該 hello 診斷監視器所監視的目錄。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-142">**WADDirectoriesTable** – Directories that hello diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="1cdb3-143">這包括 IIS 記錄檔、IIS 失敗要求記錄檔和自訂目錄。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="1cdb3-144">hello Container 欄位中指定 hello hello blob 記錄檔的位置，且 hello hello blob 名稱 hello RelativePath 欄位中。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-144">hello location of hello blob log file is specified in hello Container field and hello name of hello blob is in hello RelativePath field.</span></span>  <span data-ttu-id="1cdb3-145">hello AbsolutePath 欄位會指示 hello 位置和名稱 hello 檔案，存在於 hello Azure 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-145">hello AbsolutePath field indicates hello location and name of hello file as it existed on hello Azure virtual machine.</span></span>
* <span data-ttu-id="1cdb3-146">**WADPerformanceCountersTable** - 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="1cdb3-147">**WADWindowsEventLogsTable** – Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="1cdb3-148">**Blobs (英文)**</span><span class="sxs-lookup"><span data-stu-id="1cdb3-148">**Blobs**</span></span>

* <span data-ttu-id="1cdb3-149">**wad 控制項容器**– （僅 SDK 2.4 及先前） 包含控制 hello Azure 診斷的 hello XML 組態檔。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains hello XML configuration files that controls hello Azure diagnostics .</span></span>
* <span data-ttu-id="1cdb3-150">**wad-iis-failedreqlogfiles** – 包含 IIS 失敗要求記錄檔中的資訊。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="1cdb3-151">**wad-iis-logfiles** – 包含 IIS 記錄檔的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="1cdb3-152">**"custom"** – 自訂容器，根據設定 hello 診斷監視器所監視的目錄。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-152">**"custom"** – A custom container based on configuring directories that are monitored by hello diagnostic monitor.</span></span>  <span data-ttu-id="1cdb3-153">hello 這個 blob 容器的名稱將會在 WADDirectoriesTable 中指定。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-153">hello name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-tooview-diagnostic-data"></a><span data-ttu-id="1cdb3-154">工具 tooview 診斷資料</span><span class="sxs-lookup"><span data-stu-id="1cdb3-154">Tools tooview diagnostic data</span></span>
<span data-ttu-id="1cdb3-155">數個工具都可用 tooview hello 資料之後傳送的 toostorage。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-155">Several tools are available tooview hello data after it is transferred toostorage.</span></span> <span data-ttu-id="1cdb3-156">例如：</span><span class="sxs-lookup"><span data-stu-id="1cdb3-156">For example:</span></span>

* <span data-ttu-id="1cdb3-157">伺服器總管，在 Visual Studio-如果您已安裝 hello Azure Tools for Microsoft Visual Studio，您可以使用 hello Azure 儲存體節點在 伺服器總管 tooview 唯讀 blob 和資料表資料從 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-157">Server Explorer in Visual Studio - If you have installed hello Azure Tools for Microsoft Visual Studio, you can use hello Azure Storage node in Server Explorer tooview read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="1cdb3-158">您可以從您的本機儲存體模擬器帳戶顯示資料，也可以從您為 Azure 建立的儲存體帳戶顯示資料。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="1cdb3-159">如需詳細資訊，請參閱 [使用伺服器總管瀏覽和管理儲存體資源](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="1cdb3-160">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是獨立應用程式，可讓您 tooeasily 使用在 Windows、 OSX 和 Linux 的 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="1cdb3-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction)包含 Azure 診斷管理員可讓您 tooview，下載及管理 hello hello Azure 上執行的應用程式所收集的診斷資料。</span><span class="sxs-lookup"><span data-stu-id="1cdb3-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you tooview, download and manage hello diagnostics data collected by hello applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cdb3-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1cdb3-162">Next Steps</span></span>
[<span data-ttu-id="1cdb3-163">在雲端服務應用程式中使用 Azure 診斷追蹤 hello 流程</span><span class="sxs-lookup"><span data-stu-id="1cdb3-163">Trace hello flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

