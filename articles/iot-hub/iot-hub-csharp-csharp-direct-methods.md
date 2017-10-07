---
title: "Azure IoT 中樞 aaaUse 直接方法 (.NET/.NET) |Microsoft 文件"
description: "如何 toouse Azure IoT 中樞直接的方法。 您可以使用 hello Azure IoT 裝置 SDK for.NET tooimplement 模擬的裝置應用程式，其中包含直接的方法和 hello Azure IoT 服務 SDK for.NET tooimplement hello 直接的方法會叫用的服務應用程式。"
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a>使用直接方法 (.NET/.NET)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

在本教學課程中，我們會持續 toodevelop 兩個.NET 主控台應用程式：

* **CallMethodOnDevice**後, 端應用程式，會呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。
* **SimulateDeviceMethods**，主控台應用程式的模擬連接 tooyour IoT 中樞與 hello 稍早建立的裝置身分識別的裝置，以及回應 hello 雲端呼叫 toohello 方法。

> [!NOTE]
> hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 這兩個應用程式 toorun 裝置和您的方案後端上。
> 
> 

toocomplete 本教學課程中，您需要：

* Visual Studio 2015 或 Visual Studio 2017。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

如果您想 toocreate hello 裝置身分識別以程式設計方式相反地，讀取 hello 對應的章節 hello[連接您使用適用於.NET 的模擬的裝置 tooyour IoT 中樞][ lnk-device-identity-csharp]發行項。


## <a name="create-a-simulated-device-app"></a>建立模擬裝置應用程式
在本節中，您可以建立回應 hello 方案回呼叫端的 tooa 方法 .NET 主控台應用程式。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。 名稱 hello 專案**SimulateDeviceMethods**。
   
    ![新的 Visual C# Windows 傳統裝置應用程式][img-createdeviceapp]
    
1. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **SimulateDeviceMethods**專案，然後再按一下**管理 NuGet 封裝...**.
1. 在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**並搜尋**microsoft.azure.devices.client**。 選取**安裝**tooinstall hello **Microsoft.Azure.Devices.Client**封裝，並接受使用規定 hello。 此程序下載、 安裝，並新增參考 toohello [Azure IoT 裝置 SDK] [ lnk-nuget-client-sdk] NuGet 封裝和其相依性。
   
    ![NuGet 套件管理員視窗用戶端應用程式][img-clientnuget]
1. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. 新增下列欄位 toohello hello**程式**類別。 取代您記下 hello 前一節中的 hello 裝置連接字串中的 hello 預留位置的值。
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. 新增下列 tooimplement hello 直接方法 hello 裝置上的 hello:

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. 最後，加入下列程式碼 toohello hello **Main**方法 tooopen hello 連接 tooyour IoT 中樞和初始化 hello 方法接聽程式：
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. 在 hello Visual Studio 方案總管]，以滑鼠右鍵按一下您的方案，然後按一下**設定啟始專案...**.選取**單一啟始專案**，然後選取 [hello **SimulateDeviceMethods** hello 下拉式功能表中的專案。        

> [!NOTE]
> 簡單 tookeep 方面，本教學課程未實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如連線重試），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>在裝置上呼叫直接方法
在本節中，您可以建立.NET 主控台應用程式會呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。 請確定 hello.NET Framework 版本 4.5.1 或更新版本。 名稱 hello 專案**CallMethodOnDevice**。
   
    ![新的 Visual C# Windows 傳統桌面專案][img-createserviceapp]
2. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **CallMethodOnDevice**專案，然後再按一下**管理 NuGet 封裝...**.
3. 在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。 此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。
   
    ![NuGet 封裝管理員視窗][img-servicenuget]

4. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. 新增下列欄位 toohello hello**程式**類別。 取代 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. 新增下列方法 toohello hello**程式**類別：
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    這個方法會叫用具有名稱的直接方法`writeLine`上 hello`myDeviceId`裝置。 然後，它會寫入 hello 回應 hello 裝置 hello 主控台上所提供。 請注意如何可能 toospecify hello 裝置 toorespond 的逾時值。
7. 最後，加入下列行 toohello hello **Main**方法：
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. 在 hello Visual Studio 方案總管]，以滑鼠右鍵按一下您的方案，然後按一下**設定啟始專案...**.選取**單一啟始專案**，然後選取 [hello **CallMethodOnDevice** hello 下拉式功能表中的專案。

## <a name="run-hello-applications"></a>執行 hello 應用程式
現在您已經準備就緒 toorun hello 應用程式。

1. 執行 hello.NET 裝置的應用程式**SimulateDeviceMethods**。 它應該會開始接聽來自 IoT 中樞的方法呼叫： 

    ![裝置應用程式已執行][img-deviceapprun]
1. 現在該 hello 裝置連線，並等候方法叫用時，執行 hello.NET **CallMethodOnDevice** hello 模擬的裝置應用程式中的應用程式 tooinvoke hello 方法。 您應該會看到寫入 hello 主控台中的 hello 裝置回應。
   
    ![裝置應用程式已執行][img-serviceapprun]
1. hello 裝置然後反應 toohello 方法列印此訊息：
   
    ![直接在 hello 裝置上叫用的方法][img-directmethodinvoked]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。 您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 tooreact toomethods hello 雲端所叫用。 您也會建立叫用 hello 裝置上的方法，並會顯示 hello 回應 hello 裝置的應用程式。 

使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：

* [IoT 中心入門]
* [排程多個裝置上的作業][lnk-devguide-jobs]

toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[IoT 中心入門]: iot-hub-node-node-getstarted.md
