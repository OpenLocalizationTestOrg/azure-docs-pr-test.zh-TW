## <a name="create-a-device-identity"></a><span data-ttu-id="fee3d-101">建立裝置識別</span><span class="sxs-lookup"><span data-stu-id="fee3d-101">Create a device identity</span></span>
<span data-ttu-id="fee3d-102">在本節中，您會建立 .NET 主控台應用程式，它會在 IoT 中樞的身分識別登錄中建立裝置識別。</span><span class="sxs-lookup"><span data-stu-id="fee3d-102">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="fee3d-103">裝置無法連線到 IoT 中樞，除非它在身分識別登錄中具有項目。</span><span class="sxs-lookup"><span data-stu-id="fee3d-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="fee3d-104">如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]的＜身分識別登錄＞一節。</span><span class="sxs-lookup"><span data-stu-id="fee3d-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="fee3d-105">執行這個主控台應用程式時，它會產生唯一的裝置識別碼及金鑰，當裝置向 IoT 中樞傳送裝置對雲端訊息時，可以用來識別裝置本身。</span><span class="sxs-lookup"><span data-stu-id="fee3d-105">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span> <span data-ttu-id="fee3d-106">裝置識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="fee3d-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="fee3d-107">在 Visual Studio 中，使用 [主控台應用程式 (.NET Framework)] 專案範本，將 Visual C# Windows 傳統桌面專案新增至新的解決方案。</span><span class="sxs-lookup"><span data-stu-id="fee3d-107">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="fee3d-108">確定 .NET Framework 為 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fee3d-108">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="fee3d-109">將專案命名為 **CreateDeviceIdentity**，將解決方案命名為 **IoTHubGetStarted**。</span><span class="sxs-lookup"><span data-stu-id="fee3d-109">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span></span>
   
    ![新的 Visual C# Windows 傳統桌面專案][10]
2. <span data-ttu-id="fee3d-111">在 [方案總管] 中，以滑鼠右鍵按一下 **CreateDeviceIdentity** 專案，然後按一下 [管理 Nuget 套件]。</span><span class="sxs-lookup"><span data-stu-id="fee3d-111">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="fee3d-112">在 [Nuget 套件管理員] 視窗中選取 [瀏覽]、搜尋 **microsoft.azure.devices**、選取 [安裝] 以安裝 **Microsoft.Azure.Devices** 套件，並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="fee3d-112">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="fee3d-113">此程序會下載及安裝 [Azure IoT 服務 SDK][lnk-nuget-service-sdk] NuGet 套件與其相依項目，並新增對它的參考。</span><span class="sxs-lookup"><span data-stu-id="fee3d-113">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 套件管理員視窗][11]
4. <span data-ttu-id="fee3d-115">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="fee3d-115">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="fee3d-116">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="fee3d-116">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="fee3d-117">將預留位置的值替換為您在上一節中為中樞所建立的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="fee3d-117">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="fee3d-118">將下列方法新增至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="fee3d-118">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="fee3d-119">這個方法會建立具有識別碼 **myFirstDevice**的裝置識別。</span><span class="sxs-lookup"><span data-stu-id="fee3d-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="fee3d-120">(如果該裝置識別碼已經存在身分識別登錄中，程式碼就只會擷取現有的裝置資訊)。接著，應用程式會顯示該身分識別的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="fee3d-120">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="fee3d-121">您會在模擬裝置應用程式中使用此金鑰來連線到您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="fee3d-121">You use this key in the simulated device app to connect to your IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="fee3d-122">最後，將下列幾行新增至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="fee3d-122">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="fee3d-123">執行此應用程式，並記下裝置的金鑰。</span><span class="sxs-lookup"><span data-stu-id="fee3d-123">Run this application, and make a note of the device key.</span></span>
   
    ![應用程式所產生的裝置金鑰][12]

> [!NOTE]
> <span data-ttu-id="fee3d-125">IoT 中樞身分識別登錄只會儲存裝置身分識別，以啟用對 IoT 中樞的安全存取。</span><span class="sxs-lookup"><span data-stu-id="fee3d-125">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="fee3d-126">它會儲存裝置識別碼和金鑰來作為安全性認證，以及啟用或停用旗標，讓您用來停用個別裝置的存取。</span><span class="sxs-lookup"><span data-stu-id="fee3d-126">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="fee3d-127">如果您的應用程式需要儲存其他裝置特定的中繼資料，它應該使用應用程式專用的存放區。</span><span class="sxs-lookup"><span data-stu-id="fee3d-127">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="fee3d-128">如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="fee3d-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
