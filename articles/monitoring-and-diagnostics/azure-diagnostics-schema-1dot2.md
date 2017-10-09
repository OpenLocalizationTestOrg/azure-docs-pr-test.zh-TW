---
title: "aaaAzure 診斷 1.2 組態結構描述 |Microsoft 文件"
description: "如果您是搭配 Azure 虛擬機器、虛擬機器擴展集、Service Fabric 或雲端服務使用 Azure SDK 2.5 才相關。"
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
ms.openlocfilehash: 31559317b696556a64b51b58800b176ade9a4679
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-12-configuration-schema"></a>Azure 診斷 1.2 組態結構描述
> [!NOTE]
> Azure 診斷是 hello 用元件 toocollect 效能計數器和其他統計資料從 Azure 虛擬機器、 虛擬機器擴展集、 Service Fabric 和雲端服務。  此頁面只在您使用其中一個服務時才相關。
>

Azure 診斷要與 Azure 監視器、Application Insights 和 Log Analytics 等其他 Microsoft 診斷產品搭配使用。

此結構描述定義 hello hello 診斷監視器啟動時，您可以使用 tooinitialize 診斷組態設定可能的值。  


 藉由執行下列 PowerShell 命令的 hello 下載 hello 公用組態檔結構描述定義：  

```PowerShell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 如需 Azure 診斷的詳細資訊，請參閱[在 Azure 雲端服務中啟用診斷](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/)。  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Hello 診斷組態檔的範例  
 下列範例中的 hello 顯示一般的診斷組態檔：  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">  
  <WadCfg>  
    <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  
      <PerformanceCounters scheduledTransferPeriod="PT1M">  
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
      </PerformanceCounters>  
      <Directories scheduledTransferPeriod="PT5M">  
        <IISLogs containerName="iislogs" />  
        <FailedRequestLogs containerName="iisfailed" />  
        <DataSources>  
          <DirectoryConfiguration containerName="mynewprocess">  
            <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
          </DirectoryConfiguration>  
          <DirectoryConfiguration containerName="badapp">  
            <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
          </DirectoryConfiguration>  
          <DirectoryConfiguration containerName="goodapp">  
            <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
          </DirectoryConfiguration>  
        </DataSources>  
      </Directories>  
      <EtwProviders>  
        <EtwEventSourceProviderConfiguration provider="MyProviderClass" scheduledTransferPeriod="PT5M">  
          <Event id="0"/>  
          <Event id="1" eventDestination="errorTable"/>  
          <DefaultEvents />  
        </EtwEventSourceProviderConfiguration>  
        <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
          <Event id="0"/>  
          <DefaultEvents eventDestination="defaultTable"/>  
        </EtwManifestProviderConfiguration>  
      </EtwProviders>  
      <WindowsEventLog scheduledTransferPeriod="PT5M">  
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
        <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
        <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
      </WindowsEventLog>  
      <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
        <CrashDumpConfiguration processName="mynewprocess.exe" />  
        <CrashDumpConfiguration processName="badapp.exe"/>  
      </CrashDumps>  
    </DiagnosticMonitorConfiguration>  
  </WadCfg>  
</PublicConfig>  

```  

## <a name="diagnostics-configuration-namespace"></a>診斷組態命名空間  
 hello hello 診斷組態檔的 XML 命名空間為：  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="publicconfig-element"></a>PublicConfig 元素  
 Hello 診斷組態檔的最上層元素。 hello 下表描述 hello hello 組態檔項目。  

|元素名稱|說明|  
|------------------|-----------------|  
|**WadCfg**|必要。 收集 hello 遙測資料 toobe 的組態設定。|  
|**StorageAccount**|hello 的 hello Azure 儲存體帳戶 toostore hello 資料中的名稱。 這可能也會指定為參數執行 hello 組 AzureServiceDiagnosticsExtension cmdlet 時。|  
|**LocalResourceDirectory**|hello hello 虛擬機器 toobe 上使用目錄 hello Monitoring Agent toostore 事件資料。 如果未設定，hello 預設目錄使用：<br /><br /> 針對背景工作/web 角色：`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> 針對虛擬機器：`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> 必要屬性包括：<br /><br /> -                      **路徑**-hello Azure 診斷使用的 hello 系統 toobe 目錄。<br /><br /> -                      **expandEnvironment** -控制 hello 路徑名稱中是否會展開環境變數。|  

