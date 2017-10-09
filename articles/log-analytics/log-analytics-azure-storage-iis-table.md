---
title: "aaaUse 中 Azure 記錄分析的事件的 IIS 和資料表儲存體的 blob 儲存體 |Microsoft 文件"
description: "Hello 記錄檔寫入診斷 tootable 儲存體的 Azure 服務或 IIS 記錄檔寫入 tooblob 儲存體，可讀取記錄分析。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="767b2-103">針對 Log Analytics 的事件，使用 IIS 和 Azure 表格儲存體的 Azure blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="767b2-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="767b2-104">記錄分析可讀取 hello 記錄檔中的下列撰寫 tootable 診斷儲存體或 IIS 記錄檔中寫入的 tooblob 儲存體服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="767b2-104">Log Analytics can read hello logs for hello following services that write diagnostics tootable storage or IIS logs written tooblob storage:</span></span>

* <span data-ttu-id="767b2-105">Service Fabric 叢集 (預覽)</span><span class="sxs-lookup"><span data-stu-id="767b2-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="767b2-106">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="767b2-106">Virtual Machines</span></span>
* <span data-ttu-id="767b2-107">Web/背景工作角色</span><span class="sxs-lookup"><span data-stu-id="767b2-107">Web/Worker Roles</span></span>

<span data-ttu-id="767b2-108">您必須先啟用 Azure 診斷，Log Analytics 才能收集這些資源的資料。</span><span class="sxs-lookup"><span data-stu-id="767b2-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="767b2-109">一旦啟用診斷，您可以使用 hello Azure 入口網站或 PowerShell 設定記錄分析 toocollect hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="767b2-109">Once diagnostics are enabled, you can use hello Azure portal or PowerShell configure Log Analytics toocollect hello logs.</span></span>

<span data-ttu-id="767b2-110">Azure 診斷是 Azure 擴充功能，可讓您從背景工作角色、 web 角色或在 Azure 中執行的虛擬機器的 toocollect 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="767b2-110">Azure Diagnostics is an Azure extension that enables you toocollect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="767b2-111">hello 資料儲存在 Azure 儲存體帳戶，然後可以記錄分析所收集。</span><span class="sxs-lookup"><span data-stu-id="767b2-111">hello data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="767b2-112">記錄分析 toocollect 的 Azure 診斷記錄檔，hello 記錄檔必須位於下列位置的 hello:</span><span class="sxs-lookup"><span data-stu-id="767b2-112">For Log Analytics toocollect these Azure Diagnostics logs, hello logs must be in hello following locations:</span></span>

