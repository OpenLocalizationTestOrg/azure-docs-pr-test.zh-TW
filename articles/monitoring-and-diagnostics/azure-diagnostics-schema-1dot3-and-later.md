---
title: "aaaAzure 診斷延伸模組 1.3 和更新版本的組態結構描述 |Microsoft 文件"
description: "結構描述版本 1.3 和更新版本的 Azure 診斷出貨 hello Microsoft Azure SDK 2.4 和更新版本的一部分。"
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
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a>Azure 診斷 1.3 版和更新版本的組態結構描述
> [!NOTE]
> hello Azure 診斷擴充功能是 hello 元件使用 toocollect 效能計數器和其他統計資料：
> - Azure 虛擬機器 
> - 虛擬機器擴展集
> - Service Fabric 
> - 雲端服務 
> - 網路安全性群組
> 
> 此頁面只在您使用其中一個服務時才相關。

此頁面適用於 1.3 版和更新版本 (Azure SDK 2.4 版和更新版本)。 較新的組態區段會加上註解的 tooshow 中加入哪個版本。  

此處所述的 hello 設定檔 hello 診斷監視器啟動時使用的 tooset 診斷的組態設定。  

Azure 監視、 Application Insights 和記錄分析等其他 Microsoft 診斷產品搭配使用 hello 延伸。



藉由執行下列 PowerShell 命令的 hello 下載 hello 公用組態檔結構描述定義：  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

如需有關使用 Azure 診斷的詳細資訊，請參閱 [Azure 診斷擴充功能](azure-diagnostics.md)。  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Hello 診斷組態檔的範例  
 下列範例中的 hello 顯示一般的診斷組態檔：  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
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
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
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

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

JSON 等於 hello 先前 XML 組態檔。 

因為大部分的 json 使用量情況下，它們做為傳遞不同的變數的 hello PublicConfig 和 PrivateConfig 是區隔。 這些案例包括 Resource Manager 範本、虛擬機器擴展集 PowerShell 和 Visual Studio。 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "ApplicationInsights",
                    "ApplicationInsights": "{Insert InstrumentationKey}",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a>閱讀本頁面  
 hello 下列標記的大致順序 hello 前面範例所示。  如果您沒有您預期會看到完整描述，搜尋 hello 頁面 hello 項目或屬性。  

## <a name="common-attribute-types"></a>一般屬性類型  
 **scheduledTransferPeriod** 屬性會出現在數個元素中。 它是 hello 排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘的間隔。 hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp)


## <a name="diagnosticsconfiguration-element"></a>DiagnosticsConfiguration 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration

已在 1.3 版中新增。  

hello hello 診斷組態檔的最上層項目。  

**屬性**xmlns-hello XML 命名空間，hello 診斷組態檔為：  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  


|子元素|說明|  
|--------------------|-----------------|  
|**PublicConfig**|必要。 請參閱本頁面上其他部分的說明。|  
|**PrivateConfig**|選用。 請參閱本頁面上其他部分的說明。|  
|**IsEnabled**|布林值。 請參閱本頁面上其他部分的說明。|  

## <a name="publicconfig-element"></a>PublicConfig 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig

 描述 hello 公用診斷組態。  

|子元素|說明|  
|--------------------|-----------------|  
|**WadCfg**|必要。 請參閱本頁面上其他部分的說明。|  
|**StorageAccount**|hello 的 hello Azure 儲存體帳戶 toostore hello 資料中的名稱。 可能時，也指定做為參數執行 hello 組 AzureServiceDiagnosticsExtension cmdlet。|  
|**StorageType**|可以是 Table、Blob 或 TableAndBlob。 預設值是 Table。 當選定 TableAndBlob 時，診斷資料會寫入兩次一次 tooeach 型別。|  
|**LocalResourceDirectory**|hello hello hello 監視代理程式儲存事件資料之處的虛擬機器上的目錄。 如果沒有，請設定，請使用 hello 預設目錄：<br /><br /> 針對背景工作/web 角色：`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> 針對虛擬機器：`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> 必要屬性包括：<br /><br /> - **路徑**-hello Azure 診斷使用的 hello 系統 toobe 目錄。<br /><br /> - **expandEnvironment** -控制 hello 路徑名稱中是否會展開環境變數。|  

## <a name="wadcfg-element"></a>WadCFG 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG
 
 識別，並設定 hello 遙測資料 toobe 收集。  


