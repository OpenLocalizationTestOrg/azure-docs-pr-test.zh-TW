---
title: "在 Azure 儲存體中儲存和檢視診斷資料 | Microsoft Docs"
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
ms.openlocfilehash: 374cc179e13c00e439415e3df16e0c6d5ccba5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="1b69b-103">在 Azure 儲存體中儲存和檢視診斷資料</span><span class="sxs-lookup"><span data-stu-id="1b69b-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="1b69b-104">除非您將診斷資料傳輸至 Microsoft Azure 儲存體模擬器或 Azure 儲存體，否則不會永久儲存診斷資料。</span><span class="sxs-lookup"><span data-stu-id="1b69b-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="1b69b-105">一旦位於儲存體，即可利用其中一個可用的工具進行檢視。</span><span class="sxs-lookup"><span data-stu-id="1b69b-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="1b69b-106">指定儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1b69b-106">Specify a storage account</span></span>
<span data-ttu-id="1b69b-107">您可指定您要在 ServiceConfiguration.cscfg 檔案中使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b69b-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="1b69b-108">帳戶資訊會定義為組態設定中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="1b69b-108">The account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="1b69b-109">下列範例顯示在 Visual Studio 中為新的雲端服務專案建立的預設連接字串：</span><span class="sxs-lookup"><span data-stu-id="1b69b-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="1b69b-110">您可以變更此連接字串，以提供 Azure 儲存體帳戶的帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="1b69b-110">You can change this connection string to provide account information for an Azure storage account.</span></span>

<span data-ttu-id="1b69b-111">視所收集的診斷資料類型而定，Azure 診斷會使用 Blob 服務或資料表服務。</span><span class="sxs-lookup"><span data-stu-id="1b69b-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span></span> <span data-ttu-id="1b69b-112">下表顯示保存的資料來源以及其格式。</span><span class="sxs-lookup"><span data-stu-id="1b69b-112">The following table shows the data sources that are persisted and their format.</span></span>

| <span data-ttu-id="1b69b-113">資料來源</span><span class="sxs-lookup"><span data-stu-id="1b69b-113">Data source</span></span> | <span data-ttu-id="1b69b-114">儲存體格式</span><span class="sxs-lookup"><span data-stu-id="1b69b-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="1b69b-115">Azure 記錄檔</span><span class="sxs-lookup"><span data-stu-id="1b69b-115">Azure logs</span></span> |<span data-ttu-id="1b69b-116">資料表</span><span class="sxs-lookup"><span data-stu-id="1b69b-116">Table</span></span> |
| <span data-ttu-id="1b69b-117">IIS 7.0 記錄檔</span><span class="sxs-lookup"><span data-stu-id="1b69b-117">IIS 7.0 logs</span></span> |<span data-ttu-id="1b69b-118">Blob</span><span class="sxs-lookup"><span data-stu-id="1b69b-118">Blob</span></span> |
| <span data-ttu-id="1b69b-119">Azure 診斷基礎結構記錄檔</span><span class="sxs-lookup"><span data-stu-id="1b69b-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="1b69b-120">資料表</span><span class="sxs-lookup"><span data-stu-id="1b69b-120">Table</span></span> |
| <span data-ttu-id="1b69b-121">失敗要求追蹤記錄檔</span><span class="sxs-lookup"><span data-stu-id="1b69b-121">Failed Request Trace logs</span></span> |<span data-ttu-id="1b69b-122">Blob</span><span class="sxs-lookup"><span data-stu-id="1b69b-122">Blob</span></span> |
| <span data-ttu-id="1b69b-123">Windows 事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="1b69b-123">Windows Event logs</span></span> |<span data-ttu-id="1b69b-124">資料表</span><span class="sxs-lookup"><span data-stu-id="1b69b-124">Table</span></span> |
| <span data-ttu-id="1b69b-125">效能計數器</span><span class="sxs-lookup"><span data-stu-id="1b69b-125">Performance counters</span></span> |<span data-ttu-id="1b69b-126">資料表</span><span class="sxs-lookup"><span data-stu-id="1b69b-126">Table</span></span> |
| <span data-ttu-id="1b69b-127">損毀傾印</span><span class="sxs-lookup"><span data-stu-id="1b69b-127">Crash dumps</span></span> |<span data-ttu-id="1b69b-128">Blob</span><span class="sxs-lookup"><span data-stu-id="1b69b-128">Blob</span></span> |
| <span data-ttu-id="1b69b-129">自訂錯誤記錄檔</span><span class="sxs-lookup"><span data-stu-id="1b69b-129">Custom error logs</span></span> |<span data-ttu-id="1b69b-130">Blob</span><span class="sxs-lookup"><span data-stu-id="1b69b-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="1b69b-131">傳輸診斷資料</span><span class="sxs-lookup"><span data-stu-id="1b69b-131">Transfer diagnostic data</span></span>
<span data-ttu-id="1b69b-132">若為 SDK 2.5 和更新版本，可以透過組態檔進行傳輸診斷資料的要求。</span><span class="sxs-lookup"><span data-stu-id="1b69b-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span></span> <span data-ttu-id="1b69b-133">您可以依照組態中指定的排程間隔來傳輸診斷資料。</span><span class="sxs-lookup"><span data-stu-id="1b69b-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span></span>

