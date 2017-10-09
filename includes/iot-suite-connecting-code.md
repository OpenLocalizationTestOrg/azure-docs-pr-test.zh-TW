## <a name="specify-hello-behavior-of-hello-iot-device"></a><span data-ttu-id="cca39-101">指定 hello IoT 裝置 hello 的行為</span><span class="sxs-lookup"><span data-stu-id="cca39-101">Specify hello behavior of hello IoT device</span></span>

<span data-ttu-id="cca39-102">hello IoT 中樞序列化程式用戶端程式庫會使用模型 toospecify hello 格式的 hello 訊息 hello 裝置交換與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="cca39-102">hello IoT Hub serializer client library uses a model toospecify hello format of hello messages hello device exchanges with IoT Hub.</span></span>

1. <span data-ttu-id="cca39-103">加入下列變數宣告之後 hello hello`#include`陳述式。</span><span class="sxs-lookup"><span data-stu-id="cca39-103">Add hello following variable declarations after hello `#include` statements.</span></span> <span data-ttu-id="cca39-104">取代 hello 預留位置值 [裝置識別碼] 和 [裝置機碼] 與您記下您的裝置 hello 遠端監視方案儀表板中的值。</span><span class="sxs-lookup"><span data-stu-id="cca39-104">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="cca39-105">使用從 hello 方案儀表板 tooreplace [iot 中樞名稱] 的 hello IoT 中樞的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="cca39-105">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="cca39-106">例如，若您的 IoT 中樞主機名稱是 **contoso.azure-devices.net**，請使用 **contoso** 取代 [IoTHub Name]：</span><span class="sxs-lookup"><span data-stu-id="cca39-106">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. <span data-ttu-id="cca39-107">新增下列程式碼 toodefine hello 模型，可讓與 IoT 中樞 hello 裝置 toocommunicate hello。</span><span class="sxs-lookup"><span data-stu-id="cca39-107">Add hello following code toodefine hello model that enables hello device toocommunicate with IoT Hub.</span></span> <span data-ttu-id="cca39-108">此模型會指定該 hello 裝置：</span><span class="sxs-lookup"><span data-stu-id="cca39-108">This model specifies that hello device:</span></span>

   - <span data-ttu-id="cca39-109">可以傳送溫度、外部溫度、濕度及裝置識別碼作為遙測資料。</span><span class="sxs-lookup"><span data-stu-id="cca39-109">Can send temperature, external temperature, humidity, and a device id as telemetry.</span></span>
   - <span data-ttu-id="cca39-110">可以傳送嗨裝置 tooIoT 中樞的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="cca39-110">Can send metadata about hello device tooIoT Hub.</span></span> <span data-ttu-id="cca39-111">hello 裝置傳送基本中繼資料**DeviceInfo**在啟動時的物件。</span><span class="sxs-lookup"><span data-stu-id="cca39-111">hello device sends basic metadata in a **DeviceInfo** object at startup.</span></span>
   - <span data-ttu-id="cca39-112">可以傳送報告的內容，toohello 裝置的兩個在 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="cca39-112">Can send reported properties, toohello device twin in IoT Hub.</span></span> <span data-ttu-id="cca39-113">這些回報的屬性會依組態、裝置及系統屬性分組。</span><span class="sxs-lookup"><span data-stu-id="cca39-113">These reported properties are grouped into configuration, device, and system properties.</span></span>
   - <span data-ttu-id="cca39-114">可以接收及處理在 IoT 中樞中的 hello 裝置兩個設定所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="cca39-114">Can receive and act on desired properties set in hello device twin in IoT Hub.</span></span>
   - <span data-ttu-id="cca39-115">可以回應 toohello**重新開機**和**InitiateFirmwareUpdate**直接叫用透過 hello 方案入口網站的方法。</span><span class="sxs-lookup"><span data-stu-id="cca39-115">Can respond toohello **Reboot** and **InitiateFirmwareUpdate** direct methods invoked through hello solution portal.</span></span> <span data-ttu-id="cca39-116">hello 裝置傳送它支援使用報告的屬性 hello 直接方法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="cca39-116">hello device sends information about hello direct methods it supports using reported properties.</span></span>
   
    ```c
    // Define hello Model
    BEGIN_NAMESPACE(Contoso);

    /* Reported properties */
    DECLARE_STRUCT(SystemProperties,
      ascii_char_ptr, Manufacturer,
      ascii_char_ptr, FirmwareVersion,
      ascii_char_ptr, InstalledRAM,
      ascii_char_ptr, ModelNumber,
      ascii_char_ptr, Platform,
      ascii_char_ptr, Processor,
      ascii_char_ptr, SerialNumber
    );

    DECLARE_STRUCT(LocationProperties,
      double, Latitude,
      double, Longitude
    );

    DECLARE_STRUCT(ReportedDeviceProperties,
      ascii_char_ptr, DeviceState,
      LocationProperties, Location
    );

    DECLARE_MODEL(ConfigProperties,
      WITH_REPORTED_PROPERTY(double, TemperatureMeanValue),
      WITH_REPORTED_PROPERTY(uint8_t, TelemetryInterval)
    );

    /* Part of DeviceInfo */
    DECLARE_STRUCT(DeviceProperties,
      ascii_char_ptr, DeviceID,
      _Bool, HubEnabledState
    );

    DECLARE_DEVICETWIN_MODEL(Thermostat,
      /* Telemetry (temperature, external temperature and humidity) */
      WITH_DATA(double, Temperature),
      WITH_DATA(double, ExternalTemperature),
      WITH_DATA(double, Humidity),
      WITH_DATA(ascii_char_ptr, DeviceId),

      /* DeviceInfo */
      WITH_DATA(ascii_char_ptr, ObjectType),
      WITH_DATA(_Bool, IsSimulatedDevice),
      WITH_DATA(ascii_char_ptr, Version),
      WITH_DATA(DeviceProperties, DeviceProperties),

      /* Device twin properties */
      WITH_REPORTED_PROPERTY(ReportedDeviceProperties, Device),
      WITH_REPORTED_PROPERTY(ConfigProperties, Config),
      WITH_REPORTED_PROPERTY(SystemProperties, System),

      WITH_DESIRED_PROPERTY(double, TemperatureMeanValue, onDesiredTemperatureMeanValue),
      WITH_DESIRED_PROPERTY(uint8_t, TelemetryInterval, onDesiredTelemetryInterval),

      /* Direct methods implemented by hello device */
      WITH_METHOD(Reboot),
      WITH_METHOD(InitiateFirmwareUpdate, ascii_char_ptr, FwPackageURI),

      /* Register direct methods with solution portal */
      WITH_REPORTED_PROPERTY(ascii_char_ptr_no_quotes, SupportedMethods)
    );

    END_NAMESPACE(Contoso);
    ```

