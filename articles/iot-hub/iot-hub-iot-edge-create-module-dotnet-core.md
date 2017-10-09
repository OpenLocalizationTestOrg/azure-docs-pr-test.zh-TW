---
title: "使用 C# 的 Azure IoT 邊緣模組 aaaCreate |Microsoft 文件"
description: "本教學課程會示範如何 toowrite b 資料轉換器模組使用 hello 最新的 Azure IoT 邊緣 NuGet 封裝，Visual Studio 程式碼和 C#。"
services: iot-hub
author: jeffreyCline
manager: timlt
keywords: "azure, iot, 教學課程, 模組, nuget, vscode, csharp, edge"
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: jcline
ms.openlocfilehash: b104609c05d1613e21acc7d7bed547f311179151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a>使用 C&#x23; 建立 Azure IoT Edge 模組

本教學課程示範如何適用於模組的 toocreate`Azure IoT Edge`使用`Visual Studio Code`和`C#`。

在本教學課程中，我們將逐步檢視環境的設定以及如何 toowrite [b](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy)資料轉換器模組使用最新 hello`Azure IoT Edge NuGet`封裝。 

>[!NOTE]
本教學課程使用 hello `.NET Core SDK`，可支援跨平台相容性。 hello 下列教學課程以使用 hello`Windows 10`作業系統。 本教學課程中的 hello 命令的某些可能會不同，取決於您`development environment`。 

## <a name="prerequisites"></a>必要條件

在本節中，我們會針對 `Azure IoT Edge` 模組開發設定您的環境。 它會套用 tooboth **64 位元 Windows**和**64 位元 Linux (Ubuntu/Debian 8)**作業系統。

hello 下列軟體，則需要：

