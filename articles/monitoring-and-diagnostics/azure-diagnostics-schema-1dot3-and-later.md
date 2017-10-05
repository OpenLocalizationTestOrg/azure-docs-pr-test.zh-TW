---
title: "Azure 診斷擴充功能 1.3 版和更新版本的組態結構描述 | Microsoft Docs"
description: "適用於 Azure 診斷的結構描述 1.3 版和更新版本隨附於 Microsoft Azure SDK 2.4 版和更新版本中。"
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
ms.openlocfilehash: 0d814825fb08452238a254ccd30bde230380c74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="08163-103">Azure 診斷 1.3 版和更新版本的組態結構描述</span><span class="sxs-lookup"><span data-stu-id="08163-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="08163-104">Azure 診斷擴充功能這個元件可用來收集下列項目的效能計數器和其他統計資料︰</span><span class="sxs-lookup"><span data-stu-id="08163-104">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="08163-105">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="08163-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="08163-106">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="08163-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="08163-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="08163-107">Service Fabric</span></span> 
> - <span data-ttu-id="08163-108">雲端服務</span><span class="sxs-lookup"><span data-stu-id="08163-108">Cloud Services</span></span> 
> - <span data-ttu-id="08163-109">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="08163-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="08163-110">此頁面只在您使用其中一個服務時才相關。</span><span class="sxs-lookup"><span data-stu-id="08163-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="08163-111">此頁面適用於 1.3 版和更新版本 (Azure SDK 2.4 版和更新版本)。</span><span class="sxs-lookup"><span data-stu-id="08163-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="08163-112">我們會在較新的組態區段中加入標記，表示已將它們新增至哪一個版本中。</span><span class="sxs-lookup"><span data-stu-id="08163-112">Newer configuration sections are commented to show in what version they were added.</span></span>  

<span data-ttu-id="08163-113">當診斷監視器啟動時，此處所述的組態檔會用來設定診斷組態設定。</span><span class="sxs-lookup"><span data-stu-id="08163-113">The configuration file described here is used to set diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