## <a name="wadcfg-element"></a>WadCFG 元素  
定義 hello 收集的遙測資料 toobe 的組態設定。 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|必要。 選用屬性包括：<br /><br /> -                     **overallQuotaInMB** -Azure 診斷所收集的 hello 可供 hello 的本機磁碟空間數量最大各種類型的診斷資料。 hello 預設設定為 5120 MB。<br /><br /> -                     **useProxyServer** -設定 Azure 診斷 toouse hello proxy 伺服器設定在 IE 設定中。|  
|**CrashDumps**|啟用收集損毀傾印。 選用屬性包括：<br /><br /> -                     **containerName** -hello blob 容器，在您的 Azure 儲存體帳戶 toobe hello 名稱使用 toostore 損毀傾印。<br /><br /> -                     **crashDumpType** -設定 Azure 診斷 toocollect 迷你] 或 [完整損毀傾印。<br /><br /> -                     **directoryQuotaPercentage**-設定 hello 百分比**overallQuotaInMB** toobe 保留給 hello VM 上的損毀傾印。|  
|**DiagnosticInfrastructureLogs**|啟用收集 Azure 診斷所產生的記錄。 hello 診斷基礎結構記錄檔可用於疑難排解 hello 診斷系統本身。 選用屬性包括：<br /><br /> -                     **scheduledTransferLogLevelFilter** -設定 hello 最低嚴重性層級的 hello 所收集的記錄檔。<br /><br /> -                     **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**Directories**|啟用 hello hello 的目錄內容的集合，IIS 無法存取要求記錄檔及/或 IIS 記錄檔。 選用屬性：<br /><br /> **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**EtwProviders**|設定要收集來自 EventSource 和/或以 ETW 資訊清單為基礎之提供者的 ETW 事件。|  
|**計量**|這個項目可讓您 toogenerate 最適合用於快速查詢的效能計數器資料表。 Hello 中定義每個效能計數器**PerformanceCounters**項目會儲存在加法 toohello 效能計數器資料表中的 hello 度量資料表。 必要屬性：<br /><br /> **resourceId** -這是 hello hello 您要部署至 Azure 診斷的虛擬機器的資源識別碼。 取得 hello **resourceID**從 hello [Azure 入口網站](https://portal.azure.com)。 選取 [瀏覽][資源群組] ->  -> **<Name\>**。 按一下 hello**屬性**磚，然後從 hello 複製 hello 值**識別碼**欄位。|  
|**PerformanceCounters**|啟用效能計數器 hello 集合。 選用屬性：<br /><br /> **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 值是 [XML「持續時間資料類型」(英文)](http://www.w3schools.com/schema/schema_dtypes_date.asp)。|  
|**WindowsEventLog**|啟用 hello 集合的 「 Windows 事件記錄檔。 選用屬性：<br /><br /> **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 值是 [XML「持續時間資料類型」(英文)](http://www.w3schools.com/schema/schema_dtypes_date.asp)。|  

## <a name="crashdumps-element"></a>CrashDumps 元素  
 啟用收集損毀傾印。 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**CrashDumpConfiguration**|必要。 必要屬性：<br /><br /> **processName** -hello hello 您想要 Azure 診斷 toocollect 損毀傾印的處理程序的名稱。|  
|**crashDumpType**|設定 Azure 診斷 toocollect 迷你或完整損毀傾印。|  
|**directoryQuotaPercentage**|設定 hello 百分比**overallQuotaInMB** toobe 保留給 hello VM 上的損毀傾印。|  

## <a name="directories-element"></a>Directories 元素  
 啟用 hello hello 的目錄內容的集合，IIS 無法存取要求記錄檔及/或 IIS 記錄檔。 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**DataSources**|目錄 toomonitor 清單。|  
|**FailedRequestLogs**|這個項目包括 hello 組態中啟用有關失敗的要求 tooan IIS 網站或應用程式記錄檔集合。 您也必須在 **Web.config** 的 **system.WebServer** 下啟用追蹤選項。|  
|**IISLogs**|Hello 組態中包含這個項目可讓 hello 收集 IIS 記錄檔：<br /><br /> **containerName** -hello blob 容器，在您的 Azure 儲存體帳戶 toobe hello 名稱使用 toostore hello IIS 記錄檔。|  

## <a name="datasources-element"></a>DataSources 元素  
 目錄 toomonitor 清單。 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**DirectoryConfiguration**|必要。 必要屬性：<br /><br /> **containerName** -hello 名稱 hello blob 容器，在您的 Azure 儲存體帳戶使用 toobe toostore hello 記錄檔。|  

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration 元素  
 **DirectoryConfiguration**可能包含任一 hello**絕對**或**LocalResource**項目，但非兩者。 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**Absolute**|絕對路徑 toohello 目錄 toomonitor hello。 hello 下列屬性是必要的：<br /><br /> -                     **路徑**-hello 絕對路徑 toohello 目錄 toomonitor。<br /><br /> -                      **expandEnvironment** - 設定是否要展開 Path 中的環境變數。|  
|**LocalResource**|hello 路徑相對 tooa 本機資源 toomonitor。 必要屬性包括：<br /><br /> -                     **名稱**-hello 包含 hello 目錄 toomonitor 的本機資源<br /><br /> -                     **relativePath** -hello 路徑相對 tooName 包含 hello 目錄 toomonitor|  

## <a name="etwproviders-element"></a>EtwProviders 元素  
 設定要收集來自 EventSource 和/或以 ETW 資訊清單為基礎之提供者的 ETW 事件。 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|設定要收集從 [EventSource 類別](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)產生的事件。 必要屬性：<br /><br /> **提供者**-hello hello EventSource 事件類別名稱。<br /><br /> 選用屬性包括：<br /><br /> -                     **scheduledTransferLogLevelFilter** -hello 最低嚴重性層級 tootransfer tooyour 儲存體帳戶。<br /><br /> -                     **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 值是 [XML「持續時間資料類型」(英文)](http://www.w3schools.com/schema/schema_dtypes_date.asp)。|  
|**EtwManifestProviderConfiguration**|必要屬性：<br /><br /> **提供者**-hello hello 事件提供者的 GUID<br /><br /> 選用屬性包括：<br /><br /> - **scheduledTransferLogLevelFilter** -hello 最低嚴重性層級 tootransfer tooyour 儲存體帳戶。<br /><br /> -                     **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 值是 [XML「持續時間資料類型」(英文)](http://www.w3schools.com/schema/schema_dtypes_date.asp)。|  

## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration 元素  
 設定要收集從 [EventSource 類別](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)產生的事件。 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**DefaultEvents**|選用屬性：<br /><br /> **eventDestination** -hello hello 資料表 toostore hello 中的事件名稱|  
|**Event**|必要屬性：<br /><br /> **識別碼**-hello 事件識別碼 hello。<br /><br /> 選用屬性：<br /><br /> **eventDestination** -hello hello 資料表 toostore hello 中的事件名稱|  

## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration 元素  
 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**DefaultEvents**|選用屬性：<br /><br /> **eventDestination** -hello hello 資料表 toostore hello 中的事件名稱|  
|**Event**|必要屬性：<br /><br /> **識別碼**-hello 事件識別碼 hello。<br /><br /> 選用屬性：<br /><br /> **eventDestination** -hello hello 資料表 toostore hello 中的事件名稱|  

## <a name="metrics-element"></a>Metrics 元素  
 可讓您 toogenerate 最適合用於快速查詢的效能計數器資料表。 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**MetricAggregation**|必要屬性：<br /><br /> **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 值是 [XML「持續時間資料類型」(英文)](http://www.w3schools.com/schema/schema_dtypes_date.asp)。|  

## <a name="performancecounters-element"></a>PerformanceCounters 元素  
 啟用效能計數器 hello 集合。 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**PerformanceCounterConfiguration**|hello 下列屬性是必要的：<br /><br /> -                     **counterSpecifier** -hello hello 效能計數器的名稱。 例如： `\Processor(_Total)\% Processor Time`。 tooget 執行 hello 命令在您主機上的效能計數器清單`typeperf`。<br /><br /> -                     **sampleRate** -頻率 hello 應該取樣。<br /><br /> 選用屬性：<br /><br /> **單位**-hello hello 計數器的測量單位。|  

## <a name="performancecounterconfiguration-element"></a>PerformanceCounterConfiguration 元素  
 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**annotation**|必要屬性：<br /><br /> **displayName** -hello hello 計數器的顯示名稱<br /><br /> 選用屬性：<br /><br /> **地區設定**-hello toouse 地區設定時顯示 hello 計數器名稱|  

## <a name="windowseventlog-element"></a>WindowsEventLog 元素  
 hello 下表描述子元素：  

|元素名稱|說明|  
|------------------|-----------------|  
|**DataSource**|hello Windows 事件記錄檔 toocollect。 必要屬性：<br /><br /> **名稱**-收集描述 hello windows 事件 toobe hello XPath 查詢。 例如：<br /><br /> `Application!*[System[(Level >= 3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level >= 3]]`<br /><br /> toocollect 所有事件，都指定"*"。|