- [Git 用戶端](https://git-scm.com/downloads)
- [.NET Core SDK](https://www.microsoft.com/net/core#windowscmd)
- [Visual Studio Code](https://code.visualstudio.com/)

您不需要為此範例 tooclone hello 儲存機制，不過所有 hello 範例在本教學課程所討論的程式碼都位於下列儲存機制的 hello:

- `git clone https://github.com/Azure-Samples/iot-edge-samples.git`。
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a>開始使用

1. 安裝 `.NET Core SDK`。
2. 安裝`Visual Studio Code`和 hello`C# extension`從 Visual Studio 程式碼 Marketplace hello。

檢視此[快速的視訊教學課程](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows)有關 tooget 如何開始使用`Visual Studio Code`和 hello `.NET Core SDK`。

## <a name="creating-hello-azure-iot-edge-converter-module"></a>建立 hello Azure IoT 邊緣轉換器模組

1. 初始化新 `.NET Core` 類別庫 C# 專案：
    - 開啟命令提示字元 (`Windows + R` -> `cmd` -> `enter`)。
    - 瀏覽您要 toocreate hello toohello 資料夾`C#`專案。
    - 輸入 **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**。 
    - 此命令會在專案目錄中建立名為 `Class1.cs` 的空類別。
2. 瀏覽 toohello 我們剛建立的資料夾 hello 類別庫專案輸入**cd IoTEdgeConverterModule**。
3. 在開啟 hello 專案`Visual Studio Code`輸入**程式碼。**。
4. 一旦 hello 專案以`Visual Studio Code`，按一下 hello **IoTEdgeConverterModule.csproj** tooopen hello 檔案 hello 下列影像所示：

    ![Visual Studio Code 編輯視窗](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. 插入 hello `XML` hello 之間 hello 關閉下列程式碼片段所示的 blob`PropertyGroup`標記並 hello 關閉`Project`標記; 行六個 in hello 前面映像並按下儲存 hello 檔案`Ctrl`  +  `S`.

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. 一旦您儲存 hello`.csproj`檔案，`Visual Studio Code`應該會提示您使用`unresolved dependencies`對話方塊 hello 下列影像所示： 

    ![Visual Studio Code 還原相依性對話方塊](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    a） 按一下`Restore`toorestore hello 專案中的 hello 所有參考`.csproj`檔案包括 hello`PackageReferences`我們新增了。 

    b)`Visual Studio Code`會自動建立 hello`project.assets.json`專案中的檔案`obj`資料夾。 此檔案包含您的專案相依性 toomake 後續還原更快的相關資訊。
 
    >[!NOTE]
    `.NET Core Tools` 現在以 MSBuild 為基礎。 這表示會建立 `.csproj` 專案檔案而非 `project.json`。

    - 如果 `Visual Studio Code` 沒有提示您也沒有關係，我們可以手動執行此動作。 開啟 hello`Visual Studio Code`整合終端機視窗按 hello `Ctrl`  +  `backtick`鍵，或使用 hello 功能表`View`  ->  `Integrated Terminal`。
    - 在 hello`Integrated Terminal`視窗類型**dotnet 還原**。
    
7. 重新命名 hello`Class1.cs`檔案太`BleConverterModule.cs`。 

    a) toorename hello 檔案先 hello 檔案上按一下，然後按下 hello`F2`索引鍵。
    
    b） 在 hello 新名稱的型別**BleConverterModule**、 hello 下列影像所示：

    ![重新命名類別的 Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. Hello hello 中的現有程式碼取代`BleConverterModule.cs`檔案複製並貼上下列程式碼片段至的 hello 您`BleConverterModule.cs`檔案。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Globalization;
   using System.Linq;
   using System.Text;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace IoTEdgeConverterModule
   {
       public class BleConverterModule : IGatewayModule, IGatewayModuleStart
       {
           private Broker broker;
           private string configuration;
           private int messageCount;

           public void Create(Broker broker, byte[] configuration)
           {
               this.broker = broker;
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Start()
           {
           }

           public void Destroy()
           {
           }

           public void Receive(Message received_message)
           {
               string recMsg = Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               BleData receivedData = JsonConvert.DeserializeObject<BleData>(recMsg);

               float temperature = float.Parse(receivedData.Temperature, CultureInfo.InvariantCulture.NumberFormat); 
               Dictionary<string, string> receivedProperties = received_message.Properties;
            
               Dictionary<string, string> properties = new Dictionary<string, string>();
               properties.Add("source", receivedProperties["source"]);
               properties.Add("macAddress", receivedProperties["macAddress"]);
               properties.Add("temperatureAlert", temperature > 30 ? "true" : "false");
   
               String content = String.Format("{0} \"deviceId\": \"Intel NUC Gateway\", \"messageId\": {1}, \"temperature\": {2} {3}", "{", ++this.messageCount, temperature, "}");
               Message messageToPublish = new Message(content, properties);
   
               this.broker.Publish(messageToPublish);
           }
       }
   }
   ```

9. 按下儲存 hello 檔案`Ctrl`  +  `S`。

10. 建立新的檔案稱為`Untitled-1`所按的 hello `Ctrl`  +  `N`金鑰 hello 下列影像所示：

    ![Visual Studio Code 新檔案](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. toodeserialize hello`JSON`物件，我們收到 hello 模擬`BLE`裝置、 hello 成下列程式碼複製 hello`Untitled-1`檔案的程式碼編輯器 視窗。 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace IoTEdgeConverterModule
   {
       public class BleData
       {
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

12. 將 hello 檔案儲存為`BleData.cs`按`Ctrl`  +  `Shift`  +  `S`索引鍵。
    - Hello 上將儲存為對話方塊中，在 hello`Save as Type`下拉式功能表中，選取`C# (*.cs;*.csx)`hello 下列影像所示：

    ![Visual Studio Code 另存新檔對話方塊](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. 建立新的檔案稱為`Untitled-1`所按的 hello `Ctrl`  +  `N`索引鍵。

14. 複製並貼上下列程式碼片段至 hello hello`Untitled-1`檔案。 這個類別是`Azure IoT Edge`模組，我們會使用來自 toooutput hello 資料我們`BleConverterModule`。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace PrinterModule
   {
       public class DotNetPrinterModule : IGatewayModule
       {
           private string configuration;
           public void Create(Broker broker, byte[] configuration)
           {
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Destroy()
           {
           }
   
           public void Receive(Message received_message)
           {
               string recMsg = System.Text.Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               Dictionary<string, string> receivedProperties = received_message.Properties;
               
               BleConverterData receivedData = JsonConvert.DeserializeObject<BleConverterData>(recMsg);
   
               Console.WriteLine();
               Console.WriteLine("Module           : [DotNetPrinterModule]");
               Console.WriteLine("received_message : {0}", recMsg);
   
               if(received_message.Properties["source"] == "bleTelemetry")
               {
                   Console.WriteLine("Source           : {0}", receivedProperties["source"]);
                   Console.WriteLine("MAC address      : {0}", receivedProperties["macAddress"]);
                   Console.WriteLine("Temperature Alert: {0}", receivedProperties["temperatureAlert"]);
                   Console.WriteLine("Deserialized Obj : [BleConverterData]");
                   Console.WriteLine("  DeviceId       : {0}", receivedData.DeviceId);
                   Console.WriteLine("  MessageId      : {0}", receivedData.MessageId);
                   Console.WriteLine("  Temperature    : {0}", receivedData.Temperature);
               }
   
               Console.WriteLine();
           }
       }
   }
   ```

15. 將 hello 檔案儲存為`DotNetPrinterModule.cs`按`Ctrl`  +  `Shift`  +  `S`。
    - Hello 上將儲存為對話方塊中，在 hello`Save as Type`下拉式功能表中，選取`C# (*.cs;*.csx)`。

16. 建立新的檔案稱為`Untitled-1`所按的 hello `Ctrl`  +  `N`索引鍵。

17. toodeserialize hello`JSON`物件，我們收到 hello `BleConverterModule`，複製和貼上 hello 下列程式碼片段至 hello`Untitled-1`檔案。 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace PrinterModule
   {
       public class BleConverterData
       {
           [JsonProperty(PropertyName = "deviceId")]
           public string DeviceId { get; set; }
   
           [JsonProperty(PropertyName = "messageId")]
           public string MessageId { get; set; }
   
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

18. 將 hello 檔案儲存為`BleConverterData.cs`按`Ctrl`  +  `Shift`  +  `S`。
    - Hello 上將儲存為對話方塊中，在 hello`Save as Type`下拉式功能表中，選取`C# (*.cs;*.csx)`。

19. 建立新的檔案稱為`Untitled-1`所按的 hello `Ctrl`  +  `N`索引鍵。

20. 複製並貼上下列程式碼片段至 hello hello`Untitled-1`檔案。

   ```json
   {
       "loaders": [
           {
               "type": "dotnetcore",
               "name": "dotnetcore",
               "configuration": {
                   "binding.path": "dotnetcore.dll",
                   "binding.coreclrpath": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\coreclr.dll",
                   "binding.trustedplatformassemblieslocation": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\"
               }
           }
       ],
          "modules": [
           {
               "name": "simulated_device",
               "loader": {
                   "name": "native",
                   "entrypoint": {
                       "module.path": "simulated_device.dll"
                   }
               },
               "args": {
                   "macAddress": "01:02:03:03:02:01",
                   "messagePeriod": 500
               }
           },
           {
               "name": "ble_converter_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "IoTEdgeConverterModule.BleConverterModule"
                   }
               },
               "args": ""
           },
           {
               "name": "printer_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "PrinterModule.DotNetPrinterModule"
                   }
               },
               "args": ""
           }
       ],
       "links": [
           {
               "source": "simulated_device", "sink": "ble_converter_module"
           },
           {
               "source": "ble_converter_module", "sink": "printer_module"
           }
   ]
   }
   ```

21. 將 hello 檔案儲存為`gw-config.json`按`Ctrl`  +  `Shift`  +  `S`。
    - Hello 上將儲存為對話方塊中，在 hello`Save as Type`下拉式功能表中，選取`JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`。

22. tooenable 複製 hello 設定檔 toohello 的輸出目錄中，更新 hello`IoTEdgeConverterModule.csproj`以下列 XML blob 的 hello:

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - 更新的 hello`IoTEdgeConverterModule.csproj`應該看起來像 hello 下列映像：

    ![Visual Studio Code 更新後的 .csproj 檔案](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. 建立新的檔案稱為`Untitled-1`所按的 hello `Ctrl`  +  `N`索引鍵。

24. 複製並貼上下列程式碼片段至 hello hello`Untitled-1`檔案。

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. 將 hello 檔案儲存為`binplace.ps1`按`Ctrl`  +  `Shift`  +  `S`。
    - Hello 上將儲存為對話方塊中，在 hello`Save as Type`下拉式功能表中，選取`PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`。

26. 按下 hello 建置 hello 專案`Ctrl`  +  `Shift`  +  `B`索引鍵。 當您第一次建置 hello 的 hello 專案`Visual Studio Code`會提示您以 hello`No build task defined.`對話方塊 hello 下列影像所示：

    ![Visual Studio Code 建置工作對話方塊](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    a） 按一下 hello `Configure Build Task`  按鈕。

    b） 在 hello`Select a Task Runner`對話方塊下拉式功能表。 選取`.NET Core`hello 下列影像所示： 

    ![Visual Studio Code 選取工作對話方塊](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    c） 按一下 hello`.NET Core`項目建立 hello`tasks.json`檔案中您`.vscode`目錄，並開啟 hello 檔案在 hello`code editor`視窗。 沒有任何需要 toomodify 此檔案，請關閉 hello 索引標籤。

27.  開啟 hello`Visual Studio Code`整合終端機視窗按 hello `Ctrl`  +  `backtick`鍵，或使用 hello 功能表`View`  ->  `Integrated Terminal`和型別**.\binplace.ps1**到 hello`PowerShell`命令提示字元。 此命令會複製所有我們相依性 toohello 輸出目錄。

28. 瀏覽 toohello 專案輸出目錄中 hello`Integrated Terminal`視窗輸入**cd.\bin\Debug\netstandard1.3**。

29. 輸入執行 hello 範例專案**。 \gw.exe gw config.json**到 hello`Integrated Terminal`視窗提示。 
    - 如果您有密切遵循 hello 步驟在本教學課程，您應該立即執行 hello `Azure IoT Edge BLE Data Converter Module` hello 下列影像所示的範例專案：
    
        ![在 Visual Studio Code 中執行的模擬裝置範例](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - 如果您想 tooterminate hello 應用程式，請按 hello`<Enter>`索引鍵。

>[!IMPORTANT]
建議您不要 toouse `Ctrl`  +  `C` tooterminate hello`IoT Edge`閘道應用程式 (也就是**gw.exe**)。 為此動作可能導致 hello 程序 tooterminate 異常。

