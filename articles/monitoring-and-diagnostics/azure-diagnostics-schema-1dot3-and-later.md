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
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="0e940-103">Azure 診斷 1.3 版和更新版本的組態結構描述</span><span class="sxs-lookup"><span data-stu-id="0e940-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="0e940-104">hello Azure 診斷擴充功能是 hello 元件使用 toocollect 效能計數器和其他統計資料：</span><span class="sxs-lookup"><span data-stu-id="0e940-104">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="0e940-105">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0e940-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="0e940-106">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="0e940-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="0e940-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0e940-107">Service Fabric</span></span> 
> - <span data-ttu-id="0e940-108">雲端服務</span><span class="sxs-lookup"><span data-stu-id="0e940-108">Cloud Services</span></span> 
> - <span data-ttu-id="0e940-109">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="0e940-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="0e940-110">此頁面只在您使用其中一個服務時才相關。</span><span class="sxs-lookup"><span data-stu-id="0e940-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="0e940-111">此頁面適用於 1.3 版和更新版本 (Azure SDK 2.4 版和更新版本)。</span><span class="sxs-lookup"><span data-stu-id="0e940-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="0e940-112">較新的組態區段會加上註解的 tooshow 中加入哪個版本。</span><span class="sxs-lookup"><span data-stu-id="0e940-112">Newer configuration sections are commented tooshow in what version they were added.</span></span>  

<span data-ttu-id="0e940-113">此處所述的 hello 設定檔 hello 診斷監視器啟動時使用的 tooset 診斷的組態設定。</span><span class="sxs-lookup"><span data-stu-id="0e940-113">hello configuration file described here is used tooset diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

