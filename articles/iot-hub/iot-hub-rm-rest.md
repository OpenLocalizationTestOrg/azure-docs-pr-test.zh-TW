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
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a><span data-ttu-id="6d8fd-103">建立 IoT 中心使用 hello 資源提供者 REST API (.NET)</span><span class="sxs-lookup"><span data-stu-id="6d8fd-103">Create an IoT hub using hello resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="6d8fd-104">您可以使用 hello [IoT 中樞資源提供者 REST API] [ lnk-rest-api] toocreate 並以程式設計方式管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-104">You can use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="6d8fd-105">本教學課程會示範如何 toouse 會 hello IoT 中樞資源提供者 REST API toocreate C# 程式從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-105">This tutorial shows you how toouse hello IoT Hub resource provider REST API toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="6d8fd-106">Azure 有兩種不同的部署模型可建立和處理資源：[Azure Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="6d8fd-107">本文件涵蓋使用 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="6d8fd-108">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="6d8fd-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="6d8fd-109">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="6d8fd-110">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-110">An active Azure account.</span></span> <br/><span data-ttu-id="6d8fd-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="6d8fd-112">[Azure PowerShell 1.0][lnk-powershell-install] 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="6d8fd-113">準備 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="6d8fd-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="6d8fd-114">在 Visual Studio 中，建立 Visual C# Windows 傳統桌面專案使用 hello**主控台應用程式 (.NET Framework)**專案範本。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="6d8fd-115">名稱 hello 專案**CreateIoTHubREST**。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-115">Name hello project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="6d8fd-116">在方案總管中，於專案上按一下滑鼠右鍵，然後按一下管理 NuGet 封裝 。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="6d8fd-117">在 [NuGet 封裝管理員] 中，檢查**包含發行前版本**，在 hello**瀏覽**頁面搜尋**Microsoft.Azure.Management.ResourceManager**。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-117">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="6d8fd-118">選取 hello 封裝，按一下**安裝**，請在**檢閱變更**按一下**確定**，然後按一下 **我接受**tooaccept hello 授權。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-118">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="6d8fd-119">在 NuGet 套件管理員中，搜尋 **Microsoft.IdentityModel.Clients.ActiveDirectory**。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="6d8fd-120">按一下**安裝**，請在**檢閱變更**按一下**確定**，然後按一下 **我接受**tooaccept hello 授權。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="6d8fd-121">在 Program.cs 中，取代現有的 hello**使用**陳述式，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6d8fd-121">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

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

6. <span data-ttu-id="6d8fd-122">在 Program.cs 中，加入下列取代 hello 預留位置值的靜態變數的 hello。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-122">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="6d8fd-123">您先前已在本教學課程中記下 **ApplicationId**、**SubscriptionId**、**TenantId** 及 **Password**。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="6d8fd-124">**資源群組名稱**hello hello 建立 hello IoT 中樞時所使用的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-124">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="6d8fd-125">您可以使用預先存在或新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="6d8fd-126">**IoT 中樞名稱**hello hello 您建立時，例如 IoT 中樞名稱**MyIoTHub**。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-126">**IoT Hub name** is hello name of hello IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="6d8fd-127">IoT 中樞 hello 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-127">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="6d8fd-128">**部署名稱**是 hello 部署的名稱，例如**Deployment_01**。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a><span data-ttu-id="6d8fd-129">使用 hello 資源提供者 REST API toocreate IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="6d8fd-129">Use hello resource provider REST API toocreate an IoT hub</span></span>

<span data-ttu-id="6d8fd-130">使用 hello [IoT 中樞資源提供者 REST API] [ lnk-rest-api] toocreate IoT 中樞資源群組中。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-130">Use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="6d8fd-131">您也可以使用 hello 資源提供者 REST API toomake 變更 tooan 現有 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-131">You can also use hello resource provider REST API toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="6d8fd-132">加入下列方法 tooProgram.cs hello:</span><span class="sxs-lookup"><span data-stu-id="6d8fd-132">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="6d8fd-133">新增下列程式碼 toohello hello **CreateIoTHub**方法。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-133">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="6d8fd-134">此程式碼建立**HttpClient**與 hello 標頭中的 hello 驗證權杖的物件：</span><span class="sxs-lookup"><span data-stu-id="6d8fd-134">This code creates an **HttpClient** object with hello authentication token in hello headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="6d8fd-135">新增下列程式碼 toohello hello **CreateIoTHub**方法。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-135">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="6d8fd-136">此程式碼說明 hello IoT 中樞 toocreate，並產生的 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-136">This code describes hello IoT hub toocreate and generates a JSON representation.</span></span> <span data-ttu-id="6d8fd-137">如 hello 目前的位置，其支援 IoT 中樞的清單，請參閱[Azure 狀態][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="6d8fd-137">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="6d8fd-138">新增下列程式碼 toohello hello **CreateIoTHub**方法。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-138">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="6d8fd-139">此程式碼會送出 hello REST 要求 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-139">This code submits hello REST request tooAzure.</span></span> <span data-ttu-id="6d8fd-140">hello 程式碼會檢查 hello 回應，然後擷取 hello URL，您可以使用 toomonitor hello hello 部署工作狀態：</span><span class="sxs-lookup"><span data-stu-id="6d8fd-140">hello code then checks hello response and retrieves hello URL you can use toomonitor hello state of hello deployment task:</span></span>

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

5. <span data-ttu-id="6d8fd-141">新增下列程式碼 toohello 結尾 hello hello **CreateIoTHub**方法。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-141">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="6d8fd-142">此程式碼使用 hello **asyncStatusUri**位址擷取中的 hello 部署 toocomplete hello 上一個步驟 toowait:</span><span class="sxs-lookup"><span data-stu-id="6d8fd-142">This code uses hello **asyncStatusUri** address retrieved in hello previous step toowait for hello deployment toocomplete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="6d8fd-143">新增下列程式碼 toohello 結尾 hello hello **CreateIoTHub**方法。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-143">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="6d8fd-144">此程式碼會擷取 hello IoT 中樞，您建立並列印 toohello 主控台 hello 索引鍵：</span><span class="sxs-lookup"><span data-stu-id="6d8fd-144">This code retrieves hello keys of hello IoT hub you created and prints them toohello console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="6d8fd-145">完成並執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="6d8fd-145">Complete and run hello application</span></span>

<span data-ttu-id="6d8fd-146">您現在可以完成 hello 應用程式呼叫 hello **CreateIoTHub**方法再進行建置和執行它。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-146">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="6d8fd-147">新增下列程式碼 toohello 結尾 hello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="6d8fd-147">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="6d8fd-148">按一下 [建置]，然後按一下 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="6d8fd-149">更正所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-149">Correct any errors.</span></span>

3. <span data-ttu-id="6d8fd-150">按一下**偵錯**然後**開始偵錯**toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-150">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="6d8fd-151">可能需要幾分鐘的時間 hello 部署 toorun。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-151">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="6d8fd-152">加入您的應用程式的 tooverify hello IoT 中樞，請瀏覽 hello [Azure 入口網站][ lnk-azure-portal]並檢視您資源的清單。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-152">tooverify that your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="6d8fd-153">或者，使用 hello **Get AzureRmResource** PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-153">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="6d8fd-154">此範例應用程式會加入您付費的「S1 標準 IoT 中樞」。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="6d8fd-155">當您完成時，您可以刪除透過 hello hello IoT 中樞[Azure 入口網站][ lnk-azure-portal]或使用 hello**移除 AzureRmResource** PowerShell 指令程式完成時。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-155">When you are finished, you can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d8fd-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d8fd-156">Next steps</span></span>
<span data-ttu-id="6d8fd-157">現在您已經部署使用 hello 資源提供者 REST API IoT 中樞，您可以進一步 tooexplore:</span><span class="sxs-lookup"><span data-stu-id="6d8fd-157">Now you have deployed an IoT hub using hello resource provider REST API, you may want tooexplore further:</span></span>

* <span data-ttu-id="6d8fd-158">閱讀有關 hello hello 功能[IoT 中樞資源提供者 REST API][lnk-rest-api]。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-158">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="6d8fd-159">讀取[Azure 資源管理員概觀][ lnk-azure-rm-overview] toolearn 更多關於 hello 功能的 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="6d8fd-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="6d8fd-160">進一步了解開發的 IoT 中樞 toolearn，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="6d8fd-160">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="6d8fd-161">[簡介 tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="6d8fd-161">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="6d8fd-162">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="6d8fd-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="6d8fd-163">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="6d8fd-163">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6d8fd-164">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6d8fd-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
