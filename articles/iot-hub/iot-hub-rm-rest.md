---
title: "使用資源提供者 REST API 建立 Azure IoT 中樞 | Microsoft Docs"
description: "如何使用資源提供者 REST API 建立 IoT 中樞。"
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
ms.openlocfilehash: e443259507aacbefca141be4c9c1688ab19bf6ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-resource-provider-rest-api-net"></a><span data-ttu-id="6da6e-103">使用資源提供者 REST API 建立 IoT 中樞 (.NET)</span><span class="sxs-lookup"><span data-stu-id="6da6e-103">Create an IoT hub using the resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="6da6e-104">您可透過程式設計方式，使用 [IoT 中樞資源提供者 REST API][lnk-rest-api] 建立和管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6da6e-104">You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="6da6e-105">本教學課程說明如何使用「IoT 中樞資源提供者 REST API」從 C# 程式建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6da6e-105">This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="6da6e-106">Azure 有兩種不同的部署模型可建立和處理資源：[Azure Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6da6e-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="6da6e-107">本文涵蓋使用 Azure Resource Manager 部署模型的部分。</span><span class="sxs-lookup"><span data-stu-id="6da6e-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="6da6e-108">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6da6e-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="6da6e-109">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="6da6e-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="6da6e-110">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6da6e-110">An active Azure account.</span></span> <br/><span data-ttu-id="6da6e-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="6da6e-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="6da6e-112">[Azure PowerShell 1.0][lnk-powershell-install] 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6da6e-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="6da6e-113">準備 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="6da6e-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="6da6e-114">在 Visual Studio 中，使用 [主控台應用程式 (.NET Framework)] 專案範本，建立 Visual C# Windows 傳統桌面專案。</span><span class="sxs-lookup"><span data-stu-id="6da6e-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="6da6e-115">將專案命名為 **CreateIoTHubREST**。</span><span class="sxs-lookup"><span data-stu-id="6da6e-115">Name the project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="6da6e-116">在方案總管中，於專案上按一下滑鼠右鍵，然後按一下 [管理 NuGet 封裝] 。</span><span class="sxs-lookup"><span data-stu-id="6da6e-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="6da6e-117">在 NuGet 套件管理員中，勾選 [包含發行前版本]，然後在 [瀏覽] 頁面上搜尋 **Microsoft.Azure.Management.ResourceManager**。</span><span class="sxs-lookup"><span data-stu-id="6da6e-117">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="6da6e-118">選取套件，按一下 [安裝]，在 [檢閱變更] 中按一下 [確定]，然後按一下 [我接受] 來接受授權。</span><span class="sxs-lookup"><span data-stu-id="6da6e-118">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="6da6e-119">在 NuGet 套件管理員中，搜尋 **Microsoft.IdentityModel.Clients.ActiveDirectory**。</span><span class="sxs-lookup"><span data-stu-id="6da6e-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="6da6e-120">按一下 [安裝]，在 [檢閱變更] 中按一下 [確定]，然後按一下 [我接受] 來接受授權。</span><span class="sxs-lookup"><span data-stu-id="6da6e-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="6da6e-121">在 Program.cs 中，以下列程式碼取代現有的 **using** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="6da6e-121">In Program.cs, replace the existing **using** statements with the following code:</span></span>

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

6. <span data-ttu-id="6da6e-122">在 Program.cs 中，以下列靜態變數取代預留位置值。</span><span class="sxs-lookup"><span data-stu-id="6da6e-122">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="6da6e-123">您先前已在本教學課程中記下 **ApplicationId**、**SubscriptionId**、**TenantId** 及 **Password**。</span><span class="sxs-lookup"><span data-stu-id="6da6e-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="6da6e-124">**資源群組名稱**是您建立 IoT 中樞時所使用之資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="6da6e-124">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="6da6e-125">您可以使用預先存在或新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6da6e-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="6da6e-126">**IoT 中樞名稱**是您建立的 IoT 中樞名稱，例如 **MyIoTHub**。</span><span class="sxs-lookup"><span data-stu-id="6da6e-126">**IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="6da6e-127">您 IoT 中樞的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="6da6e-127">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="6da6e-128">**部署名稱**是部署的名稱，例如 **Deployment_01**。</span><span class="sxs-lookup"><span data-stu-id="6da6e-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-the-resource-provider-rest-api-to-create-an-iot-hub"></a><span data-ttu-id="6da6e-129">使用資源提供者 REST API 建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="6da6e-129">Use the resource provider REST API to create an IoT hub</span></span>