<span data-ttu-id="0e940-114">Azure 監視、 Application Insights 和記錄分析等其他 Microsoft 診斷產品搭配使用 hello 延伸。</span><span class="sxs-lookup"><span data-stu-id="0e940-114">hello extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="0e940-115">藉由執行下列 PowerShell 命令的 hello 下載 hello 公用組態檔結構描述定義：</span><span class="sxs-lookup"><span data-stu-id="0e940-115">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="0e940-116">如需有關使用 Azure 診斷的詳細資訊，請參閱 [Azure 診斷擴充功能](azure-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="0e940-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="0e940-117">Hello 診斷組態檔的範例</span><span class="sxs-lookup"><span data-stu-id="0e940-117">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="0e940-118">下列範例中的 hello 顯示一般的診斷組態檔：</span><span class="sxs-lookup"><span data-stu-id="0e940-118">hello following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="0e940-119">JSON 等於 hello 先前 XML 組態檔。</span><span class="sxs-lookup"><span data-stu-id="0e940-119">JSON equivalent of hello previous XML configuration file.</span></span> 

<span data-ttu-id="0e940-120">因為大部分的 json 使用量情況下，它們做為傳遞不同的變數的 hello PublicConfig 和 PrivateConfig 是區隔。</span><span class="sxs-lookup"><span data-stu-id="0e940-120">hello PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="0e940-121">這些案例包括 Resource Manager 範本、虛擬機器擴展集 PowerShell 和 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="0e940-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="0e940-122">閱讀本頁面</span><span class="sxs-lookup"><span data-stu-id="0e940-122">Reading this page</span></span>  
 <span data-ttu-id="0e940-123">hello 下列標記的大致順序 hello 前面範例所示。</span><span class="sxs-lookup"><span data-stu-id="0e940-123">hello tags following are roughly in order shown in hello preceding example.</span></span>  <span data-ttu-id="0e940-124">如果您沒有您預期會看到完整描述，搜尋 hello 頁面 hello 項目或屬性。</span><span class="sxs-lookup"><span data-stu-id="0e940-124">If you don't see a full description where you expect it, search hello page for hello element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="0e940-125">一般屬性類型</span><span class="sxs-lookup"><span data-stu-id="0e940-125">Common Attribute Types</span></span>  
 <span data-ttu-id="0e940-126">**scheduledTransferPeriod** 屬性會出現在數個元素中。</span><span class="sxs-lookup"><span data-stu-id="0e940-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="0e940-127">它是 hello 排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘的間隔。</span><span class="sxs-lookup"><span data-stu-id="0e940-127">It is hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="0e940-128">hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0e940-128">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="0e940-129">DiagnosticsConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="0e940-130">樹狀結構︰根目錄 - DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="0e940-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="0e940-131">已在 1.3 版中新增。</span><span class="sxs-lookup"><span data-stu-id="0e940-131">Added in version 1.3.</span></span>  

<span data-ttu-id="0e940-132">hello hello 診斷組態檔的最上層項目。</span><span class="sxs-lookup"><span data-stu-id="0e940-132">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="0e940-133">**屬性**xmlns-hello XML 命名空間，hello 診斷組態檔為：</span><span class="sxs-lookup"><span data-stu-id="0e940-133">**Attribute**  xmlns - hello XML namespace for hello diagnostics configuration file is:</span></span>  
<span data-ttu-id="0e940-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="0e940-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="0e940-135">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-135">Child Elements</span></span>|<span data-ttu-id="0e940-136">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="0e940-137">**PublicConfig**</span></span>|<span data-ttu-id="0e940-138">必要。</span><span class="sxs-lookup"><span data-stu-id="0e940-138">Required.</span></span> <span data-ttu-id="0e940-139">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0e940-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="0e940-140">**PrivateConfig**</span></span>|<span data-ttu-id="0e940-141">選用。</span><span class="sxs-lookup"><span data-stu-id="0e940-141">Optional.</span></span> <span data-ttu-id="0e940-142">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0e940-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="0e940-143">**IsEnabled**</span></span>|<span data-ttu-id="0e940-144">布林值。</span><span class="sxs-lookup"><span data-stu-id="0e940-144">Boolean.</span></span> <span data-ttu-id="0e940-145">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="0e940-146">PublicConfig 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-146">PublicConfig Element</span></span>  
 <span data-ttu-id="0e940-147">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig</span><span class="sxs-lookup"><span data-stu-id="0e940-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="0e940-148">描述 hello 公用診斷組態。</span><span class="sxs-lookup"><span data-stu-id="0e940-148">Describes hello public diagnostics configuration.</span></span>  

|<span data-ttu-id="0e940-149">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-149">Child Elements</span></span>|<span data-ttu-id="0e940-150">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="0e940-151">**WadCfg**</span></span>|<span data-ttu-id="0e940-152">必要。</span><span class="sxs-lookup"><span data-stu-id="0e940-152">Required.</span></span> <span data-ttu-id="0e940-153">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0e940-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="0e940-154">**StorageAccount**</span></span>|<span data-ttu-id="0e940-155">hello 的 hello Azure 儲存體帳戶 toostore hello 資料中的名稱。</span><span class="sxs-lookup"><span data-stu-id="0e940-155">hello name of hello Azure Storage account toostore hello data in.</span></span> <span data-ttu-id="0e940-156">可能時，也指定做為參數執行 hello 組 AzureServiceDiagnosticsExtension cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0e940-156">May also be specified as a parameter when executing hello Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="0e940-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="0e940-157">**StorageType**</span></span>|<span data-ttu-id="0e940-158">可以是 Table、Blob 或 TableAndBlob。</span><span class="sxs-lookup"><span data-stu-id="0e940-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="0e940-159">預設值是 Table。</span><span class="sxs-lookup"><span data-stu-id="0e940-159">Table is default.</span></span> <span data-ttu-id="0e940-160">當選定 TableAndBlob 時，診斷資料會寫入兩次一次 tooeach 型別。</span><span class="sxs-lookup"><span data-stu-id="0e940-160">When TableAndBlob is chosen, diagnostic data is written twice -- once tooeach type.</span></span>|  
|<span data-ttu-id="0e940-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="0e940-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="0e940-162">hello hello hello 監視代理程式儲存事件資料之處的虛擬機器上的目錄。</span><span class="sxs-lookup"><span data-stu-id="0e940-162">hello directory on hello virtual machine where hello Monitoring Agent stores event data.</span></span> <span data-ttu-id="0e940-163">如果沒有，請設定，請使用 hello 預設目錄：</span><span class="sxs-lookup"><span data-stu-id="0e940-163">If not, set, hello default directory is used:</span></span><br /><br /> <span data-ttu-id="0e940-164">針對背景工作/web 角色：`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="0e940-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="0e940-165">針對虛擬機器：`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="0e940-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="0e940-166">必要屬性包括：</span><span class="sxs-lookup"><span data-stu-id="0e940-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="0e940-167">- **路徑**-hello Azure 診斷使用的 hello 系統 toobe 目錄。</span><span class="sxs-lookup"><span data-stu-id="0e940-167">- **path** - hello directory on hello system toobe used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="0e940-168">- **expandEnvironment** -控制 hello 路徑名稱中是否會展開環境變數。</span><span class="sxs-lookup"><span data-stu-id="0e940-168">- **expandEnvironment** - Controls whether environment variables are expanded in hello path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="0e940-169">WadCFG 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-169">WadCFG Element</span></span>  
 <span data-ttu-id="0e940-170">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG</span><span class="sxs-lookup"><span data-stu-id="0e940-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="0e940-171">識別，並設定 hello 遙測資料 toobe 收集。</span><span class="sxs-lookup"><span data-stu-id="0e940-171">Identifies and configures hello telemetry data toobe collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="0e940-172">DiagnosticMonitorConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="0e940-173">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="0e940-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="0e940-174">必要</span><span class="sxs-lookup"><span data-stu-id="0e940-174">Required</span></span> 

|<span data-ttu-id="0e940-175">屬性</span><span class="sxs-lookup"><span data-stu-id="0e940-175">Attributes</span></span>|<span data-ttu-id="0e940-176">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="0e940-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0e940-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="0e940-178">hello 可供 hello 的本機磁碟空間數量最大 Azure 診斷所收集的診斷資料的各種類型。</span><span class="sxs-lookup"><span data-stu-id="0e940-178">hello maximum amount of local disk space that may be consumed by hello various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="0e940-179">hello 預設設定為 5120 MB。</span><span class="sxs-lookup"><span data-stu-id="0e940-179">hello default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="0e940-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="0e940-180">**useProxyServer**</span></span> | <span data-ttu-id="0e940-181">在 IE 設定中設定 Azure 診斷 toouse hello proxy 伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="0e940-181">Configure Azure Diagnostics toouse hello proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="0e940-182">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-182">Child Elements</span></span>|<span data-ttu-id="0e940-183">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="0e940-184">**CrashDumps**</span></span>|<span data-ttu-id="0e940-185">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0e940-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="0e940-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="0e940-187">啟用收集 Azure 診斷所產生的記錄。</span><span class="sxs-lookup"><span data-stu-id="0e940-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="0e940-188">hello 診斷基礎結構記錄檔可用於疑難排解 hello 診斷系統本身。</span><span class="sxs-lookup"><span data-stu-id="0e940-188">hello diagnostic infrastructure logs are useful for troubleshooting hello diagnostics system itself.</span></span> <span data-ttu-id="0e940-189">選用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="0e940-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="0e940-190">- **scheduledTransferLogLevelFilter** -設定 hello 最低嚴重性層級的 hello 所收集的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0e940-190">- **scheduledTransferLogLevelFilter** - Configures hello minimum severity level of hello logs collected.</span></span><br /><br /> <span data-ttu-id="0e940-191">- **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。</span><span class="sxs-lookup"><span data-stu-id="0e940-191">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="0e940-192">hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0e940-192">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="0e940-193">**Directories**</span><span class="sxs-lookup"><span data-stu-id="0e940-193">**Directories**</span></span>|<span data-ttu-id="0e940-194">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0e940-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="0e940-195">**EtwProviders**</span></span>|<span data-ttu-id="0e940-196">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0e940-197">**計量**</span><span class="sxs-lookup"><span data-stu-id="0e940-197">**Metrics**</span></span>|<span data-ttu-id="0e940-198">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0e940-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="0e940-199">**PerformanceCounters**</span></span>|<span data-ttu-id="0e940-200">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="0e940-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="0e940-201">**WindowsEventLog**</span></span>|<span data-ttu-id="0e940-202">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="0e940-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="0e940-203">**DockerSources**</span></span>|<span data-ttu-id="0e940-204">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="0e940-205">CrashDumps 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-205">CrashDumps Element</span></span>  
 <span data-ttu-id="0e940-206">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps</span><span class="sxs-lookup"><span data-stu-id="0e940-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="0e940-207">啟用損毀傾印 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="0e940-207">Enable hello collection of crash dumps.</span></span>  

|<span data-ttu-id="0e940-208">屬性</span><span class="sxs-lookup"><span data-stu-id="0e940-208">Attributes</span></span>|<span data-ttu-id="0e940-209">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="0e940-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="0e940-210">**containerName**</span></span>|<span data-ttu-id="0e940-211">選用。</span><span class="sxs-lookup"><span data-stu-id="0e940-211">Optional.</span></span> <span data-ttu-id="0e940-212">在您的 Azure 儲存體帳戶 toobe hello blob 容器 hello 名稱使用 toostore 損毀傾印。</span><span class="sxs-lookup"><span data-stu-id="0e940-212">hello name of hello blob container in your Azure Storage account toobe used toostore crash dumps.</span></span>|  
|<span data-ttu-id="0e940-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="0e940-213">**crashDumpType**</span></span>|<span data-ttu-id="0e940-214">選用。</span><span class="sxs-lookup"><span data-stu-id="0e940-214">Optional.</span></span>  <span data-ttu-id="0e940-215">設定 Azure 診斷 toocollect 迷你或完整損毀傾印。</span><span class="sxs-lookup"><span data-stu-id="0e940-215">Configures Azure Diagnostics toocollect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="0e940-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="0e940-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="0e940-217">選用。</span><span class="sxs-lookup"><span data-stu-id="0e940-217">Optional.</span></span>  <span data-ttu-id="0e940-218">設定 hello 百分比**overallQuotaInMB** toobe 保留給 hello VM 上的損毀傾印。</span><span class="sxs-lookup"><span data-stu-id="0e940-218">Configures hello percentage of **overallQuotaInMB** toobe reserved for crash dumps on hello VM.</span></span>|  

|<span data-ttu-id="0e940-219">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-219">Child Elements</span></span>|<span data-ttu-id="0e940-220">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0e940-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="0e940-222">必要。</span><span class="sxs-lookup"><span data-stu-id="0e940-222">Required.</span></span> <span data-ttu-id="0e940-223">定義每個處理序的組態值。</span><span class="sxs-lookup"><span data-stu-id="0e940-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="0e940-224">下列屬性的 hello 也是必要的：</span><span class="sxs-lookup"><span data-stu-id="0e940-224">hello following attribute is also required:</span></span><br /><br /> <span data-ttu-id="0e940-225">**processName** -hello hello 您想要 Azure 診斷 toocollect 損毀傾印的處理程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="0e940-225">**processName** - hello name of hello process you want Azure Diagnostics toocollect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="0e940-226">Directories 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-226">Directories Element</span></span> 
 <span data-ttu-id="0e940-227">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories</span><span class="sxs-lookup"><span data-stu-id="0e940-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="0e940-228">啟用 hello hello 的目錄內容的集合，IIS 無法存取要求記錄檔及/或 IIS 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0e940-228">Enables hello collection of hello contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="0e940-229">選用的 **scheduledTransferPeriod** 屬性。</span><span class="sxs-lookup"><span data-stu-id="0e940-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="0e940-230">請參閱稍早的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-230">See explanation earlier.</span></span>  

|<span data-ttu-id="0e940-231">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-231">Child Elements</span></span>|<span data-ttu-id="0e940-232">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="0e940-233">**IISLogs**</span></span>|<span data-ttu-id="0e940-234">Hello 組態中包含這個項目可讓 hello 收集 IIS 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="0e940-234">Including this element in hello configuration enables hello collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="0e940-235">**containerName** -hello blob 容器，在您的 Azure 儲存體帳戶 toobe hello 名稱使用 toostore hello IIS 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0e940-235">**containerName** - hello name of hello blob container in your Azure Storage account toobe used toostore hello IIS logs.</span></span>|   
|<span data-ttu-id="0e940-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="0e940-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="0e940-237">這個項目包括 hello 組態中啟用有關失敗的要求 tooan IIS 網站或應用程式記錄檔集合。</span><span class="sxs-lookup"><span data-stu-id="0e940-237">Including this element in hello configuration enables collection of logs about failed requests tooan IIS site or application.</span></span> <span data-ttu-id="0e940-238">您也必須在 **Web.config** 的 **system.WebServer** 下啟用追蹤選項。</span><span class="sxs-lookup"><span data-stu-id="0e940-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="0e940-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="0e940-239">**DataSources**</span></span>|<span data-ttu-id="0e940-240">目錄 toomonitor 清單。</span><span class="sxs-lookup"><span data-stu-id="0e940-240">A list of directories toomonitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="0e940-241">DataSources 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-241">DataSources Element</span></span>  
 <span data-ttu-id="0e940-242">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources</span><span class="sxs-lookup"><span data-stu-id="0e940-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="0e940-243">目錄 toomonitor 清單。</span><span class="sxs-lookup"><span data-stu-id="0e940-243">A list of directories toomonitor.</span></span>  

|<span data-ttu-id="0e940-244">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-244">Child Elements</span></span>|<span data-ttu-id="0e940-245">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0e940-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="0e940-247">必要。</span><span class="sxs-lookup"><span data-stu-id="0e940-247">Required.</span></span> <span data-ttu-id="0e940-248">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="0e940-249">**containerName** -hello hello Azure 儲存體帳戶的 toobe 使用 toostore hello 記錄檔中的 blob 容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="0e940-249">**containerName** - hello name of hello blob container in your Azure Storage account that toobe used toostore hello log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="0e940-250">DirectoryConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="0e940-251">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="0e940-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="0e940-252">可能包含任一 hello**絕對**或**LocalResource**項目，但非兩者。</span><span class="sxs-lookup"><span data-stu-id="0e940-252">May include either hello **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="0e940-253">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-253">Child Elements</span></span>|<span data-ttu-id="0e940-254">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="0e940-255">**Absolute**</span></span>|<span data-ttu-id="0e940-256">絕對路徑 toohello 目錄 toomonitor hello。</span><span class="sxs-lookup"><span data-stu-id="0e940-256">hello absolute path toohello directory toomonitor.</span></span> <span data-ttu-id="0e940-257">hello 下列屬性是必要的：</span><span class="sxs-lookup"><span data-stu-id="0e940-257">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="0e940-258">- **路徑**-hello 絕對路徑 toohello 目錄 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="0e940-258">- **Path** - hello absolute path toohello directory toomonitor.</span></span><br /><br /> <span data-ttu-id="0e940-259">- **expandEnvironment** - 設定是否要展開 Path 中的環境變數。</span><span class="sxs-lookup"><span data-stu-id="0e940-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="0e940-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="0e940-260">**LocalResource**</span></span>|<span data-ttu-id="0e940-261">hello 路徑相對 tooa 本機資源 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="0e940-261">hello path relative tooa local resource toomonitor.</span></span> <span data-ttu-id="0e940-262">必要屬性包括：</span><span class="sxs-lookup"><span data-stu-id="0e940-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="0e940-263">- **名稱**-hello 包含 hello 目錄 toomonitor 的本機資源</span><span class="sxs-lookup"><span data-stu-id="0e940-263">- **Name** - hello local resource that contains hello directory toomonitor</span></span><br /><br /> <span data-ttu-id="0e940-264">- **relativePath** -hello 路徑相對 tooName 包含 hello 目錄 toomonitor</span><span class="sxs-lookup"><span data-stu-id="0e940-264">- **relativePath** - hello path relative tooName that contains hello directory toomonitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="0e940-265">EtwProviders 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-265">EtwProviders Element</span></span>  
 <span data-ttu-id="0e940-266">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders</span><span class="sxs-lookup"><span data-stu-id="0e940-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="0e940-267">設定要收集來自 EventSource 和/或以 ETW 資訊清單為基礎之提供者的 ETW 事件。</span><span class="sxs-lookup"><span data-stu-id="0e940-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="0e940-268">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-268">Child Elements</span></span>|<span data-ttu-id="0e940-269">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0e940-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="0e940-271">設定要收集從 [EventSource 類別](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)產生的事件。</span><span class="sxs-lookup"><span data-stu-id="0e940-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="0e940-272">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="0e940-273">**提供者**-hello hello EventSource 事件類別名稱。</span><span class="sxs-lookup"><span data-stu-id="0e940-273">**provider** - hello class name of hello EventSource event.</span></span><br /><br /> <span data-ttu-id="0e940-274">選用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="0e940-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="0e940-275">- **scheduledTransferLogLevelFilter** -hello 最低嚴重性層級 tootransfer tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e940-275">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="0e940-276">- **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。</span><span class="sxs-lookup"><span data-stu-id="0e940-276">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="0e940-277">hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0e940-277">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="0e940-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0e940-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="0e940-279">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="0e940-280">**提供者**-hello hello 事件提供者的 GUID</span><span class="sxs-lookup"><span data-stu-id="0e940-280">**provider** - hello GUID of hello event provider</span></span><br /><br /> <span data-ttu-id="0e940-281">選用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="0e940-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="0e940-282">- **scheduledTransferLogLevelFilter** -hello 最低嚴重性層級 tootransfer tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e940-282">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="0e940-283">- **scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。</span><span class="sxs-lookup"><span data-stu-id="0e940-283">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="0e940-284">hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0e940-284">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="0e940-285">EtwEventSourceProviderConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="0e940-286">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="0e940-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="0e940-287">設定要收集從 [EventSource 類別](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)產生的事件。</span><span class="sxs-lookup"><span data-stu-id="0e940-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="0e940-288">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-288">Child Elements</span></span>|<span data-ttu-id="0e940-289">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="0e940-290">**DefaultEvents**</span></span>|<span data-ttu-id="0e940-291">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="0e940-292">**eventDestination** -hello hello 資料表 toostore hello 中的事件名稱</span><span class="sxs-lookup"><span data-stu-id="0e940-292">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="0e940-293">**Event**</span><span class="sxs-lookup"><span data-stu-id="0e940-293">**Event**</span></span>|<span data-ttu-id="0e940-294">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="0e940-295">**識別碼**-hello 事件識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="0e940-295">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="0e940-296">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0e940-297">**eventDestination** -hello hello 資料表 toostore hello 中的事件名稱</span><span class="sxs-lookup"><span data-stu-id="0e940-297">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="0e940-298">EtwManifestProviderConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="0e940-299">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="0e940-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="0e940-300">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-300">Child Elements</span></span>|<span data-ttu-id="0e940-301">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="0e940-302">**DefaultEvents**</span></span>|<span data-ttu-id="0e940-303">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0e940-304">**eventDestination** -hello hello 資料表 toostore hello 中的事件名稱</span><span class="sxs-lookup"><span data-stu-id="0e940-304">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="0e940-305">**Event**</span><span class="sxs-lookup"><span data-stu-id="0e940-305">**Event**</span></span>|<span data-ttu-id="0e940-306">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="0e940-307">**識別碼**-hello 事件識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="0e940-307">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="0e940-308">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0e940-309">**eventDestination** -hello hello 資料表 toostore hello 中的事件名稱</span><span class="sxs-lookup"><span data-stu-id="0e940-309">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="0e940-310">Metrics 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-310">Metrics Element</span></span>  
 <span data-ttu-id="0e940-311">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics</span><span class="sxs-lookup"><span data-stu-id="0e940-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="0e940-312">可讓您 toogenerate 最適合用於快速查詢的效能計數器資料表。</span><span class="sxs-lookup"><span data-stu-id="0e940-312">Enables you toogenerate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="0e940-313">Hello 中定義每個效能計數器**PerformanceCounters**項目會儲存在加法 toohello 效能計數器資料表中的 hello 度量資料表。</span><span class="sxs-lookup"><span data-stu-id="0e940-313">Each performance counter that is defined in hello **PerformanceCounters** element is stored in hello Metrics table in addition toohello Performance Counter table.</span></span>  

 <span data-ttu-id="0e940-314">hello **resourceId**是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="0e940-314">hello **resourceId** attribute is required.</span></span>  <span data-ttu-id="0e940-315">hello hello 您要部署至 Azure 診斷的虛擬機器的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="0e940-315">hello resource ID of hello Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="0e940-316">取得 hello **resourceID**從 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="0e940-316">Get hello **resourceID** from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0e940-317">選取 [瀏覽][資源群組] ->  -> **<Name\>**。</span><span class="sxs-lookup"><span data-stu-id="0e940-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="0e940-318">按一下 hello**屬性**磚，然後從 hello 複製 hello 值**識別碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="0e940-318">Click hello **Properties** tile and copy hello value from hello **ID** field.</span></span>  

|<span data-ttu-id="0e940-319">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-319">Child Elements</span></span>|<span data-ttu-id="0e940-320">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="0e940-321">**MetricAggregation**</span></span>|<span data-ttu-id="0e940-322">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="0e940-323">**scheduledTransferPeriod** -hello 間隔排程的傳輸 toostorage 無條件進位 toohello 最接近的分鐘。</span><span class="sxs-lookup"><span data-stu-id="0e940-323">**scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="0e940-324">hello 值是[XML 「 持續時間資料類型 」。](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="0e940-324">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="0e940-325">PerformanceCounters 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="0e940-326">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="0e940-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="0e940-327">啟用效能計數器 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="0e940-327">Enables hello collection of performance counters.</span></span>  

 <span data-ttu-id="0e940-328">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-328">Optional attribute:</span></span>  

 <span data-ttu-id="0e940-329">選用的 **scheduledTransferPeriod** 屬性。</span><span class="sxs-lookup"><span data-stu-id="0e940-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="0e940-330">請參閱稍早的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-330">See explanation earlier.</span></span>

|<span data-ttu-id="0e940-331">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-331">Child Element</span></span>|<span data-ttu-id="0e940-332">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="0e940-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="0e940-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="0e940-334">hello 下列屬性是必要的：</span><span class="sxs-lookup"><span data-stu-id="0e940-334">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="0e940-335">- **counterSpecifier** -hello hello 效能計數器的名稱。</span><span class="sxs-lookup"><span data-stu-id="0e940-335">- **counterSpecifier** - hello name of hello performance counter.</span></span> <span data-ttu-id="0e940-336">例如： `\Processor(_Total)\% Processor Time`。</span><span class="sxs-lookup"><span data-stu-id="0e940-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="0e940-337">tooget 一份效能計數器，您在主機上，執行 hello 命令`typeperf`。</span><span class="sxs-lookup"><span data-stu-id="0e940-337">tooget a list of performance counters on your host, run hello command `typeperf`.</span></span><br /><br /> <span data-ttu-id="0e940-338">- **sampleRate** -頻率 hello 應該取樣。</span><span class="sxs-lookup"><span data-stu-id="0e940-338">- **sampleRate** - How often hello counter should be sampled.</span></span><br /><br /> <span data-ttu-id="0e940-339">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="0e940-340">**單位**-hello hello 計數器的測量單位。</span><span class="sxs-lookup"><span data-stu-id="0e940-340">**unit** - hello unit of measure of hello counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="0e940-341">WindowsEventLog 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="0e940-342">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="0e940-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="0e940-343">啟用 hello 集合的 「 Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0e940-343">Enables hello collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="0e940-344">選用的 **scheduledTransferPeriod** 屬性。</span><span class="sxs-lookup"><span data-stu-id="0e940-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="0e940-345">請參閱稍早的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="0e940-346">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-346">Child Element</span></span>|<span data-ttu-id="0e940-347">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="0e940-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="0e940-348">**DataSource**</span></span>|<span data-ttu-id="0e940-349">hello Windows 事件記錄檔 toocollect。</span><span class="sxs-lookup"><span data-stu-id="0e940-349">hello Windows Event logs toocollect.</span></span> <span data-ttu-id="0e940-350">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="0e940-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="0e940-351">**名稱**-收集描述 hello windows 事件 toobe hello XPath 查詢。</span><span class="sxs-lookup"><span data-stu-id="0e940-351">**name** - hello XPath query describing hello windows events toobe collected.</span></span> <span data-ttu-id="0e940-352">例如：</span><span class="sxs-lookup"><span data-stu-id="0e940-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="0e940-353">toocollect 所有事件，都指定"*"</span><span class="sxs-lookup"><span data-stu-id="0e940-353">toocollect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="0e940-354">Logs 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-354">Logs Element</span></span>  
 <span data-ttu-id="0e940-355">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs</span><span class="sxs-lookup"><span data-stu-id="0e940-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="0e940-356">出現在 1.0 和 1.1 版中。</span><span class="sxs-lookup"><span data-stu-id="0e940-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="0e940-357">在 1.2 中消失。</span><span class="sxs-lookup"><span data-stu-id="0e940-357">Missing in 1.2.</span></span> <span data-ttu-id="0e940-358">再度新增於 1.3 中。</span><span class="sxs-lookup"><span data-stu-id="0e940-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="0e940-359">定義基本 Azure 記錄檔的 hello 緩衝區組態。</span><span class="sxs-lookup"><span data-stu-id="0e940-359">Defines hello buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="0e940-360">屬性</span><span class="sxs-lookup"><span data-stu-id="0e940-360">Attribute</span></span>|<span data-ttu-id="0e940-361">類型</span><span class="sxs-lookup"><span data-stu-id="0e940-361">Type</span></span>|<span data-ttu-id="0e940-362">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0e940-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="0e940-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="0e940-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="0e940-364">**unsignedInt**</span></span>|<span data-ttu-id="0e940-365">選用。</span><span class="sxs-lookup"><span data-stu-id="0e940-365">Optional.</span></span> <span data-ttu-id="0e940-366">指定的檔案系統儲存體可供指定的 hello hello 最大數量的資料。</span><span class="sxs-lookup"><span data-stu-id="0e940-366">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="0e940-367">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="0e940-367">hello default is 0.</span></span>|  
|<span data-ttu-id="0e940-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="0e940-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="0e940-369">**字串**</span><span class="sxs-lookup"><span data-stu-id="0e940-369">**string**</span></span>|<span data-ttu-id="0e940-370">選用。</span><span class="sxs-lookup"><span data-stu-id="0e940-370">Optional.</span></span> <span data-ttu-id="0e940-371">指定最低嚴重性層級 hello 傳送的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="0e940-371">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="0e940-372">hello 預設值是**Undefined**，傳輸的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="0e940-372">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="0e940-373">其他可能的值 （依順序的最多 tooleast 資訊） 為**Verbose**，**資訊**，**警告**，**錯誤**，和**重大**。</span><span class="sxs-lookup"><span data-stu-id="0e940-373">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="0e940-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="0e940-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="0e940-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="0e940-375">**duration**</span></span>|<span data-ttu-id="0e940-376">選用。</span><span class="sxs-lookup"><span data-stu-id="0e940-376">Optional.</span></span> <span data-ttu-id="0e940-377">指定 hello 排程傳輸的資料，無條件進位 toohello 最接近的分鐘的間隔。</span><span class="sxs-lookup"><span data-stu-id="0e940-377">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="0e940-378">hello 預設值是 PT0S。</span><span class="sxs-lookup"><span data-stu-id="0e940-378">hello default is PT0S.</span></span>|  
|<span data-ttu-id="0e940-379">**sinks** 已在 1.5 中新增</span><span class="sxs-lookup"><span data-stu-id="0e940-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="0e940-380">**字串**</span><span class="sxs-lookup"><span data-stu-id="0e940-380">**string**</span></span>|<span data-ttu-id="0e940-381">選用。</span><span class="sxs-lookup"><span data-stu-id="0e940-381">Optional.</span></span> <span data-ttu-id="0e940-382">點 tooa 接收位置 tooalso 傳送診斷資料。</span><span class="sxs-lookup"><span data-stu-id="0e940-382">Points tooa sink location tooalso send diagnostic data.</span></span> <span data-ttu-id="0e940-383">例如 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="0e940-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="0e940-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="0e940-384">DockerSources</span></span>
 <span data-ttu-id="0e940-385">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources</span><span class="sxs-lookup"><span data-stu-id="0e940-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="0e940-386">已在 1.9 版中新增。</span><span class="sxs-lookup"><span data-stu-id="0e940-386">Added in 1.9.</span></span>

|<span data-ttu-id="0e940-387">元素名稱</span><span class="sxs-lookup"><span data-stu-id="0e940-387">Element Name</span></span>|<span data-ttu-id="0e940-388">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="0e940-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="0e940-389">**Stats**</span></span>|<span data-ttu-id="0e940-390">會告知 hello 系統 toocollect Docker 容器的統計資料</span><span class="sxs-lookup"><span data-stu-id="0e940-390">Tells hello system toocollect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="0e940-391">SinksConfig 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-391">SinksConfig Element</span></span>  
 <span data-ttu-id="0e940-392">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig</span><span class="sxs-lookup"><span data-stu-id="0e940-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="0e940-393">位置 toosend 診斷資料 tooand hello 組態與那些位置相關聯的清單。</span><span class="sxs-lookup"><span data-stu-id="0e940-393">A list of locations toosend diagnostics data tooand hello configuration associated with those locations.</span></span>  

|<span data-ttu-id="0e940-394">元素名稱</span><span class="sxs-lookup"><span data-stu-id="0e940-394">Element Name</span></span>|<span data-ttu-id="0e940-395">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="0e940-396">**接收**</span><span class="sxs-lookup"><span data-stu-id="0e940-396">**Sink**</span></span>|<span data-ttu-id="0e940-397">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="0e940-398">Sink 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-398">Sink Element</span></span>
 <span data-ttu-id="0e940-399">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink</span><span class="sxs-lookup"><span data-stu-id="0e940-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="0e940-400">已在 1.5 版中新增。</span><span class="sxs-lookup"><span data-stu-id="0e940-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="0e940-401">定義位置 toosend 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="0e940-401">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="0e940-402">例如，hello Application Insights 服務。</span><span class="sxs-lookup"><span data-stu-id="0e940-402">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="0e940-403">屬性</span><span class="sxs-lookup"><span data-stu-id="0e940-403">Attribute</span></span>|<span data-ttu-id="0e940-404">類型</span><span class="sxs-lookup"><span data-stu-id="0e940-404">Type</span></span>|<span data-ttu-id="0e940-405">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="0e940-406">**name**</span><span class="sxs-lookup"><span data-stu-id="0e940-406">**name**</span></span>|<span data-ttu-id="0e940-407">字串</span><span class="sxs-lookup"><span data-stu-id="0e940-407">string</span></span>|<span data-ttu-id="0e940-408">字串識別 hello sinkname。</span><span class="sxs-lookup"><span data-stu-id="0e940-408">A string identifying hello sinkname.</span></span>|  

|<span data-ttu-id="0e940-409">元素</span><span class="sxs-lookup"><span data-stu-id="0e940-409">Element</span></span>|<span data-ttu-id="0e940-410">類型</span><span class="sxs-lookup"><span data-stu-id="0e940-410">Type</span></span>|<span data-ttu-id="0e940-411">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="0e940-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="0e940-412">**Application Insights**</span></span>|<span data-ttu-id="0e940-413">字串</span><span class="sxs-lookup"><span data-stu-id="0e940-413">string</span></span>|<span data-ttu-id="0e940-414">只有在傳送資料 tooApplication Insights 時，才使用。</span><span class="sxs-lookup"><span data-stu-id="0e940-414">Used only when sending data tooApplication Insights.</span></span> <span data-ttu-id="0e940-415">包含 hello 檢測金鑰的使用中的 Application Insights 帳戶具有存取權。</span><span class="sxs-lookup"><span data-stu-id="0e940-415">Contain hello Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="0e940-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="0e940-416">**Channels**</span></span>|<span data-ttu-id="0e940-417">字串</span><span class="sxs-lookup"><span data-stu-id="0e940-417">string</span></span>|<span data-ttu-id="0e940-418">每個可額外篩選該資料流的其中一個</span><span class="sxs-lookup"><span data-stu-id="0e940-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="0e940-419">Channels 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-419">Channels Element</span></span>  
 <span data-ttu-id="0e940-420">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels</span><span class="sxs-lookup"><span data-stu-id="0e940-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="0e940-421">已在 1.5 版中新增。</span><span class="sxs-lookup"><span data-stu-id="0e940-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="0e940-422">針對通過接收之記錄資料的資料流定義篩選器。</span><span class="sxs-lookup"><span data-stu-id="0e940-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="0e940-423">元素</span><span class="sxs-lookup"><span data-stu-id="0e940-423">Element</span></span>|<span data-ttu-id="0e940-424">類型</span><span class="sxs-lookup"><span data-stu-id="0e940-424">Type</span></span>|<span data-ttu-id="0e940-425">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="0e940-426">**Channel**</span><span class="sxs-lookup"><span data-stu-id="0e940-426">**Channel**</span></span>|<span data-ttu-id="0e940-427">字串</span><span class="sxs-lookup"><span data-stu-id="0e940-427">string</span></span>|<span data-ttu-id="0e940-428">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="0e940-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="0e940-429">Channel 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-429">Channel Element</span></span>
 <span data-ttu-id="0e940-430">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel</span><span class="sxs-lookup"><span data-stu-id="0e940-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="0e940-431">已在 1.5 版中新增。</span><span class="sxs-lookup"><span data-stu-id="0e940-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="0e940-432">定義位置 toosend 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="0e940-432">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="0e940-433">例如，hello Application Insights 服務。</span><span class="sxs-lookup"><span data-stu-id="0e940-433">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="0e940-434">屬性</span><span class="sxs-lookup"><span data-stu-id="0e940-434">Attributes</span></span>|<span data-ttu-id="0e940-435">類型</span><span class="sxs-lookup"><span data-stu-id="0e940-435">Type</span></span>|<span data-ttu-id="0e940-436">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="0e940-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="0e940-437">**logLevel**</span></span>|<span data-ttu-id="0e940-438">**字串**</span><span class="sxs-lookup"><span data-stu-id="0e940-438">**string**</span></span>|<span data-ttu-id="0e940-439">指定最低嚴重性層級 hello 傳送的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="0e940-439">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="0e940-440">hello 預設值是**Undefined**，傳輸的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="0e940-440">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="0e940-441">其他可能的值 （依順序的最多 tooleast 資訊） 為**Verbose**，**資訊**，**警告**，**錯誤**，和**重大**。</span><span class="sxs-lookup"><span data-stu-id="0e940-441">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="0e940-442">**name**</span><span class="sxs-lookup"><span data-stu-id="0e940-442">**name**</span></span>|<span data-ttu-id="0e940-443">**字串**</span><span class="sxs-lookup"><span data-stu-id="0e940-443">**string**</span></span>|<span data-ttu-id="0e940-444">Hello 通道 toorefer 以唯一的名稱</span><span class="sxs-lookup"><span data-stu-id="0e940-444">A unique name of hello channel toorefer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="0e940-445">PrivateConfig 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="0e940-446">樹狀結構︰根目錄 - DiagnosticsConfiguration - PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="0e940-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="0e940-447">已在 1.3 版中新增。</span><span class="sxs-lookup"><span data-stu-id="0e940-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="0e940-448">選用</span><span class="sxs-lookup"><span data-stu-id="0e940-448">Optional</span></span>  

 <span data-ttu-id="0e940-449">儲存 hello hello 儲存體帳戶 （名稱、 金鑰和端點） 的私用詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e940-449">Stores hello private details of hello storage account (name, key, and endpoint).</span></span> <span data-ttu-id="0e940-450">這項資訊會傳送 toohello 虛擬機器，但無法從其擷取。</span><span class="sxs-lookup"><span data-stu-id="0e940-450">This information is sent toohello virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="0e940-451">子元素</span><span class="sxs-lookup"><span data-stu-id="0e940-451">Child Elements</span></span>|<span data-ttu-id="0e940-452">說明</span><span class="sxs-lookup"><span data-stu-id="0e940-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="0e940-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="0e940-453">**StorageAccount**</span></span>|<span data-ttu-id="0e940-454">hello 儲存體帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="0e940-454">hello storage account toouse.</span></span> <span data-ttu-id="0e940-455">所需的下列屬性的 hello</span><span class="sxs-lookup"><span data-stu-id="0e940-455">hello following attributes are required</span></span><br /><br /> <span data-ttu-id="0e940-456">- **名稱**-hello hello 儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="0e940-456">- **name** - hello name of hello storage account.</span></span><br /><br /> <span data-ttu-id="0e940-457">- **索引鍵**-hello 金鑰 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e940-457">- **key** - hello key toohello storage account.</span></span><br /><br /> <span data-ttu-id="0e940-458">- **端點**-hello 端點 tooaccess hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e940-458">- **endpoint** - hello endpoint tooaccess hello storage account.</span></span> <br /><br /> <span data-ttu-id="0e940-459">-**sasToken** （加入 1.8.1)-您可以在 hello 私用組態中指定的 SAS 權杖，而不是儲存體帳戶金鑰。如果提供，則會忽略 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="0e940-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in hello private config. If provided, hello storage account key is ignored.</span></span> <br /><span data-ttu-id="0e940-460">Hello SAS 權杖的需求：</span><span class="sxs-lookup"><span data-stu-id="0e940-460">Requirements for hello SAS Token:</span></span> <br /><span data-ttu-id="0e940-461">- 僅支援帳戶 SAS 權杖</span><span class="sxs-lookup"><span data-stu-id="0e940-461">- Supports account SAS token only</span></span> <br /><span data-ttu-id="0e940-462">- 需要 b、t 服務類型。</span><span class="sxs-lookup"><span data-stu-id="0e940-462">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="0e940-463">- 需要 a、c、u、w 權限。</span><span class="sxs-lookup"><span data-stu-id="0e940-463">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="0e940-464">- 需要 c、o 資源類型。</span><span class="sxs-lookup"><span data-stu-id="0e940-464">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="0e940-465">-支援 hello HTTPS 通訊協定</span><span class="sxs-lookup"><span data-stu-id="0e940-465">- Supports hello HTTPS protocol only</span></span> <br /> <span data-ttu-id="0e940-466">- 開始和到期時間必須是有效的。</span><span class="sxs-lookup"><span data-stu-id="0e940-466">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="0e940-467">IsEnabled 元素</span><span class="sxs-lookup"><span data-stu-id="0e940-467">IsEnabled Element</span></span>  
 <span data-ttu-id="0e940-468">樹狀結構︰根目錄 - DiagnosticsConfiguration - IsEnabled</span><span class="sxs-lookup"><span data-stu-id="0e940-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="0e940-469">布林值。</span><span class="sxs-lookup"><span data-stu-id="0e940-469">Boolean.</span></span> <span data-ttu-id="0e940-470">使用`true`tooenable hello 診斷或`false`toodisable hello 診斷。</span><span class="sxs-lookup"><span data-stu-id="0e940-470">Use `true` tooenable hello diagnostics or `false` toodisable hello diagnostics.</span></span>
