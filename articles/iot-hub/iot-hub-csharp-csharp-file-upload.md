---
title: "將裝置中的檔案上傳至使用 .NET 的 Azure IoT 中樞 | Microsoft Docs"
description: "如何使用適用於 .NET 的 Azure IoT 裝置 SDK 將檔案從裝置上傳至雲端。 上傳的檔案會儲存在 Azure 儲存體 blob 容器中。"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: b45d85d0d77cf47f36cb793bc8c0dbe2d5c12634
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub-using-net"></a><span data-ttu-id="9e1cf-104">以使用 .NET 的 IoT 中樞將檔案從裝置上傳至雲端</span><span class="sxs-lookup"><span data-stu-id="9e1cf-104">Upload files from your device to the cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="9e1cf-105">本教學課程是以 [使用 IoT 中樞傳送雲端到裝置訊息](iot-hub-csharp-csharp-c2d.md) 教學課程中的程式碼來建置，示範如何使用 IoT 中樞的檔案上傳功能。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial to show you how to use the file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="9e1cf-106">這會說明如何：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-106">It shows you how to:</span></span>

- <span data-ttu-id="9e1cf-107">安全地將 Azure Blob URI 提供給裝置，以便上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="9e1cf-108">您可以使用 IoT 中樞檔案上傳通知來觸發在您的應用程式後端中處理此檔案。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="9e1cf-109">[開始使用 IoT 中樞](iot-hub-csharp-csharp-getstarted.md)和[使用 IoT 中樞傳送雲端到裝置訊息](iot-hub-csharp-csharp-c2d.md)教學課程，示範 IoT 中樞基本的裝置到雲端和雲端到裝置的傳訊功能。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-109">The [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="9e1cf-110">[處理裝置到雲端訊息](iot-hub-csharp-csharp-process-d2c.md)教學課程說明能在 Azure Blob 儲存體中可靠地儲存裝置到雲端訊息的方法。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-110">The [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="9e1cf-111">不過，在某些情況下，您無法輕易地將裝置傳送的資料對應到 IoT 中樞接受且相對較小的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="9e1cf-112">例如：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-112">For example:</span></span>

* <span data-ttu-id="9e1cf-113">包含映像的大型檔案</span><span class="sxs-lookup"><span data-stu-id="9e1cf-113">Large files that contain images</span></span>
* <span data-ttu-id="9e1cf-114">影片</span><span class="sxs-lookup"><span data-stu-id="9e1cf-114">Videos</span></span>
* <span data-ttu-id="9e1cf-115">取樣高頻率的震動資料</span><span class="sxs-lookup"><span data-stu-id="9e1cf-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="9e1cf-116">某種經前置處理過的資料</span><span class="sxs-lookup"><span data-stu-id="9e1cf-116">Some form of preprocessed data</span></span>

<span data-ttu-id="9e1cf-117">這些檔案通常會使用工具 (例如 [Azure Data Factory](../data-factory/index.md) 或 [Hadoop](../hdinsight/index.md) 堆疊) 在雲端中進行批次處理。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="9e1cf-118">當您需要從裝置上傳檔案時，您仍然可以使用安全可靠的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-118">When you need to upload files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="9e1cf-119">在本教學課程結尾處，您會執行兩個 .NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-119">At the end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="9e1cf-120">**SimulatedDevice**，此為[使用 IoT 中樞傳送雲端到裝置訊息](iot-hub-csharp-csharp-c2d.md)教學課程中建立的應用程式修改版本。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-120">**SimulatedDevice**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="9e1cf-121">此應用程式可以使用 IoT 中樞提供的 SAS URI，將檔案上傳到儲存體。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="9e1cf-122">**ReadFileUploadNotification**，它會接收來自 IoT 中樞的檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="9e1cf-123">IoT 中樞透過 Azure IoT 裝置 SDK 來支援許多裝置平台和語言 (包括 C、Java 及 Javascript)。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="9e1cf-124">如需如何將您的裝置連接到 Azure IoT 中樞的逐步指示，請參閱 [Azure IoT 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="9e1cf-125">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="9e1cf-126">Visual Studio 2015 或 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9e1cf-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="9e1cf-127">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-127">An active Azure account.</span></span> <span data-ttu-id="9e1cf-128">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="9e1cf-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="9e1cf-129">從裝置應用程式上傳檔案</span><span class="sxs-lookup"><span data-stu-id="9e1cf-129">Upload a file from a device app</span></span>

<span data-ttu-id="9e1cf-130">在本節中，您將修改在[使用 IoT 中樞傳送雲端到裝置訊息](iot-hub-csharp-csharp-c2d.md)中建立的裝置應用程式，以接收來自 IoT 中樞的雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-130">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="9e1cf-131">在 Visual Studio 中，以滑鼠右鍵按一下 **SimulatedDevice** 專案，按一下 [新增]，然後按一下 [現有項目]。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-131">In Visual Studio, right-click the **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="9e1cf-132">瀏覽至影像檔並將它包含在您的專案中。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-132">Navigate to an image file and include it in your project.</span></span> <span data-ttu-id="9e1cf-133">本教學課程假設影像名稱為 `image.jpg`。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-133">This tutorial assumes the image is named `image.jpg`.</span></span>

1. <span data-ttu-id="9e1cf-134">以滑鼠右鍵按一下影像，然後按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-134">Right-click on the image, and then click **Properties**.</span></span> <span data-ttu-id="9e1cf-135">確定 [複製到輸出目錄] 是設為 [一律複製]。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-135">Make sure that **Copy to Output Directory** is set to **Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="9e1cf-136">在 **Program.cs** 檔的頂端，新增下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-136">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="9e1cf-137">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-137">Add the following method to the **Program** class:</span></span>

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time to upload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    <span data-ttu-id="9e1cf-138">`UploadToBlobAsync` 方法會取得要上傳之檔案的檔案名稱與資料流來源，然後處理上傳至儲存體的工作。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-138">The `UploadToBlobAsync` method takes in the file name and stream source of the file to be uploaded and handles the upload to storage.</span></span> <span data-ttu-id="9e1cf-139">主控台應用程式會顯示上傳檔案所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-139">The console app displays the time it takes to upload the file.</span></span>

1. <span data-ttu-id="9e1cf-140">將下列方法新增到 **Main** 方法中緊接在 `Console.ReadLine()` 行前面：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-140">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="9e1cf-141">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="9e1cf-142">在生產環境程式碼中，您應該如 MSDN 文章 [暫時性錯誤處理]所建議，實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="9e1cf-143">接收檔案上傳通知</span><span class="sxs-lookup"><span data-stu-id="9e1cf-143">Receive a file upload notification</span></span>

<span data-ttu-id="9e1cf-144">在本節中，您將撰寫 .NET 主控台應用程式，以接收來自 IoT 中樞的檔案上傳通知訊息。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="9e1cf-145">在目前的 Visual Studio 方案中，使用 [主控台應用程式] 專案範本來建立 Visual C# Windows 專案。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-145">In the current Visual Studio solution, create a Visual C# Windows project by using the **Console Application** project template.</span></span> <span data-ttu-id="9e1cf-146">將專案命名為 **ReadFileUploadNotification**。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-146">Name the project **ReadFileUploadNotification**.</span></span>

    ![Visual Studio 中的新專案][2]

1. <span data-ttu-id="9e1cf-148">在 [方案總管] 中，以滑鼠右鍵按一下 **ReadFileUploadNotification** 專案，然後按一下 [管理 NuGet 套件...]。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-148">In Solution Explorer, right-click the **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="9e1cf-149">在 [NuGet 套件管理員] 視窗中，搜尋 **Microsoft.Azure.Devices**，按一下 [安裝] 並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-149">In the **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span>

    <span data-ttu-id="9e1cf-150">此動作會下載和安裝 [Azure IoT 服務 SDK NuGet 套件]，並在 **ReadFileUploadNotification** 專案中新增此套件的參考。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-150">This action downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package] in the **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="9e1cf-151">在 **Program.cs** 檔的頂端，新增下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-151">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="9e1cf-152">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="9e1cf-153">以 [開始使用 IoT 中樞]的 IoT 中樞連接字串取代預留位置的值：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-153">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="9e1cf-154">將下列方法新增至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-154">Add the following method to the **Program** class:</span></span>

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    <span data-ttu-id="9e1cf-155">請注意，此接收模式與用來從裝置應用程式接收雲端到裝置訊息的模式相同。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-155">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>

1. <span data-ttu-id="9e1cf-156">最後，將下列幾行加入至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-156">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter to exit\n");
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="9e1cf-157">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="9e1cf-157">Run the applications</span></span>

