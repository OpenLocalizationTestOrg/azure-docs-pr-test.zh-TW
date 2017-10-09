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
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="76048-104">使用 C&#x23; 建立 Azure IoT Edge 模組</span><span class="sxs-lookup"><span data-stu-id="76048-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="76048-105">本教學課程示範如何適用於模組的 toocreate`Azure IoT Edge`使用`Visual Studio Code`和`C#`。</span><span class="sxs-lookup"><span data-stu-id="76048-105">This tutorial showcases how toocreate a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="76048-106">在本教學課程中，我們將逐步檢視環境的設定以及如何 toowrite [b](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy)資料轉換器模組使用最新 hello`Azure IoT Edge NuGet`封裝。</span><span class="sxs-lookup"><span data-stu-id="76048-106">In this tutorial, we walk through environment set-up and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="76048-107">本教學課程使用 hello `.NET Core SDK`，可支援跨平台相容性。</span><span class="sxs-lookup"><span data-stu-id="76048-107">This tutorial is using hello `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="76048-108">hello 下列教學課程以使用 hello`Windows 10`作業系統。</span><span class="sxs-lookup"><span data-stu-id="76048-108">hello following tutorial is written using hello `Windows 10` operating system.</span></span> <span data-ttu-id="76048-109">本教學課程中的 hello 命令的某些可能會不同，取決於您`development environment`。</span><span class="sxs-lookup"><span data-stu-id="76048-109">Some of hello commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="76048-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="76048-110">Prerequisites</span></span>

<span data-ttu-id="76048-111">在本節中，我們會針對 `Azure IoT Edge` 模組開發設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="76048-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="76048-112">它會套用 tooboth **64 位元 Windows**和**64 位元 Linux (Ubuntu/Debian 8)**作業系統。</span><span class="sxs-lookup"><span data-stu-id="76048-112">It applies tooboth **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="76048-113">hello 下列軟體，則需要：</span><span class="sxs-lookup"><span data-stu-id="76048-113">hello following software is required:</span></span>

