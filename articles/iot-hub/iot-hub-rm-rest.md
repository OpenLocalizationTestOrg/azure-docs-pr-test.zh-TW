---
title: "Azure IoT 中樞使用的 aaaCreate hello 資源提供者 REST API |Microsoft 文件"
description: "如何 toouse hello 資源提供者 REST API toocreate IoT 中樞。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a>建立 IoT 中心使用 hello 資源提供者 REST API (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

您可以使用 hello [IoT 中樞資源提供者 REST API] [ lnk-rest-api] toocreate 並以程式設計方式管理 Azure IoT 中樞。 本教學課程會示範如何 toouse 會 hello IoT 中樞資源提供者 REST API toocreate C# 程式從 IoT 中樞。

> [!NOTE]
> Azure 有兩種不同的部署模型可建立和處理資源：[Azure Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。  本文件涵蓋使用 hello Azure Resource Manager 部署模型。

toocomplete 本教學課程中，您需要遵循的 hello:

* Visual Studio 2015 或 Visual Studio 2017。
* 使用中的 Azure 帳戶。 <br/>如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* [Azure PowerShell 1.0][lnk-powershell-install] 或更新版本。

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>準備 Visual Studio 專案

1. 在 Visual Studio 中，建立 Visual C# Windows 傳統桌面專案使用 hello**主控台應用程式 (.NET Framework)**專案範本。 名稱 hello 專案**CreateIoTHubREST**。

2. 在方案總管中，於專案上按一下滑鼠右鍵，然後按一下管理 NuGet 封裝 。

3. 在 [NuGet 封裝管理員] 中，檢查**包含發行前版本**，在 hello**瀏覽**頁面搜尋**Microsoft.Azure.Management.ResourceManager**。 選取 hello 封裝，按一下**安裝**，請在**檢閱變更**按一下**確定**，然後按一下 **我接受**tooaccept hello 授權。

4. 在 NuGet 套件管理員中，搜尋 **Microsoft.IdentityModel.Clients.ActiveDirectory**。  按一下**安裝**，請在**檢閱變更**按一下**確定**，然後按一下 **我接受**tooaccept hello 授權。

5. 在 Program.cs 中，取代現有的 hello**使用**陳述式，以下列程式碼的 hello:

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. 在 Program.cs 中，加入下列取代 hello 預留位置值的靜態變數的 hello。 您先前已在本教學課程中記下 **ApplicationId**、**SubscriptionId**、**TenantId** 及 **Password**。 **資源群組名稱**hello hello 建立 hello IoT 中樞時所使用的資源群組名稱。 您可以使用預先存在或新的資源群組。 **IoT 中樞名稱**hello hello 您建立時，例如 IoT 中樞名稱**MyIoTHub**。 IoT 中樞 hello 名稱必須是全域唯一的。 **部署名稱**是 hello 部署的名稱，例如**Deployment_01**。

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a>使用 hello 資源提供者 REST API toocreate IoT 中樞

使用 hello [IoT 中樞資源提供者 REST API] [ lnk-rest-api] toocreate IoT 中樞資源群組中。 您也可以使用 hello 資源提供者 REST API toomake 變更 tooan 現有 IoT 中樞。

1. 加入下列方法 tooProgram.cs hello:

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. 新增下列程式碼 toohello hello **CreateIoTHub**方法。 此程式碼建立**HttpClient**與 hello 標頭中的 hello 驗證權杖的物件：

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. 新增下列程式碼 toohello hello **CreateIoTHub**方法。 此程式碼說明 hello IoT 中樞 toocreate，並產生的 JSON 表示法。 如 hello 目前的位置，其支援 IoT 中樞的清單，請參閱[Azure 狀態][lnk-status]:

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. 新增下列程式碼 toohello hello **CreateIoTHub**方法。 此程式碼會送出 hello REST 要求 tooAzure。 hello 程式碼會檢查 hello 回應，然後擷取 hello URL，您可以使用 toomonitor hello hello 部署工作狀態：

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. 新增下列程式碼 toohello 結尾 hello hello **CreateIoTHub**方法。 此程式碼使用 hello **asyncStatusUri**位址擷取中的 hello 部署 toocomplete hello 上一個步驟 toowait:

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. 新增下列程式碼 toohello 結尾 hello hello **CreateIoTHub**方法。 此程式碼會擷取 hello IoT 中樞，您建立並列印 toohello 主控台 hello 索引鍵：

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a>完成並執行 hello 應用程式

您現在可以完成 hello 應用程式呼叫 hello **CreateIoTHub**方法再進行建置和執行它。

1. 新增下列程式碼 toohello 結尾 hello hello **Main**方法：

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. 按一下 [建置]，然後按一下 [建置方案]。 更正所有錯誤。

3. 按一下**偵錯**然後**開始偵錯**toorun hello 應用程式。 可能需要幾分鐘的時間 hello 部署 toorun。

4. 加入您的應用程式的 tooverify hello IoT 中樞，請瀏覽 hello [Azure 入口網站][ lnk-azure-portal]並檢視您資源的清單。 或者，使用 hello **Get AzureRmResource** PowerShell cmdlet。

> [!NOTE]
> 此範例應用程式會加入您付費的「S1 標準 IoT 中樞」。 當您完成時，您可以刪除透過 hello hello IoT 中樞[Azure 入口網站][ lnk-azure-portal]或使用 hello**移除 AzureRmResource** PowerShell 指令程式完成時。

## <a name="next-steps"></a>後續步驟
現在您已經部署使用 hello 資源提供者 REST API IoT 中樞，您可以進一步 tooexplore:

* 閱讀有關 hello hello 功能[IoT 中樞資源提供者 REST API][lnk-rest-api]。
* 讀取[Azure 資源管理員概觀][ lnk-azure-rm-overview] toolearn 更多關於 hello 功能的 Azure 資源管理員。

進一步了解開發的 IoT 中樞 toolearn，請參閱下列文章的 hello:

* [簡介 tooC SDK][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