<span data-ttu-id="9e1cf-158">現在您已經準備好執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-158">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="9e1cf-159">在 Visual Studio 中，在您的方案上按一下滑鼠右鍵，然後選取 [設定啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="9e1cf-160">選取 [多個啟始專案]，然後針對 **ReadFileUploadNotification** 和 **SimulatedDevice** 選取 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-160">Select **Multiple startup projects**, then select the **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="9e1cf-161">按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-161">Press **F5**.</span></span> <span data-ttu-id="9e1cf-162">這兩個應用程式應該都會啟動。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-162">Both applications should start.</span></span> <span data-ttu-id="9e1cf-163">您應該會在其中一個主控台應用程式中看到上傳已完成，以及另一個主控台應用程式所收到的上傳通知訊息。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-163">You should see the upload completed in one console app and the upload notification message received by the other console app.</span></span> <span data-ttu-id="9e1cf-164">您可以使用 [Azure 入口網站]或 Visual Studio 伺服器總管，在您的 Azure 儲存體帳戶中檢查上傳的檔案是否存在。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-164">You can use the [Azure portal] or Visual Studio Server Explorer to check for the presence of the uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="9e1cf-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e1cf-165">Next steps</span></span>

<span data-ttu-id="9e1cf-166">在本教學課程中，您已學到如何使用 IoT 中樞的檔案上傳功能來簡化從裝置上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="9e1cf-166">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="9e1cf-167">您可以利用下列文章繼續探索 IoT 中樞功能和案例：</span><span class="sxs-lookup"><span data-stu-id="9e1cf-167">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="9e1cf-168">[以程式設計方式建立 IoT 中樞][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="9e1cf-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="9e1cf-169">[C SDK 簡介][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="9e1cf-169">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="9e1cf-170">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="9e1cf-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="9e1cf-171">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="9e1cf-171">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9e1cf-172">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="9e1cf-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

<span data-ttu-id="9e1cf-173">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="9e1cf-173">[Azure portal]: https://portal.azure.com/</span></span>

<span data-ttu-id="9e1cf-174">[Azure IoT 開發人員中心]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="9e1cf-174">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>

<span data-ttu-id="9e1cf-175">[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="9e1cf-175">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="9e1cf-176">[Azure IoT 服務 SDK NuGet 套件]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span><span class="sxs-lookup"><span data-stu-id="9e1cf-176">[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
