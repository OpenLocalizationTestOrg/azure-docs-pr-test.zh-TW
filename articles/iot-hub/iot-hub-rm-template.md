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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="1a50d-103">使用 Azure Resource Manager 範本建立 IoT 中樞 (.NET)</span><span class="sxs-lookup"><span data-stu-id="1a50d-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="1a50d-104">您可以使用 Azure Resource Manager toocreate，並以程式設計方式管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1a50d-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="1a50d-105">本教學課程示範如何 toouse Azure Resource Manager 範本 toocreate C# 程式從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1a50d-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="1a50d-106">Azure 有兩種不同的部署模型可建立和處理資源：[Azure Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1a50d-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="1a50d-107">本文件涵蓋使用 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="1a50d-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="1a50d-108">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="1a50d-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1a50d-109">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="1a50d-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="1a50d-110">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1a50d-110">An active Azure account.</span></span> <br/><span data-ttu-id="1a50d-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="1a50d-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="1a50d-112">可供您儲存 Azure Resource Manager 範本檔案的 [Azure 儲存體帳戶][lnk-storage-account]。</span><span class="sxs-lookup"><span data-stu-id="1a50d-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="1a50d-113">[Azure PowerShell 1.0][lnk-powershell-install] 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1a50d-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="1a50d-114">準備 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="1a50d-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="1a50d-115">在 Visual Studio 中，建立 Visual C# Windows 傳統桌面專案使用 hello**主控台應用程式 (.NET Framework)**專案範本。</span><span class="sxs-lookup"><span data-stu-id="1a50d-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="1a50d-116">名稱 hello 專案**CreateIoTHub**。</span><span class="sxs-lookup"><span data-stu-id="1a50d-116">Name hello project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="1a50d-117">在方案總管中，於專案上按一下滑鼠右鍵，然後按一下管理 NuGet 封裝 。</span><span class="sxs-lookup"><span data-stu-id="1a50d-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="1a50d-118">在 [NuGet 封裝管理員] 中，檢查**包含發行前版本**，在 hello**瀏覽**頁面搜尋**Microsoft.Azure.Management.ResourceManager**。</span><span class="sxs-lookup"><span data-stu-id="1a50d-118">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="1a50d-119">選取 hello 封裝，按一下**安裝**，請在**檢閱變更**按一下**確定**，然後按一下 **我接受**tooaccept hello 授權。</span><span class="sxs-lookup"><span data-stu-id="1a50d-119">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="1a50d-120">在 NuGet 套件管理員中，搜尋 **Microsoft.IdentityModel.Clients.ActiveDirectory**。</span><span class="sxs-lookup"><span data-stu-id="1a50d-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="1a50d-121">按一下**安裝**，請在**檢閱變更**按一下**確定**，然後按一下 **我接受**tooaccept hello 授權。</span><span class="sxs-lookup"><span data-stu-id="1a50d-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="1a50d-122">在 Program.cs 中，取代現有的 hello**使用**陳述式，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="1a50d-122">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="1a50d-123">在 Program.cs 中，加入下列取代 hello 預留位置值的靜態變數的 hello。</span><span class="sxs-lookup"><span data-stu-id="1a50d-123">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="1a50d-124">您先前已在本教學課程中記下 **ApplicationId**、**SubscriptionId**、**TenantId** 及 **Password**。</span><span class="sxs-lookup"><span data-stu-id="1a50d-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="1a50d-125">**您的 Azure 儲存體帳戶名稱**是 hello hello Azure 儲存體帳戶名稱，其中儲存您的 Azure 資源管理員範本檔案。</span><span class="sxs-lookup"><span data-stu-id="1a50d-125">**Your Azure Storage account name** is hello name of hello Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="1a50d-126">**資源群組名稱**hello hello 建立 hello IoT 中樞時所使用的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="1a50d-126">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="1a50d-127">hello 名稱可以是現有或新資源群組。</span><span class="sxs-lookup"><span data-stu-id="1a50d-127">hello name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="1a50d-128">**部署名稱**是 hello 部署的名稱，例如**Deployment_01**。</span><span class="sxs-lookup"><span data-stu-id="1a50d-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="1a50d-129">送出範本 toocreate IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="1a50d-129">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="1a50d-130">使用資源群組中的 JSON 範本和參數檔案 toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1a50d-130">Use a JSON template and parameter file toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="1a50d-131">您也可以使用 Azure Resource Manager 範本 toomake 變更 tooan 現有 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1a50d-131">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="1a50d-132">在 方案總管 中，於專案上按一下滑鼠右鍵，按一下 加入，然後按一下新增項目。</span><span class="sxs-lookup"><span data-stu-id="1a50d-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="1a50d-133">加入名為的 JSON 檔案**template.json** tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="1a50d-133">Add a JSON file called **template.json** tooyour project.</span></span>

