---
title: "使用 C# 建立 Azure IoT Edge 模組 | Microsoft Docs"
description: "本教學課程示範如何使用最新的 Azure IoT Edge NuGet 套件、Visual Studio Code 與 C# 撰寫 BLE 資料轉換器模組。"
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
ms.openlocfilehash: 7175ffc8de2c043593d61143b402484d33e4a8cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="ab35e-104">使用 C&#x23; 建立 Azure IoT Edge 模組</span><span class="sxs-lookup"><span data-stu-id="ab35e-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="ab35e-105">本教學課程示範如何使用 `Visual Studio Code` 和 `C#` 建立 `Azure IoT Edge` 的模組。</span><span class="sxs-lookup"><span data-stu-id="ab35e-105">This tutorial showcases how to create a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="ab35e-106">在本教學課程中，我們將逐步說明環境設定，以及如何使用最新的 `Azure IoT Edge NuGet` 套件撰寫 [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 資料轉換器模組。</span><span class="sxs-lookup"><span data-stu-id="ab35e-106">In this tutorial, we walk through environment set-up and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="ab35e-107">本教學課程使用支援跨平台相容性的 `.NET Core SDK`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-107">This tutorial is using the `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="ab35e-108">下列教學課程使用 `Windows 10` 作業系統撰寫。</span><span class="sxs-lookup"><span data-stu-id="ab35e-108">The following tutorial is written using the `Windows 10` operating system.</span></span> <span data-ttu-id="ab35e-109">此教學課程中的某些命令可能因您的 `development environment` 而不同。</span><span class="sxs-lookup"><span data-stu-id="ab35e-109">Some of the commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ab35e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ab35e-110">Prerequisites</span></span>

<span data-ttu-id="ab35e-111">在本節中，我們會針對 `Azure IoT Edge` 模組開發設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="ab35e-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="ab35e-112">它同時適用於 **64 位元 Windows** 和 **64 位元 Linux (Ubuntu/Debian 8)** 作業系統。</span><span class="sxs-lookup"><span data-stu-id="ab35e-112">It applies to both **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="ab35e-113">需要下列軟體：</span><span class="sxs-lookup"><span data-stu-id="ab35e-113">The following software is required:</span></span>