<span data-ttu-id="1b69b-134">若為 SDK 2.4 和更舊版本，您可以透過組態檔以及程式設計方式要求傳輸診斷資料。</span><span class="sxs-lookup"><span data-stu-id="1b69b-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span></span> <span data-ttu-id="1b69b-135">程式設計的方式也可讓您進行隨選傳輸。</span><span class="sxs-lookup"><span data-stu-id="1b69b-135">The programmatic approach also allows you to do on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b69b-136">當您將診斷資料傳輸至 Azure 儲存體帳戶時，您的診斷資料所用的儲存體資源就會發生成本。</span><span class="sxs-lookup"><span data-stu-id="1b69b-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="1b69b-137">儲存診斷資料</span><span class="sxs-lookup"><span data-stu-id="1b69b-137">Store diagnostic data</span></span>
<span data-ttu-id="1b69b-138">記錄檔資料會以下列名稱儲存在 Blob 或資料表儲存體中：</span><span class="sxs-lookup"><span data-stu-id="1b69b-138">Log data is stored in either Blob or Table storage with the following names:</span></span>

<span data-ttu-id="1b69b-139">**資料表 (英文)**</span><span class="sxs-lookup"><span data-stu-id="1b69b-139">**Tables**</span></span>

* <span data-ttu-id="1b69b-140">**WadLogsTable** - 使用追蹤接聽程式在程式碼中寫入的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1b69b-140">**WadLogsTable** - Logs written in code using the trace listener.</span></span>
* <span data-ttu-id="1b69b-141">**WADDiagnosticInfrastructureLogsTable** - 診斷監視器和組態變更。</span><span class="sxs-lookup"><span data-stu-id="1b69b-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="1b69b-142">**WADDirectoriesTable** – 診斷監視器所監視的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b69b-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="1b69b-143">這包括 IIS 記錄檔、IIS 失敗要求記錄檔和自訂目錄。</span><span class="sxs-lookup"><span data-stu-id="1b69b-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="1b69b-144">Blob 記錄檔的位置是在 [容器] 欄位中指定，而 Blob 的名稱則是在 RelativePath 欄位中指定。</span><span class="sxs-lookup"><span data-stu-id="1b69b-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span></span>  <span data-ttu-id="1b69b-145">AbsolutePath 欄位會指出檔案存在於 Azure 虛擬機器上的位置和名稱。</span><span class="sxs-lookup"><span data-stu-id="1b69b-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span></span>
* <span data-ttu-id="1b69b-146">**WADPerformanceCountersTable** - 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="1b69b-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="1b69b-147">**WADWindowsEventLogsTable** – Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1b69b-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="1b69b-148">**Blobs (英文)**</span><span class="sxs-lookup"><span data-stu-id="1b69b-148">**Blobs**</span></span>

* <span data-ttu-id="1b69b-149">**wad-control-container** – (僅適用於 SDK 2.4 和前一版) 包含可控制 Azure 診斷的 XML 組態檔。</span><span class="sxs-lookup"><span data-stu-id="1b69b-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span></span>
* <span data-ttu-id="1b69b-150">**wad-iis-failedreqlogfiles** – 包含 IIS 失敗要求記錄檔中的資訊。</span><span class="sxs-lookup"><span data-stu-id="1b69b-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="1b69b-151">**wad-iis-logfiles** – 包含 IIS 記錄檔的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1b69b-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="1b69b-152">**"custom"** – 自訂容器，該容器是以設定診斷監視器所監視的目錄為基礎。</span><span class="sxs-lookup"><span data-stu-id="1b69b-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span></span>  <span data-ttu-id="1b69b-153">將會在 WADDirectoriesTable 中指定此 Blob 容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="1b69b-153">The name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-to-view-diagnostic-data"></a><span data-ttu-id="1b69b-154">用來檢視診斷資料的工具</span><span class="sxs-lookup"><span data-stu-id="1b69b-154">Tools to view diagnostic data</span></span>
<span data-ttu-id="1b69b-155">有數個工具可用來檢視傳輸至儲存體後的資料。</span><span class="sxs-lookup"><span data-stu-id="1b69b-155">Several tools are available to view the data after it is transferred to storage.</span></span> <span data-ttu-id="1b69b-156">例如：</span><span class="sxs-lookup"><span data-stu-id="1b69b-156">For example:</span></span>

* <span data-ttu-id="1b69b-157">Visual Studio 中的伺服器總管 - 如果您已安裝 Azure Tools for Microsoft Visual Studio，您可以在伺服器總管中使用 Azure 儲存體節點，從您的 Azure 儲存體帳戶檢視唯讀的 Blob 和資料表資料。</span><span class="sxs-lookup"><span data-stu-id="1b69b-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="1b69b-158">您可以從您的本機儲存體模擬器帳戶顯示資料，也可以從您為 Azure 建立的儲存體帳戶顯示資料。</span><span class="sxs-lookup"><span data-stu-id="1b69b-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="1b69b-159">如需詳細資訊，請參閱 [使用伺服器總管瀏覽和管理儲存體資源](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="1b69b-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="1b69b-160">[Microsoft Azure 儲存體 Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個獨立應用程式，可讓您在 Windows、OSX 和 Linux 上輕鬆使用 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="1b69b-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="1b69b-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) 包含 Azure 診斷管理員，可讓您檢視、下載及管理在 Azure 上執行的應用程式所收集的診斷資料。</span><span class="sxs-lookup"><span data-stu-id="1b69b-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b69b-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b69b-162">Next Steps</span></span>
[<span data-ttu-id="1b69b-163">使用 Azure 診斷追蹤雲端服務應用程式中的流程</span><span class="sxs-lookup"><span data-stu-id="1b69b-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

