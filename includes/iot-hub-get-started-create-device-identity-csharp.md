## <a name="create-a-device-identity"></a><span data-ttu-id="61a38-101">建立裝置識別</span><span class="sxs-lookup"><span data-stu-id="61a38-101">Create a device identity</span></span>
<span data-ttu-id="61a38-102">在本節中，您可以建立 IoT 中樞中的 hello 身分識別登錄中建立裝置身分識別的.NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="61a38-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="61a38-103">裝置無法連線 tooIoT 中樞，除非它有 hello 身分識別登錄中的項目。</span><span class="sxs-lookup"><span data-stu-id="61a38-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="61a38-104">如需詳細資訊，請參閱 hello hello 「 身分識別登錄 」 一節[IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="61a38-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="61a38-105">當您執行此主控台應用程式時，它會產生唯一的裝置識別碼，並傳送至雲端的裝置時，您的裝置，可以使用 tooidentify 本身的索引鍵郵件 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="61a38-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="61a38-106">裝置識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="61a38-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="61a38-107">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 tooa 新方案使用 hello**主控台應用程式 (.NET Framework)**專案範本。</span><span class="sxs-lookup"><span data-stu-id="61a38-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="61a38-108">請確定 hello.NET Framework 版本 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="61a38-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="61a38-109">名稱 hello 專案**CreateDeviceIdentity**和名稱 hello 方案**IoTHubGetStarted**。</span><span class="sxs-lookup"><span data-stu-id="61a38-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![新的 Visual C# Windows 傳統桌面專案][10]
2. <span data-ttu-id="61a38-111">在 [方案總管] 中，以滑鼠右鍵按一下 hello **CreateDeviceIdentity**專案，然後再按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="61a38-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="61a38-112">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="61a38-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="61a38-113">此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="61a38-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 封裝管理員視窗][11]
4. <span data-ttu-id="61a38-115">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="61a38-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="61a38-116">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="61a38-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="61a38-117">取代 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="61a38-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="61a38-118">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="61a38-118">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="61a38-119">這個方法會建立具有識別碼 **myFirstDevice**的裝置識別。</span><span class="sxs-lookup"><span data-stu-id="61a38-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="61a38-120">（如果該裝置識別碼已經存在 hello 身分識別登錄中，hello 程式碼只會擷取 hello 現有裝置的資訊。）hello 應用程式接著會顯示為該身分識別的 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="61a38-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="61a38-121">您可以使用這個金鑰在 hello 模擬裝置的應用程式 tooconnect tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="61a38-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="61a38-122">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="61a38-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="61a38-123">執行此應用程式，並記下 hello 裝置金鑰。</span><span class="sxs-lookup"><span data-stu-id="61a38-123">Run this application, and make a note of hello device key.</span></span>
   
    ![裝置 hello 應用程式所產生的金鑰][12]

> [!NOTE]
> <span data-ttu-id="61a38-125">hello IoT 中樞身分識別登錄只會儲存裝置身分識別 tooenable 安全存取 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="61a38-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="61a38-126">它會儲存裝置識別碼和金鑰 toouse 安全性認證，以及您可以針對個別裝置使用 toodisable 存取啟用/停用旗標。</span><span class="sxs-lookup"><span data-stu-id="61a38-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="61a38-127">如果您的應用程式需要 toostore 其他裝置專屬的中繼資料，它應該使用特定應用程式存放區。</span><span class="sxs-lookup"><span data-stu-id="61a38-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="61a38-128">如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="61a38-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
