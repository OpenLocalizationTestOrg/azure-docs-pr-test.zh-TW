## <a name="specify-the-behavior-of-the-iot-device"></a><span data-ttu-id="31029-101">指定 IoT 裝置的行為</span><span class="sxs-lookup"><span data-stu-id="31029-101">Specify the behavior of the IoT device</span></span>

<span data-ttu-id="31029-102">IoT 中樞序列化程式用戶端程式庫會使用模型來指定裝置與 IoT 中樞交換之訊息的格式。</span><span class="sxs-lookup"><span data-stu-id="31029-102">The IoT Hub serializer client library uses a model to specify the format of the messages the device exchanges with IoT Hub.</span></span>

1. <span data-ttu-id="31029-103">在 `#include` 陳述式之後新增下列變數宣告。</span><span class="sxs-lookup"><span data-stu-id="31029-103">Add the following variable declarations after the `#include` statements.</span></span> <span data-ttu-id="31029-104">使用您在遠端監視解決方案儀表板中為裝置記下的值來取代 [Device Id] 和 [Device Key] 預留位置值。</span><span class="sxs-lookup"><span data-stu-id="31029-104">Replace the placeholder values [Device Id] and [Device Key] with values you noted for your device in the remote monitoring solution dashboard.</span></span> <span data-ttu-id="31029-105">使用解決方案儀表板中的「IoT 中樞主機名稱」來取代 [IoTHub Name]。</span><span class="sxs-lookup"><span data-stu-id="31029-105">Use the IoT Hub Hostname from the solution dashboard to replace [IoTHub Name].</span></span> <span data-ttu-id="31029-106">例如，若您的 IoT 中樞主機名稱是 **contoso.azure-devices.net**，請使用 **contoso** 取代 [IoTHub Name]：</span><span class="sxs-lookup"><span data-stu-id="31029-106">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. <span data-ttu-id="31029-107">新增下列程式碼以定義可讓裝置與 IoT 中樞通訊的模型。</span><span class="sxs-lookup"><span data-stu-id="31029-107">Add the following code to define the model that enables the device to communicate with IoT Hub.</span></span> <span data-ttu-id="31029-108">此模型會指定裝置：</span><span class="sxs-lookup"><span data-stu-id="31029-108">This model specifies that the device:</span></span>

   - <span data-ttu-id="31029-109">可以傳送溫度、外部溫度、濕度及裝置識別碼作為遙測資料。</span><span class="sxs-lookup"><span data-stu-id="31029-109">Can send temperature, external temperature, humidity, and a device id as telemetry.</span></span>
   - <span data-ttu-id="31029-110">可以將裝置相關中繼資料傳送給 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="31029-110">Can send metadata about the device to IoT Hub.</span></span> <span data-ttu-id="31029-111">裝置會在啟動時傳送 **DeviceInfo** 物件中的基本中繼資料。</span><span class="sxs-lookup"><span data-stu-id="31029-111">The device sends basic metadata in a **DeviceInfo** object at startup.</span></span>
   - <span data-ttu-id="31029-112">可以將回報的屬性傳送給 IoT 中樞內的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="31029-112">Can send reported properties, to the device twin in IoT Hub.</span></span> <span data-ttu-id="31029-113">這些回報的屬性會依組態、裝置及系統屬性分組。</span><span class="sxs-lookup"><span data-stu-id="31029-113">These reported properties are grouped into configuration, device, and system properties.</span></span>
   - <span data-ttu-id="31029-114">可以接收 IoT 中樞內裝置對應項中設定的所需屬性，並根據這些屬性採取動作。</span><span class="sxs-lookup"><span data-stu-id="31029-114">Can receive and act on desired properties set in the device twin in IoT Hub.</span></span>
   - <span data-ttu-id="31029-115">可以回應透過解決方案入口網站叫用的 **Reboot** 和 **InitiateFirmwareUpdate** 直接方法。</span><span class="sxs-lookup"><span data-stu-id="31029-115">Can respond to the **Reboot** and **InitiateFirmwareUpdate** direct methods invoked through the solution portal.</span></span> <span data-ttu-id="31029-116">裝置會使用回報的屬性來傳送它所支援之直接方法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="31029-116">The device sends information about the direct methods it supports using reported properties.</span></span>
   
    ```c
    // Define the Model
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

      /* Direct methods implemented by the device */
      WITH_METHOD(Reboot),
      WITH_METHOD(InitiateFirmwareUpdate, ascii_char_ptr, FwPackageURI),

      /* Register direct methods with solution portal */
      WITH_REPORTED_PROPERTY(ascii_char_ptr_no_quotes, SupportedMethods)
    );

    END_NAMESPACE(Contoso);
    ```

## <a name="implement-the-behavior-of-the-device"></a><span data-ttu-id="31029-117">實作裝置的行為</span><span class="sxs-lookup"><span data-stu-id="31029-117">Implement the behavior of the device</span></span>
<span data-ttu-id="31029-118">現在，請新增程式碼來實作模型中所定義的行為。</span><span class="sxs-lookup"><span data-stu-id="31029-118">Now add code that implements the behavior defined in the model.</span></span>