## <a name="implement-hello-behavior-of-hello-device"></a><span data-ttu-id="cca39-117">可實作 hello 裝置 hello 行為</span><span class="sxs-lookup"><span data-stu-id="cca39-117">Implement hello behavior of hello device</span></span>
<span data-ttu-id="cca39-118">現在加入程式碼會實作 hello hello 模型中定義的行為。</span><span class="sxs-lookup"><span data-stu-id="cca39-118">Now add code that implements hello behavior defined in hello model.</span></span>

1. <span data-ttu-id="cca39-119">加入下列函式可處理預期的 hello 屬性設定 hello 方案儀表板中的 hello。</span><span class="sxs-lookup"><span data-stu-id="cca39-119">Add hello following functions that handle hello desired properties set in hello solution dashboard.</span></span> <span data-ttu-id="cca39-120">Hello 模型中定義這些所需的屬性：</span><span class="sxs-lookup"><span data-stu-id="cca39-120">These desired properties are defined in hello model:</span></span>

    ```c
    void onDesiredTemperatureMeanValue(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TemperatureMeanValue = %f\r\n", thermostat->TemperatureMeanValue);

    }

    void onDesiredTelemetryInterval(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TelemetryInterval = %d\r\n", thermostat->TelemetryInterval);
    }
    ```

