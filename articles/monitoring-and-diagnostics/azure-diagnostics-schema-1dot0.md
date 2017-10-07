---
title: "aaaAzure 診斷 1.0 組態結構描述 |Microsoft 文件"
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
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="df8de-103">Azure 診斷 1.0 組態結構描述</span><span class="sxs-lookup"><span data-stu-id="df8de-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="df8de-104">Azure 診斷是 hello 用元件 toocollect 效能計數器和其他統計資料從 Azure 虛擬機器、 虛擬機器擴展集、 Service Fabric 和雲端服務。</span><span class="sxs-lookup"><span data-stu-id="df8de-104">Azure Diagnostics is hello component used toocollect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="df8de-105">此頁面只在您使用其中一個服務時才相關。</span><span class="sxs-lookup"><span data-stu-id="df8de-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="df8de-106">Azure 診斷要與 Azure 監視器、Application Insights 和 Log Analytics 等其他 Microsoft 診斷產品搭配使用。</span><span class="sxs-lookup"><span data-stu-id="df8de-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="df8de-107">hello Azure 診斷組態檔會定義使用的 tooinitialize hello 診斷監視器的值。</span><span class="sxs-lookup"><span data-stu-id="df8de-107">hello Azure Diagnostics configuration file defines values that are used tooinitialize hello Diagnostics Monitor.</span></span> <span data-ttu-id="df8de-108">Hello 診斷監視器啟動時，這個檔案是使用的 tooinitialize 診斷的組態設定。</span><span class="sxs-lookup"><span data-stu-id="df8de-108">This file is used tooinitialize diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

 <span data-ttu-id="df8de-109">根據預設，hello Azure 診斷組態結構描述檔案是安裝的 toohello`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas`目錄。</span><span class="sxs-lookup"><span data-stu-id="df8de-109">By default, hello Azure Diagnostics configuration schema file is installed toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="df8de-110">取代`<version>`hello 安裝版的 hello 與[Azure SDK](http://www.windowsazure.com/develop/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="df8de-110">Replace `<version>` with hello installed version of hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="df8de-111">hello 診斷組態檔通常搭配需要稍早在 hello 啟動程序中收集的診斷資料 toobe 的啟動工作。</span><span class="sxs-lookup"><span data-stu-id="df8de-111">hello diagnostics configuration file is typically used with startup tasks that require diagnostic data toobe collected earlier in hello startup process.</span></span> <span data-ttu-id="df8de-112">如需使用 Azure 診斷的詳細資訊，請參閱[使用 Azure 診斷收集記錄資料](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7)。</span><span class="sxs-lookup"><span data-stu-id="df8de-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="df8de-113">Hello 診斷組態檔的範例</span><span class="sxs-lookup"><span data-stu-id="df8de-113">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="df8de-114">下列範例中的 hello 顯示一般的診斷組態檔：</span><span class="sxs-lookup"><span data-stu-id="df8de-114">hello following example shows a typical diagnostics configuration file:</span></span>  

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

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="df8de-115">DiagnosticsConfiguration 命名空間</span><span class="sxs-lookup"><span data-stu-id="df8de-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="df8de-116">hello hello 診斷組態檔的 XML 命名空間為：</span><span class="sxs-lookup"><span data-stu-id="df8de-116">hello XML namespace for hello diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="df8de-117">結構描述元素</span><span class="sxs-lookup"><span data-stu-id="df8de-117">Schema Elements</span></span>  
 <span data-ttu-id="df8de-118">hello 診斷組態檔包含下列項目 hello。</span><span class="sxs-lookup"><span data-stu-id="df8de-118">hello diagnostics configuration file includes hello following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="df8de-119">DiagnosticMonitorConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="df8de-120">hello hello 診斷組態檔的最上層項目。</span><span class="sxs-lookup"><span data-stu-id="df8de-120">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="df8de-121">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-121">Attributes:</span></span>

|<span data-ttu-id="df8de-122">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-122">Attribute</span></span>  |<span data-ttu-id="df8de-123">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-123">Type</span></span>   |<span data-ttu-id="df8de-124">必要</span><span class="sxs-lookup"><span data-stu-id="df8de-124">Required</span></span>| <span data-ttu-id="df8de-125">預設值</span><span class="sxs-lookup"><span data-stu-id="df8de-125">Default</span></span> | <span data-ttu-id="df8de-126">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="df8de-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="df8de-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="df8de-128">duration</span><span class="sxs-lookup"><span data-stu-id="df8de-128">duration</span></span>|<span data-ttu-id="df8de-129">選用</span><span class="sxs-lookup"><span data-stu-id="df8de-129">Optional</span></span> | <span data-ttu-id="df8de-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="df8de-130">PT1M</span></span>| <span data-ttu-id="df8de-131">指定 hello 間隔的 hello 診斷監視器輪詢診斷組態變更。</span><span class="sxs-lookup"><span data-stu-id="df8de-131">Specifies hello interval at which hello diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="df8de-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="df8de-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="df8de-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="df8de-133">unsignedInt</span></span>|<span data-ttu-id="df8de-134">選用</span><span class="sxs-lookup"><span data-stu-id="df8de-134">Optional</span></span>| <span data-ttu-id="df8de-135">4000 MB。</span><span class="sxs-lookup"><span data-stu-id="df8de-135">4000 MB.</span></span> <span data-ttu-id="df8de-136">如果您提供值，該值不能超過此數量</span><span class="sxs-lookup"><span data-stu-id="df8de-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="df8de-137">hello 的檔案系統儲存體的所有記錄緩衝區配置的總容量。</span><span class="sxs-lookup"><span data-stu-id="df8de-137">hello total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="df8de-138">DiagnosticInfrastructureLogs 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="df8de-139">定義 hello hello hello 基礎診斷基礎結構所產生的記錄檔的緩衝區組態。</span><span class="sxs-lookup"><span data-stu-id="df8de-139">Defines hello buffer configuration for hello logs that are generated by hello underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="df8de-140">父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="df8de-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="df8de-141">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-141">Attributes:</span></span>

|<span data-ttu-id="df8de-142">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-142">Attribute</span></span>|<span data-ttu-id="df8de-143">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-143">Type</span></span>|<span data-ttu-id="df8de-144">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="df8de-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="df8de-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="df8de-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="df8de-146">unsignedInt</span></span>|<span data-ttu-id="df8de-147">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-147">Optional.</span></span> <span data-ttu-id="df8de-148">指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。</span><span class="sxs-lookup"><span data-stu-id="df8de-148">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="df8de-149">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="df8de-149">hello default is 0.</span></span>|  
|<span data-ttu-id="df8de-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="df8de-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="df8de-151">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-151">string</span></span>|<span data-ttu-id="df8de-152">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-152">Optional.</span></span> <span data-ttu-id="df8de-153">指定最低嚴重性層級 hello 傳送的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="df8de-153">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="df8de-154">hello 預設值是**Undefined**。</span><span class="sxs-lookup"><span data-stu-id="df8de-154">hello default value is **Undefined**.</span></span> <span data-ttu-id="df8de-155">其他可能的值為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。</span><span class="sxs-lookup"><span data-stu-id="df8de-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="df8de-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="df8de-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="df8de-157">duration</span><span class="sxs-lookup"><span data-stu-id="df8de-157">duration</span></span>|<span data-ttu-id="df8de-158">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-158">Optional.</span></span> <span data-ttu-id="df8de-159">指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。</span><span class="sxs-lookup"><span data-stu-id="df8de-159">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="df8de-160">hello 預設值是 PT0S。</span><span class="sxs-lookup"><span data-stu-id="df8de-160">hello default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="df8de-161">Logs 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-161">Logs Element</span></span>  
 <span data-ttu-id="df8de-162">定義基本 Azure 記錄檔的 hello 緩衝區組態。</span><span class="sxs-lookup"><span data-stu-id="df8de-162">Defines hello buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="df8de-163">父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="df8de-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="df8de-164">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-164">Attributes:</span></span>  

|<span data-ttu-id="df8de-165">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-165">Attribute</span></span>|<span data-ttu-id="df8de-166">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-166">Type</span></span>|<span data-ttu-id="df8de-167">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="df8de-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="df8de-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="df8de-169">unsignedInt</span></span>|<span data-ttu-id="df8de-170">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-170">Optional.</span></span> <span data-ttu-id="df8de-171">指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。</span><span class="sxs-lookup"><span data-stu-id="df8de-171">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="df8de-172">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="df8de-172">hello default is 0.</span></span>|  
|<span data-ttu-id="df8de-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="df8de-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="df8de-174">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-174">string</span></span>|<span data-ttu-id="df8de-175">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-175">Optional.</span></span> <span data-ttu-id="df8de-176">指定最低嚴重性層級 hello 傳送的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="df8de-176">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="df8de-177">hello 預設值是**Undefined**。</span><span class="sxs-lookup"><span data-stu-id="df8de-177">hello default value is **Undefined**.</span></span> <span data-ttu-id="df8de-178">其他可能的值為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。</span><span class="sxs-lookup"><span data-stu-id="df8de-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="df8de-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="df8de-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="df8de-180">duration</span><span class="sxs-lookup"><span data-stu-id="df8de-180">duration</span></span>|<span data-ttu-id="df8de-181">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-181">Optional.</span></span> <span data-ttu-id="df8de-182">指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。</span><span class="sxs-lookup"><span data-stu-id="df8de-182">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="df8de-183">hello 預設值是 PT0S。</span><span class="sxs-lookup"><span data-stu-id="df8de-183">hello default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="df8de-184">Directories 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-184">Directories Element</span></span>  
<span data-ttu-id="df8de-185">定義您可以定義檔案式記錄檔的 hello 緩衝區組態。</span><span class="sxs-lookup"><span data-stu-id="df8de-185">Defines hello buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="df8de-186">父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="df8de-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="df8de-187">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-187">Attributes:</span></span>  

|<span data-ttu-id="df8de-188">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-188">Attribute</span></span>|<span data-ttu-id="df8de-189">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-189">Type</span></span>|<span data-ttu-id="df8de-190">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="df8de-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="df8de-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="df8de-192">unsignedInt</span></span>|<span data-ttu-id="df8de-193">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-193">Optional.</span></span> <span data-ttu-id="df8de-194">指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。</span><span class="sxs-lookup"><span data-stu-id="df8de-194">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="df8de-195">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="df8de-195">hello default is 0.</span></span>|  
|<span data-ttu-id="df8de-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="df8de-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="df8de-197">duration</span><span class="sxs-lookup"><span data-stu-id="df8de-197">duration</span></span>|<span data-ttu-id="df8de-198">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-198">Optional.</span></span> <span data-ttu-id="df8de-199">指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。</span><span class="sxs-lookup"><span data-stu-id="df8de-199">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="df8de-200">hello 預設值是 PT0S。</span><span class="sxs-lookup"><span data-stu-id="df8de-200">hello default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="df8de-201">CrashDumps 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-201">CrashDumps Element</span></span>  
 <span data-ttu-id="df8de-202">定義 hello 損毀傾印目錄。</span><span class="sxs-lookup"><span data-stu-id="df8de-202">Defines hello crash dumps directory.</span></span>

 <span data-ttu-id="df8de-203">父元素︰[Directories 元素](#Directories)。</span><span class="sxs-lookup"><span data-stu-id="df8de-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="df8de-204">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-204">Attributes:</span></span>  

|<span data-ttu-id="df8de-205">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-205">Attribute</span></span>|<span data-ttu-id="df8de-206">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-206">Type</span></span>|<span data-ttu-id="df8de-207">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-208">**container**</span><span class="sxs-lookup"><span data-stu-id="df8de-208">**container**</span></span>|<span data-ttu-id="df8de-209">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-209">string</span></span>|<span data-ttu-id="df8de-210">傳送 hello 容器是 hello 目錄 hello 內容 toobe hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="df8de-210">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="df8de-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="df8de-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="df8de-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="df8de-212">unsignedInt</span></span>|<span data-ttu-id="df8de-213">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-213">Optional.</span></span> <span data-ttu-id="df8de-214">指定 hello hello 目錄的大小上限以 mb 為單位。</span><span class="sxs-lookup"><span data-stu-id="df8de-214">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="df8de-215">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="df8de-215">hello default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="df8de-216">FailedRequestLogs 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="df8de-217">定義 hello 失敗的要求記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="df8de-217">Defines hello failed request log directory.</span></span>

 <span data-ttu-id="df8de-218">父元素︰[Directories 元素](#Directories)。</span><span class="sxs-lookup"><span data-stu-id="df8de-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="df8de-219">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-219">Attributes:</span></span>  

|<span data-ttu-id="df8de-220">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-220">Attribute</span></span>|<span data-ttu-id="df8de-221">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-221">Type</span></span>|<span data-ttu-id="df8de-222">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-223">**container**</span><span class="sxs-lookup"><span data-stu-id="df8de-223">**container**</span></span>|<span data-ttu-id="df8de-224">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-224">string</span></span>|<span data-ttu-id="df8de-225">傳送 hello 容器是 hello 目錄 hello 內容 toobe hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="df8de-225">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="df8de-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="df8de-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="df8de-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="df8de-227">unsignedInt</span></span>|<span data-ttu-id="df8de-228">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-228">Optional.</span></span> <span data-ttu-id="df8de-229">指定 hello hello 目錄的大小上限以 mb 為單位。</span><span class="sxs-lookup"><span data-stu-id="df8de-229">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="df8de-230">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="df8de-230">hello default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="df8de-231">IISLogs 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-231">IISLogs Element</span></span>  
 <span data-ttu-id="df8de-232">定義 hello IIS 記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="df8de-232">Defines hello IIS log directory.</span></span>

 <span data-ttu-id="df8de-233">父元素︰[Directories 元素](#Directories)。</span><span class="sxs-lookup"><span data-stu-id="df8de-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="df8de-234">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-234">Attributes:</span></span>  

|<span data-ttu-id="df8de-235">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-235">Attribute</span></span>|<span data-ttu-id="df8de-236">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-236">Type</span></span>|<span data-ttu-id="df8de-237">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-238">**container**</span><span class="sxs-lookup"><span data-stu-id="df8de-238">**container**</span></span>|<span data-ttu-id="df8de-239">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-239">string</span></span>|<span data-ttu-id="df8de-240">傳送 hello 容器是 hello 目錄 hello 內容 toobe hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="df8de-240">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="df8de-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="df8de-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="df8de-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="df8de-242">unsignedInt</span></span>|<span data-ttu-id="df8de-243">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-243">Optional.</span></span> <span data-ttu-id="df8de-244">指定 hello hello 目錄的大小上限以 mb 為單位。</span><span class="sxs-lookup"><span data-stu-id="df8de-244">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="df8de-245">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="df8de-245">hello default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="df8de-246">DataSources 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-246">DataSources Element</span></span>  
 <span data-ttu-id="df8de-247">定義零或多個額外的記錄目錄。</span><span class="sxs-lookup"><span data-stu-id="df8de-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="df8de-248">父元素︰[Directories 元素](#Directories)。</span><span class="sxs-lookup"><span data-stu-id="df8de-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="df8de-249">DirectoryConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="df8de-250">定義記錄檔 toomonitor hello 的目錄。</span><span class="sxs-lookup"><span data-stu-id="df8de-250">Defines hello directory of log files toomonitor.</span></span>

 <span data-ttu-id="df8de-251">父元素︰[DataSources 元素](#DataSources)。</span><span class="sxs-lookup"><span data-stu-id="df8de-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="df8de-252">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-252">Attributes:</span></span>

|<span data-ttu-id="df8de-253">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-253">Attribute</span></span>|<span data-ttu-id="df8de-254">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-254">Type</span></span>|<span data-ttu-id="df8de-255">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-256">**container**</span><span class="sxs-lookup"><span data-stu-id="df8de-256">**container**</span></span>|<span data-ttu-id="df8de-257">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-257">string</span></span>|<span data-ttu-id="df8de-258">傳送 hello 容器是 hello 目錄 hello 內容 toobe hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="df8de-258">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="df8de-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="df8de-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="df8de-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="df8de-260">unsignedInt</span></span>|<span data-ttu-id="df8de-261">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-261">Optional.</span></span> <span data-ttu-id="df8de-262">指定 hello hello 目錄的大小上限以 mb 為單位。</span><span class="sxs-lookup"><span data-stu-id="df8de-262">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="df8de-263">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="df8de-263">hello default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="df8de-264">Absolute 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-264">Absolute Element</span></span>  
 <span data-ttu-id="df8de-265">定義選擇性環境展開 hello 目錄 toomonitor 的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="df8de-265">Defines an absolute path of hello directory toomonitor with optional environment expansion.</span></span>

 <span data-ttu-id="df8de-266">父元素：[DirectoryConfiguration 元素](#DirectoryConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="df8de-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="df8de-267">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-267">Attributes:</span></span>  

|<span data-ttu-id="df8de-268">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-268">Attribute</span></span>|<span data-ttu-id="df8de-269">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-269">Type</span></span>|<span data-ttu-id="df8de-270">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-271">**路徑**</span><span class="sxs-lookup"><span data-stu-id="df8de-271">**path**</span></span>|<span data-ttu-id="df8de-272">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-272">string</span></span>|<span data-ttu-id="df8de-273">必要。</span><span class="sxs-lookup"><span data-stu-id="df8de-273">Required.</span></span> <span data-ttu-id="df8de-274">絕對路徑 toohello 目錄 toomonitor hello。</span><span class="sxs-lookup"><span data-stu-id="df8de-274">hello absolute path toohello directory toomonitor.</span></span>|  
|<span data-ttu-id="df8de-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="df8de-275">**expandEnvironment**</span></span>|<span data-ttu-id="df8de-276">布林值</span><span class="sxs-lookup"><span data-stu-id="df8de-276">boolean</span></span>|<span data-ttu-id="df8de-277">必要。</span><span class="sxs-lookup"><span data-stu-id="df8de-277">Required.</span></span> <span data-ttu-id="df8de-278">如果設定太**true**，hello 路徑中的環境變數會展開。</span><span class="sxs-lookup"><span data-stu-id="df8de-278">If set too**true**, environment variables in hello path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="df8de-279">LocalResource 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-279">LocalResource Element</span></span>  
 <span data-ttu-id="df8de-280">定義在 hello 服務定義中定義之路徑的相對 tooa 本機資源。</span><span class="sxs-lookup"><span data-stu-id="df8de-280">Defines a path relative tooa local resource defined in hello service definition.</span></span>

 <span data-ttu-id="df8de-281">父元素：[DirectoryConfiguration 元素](#DirectoryConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="df8de-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="df8de-282">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-282">Attributes:</span></span>  

|<span data-ttu-id="df8de-283">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-283">Attribute</span></span>|<span data-ttu-id="df8de-284">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-284">Type</span></span>|<span data-ttu-id="df8de-285">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-286">**name**</span><span class="sxs-lookup"><span data-stu-id="df8de-286">**name**</span></span>|<span data-ttu-id="df8de-287">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-287">string</span></span>|<span data-ttu-id="df8de-288">必要。</span><span class="sxs-lookup"><span data-stu-id="df8de-288">Required.</span></span> <span data-ttu-id="df8de-289">hello 包含 hello 目錄 toomonitor hello 本機資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="df8de-289">hello name of hello local resource that contains hello directory toomonitor.</span></span>|  
|<span data-ttu-id="df8de-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="df8de-290">**relativePath**</span></span>|<span data-ttu-id="df8de-291">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-291">string</span></span>|<span data-ttu-id="df8de-292">必要。</span><span class="sxs-lookup"><span data-stu-id="df8de-292">Required.</span></span> <span data-ttu-id="df8de-293">hello 路徑相對 toohello 本機資源 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="df8de-293">hello path relative toohello local resource toomonitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="df8de-294">PerformanceCounters 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="df8de-295">定義 hello 路徑 toohello 效能計數器 toocollect。</span><span class="sxs-lookup"><span data-stu-id="df8de-295">Defines hello path toohello performance counter toocollect.</span></span>

 <span data-ttu-id="df8de-296">父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="df8de-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="df8de-297">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-297">Attributes:</span></span>  

|<span data-ttu-id="df8de-298">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-298">Attribute</span></span>|<span data-ttu-id="df8de-299">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-299">Type</span></span>|<span data-ttu-id="df8de-300">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="df8de-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="df8de-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="df8de-302">unsignedInt</span></span>|<span data-ttu-id="df8de-303">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-303">Optional.</span></span> <span data-ttu-id="df8de-304">指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。</span><span class="sxs-lookup"><span data-stu-id="df8de-304">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="df8de-305">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="df8de-305">hello default is 0.</span></span>|  
|<span data-ttu-id="df8de-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="df8de-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="df8de-307">duration</span><span class="sxs-lookup"><span data-stu-id="df8de-307">duration</span></span>|<span data-ttu-id="df8de-308">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-308">Optional.</span></span> <span data-ttu-id="df8de-309">指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。</span><span class="sxs-lookup"><span data-stu-id="df8de-309">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="df8de-310">hello 預設值是 PT0S。</span><span class="sxs-lookup"><span data-stu-id="df8de-310">hello default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="df8de-311">PerformanceCounterConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="df8de-312">定義 hello 效能計數器 toocollect。</span><span class="sxs-lookup"><span data-stu-id="df8de-312">Defines hello performance counter toocollect.</span></span>

 <span data-ttu-id="df8de-313">父元素︰[PerformanceCounters 元素](#PerformanceCounters)。</span><span class="sxs-lookup"><span data-stu-id="df8de-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="df8de-314">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-314">Attributes:</span></span>  

|<span data-ttu-id="df8de-315">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-315">Attribute</span></span>|<span data-ttu-id="df8de-316">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-316">Type</span></span>|<span data-ttu-id="df8de-317">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="df8de-318">**counterSpecifier**</span></span>|<span data-ttu-id="df8de-319">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-319">string</span></span>|<span data-ttu-id="df8de-320">必要。</span><span class="sxs-lookup"><span data-stu-id="df8de-320">Required.</span></span> <span data-ttu-id="df8de-321">hello 路徑 toohello 效能計數器 toocollect。</span><span class="sxs-lookup"><span data-stu-id="df8de-321">hello path toohello performance counter toocollect.</span></span>|  
|<span data-ttu-id="df8de-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="df8de-322">**sampleRate**</span></span>|<span data-ttu-id="df8de-323">duration</span><span class="sxs-lookup"><span data-stu-id="df8de-323">duration</span></span>|<span data-ttu-id="df8de-324">必要。</span><span class="sxs-lookup"><span data-stu-id="df8de-324">Required.</span></span> <span data-ttu-id="df8de-325">您應該在哪一個 hello 收集效能計數器的 hello 速率。</span><span class="sxs-lookup"><span data-stu-id="df8de-325">hello rate at which hello performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="df8de-326">WindowsEventLog 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="df8de-327">定義 hello 事件記錄檔 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="df8de-327">Defines hello event logs toomonitor.</span></span>

 <span data-ttu-id="df8de-328">父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。</span><span class="sxs-lookup"><span data-stu-id="df8de-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="df8de-329">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-329">Attributes:</span></span>

|<span data-ttu-id="df8de-330">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-330">Attribute</span></span>|<span data-ttu-id="df8de-331">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-331">Type</span></span>|<span data-ttu-id="df8de-332">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="df8de-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="df8de-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="df8de-334">unsignedInt</span></span>|<span data-ttu-id="df8de-335">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-335">Optional.</span></span> <span data-ttu-id="df8de-336">指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。</span><span class="sxs-lookup"><span data-stu-id="df8de-336">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="df8de-337">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="df8de-337">hello default is 0.</span></span>|  
|<span data-ttu-id="df8de-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="df8de-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="df8de-339">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-339">string</span></span>|<span data-ttu-id="df8de-340">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-340">Optional.</span></span> <span data-ttu-id="df8de-341">指定最低嚴重性層級 hello 傳送的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="df8de-341">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="df8de-342">hello 預設值是**Undefined**。</span><span class="sxs-lookup"><span data-stu-id="df8de-342">hello default value is **Undefined**.</span></span> <span data-ttu-id="df8de-343">其他可能的值為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。</span><span class="sxs-lookup"><span data-stu-id="df8de-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="df8de-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="df8de-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="df8de-345">duration</span><span class="sxs-lookup"><span data-stu-id="df8de-345">duration</span></span>|<span data-ttu-id="df8de-346">選用。</span><span class="sxs-lookup"><span data-stu-id="df8de-346">Optional.</span></span> <span data-ttu-id="df8de-347">指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。</span><span class="sxs-lookup"><span data-stu-id="df8de-347">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="df8de-348">hello 預設值是 PT0S。</span><span class="sxs-lookup"><span data-stu-id="df8de-348">hello default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="df8de-349">DataSource 元素</span><span class="sxs-lookup"><span data-stu-id="df8de-349">DataSource Element</span></span>  
 <span data-ttu-id="df8de-350">定義 hello 事件記錄檔 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="df8de-350">Defines hello event log toomonitor.</span></span>

 <span data-ttu-id="df8de-351">父元素︰[WindowsEventLog 元素](#windowsEventLog)。</span><span class="sxs-lookup"><span data-stu-id="df8de-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="df8de-352">屬性：</span><span class="sxs-lookup"><span data-stu-id="df8de-352">Attributes:</span></span>

|<span data-ttu-id="df8de-353">屬性</span><span class="sxs-lookup"><span data-stu-id="df8de-353">Attribute</span></span>|<span data-ttu-id="df8de-354">類型</span><span class="sxs-lookup"><span data-stu-id="df8de-354">Type</span></span>|<span data-ttu-id="df8de-355">說明</span><span class="sxs-lookup"><span data-stu-id="df8de-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="df8de-356">**name**</span><span class="sxs-lookup"><span data-stu-id="df8de-356">**name**</span></span>|<span data-ttu-id="df8de-357">字串</span><span class="sxs-lookup"><span data-stu-id="df8de-357">string</span></span>|<span data-ttu-id="df8de-358">必要。</span><span class="sxs-lookup"><span data-stu-id="df8de-358">Required.</span></span> <span data-ttu-id="df8de-359">指定 hello 記錄 toocollect XPath 運算式。</span><span class="sxs-lookup"><span data-stu-id="df8de-359">An XPath expression specifying hello log toocollect.</span></span>|  
