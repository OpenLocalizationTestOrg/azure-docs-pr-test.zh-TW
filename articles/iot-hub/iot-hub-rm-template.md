---
title: "aaaCreate Azure IoT 中樞使用的範本 (.NET) |Microsoft 文件"
description: "如何 toouse Azure Resource Manager 範本 toocreate IoT 中樞與 C# 程式。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a>使用 Azure Resource Manager 範本建立 IoT 中樞 (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

您可以使用 Azure Resource Manager toocreate，並以程式設計方式管理 Azure IoT 中樞。 本教學課程示範如何 toouse Azure Resource Manager 範本 toocreate C# 程式從 IoT 中樞。

> [!NOTE]
> Azure 有兩種不同的部署模型可建立和處理資源：[Azure Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。  本文件涵蓋使用 hello Azure Resource Manager 部署模型。

toocomplete 本教學課程中，您需要遵循的 hello:

* Visual Studio 2015 或 Visual Studio 2017。
* 使用中的 Azure 帳戶。 <br/>如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* 可供您儲存 Azure Resource Manager 範本檔案的 [Azure 儲存體帳戶][lnk-storage-account]。
* [Azure PowerShell 1.0][lnk-powershell-install] 或更新版本。

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>準備 Visual Studio 專案

1. 在 Visual Studio 中，建立 Visual C# Windows 傳統桌面專案使用 hello**主控台應用程式 (.NET Framework)**專案範本。 名稱 hello 專案**CreateIoTHub**。

2. 在方案總管中，於專案上按一下滑鼠右鍵，然後按一下管理 NuGet 封裝 。

3. 在 [NuGet 封裝管理員] 中，檢查**包含發行前版本**，在 hello**瀏覽**頁面搜尋**Microsoft.Azure.Management.ResourceManager**。 選取 hello 封裝，按一下**安裝**，請在**檢閱變更**按一下**確定**，然後按一下 **我接受**tooaccept hello 授權。

4. 在 NuGet 套件管理員中，搜尋 **Microsoft.IdentityModel.Clients.ActiveDirectory**。  按一下**安裝**，請在**檢閱變更**按一下**確定**，然後按一下 **我接受**tooaccept hello 授權。

5. 在 Program.cs 中，取代現有的 hello**使用**陳述式，以下列程式碼的 hello:

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. 在 Program.cs 中，加入下列取代 hello 預留位置值的靜態變數的 hello。 您先前已在本教學課程中記下 **ApplicationId**、**SubscriptionId**、**TenantId** 及 **Password**。 **您的 Azure 儲存體帳戶名稱**是 hello hello Azure 儲存體帳戶名稱，其中儲存您的 Azure 資源管理員範本檔案。 **資源群組名稱**hello hello 建立 hello IoT 中樞時所使用的資源群組名稱。 hello 名稱可以是現有或新資源群組。 **部署名稱**是 hello 部署的名稱，例如**Deployment_01**。

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-toocreate-an-iot-hub"></a>送出範本 toocreate IoT 中樞

使用資源群組中的 JSON 範本和參數檔案 toocreate IoT 中樞。 您也可以使用 Azure Resource Manager 範本 toomake 變更 tooan 現有 IoT 中樞。

1. 在 方案總管 中，於專案上按一下滑鼠右鍵，按一下 加入，然後按一下新增項目。 加入名為的 JSON 檔案**template.json** tooyour 專案。

2. 標準的 IoT 中樞 toohello tooadd**美國東部**區域中，取代 hello 內容**template.json**以 hello 下列資源定義。 針對 hello 目前支援 IoT 中樞的區域清單，請參閱[Azure 狀態][lnk-status]:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

3. 在 方案總管 中，於專案上按一下滑鼠右鍵，按一下 加入，然後按一下新增項目。 加入名為的 JSON 檔案**parameters.json** tooyour 專案。

4. 取代 hello 內容**parameters.json**以下列這類設定 hello 新的 IoT 中樞名稱的參數資訊的 hello **{縮寫} mynewiothub**。 hello IoT 中樞名稱必須是全域唯一的因此它應該包含您的名稱或縮寫：

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. 在**伺服器總管**、 連接 tooyour Azure 訂用帳戶，並在您的 Azure 儲存體帳戶會建立稱為容器**範本**。 在 hello**屬性**面板、 組 hello**公用讀取權限**hello 的權限**範本**容器太**Blob**。

6. 在**伺服器總管**，以滑鼠右鍵按一下 hello**範本**容器，然後按一下**檢視 Blob 容器**。 按一下 hello**上傳 Blob**按鈕、 選取 hello 兩個檔案， **parameters.json**和**templates.json**，然後按一下**開啟**tooupload hello JSON 檔案 toohello**範本**容器。 hello 的 hello blob 包含 hello JSON 資料的 Url 是：

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. 加入下列方法 tooProgram.cs hello:

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. 新增下列程式碼 toohello hello **CreateIoTHub**方法 toosubmit hello 範本和參數檔案 toohello Azure 資源管理員：

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. 新增下列程式碼 toohello hello **CreateIoTHub**顯示 hello 狀態和 hello hello 新的 IoT 中樞的方法：

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a>完成並執行 hello 應用程式

您現在可以完成 hello 應用程式呼叫 hello **CreateIoTHub**方法再進行建置和執行它。

1. 新增下列程式碼 toohello 結尾 hello hello **Main**方法：

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. 按一下 [建置]，然後按一下 [建置方案]。 更正所有錯誤。

3. 按一下**偵錯**然後**開始偵錯**toorun hello 應用程式。 可能需要幾分鐘的時間 hello 部署 toorun。

4. 您的應用程式加入的 tooverify hello IoT 中樞，請瀏覽 hello [Azure 入口網站][ lnk-azure-portal]並檢視您資源的清單。 或者，使用 hello **Get AzureRmResource** PowerShell cmdlet。

> [!NOTE]
> 此範例應用程式會加入您付費的「S1 標準 IoT 中樞」。 您可以刪除透過 hello hello IoT 中樞[Azure 入口網站][ lnk-azure-portal]或使用 hello**移除 AzureRmResource** PowerShell 指令程式完成時。

## <a name="next-steps"></a>後續步驟
現在您已經部署 IoT 中樞與 C# 程式使用 Azure Resource Manager 範本，您可以進一步 tooexplore:

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
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
