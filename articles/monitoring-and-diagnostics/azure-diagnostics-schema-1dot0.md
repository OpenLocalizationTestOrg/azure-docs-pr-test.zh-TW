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
# <a name="azure-diagnostics-10-configuration-schema"></a>Azure 診斷 1.0 組態結構描述
> [!NOTE]
> Azure 診斷是 hello 用元件 toocollect 效能計數器和其他統計資料從 Azure 虛擬機器、 虛擬機器擴展集、 Service Fabric 和雲端服務。  此頁面只在您使用其中一個服務時才相關。
>

Azure 診斷要與 Azure 監視器、Application Insights 和 Log Analytics 等其他 Microsoft 診斷產品搭配使用。

hello Azure 診斷組態檔會定義使用的 tooinitialize hello 診斷監視器的值。 Hello 診斷監視器啟動時，這個檔案是使用的 tooinitialize 診斷的組態設定。  

 根據預設，hello Azure 診斷組態結構描述檔案是安裝的 toohello`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas`目錄。 取代`<version>`hello 安裝版的 hello 與[Azure SDK](http://www.windowsazure.com/develop/downloads/)。  

> [!NOTE]
>  hello 診斷組態檔通常搭配需要稍早在 hello 啟動程序中收集的診斷資料 toobe 的啟動工作。 如需使用 Azure 診斷的詳細資訊，請參閱[使用 Azure 診斷收集記錄資料](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7)。  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Hello 診斷組態檔的範例  
 下列範例中的 hello 顯示一般的診斷組態檔：  

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

## <a name="diagnosticsconfiguration-namespace"></a>DiagnosticsConfiguration 命名空間  
 hello hello 診斷組態檔的 XML 命名空間為：  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a>結構描述元素  
 hello 診斷組態檔包含下列項目 hello。


## <a name="diagnosticmonitorconfiguration-element"></a>DiagnosticMonitorConfiguration 元素  
hello hello 診斷組態檔的最上層項目。  

屬性：

|屬性  |類型   |必要| 預設值 | 說明|  
|-----------|-------|--------|---------|------------|  
|**configurationChangePollInterval**|duration|選用 | PT1M| 指定 hello 間隔的 hello 診斷監視器輪詢診斷組態變更。|  
|**overallQuotaInMB**|unsignedInt|選用| 4000 MB。 如果您提供值，該值不能超過此數量 |hello 的檔案系統儲存體的所有記錄緩衝區配置的總容量。|  

## <a name="diagnosticinfrastructurelogs-element"></a>DiagnosticInfrastructureLogs 元素  
定義 hello hello hello 基礎診斷基礎結構所產生的記錄檔的緩衝區組態。

父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。  

屬性：

|屬性|類型|說明|  
|---------|----|-----------------|  
|**bufferQuotaInMB**|unsignedInt|選用。 指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。<br /><br /> hello 預設值為 0。|  
|**scheduledTransferLogLevelFilter**|字串|選用。 指定最低嚴重性層級 hello 傳送的記錄項目。 hello 預設值是**Undefined**。 其他可能的值為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。|  
|**scheduledTransferPeriod**|duration|選用。 指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。<br /><br /> hello 預設值是 PT0S。|  

## <a name="logs-element"></a>Logs 元素  
 定義基本 Azure 記錄檔的 hello 緩衝區組態。

 父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。  

屬性：  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|選用。 指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。<br /><br /> hello 預設值為 0。|  
|**scheduledTransferLogLevelFilter**|字串|選用。 指定最低嚴重性層級 hello 傳送的記錄項目。 hello 預設值是**Undefined**。 其他可能的值為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。|  
|**scheduledTransferPeriod**|duration|選用。 指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。<br /><br /> hello 預設值是 PT0S。|  

## <a name="directories-element"></a>Directories 元素  
定義您可以定義檔案式記錄檔的 hello 緩衝區組態。

父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。  


屬性：  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|選用。 指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。<br /><br /> hello 預設值為 0。|  
|**scheduledTransferPeriod**|duration|選用。 指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。<br /><br /> hello 預設值是 PT0S。|  

## <a name="crashdumps-element"></a>CrashDumps 元素  
 定義 hello 損毀傾印目錄。

 父元素︰[Directories 元素](#Directories)。  

屬性：  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**container**|字串|傳送 hello 容器是 hello 目錄 hello 內容 toobe hello 名稱。|  
|**directoryQuotaInMB**|unsignedInt|選用。 指定 hello hello 目錄的大小上限以 mb 為單位。<br /><br /> hello 預設值為 0。|  

## <a name="failedrequestlogs-element"></a>FailedRequestLogs 元素  
 定義 hello 失敗的要求記錄檔目錄。

 父元素︰[Directories 元素](#Directories)。  

屬性：  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**container**|字串|傳送 hello 容器是 hello 目錄 hello 內容 toobe hello 名稱。|  
|**directoryQuotaInMB**|unsignedInt|選用。 指定 hello hello 目錄的大小上限以 mb 為單位。<br /><br /> hello 預設值為 0。|  

##  <a name="iislogs-element"></a>IISLogs 元素  
 定義 hello IIS 記錄檔目錄。

 父元素︰[Directories 元素](#Directories)。  

屬性：  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**container**|字串|傳送 hello 容器是 hello 目錄 hello 內容 toobe hello 名稱。|  
|**directoryQuotaInMB**|unsignedInt|選用。 指定 hello hello 目錄的大小上限以 mb 為單位。<br /><br /> hello 預設值為 0。|  

## <a name="datasources-element"></a>DataSources 元素  
 定義零或多個額外的記錄目錄。

 父元素︰[Directories 元素](#Directories)。

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration 元素  
 定義記錄檔 toomonitor hello 的目錄。

 父元素︰[DataSources 元素](#DataSources)。

屬性：

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**container**|字串|傳送 hello 容器是 hello 目錄 hello 內容 toobe hello 名稱。|  
|**directoryQuotaInMB**|unsignedInt|選用。 指定 hello hello 目錄的大小上限以 mb 為單位。<br /><br /> hello 預設值為 0。|  

## <a name="absolute-element"></a>Absolute 元素  
 定義選擇性環境展開 hello 目錄 toomonitor 的絕對路徑。

 父元素：[DirectoryConfiguration 元素](#DirectoryConfiguration)。  

屬性：  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**路徑**|字串|必要。 絕對路徑 toohello 目錄 toomonitor hello。|  
|**expandEnvironment**|布林值|必要。 如果設定太**true**，hello 路徑中的環境變數會展開。|  

## <a name="localresource-element"></a>LocalResource 元素  
 定義在 hello 服務定義中定義之路徑的相對 tooa 本機資源。

 父元素：[DirectoryConfiguration 元素](#DirectoryConfiguration)。  

屬性：  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**name**|字串|必要。 hello 包含 hello 目錄 toomonitor hello 本機資源的名稱。|  
|**relativePath**|字串|必要。 hello 路徑相對 toohello 本機資源 toomonitor。|  

## <a name="performancecounters-element"></a>PerformanceCounters 元素  
 定義 hello 路徑 toohello 效能計數器 toocollect。

 父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。


 屬性：  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|選用。 指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。<br /><br /> hello 預設值為 0。|  
|**scheduledTransferPeriod**|duration|選用。 指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。<br /><br /> hello 預設值是 PT0S。|  

## <a name="performancecounterconfiguration-element"></a>PerformanceCounterConfiguration 元素  
 定義 hello 效能計數器 toocollect。

 父元素︰[PerformanceCounters 元素](#PerformanceCounters)。  

 屬性：  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**counterSpecifier**|字串|必要。 hello 路徑 toohello 效能計數器 toocollect。|  
|**sampleRate**|duration|必要。 您應該在哪一個 hello 收集效能計數器的 hello 速率。|  

## <a name="windowseventlog-element"></a>WindowsEventLog 元素  
 定義 hello 事件記錄檔 toomonitor。

 父元素：[DiagnosticMonitorConfiguration 元素](#DiagnosticMonitorConfiguration)。

  屬性：

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|選用。 指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。<br /><br /> hello 預設值為 0。|  
|**scheduledTransferLogLevelFilter**|字串|選用。 指定最低嚴重性層級 hello 傳送的記錄項目。 hello 預設值是**Undefined**。 其他可能的值為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。|  
|**scheduledTransferPeriod**|duration|選用。 指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。<br /><br /> hello 預設值是 PT0S。|  

## <a name="datasource-element"></a>DataSource 元素  
 定義 hello 事件記錄檔 toomonitor。

 父元素︰[WindowsEventLog 元素](#windowsEventLog)。  

 屬性：

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**name**|字串|必要。 指定 hello 記錄 toocollect XPath 運算式。|  