1. <span data-ttu-id="cca39-121">加入下列函式可處理 hello 直接的方法，透過 hello IoT 中樞叫用的 hello。</span><span class="sxs-lookup"><span data-stu-id="cca39-121">Add hello following functions that handle hello direct methods invoked through hello IoT hub.</span></span> <span data-ttu-id="cca39-122">Hello 模型中定義這些直接的方法：</span><span class="sxs-lookup"><span data-stu-id="cca39-122">These direct methods are defined in hello model:</span></span>

    ```c
    /* Handlers for direct methods */
    METHODRETURN_HANDLE Reboot(Thermostat* thermostat)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Rebooting\"");
      printf("Received reboot request\r\n");
      return result;
    }

    METHODRETURN_HANDLE InitiateFirmwareUpdate(Thermostat* thermostat, ascii_char_ptr FwPackageURI)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Initiating Firmware Update\"");
      printf("Recieved firmware update request. Use package at: %s\r\n", FwPackageURI);
      return result;
    }
    ```

1. <span data-ttu-id="cca39-123">新增下列傳送郵件 toohello 預先設定的解決方案函式的 hello:</span><span class="sxs-lookup"><span data-stu-id="cca39-123">Add hello following function that sends a message toohello preconfigured solution:</span></span>
   
    ```c
    /* Send data tooIoT Hub */
    static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
    {
      IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
      if (messageHandle == NULL)
      {
        printf("unable toocreate a new IoTHubMessage\r\n");
      }
      else
      {
        if (IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, NULL, NULL) != IOTHUB_CLIENT_OK)
        {
          printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
          printf("IoTHubClient accepted hello message for delivery\r\n");
        }

        IoTHubMessage_Destroy(messageHandle);
      }
      free((void*)buffer);
    }
    ```