## <a name="diagnosticmonitorconfiguration-element"></a>DiagnosticMonitorConfiguration 元素 
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration

 必要 

|屬性|說明|  
|----------------|-----------------|  
| **overallQuotaInMB** | hello 可供 hello 的本機磁碟空間數量最大 Azure 診斷所收集的診斷資料的各種類型。 hello 預設設定為 5120 MB。<br />
|**useProxyServer** | 在 IE 設定中設定 Azure 診斷 toouse hello proxy 伺服器設定。|  

<br /> <br />

|子元素|說明|  
|--------------------|-----------------|  
|**CrashDumps**|請參閱本頁面上其他部分的說明。|  
|**DiagnosticInfrastructureLogs**|啟用收集 Azure 診斷所產生的記錄。 hello 診斷基礎結構記錄檔可用於疑難排解 hello 診斷系統本身。 選用屬性包括：<br /><br /> - **scheduledTransferLogLevelFilter** -設定 hello 最低嚴重性層級的 hello 所收集的記錄檔。<br /><br /> - **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Directories**|請參閱本頁面上其他部分的說明。|  
|**EtwProviders**|請參閱本頁面上其他部分的說明。|  
|**計量**|請參閱本頁面上其他部分的說明。|  
|**PerformanceCounters**|請參閱本頁面上其他部分的說明。|  
|**WindowsEventLog**|請參閱本頁面上其他部分的說明。| 
|**DockerSources**|請參閱本頁面上其他部分的說明。 | 



## <a name="crashdumps-element"></a>CrashDumps 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps
 
 啟用損毀傾印 hello 集合。  

|屬性|說明|  
|----------------|-----------------|  
|**containerName**|選用。 在您的 Azure 儲存體帳戶 toobe hello blob 容器 hello 名稱使用 toostore 損毀傾印。|  
|**crashDumpType**|選用。  設定 Azure 診斷 toocollect 迷你或完整損毀傾印。|  
|**directoryQuotaPercentage**|選用。  設定 hello 百分比**overallQuotaInMB** toobe 保留給 hello VM 上的損毀傾印。|  

|子元素|說明|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|必要。 定義每個處理序的組態值。<br /><br /> 下列屬性的 hello 也是必要的：<br /><br /> **processName** -hello hello 您想要 Azure 診斷 toocollect 損毀傾印的處理程序的名稱。|  

## <a name="directories-element"></a>Directories 元素 
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories

 啟用 hello hello 的目錄內容的集合，IIS 無法存取要求記錄檔及/或 IIS 記錄檔。  

 選用的 **scheduledTransferPeriod** 屬性。 請參閱稍早的說明。  

|子元素|說明|  
|--------------------|-----------------|  
|**IISLogs**|Hello 組態中包含這個項目可讓 hello 收集 IIS 記錄檔：<br /><br /> **containerName** -hello blob 容器，在您的 Azure 儲存體帳戶 toobe hello 名稱使用 toostore hello IIS 記錄檔。|   
|**FailedRequestLogs**|這個項目包括 hello 組態中啟用有關失敗的要求 tooan IIS 網站或應用程式記錄檔集合。 您也必須在 **Web.config** 的 **system.WebServer** 下啟用追蹤選項。|  
|**DataSources**|目錄 toomonitor 清單。| 




## <a name="datasources-element"></a>DataSources 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources

 目錄 toomonitor 清單。  

|子元素|說明|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|必要。 必要屬性：<br /><br /> **containerName** -hello hello Azure 儲存體帳戶的 toobe 使用 toostore hello 記錄檔中的 blob 容器的名稱。|  





## <a name="directoryconfiguration-element"></a>DirectoryConfiguration 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration

 可能包含任一 hello**絕對**或**LocalResource**項目，但非兩者。  

|子元素|說明|  
|--------------------|-----------------|  
|**Absolute**|絕對路徑 toohello 目錄 toomonitor hello。 hello 下列屬性是必要的：<br /><br /> - **路徑**-hello 絕對路徑 toohello 目錄 toomonitor。<br /><br /> - **expandEnvironment** - 設定是否要展開 Path 中的環境變數。|  
|**LocalResource**|hello 路徑相對 tooa 本機資源 toomonitor。 必要屬性包括：<br /><br /> - **名稱**-hello 包含 hello 目錄 toomonitor 的本機資源<br /><br /> - **relativePath** -hello 路徑相對 tooName 包含 hello 目錄 toomonitor|  