<span data-ttu-id="08163-114">此擴充功能要與 Azure 監視器、Application Insights 和 Log Analytics 等其他 Microsoft 診斷產品搭配使用。</span><span class="sxs-lookup"><span data-stu-id="08163-114">The extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="08163-115">執行下列 PowerShell 命令，以下載公用組態檔結構描述定義：</span><span class="sxs-lookup"><span data-stu-id="08163-115">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="08163-116">如需有關使用 Azure 診斷的詳細資訊，請參閱 [Azure 診斷擴充功能](azure-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="08163-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="08163-117">診斷組態檔的範例</span><span class="sxs-lookup"><span data-stu-id="08163-117">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="08163-118">下列範例顯示一般的診斷組態檔：</span><span class="sxs-lookup"><span data-stu-id="08163-118">The following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="08163-119">先前 XML 組態檔的對應 JSON。</span><span class="sxs-lookup"><span data-stu-id="08163-119">JSON equivalent of the previous XML configuration file.</span></span> 

<span data-ttu-id="08163-120">因為在大部分的 JSON 使用案例中，PublicConfig 和 PrivateConfig 會分隔開來，因此我們會以不同變數來傳遞這兩個檔案。</span><span class="sxs-lookup"><span data-stu-id="08163-120">The PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="08163-121">這些案例包括 Resource Manager 範本、虛擬機器擴展集 PowerShell 和 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="08163-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="08163-122">閱讀本頁面</span><span class="sxs-lookup"><span data-stu-id="08163-122">Reading this page</span></span>  
 <span data-ttu-id="08163-123">下列標籤大致上會遵循上述範例中所示的順序。</span><span class="sxs-lookup"><span data-stu-id="08163-123">The tags following are roughly in order shown in the preceding example.</span></span>  <span data-ttu-id="08163-124">如果您未在預期之處看見完整說明，請在頁面中搜尋該元素或屬性。</span><span class="sxs-lookup"><span data-stu-id="08163-124">If you don't see a full description where you expect it, search the page for the element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="08163-125">一般屬性類型</span><span class="sxs-lookup"><span data-stu-id="08163-125">Common Attribute Types</span></span>  
 <span data-ttu-id="08163-126">**scheduledTransferPeriod** 屬性會出現在數個元素中。</span><span class="sxs-lookup"><span data-stu-id="08163-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="08163-127">其為排程傳輸至儲存體之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="08163-127">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="08163-128">值是 [XML「持續時間資料類型」(英文)](http://www.w3schools.com/schema/schema_dtypes_date.asp)。</span><span class="sxs-lookup"><span data-stu-id="08163-128">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="08163-129">DiagnosticsConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="08163-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="08163-130">樹狀結構︰根目錄 - DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="08163-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="08163-131">已在 1.3 版中新增。</span><span class="sxs-lookup"><span data-stu-id="08163-131">Added in version 1.3.</span></span>  

<span data-ttu-id="08163-132">診斷組態檔的最上層元素。</span><span class="sxs-lookup"><span data-stu-id="08163-132">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="08163-133">**屬性** xmlns - 適用於診斷組態檔的 XML 命名空間如下：</span><span class="sxs-lookup"><span data-stu-id="08163-133">**Attribute**  xmlns - The XML namespace for the diagnostics configuration file is:</span></span>  
<span data-ttu-id="08163-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="08163-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="08163-135">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-135">Child Elements</span></span>|<span data-ttu-id="08163-136">說明</span><span class="sxs-lookup"><span data-stu-id="08163-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="08163-137">**PublicConfig**</span></span>|<span data-ttu-id="08163-138">必要。</span><span class="sxs-lookup"><span data-stu-id="08163-138">Required.</span></span> <span data-ttu-id="08163-139">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="08163-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="08163-140">**PrivateConfig**</span></span>|<span data-ttu-id="08163-141">選用。</span><span class="sxs-lookup"><span data-stu-id="08163-141">Optional.</span></span> <span data-ttu-id="08163-142">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="08163-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="08163-143">**IsEnabled**</span></span>|<span data-ttu-id="08163-144">布林值。</span><span class="sxs-lookup"><span data-stu-id="08163-144">Boolean.</span></span> <span data-ttu-id="08163-145">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="08163-146">PublicConfig 元素</span><span class="sxs-lookup"><span data-stu-id="08163-146">PublicConfig Element</span></span>  
 <span data-ttu-id="08163-147">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig</span><span class="sxs-lookup"><span data-stu-id="08163-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="08163-148">說明公用診斷組態。</span><span class="sxs-lookup"><span data-stu-id="08163-148">Describes the public diagnostics configuration.</span></span>  

|<span data-ttu-id="08163-149">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-149">Child Elements</span></span>|<span data-ttu-id="08163-150">說明</span><span class="sxs-lookup"><span data-stu-id="08163-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="08163-151">**WadCfg**</span></span>|<span data-ttu-id="08163-152">必要。</span><span class="sxs-lookup"><span data-stu-id="08163-152">Required.</span></span> <span data-ttu-id="08163-153">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="08163-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="08163-154">**StorageAccount**</span></span>|<span data-ttu-id="08163-155">要儲存資料的 Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="08163-155">The name of the Azure Storage account to store the data in.</span></span> <span data-ttu-id="08163-156">可能也會在執行 Set-AzureServiceDiagnosticsExtension Cmdlet 時指定為參數。</span><span class="sxs-lookup"><span data-stu-id="08163-156">May also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="08163-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="08163-157">**StorageType**</span></span>|<span data-ttu-id="08163-158">可以是 Table、Blob 或 TableAndBlob。</span><span class="sxs-lookup"><span data-stu-id="08163-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="08163-159">預設值是 Table。</span><span class="sxs-lookup"><span data-stu-id="08163-159">Table is default.</span></span> <span data-ttu-id="08163-160">若選擇 TableAndBlob，系統會將診斷資料寫入兩次 -- 每種類型寫入一次。</span><span class="sxs-lookup"><span data-stu-id="08163-160">When TableAndBlob is chosen, diagnostic data is written twice -- once to each type.</span></span>|  
|<span data-ttu-id="08163-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="08163-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="08163-162">虛擬機器上監視代理程式儲存事件資料的目錄。</span><span class="sxs-lookup"><span data-stu-id="08163-162">The directory on the virtual machine where the Monitoring Agent stores event data.</span></span> <span data-ttu-id="08163-163">如果沒有，請設定，否則會使用預設的目錄：</span><span class="sxs-lookup"><span data-stu-id="08163-163">If not, set, the default directory is used:</span></span><br /><br /> <span data-ttu-id="08163-164">針對背景工作/web 角色：`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="08163-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="08163-165">針對虛擬機器：`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="08163-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="08163-166">必要屬性包括：</span><span class="sxs-lookup"><span data-stu-id="08163-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="08163-167">- **path** - 系統上 Azure 診斷所使用的目錄。</span><span class="sxs-lookup"><span data-stu-id="08163-167">- **path** - The directory on the system to be used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="08163-168">- **expandEnvironment** - 控制是否要展開路徑名稱中的環境變數。</span><span class="sxs-lookup"><span data-stu-id="08163-168">- **expandEnvironment** - Controls whether environment variables are expanded in the path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="08163-169">WadCFG 元素</span><span class="sxs-lookup"><span data-stu-id="08163-169">WadCFG Element</span></span>  
 <span data-ttu-id="08163-170">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG</span><span class="sxs-lookup"><span data-stu-id="08163-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="08163-171">識別並設定要收集的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="08163-171">Identifies and configures the telemetry data to be collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="08163-172">DiagnosticMonitorConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="08163-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="08163-173">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="08163-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="08163-174">必要</span><span class="sxs-lookup"><span data-stu-id="08163-174">Required</span></span> 

|<span data-ttu-id="08163-175">屬性</span><span class="sxs-lookup"><span data-stu-id="08163-175">Attributes</span></span>|<span data-ttu-id="08163-176">說明</span><span class="sxs-lookup"><span data-stu-id="08163-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="08163-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="08163-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="08163-178">可供 Azure 診斷所收集的各種類型診斷資料取用的本機磁碟空間量上限。</span><span class="sxs-lookup"><span data-stu-id="08163-178">The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="08163-179">預設設定為 5120 MB。</span><span class="sxs-lookup"><span data-stu-id="08163-179">The default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="08163-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="08163-180">**useProxyServer**</span></span> | <span data-ttu-id="08163-181">設定 Azure 診斷來使用 Proxy 伺服器設定，如 IE 設定中所設定。</span><span class="sxs-lookup"><span data-stu-id="08163-181">Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="08163-182">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-182">Child Elements</span></span>|<span data-ttu-id="08163-183">說明</span><span class="sxs-lookup"><span data-stu-id="08163-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="08163-184">**CrashDumps**</span></span>|<span data-ttu-id="08163-185">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="08163-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="08163-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="08163-187">啟用收集 Azure 診斷所產生的記錄。</span><span class="sxs-lookup"><span data-stu-id="08163-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="08163-188">診斷基礎結構記錄適用於疑難排解診斷系統本身。</span><span class="sxs-lookup"><span data-stu-id="08163-188">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span></span> <span data-ttu-id="08163-189">選用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="08163-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="08163-190">- **scheduledTransferLogLevelFilter** - 設定所收集之記錄的最低嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="08163-190">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span></span><br /><br /> <span data-ttu-id="08163-191">- **scheduledTransferPeriod** - 排程傳輸至儲存體之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="08163-191">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="08163-192">值是 [XML「持續時間資料類型」(英文)](http://www.w3schools.com/schema/schema_dtypes_date.asp)。</span><span class="sxs-lookup"><span data-stu-id="08163-192">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="08163-193">**Directories**</span><span class="sxs-lookup"><span data-stu-id="08163-193">**Directories**</span></span>|<span data-ttu-id="08163-194">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="08163-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="08163-195">**EtwProviders**</span></span>|<span data-ttu-id="08163-196">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="08163-197">**計量**</span><span class="sxs-lookup"><span data-stu-id="08163-197">**Metrics**</span></span>|<span data-ttu-id="08163-198">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="08163-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="08163-199">**PerformanceCounters**</span></span>|<span data-ttu-id="08163-200">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="08163-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="08163-201">**WindowsEventLog**</span></span>|<span data-ttu-id="08163-202">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="08163-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="08163-203">**DockerSources**</span></span>|<span data-ttu-id="08163-204">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="08163-205">CrashDumps 元素</span><span class="sxs-lookup"><span data-stu-id="08163-205">CrashDumps Element</span></span>  
 <span data-ttu-id="08163-206">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps</span><span class="sxs-lookup"><span data-stu-id="08163-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="08163-207">啟用收集損毀傾印。</span><span class="sxs-lookup"><span data-stu-id="08163-207">Enable the collection of crash dumps.</span></span>  

|<span data-ttu-id="08163-208">屬性</span><span class="sxs-lookup"><span data-stu-id="08163-208">Attributes</span></span>|<span data-ttu-id="08163-209">說明</span><span class="sxs-lookup"><span data-stu-id="08163-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="08163-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="08163-210">**containerName**</span></span>|<span data-ttu-id="08163-211">選用。</span><span class="sxs-lookup"><span data-stu-id="08163-211">Optional.</span></span> <span data-ttu-id="08163-212">在您的 Azure 儲存體帳戶中用來儲存損毀傾印的 Blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="08163-212">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span></span>|  
|<span data-ttu-id="08163-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="08163-213">**crashDumpType**</span></span>|<span data-ttu-id="08163-214">選用。</span><span class="sxs-lookup"><span data-stu-id="08163-214">Optional.</span></span>  <span data-ttu-id="08163-215">設定 Azure 診斷來收集迷你或完整的損毀傾印。</span><span class="sxs-lookup"><span data-stu-id="08163-215">Configures Azure Diagnostics to collect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="08163-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="08163-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="08163-217">選用。</span><span class="sxs-lookup"><span data-stu-id="08163-217">Optional.</span></span>  <span data-ttu-id="08163-218">設定要在 VM 上保留以供損毀傾印使用的 **overallQuotaInMB** 百分比。</span><span class="sxs-lookup"><span data-stu-id="08163-218">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span></span>|  

|<span data-ttu-id="08163-219">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-219">Child Elements</span></span>|<span data-ttu-id="08163-220">說明</span><span class="sxs-lookup"><span data-stu-id="08163-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="08163-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="08163-222">必要。</span><span class="sxs-lookup"><span data-stu-id="08163-222">Required.</span></span> <span data-ttu-id="08163-223">定義每個處理序的組態值。</span><span class="sxs-lookup"><span data-stu-id="08163-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="08163-224">以下也是必要屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-224">The following attribute is also required:</span></span><br /><br /> <span data-ttu-id="08163-225">**processName** - 您希望 Azure 診斷收集損毀傾印的處理序名稱。</span><span class="sxs-lookup"><span data-stu-id="08163-225">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="08163-226">Directories 元素</span><span class="sxs-lookup"><span data-stu-id="08163-226">Directories Element</span></span> 
 <span data-ttu-id="08163-227">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories</span><span class="sxs-lookup"><span data-stu-id="08163-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="08163-228">啟用收集目錄、IIS 失敗的存取要求記錄和/或 IIS 記錄的內容。</span><span class="sxs-lookup"><span data-stu-id="08163-228">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="08163-229">選用的 **scheduledTransferPeriod** 屬性。</span><span class="sxs-lookup"><span data-stu-id="08163-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="08163-230">請參閱稍早的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-230">See explanation earlier.</span></span>  

|<span data-ttu-id="08163-231">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-231">Child Elements</span></span>|<span data-ttu-id="08163-232">說明</span><span class="sxs-lookup"><span data-stu-id="08163-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="08163-233">**IISLogs**</span></span>|<span data-ttu-id="08163-234">在組態中包含此元素，就能收集 IIS 記錄：</span><span class="sxs-lookup"><span data-stu-id="08163-234">Including this element in the configuration enables the collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="08163-235">**containerName** - 在您的 Azure 儲存體帳戶中用來儲存 IIS 記錄的 Blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="08163-235">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span></span>|   
|<span data-ttu-id="08163-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="08163-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="08163-237">在組態中包含此元素，就能夠收集對於 IIS 站台或應用程式之失敗要求的相關記錄。</span><span class="sxs-lookup"><span data-stu-id="08163-237">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span></span> <span data-ttu-id="08163-238">您也必須在 **Web.config** 的 **system.WebServer** 下啟用追蹤選項。</span><span class="sxs-lookup"><span data-stu-id="08163-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="08163-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="08163-239">**DataSources**</span></span>|<span data-ttu-id="08163-240">要監視的目錄清單。</span><span class="sxs-lookup"><span data-stu-id="08163-240">A list of directories to monitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="08163-241">DataSources 元素</span><span class="sxs-lookup"><span data-stu-id="08163-241">DataSources Element</span></span>  
 <span data-ttu-id="08163-242">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources</span><span class="sxs-lookup"><span data-stu-id="08163-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="08163-243">要監視的目錄清單。</span><span class="sxs-lookup"><span data-stu-id="08163-243">A list of directories to monitor.</span></span>  

|<span data-ttu-id="08163-244">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-244">Child Elements</span></span>|<span data-ttu-id="08163-245">說明</span><span class="sxs-lookup"><span data-stu-id="08163-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="08163-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="08163-247">必要。</span><span class="sxs-lookup"><span data-stu-id="08163-247">Required.</span></span> <span data-ttu-id="08163-248">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="08163-249">**containerName** - 在您的 Azure 儲存體帳戶中用來儲存記錄檔的 Blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="08163-249">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="08163-250">DirectoryConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="08163-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="08163-251">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="08163-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="08163-252">可能包括 **Absolute** 或 **LocalResource** 元素，但非兩者。</span><span class="sxs-lookup"><span data-stu-id="08163-252">May include either the **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="08163-253">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-253">Child Elements</span></span>|<span data-ttu-id="08163-254">說明</span><span class="sxs-lookup"><span data-stu-id="08163-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="08163-255">**Absolute**</span></span>|<span data-ttu-id="08163-256">要監視之目錄的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="08163-256">The absolute path to the directory to monitor.</span></span> <span data-ttu-id="08163-257">以下為必要屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-257">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="08163-258">- **Path** - 要監視之目錄的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="08163-258">- **Path** - The absolute path to the directory to monitor.</span></span><br /><br /> <span data-ttu-id="08163-259">- **expandEnvironment** - 設定是否要展開 Path 中的環境變數。</span><span class="sxs-lookup"><span data-stu-id="08163-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="08163-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="08163-260">**LocalResource**</span></span>|<span data-ttu-id="08163-261">相對於要監視之本機資源的路徑。</span><span class="sxs-lookup"><span data-stu-id="08163-261">The path relative to a local resource to monitor.</span></span> <span data-ttu-id="08163-262">必要屬性包括：</span><span class="sxs-lookup"><span data-stu-id="08163-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="08163-263">- **Name** - 包含要監視之目錄的本機資源</span><span class="sxs-lookup"><span data-stu-id="08163-263">- **Name** - The local resource that contains the directory to monitor</span></span><br /><br /> <span data-ttu-id="08163-264">- **relativePath** - 包含要監視目錄之 Name 的相對路徑</span><span class="sxs-lookup"><span data-stu-id="08163-264">- **relativePath** - The path relative to Name that contains the directory to monitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="08163-265">EtwProviders 元素</span><span class="sxs-lookup"><span data-stu-id="08163-265">EtwProviders Element</span></span>  
 <span data-ttu-id="08163-266">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders</span><span class="sxs-lookup"><span data-stu-id="08163-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="08163-267">設定要收集來自 EventSource 和/或以 ETW 資訊清單為基礎之提供者的 ETW 事件。</span><span class="sxs-lookup"><span data-stu-id="08163-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="08163-268">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-268">Child Elements</span></span>|<span data-ttu-id="08163-269">說明</span><span class="sxs-lookup"><span data-stu-id="08163-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="08163-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="08163-271">設定要收集從 [EventSource 類別](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)產生的事件。</span><span class="sxs-lookup"><span data-stu-id="08163-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="08163-272">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="08163-273">**provider** - EventSource 事件的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="08163-273">**provider** - The class name of the EventSource event.</span></span><br /><br /> <span data-ttu-id="08163-274">選用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="08163-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="08163-275">- **scheduledTransferLogLevelFilter** - 要傳輸至儲存體帳戶的最低嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="08163-275">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="08163-276">- **scheduledTransferPeriod** - 排程傳輸至儲存體之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="08163-276">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="08163-277">值是 [XML「持續時間資料類型」(英文)](http://www.w3schools.com/schema/schema_dtypes_date.asp)。</span><span class="sxs-lookup"><span data-stu-id="08163-277">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="08163-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="08163-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="08163-279">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="08163-280">**provider** - 事件提供者的 GUID</span><span class="sxs-lookup"><span data-stu-id="08163-280">**provider** - The GUID of the event provider</span></span><br /><br /> <span data-ttu-id="08163-281">選用屬性包括：</span><span class="sxs-lookup"><span data-stu-id="08163-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="08163-282">- **scheduledTransferLogLevelFilter** - 要傳輸至儲存體帳戶的最低嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="08163-282">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="08163-283">- **scheduledTransferPeriod** - 排程傳輸至儲存體之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="08163-283">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="08163-284">值是 [XML「持續時間資料類型」(英文)](http://www.w3schools.com/schema/schema_dtypes_date.asp)。</span><span class="sxs-lookup"><span data-stu-id="08163-284">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="08163-285">EtwEventSourceProviderConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="08163-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="08163-286">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="08163-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="08163-287">設定要收集從 [EventSource 類別](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)產生的事件。</span><span class="sxs-lookup"><span data-stu-id="08163-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="08163-288">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-288">Child Elements</span></span>|<span data-ttu-id="08163-289">說明</span><span class="sxs-lookup"><span data-stu-id="08163-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="08163-290">**DefaultEvents**</span></span>|<span data-ttu-id="08163-291">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="08163-292">**eventDestination** - 要儲存事件的資料表名稱</span><span class="sxs-lookup"><span data-stu-id="08163-292">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="08163-293">**Event**</span><span class="sxs-lookup"><span data-stu-id="08163-293">**Event**</span></span>|<span data-ttu-id="08163-294">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="08163-295">**id** - 事件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="08163-295">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="08163-296">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="08163-297">**eventDestination** - 要儲存事件的資料表名稱</span><span class="sxs-lookup"><span data-stu-id="08163-297">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="08163-298">EtwManifestProviderConfiguration 元素</span><span class="sxs-lookup"><span data-stu-id="08163-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="08163-299">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="08163-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="08163-300">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-300">Child Elements</span></span>|<span data-ttu-id="08163-301">說明</span><span class="sxs-lookup"><span data-stu-id="08163-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="08163-302">**DefaultEvents**</span></span>|<span data-ttu-id="08163-303">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="08163-304">**eventDestination** - 要儲存事件的資料表名稱</span><span class="sxs-lookup"><span data-stu-id="08163-304">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="08163-305">**Event**</span><span class="sxs-lookup"><span data-stu-id="08163-305">**Event**</span></span>|<span data-ttu-id="08163-306">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="08163-307">**id** - 事件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="08163-307">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="08163-308">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="08163-309">**eventDestination** - 要儲存事件的資料表名稱</span><span class="sxs-lookup"><span data-stu-id="08163-309">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="08163-310">Metrics 元素</span><span class="sxs-lookup"><span data-stu-id="08163-310">Metrics Element</span></span>  
 <span data-ttu-id="08163-311">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics</span><span class="sxs-lookup"><span data-stu-id="08163-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="08163-312">讓您能夠產生已最佳化的效能計數器資料表來進行快速查詢。</span><span class="sxs-lookup"><span data-stu-id="08163-312">Enables you to generate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="08163-313">除了效能計數器資料表之外，**PerformanceCounters** 元素中所定義的每個效能計數器都會儲存於 Metrics 資料表中。</span><span class="sxs-lookup"><span data-stu-id="08163-313">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span></span>  

 <span data-ttu-id="08163-314">**resourceId** 是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="08163-314">The **resourceId** attribute is required.</span></span>  <span data-ttu-id="08163-315">您要部署 Azure 診斷的虛擬機器資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="08163-315">The resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="08163-316">從 [Azure 入口網站](https://portal.azure.com)取得 **resourceID**。</span><span class="sxs-lookup"><span data-stu-id="08163-316">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="08163-317">選取 [瀏覽][資源群組] ->  -> **<Name\>**。</span><span class="sxs-lookup"><span data-stu-id="08163-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="08163-318">按一下 [屬性] 圖格，並複製 [識別碼] 欄位的值。</span><span class="sxs-lookup"><span data-stu-id="08163-318">Click the **Properties** tile and copy the value from the **ID** field.</span></span>  

|<span data-ttu-id="08163-319">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-319">Child Elements</span></span>|<span data-ttu-id="08163-320">說明</span><span class="sxs-lookup"><span data-stu-id="08163-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="08163-321">**MetricAggregation**</span></span>|<span data-ttu-id="08163-322">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="08163-323">**scheduledTransferPeriod** - 排程傳輸至儲存體之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="08163-323">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="08163-324">值是 [XML「持續時間資料類型」(英文)](http://www.w3schools.com/schema/schema_dtypes_date.asp)。</span><span class="sxs-lookup"><span data-stu-id="08163-324">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="08163-325">PerformanceCounters 元素</span><span class="sxs-lookup"><span data-stu-id="08163-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="08163-326">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="08163-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="08163-327">啟用收集效能計數器。</span><span class="sxs-lookup"><span data-stu-id="08163-327">Enables the collection of performance counters.</span></span>  

 <span data-ttu-id="08163-328">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-328">Optional attribute:</span></span>  

 <span data-ttu-id="08163-329">選用的 **scheduledTransferPeriod** 屬性。</span><span class="sxs-lookup"><span data-stu-id="08163-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="08163-330">請參閱稍早的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-330">See explanation earlier.</span></span>

|<span data-ttu-id="08163-331">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-331">Child Element</span></span>|<span data-ttu-id="08163-332">說明</span><span class="sxs-lookup"><span data-stu-id="08163-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="08163-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="08163-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="08163-334">以下為必要屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-334">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="08163-335">- **counterSpecifier** - 效能計數器的名稱。</span><span class="sxs-lookup"><span data-stu-id="08163-335">- **counterSpecifier** - The name of the performance counter.</span></span> <span data-ttu-id="08163-336">例如： `\Processor(_Total)\% Processor Time`。</span><span class="sxs-lookup"><span data-stu-id="08163-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="08163-337">若要在主機上取得效能計數器清單，請執行 `typeperf` 命令。</span><span class="sxs-lookup"><span data-stu-id="08163-337">To get a list of performance counters on your host, run the command `typeperf`.</span></span><br /><br /> <span data-ttu-id="08163-338">- **sampleRate** - 應針對計數器進行取樣的頻率。</span><span class="sxs-lookup"><span data-stu-id="08163-338">- **sampleRate** - How often the counter should be sampled.</span></span><br /><br /> <span data-ttu-id="08163-339">選用屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="08163-340">**unit** - 計數器的測量單位。</span><span class="sxs-lookup"><span data-stu-id="08163-340">**unit** - The unit of measure of the counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="08163-341">WindowsEventLog 元素</span><span class="sxs-lookup"><span data-stu-id="08163-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="08163-342">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="08163-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="08163-343">啟用收集 Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="08163-343">Enables the collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="08163-344">選用的 **scheduledTransferPeriod** 屬性。</span><span class="sxs-lookup"><span data-stu-id="08163-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="08163-345">請參閱稍早的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="08163-346">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-346">Child Element</span></span>|<span data-ttu-id="08163-347">說明</span><span class="sxs-lookup"><span data-stu-id="08163-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="08163-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="08163-348">**DataSource**</span></span>|<span data-ttu-id="08163-349">要收集的 Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="08163-349">The Windows Event logs to collect.</span></span> <span data-ttu-id="08163-350">必要屬性：</span><span class="sxs-lookup"><span data-stu-id="08163-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="08163-351">**name** - 說明要收集之 Windows 事件的 XPath 查詢。</span><span class="sxs-lookup"><span data-stu-id="08163-351">**name** - The XPath query describing the windows events to be collected.</span></span> <span data-ttu-id="08163-352">例如：</span><span class="sxs-lookup"><span data-stu-id="08163-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="08163-353">若要收集所有事件，請指定 "*"</span><span class="sxs-lookup"><span data-stu-id="08163-353">To collect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="08163-354">Logs 元素</span><span class="sxs-lookup"><span data-stu-id="08163-354">Logs Element</span></span>  
 <span data-ttu-id="08163-355">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs</span><span class="sxs-lookup"><span data-stu-id="08163-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="08163-356">出現在 1.0 和 1.1 版中。</span><span class="sxs-lookup"><span data-stu-id="08163-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="08163-357">在 1.2 中消失。</span><span class="sxs-lookup"><span data-stu-id="08163-357">Missing in 1.2.</span></span> <span data-ttu-id="08163-358">再度新增於 1.3 中。</span><span class="sxs-lookup"><span data-stu-id="08163-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="08163-359">定義基本 Azure 記錄的緩衝區組態。</span><span class="sxs-lookup"><span data-stu-id="08163-359">Defines the buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="08163-360">屬性</span><span class="sxs-lookup"><span data-stu-id="08163-360">Attribute</span></span>|<span data-ttu-id="08163-361">類型</span><span class="sxs-lookup"><span data-stu-id="08163-361">Type</span></span>|<span data-ttu-id="08163-362">說明</span><span class="sxs-lookup"><span data-stu-id="08163-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="08163-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="08163-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="08163-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="08163-364">**unsignedInt**</span></span>|<span data-ttu-id="08163-365">選用。</span><span class="sxs-lookup"><span data-stu-id="08163-365">Optional.</span></span> <span data-ttu-id="08163-366">指定適用於所指定資料的檔案系統儲存體數量上限。</span><span class="sxs-lookup"><span data-stu-id="08163-366">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="08163-367">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="08163-367">The default is 0.</span></span>|  
|<span data-ttu-id="08163-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="08163-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="08163-369">**字串**</span><span class="sxs-lookup"><span data-stu-id="08163-369">**string**</span></span>|<span data-ttu-id="08163-370">選用。</span><span class="sxs-lookup"><span data-stu-id="08163-370">Optional.</span></span> <span data-ttu-id="08163-371">指定所傳輸記錄項目的最低嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="08163-371">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="08163-372">預設值為 **Undefined**，會傳輸所有記錄。</span><span class="sxs-lookup"><span data-stu-id="08163-372">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="08163-373">其他可能的值 (按照從大到小的順序排列) 為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。</span><span class="sxs-lookup"><span data-stu-id="08163-373">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="08163-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="08163-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="08163-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="08163-375">**duration**</span></span>|<span data-ttu-id="08163-376">選用。</span><span class="sxs-lookup"><span data-stu-id="08163-376">Optional.</span></span> <span data-ttu-id="08163-377">指定排程傳輸資料之間的間隔，無條件進位到最接近的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="08163-377">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="08163-378">預設值為 PT0S。</span><span class="sxs-lookup"><span data-stu-id="08163-378">The default is PT0S.</span></span>|  
|<span data-ttu-id="08163-379">**sinks** 已在 1.5 中新增</span><span class="sxs-lookup"><span data-stu-id="08163-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="08163-380">**字串**</span><span class="sxs-lookup"><span data-stu-id="08163-380">**string**</span></span>|<span data-ttu-id="08163-381">選用。</span><span class="sxs-lookup"><span data-stu-id="08163-381">Optional.</span></span> <span data-ttu-id="08163-382">同時要傳送診斷資料的接收位置指標。</span><span class="sxs-lookup"><span data-stu-id="08163-382">Points to a sink location to also send diagnostic data.</span></span> <span data-ttu-id="08163-383">例如 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="08163-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="08163-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="08163-384">DockerSources</span></span>
 <span data-ttu-id="08163-385">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources</span><span class="sxs-lookup"><span data-stu-id="08163-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="08163-386">已在 1.9 版中新增。</span><span class="sxs-lookup"><span data-stu-id="08163-386">Added in 1.9.</span></span>

|<span data-ttu-id="08163-387">元素名稱</span><span class="sxs-lookup"><span data-stu-id="08163-387">Element Name</span></span>|<span data-ttu-id="08163-388">說明</span><span class="sxs-lookup"><span data-stu-id="08163-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="08163-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="08163-389">**Stats**</span></span>|<span data-ttu-id="08163-390">會請系統收集 Docker 容器的統計資料</span><span class="sxs-lookup"><span data-stu-id="08163-390">Tells the system to collect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="08163-391">SinksConfig 元素</span><span class="sxs-lookup"><span data-stu-id="08163-391">SinksConfig Element</span></span>  
 <span data-ttu-id="08163-392">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig</span><span class="sxs-lookup"><span data-stu-id="08163-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="08163-393">傳送診斷資料的位置清單，以及與這些位置相關聯的組態。</span><span class="sxs-lookup"><span data-stu-id="08163-393">A list of locations to send diagnostics data to and the configuration associated with those locations.</span></span>  

|<span data-ttu-id="08163-394">元素名稱</span><span class="sxs-lookup"><span data-stu-id="08163-394">Element Name</span></span>|<span data-ttu-id="08163-395">說明</span><span class="sxs-lookup"><span data-stu-id="08163-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="08163-396">**接收**</span><span class="sxs-lookup"><span data-stu-id="08163-396">**Sink**</span></span>|<span data-ttu-id="08163-397">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="08163-398">Sink 元素</span><span class="sxs-lookup"><span data-stu-id="08163-398">Sink Element</span></span>
 <span data-ttu-id="08163-399">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink</span><span class="sxs-lookup"><span data-stu-id="08163-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="08163-400">已在 1.5 版中新增。</span><span class="sxs-lookup"><span data-stu-id="08163-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="08163-401">定義要傳送診斷資料的目標位置。</span><span class="sxs-lookup"><span data-stu-id="08163-401">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="08163-402">例如 Application Insights 服務。</span><span class="sxs-lookup"><span data-stu-id="08163-402">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="08163-403">屬性</span><span class="sxs-lookup"><span data-stu-id="08163-403">Attribute</span></span>|<span data-ttu-id="08163-404">類型</span><span class="sxs-lookup"><span data-stu-id="08163-404">Type</span></span>|<span data-ttu-id="08163-405">說明</span><span class="sxs-lookup"><span data-stu-id="08163-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="08163-406">**name**</span><span class="sxs-lookup"><span data-stu-id="08163-406">**name**</span></span>|<span data-ttu-id="08163-407">字串</span><span class="sxs-lookup"><span data-stu-id="08163-407">string</span></span>|<span data-ttu-id="08163-408">識別 sinkname 的字串。</span><span class="sxs-lookup"><span data-stu-id="08163-408">A string identifying the sinkname.</span></span>|  

|<span data-ttu-id="08163-409">元素</span><span class="sxs-lookup"><span data-stu-id="08163-409">Element</span></span>|<span data-ttu-id="08163-410">類型</span><span class="sxs-lookup"><span data-stu-id="08163-410">Type</span></span>|<span data-ttu-id="08163-411">說明</span><span class="sxs-lookup"><span data-stu-id="08163-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="08163-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="08163-412">**Application Insights**</span></span>|<span data-ttu-id="08163-413">字串</span><span class="sxs-lookup"><span data-stu-id="08163-413">string</span></span>|<span data-ttu-id="08163-414">僅會在將資料傳送至 Application Insights 時使用。</span><span class="sxs-lookup"><span data-stu-id="08163-414">Used only when sending data to Application Insights.</span></span> <span data-ttu-id="08163-415">包含您有權存取之使用中 Application Insights 帳戶的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="08163-415">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="08163-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="08163-416">**Channels**</span></span>|<span data-ttu-id="08163-417">字串</span><span class="sxs-lookup"><span data-stu-id="08163-417">string</span></span>|<span data-ttu-id="08163-418">每個可額外篩選該資料流的其中一個</span><span class="sxs-lookup"><span data-stu-id="08163-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="08163-419">Channels 元素</span><span class="sxs-lookup"><span data-stu-id="08163-419">Channels Element</span></span>  
 <span data-ttu-id="08163-420">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels</span><span class="sxs-lookup"><span data-stu-id="08163-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="08163-421">已在 1.5 版中新增。</span><span class="sxs-lookup"><span data-stu-id="08163-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="08163-422">針對通過接收之記錄資料的資料流定義篩選器。</span><span class="sxs-lookup"><span data-stu-id="08163-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="08163-423">元素</span><span class="sxs-lookup"><span data-stu-id="08163-423">Element</span></span>|<span data-ttu-id="08163-424">類型</span><span class="sxs-lookup"><span data-stu-id="08163-424">Type</span></span>|<span data-ttu-id="08163-425">說明</span><span class="sxs-lookup"><span data-stu-id="08163-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="08163-426">**Channel**</span><span class="sxs-lookup"><span data-stu-id="08163-426">**Channel**</span></span>|<span data-ttu-id="08163-427">字串</span><span class="sxs-lookup"><span data-stu-id="08163-427">string</span></span>|<span data-ttu-id="08163-428">請參閱本頁面上其他部分的說明。</span><span class="sxs-lookup"><span data-stu-id="08163-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="08163-429">Channel 元素</span><span class="sxs-lookup"><span data-stu-id="08163-429">Channel Element</span></span>
 <span data-ttu-id="08163-430">樹狀結構︰根目錄 - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel</span><span class="sxs-lookup"><span data-stu-id="08163-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="08163-431">已在 1.5 版中新增。</span><span class="sxs-lookup"><span data-stu-id="08163-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="08163-432">定義要傳送診斷資料的目標位置。</span><span class="sxs-lookup"><span data-stu-id="08163-432">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="08163-433">例如 Application Insights 服務。</span><span class="sxs-lookup"><span data-stu-id="08163-433">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="08163-434">屬性</span><span class="sxs-lookup"><span data-stu-id="08163-434">Attributes</span></span>|<span data-ttu-id="08163-435">類型</span><span class="sxs-lookup"><span data-stu-id="08163-435">Type</span></span>|<span data-ttu-id="08163-436">說明</span><span class="sxs-lookup"><span data-stu-id="08163-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="08163-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="08163-437">**logLevel**</span></span>|<span data-ttu-id="08163-438">**字串**</span><span class="sxs-lookup"><span data-stu-id="08163-438">**string**</span></span>|<span data-ttu-id="08163-439">指定所傳輸記錄項目的最低嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="08163-439">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="08163-440">預設值為 **Undefined**，會傳輸所有記錄。</span><span class="sxs-lookup"><span data-stu-id="08163-440">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="08163-441">其他可能的值 (按照從大到小的順序排列) 為 **Verbose**、**Information**、**Warning**、**Error** 及 **Critical**。</span><span class="sxs-lookup"><span data-stu-id="08163-441">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="08163-442">**name**</span><span class="sxs-lookup"><span data-stu-id="08163-442">**name**</span></span>|<span data-ttu-id="08163-443">**字串**</span><span class="sxs-lookup"><span data-stu-id="08163-443">**string**</span></span>|<span data-ttu-id="08163-444">要參考之通道的唯一名稱</span><span class="sxs-lookup"><span data-stu-id="08163-444">A unique name of the channel to refer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="08163-445">PrivateConfig 元素</span><span class="sxs-lookup"><span data-stu-id="08163-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="08163-446">樹狀結構︰根目錄 - DiagnosticsConfiguration - PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="08163-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="08163-447">已在 1.3 版中新增。</span><span class="sxs-lookup"><span data-stu-id="08163-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="08163-448">選用</span><span class="sxs-lookup"><span data-stu-id="08163-448">Optional</span></span>  

 <span data-ttu-id="08163-449">存放儲存體帳戶的私用詳細資料 (名稱、金鑰和端點)。</span><span class="sxs-lookup"><span data-stu-id="08163-449">Stores the private details of the storage account (name, key, and endpoint).</span></span> <span data-ttu-id="08163-450">此資訊會傳送至虛擬機器，但無法從中擷取。</span><span class="sxs-lookup"><span data-stu-id="08163-450">This information is sent to the virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="08163-451">子元素</span><span class="sxs-lookup"><span data-stu-id="08163-451">Child Elements</span></span>|<span data-ttu-id="08163-452">說明</span><span class="sxs-lookup"><span data-stu-id="08163-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="08163-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="08163-453">**StorageAccount**</span></span>|<span data-ttu-id="08163-454">要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="08163-454">The storage account to use.</span></span> <span data-ttu-id="08163-455">以下為必要屬性</span><span class="sxs-lookup"><span data-stu-id="08163-455">The following attributes are required</span></span><br /><br /> <span data-ttu-id="08163-456">- **name** - 儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="08163-456">- **name** - The name of the storage account.</span></span><br /><br /> <span data-ttu-id="08163-457">- **key** - 儲存體帳戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="08163-457">- **key** - The key to the storage account.</span></span><br /><br /> <span data-ttu-id="08163-458">- **endpoint** - 要存取儲存體帳戶的端點。</span><span class="sxs-lookup"><span data-stu-id="08163-458">- **endpoint** - The endpoint to access the storage account.</span></span> <br /><br /> <span data-ttu-id="08163-459">-**sasToken** (已在 1.8.1 版中新增) - 您可以在私用組態中指定 SAS 權杖 (而不是儲存體帳戶金鑰)。</span><span class="sxs-lookup"><span data-stu-id="08163-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="08163-460">如果提供此屬性，系統會忽略儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="08163-460">If provided, the storage account key is ignored.</span></span> <br /><span data-ttu-id="08163-461">SAS 權杖的需求︰</span><span class="sxs-lookup"><span data-stu-id="08163-461">Requirements for the SAS Token:</span></span> <br /><span data-ttu-id="08163-462">- 僅支援帳戶 SAS 權杖</span><span class="sxs-lookup"><span data-stu-id="08163-462">- Supports account SAS token only</span></span> <br /><span data-ttu-id="08163-463">- 需要 b、t 服務類型。</span><span class="sxs-lookup"><span data-stu-id="08163-463">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="08163-464">- 需要 a、c、u、w 權限。</span><span class="sxs-lookup"><span data-stu-id="08163-464">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="08163-465">- 需要 c、o 資源類型。</span><span class="sxs-lookup"><span data-stu-id="08163-465">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="08163-466">- 僅支援 HTTPS 通訊協定</span><span class="sxs-lookup"><span data-stu-id="08163-466">- Supports the HTTPS protocol only</span></span> <br /> <span data-ttu-id="08163-467">- 開始和到期時間必須是有效的。</span><span class="sxs-lookup"><span data-stu-id="08163-467">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="08163-468">IsEnabled 元素</span><span class="sxs-lookup"><span data-stu-id="08163-468">IsEnabled Element</span></span>  
 <span data-ttu-id="08163-469">樹狀結構︰根目錄 - DiagnosticsConfiguration - IsEnabled</span><span class="sxs-lookup"><span data-stu-id="08163-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="08163-470">布林值。</span><span class="sxs-lookup"><span data-stu-id="08163-470">Boolean.</span></span> <span data-ttu-id="08163-471">使用 `true` 來啟用診斷或 `false` 來停用診斷。</span><span class="sxs-lookup"><span data-stu-id="08163-471">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span></span>
