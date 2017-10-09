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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a>從您的裝置 toohello 雲端的檔案上傳與使用適用於.NET 的 IoT 中樞

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

本教學課程是 hello 程式碼在 hello[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-csharp-csharp-c2d.md)教學課程 tooshow 您 toouse hello 的 IoT 中樞的檔案上傳功能的方式。 這會說明如何：

- 安全地將 Azure Blob URI 提供給裝置，以便上傳檔案。
- 使用 hello IoT 中樞檔案上傳通知 tootrigger 處理您的應用程式後端中的 hello 檔案。

hello[開始使用 IoT 中樞](iot-hub-csharp-csharp-getstarted.md)和[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-csharp-csharp-c2d.md)教學課程示範 hello 基本裝置到雲端 」 和 「 雲端到裝置訊息功能的 IoT 中樞。 hello[程序裝置到雲端訊息](iot-hub-csharp-csharp-process-d2c.md)教學課程描述方式 tooreliably 將裝置到雲端訊息儲存在 Azure blob 儲存體。 不過，在某些情況下您無法輕鬆地 hello 資料對應您的裝置傳送到 hello 相對較小裝置到雲端 IoT 中樞所接受訊息。 例如：

* 包含映像的大型檔案
* 影片
* 取樣高頻率的震動資料
* 某種經前置處理過的資料

這些檔案通常是使用類似的 hello 雲端中處理的批次[Azure Data Factory](../data-factory/index.md)或 hello [Hadoop](../hdinsight/index.md)堆疊。 當您需要從裝置 tooupload 檔案時，您仍然可以使用 hello 安全性和可靠性的 IoT 中樞。

在本教學課程中的 hello 結尾，您會執行兩個.NET 主控台應用程式：

* **SimulatedDevice**，hello hello 中建立的應用程式的修改的版本[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-csharp-csharp-c2d.md)教學課程。 此應用程式上傳檔案 toostorage 使用提供的 IoT 中樞的 SAS URI。
* **ReadFileUploadNotification**，它會接收來自 IoT 中樞的檔案上傳通知。

> [!NOTE]
> IoT 中樞透過 Azure IoT 裝置 SDK 來支援許多裝置平台和語言 (包括 C、Java 及 Javascript)。 請參閱 toohello [Azure IoT 開發人員中心]的逐步指示 tooconnect 您裝置 tooAzure IoT 中樞。

toocomplete 本教學課程中，您需要遵循的 hello:

* Visual Studio 2015 或 Visual Studio 2017
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>從裝置應用程式上傳檔案

在本節中，您將修改 hello 裝置應用程式中建立[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-csharp-csharp-c2d.md)tooreceive 雲端到裝置訊息從 hello IoT 中樞。

1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello **SimulatedDevice**專案中，按一下 **新增**，然後按一下**現有項目**。 瀏覽 tooan 映像檔，並將它包含在您的專案。 本教學課程會假設名為 hello 映像`image.jpg`。

1. Hello 影像上按一下滑鼠右鍵，然後按一下**屬性**。 請確定**複製 tooOutput 目錄**設定得**永遠複製**。

    ![][1]

1. 在 hello **Program.cs**檔案中加入下列陳述式在 hello hello 檔案最上方的 hello:

    ```csharp
    using System.IO;
    ```

1. 新增下列方法 toohello hello**程式**類別：

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

    hello`UploadToBlobAsync`方法會在 hello 檔案名稱和資料流來源的 hello 檔案 toobe 上傳和控制代碼 hello 上載 toostorage。 hello 主控台應用程式會顯示 hello tooupload hello 檔案所花費的時間。

1. 新增下列方法在 hello hello **Main**方法中的前 hello,`Console.ReadLine()`行：

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> 為了簡單起見，本教學課程不會實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理]。

## <a name="receive-a-file-upload-notification"></a>接收檔案上傳通知

在本節中，您將撰寫 .NET 主控台應用程式，以接收來自 IoT 中樞的檔案上傳通知訊息。

1. Hello 目前 Visual Studio 方案中建立 Visual C# Windows 專案使用 hello**主控台應用程式**專案範本。 名稱 hello 專案**ReadFileUploadNotification**。

    ![Visual Studio 中的新專案][2]

1. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **ReadFileUploadNotification**專案，然後再按一下**管理 NuGet 封裝...**.

1. 在 hello **NuGet 套件管理員**視窗中，搜尋**Microsoft.Azure.Devices**，按一下 **安裝**，並接受使用規定 hello。

    這個動作會下載、 安裝，並將參考 toohello [Azure IoT 服務 SDK 的 NuGet 封裝]在 hello **ReadFileUploadNotification**專案。

1. 在 hello **Program.cs**檔案中加入下列陳述式在 hello hello 檔案最上方的 hello:

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. 新增下列欄位 toohello hello**程式**類別。 替代 hello 預留位置的值與 hello IoT 中樞連接字串從 [開始使用 IoT 中樞]:

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. 新增下列方法 toohello hello**程式**類別：

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

    請注意此接收模式是 hello hello 裝置應用程式來自相同一個使用的 tooreceive 雲端到裝置訊息。

1. 最後，加入下列行 toohello hello **Main**方法：

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>執行 hello 應用程式

現在您已準備好 toorun hello 應用程式。

1. 在 Visual Studio 中，在您的方案上按一下滑鼠右鍵，然後選取 [設定啟始專案]。 選取**多個啟始專案**，然後選取 hello**啟動**動作**ReadFileUploadNotification**和**SimulatedDevice**。

1. 按 **F5**。 這兩個應用程式應該都會啟動。 您應該會看到一個主控台應用程式中的 hello 上傳完成，而且所收到 hello 上傳通知訊息 hello 其他主控台應用程式。 您可以使用 hello [Azure 入口網站]或 Visual Studio 伺服器總管 toocheck hello hello 存在上傳您的 Azure 儲存體帳戶中的檔案。

    ![][50]

## <a name="next-steps"></a>後續步驟

在此教學課程中，您學會如何 toouse hello 檔案上傳的 IoT 中樞 toosimplify file uploads 從裝置的功能。 您可以繼續 tooexplore IoT 中樞功能和案例以下列發行項的 hello:

* [以程式設計方式建立 IoT 中樞][lnk-create-hub]
* [簡介 tooC SDK][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [使用 IoT Edge 來模擬裝置][lnk-iotedge]

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
