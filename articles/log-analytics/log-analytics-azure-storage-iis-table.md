---
title: "對 IIS 使用 Blob 儲存體，對 Azure Log Analytics 中的事件使用表格儲存體 | Microsoft Docs"
description: "Log Analytics 可以讀取 Azure 服務 (將診斷寫入表格儲存體) 的記錄，或讀取寫入 Blob 儲存體的 IIS 記錄。"
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
ms.openlocfilehash: 459ef90ca1d76bada6565bfefd7b4bd1086197d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="69c0d-103">針對 Log Analytics 的事件，使用 IIS 和 Azure 表格儲存體的 Azure blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="69c0d-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="69c0d-104">Log Analytics 可以讀取下列服務 (將診斷寫入表格儲存體) 的記錄，或讀取寫入 Blob 儲存體的 IIS 記錄：</span><span class="sxs-lookup"><span data-stu-id="69c0d-104">Log Analytics can read the logs for the following services that write diagnostics to table storage or IIS logs written to blob storage:</span></span>

* <span data-ttu-id="69c0d-105">Service Fabric 叢集 (預覽)</span><span class="sxs-lookup"><span data-stu-id="69c0d-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="69c0d-106">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="69c0d-106">Virtual Machines</span></span>
* <span data-ttu-id="69c0d-107">Web/背景工作角色</span><span class="sxs-lookup"><span data-stu-id="69c0d-107">Web/Worker Roles</span></span>

<span data-ttu-id="69c0d-108">您必須先啟用 Azure 診斷，Log Analytics 才能收集這些資源的資料。</span><span class="sxs-lookup"><span data-stu-id="69c0d-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="69c0d-109">啟用診斷之後，您可以使用 Azure 入口網站或 PowerShell，設定 Log Analytics 來收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="69c0d-109">Once diagnostics are enabled, you can use the Azure portal or PowerShell configure Log Analytics to collect the logs.</span></span>

<span data-ttu-id="69c0d-110">Azure 診斷是 Azure 的擴充功能，可讓您從背景工作角色、Web 角色或 Azure 中執行的虛擬機器收集診斷資料。</span><span class="sxs-lookup"><span data-stu-id="69c0d-110">Azure Diagnostics is an Azure extension that enables you to collect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="69c0d-111">資料會儲存在 Azure 儲存體帳戶中，接著可由 Log Analytics 收集。</span><span class="sxs-lookup"><span data-stu-id="69c0d-111">The data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="69c0d-112">若要讓 Log Analytics 收集這些 Azure 診斷記錄，記錄檔必須位於下列位置：</span><span class="sxs-lookup"><span data-stu-id="69c0d-112">For Log Analytics to collect these Azure Diagnostics logs, the logs must be in the following locations:</span></span>