<span data-ttu-id="6da6e-130">使用 [IoT 中樞資源提供者 REST API][lnk-rest-api] 在資源群組中建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6da6e-130">Use the [IoT Hub resource provider REST API][lnk-rest-api] to create an IoT hub in your resource group.</span></span> <span data-ttu-id="6da6e-131">您也可以使用資源提供者 REST API 變更現有的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6da6e-131">You can also use the resource provider REST API to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="6da6e-132">將下列方法新增至 Program.cs：</span><span class="sxs-lookup"><span data-stu-id="6da6e-132">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="6da6e-133">將下列程式碼加入 **CreateIoTHub** 方法。</span><span class="sxs-lookup"><span data-stu-id="6da6e-133">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="6da6e-134">此程式碼會建立標頭中含有驗證權杖的 **HttpClient** 物件：</span><span class="sxs-lookup"><span data-stu-id="6da6e-134">This code creates an **HttpClient** object with the authentication token in the headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="6da6e-135">將下列程式碼加入 **CreateIoTHub** 方法。</span><span class="sxs-lookup"><span data-stu-id="6da6e-135">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="6da6e-136">此程式碼說明 IoT 中樞建立並產生 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="6da6e-136">This code describes the IoT hub to create and generates a JSON representation.</span></span> <span data-ttu-id="6da6e-137">如需目前支援「IoT 中樞」的位置清單，請參閱 [Azure 狀態][lnk-status]：</span><span class="sxs-lookup"><span data-stu-id="6da6e-137">For the current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="6da6e-138">將下列程式碼加入 **CreateIoTHub** 方法。</span><span class="sxs-lookup"><span data-stu-id="6da6e-138">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="6da6e-139">這段程式碼會將 REST 要求提交至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6da6e-139">This code submits the REST request to Azure.</span></span> <span data-ttu-id="6da6e-140">程式碼接著會檢查回應，並擷取可用來監視部署工作狀態的 URL：</span><span class="sxs-lookup"><span data-stu-id="6da6e-140">The code then checks the response and retrieves the URL you can use to monitor the state of the deployment task:</span></span>

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

5. <span data-ttu-id="6da6e-141">將下列程式碼加入 **CreateIoTHub** 方法的結尾。</span><span class="sxs-lookup"><span data-stu-id="6da6e-141">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="6da6e-142">此程式碼會使用上一個步驟中擷取的 **asyncStatusUri** 位址來等待部署完成：</span><span class="sxs-lookup"><span data-stu-id="6da6e-142">This code uses the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="6da6e-143">將下列程式碼加入 **CreateIoTHub** 方法的結尾。</span><span class="sxs-lookup"><span data-stu-id="6da6e-143">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="6da6e-144">此程式碼會擷取您建立的 IoT 中樞索引鍵，並列印到主控台︰</span><span class="sxs-lookup"><span data-stu-id="6da6e-144">This code retrieves the keys of the IoT hub you created and prints them to the console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="6da6e-145">完成並執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6da6e-145">Complete and run the application</span></span>

<span data-ttu-id="6da6e-146">在建置和執行應用程式之前，您現在可以呼叫 **CreateIoTHub** 方法來完成應用程式。</span><span class="sxs-lookup"><span data-stu-id="6da6e-146">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="6da6e-147">在 **Main** 方法的結尾加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6da6e-147">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="6da6e-148">按一下 [建置]，然後按一下 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="6da6e-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="6da6e-149">更正所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="6da6e-149">Correct any errors.</span></span>

3. <span data-ttu-id="6da6e-150">按一下 [偵錯]，然後按一下 [開始偵錯] 以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6da6e-150">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="6da6e-151">可能需要數分鐘的時間，部署才會開始執行。</span><span class="sxs-lookup"><span data-stu-id="6da6e-151">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="6da6e-152">若要確認您的應用程式已新增新的 IoT 中樞，請前往 [Azure 入口網站][ lnk-azure-portal]並檢視您的資源清單。</span><span class="sxs-lookup"><span data-stu-id="6da6e-152">To verify that your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="6da6e-153">或者，使用 **Get-AzureRmResource** PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6da6e-153">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="6da6e-154">此範例應用程式會加入您付費的「S1 標準 IoT 中樞」。</span><span class="sxs-lookup"><span data-stu-id="6da6e-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="6da6e-155">完成後，您可透過 [Azure 入口網站][lnk-azure-portal]刪除此 IoT 中樞，或在完成後使用 **Remove-AzureRmResource** PowerShell Cmdlet 加以刪除。</span><span class="sxs-lookup"><span data-stu-id="6da6e-155">When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6da6e-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6da6e-156">Next steps</span></span>
<span data-ttu-id="6da6e-157">現在您已經使用資源提供者 REST API 部署 IoT 中樞，您可以進一步探索：</span><span class="sxs-lookup"><span data-stu-id="6da6e-157">Now you have deployed an IoT hub using the resource provider REST API, you may want to explore further:</span></span>

* <span data-ttu-id="6da6e-158">閱讀 [IoT 中樞資源提供者 REST API][lnk-rest-api] 功能的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6da6e-158">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="6da6e-159">如需 Azure Resource Manager 功能的詳細資訊，請參閱 [Azure Resource Manager 概觀][lnk-azure-rm-overview]。</span><span class="sxs-lookup"><span data-stu-id="6da6e-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="6da6e-160">若要深入了解如何開發 IoT 中樞，請參閱以下文章︰</span><span class="sxs-lookup"><span data-stu-id="6da6e-160">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="6da6e-161">[C SDK 簡介][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="6da6e-161">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="6da6e-162">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="6da6e-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="6da6e-163">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="6da6e-163">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6da6e-164">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6da6e-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