- [<span data-ttu-id="76048-114">Git 用戶端</span><span class="sxs-lookup"><span data-stu-id="76048-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="76048-115">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="76048-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="76048-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="76048-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="76048-117">您不需要為此範例 tooclone hello 儲存機制，不過所有 hello 範例在本教學課程所討論的程式碼都位於下列儲存機制的 hello:</span><span class="sxs-lookup"><span data-stu-id="76048-117">You do not need tooclone hello repo for this sample, however all of hello sample code discussed in this tutorial is located in hello following repository:</span></span>

- <span data-ttu-id="76048-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`。</span><span class="sxs-lookup"><span data-stu-id="76048-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="76048-119">開始使用</span><span class="sxs-lookup"><span data-stu-id="76048-119">Getting started</span></span>

1. <span data-ttu-id="76048-120">安裝 `.NET Core SDK`。</span><span class="sxs-lookup"><span data-stu-id="76048-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="76048-121">安裝`Visual Studio Code`和 hello`C# extension`從 Visual Studio 程式碼 Marketplace hello。</span><span class="sxs-lookup"><span data-stu-id="76048-121">Install `Visual Studio Code` and hello `C# extension` from hello Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="76048-122">檢視此[快速的視訊教學課程](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows)有關 tooget 如何開始使用`Visual Studio Code`和 hello `.NET Core SDK`。</span><span class="sxs-lookup"><span data-stu-id="76048-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how tooget started using `Visual Studio Code` and hello `.NET Core SDK`.</span></span>

## <a name="creating-hello-azure-iot-edge-converter-module"></a><span data-ttu-id="76048-123">建立 hello Azure IoT 邊緣轉換器模組</span><span class="sxs-lookup"><span data-stu-id="76048-123">Creating hello Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="76048-124">初始化新 `.NET Core` 類別庫 C# 專案：</span><span class="sxs-lookup"><span data-stu-id="76048-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="76048-125">開啟命令提示字元 (`Windows + R` -> `cmd` -> `enter`)。</span><span class="sxs-lookup"><span data-stu-id="76048-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="76048-126">瀏覽您要 toocreate hello toohello 資料夾`C#`專案。</span><span class="sxs-lookup"><span data-stu-id="76048-126">Navigate toohello folder where you'd like toocreate hello `C#` project.</span></span>
    - <span data-ttu-id="76048-127">輸入 **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**。</span><span class="sxs-lookup"><span data-stu-id="76048-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="76048-128">此命令會在專案目錄中建立名為 `Class1.cs` 的空類別。</span><span class="sxs-lookup"><span data-stu-id="76048-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="76048-129">瀏覽 toohello 我們剛建立的資料夾 hello 類別庫專案輸入**cd IoTEdgeConverterModule**。</span><span class="sxs-lookup"><span data-stu-id="76048-129">Navigate toohello folder where we just created hello class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="76048-130">在開啟 hello 專案`Visual Studio Code`輸入**程式碼。**。</span><span class="sxs-lookup"><span data-stu-id="76048-130">Open hello project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="76048-131">一旦 hello 專案以`Visual Studio Code`，按一下 hello **IoTEdgeConverterModule.csproj** tooopen hello 檔案 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="76048-131">Once hello project is opened in `Visual Studio Code`, click on hello **IoTEdgeConverterModule.csproj** tooopen hello file as shown in hello following image:</span></span>

    ![Visual Studio Code 編輯視窗](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="76048-133">插入 hello `XML` hello 之間 hello 關閉下列程式碼片段所示的 blob`PropertyGroup`標記並 hello 關閉`Project`標記; 行六個 in hello 前面映像並按下儲存 hello 檔案`Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="76048-133">Insert hello `XML` blob shown in hello following code snippet between hello closing `PropertyGroup` tag and hello closing `Project` tag; line six in hello preceding image and save hello file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="76048-134">一旦您儲存 hello`.csproj`檔案，`Visual Studio Code`應該會提示您使用`unresolved dependencies`對話方塊 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="76048-134">Once you save hello `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in hello following image:</span></span> 

    ![Visual Studio Code 還原相依性對話方塊](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="76048-136">a） 按一下`Restore`toorestore hello 專案中的 hello 所有參考`.csproj`檔案包括 hello`PackageReferences`我們新增了。</span><span class="sxs-lookup"><span data-stu-id="76048-136">a) Click `Restore` toorestore all of hello references in hello projects `.csproj` file including hello `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="76048-137">b)`Visual Studio Code`會自動建立 hello`project.assets.json`專案中的檔案`obj`資料夾。</span><span class="sxs-lookup"><span data-stu-id="76048-137">b) `Visual Studio Code` automatically creates hello `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="76048-138">此檔案包含您的專案相依性 toomake 後續還原更快的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="76048-138">This file contains information about your project's dependencies toomake subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="76048-139">`.NET Core Tools` 現在以 MSBuild 為基礎。</span><span class="sxs-lookup"><span data-stu-id="76048-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="76048-140">這表示會建立 `.csproj` 專案檔案而非 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="76048-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="76048-141">如果 `Visual Studio Code` 沒有提示您也沒有關係，我們可以手動執行此動作。</span><span class="sxs-lookup"><span data-stu-id="76048-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="76048-142">開啟 hello`Visual Studio Code`整合終端機視窗按 hello `Ctrl`  +  `backtick`鍵，或使用 hello 功能表`View`  ->  `Integrated Terminal`。</span><span class="sxs-lookup"><span data-stu-id="76048-142">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="76048-143">在 hello`Integrated Terminal`視窗類型**dotnet 還原**。</span><span class="sxs-lookup"><span data-stu-id="76048-143">In hello `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="76048-144">重新命名 hello`Class1.cs`檔案太`BleConverterModule.cs`。</span><span class="sxs-lookup"><span data-stu-id="76048-144">Rename hello `Class1.cs` file too`BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="76048-145">a) toorename hello 檔案先 hello 檔案上按一下，然後按下 hello`F2`索引鍵。</span><span class="sxs-lookup"><span data-stu-id="76048-145">a) toorename hello file first click on hello file then press hello `F2` key.</span></span>
    
    <span data-ttu-id="76048-146">b） 在 hello 新名稱的型別**BleConverterModule**、 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="76048-146">b) Type in hello new name **BleConverterModule**, as seen in hello following image:</span></span>

    ![重新命名類別的 Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="76048-148">Hello hello 中的現有程式碼取代`BleConverterModule.cs`檔案複製並貼上下列程式碼片段至的 hello 您`BleConverterModule.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="76048-148">Replace hello existing code in hello `BleConverterModule.cs` file by copying and pasting hello following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="76048-149">按下儲存 hello 檔案`Ctrl`  +  `S`。</span><span class="sxs-lookup"><span data-stu-id="76048-149">Save hello file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="76048-150">建立新的檔案稱為`Untitled-1`所按的 hello `Ctrl`  +  `N`金鑰 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="76048-150">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys as seen in hello following image:</span></span>

    ![Visual Studio Code 新檔案](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="76048-152">toodeserialize hello`JSON`物件，我們收到 hello 模擬`BLE`裝置、 hello 成下列程式碼複製 hello`Untitled-1`檔案的程式碼編輯器 視窗。</span><span class="sxs-lookup"><span data-stu-id="76048-152">toodeserialize hello `JSON` object that we receive from hello simulated `BLE` device, copy hello following code into hello `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="76048-153">將 hello 檔案儲存為`BleData.cs`按`Ctrl`  +  `Shift`  +  `S`索引鍵。</span><span class="sxs-lookup"><span data-stu-id="76048-153">Save hello file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="76048-154">Hello 上將儲存為對話方塊中，在 hello`Save as Type`下拉式功能表中，選取`C# (*.cs;*.csx)`hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="76048-154">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in hello following image:</span></span>

    ![Visual Studio Code 另存新檔對話方塊](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="76048-156">建立新的檔案稱為`Untitled-1`所按的 hello `Ctrl`  +  `N`索引鍵。</span><span class="sxs-lookup"><span data-stu-id="76048-156">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="76048-157">複製並貼上下列程式碼片段至 hello hello`Untitled-1`檔案。</span><span class="sxs-lookup"><span data-stu-id="76048-157">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> <span data-ttu-id="76048-158">這個類別是`Azure IoT Edge`模組，我們會使用來自 toooutput hello 資料我們`BleConverterModule`。</span><span class="sxs-lookup"><span data-stu-id="76048-158">This class is a `Azure IoT Edge` module, which we use toooutput hello data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="76048-159">將 hello 檔案儲存為`DotNetPrinterModule.cs`按`Ctrl`  +  `Shift`  +  `S`。</span><span class="sxs-lookup"><span data-stu-id="76048-159">Save hello file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="76048-160">Hello 上將儲存為對話方塊中，在 hello`Save as Type`下拉式功能表中，選取`C# (*.cs;*.csx)`。</span><span class="sxs-lookup"><span data-stu-id="76048-160">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="76048-161">建立新的檔案稱為`Untitled-1`所按的 hello `Ctrl`  +  `N`索引鍵。</span><span class="sxs-lookup"><span data-stu-id="76048-161">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="76048-162">toodeserialize hello`JSON`物件，我們收到 hello `BleConverterModule`，複製和貼上 hello 下列程式碼片段至 hello`Untitled-1`檔案。</span><span class="sxs-lookup"><span data-stu-id="76048-162">toodeserialize hello `JSON` object that we receive from hello `BleConverterModule`, Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="76048-163">將 hello 檔案儲存為`BleConverterData.cs`按`Ctrl`  +  `Shift`  +  `S`。</span><span class="sxs-lookup"><span data-stu-id="76048-163">Save hello file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="76048-164">Hello 上將儲存為對話方塊中，在 hello`Save as Type`下拉式功能表中，選取`C# (*.cs;*.csx)`。</span><span class="sxs-lookup"><span data-stu-id="76048-164">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="76048-165">建立新的檔案稱為`Untitled-1`所按的 hello `Ctrl`  +  `N`索引鍵。</span><span class="sxs-lookup"><span data-stu-id="76048-165">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="76048-166">複製並貼上下列程式碼片段至 hello hello`Untitled-1`檔案。</span><span class="sxs-lookup"><span data-stu-id="76048-166">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="76048-167">將 hello 檔案儲存為`gw-config.json`按`Ctrl`  +  `Shift`  +  `S`。</span><span class="sxs-lookup"><span data-stu-id="76048-167">Save hello file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="76048-168">Hello 上將儲存為對話方塊中，在 hello`Save as Type`下拉式功能表中，選取`JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`。</span><span class="sxs-lookup"><span data-stu-id="76048-168">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="76048-169">tooenable 複製 hello 設定檔 toohello 的輸出目錄中，更新 hello`IoTEdgeConverterModule.csproj`以下列 XML blob 的 hello:</span><span class="sxs-lookup"><span data-stu-id="76048-169">tooenable copying of hello configuration file toohello output directory, update hello `IoTEdgeConverterModule.csproj` with hello following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="76048-170">更新的 hello`IoTEdgeConverterModule.csproj`應該看起來像 hello 下列映像：</span><span class="sxs-lookup"><span data-stu-id="76048-170">hello updated `IoTEdgeConverterModule.csproj` should look like hello following image:</span></span>

    ![Visual Studio Code 更新後的 .csproj 檔案](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="76048-172">建立新的檔案稱為`Untitled-1`所按的 hello `Ctrl`  +  `N`索引鍵。</span><span class="sxs-lookup"><span data-stu-id="76048-172">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="76048-173">複製並貼上下列程式碼片段至 hello hello`Untitled-1`檔案。</span><span class="sxs-lookup"><span data-stu-id="76048-173">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="76048-174">將 hello 檔案儲存為`binplace.ps1`按`Ctrl`  +  `Shift`  +  `S`。</span><span class="sxs-lookup"><span data-stu-id="76048-174">Save hello file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="76048-175">Hello 上將儲存為對話方塊中，在 hello`Save as Type`下拉式功能表中，選取`PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`。</span><span class="sxs-lookup"><span data-stu-id="76048-175">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="76048-176">按下 hello 建置 hello 專案`Ctrl`  +  `Shift`  +  `B`索引鍵。</span><span class="sxs-lookup"><span data-stu-id="76048-176">Build hello project by pressing hello `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="76048-177">當您第一次建置 hello 的 hello 專案`Visual Studio Code`會提示您以 hello`No build task defined.`對話方塊 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="76048-177">When you build hello project for hello first time, `Visual Studio Code` prompts you with hello `No build task defined.` dialog as seen in hello following image:</span></span>

    ![Visual Studio Code 建置工作對話方塊](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="76048-179">a） 按一下 hello `Configure Build Task`  按鈕。</span><span class="sxs-lookup"><span data-stu-id="76048-179">a) Click hello `Configure Build Task` button.</span></span>

    <span data-ttu-id="76048-180">b） 在 hello`Select a Task Runner`對話方塊下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="76048-180">b) In hello `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="76048-181">選取`.NET Core`hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="76048-181">Select `.NET Core` as seen in hello following image:</span></span> 

    ![Visual Studio Code 選取工作對話方塊](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="76048-183">c） 按一下 hello`.NET Core`項目建立 hello`tasks.json`檔案中您`.vscode`目錄，並開啟 hello 檔案在 hello`code editor`視窗。</span><span class="sxs-lookup"><span data-stu-id="76048-183">c) Clicking hello `.NET Core` item creates hello `tasks.json` file in your `.vscode` directory and opens hello file in hello `code editor` window.</span></span> <span data-ttu-id="76048-184">沒有任何需要 toomodify 此檔案，請關閉 hello 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="76048-184">There is no need toomodify this file, close hello tab.</span></span>

27.  <span data-ttu-id="76048-185">開啟 hello`Visual Studio Code`整合終端機視窗按 hello `Ctrl`  +  `backtick`鍵，或使用 hello 功能表`View`  ->  `Integrated Terminal`和型別**.\binplace.ps1**到 hello`PowerShell`命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="76048-185">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into hello `PowerShell` command prompt.</span></span> <span data-ttu-id="76048-186">此命令會複製所有我們相依性 toohello 輸出目錄。</span><span class="sxs-lookup"><span data-stu-id="76048-186">This command copies all our dependencies toohello output directory.</span></span>

28. <span data-ttu-id="76048-187">瀏覽 toohello 專案輸出目錄中 hello`Integrated Terminal`視窗輸入**cd.\bin\Debug\netstandard1.3**。</span><span class="sxs-lookup"><span data-stu-id="76048-187">Navigate toohello projects output directory in hello `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="76048-188">輸入執行 hello 範例專案**。 \gw.exe gw config.json**到 hello`Integrated Terminal`視窗提示。</span><span class="sxs-lookup"><span data-stu-id="76048-188">Run hello sample project by typing **.\gw.exe gw-config.json** into hello `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="76048-189">如果您有密切遵循 hello 步驟在本教學課程，您應該立即執行 hello `Azure IoT Edge BLE Data Converter Module` hello 下列影像所示的範例專案：</span><span class="sxs-lookup"><span data-stu-id="76048-189">If you have followed hello steps in this tutorial closely, you should now be running hello `Azure IoT Edge BLE Data Converter Module` sample project as seen in hello following image:</span></span>
    
        ![在 Visual Studio Code 中執行的模擬裝置範例](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="76048-191">如果您想 tooterminate hello 應用程式，請按 hello`<Enter>`索引鍵。</span><span class="sxs-lookup"><span data-stu-id="76048-191">If you want tooterminate hello application, press hello `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="76048-192">建議您不要 toouse `Ctrl`  +  `C` tooterminate hello`IoT Edge`閘道應用程式 (也就是**gw.exe**)。</span><span class="sxs-lookup"><span data-stu-id="76048-192">It is not recommended toouse `Ctrl` + `C` tooterminate hello `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="76048-193">為此動作可能導致 hello 程序 tooterminate 異常。</span><span class="sxs-lookup"><span data-stu-id="76048-193">As this action may cause hello process tooterminate abnormally.</span></span>

