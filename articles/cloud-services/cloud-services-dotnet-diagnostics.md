---
title: "aaaHow toouse 與雲端服務的 Azure 診斷 (.NET) |Microsoft 文件"
description: "使用 Azure 診斷 toogather 資料從 Azure 雲端服務進行偵錯，測量效能、 監視、 流量分析和更多。"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a>在 Azure 雲端服務中啟用 Azure 診斷
如需有關 Azure 診斷的背景資訊，請參閱 [Azure 診斷概觀](../azure-diagnostics.md) 。

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a>如何 tooEnable 背景工作角色中的診斷
本逐步解說描述如何 tooimplement 發出遙測資料使用的 Azure 背景工作角色 hello.NET EventSource 類別。 Azure 診斷功能會使用的 toocollect hello 遙測資料，並將它儲存在 Azure 儲存體帳戶。 建立背景工作角色時，Visual Studio 會自動啟用診斷 1.0 做為 Azure Sdk for.NET 2.4 及更早版本中的 hello 方案的一部分。 hello 下列指示描述 hello 程序建立 hello 背景工作角色，從 hello 方案停用診斷 1.0 及部署診斷 1.2 或 1.3 tooyour 背景工作角色。

### <a name="prerequisites"></a>必要條件
本文假設您有 Azure 訂用帳戶，並使用 Visual Studio 以 hello Azure SDK。 如果您沒有 Azure 訂用帳戶，您可以申請 hello[免費試用版][Free Trial]。 請確定太[安裝和設定 Azure PowerShell 0.8.7 版或更新版本][Install and configure Azure PowerShell version 0.8.7 or later]。

### <a name="step-1-create-a-worker-role"></a>步驟 1：建立背景工作角色
1. 啟動 **Visual Studio**。
2. 建立**Azure 雲端服務**專案從 hello**雲端**以.NET Framework 4.5 為目標的範本。  Hello 專案 」 WadExample 」 的名稱，然後按一下 [確定]。
3. 選取 [ **背景工作角色** ] 並按一下 [確定]。 將會建立 hello 專案。
4. 在**方案總管 中**，按兩下 hello **WorkerRole1**屬性檔。
5. 在 hello**組態**索引標籤上，取消核取**啟用診斷**toodisable Diagnostics 1.0 (2.4 及更早版本 Azure SDK)。
6. 建置方案 tooverify 未出現任何錯誤。

### <a name="step-2-instrument-your-code"></a>步驟 2：實作您的程式碼
取代下列程式碼的 hello WorkerRole.cs hello 內容。 hello 類別 SampleEventSourceWriter，繼承自 hello [EventSource 類別][EventSource Class]，實作四個記錄的方法： **SendEnums**， **MessageMethod**， **SetOther**和**HighFreq**。 hello 第一個參數 toohello **WriteEvent**方法定義 hello hello 各事件的識別碼。 hello Run 方法實作無限的迴圈記錄 hello 中實作的方法會呼叫每個 hello **SampleEventSourceWriter**類別每隔 10 秒。

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a>步驟 3：部署您的背景工作角色

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. 部署您從背景工作角色 tooAzure，Visual Studio 中的，選取 hello **WadExample** hello 然後方案總管 中的專案**發行**從 hello**建置**功能表。
2. 選擇您的訂用帳戶。
3. 在 hello **Microsoft Azure 發行設定**對話方塊中，選取**新建...**.
4. 在 hello**建立雲端服務和儲存體帳戶** 對話方塊中，輸入**名稱**(例如，"WadExample")，並選取區域或同質群組。
5. 設定 hello**環境**太**臨時**。
6. 適當地修改其他任何 [設定]，然後按一下 [發佈]。
7. 部署已完成之後，請確認在 Azure 入口網站，您的雲端服務中的 hello**執行**狀態。

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a>步驟 4： 建立您的診斷組態檔，並安裝 hello 擴充功能
1. 藉由執行下列 PowerShell 命令的 hello 下載 hello 公用組態檔結構描述定義：

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. 新增 XML 檔案 tooyour **WorkerRole1**專案，以滑鼠右鍵按一下 hello **WorkerRole1**專案，然後選取**新增** -> **新項目...** -> [Visual C# 項目] -> [資料] -> [XML 檔案]。 Hello 檔案名稱"WadExample.xml"。

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. Hello WadConfig.xsd 關聯 hello 設定檔。 請確定 hello WadExample.xml 編輯器視窗 hello 作用中視窗。 按**F4** tooopen hello**屬性**視窗。 按一下 hello**結構描述**屬性在 hello**屬性**視窗。 按一下 hello **...** 在 hello**結構描述**屬性。 按一下 hello**新增...** 按鈕，然後瀏覽儲存 hello XSD 檔案，以及選取 hello 檔案 WadConfig.xsd toohello 位置。 按一下 [確定] 。

4. 以下列 XML 的 hello 和儲存 hello 檔案，請取代 hello 內容 hello WadExample.xml 組態檔。 此組態檔會定義幾個效能計數器 toocollect: CPU 使用率和記憶體使用率。 然後 hello 組態會定義對應 toohello 方法 hello SampleEventSourceWriter 類別中的 hello 四個事件。

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a>步驟 5：在您的背景工作角色上安裝診斷
hello PowerShell cmdlet 來管理診斷 web 或背景工作角色是： 集 AzureServiceDiagnosticsExtension、 Get AzureServiceDiagnosticsExtension，以及移除 AzureServiceDiagnosticsExtension。

1. 開啟 Azure PowerShell。
2. 在工作者角色上執行 hello 指令碼 tooinstall 診斷 (取代*StorageAccountKey*與 hello wadexample 儲存體帳戶的儲存體帳戶金鑰和*config_path* hello 路徑toohello *WadExample.xml*檔案):

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a>步驟 6：查看您的遙測資料
在 Visual Studio hello**伺服器總管**，瀏覽 toohello wadexample 儲存體帳戶。 Hello 雲端服務已經執行約 5 分鐘之後，您應該會看到 hello 資料表**WADEnumsTable**， **WADHighFreqTable**， **WADMessageTable**， **WADPerformanceCountersTable**和**WADSetOtherTable**。 按兩下其中一個 hello 資料表 tooview hello 遙測收集而來。

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a>組態檔結構描述
hello 診斷組態檔定義 hello 診斷代理程式啟動時，會使用的 tooinitialize 診斷的組態設定的值。 請參閱 hello[最新的結構描述參考](https://msdn.microsoft.com/library/azure/mt634524.aspx)有效的值和範例。

## <a name="troubleshooting"></a>疑難排解
如果您遇到困難，請參閱 [Azure 診斷的疑難排解](../azure-diagnostics-troubleshooting.md) ，以解決常見的問題。

## <a name="next-steps"></a>後續步驟
[看到一份相關 Azure 的虛擬機器診斷文章](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics)toochange hello 資料收集之後，問題進行疑難排解，或深入了解診斷一般。

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
