---
title: "使用範本建立 Azure IoT 中樞 (.NET) | Microsoft Docs"
description: "如何在 C# 程式中使用 Azure Resource Manager 範本建立 IoT 中樞。"
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
ms.openlocfilehash: 0f197a28e0c51b06d0b47a03c29fe1fde0c6b78d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="ee381-103">使用 Azure Resource Manager 範本建立 IoT 中樞 (.NET)</span><span class="sxs-lookup"><span data-stu-id="ee381-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="ee381-104">您可以使用 Azure 資源管理員，以程式設計方式建立和管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ee381-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="ee381-105">本教學課程示範如何使用 Azure Resource Manager 範本從 C# 程式建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ee381-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="ee381-106">Azure 有兩種不同的部署模型可建立和處理資源：[Azure Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ee381-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="ee381-107">本文涵蓋使用 Azure Resource Manager 部署模型的部分。</span><span class="sxs-lookup"><span data-stu-id="ee381-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="ee381-108">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ee381-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="ee381-109">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="ee381-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="ee381-110">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee381-110">An active Azure account.</span></span> <br/><span data-ttu-id="ee381-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="ee381-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="ee381-112">可供您儲存 Azure Resource Manager 範本檔案的 [Azure 儲存體帳戶][lnk-storage-account]。</span><span class="sxs-lookup"><span data-stu-id="ee381-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="ee381-113">[Azure PowerShell 1.0][lnk-powershell-install] 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ee381-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="ee381-114">準備 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="ee381-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="ee381-115">在 Visual Studio 中，使用 [主控台應用程式 (.NET Framework)] 專案範本，建立 Visual C# Windows 傳統桌面專案。</span><span class="sxs-lookup"><span data-stu-id="ee381-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="ee381-116">將專案命名為 **CreateIoTHub**。</span><span class="sxs-lookup"><span data-stu-id="ee381-116">Name the project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="ee381-117">在方案總管中，於專案上按一下滑鼠右鍵，然後按一下 [管理 NuGet 封裝] 。</span><span class="sxs-lookup"><span data-stu-id="ee381-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="ee381-118">在 NuGet 套件管理員中，勾選 [包含發行前版本]，然後在 [瀏覽] 頁面上搜尋 **Microsoft.Azure.Management.ResourceManager**。</span><span class="sxs-lookup"><span data-stu-id="ee381-118">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="ee381-119">選取套件，按一下 [安裝]，在 [檢閱變更] 中按一下 [確定]，然後按一下 [我接受] 來接受授權。</span><span class="sxs-lookup"><span data-stu-id="ee381-119">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="ee381-120">在 NuGet 套件管理員中，搜尋 **Microsoft.IdentityModel.Clients.ActiveDirectory**。</span><span class="sxs-lookup"><span data-stu-id="ee381-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="ee381-121">按一下 [安裝]，在 [檢閱變更] 中按一下 [確定]，然後按一下 [我接受] 來接受授權。</span><span class="sxs-lookup"><span data-stu-id="ee381-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="ee381-122">在 Program.cs 中，以下列程式碼取代現有的 **using** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ee381-122">In Program.cs, replace the existing **using** statements with the following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="ee381-123">在 Program.cs 中，以下列靜態變數取代預留位置值。</span><span class="sxs-lookup"><span data-stu-id="ee381-123">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="ee381-124">您先前已在本教學課程中記下 **ApplicationId**、**SubscriptionId**、**TenantId** 及 **Password**。</span><span class="sxs-lookup"><span data-stu-id="ee381-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="ee381-125">**儲存體帳戶名稱**是您儲存 Azure Resource Manager 範本檔案之「Azure 儲存體」帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="ee381-125">**Your Azure Storage account name** is the name of the Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="ee381-126">**資源群組名稱**是您建立 IoT 中樞時所使用之資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="ee381-126">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="ee381-127">名稱可以是預先存在或新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ee381-127">The name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="ee381-128">**部署名稱**是部署的名稱，例如 **Deployment_01**。</span><span class="sxs-lookup"><span data-stu-id="ee381-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="ee381-129">提交範本，以建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="ee381-129">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="ee381-130">使用 JSON 範本和參數檔案，在資源群組中建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ee381-130">Use a JSON template and parameter file to create an IoT hub in your resource group.</span></span> <span data-ttu-id="ee381-131">您也可以使用 Azure Resource Manager 範本來對現有的 IoT 中樞進行變更。</span><span class="sxs-lookup"><span data-stu-id="ee381-131">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="ee381-132">在 [方案總管] 中，於專案上按一下滑鼠右鍵，按一下 [加入]，然後按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="ee381-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="ee381-133">將名為 **template.json** 的 JSON 檔案新增到專案中。</span><span class="sxs-lookup"><span data-stu-id="ee381-133">Add a JSON file called **template.json** to your project.</span></span>

2. <span data-ttu-id="ee381-134">若要將標準 IoT 中樞新增到**美國東部**區域，請以下列資源定義取代 **template.json** 的內容。</span><span class="sxs-lookup"><span data-stu-id="ee381-134">To add a standard IoT hub to the **East US** region, replace the contents of **template.json** with the following resource definition.</span></span> <span data-ttu-id="ee381-135">如需目前支援「IoT 中樞」的區域清單，請參閱 [Azure 狀態][lnk-status]：</span><span class="sxs-lookup"><span data-stu-id="ee381-135">For the current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="ee381-136">在 [方案總管] 中，於專案上按一下滑鼠右鍵，按一下 [加入]，然後按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="ee381-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="ee381-137">將名為 **parameters.json** 的 JSON 檔案新增到專案中。</span><span class="sxs-lookup"><span data-stu-id="ee381-137">Add a JSON file called **parameters.json** to your project.</span></span>