1. <span data-ttu-id="31029-119">新增下列函式，這些函式會處理在解決方案儀表板中設定的所需屬性。</span><span class="sxs-lookup"><span data-stu-id="31029-119">Add the following functions that handle the desired properties set in the solution dashboard.</span></span> <span data-ttu-id="31029-120">這些所需屬性是在模型中定義：</span><span class="sxs-lookup"><span data-stu-id="31029-120">These desired properties are defined in the model:</span></span>

    ```c
    void onDesiredTemperatureMeanValue(void* argument)
    {
      /* By convention 'argument' is of the type of the MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TemperatureMeanValue = %f\r\n", thermostat->TemperatureMeanValue);

    }

    void onDesiredTelemetryInterval(void* argument)
    {
      /* By convention 'argument' is of the type of the MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TelemetryInterval = %d\r\n", thermostat->TelemetryInterval);
    }
    ```

1. <span data-ttu-id="31029-121">新增下列函式，這些函式會處理透過 IoT 中樞叫用的直接方法。</span><span class="sxs-lookup"><span data-stu-id="31029-121">Add the following functions that handle the direct methods invoked through the IoT hub.</span></span> <span data-ttu-id="31029-122">這些直接方法是在模型中定義：</span><span class="sxs-lookup"><span data-stu-id="31029-122">These direct methods are defined in the model:</span></span>

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

1. <span data-ttu-id="31029-123">新增下列函式，此函式會傳送訊息給預先設定的解決方案：</span><span class="sxs-lookup"><span data-stu-id="31029-123">Add the following function that sends a message to the preconfigured solution:</span></span>
   
    ```c
    /* Send data to IoT Hub */
    static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
    {
      IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
      if (messageHandle == NULL)
      {
        printf("unable to create a new IoTHubMessage\r\n");
      }
      else
      {
        if (IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, NULL, NULL) != IOTHUB_CLIENT_OK)
        {
          printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
          printf("IoTHubClient accepted the message for delivery\r\n");
        }

        IoTHubMessage_Destroy(messageHandle);
      }
      free((void*)buffer);
    }
    ```

1. <span data-ttu-id="31029-124">新增下列回呼處理常式，此處理常式會在裝置將新回報的屬性值傳送給預先設定的解決方案後執行：</span><span class="sxs-lookup"><span data-stu-id="31029-124">Add the following callback handler that runs when the device has sent new reported property values to the preconfigured solution:</span></span>

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. <span data-ttu-id="31029-125">新增下列函式，以將您的裝置連接到雲端中的預先設定解決方案，然後交換資料。</span><span class="sxs-lookup"><span data-stu-id="31029-125">Add the following function to connect your device to the preconfigured solution in the cloud, and exchange data.</span></span> <span data-ttu-id="31029-126">此函式會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="31029-126">This function performs the following steps:</span></span>

    - <span data-ttu-id="31029-127">將平台初始化。</span><span class="sxs-lookup"><span data-stu-id="31029-127">Initializes the platform.</span></span>
    - <span data-ttu-id="31029-128">使用序列化程式庫來註冊 Contoso 命名空間。</span><span class="sxs-lookup"><span data-stu-id="31029-128">Registers the Contoso namespace with the serialization library.</span></span>
    - <span data-ttu-id="31029-129">使用裝置連接字串將用戶端初始化。</span><span class="sxs-lookup"><span data-stu-id="31029-129">Initializes the client with the device connection string.</span></span>
    - <span data-ttu-id="31029-130">建立「控溫器」模型的執行個體。</span><span class="sxs-lookup"><span data-stu-id="31029-130">Create an instance of the **Thermostat** model.</span></span>
    - <span data-ttu-id="31029-131">建立並傳送回報的屬性值。</span><span class="sxs-lookup"><span data-stu-id="31029-131">Creates and sends reported property values.</span></span>
    - <span data-ttu-id="31029-132">傳送 **DeviceInfo** 物件。</span><span class="sxs-lookup"><span data-stu-id="31029-132">Sends a **DeviceInfo** object.</span></span>
    - <span data-ttu-id="31029-133">建立迴圈來每秒傳送遙測資料。</span><span class="sxs-lookup"><span data-stu-id="31029-133">Creates a loop to send telemetry every second.</span></span>
    - <span data-ttu-id="31029-134">將所有資源取消初始化。</span><span class="sxs-lookup"><span data-stu-id="31029-134">Deinitializes all resources.</span></span>

      ```c
      void remote_monitoring_run(void)
      {
        if (platform_init() != 0)
        {
          printf("Failed to initialize the platform.\n");
        }
        else
        {
          if (SERIALIZER_REGISTER_NAMESPACE(Contoso) == NULL)
          {
            printf("Unable to SERIALIZER_REGISTER_NAMESPACE\n");
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
              // For mbed add the certificate information
              if (IoTHubClient_SetOption(iotHubClientHandle, "TrustedCerts", certificates) != IOTHUB_CLIENT_OK)
              {
                  printf("Failed to set option \"TrustedCerts\"\n");
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
                /* Specify the signatures of the supported direct methods */
                thermostat->SupportedMethods = "{\"Reboot\": \"Reboot the device\", \"InitiateFirmwareUpdate--FwPackageURI-string\": \"Updates device Firmware. Use parameter FwPackageURI to specifiy the URI of the firmware file\"}";

                /* Send reported properties to IoT Hub */
                if (IoTHubDeviceTwin_SendReportedStateThermostat(thermostat, deviceTwinCallback, NULL) != IOTHUB_CLIENT_OK)
                {
                  printf("Failed sending serialized reported state\n");
                }
                else
                {
                  printf("Send DeviceInfo object to IoT Hub at startup\n");
      
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
   
    <span data-ttu-id="31029-135">以下是一個傳送給預先設定之解決方案的範例「遙測」訊息，可供您參考：</span><span class="sxs-lookup"><span data-stu-id="31029-135">For reference, here is a sample **Telemetry** message sent to the preconfigured solution:</span></span>
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```