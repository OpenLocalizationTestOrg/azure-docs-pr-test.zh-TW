## <a name="create-a-device-identity"></a>建立裝置識別
在本節中，您可以建立 IoT 中樞中的 hello 身分識別登錄中建立裝置身分識別的.NET 主控台應用程式。 裝置無法連線 tooIoT 中樞，除非它有 hello 身分識別登錄中的項目。 如需詳細資訊，請參閱 hello hello 「 身分識別登錄 」 一節[IoT 中樞開發人員指南][lnk-devguide-identity]。 當您執行此主控台應用程式時，它會產生唯一的裝置識別碼，並傳送至雲端的裝置時，您的裝置，可以使用 tooidentify 本身的索引鍵郵件 tooIoT 中樞。 裝置識別碼會區分大小寫。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 tooa 新方案使用 hello**主控台應用程式 (.NET Framework)**專案範本。 請確定 hello.NET Framework 版本 4.5.1 或更新版本。 名稱 hello 專案**CreateDeviceIdentity**和名稱 hello 方案**IoTHubGetStarted**。
   
    ![新的 Visual C# Windows 傳統桌面專案][10]
2. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **CreateDeviceIdentity**專案，然後再按一下**管理 NuGet 封裝**。
3. 在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。 此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。
   
    ![NuGet 封裝管理員視窗][11]
4. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. 新增下列欄位 toohello hello**程式**類別。 取代 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. 新增下列方法 toohello hello**程式**類別：
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    這個方法會建立具有識別碼 **myFirstDevice**的裝置識別。 （如果該裝置識別碼已經存在 hello 身分識別登錄中，hello 程式碼只會擷取 hello 現有裝置的資訊。）hello 應用程式接著會顯示為該身分識別的 hello 主索引鍵。 您可以使用這個金鑰在 hello 模擬裝置的應用程式 tooconnect tooyour IoT 中樞。
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. 最後，加入下列行 toohello hello **Main**方法：
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. 執行此應用程式，並記下 hello 裝置金鑰。
   
    ![裝置 hello 應用程式所產生的金鑰][12]

> [!NOTE]
> hello IoT 中樞身分識別登錄只會儲存裝置身分識別 tooenable 安全存取 toohello IoT 中樞。 它會儲存裝置識別碼和金鑰 toouse 安全性認證，以及您可以針對個別裝置使用 toodisable 存取啟用/停用旗標。 如果您的應用程式需要 toostore 其他裝置專屬的中繼資料，它應該使用特定應用程式存放區。 如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]。
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