1. <span data-ttu-id="cca39-124">新增下列 hello 裝置已傳送新的報告的屬性值 toohello 預先設定的方案時執行的回呼處理常式的 hello:</span><span class="sxs-lookup"><span data-stu-id="cca39-124">Add hello following callback handler that runs when hello device has sent new reported property values toohello preconfigured solution:</span></span>

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. <span data-ttu-id="cca39-125">加入下列 hello 函式 tooconnect hello 雲端中您裝置 toohello 預先設定的解決方案，並交換資料。</span><span class="sxs-lookup"><span data-stu-id="cca39-125">Add hello following function tooconnect your device toohello preconfigured solution in hello cloud, and exchange data.</span></span> <span data-ttu-id="cca39-126">此函式會執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cca39-126">This function performs hello following steps:</span></span>

    - <span data-ttu-id="cca39-127">初始化 hello 平台。</span><span class="sxs-lookup"><span data-stu-id="cca39-127">Initializes hello platform.</span></span>
    - <span data-ttu-id="cca39-128">使用 hello 序列化文件庫中註冊 hello Contoso 命名空間。</span><span class="sxs-lookup"><span data-stu-id="cca39-128">Registers hello Contoso namespace with hello serialization library.</span></span>
    - <span data-ttu-id="cca39-129">初始化用戶端 hello hello 裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="cca39-129">Initializes hello client with hello device connection string.</span></span>
    - <span data-ttu-id="cca39-130">建立執行個體的 hello **Thermostat**模型。</span><span class="sxs-lookup"><span data-stu-id="cca39-130">Create an instance of hello **Thermostat** model.</span></span>
    - <span data-ttu-id="cca39-131">建立並傳送回報的屬性值。</span><span class="sxs-lookup"><span data-stu-id="cca39-131">Creates and sends reported property values.</span></span>
    - <span data-ttu-id="cca39-132">傳送 **DeviceInfo** 物件。</span><span class="sxs-lookup"><span data-stu-id="cca39-132">Sends a **DeviceInfo** object.</span></span>
    - <span data-ttu-id="cca39-133">每秒建立迴圈 toosend 遙測。</span><span class="sxs-lookup"><span data-stu-id="cca39-133">Creates a loop toosend telemetry every second.</span></span>
    - <span data-ttu-id="cca39-134">將所有資源取消初始化。</span><span class="sxs-lookup"><span data-stu-id="cca39-134">Deinitializes all resources.</span></span>

      ```c
      void remote_monitoring_run(void)
      {
        if (platform_init() != 0)
        {
          printf("Failed tooinitialize hello platform.\n");
        }
        else
        {
          if (SERIALIZER_REGISTER_NAMESPACE(Contoso) == NULL)
          {
            printf("Unable tooSERIALIZER_REGISTER_NAMESPACE\n");
          }
          else
          {
            IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, MQTT_Protocol);
            if (iotHubClientHandle == NULL)
            {
              printf("Failure in IoTHubClient_CreateFromConnectionString\n");
            }
            else
            {
      #ifdef MBED_BUILD_TIMESTAMP
              // For mbed add hello certificate information
              if (IoTHubClient_SetOption(iotHubClientHandle, "TrustedCerts", certificates) != IOTHUB_CLIENT_OK)
              {
                  printf("Failed tooset option \"TrustedCerts\"\n");
              }
      #endif // MBED_BUILD_TIMESTAMP
              Thermostat* thermostat = IoTHubDeviceTwin_CreateThermostat(iotHubClientHandle);
              if (thermostat == NULL)
              {
                printf("Failure in IoTHubDeviceTwin_CreateThermostat\n");
              }
              else
              {
                /* Set values for reported properties */
                thermostat->Config.TemperatureMeanValue = 55.5;
                thermostat->Config.TelemetryInterval = 3;
                thermostat->Device.DeviceState = "normal";
                thermostat->Device.Location.Latitude = 47.642877;
                thermostat->Device.Location.Longitude = -122.125497;
                thermostat->System.Manufacturer = "Contoso Inc.";
                thermostat->System.FirmwareVersion = "2.22";
                thermostat->System.InstalledRAM = "8 MB";
                thermostat->System.ModelNumber = "DB-14";
                thermostat->System.Platform = "Plat 9.75";
                thermostat->System.Processor = "i3-7";
                thermostat->System.SerialNumber = "SER21";
                /* Specify hello signatures of hello supported direct methods */
                thermostat->SupportedMethods = "{\"Reboot\": \"Reboot hello device\", \"InitiateFirmwareUpdate--FwPackageURI-string\": \"Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file\"}";

                /* Send reported properties tooIoT Hub */
                if (IoTHubDeviceTwin_SendReportedStateThermostat(thermostat, deviceTwinCallback, NULL) != IOTHUB_CLIENT_OK)
                {
                  printf("Failed sending serialized reported state\n");
                }
                else
                {
                  printf("Send DeviceInfo object tooIoT Hub at startup\n");
      
                  thermostat->ObjectType = "DeviceInfo";
                  thermostat->IsSimulatedDevice = 0;
                  thermostat->Version = "1.0";
                  thermostat->DeviceProperties.HubEnabledState = 1;
                  thermostat->DeviceProperties.DeviceID = (char*)deviceId;

                  unsigned char* buffer;
                  size_t bufferSize;

                  if (SERIALIZE(&buffer, &bufferSize, thermostat->ObjectType, thermostat->Version, thermostat->IsSimulatedDevice, thermostat->DeviceProperties) != CODEFIRST_OK)
                  {
                    (void)printf("Failed serializing DeviceInfo\n");
                  }
                  else
                  {
                    sendMessage(iotHubClientHandle, buffer, bufferSize);
                  }

                  /* Send telemetry */
                  thermostat->Temperature = 50;
                  thermostat->ExternalTemperature = 55;
                  thermostat->Humidity = 50;
                  thermostat->DeviceId = (char*)deviceId;

                  while (1)
                  {
                    unsigned char*buffer;
                    size_t bufferSize;

                    (void)printf("Sending sensor value Temperature = %f, Humidity = %f\n", thermostat->Temperature, thermostat->Humidity);

                    if (SERIALIZE(&buffer, &bufferSize, thermostat->DeviceId, thermostat->Temperature, thermostat->Humidity, thermostat->ExternalTemperature) != CODEFIRST_OK)
                    {
                      (void)printf("Failed sending sensor value\r\n");
                    }
                    else
                    {
                      sendMessage(iotHubClientHandle, buffer, bufferSize);
                    }

                    ThreadAPI_Sleep(1000);
                  }

                  IoTHubDeviceTwin_DestroyThermostat(thermostat);
                }
              }
              IoTHubClient_Destroy(iotHubClientHandle);
            }
            serializer_deinit();
          }
        }
        platform_deinit();
      }
    ```
   
    <span data-ttu-id="cca39-135">如需參考，以下是範例**遙測**傳送訊息 toohello 預先設定的方案：</span><span class="sxs-lookup"><span data-stu-id="cca39-135">For reference, here is a sample **Telemetry** message sent toohello preconfigured solution:</span></span>
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```