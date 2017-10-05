---
title: "Azure 診斷 1.0 組態結構描述 | Microsoft Docs"
description: "如果您是搭配 Azure 虛擬機器、虛擬機器擴展集、Service Fabric 或雲端服務使用 Azure SDK 2.4 和以下版本才相關。"
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: a8fdfb52d5091d3fc9779657737c7430fcfada51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="050cc-103">Azure 診斷 1.0 組態結構描述</span><span class="sxs-lookup"><span data-stu-id="050cc-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="050cc-104">Azure 診斷是一種元件，可針對 Azure 虛擬機器、虛擬機器擴展集，Service Fabric 以及雲端服務，收集相關效能計數器和其他統計資料。</span><span class="sxs-lookup"><span data-stu-id="050cc-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="050cc-105">此頁面只在您使用其中一個服務時才相關。</span><span class="sxs-lookup"><span data-stu-id="050cc-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="050cc-106">Azure 診斷要與 Azure 監視器、Application Insights 和 Log Analytics 等其他 Microsoft 診斷產品搭配使用。</span><span class="sxs-lookup"><span data-stu-id="050cc-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="050cc-107">Azure 診斷組態檔會定義用來初始化診斷監視器的值。</span><span class="sxs-lookup"><span data-stu-id="050cc-107">The Azure Diagnostics configuration file defines values that are used to initialize the Diagnostics Monitor.</span></span> <span data-ttu-id="050cc-108">在診斷監視器啟動時，會使用此檔案來初始化診斷組態設定。</span><span class="sxs-lookup"><span data-stu-id="050cc-108">This file is used to initialize diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

 <span data-ttu-id="050cc-109">根據預設，Azure 診斷組態結構描述檔案是安裝於 `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` 目錄中。</span><span class="sxs-lookup"><span data-stu-id="050cc-109">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="050cc-110">請使用安裝的 [Azure SDK](http://www.windowsazure.com/develop/downloads/) 版本來取代 `<version>`。</span><span class="sxs-lookup"><span data-stu-id="050cc-110">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="050cc-111">診斷組態檔通常會與啟動工作搭配使用，這類啟動工作需要在啟動程序前期收集診斷資料。</span><span class="sxs-lookup"><span data-stu-id="050cc-111">The diagnostics configuration file is typically used with startup tasks that require diagnostic data to be collected earlier in the startup process.</span></span> <span data-ttu-id="050cc-112">如需使用 Azure 診斷的詳細資訊，請參閱[使用 Azure 診斷收集記錄資料](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7)。</span><span class="sxs-lookup"><span data-stu-id="050cc-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="050cc-113">診斷組態檔的範例</span><span class="sxs-lookup"><span data-stu-id="050cc-113">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="050cc-114">下列範例顯示一般的診斷組態檔：</span><span class="sxs-lookup"><span data-stu-id="050cc-114">The following example shows a typical diagnostics configuration file:</span></span>  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify the special directories   
           that are set up for the log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories the DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative to a local   
                 resource defined in the service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- The counter specifier is in the same format as the imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- The event log name is in the same format as the imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="050cc-115">DiagnosticsConfiguration 命名空間</span><span class="sxs-lookup"><span data-stu-id="050cc-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="050cc-116">適用於診斷組態檔的 XML 命名空間如下：</span><span class="sxs-lookup"><span data-stu-id="050cc-116">The XML namespace for the diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="050cc-117">結構描述元素</span><span class="sxs-lookup"><span data-stu-id="050cc-117">Schema Elements</span></span>  
 <span data-ttu-id="050cc-118">診斷組態檔包含下列元素。</span><span class="sxs-lookup"><span data-stu-id="050cc-118">The diagnostics configuration file includes the following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="050cc-119">DiagnosticMonitorConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="050cc-120">診斷組態檔的最上層元素。</span><span class="sxs-lookup"><span data-stu-id="050cc-120">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="050cc-121">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-121">Attributes:</span></span>

|<span data-ttu-id="050cc-122">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-122">Attribute</span></span>  |<span data-ttu-id="050cc-123">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-123">Type</span></span>   |<span data-ttu-id="050cc-124">必要</span><span class="sxs-lookup"><span data-stu-id="050cc-124">Required</span></span>| <span data-ttu-id="050cc-125">預設值</span><span class="sxs-lookup"><span data-stu-id="050cc-125">Default</span></span> | <span data-ttu-id="050cc-126">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="050cc-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="050cc-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="050cc-128">duration</span><span class="sxs-lookup"><span data-stu-id="050cc-128">duration</span></span>|<span data-ttu-id="050cc-129">選用</span><span class="sxs-lookup"><span data-stu-id="050cc-129">Optional</span></span> | <span data-ttu-id="050cc-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="050cc-130">PT1M</span></span>| <span data-ttu-id="050cc-131">指定診斷監視器輪詢診斷組態變更的間隔。</span><span class="sxs-lookup"><span data-stu-id="050cc-131">Specifies the interval at which the diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="050cc-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="050cc-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="050cc-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="050cc-133">unsignedInt</span></span>|<span data-ttu-id="050cc-134">選用</span><span class="sxs-lookup"><span data-stu-id="050cc-134">Optional</span></span>| <span data-ttu-id="050cc-135">4000 MB。</span><span class="sxs-lookup"><span data-stu-id="050cc-135">4000 MB.</span></span> <span data-ttu-id="050cc-136">如果您提供值，該值不能超過此數量</span><span class="sxs-lookup"><span data-stu-id="050cc-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="050cc-137">針對所有記錄緩衝區配置的檔案系統儲存體總數量。</span><span class="sxs-lookup"><span data-stu-id="050cc-137">The total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="050cc-138">DiagnosticInfrastructureLogs 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="050cc-139">針對基本診斷基礎結構所產生的記錄定義緩衝區組態。</span><span class="sxs-lookup"><span data-stu-id="050cc-139">Defines the buffer configuration for the logs that are generated by the underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="050cc-140">父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="050cc-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="050cc-141">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-141">Attributes:</span></span>

|<span data-ttu-id="050cc-142">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-142">Attribute</span></span>|<span data-ttu-id="050cc-143">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-143">Type</span></span>|<span data-ttu-id="050cc-144">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="050cc-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="050cc-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="050cc-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="050cc-146">unsignedInt</span></span>|<span data-ttu-id="050cc-147">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-147">Optional.</span></span> <span data-ttu-id="050cc-148">指定適用於所指定資料的檔案系統儲存體數量上限。</span><span class="sxs-lookup"><span data-stu-id="050cc-148">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="050cc-149">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="050cc-149">The default is 0.</span></span>|  
|<span data-ttu-id="050cc-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="050cc-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="050cc-151">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-151">string</span></span>|<span data-ttu-id="050cc-152">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-152">Optional.</span></span> <span data-ttu-id="050cc-153">指定所傳輸記錄項目的最低嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="050cc-153">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="050cc-154">預設值為 **Undefined**。</span><span class="sxs-lookup"><span data-stu-id="050cc-154">The default value is **Undefined**.</span></span> <span data-ttu-id="050cc-155">其他可能的值為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。</span><span class="sxs-lookup"><span data-stu-id="050cc-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="050cc-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="050cc-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="050cc-157">duration</span><span class="sxs-lookup"><span data-stu-id="050cc-157">duration</span></span>|<span data-ttu-id="050cc-158">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-158">Optional.</span></span> <span data-ttu-id="050cc-159">指定排程傳輸資料之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="050cc-159">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="050cc-160">預設值為 PT0S。</span><span class="sxs-lookup"><span data-stu-id="050cc-160">The default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="050cc-161">Logs 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-161">Logs Element</span></span>  
 <span data-ttu-id="050cc-162">定義基本 Azure 記錄的緩衝區組態。</span><span class="sxs-lookup"><span data-stu-id="050cc-162">Defines the buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="050cc-163">父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="050cc-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="050cc-164">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-164">Attributes:</span></span>  

|<span data-ttu-id="050cc-165">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-165">Attribute</span></span>|<span data-ttu-id="050cc-166">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-166">Type</span></span>|<span data-ttu-id="050cc-167">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="050cc-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="050cc-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="050cc-169">unsignedInt</span></span>|<span data-ttu-id="050cc-170">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-170">Optional.</span></span> <span data-ttu-id="050cc-171">指定適用於所指定資料的檔案系統儲存體數量上限。</span><span class="sxs-lookup"><span data-stu-id="050cc-171">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="050cc-172">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="050cc-172">The default is 0.</span></span>|  
|<span data-ttu-id="050cc-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="050cc-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="050cc-174">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-174">string</span></span>|<span data-ttu-id="050cc-175">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-175">Optional.</span></span> <span data-ttu-id="050cc-176">指定所傳輸記錄項目的最低嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="050cc-176">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="050cc-177">預設值為 **Undefined**。</span><span class="sxs-lookup"><span data-stu-id="050cc-177">The default value is **Undefined**.</span></span> <span data-ttu-id="050cc-178">其他可能的值為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。</span><span class="sxs-lookup"><span data-stu-id="050cc-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="050cc-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="050cc-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="050cc-180">duration</span><span class="sxs-lookup"><span data-stu-id="050cc-180">duration</span></span>|<span data-ttu-id="050cc-181">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-181">Optional.</span></span> <span data-ttu-id="050cc-182">指定排程傳輸資料之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="050cc-182">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="050cc-183">預設值為 PT0S。</span><span class="sxs-lookup"><span data-stu-id="050cc-183">The default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="050cc-184">Directories 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-184">Directories Element</span></span>  
<span data-ttu-id="050cc-185">定義您可以定義之檔案式記錄的緩衝區組態。</span><span class="sxs-lookup"><span data-stu-id="050cc-185">Defines the buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="050cc-186">父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="050cc-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="050cc-187">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-187">Attributes:</span></span>  

|<span data-ttu-id="050cc-188">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-188">Attribute</span></span>|<span data-ttu-id="050cc-189">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-189">Type</span></span>|<span data-ttu-id="050cc-190">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="050cc-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="050cc-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="050cc-192">unsignedInt</span></span>|<span data-ttu-id="050cc-193">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-193">Optional.</span></span> <span data-ttu-id="050cc-194">指定適用於所指定資料的檔案系統儲存體數量上限。</span><span class="sxs-lookup"><span data-stu-id="050cc-194">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="050cc-195">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="050cc-195">The default is 0.</span></span>|  
|<span data-ttu-id="050cc-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="050cc-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="050cc-197">duration</span><span class="sxs-lookup"><span data-stu-id="050cc-197">duration</span></span>|<span data-ttu-id="050cc-198">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-198">Optional.</span></span> <span data-ttu-id="050cc-199">指定排程傳輸資料之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="050cc-199">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="050cc-200">預設值為 PT0S。</span><span class="sxs-lookup"><span data-stu-id="050cc-200">The default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="050cc-201">CrashDumps 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-201">CrashDumps Element</span></span>  
 <span data-ttu-id="050cc-202">定義損毀傾印目錄。</span><span class="sxs-lookup"><span data-stu-id="050cc-202">Defines the crash dumps directory.</span></span>

 <span data-ttu-id="050cc-203">父元素︰[Directories 元素](#Directories)。</span><span class="sxs-lookup"><span data-stu-id="050cc-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="050cc-204">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-204">Attributes:</span></span>  

|<span data-ttu-id="050cc-205">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-205">Attribute</span></span>|<span data-ttu-id="050cc-206">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-206">Type</span></span>|<span data-ttu-id="050cc-207">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-208">**container**</span><span class="sxs-lookup"><span data-stu-id="050cc-208">**container**</span></span>|<span data-ttu-id="050cc-209">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-209">string</span></span>|<span data-ttu-id="050cc-210">要傳輸目錄內容的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="050cc-210">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="050cc-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="050cc-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="050cc-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="050cc-212">unsignedInt</span></span>|<span data-ttu-id="050cc-213">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-213">Optional.</span></span> <span data-ttu-id="050cc-214">指定目錄的大小上限，以 MB 為單位。</span><span class="sxs-lookup"><span data-stu-id="050cc-214">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="050cc-215">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="050cc-215">The default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="050cc-216">FailedRequestLogs 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="050cc-217">定義失敗的要求記錄目錄。</span><span class="sxs-lookup"><span data-stu-id="050cc-217">Defines the failed request log directory.</span></span>

 <span data-ttu-id="050cc-218">父元素︰[Directories 元素](#Directories)。</span><span class="sxs-lookup"><span data-stu-id="050cc-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="050cc-219">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-219">Attributes:</span></span>  

|<span data-ttu-id="050cc-220">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-220">Attribute</span></span>|<span data-ttu-id="050cc-221">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-221">Type</span></span>|<span data-ttu-id="050cc-222">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-223">**container**</span><span class="sxs-lookup"><span data-stu-id="050cc-223">**container**</span></span>|<span data-ttu-id="050cc-224">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-224">string</span></span>|<span data-ttu-id="050cc-225">要傳輸目錄內容的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="050cc-225">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="050cc-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="050cc-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="050cc-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="050cc-227">unsignedInt</span></span>|<span data-ttu-id="050cc-228">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-228">Optional.</span></span> <span data-ttu-id="050cc-229">指定目錄的大小上限，以 MB 為單位。</span><span class="sxs-lookup"><span data-stu-id="050cc-229">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="050cc-230">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="050cc-230">The default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="050cc-231">IISLogs 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-231">IISLogs Element</span></span>  
 <span data-ttu-id="050cc-232">定義 IIS 記錄目錄。</span><span class="sxs-lookup"><span data-stu-id="050cc-232">Defines the IIS log directory.</span></span>

 <span data-ttu-id="050cc-233">父元素︰[Directories 元素](#Directories)。</span><span class="sxs-lookup"><span data-stu-id="050cc-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="050cc-234">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-234">Attributes:</span></span>  

|<span data-ttu-id="050cc-235">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-235">Attribute</span></span>|<span data-ttu-id="050cc-236">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-236">Type</span></span>|<span data-ttu-id="050cc-237">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-238">**container**</span><span class="sxs-lookup"><span data-stu-id="050cc-238">**container**</span></span>|<span data-ttu-id="050cc-239">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-239">string</span></span>|<span data-ttu-id="050cc-240">要傳輸目錄內容的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="050cc-240">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="050cc-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="050cc-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="050cc-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="050cc-242">unsignedInt</span></span>|<span data-ttu-id="050cc-243">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-243">Optional.</span></span> <span data-ttu-id="050cc-244">指定目錄的大小上限，以 MB 為單位。</span><span class="sxs-lookup"><span data-stu-id="050cc-244">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="050cc-245">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="050cc-245">The default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="050cc-246">DataSources 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-246">DataSources Element</span></span>  
 <span data-ttu-id="050cc-247">定義零或多個額外的記錄目錄。</span><span class="sxs-lookup"><span data-stu-id="050cc-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="050cc-248">父元素︰[Directories 元素](#Directories)。</span><span class="sxs-lookup"><span data-stu-id="050cc-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="050cc-249">DirectoryConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="050cc-250">定義要監視的記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="050cc-250">Defines the directory of log files to monitor.</span></span>

 <span data-ttu-id="050cc-251">父元素︰[DataSources 元素](#DataSources)。</span><span class="sxs-lookup"><span data-stu-id="050cc-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="050cc-252">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-252">Attributes:</span></span>

|<span data-ttu-id="050cc-253">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-253">Attribute</span></span>|<span data-ttu-id="050cc-254">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-254">Type</span></span>|<span data-ttu-id="050cc-255">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-256">**container**</span><span class="sxs-lookup"><span data-stu-id="050cc-256">**container**</span></span>|<span data-ttu-id="050cc-257">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-257">string</span></span>|<span data-ttu-id="050cc-258">要傳輸目錄內容的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="050cc-258">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="050cc-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="050cc-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="050cc-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="050cc-260">unsignedInt</span></span>|<span data-ttu-id="050cc-261">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-261">Optional.</span></span> <span data-ttu-id="050cc-262">指定目錄的大小上限，以 MB 為單位。</span><span class="sxs-lookup"><span data-stu-id="050cc-262">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="050cc-263">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="050cc-263">The default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="050cc-264">Absolute 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-264">Absolute Element</span></span>  
 <span data-ttu-id="050cc-265">搭配選擇性環境變數展開來定義要監視之目錄的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="050cc-265">Defines an absolute path of the directory to monitor with optional environment expansion.</span></span>

 <span data-ttu-id="050cc-266">父元素：[DirectoryConfiguration 元素](#DirectoryConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="050cc-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="050cc-267">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-267">Attributes:</span></span>  

|<span data-ttu-id="050cc-268">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-268">Attribute</span></span>|<span data-ttu-id="050cc-269">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-269">Type</span></span>|<span data-ttu-id="050cc-270">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-271">**路徑**</span><span class="sxs-lookup"><span data-stu-id="050cc-271">**path**</span></span>|<span data-ttu-id="050cc-272">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-272">string</span></span>|<span data-ttu-id="050cc-273">必要。</span><span class="sxs-lookup"><span data-stu-id="050cc-273">Required.</span></span> <span data-ttu-id="050cc-274">要監視之目錄的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="050cc-274">The absolute path to the directory to monitor.</span></span>|  
|<span data-ttu-id="050cc-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="050cc-275">**expandEnvironment**</span></span>|<span data-ttu-id="050cc-276">布林值</span><span class="sxs-lookup"><span data-stu-id="050cc-276">boolean</span></span>|<span data-ttu-id="050cc-277">必要。</span><span class="sxs-lookup"><span data-stu-id="050cc-277">Required.</span></span> <span data-ttu-id="050cc-278">如果設定為 **true**，就會展開路徑中的環境變數。</span><span class="sxs-lookup"><span data-stu-id="050cc-278">If set to **true**, environment variables in the path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="050cc-279">LocalResource 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-279">LocalResource Element</span></span>  
 <span data-ttu-id="050cc-280">定義相對於服務定義中所定義之本機資源的路徑。</span><span class="sxs-lookup"><span data-stu-id="050cc-280">Defines a path relative to a local resource defined in the service definition.</span></span>

 <span data-ttu-id="050cc-281">父元素：[DirectoryConfiguration 元素](#DirectoryConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="050cc-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="050cc-282">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-282">Attributes:</span></span>  

|<span data-ttu-id="050cc-283">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-283">Attribute</span></span>|<span data-ttu-id="050cc-284">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-284">Type</span></span>|<span data-ttu-id="050cc-285">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-286">**name**</span><span class="sxs-lookup"><span data-stu-id="050cc-286">**name**</span></span>|<span data-ttu-id="050cc-287">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-287">string</span></span>|<span data-ttu-id="050cc-288">必要。</span><span class="sxs-lookup"><span data-stu-id="050cc-288">Required.</span></span> <span data-ttu-id="050cc-289">包含要監視之目錄的本機資源名稱。</span><span class="sxs-lookup"><span data-stu-id="050cc-289">The name of the local resource that contains the directory to monitor.</span></span>|  
|<span data-ttu-id="050cc-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="050cc-290">**relativePath**</span></span>|<span data-ttu-id="050cc-291">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-291">string</span></span>|<span data-ttu-id="050cc-292">必要。</span><span class="sxs-lookup"><span data-stu-id="050cc-292">Required.</span></span> <span data-ttu-id="050cc-293">相對於要監視之本機資源的路徑。</span><span class="sxs-lookup"><span data-stu-id="050cc-293">The path relative to the local resource to monitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="050cc-294">PerformanceCounters 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="050cc-295">定義要收集之效能計數器的路徑。</span><span class="sxs-lookup"><span data-stu-id="050cc-295">Defines the path to the performance counter to collect.</span></span>

 <span data-ttu-id="050cc-296">父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="050cc-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="050cc-297">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-297">Attributes:</span></span>  

|<span data-ttu-id="050cc-298">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-298">Attribute</span></span>|<span data-ttu-id="050cc-299">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-299">Type</span></span>|<span data-ttu-id="050cc-300">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="050cc-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="050cc-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="050cc-302">unsignedInt</span></span>|<span data-ttu-id="050cc-303">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-303">Optional.</span></span> <span data-ttu-id="050cc-304">指定適用於所指定資料的檔案系統儲存體數量上限。</span><span class="sxs-lookup"><span data-stu-id="050cc-304">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="050cc-305">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="050cc-305">The default is 0.</span></span>|  
|<span data-ttu-id="050cc-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="050cc-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="050cc-307">duration</span><span class="sxs-lookup"><span data-stu-id="050cc-307">duration</span></span>|<span data-ttu-id="050cc-308">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-308">Optional.</span></span> <span data-ttu-id="050cc-309">指定排程傳輸資料之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="050cc-309">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="050cc-310">預設值為 PT0S。</span><span class="sxs-lookup"><span data-stu-id="050cc-310">The default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="050cc-311">PerformanceCounterConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="050cc-312">定義要收集的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="050cc-312">Defines the performance counter to collect.</span></span>

 <span data-ttu-id="050cc-313">父元素︰[PerformanceCounters 元素](#PerformanceCounters)。</span><span class="sxs-lookup"><span data-stu-id="050cc-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="050cc-314">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-314">Attributes:</span></span>  

|<span data-ttu-id="050cc-315">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-315">Attribute</span></span>|<span data-ttu-id="050cc-316">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-316">Type</span></span>|<span data-ttu-id="050cc-317">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="050cc-318">**counterSpecifier**</span></span>|<span data-ttu-id="050cc-319">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-319">string</span></span>|<span data-ttu-id="050cc-320">必要。</span><span class="sxs-lookup"><span data-stu-id="050cc-320">Required.</span></span> <span data-ttu-id="050cc-321">要收集之效能計數器的路徑。</span><span class="sxs-lookup"><span data-stu-id="050cc-321">The path to the performance counter to collect.</span></span>|  
|<span data-ttu-id="050cc-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="050cc-322">**sampleRate**</span></span>|<span data-ttu-id="050cc-323">duration</span><span class="sxs-lookup"><span data-stu-id="050cc-323">duration</span></span>|<span data-ttu-id="050cc-324">必要。</span><span class="sxs-lookup"><span data-stu-id="050cc-324">Required.</span></span> <span data-ttu-id="050cc-325">應收集效能計數器的頻率。</span><span class="sxs-lookup"><span data-stu-id="050cc-325">The rate at which the performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="050cc-326">WindowsEventLog 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="050cc-327">定義要監視的事件記錄。</span><span class="sxs-lookup"><span data-stu-id="050cc-327">Defines the event logs to monitor.</span></span>

 <span data-ttu-id="050cc-328">父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="050cc-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="050cc-329">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-329">Attributes:</span></span>

|<span data-ttu-id="050cc-330">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-330">Attribute</span></span>|<span data-ttu-id="050cc-331">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-331">Type</span></span>|<span data-ttu-id="050cc-332">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="050cc-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="050cc-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="050cc-334">unsignedInt</span></span>|<span data-ttu-id="050cc-335">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-335">Optional.</span></span> <span data-ttu-id="050cc-336">指定適用於所指定資料的檔案系統儲存體數量上限。</span><span class="sxs-lookup"><span data-stu-id="050cc-336">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="050cc-337">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="050cc-337">The default is 0.</span></span>|  
|<span data-ttu-id="050cc-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="050cc-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="050cc-339">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-339">string</span></span>|<span data-ttu-id="050cc-340">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-340">Optional.</span></span> <span data-ttu-id="050cc-341">指定所傳輸記錄項目的最低嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="050cc-341">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="050cc-342">預設值為 **Undefined**。</span><span class="sxs-lookup"><span data-stu-id="050cc-342">The default value is **Undefined**.</span></span> <span data-ttu-id="050cc-343">其他可能的值為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。</span><span class="sxs-lookup"><span data-stu-id="050cc-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="050cc-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="050cc-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="050cc-345">duration</span><span class="sxs-lookup"><span data-stu-id="050cc-345">duration</span></span>|<span data-ttu-id="050cc-346">選用。</span><span class="sxs-lookup"><span data-stu-id="050cc-346">Optional.</span></span> <span data-ttu-id="050cc-347">指定排程傳輸資料之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="050cc-347">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="050cc-348">預設值為 PT0S。</span><span class="sxs-lookup"><span data-stu-id="050cc-348">The default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="050cc-349">DataSource 元素</span><span class="sxs-lookup"><span data-stu-id="050cc-349">DataSource Element</span></span>  
 <span data-ttu-id="050cc-350">定義要監視的事件記錄。</span><span class="sxs-lookup"><span data-stu-id="050cc-350">Defines the event log to monitor.</span></span>

 <span data-ttu-id="050cc-351">父元素︰[WindowsEventLog 元素](#windowsEventLog)。</span><span class="sxs-lookup"><span data-stu-id="050cc-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="050cc-352">屬性：</span><span class="sxs-lookup"><span data-stu-id="050cc-352">Attributes:</span></span>

|<span data-ttu-id="050cc-353">屬性</span><span class="sxs-lookup"><span data-stu-id="050cc-353">Attribute</span></span>|<span data-ttu-id="050cc-354">類型</span><span class="sxs-lookup"><span data-stu-id="050cc-354">Type</span></span>|<span data-ttu-id="050cc-355">說明</span><span class="sxs-lookup"><span data-stu-id="050cc-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="050cc-356">**name**</span><span class="sxs-lookup"><span data-stu-id="050cc-356">**name**</span></span>|<span data-ttu-id="050cc-357">字串</span><span class="sxs-lookup"><span data-stu-id="050cc-357">string</span></span>|<span data-ttu-id="050cc-358">必要。</span><span class="sxs-lookup"><span data-stu-id="050cc-358">Required.</span></span> <span data-ttu-id="050cc-359">指定要收集之記錄的 XPath 運算式。</span><span class="sxs-lookup"><span data-stu-id="050cc-359">An XPath expression specifying the log to collect.</span></span>|  