2. <span data-ttu-id="1a50d-134">標準的 IoT 中樞 toohello tooadd**美國東部**區域中，取代 hello 內容**template.json**以 hello 下列資源定義。</span><span class="sxs-lookup"><span data-stu-id="1a50d-134">tooadd a standard IoT hub toohello **East US** region, replace hello contents of **template.json** with hello following resource definition.</span></span> <span data-ttu-id="1a50d-135">針對 hello 目前支援 IoT 中樞的區域清單，請參閱[Azure 狀態][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="1a50d-135">For hello current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="1a50d-136">在 方案總管 中，於專案上按一下滑鼠右鍵，按一下 加入，然後按一下新增項目。</span><span class="sxs-lookup"><span data-stu-id="1a50d-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="1a50d-137">加入名為的 JSON 檔案**parameters.json** tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="1a50d-137">Add a JSON file called **parameters.json** tooyour project.</span></span>

4. <span data-ttu-id="1a50d-138">取代 hello 內容**parameters.json**以下列這類設定 hello 新的 IoT 中樞名稱的參數資訊的 hello **{縮寫} mynewiothub**。</span><span class="sxs-lookup"><span data-stu-id="1a50d-138">Replace hello contents of **parameters.json** with hello following parameter information that sets a name for hello new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="1a50d-139">hello IoT 中樞名稱必須是全域唯一的因此它應該包含您的名稱或縮寫：</span><span class="sxs-lookup"><span data-stu-id="1a50d-139">hello IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="1a50d-140">在**伺服器總管**、 連接 tooyour Azure 訂用帳戶，並在您的 Azure 儲存體帳戶會建立稱為容器**範本**。</span><span class="sxs-lookup"><span data-stu-id="1a50d-140">In **Server Explorer**, connect tooyour Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="1a50d-141">在 hello**屬性**面板、 組 hello**公用讀取權限**hello 的權限**範本**容器太**Blob**。</span><span class="sxs-lookup"><span data-stu-id="1a50d-141">In hello **Properties** panel, set hello **Public Read Access** permissions for hello **templates** container too**Blob**.</span></span>

6. <span data-ttu-id="1a50d-142">在**伺服器總管**，以滑鼠右鍵按一下 hello**範本**容器，然後按一下**檢視 Blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="1a50d-142">In **Server Explorer**, right-click on hello **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="1a50d-143">按一下 hello**上傳 Blob**按鈕、 選取 hello 兩個檔案， **parameters.json**和**templates.json**，然後按一下**開啟**tooupload hello JSON 檔案 toohello**範本**容器。</span><span class="sxs-lookup"><span data-stu-id="1a50d-143">Click hello **Upload Blob** button, select hello two files, **parameters.json** and **templates.json**, and then click **Open** tooupload hello JSON files toohello **templates** container.</span></span> <span data-ttu-id="1a50d-144">hello 的 hello blob 包含 hello JSON 資料的 Url 是：</span><span class="sxs-lookup"><span data-stu-id="1a50d-144">hello URLs of hello blobs containing hello JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="1a50d-145">加入下列方法 tooProgram.cs hello:</span><span class="sxs-lookup"><span data-stu-id="1a50d-145">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="1a50d-146">新增下列程式碼 toohello hello **CreateIoTHub**方法 toosubmit hello 範本和參數檔案 toohello Azure 資源管理員：</span><span class="sxs-lookup"><span data-stu-id="1a50d-146">Add hello following code toohello **CreateIoTHub** method toosubmit hello template and parameter files toohello Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="1a50d-147">新增下列程式碼 toohello hello **CreateIoTHub**顯示 hello 狀態和 hello hello 新的 IoT 中樞的方法：</span><span class="sxs-lookup"><span data-stu-id="1a50d-147">Add hello following code toohello **CreateIoTHub** method that displays hello status and hello keys for hello new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="1a50d-148">完成並執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="1a50d-148">Complete and run hello application</span></span>

<span data-ttu-id="1a50d-149">您現在可以完成 hello 應用程式呼叫 hello **CreateIoTHub**方法再進行建置和執行它。</span><span class="sxs-lookup"><span data-stu-id="1a50d-149">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="1a50d-150">新增下列程式碼 toohello 結尾 hello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="1a50d-150">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="1a50d-151">按一下 [建置]，然後按一下 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="1a50d-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="1a50d-152">更正所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="1a50d-152">Correct any errors.</span></span>

3. <span data-ttu-id="1a50d-153">按一下**偵錯**然後**開始偵錯**toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a50d-153">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="1a50d-154">可能需要幾分鐘的時間 hello 部署 toorun。</span><span class="sxs-lookup"><span data-stu-id="1a50d-154">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="1a50d-155">您的應用程式加入的 tooverify hello IoT 中樞，請瀏覽 hello [Azure 入口網站][ lnk-azure-portal]並檢視您資源的清單。</span><span class="sxs-lookup"><span data-stu-id="1a50d-155">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="1a50d-156">或者，使用 hello **Get AzureRmResource** PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1a50d-156">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="1a50d-157">此範例應用程式會加入您付費的「S1 標準 IoT 中樞」。</span><span class="sxs-lookup"><span data-stu-id="1a50d-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="1a50d-158">您可以刪除透過 hello hello IoT 中樞[Azure 入口網站][ lnk-azure-portal]或使用 hello**移除 AzureRmResource** PowerShell 指令程式完成時。</span><span class="sxs-lookup"><span data-stu-id="1a50d-158">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a50d-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a50d-159">Next steps</span></span>
<span data-ttu-id="1a50d-160">現在您已經部署 IoT 中樞與 C# 程式使用 Azure Resource Manager 範本，您可以進一步 tooexplore:</span><span class="sxs-lookup"><span data-stu-id="1a50d-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want tooexplore further:</span></span>

* <span data-ttu-id="1a50d-161">閱讀有關 hello hello 功能[IoT 中樞資源提供者 REST API][lnk-rest-api]。</span><span class="sxs-lookup"><span data-stu-id="1a50d-161">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="1a50d-162">讀取[Azure 資源管理員概觀][ lnk-azure-rm-overview] toolearn 更多關於 hello 功能的 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="1a50d-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="1a50d-163">進一步了解開發的 IoT 中樞 toolearn，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="1a50d-163">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="1a50d-164">[簡介 tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="1a50d-164">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="1a50d-165">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="1a50d-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="1a50d-166">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="1a50d-166">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1a50d-167">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="1a50d-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