## <a name="etwproviders-element"></a>EtwProviders 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders

 設定要收集來自 EventSource 和/或以 ETW 資訊清單為基礎之提供者的 ETW 事件。  

|子元素|說明|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|設定要收集從 [EventSource 類別](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)產生的事件。 必要屬性：<br /><br /> **提供者**-hello hello EventSource 事件類別名稱。<br /><br /> 選用屬性包括：<br /><br /> - **scheduledTransferLogLevelFilter** -hello 最低嚴重性層級 tootransfer tooyour 儲存體帳戶。<br /><br /> - **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|必要屬性：<br /><br /> **提供者**-hello hello 事件提供者的 GUID<br /><br /> 選用屬性包括：<br /><br /> - **scheduledTransferLogLevelFilter** -hello 最低嚴重性層級 tootransfer tooyour 儲存體帳戶。<br /><br /> - **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration

 設定要收集從 [EventSource 類別](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)產生的事件。  

|子元素|說明|  
|--------------------|-----------------|  
|**DefaultEvents**|選用屬性：<br/><br/> **eventDestination** -hello hello 資料表 toostore hello 中的事件名稱|  
|**Event**|必要屬性：<br /><br /> **識別碼**-hello 事件識別碼 hello。<br /><br /> 選用屬性：<br /><br /> **eventDestination** -hello hello 資料表 toostore hello 中的事件名稱|  



## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration

|子元素|說明|  
|--------------------|-----------------|  
|**DefaultEvents**|選用屬性：<br /><br /> **eventDestination** -hello hello 資料表 toostore hello 中的事件名稱|  
|**Event**|必要屬性：<br /><br /> **識別碼**-hello 事件識別碼 hello。<br /><br /> 選用屬性：<br /><br /> **eventDestination** -hello hello 資料表 toostore hello 中的事件名稱|  



