---
title: "aaaHow toouse 中虛擬機器的 Azure 診斷 |Microsoft 文件"
description: "偵錯、 測量效能、 監視、 流量分析和其他使用 Azure 診斷 toogather 資料從 Azure 虛擬機器。"
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>在 Azure 虛擬機器中啟用診斷
如需有關 Azure 診斷的背景資訊，請參閱 [Azure 診斷概觀](../monitoring-and-diagnostics/azure-diagnostics.md) 。

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a>如何 tooEnable 虛擬機器中的診斷
此逐步說明 tooremotely 從開發電腦所安裝的診斷 tooan Azure 虛擬機器。 您也了解如何在 Azure 虛擬機器上執行，並發出使用遙測資料的應用程式 tooimplement hello.NET [EventSource 類別][EventSource Class]。 Azure 診斷功能會使用的 toocollect hello 遙測，並將它儲存在 Azure 儲存體帳戶。

### <a name="pre-requisites"></a>必要條件
這個逐步解說假設您有 Azure 訂用帳戶，並使用 Visual Studio 2017 以 hello Azure SDK。 如果您沒有 Azure 訂用帳戶，您可以申請 hello[免費試用版][Free Trial]。 請確定太[安裝和設定 Azure PowerShell 0.8.7 版或更新版本][Install and configure Azure PowerShell version 0.8.7 or later]。

### <a name="step-1-create-a-virtual-machine"></a>步驟 1：建立虛擬機器
1. 在您的開發電腦上，啟動 Visual Studio 2017。
2. Hello Visual Studio 中**伺服器總管**展開**Azure**，以滑鼠右鍵按一下**虛擬機器**然後選取**建立虛擬機器**。
3. 選取您的 Azure 訂用帳戶中 hello**選擇訂用帳戶**對話方塊，再按一下**下一步**。
4. 選取**Windows Server 2012 R2 Datacenter，2017 年 6 月**在 hello**選取虛擬機器映像**對話方塊，再按一下**下一步**。
5. 在 hello**虛擬機器基本設定**，設定 hello 虛擬機器名稱太"wadexample"。 設定您的系統管理員使用者名稱和密碼，然後按 [下一步] 。
6. 在 hello**雲端服務設定**對話方塊建立新的雲端服務，名為"wadexampleVM"。 建立名為 "wadexample" 的新儲存體帳戶，然後按 [ **下一步**]。
7. 按一下 [建立] 。

### <a name="step-2-create-your-application"></a>步驟 2：建立您的應用程式
1. 在您的開發電腦上，啟動 Visual Studio 2017。
2. 建立以 .NET Framework 4.5 為目標的新 Visual C# 主控台應用程式。 Hello 專案名稱"WadExampleVM"。

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. 取代下列程式碼的 hello hello Program.cs 的內容。 hello 類別**SampleEventSourceWriter**實作四個記錄的方法： **SendEnums**， **MessageMethod**， **SetOther**和**HighFreq**。 第一個參數 toohello hello WriteEvent 方法定義 hello hello 各事件的識別碼。 hello Run 方法實作無限的迴圈記錄 hello 中實作的方法會呼叫每個 hello **SampleEventSourceWriter**類別每隔 10 秒。

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through hello loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. 儲存 hello 檔案，並選取**建置方案**從 hello**建置**功能表 toobuild 您的程式碼。

### <a name="step-3-deploy-your-application"></a>步驟 3：部署應用程式
1. 以滑鼠右鍵按一下 hello **WadExampleVM**專案中**方案總管 中**選擇**在檔案總管 中開啟資料夾**。
2. 瀏覽 toohello *bin\Debug*資料夾和所有 hello 的複製檔案 (WadExampleVM.*)
3. 在**伺服器總管**hello 虛擬機器上按一下滑鼠右鍵，然後選擇 **使用遠端桌面連線**。
4. 一旦連接 toohello VM 建立名為 WadExampleVM 的資料夾，並將您的應用程式的檔案貼到 hello 資料夾。
5. 啟動 hello 應用程式 WadExampleVM.exe。 您應該會看見空白的主控台視窗。

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a>步驟 4： 建立診斷組態和安裝 hello 延伸模組
1. 藉由執行下列 PowerShell 命令的 hello 下載 hello 公用組態檔結構描述定義 tooyour 開發電腦：

     (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
2. 在已開啟專案的 Visual Studio 中，或在未開啟專案的 Visual Studio 執行個體中，開啟新的 XML 檔。 在 Visual Studio 中，選取 [新增] -> [新項目...] -> [Visual C# 項目] -> [資料] -> [XML 檔案]。 Hello 檔案命名為"WadExample.xml"
3. Hello WadConfig.xsd 關聯 hello 設定檔。 請確定 hello WadExample.xml 編輯器視窗 hello 作用中視窗。 按**F4** tooopen hello**屬性**視窗。 按一下 hello**結構描述**屬性在 hello**屬性**視窗。 按一下 hello **...** 在 hello**結構描述**屬性。 按一下 hello**新增...** 按鈕，然後瀏覽儲存 hello XSD 檔案，以及選取 hello 檔案 WadConfig.xsd toohello 位置。 按一下 [確定] 。
4. 以下列 XML 的 hello 和儲存 hello 檔案，請取代 hello 內容 hello WadExample.xml 組態檔。 此組態檔會定義幾個效能計數器 toocollect: CPU 使用率和記憶體使用率。 然後 hello 組態會定義對應 toohello 方法 hello SampleEventSourceWriter 類別中的 hello 四個事件。

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a>步驟 5：從遠端將診斷安裝至您的 Azure 虛擬機器上
hello 管理診斷在 VM 上的 PowerShell cmdlet 是： 集 AzureVMDiagnosticsExtension、 Get AzureVMDiagnosticsExtension，以及移除 AzureVMDiagnosticsExtension。

1. 在您的開發電腦上，開啟 Azure PowerShell。
2. 在您的 VM 上執行 hello 指令碼 tooremotely 安裝診斷 (取代`<user>`以您使用者的目錄名稱。 取代`<StorageAccountKey>`與 hello wadexamplevm 儲存體帳戶的儲存體帳戶金鑰):
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a>步驟 6：查看您的遙測資料
在 Visual Studio hello**伺服器總管**瀏覽 toohello wadexample 儲存體帳戶。 Hello 執行 VM 約 5 分鐘之後，您應該看到 hello 資料表**WADEnumsTable**， **WADHighFreqTable**， **WADMessageTable**， **WADPerformanceCountersTable**和**WADSetOtherTable**。 按兩下其中一個 hello 資料表 tooview hello 遙測收集而來。

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>組態檔結構描述
hello 診斷組態檔定義 hello 診斷代理程式啟動時，會使用的 tooinitialize 診斷的組態設定的值。 請參閱 hello[最新的結構描述參考](https://msdn.microsoft.com/library/azure/mt634524.aspx)有效的值和範例。

## <a name="troubleshooting"></a>疑難排解
如需詳細資訊，請參閱 [Azure 診斷的疑難排解](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) 。

## <a name="next-steps"></a>後續步驟
[虛擬機器的清單，請參閱相關的 Azure 診斷文章](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics)toochange hello 資料收集之後，問題進行疑難排解，或深入了解診斷一般。

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