4. <span data-ttu-id="ee381-138">使用下列參數資訊來取代 **parameters.json** 的內容，此參數資訊會設定新 IoT 中樞的名稱，例如 **{your initials}mynewiothub**。</span><span class="sxs-lookup"><span data-stu-id="ee381-138">Replace the contents of **parameters.json** with the following parameter information that sets a name for the new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="ee381-139">IoT 中樞名稱必須是全域唯一的，因此應該包含您的名稱或縮寫：</span><span class="sxs-lookup"><span data-stu-id="ee381-139">The IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="ee381-140">在 [伺服器總管] 中，連接到您的 Azure 訂用帳戶，然後在您的「Azure 儲存體」帳戶中建立名為 **templates** 的容器。</span><span class="sxs-lookup"><span data-stu-id="ee381-140">In **Server Explorer**, connect to your Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="ee381-141">在 [屬性] 面板中，將 **templates** 容器的 [公用讀取存取] 權限設定為 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="ee381-141">In the **Properties** panel, set the **Public Read Access** permissions for the **templates** container to **Blob**.</span></span>

6. <span data-ttu-id="ee381-142">在 [伺服器總管] 中，於 [templates] 容器上按一下滑鼠右鍵，然後按一下 [檢視 Blob 容器]。</span><span class="sxs-lookup"><span data-stu-id="ee381-142">In **Server Explorer**, right-click on the **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="ee381-143">按一下 [上傳 Blob] 按鈕，選取 **parameters.json** 和 **templates.json** 這兩個檔案，然後按一下 [開啟]，將 JSON 檔案上傳至 **templates** 容器。</span><span class="sxs-lookup"><span data-stu-id="ee381-143">Click the **Upload Blob** button, select the two files, **parameters.json** and **templates.json**, and then click **Open** to upload the JSON files to the **templates** container.</span></span> <span data-ttu-id="ee381-144">包含 JSON 資料的 blob 的 URL 如下：</span><span class="sxs-lookup"><span data-stu-id="ee381-144">The URLs of the blobs containing the JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="ee381-145">將下列方法新增至 Program.cs：</span><span class="sxs-lookup"><span data-stu-id="ee381-145">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="ee381-146">將下列程式碼加入 **CreateIoTHub** 方法，以提交範本和參數檔案給 Azure Resource Manager：</span><span class="sxs-lookup"><span data-stu-id="ee381-146">Add the following code to the **CreateIoTHub** method to submit the template and parameter files to the Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="ee381-147">將下列程式碼加入 **CreateIoTHub** 方法，以顯示新的 IoT 中樞的狀態和金鑰：</span><span class="sxs-lookup"><span data-stu-id="ee381-147">Add the following code to the **CreateIoTHub** method that displays the status and the keys for the new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed to create iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="ee381-148">完成並執行應用程式</span><span class="sxs-lookup"><span data-stu-id="ee381-148">Complete and run the application</span></span>

<span data-ttu-id="ee381-149">在建置和執行應用程式之前，您現在可以呼叫 **CreateIoTHub** 方法來完成應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee381-149">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="ee381-150">在 **Main** 方法的結尾加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="ee381-150">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="ee381-151">按一下 [建置]，然後按一下 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="ee381-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="ee381-152">更正所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="ee381-152">Correct any errors.</span></span>

3. <span data-ttu-id="ee381-153">按一下 [偵錯]，然後按一下 [開始偵錯] 以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee381-153">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="ee381-154">可能需要數分鐘的時間，部署才會開始執行。</span><span class="sxs-lookup"><span data-stu-id="ee381-154">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="ee381-155">若要確認您的應用程式已新增新的 IoT 中樞，請前往 [Azure 入口網站][ lnk-azure-portal]並檢視您的資源清單。</span><span class="sxs-lookup"><span data-stu-id="ee381-155">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="ee381-156">或者，使用 **Get-AzureRmResource** PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ee381-156">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="ee381-157">此範例應用程式會加入您付費的「S1 標準 IoT 中樞」。</span><span class="sxs-lookup"><span data-stu-id="ee381-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="ee381-158">您可透過 [Azure 入口網站][lnk-azure-portal]刪除此 IoT 中樞，或在完成時，使用 **Remove-AzureRmResource** PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ee381-158">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee381-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee381-159">Next steps</span></span>
<span data-ttu-id="ee381-160">現在您已經使用 Azure Resource Manager 範本和 C# 程式部署 IoT 中樞，可以進一步探索：</span><span class="sxs-lookup"><span data-stu-id="ee381-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want to explore further:</span></span>

* <span data-ttu-id="ee381-161">閱讀 [IoT 中樞資源提供者 REST API][lnk-rest-api] 功能的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ee381-161">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="ee381-162">如需 Azure Resource Manager 功能的詳細資訊，請參閱 [Azure Resource Manager 概觀][lnk-azure-rm-overview]。</span><span class="sxs-lookup"><span data-stu-id="ee381-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="ee381-163">若要深入了解如何開發 IoT 中樞，請參閱以下文章︰</span><span class="sxs-lookup"><span data-stu-id="ee381-163">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="ee381-164">[C SDK 簡介][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="ee381-164">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="ee381-165">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="ee381-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="ee381-166">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="ee381-166">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ee381-167">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ee381-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