| <span data-ttu-id="767b2-113">記錄類型</span><span class="sxs-lookup"><span data-stu-id="767b2-113">Log Type</span></span> | <span data-ttu-id="767b2-114">資源類型</span><span class="sxs-lookup"><span data-stu-id="767b2-114">Resource Type</span></span> | <span data-ttu-id="767b2-115">位置</span><span class="sxs-lookup"><span data-stu-id="767b2-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="767b2-116">IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="767b2-116">IIS logs</span></span> |<span data-ttu-id="767b2-117">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="767b2-117">Virtual Machines</span></span> <br> <span data-ttu-id="767b2-118">Web 角色</span><span class="sxs-lookup"><span data-stu-id="767b2-118">Web roles</span></span> <br> <span data-ttu-id="767b2-119">背景工作角色</span><span class="sxs-lookup"><span data-stu-id="767b2-119">Worker roles</span></span> |<span data-ttu-id="767b2-120">wad-iis-logfiles (Blob 儲存體)</span><span class="sxs-lookup"><span data-stu-id="767b2-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="767b2-121">syslog</span><span class="sxs-lookup"><span data-stu-id="767b2-121">Syslog</span></span> |<span data-ttu-id="767b2-122">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="767b2-122">Virtual Machines</span></span> |<span data-ttu-id="767b2-123">LinuxsyslogVer2v0 (表格儲存體)</span><span class="sxs-lookup"><span data-stu-id="767b2-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="767b2-124">Service Fabric 運作事件</span><span class="sxs-lookup"><span data-stu-id="767b2-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="767b2-125">Service Fabric 節點</span><span class="sxs-lookup"><span data-stu-id="767b2-125">Service Fabric nodes</span></span> |<span data-ttu-id="767b2-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="767b2-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="767b2-127">Service Fabric Reliable Actor 事件</span><span class="sxs-lookup"><span data-stu-id="767b2-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="767b2-128">Service Fabric 節點</span><span class="sxs-lookup"><span data-stu-id="767b2-128">Service Fabric nodes</span></span> |<span data-ttu-id="767b2-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="767b2-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="767b2-130">Service Fabric Reliable Service 事件</span><span class="sxs-lookup"><span data-stu-id="767b2-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="767b2-131">Service Fabric 節點</span><span class="sxs-lookup"><span data-stu-id="767b2-131">Service Fabric nodes</span></span> |<span data-ttu-id="767b2-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="767b2-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="767b2-133">Windows 事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="767b2-133">Windows Event logs</span></span> |<span data-ttu-id="767b2-134">Service Fabric 節點</span><span class="sxs-lookup"><span data-stu-id="767b2-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="767b2-135">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="767b2-135">Virtual Machines</span></span> <br> <span data-ttu-id="767b2-136">Web 角色</span><span class="sxs-lookup"><span data-stu-id="767b2-136">Web roles</span></span> <br> <span data-ttu-id="767b2-137">背景工作角色</span><span class="sxs-lookup"><span data-stu-id="767b2-137">Worker roles</span></span> |<span data-ttu-id="767b2-138">WADWindowsEventLogsTable (表格儲存體)</span><span class="sxs-lookup"><span data-stu-id="767b2-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="767b2-139">Windows ETW 記錄檔</span><span class="sxs-lookup"><span data-stu-id="767b2-139">Windows ETW logs</span></span> |<span data-ttu-id="767b2-140">Service Fabric 節點</span><span class="sxs-lookup"><span data-stu-id="767b2-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="767b2-141">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="767b2-141">Virtual Machines</span></span> <br> <span data-ttu-id="767b2-142">Web 角色</span><span class="sxs-lookup"><span data-stu-id="767b2-142">Web roles</span></span> <br> <span data-ttu-id="767b2-143">背景工作角色</span><span class="sxs-lookup"><span data-stu-id="767b2-143">Worker roles</span></span> |<span data-ttu-id="767b2-144">WADETWEventTable (表格儲存體)</span><span class="sxs-lookup"><span data-stu-id="767b2-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="767b2-145">的 IIS 記錄檔，以啟用額外的見解。</span><span class="sxs-lookup"><span data-stu-id="767b2-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="767b2-146">虛擬機器，您可以選擇安裝 hello hello 選項[記錄分析代理程式](log-analytics-azure-vm-extension.md)到您的虛擬機器 tooenable 額外的見解。</span><span class="sxs-lookup"><span data-stu-id="767b2-146">For virtual machines, you have hello option of installing hello [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine tooenable additional insights.</span></span> <span data-ttu-id="767b2-147">此外 toobeing 無法 tooanalyze IIS 記錄檔和事件記錄檔，您可以執行其他分析，包括組態變更追蹤、 SQL 評估及更新評估。</span><span class="sxs-lookup"><span data-stu-id="767b2-147">In addition toobeing able tooanalyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="767b2-148">為事件記錄檔和 IIS 記錄檔集合啟用虛擬機器中的 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="767b2-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="767b2-149">使用下列程序 tooenable 中虛擬機器的 Azure 診斷，為事件記錄檔和 IIS 記錄檔集合使用 hello Microsoft Azure 入口網站的 hello。</span><span class="sxs-lookup"><span data-stu-id="767b2-149">Use hello following procedure tooenable Azure diagnostics in a virtual machine for Event Log and IIS log collection using hello Microsoft Azure portal.</span></span>

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="767b2-150">tooenable hello Azure 入口網站與虛擬機器中的 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="767b2-150">tooenable Azure diagnostics in a virtual machine with hello Azure portal</span></span>
1. <span data-ttu-id="767b2-151">當您建立虛擬機器時，請安裝 hello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="767b2-151">Install hello VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="767b2-152">如果 hello 虛擬機器已存在，請確認已安裝 VM 代理程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="767b2-152">If hello virtual machine already exists, verify that hello VM Agent is already installed.</span></span>

   * <span data-ttu-id="767b2-153">在 hello Azure 入口網站，瀏覽 toohello 虛擬機器，選取**選擇性組態**，然後**診斷**並設定**狀態**太**上**.</span><span class="sxs-lookup"><span data-stu-id="767b2-153">In hello Azure portal, navigate toohello virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** too**On**.</span></span>

     <span data-ttu-id="767b2-154">完成時，hello VM 有 hello Azure 診斷擴充功能安裝並執行。</span><span class="sxs-lookup"><span data-stu-id="767b2-154">Upon completion, hello VM has hello Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="767b2-155">此擴充功能會負責收集您的診斷資料。</span><span class="sxs-lookup"><span data-stu-id="767b2-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="767b2-156">在現有的 VM 上啟用監視和設定事件記錄。</span><span class="sxs-lookup"><span data-stu-id="767b2-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="767b2-157">您可以啟用診斷在 hello VM 層級。</span><span class="sxs-lookup"><span data-stu-id="767b2-157">You can enable diagnostics at hello VM level.</span></span> <span data-ttu-id="767b2-158">tooenable 診斷然後設定事件記錄，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="767b2-158">tooenable diagnostics and then configure event logging, perform hello following steps:</span></span>

   1. <span data-ttu-id="767b2-159">選取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="767b2-159">Select hello VM.</span></span>
   2. <span data-ttu-id="767b2-160">按一下 [監視] 。</span><span class="sxs-lookup"><span data-stu-id="767b2-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="767b2-161">按一下 [診斷] 。</span><span class="sxs-lookup"><span data-stu-id="767b2-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="767b2-162">設定 hello**狀態**太**ON**。</span><span class="sxs-lookup"><span data-stu-id="767b2-162">Set hello **Status** too**ON**.</span></span>
   5. <span data-ttu-id="767b2-163">選取您想 toocollect 每個診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="767b2-163">Select each diagnostics log that you want toocollect.</span></span>
   6. <span data-ttu-id="767b2-164">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="767b2-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="767b2-165">在 Web 角色中針對 IIS 記錄檔和事件集合啟用 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="767b2-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="767b2-166">請參閱太[如何 tooEnable 雲端服務中的診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)如需啟用 Azure 診斷功能的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="767b2-166">Refer too[How tooEnable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="767b2-167">下列 hello 指示使用這項資訊和自訂用於記錄分析。</span><span class="sxs-lookup"><span data-stu-id="767b2-167">hello instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="767b2-168">啟用 Azure 診斷時：</span><span class="sxs-lookup"><span data-stu-id="767b2-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="767b2-169">根據預設，會儲存 IIS 記錄檔，與在 hello scheduledTransferPeriod 傳輸間隔傳輸記錄資料。</span><span class="sxs-lookup"><span data-stu-id="767b2-169">IIS logs are stored by default, with log data transferred at hello scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="767b2-170">預設不會傳輸 Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="767b2-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="tooenable-diagnostics"></a><span data-ttu-id="767b2-171">tooenable 診斷</span><span class="sxs-lookup"><span data-stu-id="767b2-171">tooenable diagnostics</span></span>
<span data-ttu-id="767b2-172">tooenable Windows 事件記錄檔或 toochange hello scheduledTransferPeriod，請使用來設定 Azure 診斷 hello XML 組態檔 (diagnostics.wadcfg)，如中所示[步驟 4： 建立您的診斷組態檔並安裝 hello擴充功能](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="767b2-172">tooenable Windows Event Logs, or toochange hello scheduledTransferPeriod, configure Azure Diagnostics using hello XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="767b2-173">hello 下列範例組態檔會收集 IIS 記錄檔和所有 hello 應用程式中的事件和系統記錄檔：</span><span class="sxs-lookup"><span data-stu-id="767b2-173">hello following example configuration file collects IIS Logs and all Events from hello Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="767b2-174">請確定您的 ConfigurationSettings 會指定儲存體帳戶，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="767b2-174">Ensure that your ConfigurationSettings specifies a storage account, as in hello following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="767b2-175">hello **AccountName**和**AccountKey**值中找到 hello hello 儲存體帳戶儀表板中，在管理存取金鑰 底下的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="767b2-175">hello **AccountName** and **AccountKey** values are found in hello Azure portal in hello storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="767b2-176">hello hello 連接字串的通訊協定必須為**https**。</span><span class="sxs-lookup"><span data-stu-id="767b2-176">hello protocol for hello connection string must be **https**.</span></span>

<span data-ttu-id="767b2-177">一旦 hello 更新診斷組態套用 tooyour 雲端服務和它正在寫入診斷 tooAzure 存放裝置，則您必須準備好 tooconfigure 記錄分析。</span><span class="sxs-lookup"><span data-stu-id="767b2-177">Once hello updated diagnostic configuration is applied tooyour cloud service and it is writing diagnostics tooAzure Storage, then you are ready tooconfigure Log Analytics.</span></span>

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a><span data-ttu-id="767b2-178">使用 Azure 儲存體中的 hello Azure 入口網站 toocollect 記錄檔</span><span class="sxs-lookup"><span data-stu-id="767b2-178">Use hello Azure portal toocollect logs from Azure Storage</span></span>
<span data-ttu-id="767b2-179">您可以使用下列 Azure 服務的 hello hello Azure 入口網站 tooconfigure 記錄分析 toocollect hello 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="767b2-179">You can use hello Azure portal tooconfigure Log Analytics toocollect hello logs for hello following Azure services:</span></span>

* <span data-ttu-id="767b2-180">Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="767b2-180">Service Fabric clusters</span></span>
* <span data-ttu-id="767b2-181">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="767b2-181">Virtual Machines</span></span>
* <span data-ttu-id="767b2-182">Web/背景工作角色</span><span class="sxs-lookup"><span data-stu-id="767b2-182">Web/Worker Roles</span></span>

<span data-ttu-id="767b2-183">在 hello Azure 入口網站，瀏覽 tooyour 記錄分析工作區，並執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="767b2-183">In hello Azure portal, navigate tooyour Log Analytics workspace and perform hello following tasks:</span></span>

1. <span data-ttu-id="767b2-184">按一下 [儲存體帳戶記錄]</span><span class="sxs-lookup"><span data-stu-id="767b2-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="767b2-185">按一下 hello*新增*工作</span><span class="sxs-lookup"><span data-stu-id="767b2-185">Click hello *Add* task</span></span>
3. <span data-ttu-id="767b2-186">選取包含 hello 診斷記錄檔的 hello 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="767b2-186">Select hello Storage account that contains hello diagnostics logs</span></span>
   * <span data-ttu-id="767b2-187">這可以是傳統儲存體帳戶或 Azure Resource Manager 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="767b2-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="767b2-188">選取 hello 想 toocollect 記錄檔中的資料類型</span><span class="sxs-lookup"><span data-stu-id="767b2-188">Select hello Data Type you want toocollect logs for</span></span>
   * <span data-ttu-id="767b2-189">hello 選項包括 IIS 記錄檔。事件。Syslog (Linux);ETW 記錄檔。Service Fabric 事件</span><span class="sxs-lookup"><span data-stu-id="767b2-189">hello choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="767b2-190">根據資料類型，而且無法變更的 hello 自動填入來源 hello 值</span><span class="sxs-lookup"><span data-stu-id="767b2-190">hello value for Source is automatically populated based on hello data type and cannot be changed</span></span>
6. <span data-ttu-id="767b2-191">按一下 [確定] toosave hello 組態</span><span class="sxs-lookup"><span data-stu-id="767b2-191">Click OK toosave hello configuration</span></span>

<span data-ttu-id="767b2-192">針對您想記錄分析 toocollect 額外的儲存體帳戶和資料類型重複步驟 2-6。</span><span class="sxs-lookup"><span data-stu-id="767b2-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics toocollect.</span></span>

<span data-ttu-id="767b2-193">在大約 30 分鐘內，您就可以 toosee hello 記錄分析儲存體帳戶的資料。</span><span class="sxs-lookup"><span data-stu-id="767b2-193">In approximately 30 minutes, you are able toosee data from hello storage account in Log Analytics.</span></span> <span data-ttu-id="767b2-194">您只會看到寫入 toostorage 套用 hello 設定後的資料。</span><span class="sxs-lookup"><span data-stu-id="767b2-194">You will only see data that is written toostorage after hello configuration is applied.</span></span> <span data-ttu-id="767b2-195">記錄分析不會從 hello 儲存體帳戶讀取 hello 預先存在的資料。</span><span class="sxs-lookup"><span data-stu-id="767b2-195">Log Analytics does not read hello pre-existing data from hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="767b2-196">hello 入口網站不會驗證該來源存在 hello 儲存體帳戶中的 hello，或如果正在寫入新的資料。</span><span class="sxs-lookup"><span data-stu-id="767b2-196">hello portal does not validate that hello Source exists in hello storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="767b2-197">在虛擬機器中使用 PowerShell 來啟用 Azure 診斷以收集事件記錄檔和 IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="767b2-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="767b2-198">中的步驟使用 hello[設定記錄分析 tooindex Azure 診斷](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics)toouse PowerShell tooread 來自 Azure 診斷寫入 tootable 儲存體。</span><span class="sxs-lookup"><span data-stu-id="767b2-198">Use hello steps in [Configuring Log Analytics tooindex Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread from Azure diagnostics that are written tootable storage.</span></span>

<span data-ttu-id="767b2-199">使用 Azure PowerShell 您可以更精確地指定寫入 tooAzure 儲存體的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="767b2-199">Using Azure PowerShell you can more precisely specify hello events that are written tooAzure Storage.</span></span>
<span data-ttu-id="767b2-200">如需詳細資訊，請參閱[在 Azure 虛擬機器中啟用診斷](../virtual-machines-dotnet-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="767b2-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="767b2-201">您可以啟用和更新使用下列 PowerShell 指令碼的 hello Azure 診斷。</span><span class="sxs-lookup"><span data-stu-id="767b2-201">You can enable and update Azure diagnostics using hello following PowerShell script.</span></span>
<span data-ttu-id="767b2-202">您也可以搭配使用此指令碼與自訂記錄組態。</span><span class="sxs-lookup"><span data-stu-id="767b2-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="767b2-203">修改 hello 指令碼 tooset hello 儲存體帳戶、 服務名稱和虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="767b2-203">Modify hello script tooset hello storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="767b2-204">hello 指令碼會使用傳統的虛擬機器的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="767b2-204">hello script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="767b2-205">檢閱下列指令碼範例的 hello、 複製它、 視需要修改它、 hello 範例儲存為 PowerShell 指令碼檔案，然後再執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="767b2-205">Review hello following script sample, copy it, modify it as needed, save hello sample as a PowerShell script file, and then run hello script.</span></span>

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="767b2-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="767b2-206">Next steps</span></span>
* <span data-ttu-id="767b2-207">針對支援的 Azure 服務[收集 Azure 服務的記錄檔與計量](log-analytics-azure-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="767b2-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="767b2-208">[啟用方案](log-analytics-add-solutions.md)tooprovide 深入了解 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="767b2-208">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="767b2-209">[使用搜尋查詢](log-analytics-log-searches.md)tooanalyze hello 資料。</span><span class="sxs-lookup"><span data-stu-id="767b2-209">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>