| <span data-ttu-id="69c0d-113">記錄類型</span><span class="sxs-lookup"><span data-stu-id="69c0d-113">Log Type</span></span> | <span data-ttu-id="69c0d-114">資源類型</span><span class="sxs-lookup"><span data-stu-id="69c0d-114">Resource Type</span></span> | <span data-ttu-id="69c0d-115">位置</span><span class="sxs-lookup"><span data-stu-id="69c0d-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69c0d-116">IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="69c0d-116">IIS logs</span></span> |<span data-ttu-id="69c0d-117">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="69c0d-117">Virtual Machines</span></span> <br> <span data-ttu-id="69c0d-118">Web 角色</span><span class="sxs-lookup"><span data-stu-id="69c0d-118">Web roles</span></span> <br> <span data-ttu-id="69c0d-119">背景工作角色</span><span class="sxs-lookup"><span data-stu-id="69c0d-119">Worker roles</span></span> |<span data-ttu-id="69c0d-120">wad-iis-logfiles (Blob 儲存體)</span><span class="sxs-lookup"><span data-stu-id="69c0d-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="69c0d-121">syslog</span><span class="sxs-lookup"><span data-stu-id="69c0d-121">Syslog</span></span> |<span data-ttu-id="69c0d-122">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="69c0d-122">Virtual Machines</span></span> |<span data-ttu-id="69c0d-123">LinuxsyslogVer2v0 (表格儲存體)</span><span class="sxs-lookup"><span data-stu-id="69c0d-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="69c0d-124">Service Fabric 運作事件</span><span class="sxs-lookup"><span data-stu-id="69c0d-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="69c0d-125">Service Fabric 節點</span><span class="sxs-lookup"><span data-stu-id="69c0d-125">Service Fabric nodes</span></span> |<span data-ttu-id="69c0d-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="69c0d-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="69c0d-127">Service Fabric Reliable Actor 事件</span><span class="sxs-lookup"><span data-stu-id="69c0d-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="69c0d-128">Service Fabric 節點</span><span class="sxs-lookup"><span data-stu-id="69c0d-128">Service Fabric nodes</span></span> |<span data-ttu-id="69c0d-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="69c0d-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="69c0d-130">Service Fabric Reliable Service 事件</span><span class="sxs-lookup"><span data-stu-id="69c0d-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="69c0d-131">Service Fabric 節點</span><span class="sxs-lookup"><span data-stu-id="69c0d-131">Service Fabric nodes</span></span> |<span data-ttu-id="69c0d-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="69c0d-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="69c0d-133">Windows 事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="69c0d-133">Windows Event logs</span></span> |<span data-ttu-id="69c0d-134">Service Fabric 節點</span><span class="sxs-lookup"><span data-stu-id="69c0d-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="69c0d-135">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="69c0d-135">Virtual Machines</span></span> <br> <span data-ttu-id="69c0d-136">Web 角色</span><span class="sxs-lookup"><span data-stu-id="69c0d-136">Web roles</span></span> <br> <span data-ttu-id="69c0d-137">背景工作角色</span><span class="sxs-lookup"><span data-stu-id="69c0d-137">Worker roles</span></span> |<span data-ttu-id="69c0d-138">WADWindowsEventLogsTable (表格儲存體)</span><span class="sxs-lookup"><span data-stu-id="69c0d-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="69c0d-139">Windows ETW 記錄檔</span><span class="sxs-lookup"><span data-stu-id="69c0d-139">Windows ETW logs</span></span> |<span data-ttu-id="69c0d-140">Service Fabric 節點</span><span class="sxs-lookup"><span data-stu-id="69c0d-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="69c0d-141">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="69c0d-141">Virtual Machines</span></span> <br> <span data-ttu-id="69c0d-142">Web 角色</span><span class="sxs-lookup"><span data-stu-id="69c0d-142">Web roles</span></span> <br> <span data-ttu-id="69c0d-143">背景工作角色</span><span class="sxs-lookup"><span data-stu-id="69c0d-143">Worker roles</span></span> |<span data-ttu-id="69c0d-144">WADETWEventTable (表格儲存體)</span><span class="sxs-lookup"><span data-stu-id="69c0d-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="69c0d-145">的 IIS 記錄檔，以啟用額外的見解。</span><span class="sxs-lookup"><span data-stu-id="69c0d-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="69c0d-146">若為虛擬機器，您可以選擇將 [Log Analytics agent](log-analytics-azure-vm-extension.md) 安裝到虛擬機器中以啟用其他見解。</span><span class="sxs-lookup"><span data-stu-id="69c0d-146">For virtual machines, you have the option of installing the [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine to enable additional insights.</span></span> <span data-ttu-id="69c0d-147">除了分析 IIS 記錄檔和事件記錄檔之外，您也可以執行其他分析，包括組態變更追蹤、SQL 評估及更新評估。</span><span class="sxs-lookup"><span data-stu-id="69c0d-147">In addition to being able to analyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="69c0d-148">為事件記錄檔和 IIS 記錄檔集合啟用虛擬機器中的 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="69c0d-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="69c0d-149">您可以搭配使用下列程序與 Microsoft Azure 入口網站，為事件記錄檔和 IIS 記錄檔集合啟用虛擬機器中的 Azure 診斷。</span><span class="sxs-lookup"><span data-stu-id="69c0d-149">Use the following procedure to enable Azure diagnostics in a virtual machine for Event Log and IIS log collection using the Microsoft Azure portal.</span></span>

### <a name="to-enable-azure-diagnostics-in-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="69c0d-150">使用 Azure 入口網站啟用虛擬機器中的 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="69c0d-150">To enable Azure diagnostics in a virtual machine with the Azure portal</span></span>
1. <span data-ttu-id="69c0d-151">建立虛擬機器時安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="69c0d-151">Install the VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="69c0d-152">如果虛擬機器已經存在，請確認已安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="69c0d-152">If the virtual machine already exists, verify that the VM Agent is already installed.</span></span>

   * <span data-ttu-id="69c0d-153">在 Azure 入口網站中，瀏覽至虛擬機器，依序選取 [選擇性組態] 及 [診斷]，並將 [狀態] 設為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="69c0d-153">In the Azure portal, navigate to the virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** to **On**.</span></span>

     <span data-ttu-id="69c0d-154">完成時，VM 中就會安裝好 Azure 診斷擴充功能並執行。</span><span class="sxs-lookup"><span data-stu-id="69c0d-154">Upon completion, the VM has the Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="69c0d-155">此擴充功能會負責收集您的診斷資料。</span><span class="sxs-lookup"><span data-stu-id="69c0d-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="69c0d-156">在現有的 VM 上啟用監視和設定事件記錄。</span><span class="sxs-lookup"><span data-stu-id="69c0d-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="69c0d-157">您可以在 VM 層級上啟用診斷。</span><span class="sxs-lookup"><span data-stu-id="69c0d-157">You can enable diagnostics at the VM level.</span></span> <span data-ttu-id="69c0d-158">若要啟用診斷然後設定事件記錄，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="69c0d-158">To enable diagnostics and then configure event logging, perform the following steps:</span></span>

   1. <span data-ttu-id="69c0d-159">選取 VM。</span><span class="sxs-lookup"><span data-stu-id="69c0d-159">Select the VM.</span></span>
   2. <span data-ttu-id="69c0d-160">按一下 [監視] 。</span><span class="sxs-lookup"><span data-stu-id="69c0d-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="69c0d-161">按一下 [診斷] 。</span><span class="sxs-lookup"><span data-stu-id="69c0d-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="69c0d-162">將 [狀態] 設為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="69c0d-162">Set the **Status** to **ON**.</span></span>
   5. <span data-ttu-id="69c0d-163">選取您想要收集的每個診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="69c0d-163">Select each diagnostics log that you want to collect.</span></span>
   6. <span data-ttu-id="69c0d-164">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="69c0d-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="69c0d-165">在 Web 角色中針對 IIS 記錄檔和事件集合啟用 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="69c0d-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="69c0d-166">請參閱[如何在雲端服務中啟用診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)瞭解啟用 Azure 診斷的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="69c0d-166">Refer to [How To Enable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="69c0d-167">下面的指示會使用此資訊並自訂它來與 Log Analytics 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="69c0d-167">The instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="69c0d-168">啟用 Azure 診斷時：</span><span class="sxs-lookup"><span data-stu-id="69c0d-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="69c0d-169">預設會儲存 IIS 記錄檔，並在 scheduledTransferPeriod 傳輸間隔傳輸記錄檔資料。</span><span class="sxs-lookup"><span data-stu-id="69c0d-169">IIS logs are stored by default, with log data transferred at the scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="69c0d-170">預設不會傳輸 Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="69c0d-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="to-enable-diagnostics"></a><span data-ttu-id="69c0d-171">啟用診斷</span><span class="sxs-lookup"><span data-stu-id="69c0d-171">To enable diagnostics</span></span>
<span data-ttu-id="69c0d-172">若要啟用 Windows 事件記錄檔，或是變更 scheduledTransferPeriod，請使用 XML 組態檔 (diagnostics.wadcfg) 設定 Azure 診斷，如[步驟 4：建立您的診斷組態檔並安裝擴充功能](../cloud-services/cloud-services-dotnet-diagnostics.md)所示</span><span class="sxs-lookup"><span data-stu-id="69c0d-172">To enable Windows Event Logs, or to change the scheduledTransferPeriod, configure Azure Diagnostics using the XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install the extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="69c0d-173">下列範例組態檔會從應用程式和系統記錄檔中收集 IIS 記錄檔和所有事件：</span><span class="sxs-lookup"><span data-stu-id="69c0d-173">The following example configuration file collects IIS Logs and all Events from the Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant to Web roles -->
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

<span data-ttu-id="69c0d-174">請確定 ConfigurationSettings 指定儲存體帳戶，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="69c0d-174">Ensure that your ConfigurationSettings specifies a storage account, as in the following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="69c0d-175">**AccountName** 和 **AccountKey** 值可在 Azure 入口網站中儲存體帳戶儀表板的 [管理存取金鑰] 底下找到。</span><span class="sxs-lookup"><span data-stu-id="69c0d-175">The **AccountName** and **AccountKey** values are found in the Azure portal in the storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="69c0d-176">連接字串的通訊協定必須為 **https**。</span><span class="sxs-lookup"><span data-stu-id="69c0d-176">The protocol for the connection string must be **https**.</span></span>

<span data-ttu-id="69c0d-177">將更新的診斷組態套用至雲端服務，且該服務已開始將診斷寫入 Azure 儲存體時，您即可設定 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="69c0d-177">Once the updated diagnostic configuration is applied to your cloud service and it is writing diagnostics to Azure Storage, then you are ready to configure Log Analytics.</span></span>

## <a name="use-the-azure-portal-to-collect-logs-from-azure-storage"></a><span data-ttu-id="69c0d-178">使用 Azure 入口網站從 Azure 儲存體收集記錄</span><span class="sxs-lookup"><span data-stu-id="69c0d-178">Use the Azure portal to collect logs from Azure Storage</span></span>
<span data-ttu-id="69c0d-179">您可以使用 Azure 入口網站，設定 Log Analytics 來收集下列 Azure 服務的記錄︰</span><span class="sxs-lookup"><span data-stu-id="69c0d-179">You can use the Azure portal to configure Log Analytics to collect the logs for the following Azure services:</span></span>

* <span data-ttu-id="69c0d-180">Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="69c0d-180">Service Fabric clusters</span></span>
* <span data-ttu-id="69c0d-181">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="69c0d-181">Virtual Machines</span></span>
* <span data-ttu-id="69c0d-182">Web/背景工作角色</span><span class="sxs-lookup"><span data-stu-id="69c0d-182">Web/Worker Roles</span></span>

<span data-ttu-id="69c0d-183">在 Azure 入口網站中，瀏覽至您的 Log Analytics 工作區並執行下列工作︰</span><span class="sxs-lookup"><span data-stu-id="69c0d-183">In the Azure portal, navigate to your Log Analytics workspace and perform the following tasks:</span></span>

1. <span data-ttu-id="69c0d-184">按一下 [儲存體帳戶記錄]</span><span class="sxs-lookup"><span data-stu-id="69c0d-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="69c0d-185">按一下 [新增] 工作</span><span class="sxs-lookup"><span data-stu-id="69c0d-185">Click the *Add* task</span></span>
3. <span data-ttu-id="69c0d-186">選取包含診斷記錄的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="69c0d-186">Select the Storage account that contains the diagnostics logs</span></span>
   * <span data-ttu-id="69c0d-187">這可以是傳統儲存體帳戶或 Azure Resource Manager 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="69c0d-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="69c0d-188">選取您想要收集記錄的資料類型</span><span class="sxs-lookup"><span data-stu-id="69c0d-188">Select the Data Type you want to collect logs for</span></span>
   * <span data-ttu-id="69c0d-189">可以選擇的項目為 IIS 記錄、事件、Syslog (Linux)、ETW 記錄檔、Service Fabric 事件</span><span class="sxs-lookup"><span data-stu-id="69c0d-189">The choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="69c0d-190">「來源」的值會根據資料類型自動填入且無法變更</span><span class="sxs-lookup"><span data-stu-id="69c0d-190">The value for Source is automatically populated based on the data type and cannot be changed</span></span>
6. <span data-ttu-id="69c0d-191">按一下 [確定] 以儲存組態</span><span class="sxs-lookup"><span data-stu-id="69c0d-191">Click OK to save the configuration</span></span>

<span data-ttu-id="69c0d-192">針對您想要 Log Analytics 收集的其他儲存體帳戶及資料類型，重複步驟 2-6。</span><span class="sxs-lookup"><span data-stu-id="69c0d-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics to collect.</span></span>

<span data-ttu-id="69c0d-193">大約 30 分鐘內，您就能夠在 Log Analytics 中看到來自儲存體帳戶的資料。</span><span class="sxs-lookup"><span data-stu-id="69c0d-193">In approximately 30 minutes, you are able to see data from the storage account in Log Analytics.</span></span> <span data-ttu-id="69c0d-194">您只會看到套用組態之後寫入儲存體的資料。</span><span class="sxs-lookup"><span data-stu-id="69c0d-194">You will only see data that is written to storage after the configuration is applied.</span></span> <span data-ttu-id="69c0d-195">Log Analytics 不會從儲存體帳戶讀取預先存在的資料。</span><span class="sxs-lookup"><span data-stu-id="69c0d-195">Log Analytics does not read the pre-existing data from the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="69c0d-196">入口網站不會驗證「來源」是否存在於儲存體帳戶，或是否已寫入新的資料。</span><span class="sxs-lookup"><span data-stu-id="69c0d-196">The portal does not validate that the Source exists in the storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="69c0d-197">在虛擬機器中使用 PowerShell 來啟用 Azure 診斷以收集事件記錄檔和 IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="69c0d-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="69c0d-198">使用[設定 Log Analytics 來為 Azure 診斷編製索引](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) 中的步驟，以使用 PowerShell 從寫入表格儲存體的 Azure 診斷讀取資料。</span><span class="sxs-lookup"><span data-stu-id="69c0d-198">Use the steps in [Configuring Log Analytics to index Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) to use PowerShell to read from Azure diagnostics that are written to table storage.</span></span>

<span data-ttu-id="69c0d-199">您可以使用 Azure PowerShell，更精確地指定寫入至 Azure 儲存體的事件。</span><span class="sxs-lookup"><span data-stu-id="69c0d-199">Using Azure PowerShell you can more precisely specify the events that are written to Azure Storage.</span></span>
<span data-ttu-id="69c0d-200">如需詳細資訊，請參閱[在 Azure 虛擬機器中啟用診斷](../virtual-machines-dotnet-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="69c0d-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="69c0d-201">您可以使用下列 PowerShell 指令碼啟用和更新 Azure 診斷。</span><span class="sxs-lookup"><span data-stu-id="69c0d-201">You can enable and update Azure diagnostics using the following PowerShell script.</span></span>
<span data-ttu-id="69c0d-202">您也可以搭配使用此指令碼與自訂記錄組態。</span><span class="sxs-lookup"><span data-stu-id="69c0d-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="69c0d-203">請修改指令碼來設定儲存體帳戶、服務名稱和虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="69c0d-203">Modify the script to set the storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="69c0d-204">指令碼會使用適用於傳統虛擬機器的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="69c0d-204">The script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="69c0d-205">檢閱下列指令碼範例、複製它、視需要修改它、將範例儲存為 PowerShell 指令碼檔案，然後再執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="69c0d-205">Review the following script sample, copy it, modify it as needed, save the sample as a PowerShell script file, and then run the script.</span></span>

```
    #Connect to Azure
    Add-AzureAccount

    # settings to change:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert to config format

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
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of the extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="69c0d-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69c0d-206">Next steps</span></span>
* <span data-ttu-id="69c0d-207">針對支援的 Azure 服務[收集 Azure 服務的記錄檔與計量](log-analytics-azure-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="69c0d-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="69c0d-208">[啟用解決方案](log-analytics-add-solutions.md) 以提供資料的深入見解。</span><span class="sxs-lookup"><span data-stu-id="69c0d-208">[Enable Solutions](log-analytics-add-solutions.md) to provide insight into the data.</span></span>
* <span data-ttu-id="69c0d-209">[使用搜尋查詢](log-analytics-log-searches.md) 以分析資料。</span><span class="sxs-lookup"><span data-stu-id="69c0d-209">[Use search queries](log-analytics-log-searches.md) to analyze the data.</span></span>