## <a name="metrics-element"></a>Metrics 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics

 可讓您 toogenerate 最適合用於快速查詢的效能計數器資料表。 Hello 中定義每個效能計數器**PerformanceCounters**項目會儲存在加法 toohello 效能計數器資料表中的 hello 度量資料表。  

 hello **resourceId**是必要屬性。  hello hello 您要部署至 Azure 診斷的虛擬機器的資源識別碼。 取得 hello **resourceID**從 hello [Azure 入口網站](https://portal.azure.com)。 選取 [瀏覽][資源群組] ->  -> **<Name\>**。 按一下 hello**屬性**磚，然後從 hello 複製 hello 值**識別碼**欄位。  

|子元素|說明|  
|--------------------|-----------------|  
|**MetricAggregation**|必要屬性：<br /><br /> **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。 hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="performancecounters-element"></a>PerformanceCounters 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters

 啟用效能計數器 hello 集合。  

 選用屬性：  

 選用的 **scheduledTransferPeriod** 屬性。 請參閱稍早的說明。

|子元素|說明|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|hello 下列屬性是必要的：<br /><br /> - **counterSpecifier** -hello hello 效能計數器的名稱。 例如： `\Processor(_Total)\% Processor Time`。 tooget 一份效能計數器，您在主機上，執行 hello 命令`typeperf`。<br /><br /> - **sampleRate** -頻率 hello 應該取樣。<br /><br /> 選用屬性：<br /><br /> **單位**-hello hello 計數器的測量單位。|  




## <a name="windowseventlog-element"></a>WindowsEventLog 元素
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog
 
 啟用 hello 集合的 「 Windows 事件記錄檔。  

 選用的 **scheduledTransferPeriod** 屬性。 請參閱稍早的說明。  

|子元素|說明|  
|-------------------|-----------------|  
|**DataSource**|hello Windows 事件記錄檔 toocollect。 必要屬性：<br /><br /> **名稱**-收集描述 hello windows 事件 toobe hello XPath 查詢。 例如：<br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> toocollect 所有事件，都指定"*"|  




## <a name="logs-element"></a>Logs 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs

 出現在 1.0 和 1.1 版中。 在 1.2 中消失。 再度新增於 1.3 中。  

 定義基本 Azure 記錄檔的 hello 緩衝區組態。  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|選用。 指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。<br /><br /> hello 預設值為 0。|  
|**scheduledTransferLogLevelFilterr**|**字串**|選用。 指定最低嚴重性層級 hello 傳送的記錄項目。 hello 預設值是**Undefined**，傳輸的所有記錄。 其他可能的值 （依順序的最多 tooleast 資訊） 為**Verbose**，**資訊**，**警告**，**錯誤**，和**重大**。|  
|**scheduledTransferPeriod**|**duration**|選用。 指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。<br /><br /> hello 預設值是 PT0S。|  
|**sinks** 已在 1.5 中新增|**字串**|選用。 點 tooa 接收位置 tooalso 傳送診斷資料。 例如 Application Insights。|  

## <a name="dockersources"></a>DockerSources
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources

 已在 1.9 版中新增。

|元素名稱|說明|  
|------------------|-----------------|  
|**Stats**|會告知 hello 系統 toocollect Docker 容器的統計資料|  

## <a name="sinksconfig-element"></a>SinksConfig 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig

 位置 toosend 診斷資料 tooand hello 組態與那些位置相關聯的清單。  

|元素名稱|說明|  
|------------------|-----------------|  
|**接收**|請參閱本頁面上其他部分的說明。|  

## <a name="sink-element"></a>Sink 元素
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink

 已在 1.5 版中新增。  

 定義位置 toosend 診斷資料。 例如，hello Application Insights 服務。  

|屬性|類型|說明|  
|---------------|----------|-----------------|  
|**name**|字串|字串識別 hello sinkname。|  

|元素|類型|說明|  
|-------------|----------|-----------------|  
|**Application Insights**|字串|只有在傳送資料 tooApplication Insights 時，才使用。 包含 hello 檢測金鑰的使用中的 Application Insights 帳戶具有存取權。|  
|**Channels**|字串|每個可額外篩選該資料流的其中一個|  

## <a name="channels-element"></a>Channels 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels

 已在 1.5 版中新增。  

 針對通過接收之記錄資料的資料流定義篩選器。  

|元素|類型|說明|  
|-------------|----------|-----------------|  
|**Channel**|字串|請參閱本頁面上其他部分的說明。|  

## <a name="channel-element"></a>Channel 元素
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel

 已在 1.5 版中新增。  

 定義位置 toosend 診斷資料。 例如，hello Application Insights 服務。  

|屬性|類型|說明|  
|----------------|----------|-----------------|  
|**logLevel**|**字串**|指定最低嚴重性層級 hello 傳送的記錄項目。 hello 預設值是**Undefined**，傳輸的所有記錄。 其他可能的值 （依順序的最多 tooleast 資訊） 為**Verbose**，**資訊**，**警告**，**錯誤**，和**重大**。|  
|**name**|**字串**|Hello 通道 toorefer 以唯一的名稱|  


## <a name="privateconfig-element"></a>PrivateConfig 元素 
 樹狀結構︰根目錄 - DiagnosticsConfiguration - PrivateConfig

 已在 1.3 版中新增。  

 選用  

 儲存 hello hello 儲存體帳戶 （名稱、 金鑰和端點） 的私用詳細資料。 這項資訊會傳送 toohello 虛擬機器，但無法從其擷取。  

|子元素|說明|  
|--------------------|-----------------|  
|**StorageAccount**|hello 儲存體帳戶 toouse。 所需的下列屬性的 hello<br /><br /> - **名稱**-hello hello 儲存體帳戶的名稱。<br /><br /> - **索引鍵**-hello 金鑰 toohello 儲存體帳戶。<br /><br /> - **端點**-hello 端點 tooaccess hello 儲存體帳戶。 <br /><br /> -**sasToken** （加入 1.8.1)-您可以在 hello 私用組態中指定的 SAS 權杖，而不是儲存體帳戶金鑰。如果提供，則會忽略 hello 儲存體帳戶金鑰。 <br />Hello SAS 權杖的需求： <br />- 僅支援帳戶 SAS 權杖 <br />- 需要 b、t 服務類型。 <br /> - 需要 a、c、u、w 權限。 <br /> - 需要 c、o 資源類型。 <br /> -支援 hello HTTPS 通訊協定 <br /> - 開始和到期時間必須是有效的。|  


## <a name="isenabled-element"></a>IsEnabled 元素  
 樹狀結構︰根目錄 - DiagnosticsConfiguration - IsEnabled

 布林值。 使用`true`tooenable hello 診斷或`false`toodisable hello 診斷。
