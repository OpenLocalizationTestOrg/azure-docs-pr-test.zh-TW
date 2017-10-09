---
title: "從裝置 tooAzure IoT 中樞與.NET aaaUpload 檔案 |Microsoft 文件"
description: "如何從使用 Azure IoT 裝置 SDK for.NET 裝置 toohello 雲端檔案 tooupload。 上傳的檔案會儲存在 Azure 儲存體 blob 容器中。"
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
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a><span data-ttu-id="8b178-104">從您的裝置 toohello 雲端的檔案上傳與使用適用於.NET 的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="8b178-104">Upload files from your device toohello cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="8b178-105">本教學課程是 hello 程式碼在 hello[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-csharp-csharp-c2d.md)教學課程 tooshow 您 toouse hello 的 IoT 中樞的檔案上傳功能的方式。</span><span class="sxs-lookup"><span data-stu-id="8b178-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial tooshow you how toouse hello file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="8b178-106">這會說明如何：</span><span class="sxs-lookup"><span data-stu-id="8b178-106">It shows you how to:</span></span>

- <span data-ttu-id="8b178-107">安全地將 Azure Blob URI 提供給裝置，以便上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="8b178-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="8b178-108">使用 hello IoT 中樞檔案上傳通知 tootrigger 處理您的應用程式後端中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="8b178-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="8b178-109">hello[開始使用 IoT 中樞](iot-hub-csharp-csharp-getstarted.md)和[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-csharp-csharp-c2d.md)教學課程示範 hello 基本裝置到雲端 」 和 「 雲端到裝置訊息功能的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8b178-109">hello [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="8b178-110">hello[程序裝置到雲端訊息](iot-hub-csharp-csharp-process-d2c.md)教學課程描述方式 tooreliably 將裝置到雲端訊息儲存在 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8b178-110">hello [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="8b178-111">不過，在某些情況下您無法輕鬆地 hello 資料對應您的裝置傳送到 hello 相對較小裝置到雲端 IoT 中樞所接受訊息。</span><span class="sxs-lookup"><span data-stu-id="8b178-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="8b178-112">例如：</span><span class="sxs-lookup"><span data-stu-id="8b178-112">For example:</span></span>

* <span data-ttu-id="8b178-113">包含映像的大型檔案</span><span class="sxs-lookup"><span data-stu-id="8b178-113">Large files that contain images</span></span>
* <span data-ttu-id="8b178-114">影片</span><span class="sxs-lookup"><span data-stu-id="8b178-114">Videos</span></span>
* <span data-ttu-id="8b178-115">取樣高頻率的震動資料</span><span class="sxs-lookup"><span data-stu-id="8b178-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="8b178-116">某種經前置處理過的資料</span><span class="sxs-lookup"><span data-stu-id="8b178-116">Some form of preprocessed data</span></span>

<span data-ttu-id="8b178-117">這些檔案通常是使用類似的 hello 雲端中處理的批次[Azure Data Factory](../data-factory/index.md)或 hello [Hadoop](../hdinsight/index.md)堆疊。</span><span class="sxs-lookup"><span data-stu-id="8b178-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="8b178-118">當您需要從裝置 tooupload 檔案時，您仍然可以使用 hello 安全性和可靠性的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8b178-118">When you need tooupload files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="8b178-119">在本教學課程中的 hello 結尾，您會執行兩個.NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="8b178-119">At hello end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="8b178-120">**SimulatedDevice**，hello hello 中建立的應用程式的修改的版本[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-csharp-csharp-c2d.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="8b178-120">**SimulatedDevice**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="8b178-121">此應用程式上傳檔案 toostorage 使用提供的 IoT 中樞的 SAS URI。</span><span class="sxs-lookup"><span data-stu-id="8b178-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="8b178-122">**ReadFileUploadNotification**，它會接收來自 IoT 中樞的檔案上傳通知。</span><span class="sxs-lookup"><span data-stu-id="8b178-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="8b178-123">IoT 中樞透過 Azure IoT 裝置 SDK 來支援許多裝置平台和語言 (包括 C、Java 及 Javascript)。</span><span class="sxs-lookup"><span data-stu-id="8b178-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="8b178-124">請參閱 toohello [Azure IoT 開發人員中心]的逐步指示 tooconnect 您裝置 tooAzure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8b178-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="8b178-125">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="8b178-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="8b178-126">Visual Studio 2015 或 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8b178-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="8b178-127">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8b178-127">An active Azure account.</span></span> <span data-ttu-id="8b178-128">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="8b178-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="8b178-129">從裝置應用程式上傳檔案</span><span class="sxs-lookup"><span data-stu-id="8b178-129">Upload a file from a device app</span></span>

<span data-ttu-id="8b178-130">在本節中，您將修改 hello 裝置應用程式中建立[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-csharp-csharp-c2d.md)tooreceive 雲端到裝置訊息從 hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8b178-130">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="8b178-131">在 Visual Studio 中，以滑鼠右鍵按一下 hello **SimulatedDevice**專案中，按一下 **新增**，然後按一下**現有項目**。</span><span class="sxs-lookup"><span data-stu-id="8b178-131">In Visual Studio, right-click hello **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="8b178-132">瀏覽 tooan 映像檔，並將它包含在您的專案。</span><span class="sxs-lookup"><span data-stu-id="8b178-132">Navigate tooan image file and include it in your project.</span></span> <span data-ttu-id="8b178-133">本教學課程會假設名為 hello 映像`image.jpg`。</span><span class="sxs-lookup"><span data-stu-id="8b178-133">This tutorial assumes hello image is named `image.jpg`.</span></span>

1. <span data-ttu-id="8b178-134">Hello 影像上按一下滑鼠右鍵，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="8b178-134">Right-click on hello image, and then click **Properties**.</span></span> <span data-ttu-id="8b178-135">請確定**複製 tooOutput 目錄**設定得**永遠複製**。</span><span class="sxs-lookup"><span data-stu-id="8b178-135">Make sure that **Copy tooOutput Directory** is set too**Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="8b178-136">在 hello **Program.cs**檔案中加入下列陳述式在 hello hello 檔案最上方的 hello:</span><span class="sxs-lookup"><span data-stu-id="8b178-136">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="8b178-137">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="8b178-137">Add hello following method toohello **Program** class:</span></span>

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
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    <span data-ttu-id="8b178-138">hello`UploadToBlobAsync`方法會在 hello 檔案名稱和資料流來源的 hello 檔案 toobe 上傳和控制代碼 hello 上載 toostorage。</span><span class="sxs-lookup"><span data-stu-id="8b178-138">hello `UploadToBlobAsync` method takes in hello file name and stream source of hello file toobe uploaded and handles hello upload toostorage.</span></span> <span data-ttu-id="8b178-139">hello 主控台應用程式會顯示 hello tooupload hello 檔案所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="8b178-139">hello console app displays hello time it takes tooupload hello file.</span></span>

1. <span data-ttu-id="8b178-140">新增下列方法在 hello hello **Main**方法中的前 hello,`Console.ReadLine()`行：</span><span class="sxs-lookup"><span data-stu-id="8b178-140">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="8b178-141">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="8b178-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="8b178-142">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理]。</span><span class="sxs-lookup"><span data-stu-id="8b178-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="8b178-143">接收檔案上傳通知</span><span class="sxs-lookup"><span data-stu-id="8b178-143">Receive a file upload notification</span></span>

<span data-ttu-id="8b178-144">在本節中，您將撰寫 .NET 主控台應用程式，以接收來自 IoT 中樞的檔案上傳通知訊息。</span><span class="sxs-lookup"><span data-stu-id="8b178-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="8b178-145">Hello 目前 Visual Studio 方案中建立 Visual C# Windows 專案使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="8b178-145">In hello current Visual Studio solution, create a Visual C# Windows project by using hello **Console Application** project template.</span></span> <span data-ttu-id="8b178-146">名稱 hello 專案**ReadFileUploadNotification**。</span><span class="sxs-lookup"><span data-stu-id="8b178-146">Name hello project **ReadFileUploadNotification**.</span></span>

    ![Visual Studio 中的新專案][2]

1. <span data-ttu-id="8b178-148">在 [方案總管] 中，以滑鼠右鍵按一下 hello **ReadFileUploadNotification**專案，然後再按一下**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="8b178-148">In Solution Explorer, right-click hello **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="8b178-149">在 hello **NuGet 套件管理員**視窗中，搜尋**Microsoft.Azure.Devices**，按一下 **安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="8b178-149">In hello **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span>

    <span data-ttu-id="8b178-150">這個動作會下載、 安裝，並將參考 toohello [Azure IoT 服務 SDK 的 NuGet 封裝]在 hello **ReadFileUploadNotification**專案。</span><span class="sxs-lookup"><span data-stu-id="8b178-150">This action downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package] in hello **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="8b178-151">在 hello **Program.cs**檔案中加入下列陳述式在 hello hello 檔案最上方的 hello:</span><span class="sxs-lookup"><span data-stu-id="8b178-151">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="8b178-152">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="8b178-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="8b178-153">替代 hello 預留位置的值與 hello IoT 中樞連接字串從 [開始使用 IoT 中樞]:</span><span class="sxs-lookup"><span data-stu-id="8b178-153">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="8b178-154">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="8b178-154">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="8b178-155">請注意此接收模式是 hello hello 裝置應用程式來自相同一個使用的 tooreceive 雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="8b178-155">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>

1. <span data-ttu-id="8b178-156">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="8b178-156">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="8b178-157">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="8b178-157">Run hello applications</span></span>

<span data-ttu-id="8b178-158">現在您已準備好 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b178-158">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="8b178-159">在 Visual Studio 中，在您的方案上按一下滑鼠右鍵，然後選取 [設定啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="8b178-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="8b178-160">選取**多個啟始專案**，然後選取 hello**啟動**動作**ReadFileUploadNotification**和**SimulatedDevice**。</span><span class="sxs-lookup"><span data-stu-id="8b178-160">Select **Multiple startup projects**, then select hello **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="8b178-161">按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="8b178-161">Press **F5**.</span></span> <span data-ttu-id="8b178-162">這兩個應用程式應該都會啟動。</span><span class="sxs-lookup"><span data-stu-id="8b178-162">Both applications should start.</span></span> <span data-ttu-id="8b178-163">您應該會看到一個主控台應用程式中的 hello 上傳完成，而且所收到 hello 上傳通知訊息 hello 其他主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b178-163">You should see hello upload completed in one console app and hello upload notification message received by hello other console app.</span></span> <span data-ttu-id="8b178-164">您可以使用 hello [Azure 入口網站]或 Visual Studio 伺服器總管 toocheck hello hello 存在上傳您的 Azure 儲存體帳戶中的檔案。</span><span class="sxs-lookup"><span data-stu-id="8b178-164">You can use hello [Azure portal] or Visual Studio Server Explorer toocheck for hello presence of hello uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="8b178-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b178-165">Next steps</span></span>

<span data-ttu-id="8b178-166">在此教學課程中，您學會如何 toouse hello 檔案上傳的 IoT 中樞 toosimplify file uploads 從裝置的功能。</span><span class="sxs-lookup"><span data-stu-id="8b178-166">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="8b178-167">您可以繼續 tooexplore IoT 中樞功能和案例以下列發行項的 hello:</span><span class="sxs-lookup"><span data-stu-id="8b178-167">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="8b178-168">[以程式設計方式建立 IoT 中樞][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="8b178-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="8b178-169">[簡介 tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b178-169">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="8b178-170">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="8b178-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="8b178-171">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="8b178-171">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8b178-172">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="8b178-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

[Azure 入口網站]: https://portal.azure.com/

[Azure IoT 開發人員中心]: http://www.azure.com/develop/iot

[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure IoT 服務 SDK 的 NuGet 封裝]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