- [<span data-ttu-id="ab35e-114">Git 用戶端</span><span class="sxs-lookup"><span data-stu-id="ab35e-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="ab35e-115">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="ab35e-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="ab35e-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ab35e-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="ab35e-117">您不需要針對此範例複製存放庫，但是在本教學課程中討論的所有範例程式碼都位於下列存放庫中：</span><span class="sxs-lookup"><span data-stu-id="ab35e-117">You do not need to clone the repo for this sample, however all of the sample code discussed in this tutorial is located in the following repository:</span></span>

- <span data-ttu-id="ab35e-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="ab35e-119">開始使用</span><span class="sxs-lookup"><span data-stu-id="ab35e-119">Getting started</span></span>

1. <span data-ttu-id="ab35e-120">安裝 `.NET Core SDK`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="ab35e-121">從 Visual Studio Code Marketplace 安裝 `Visual Studio Code` 和 `C# extension`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-121">Install `Visual Studio Code` and the `C# extension` from the Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="ab35e-122">有關如何開始使用 `Visual Studio Code` 和 `.NET Core SDK`，請檢視此[快速影片教學課程](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows)。</span><span class="sxs-lookup"><span data-stu-id="ab35e-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how to get started using `Visual Studio Code` and the `.NET Core SDK`.</span></span>

## <a name="creating-the-azure-iot-edge-converter-module"></a><span data-ttu-id="ab35e-123">建立 Azure IoT Edge 轉換器模組</span><span class="sxs-lookup"><span data-stu-id="ab35e-123">Creating the Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="ab35e-124">初始化新 `.NET Core` 類別庫 C# 專案：</span><span class="sxs-lookup"><span data-stu-id="ab35e-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="ab35e-125">開啟命令提示字元 (`Windows + R` -> `cmd` -> `enter`)。</span><span class="sxs-lookup"><span data-stu-id="ab35e-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="ab35e-126">瀏覽到您想要建立 `C#` 專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ab35e-126">Navigate to the folder where you'd like to create the `C#` project.</span></span>
    - <span data-ttu-id="ab35e-127">輸入 **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**。</span><span class="sxs-lookup"><span data-stu-id="ab35e-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="ab35e-128">此命令會在專案目錄中建立名為 `Class1.cs` 的空類別。</span><span class="sxs-lookup"><span data-stu-id="ab35e-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="ab35e-129">輸入 **cd IoTEdgeConverterModule**，瀏覽到我們剛剛建立類別庫專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ab35e-129">Navigate to the folder where we just created the class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="ab35e-130">在 `Visual Studio Code` 中輸入 **code .**，開啟專案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-130">Open the project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="ab35e-131">在 `Visual Studio Code` 中開啟專案後，按一下 **IoTEdgeConverterModule.csproj** 便可如下圖所示開啟檔案：</span><span class="sxs-lookup"><span data-stu-id="ab35e-131">Once the project is opened in `Visual Studio Code`, click on the **IoTEdgeConverterModule.csproj** to open the file as shown in the following image:</span></span>

    ![Visual Studio Code 編輯視窗](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="ab35e-133">在上圖的第六行中，於結尾 `PropertyGroup` 標記和結尾 `Project` 標記之間插入下列程式碼片段所顯示的 `XML` Blob，然後按 `Ctrl` + `S` 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-133">Insert the `XML` blob shown in the following code snippet between the closing `PropertyGroup` tag and the closing `Project` tag; line six in the preceding image and save the file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="ab35e-134">儲存 `.csproj` 檔案之後，`Visual Studio Code` 應會以 `unresolved dependencies` 對話方塊提示您，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ab35e-134">Once you save the `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in the following image:</span></span> 

    ![Visual Studio Code 還原相依性對話方塊](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="ab35e-136">a) 按一下 `Restore` 可還原專案 `.csproj` 檔案中的所有相依性，包括我們已新增的 `PackageReferences`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-136">a) Click `Restore` to restore all of the references in the projects `.csproj` file including the `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="ab35e-137">b) `Visual Studio Code` 會自動在專案 `obj` 資料夾中建立 `project.assets.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-137">b) `Visual Studio Code` automatically creates the `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="ab35e-138">此檔案包含您專案相依性的相關資訊，可使後續還原速度更快。</span><span class="sxs-lookup"><span data-stu-id="ab35e-138">This file contains information about your project's dependencies to make subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="ab35e-139">`.NET Core Tools` 現在以 MSBuild 為基礎。</span><span class="sxs-lookup"><span data-stu-id="ab35e-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="ab35e-140">這表示會建立 `.csproj` 專案檔案而非 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="ab35e-141">如果 `Visual Studio Code` 沒有提示您也沒有關係，我們可以手動執行此動作。</span><span class="sxs-lookup"><span data-stu-id="ab35e-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="ab35e-142">按下 `Ctrl` + `backtick` 鍵或使用功能表 `View` -> `Integrated Terminal`，開啟 `Visual Studio Code` 整合式終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="ab35e-142">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="ab35e-143">在 `Integrated Terminal` 視窗中輸入 **dotnet restore**。</span><span class="sxs-lookup"><span data-stu-id="ab35e-143">In the `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="ab35e-144">將 `Class1.cs` 檔案重新命名為 `BleConverterModule.cs`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-144">Rename the `Class1.cs` file to `BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="ab35e-145">a) 若要重新命名檔案，請先按一下檔案，然後按 `F2` 鍵。</span><span class="sxs-lookup"><span data-stu-id="ab35e-145">a) To rename the file first click on the file then press the `F2` key.</span></span>
    
    <span data-ttu-id="ab35e-146">b) 輸入新名稱 **BleConverterModule**，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ab35e-146">b) Type in the new name **BleConverterModule**, as seen in the following image:</span></span>

    ![重新命名類別的 Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="ab35e-148">將下列程式碼片段複製並貼上到 `BleConverterModule.cs` 檔案中，取代 `BleConverterModule.cs` 檔案中的現有程式碼。</span><span class="sxs-lookup"><span data-stu-id="ab35e-148">Replace the existing code in the `BleConverterModule.cs` file by copying and pasting the following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="ab35e-149">按 `Ctrl` + `S` 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-149">Save the file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="ab35e-150">按 `Ctrl` + `N` 鍵建立名為 `Untitled-1` 的新檔案，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ab35e-150">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys as seen in the following image:</span></span>

    ![Visual Studio Code 新檔案](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="ab35e-152">若要還原序列化我們從模擬的 `BLE` 裝置收到的 `JSON` 物件，請將下列程式碼複製到 `Untitled-1` 檔案程式碼編輯器視窗。</span><span class="sxs-lookup"><span data-stu-id="ab35e-152">To deserialize the `JSON` object that we receive from the simulated `BLE` device, copy the following code into the `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="ab35e-153">按 `Ctrl` + `Shift` + `S` 鍵將檔案儲存為 `BleData.cs`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-153">Save the file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="ab35e-154">在另存新檔對話方塊的 `Save as Type` 下拉式功能表中，選取 `C# (*.cs;*.csx)`，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ab35e-154">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in the following image:</span></span>

    ![Visual Studio Code 另存新檔對話方塊](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="ab35e-156">按 `Ctrl` + `N` 鍵建立名為 `Untitled-1` 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-156">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="ab35e-157">將以下程式碼片段複製並貼上到 `Untitled-1` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ab35e-157">Copy and paste the following code snippet into the `Untitled-1` file.</span></span> <span data-ttu-id="ab35e-158">這個類別是 `Azure IoT Edge` 模組，我們會使用它來輸出從 `BleConverterModule` 接收的資料。</span><span class="sxs-lookup"><span data-stu-id="ab35e-158">This class is a `Azure IoT Edge` module, which we use to output the data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="ab35e-159">按 `Ctrl` + `Shift` + `S` 將檔案另存為 `DotNetPrinterModule.cs`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-159">Save the file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="ab35e-160">在另存新檔對話方塊的 `Save as Type` 下拉式功能表中，選取 `C# (*.cs;*.csx)`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-160">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="ab35e-161">按 `Ctrl` + `N` 鍵建立名為 `Untitled-1` 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-161">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="ab35e-162">若要還原序列化我們從 `BleConverterModule` 收到的 `JSON` 物件，請將以下程式碼片段複製並貼上到 `Untitled-1` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ab35e-162">To deserialize the `JSON` object that we receive from the `BleConverterModule`, Copy and paste the following code snippet into the `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="ab35e-163">按 `Ctrl` + `Shift` + `S` 將檔案另存為 `BleConverterData.cs`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-163">Save the file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="ab35e-164">在另存新檔對話方塊的 `Save as Type` 下拉式功能表中，選取 `C# (*.cs;*.csx)`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-164">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="ab35e-165">按 `Ctrl` + `N` 鍵建立名為 `Untitled-1` 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-165">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="ab35e-166">將以下程式碼片段複製並貼上到 `Untitled-1` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ab35e-166">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="ab35e-167">按 `Ctrl` + `Shift` + `S` 將檔案另存為 `gw-config.json`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-167">Save the file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="ab35e-168">在另存新檔對話方塊的 `Save as Type` 下拉式功能表中，選取 `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-168">On the save as dialog box, in the `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="ab35e-169">若要啟用將組態檔複製到輸出目錄，請將 `IoTEdgeConverterModule.csproj` 更新為下列 XML blob：</span><span class="sxs-lookup"><span data-stu-id="ab35e-169">To enable copying of the configuration file to the output directory, update the `IoTEdgeConverterModule.csproj` with the following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="ab35e-170">更新後的 `IoTEdgeConverterModule.csproj` 看起來應該如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ab35e-170">The updated `IoTEdgeConverterModule.csproj` should look like the following image:</span></span>

    ![Visual Studio Code 更新後的 .csproj 檔案](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="ab35e-172">按 `Ctrl` + `N` 鍵建立名為 `Untitled-1` 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-172">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="ab35e-173">將以下程式碼片段複製並貼上到 `Untitled-1` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ab35e-173">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="ab35e-174">按 `Ctrl` + `Shift` + `S` 將檔案另存為 `binplace.ps1`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-174">Save the file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="ab35e-175">在另存新檔對話方塊的 `Save as Type` 下拉式功能表中，選取 `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`。</span><span class="sxs-lookup"><span data-stu-id="ab35e-175">On the save as dialog box, in the `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="ab35e-176">按 `Ctrl` + `Shift` + `B` 鍵建置專案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-176">Build the project by pressing the `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="ab35e-177">當您第一次建置專案時，`Visual Studio Code` 會以 `No build task defined.` 對話方塊提示您，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ab35e-177">When you build the project for the first time, `Visual Studio Code` prompts you with the `No build task defined.` dialog as seen in the following image:</span></span>

    ![Visual Studio Code 建置工作對話方塊](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="ab35e-179">a) 按一下 `Configure Build Task` 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ab35e-179">a) Click the `Configure Build Task` button.</span></span>

    <span data-ttu-id="ab35e-180">b) 在 `Select a Task Runner` 對話方塊下拉式功能表中。</span><span class="sxs-lookup"><span data-stu-id="ab35e-180">b) In the `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="ab35e-181">選取 `.NET Core`，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ab35e-181">Select `.NET Core` as seen in the following image:</span></span> 

    ![Visual Studio Code 選取工作對話方塊](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="ab35e-183">c) 按一下 `.NET Core` 項目可在 `.vscode` 目錄中建立 `tasks.json` 檔案，並在 `code editor` 視窗中開啟該檔案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-183">c) Clicking the `.NET Core` item creates the `tasks.json` file in your `.vscode` directory and opens the file in the `code editor` window.</span></span> <span data-ttu-id="ab35e-184">這個檔案不需修改，請關閉索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ab35e-184">There is no need to modify this file, close the tab.</span></span>

27.  <span data-ttu-id="ab35e-185">按 `Ctrl` + `backtick` 鍵或使用功能表 `View` -> `Integrated Terminal` 開啟 `Visual Studio Code` 整合式終端機視窗，並將 **.\binplace.ps1** 輸入到 `PowerShell` 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="ab35e-185">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into the `PowerShell` command prompt.</span></span> <span data-ttu-id="ab35e-186">此命令會將我們的所有相依性複製到輸出目錄。</span><span class="sxs-lookup"><span data-stu-id="ab35e-186">This command copies all our dependencies to the output directory.</span></span>

28. <span data-ttu-id="ab35e-187">輸入 **cd .\bin\Debug\netstandard1.3**，瀏覽到 `Integrated Terminal` 視窗中的專案輸出目錄。</span><span class="sxs-lookup"><span data-stu-id="ab35e-187">Navigate to the projects output directory in the `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="ab35e-188">將 **.\gw.exe gw-config.json** 輸入到 `Integrated Terminal` 視窗提示中，執行範例專案。</span><span class="sxs-lookup"><span data-stu-id="ab35e-188">Run the sample project by typing **.\gw.exe gw-config.json** into the `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="ab35e-189">如果您嚴格遵照本教學課程中的步驟執行，現在應正執行 `Azure IoT Edge BLE Data Converter Module` 範例專案，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ab35e-189">If you have followed the steps in this tutorial closely, you should now be running the `Azure IoT Edge BLE Data Converter Module` sample project as seen in the following image:</span></span>
    
        ![在 Visual Studio Code 中執行的模擬裝置範例](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="ab35e-191">如果您想要終止應用程式，請按 `<Enter>` 鍵。</span><span class="sxs-lookup"><span data-stu-id="ab35e-191">If you want to terminate the application, press the `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="ab35e-192">不建議使用 `Ctrl` + `C` 來終止 `IoT Edge` 閘道應用程式 (即 **gw.exe**)。</span><span class="sxs-lookup"><span data-stu-id="ab35e-192">It is not recommended to use `Ctrl` + `C` to terminate the `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="ab35e-193">因為此動作可能會造成程序異常終止。</span><span class="sxs-lookup"><span data-stu-id="ab35e-193">As this action may cause the process to terminate abnormally.</span></span>

