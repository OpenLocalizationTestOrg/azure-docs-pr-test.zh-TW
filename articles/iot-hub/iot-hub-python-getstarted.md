---
title: "aaaGet 開始使用 Azure IoT 中樞 (Python) |Microsoft 文件"
description: "了解如何 toosend 裝置到雲端訊息 tooAzure 使用 IoT Sdk for Python 的 IoT 中樞。 建立模擬的裝置和服務應用程式 tooregister 您的裝置、 傳送訊息，以及從 IoT 中樞讀取訊息。"
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="3ae5a-104">連接使用 Python 您模擬的裝置 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="3ae5a-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="3ae5a-105">在本教學課程的 hello 結束時，您將擁有兩個的 Python 應用程式：</span><span class="sxs-lookup"><span data-stu-id="3ae5a-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="3ae5a-106">**CreateDeviceIdentity.py**，這樣就可以建立裝置身分識別，以及相關聯的安全性金鑰 tooconnect 應用程式模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="3ae5a-107">**SimulatedDevice.py**、 tooyour IoT 中樞連線以稍早建立的 hello 裝置身分識別，並定期傳送遙測訊息使用 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="3ae5a-108">hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 這兩個應用程式 toorun 裝置和您的方案後端上。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="3ae5a-109">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="3ae5a-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="3ae5a-110">[Python 2.x 或 3.x][lnk-python-download]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="3ae5a-111">請確定 toouse hello 32 位元或 64 位元安裝所需的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="3ae5a-112">出現提示時 hello 安裝期間，請確定 tooadd Python tooyour 平台專屬環境變數。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="3ae5a-113">如果您使用 Python 2.x，您可能需要過[安裝或升級*pip*，hello Python 封裝管理系統][lnk-install-pip]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="3ae5a-114">如果您使用 Windows 作業系統，然後[Visual c + + 可轉散發套件][ lnk-visual-c-redist] tooallow hello 使用來自 Python 的原生 Dll。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="3ae5a-115">[Node.js 4.0 或更新版本][lnk-node-download]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="3ae5a-116">請確定 toouse hello 32 位元或 64 位元安裝所需的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="3ae5a-117">這是所需的 tooinstall hello [IoT 中樞總管工具][lnk-iot-hub-explorer]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="3ae5a-118">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-118">An active Azure account.</span></span> <span data-ttu-id="3ae5a-119">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="3ae5a-120">hello *pip*封裝的`azure-iothub-service-client`和`azure-iothub-device-client`目前僅適用於 Windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="3ae5a-121">Linux/Mac OS，請參閱 toohello Linux 和 Mac OS 特定章節 hello[準備開發環境的 Python] [ lnk-python-devbox]文章。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="3ae5a-122">您現在已經建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-122">You have now created your IoT hub.</span></span> <span data-ttu-id="3ae5a-123">在本教學課程的 hello 其餘部分使用 hello IoT 中樞的主機名稱與 hello IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="3ae5a-124">您可以輕鬆建立 IoT 中樞命令列上使用 hello Python 或 Node.js 基礎 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="3ae5a-125">hello 文章[建立 IoT 中心使用 hello Azure CLI 2.0] [ lnk-azure-cli-hub]您因此 hello toodo 快速步驟所示。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="3ae5a-126">建立裝置識別</span><span class="sxs-lookup"><span data-stu-id="3ae5a-126">Create a device identity</span></span>
<span data-ttu-id="3ae5a-127">此區段會列出 hello 步驟 toocreate Python 主控台應用程式，您的 IoT 中樞 hello 身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="3ae5a-128">如果其中有傳送 hello 身分識別登錄中的裝置只能連接 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="3ae5a-129">如需詳細資訊，請參閱 hello**身分識別登錄**區段 hello [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="3ae5a-130">當您執行此主控台應用程式時，它會產生唯一的裝置識別碼，並傳送至雲端的裝置時，您的裝置，可以使用 tooidentify 本身的索引鍵郵件 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="3ae5a-131">開啟命令提示字元，並安裝 hello **Azure IoT 中樞服務 SDK for Python**。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="3ae5a-132">在您安裝 hello SDK 之後，請關閉 hello 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="3ae5a-133">建立名為 **CreateDeviceIdentity.py** 的 Python 檔案。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="3ae5a-134">在中開啟它[Python 編輯器/IDE 您選擇的][lnk-python-ide-list]，比方說，hello 預設[閒置][lnk-idle]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="3ae5a-135">新增 hello hello 服務 SDK 中的下列程式碼 tooimport hello 所需的模組：</span><span class="sxs-lookup"><span data-stu-id="3ae5a-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="3ae5a-136">新增下列程式碼、 取代 hello 預留位置 hello `[IoTHub Connection String]` hello hello IoT 中樞，您在 hello 上一節中建立的連接字串。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="3ae5a-137">您可以使用任何名稱為 hello `DEVICE_ID`。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="3ae5a-138">新增 hello 下列函式 tooprint hello 裝置資訊的某些部分。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-138">Add hello following function tooprint some of hello device information.</span></span>

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. <span data-ttu-id="3ae5a-139">新增下列使用 hello 登錄管理員函式 toocreate hello 裝置識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. <span data-ttu-id="3ae5a-140">最後，新增 hello main 函式，如下所示，並儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-140">Finally, add hello main function as follows and save hello file.</span></span>

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. <span data-ttu-id="3ae5a-141">Hello 命令提示字元處執行 hello **CreateDeviceIdentity.py** ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3ae5a-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="3ae5a-142">您應該會看到 hello 取得建立模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="3ae5a-143">記下 hello **deviceId**和 hello **primaryKey**此裝置。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="3ae5a-144">您需要這些值稍後當您建立連線 tooIoT 中樞為裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![成功建立裝置][1]

> [!NOTE]
> <span data-ttu-id="3ae5a-146">hello IoT 中樞身分識別登錄只會儲存裝置身分識別 tooenable 安全存取 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="3ae5a-147">它會儲存裝置識別碼和金鑰 toouse 安全性認證以及啟用/停用旗標，您可以使用 toodisable 存取個別的裝置。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="3ae5a-148">如果您的應用程式需要 toostore 其他裝置專屬的中繼資料，它應該使用特定應用程式存放區。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="3ae5a-149">如需詳細資訊，請參閱 hello [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="3ae5a-150">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="3ae5a-150">Create a simulated device app</span></span>
<span data-ttu-id="3ae5a-151">此區段會列出 hello 步驟 toocreate Python 主控台應用程式，可模擬裝置，並將傳送裝置到雲端訊息 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="3ae5a-152">開啟新的命令提示字元，並安裝 hello Azure IoT 中樞裝置 SDK for Python 如下。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="3ae5a-153">關閉 hello hello 安裝後的命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="3ae5a-154">建立名為 **SimulatedDevice.py** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="3ae5a-155">在您所選的 Python 編輯器/IDE (例如 IDLE) 中開啟此檔案。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="3ae5a-156">新增 hello hello 裝置 SDK 中的下列程式碼 tooimport hello 所需的模組。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="3ae5a-157">新增 hello 下列程式碼，並取代 hello 預留位置`[IoTHub Device Connection String]`與您的裝置 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="3ae5a-158">hello 裝置連接字串中的 hello 格式通常是`HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="3ae5a-159">使用 hello **deviceId**和**primaryKey** hello 裝置，您在前一個區段 tooreplace hello hello 中建立的`<deviceId>`和`<primaryKey>`分別。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="3ae5a-160">使用 IoT 中樞的主機名稱 (通常為 `<IoT hub name>.azure-devices.net`) 取代 `<hostName>`。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. <span data-ttu-id="3ae5a-161">新增下列程式碼 toodefine 傳送確認回呼 hello。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-161">Add hello following code toodefine a send confirmation callback.</span></span> 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. <span data-ttu-id="3ae5a-162">新增下列程式碼 tooinitialize hello 裝置用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="3ae5a-163">加入下列 hello 函式 tooformat，並從模擬的裝置 tooyour IoT 中樞將訊息傳送。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. <span data-ttu-id="3ae5a-164">最後，加入 hello main 函式。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="3ae5a-165">儲存並關閉 hello **SimulatedDevice.py**檔案。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="3ae5a-166">您會立即準備 toorun 此應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="3ae5a-167">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="3ae5a-168">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="3ae5a-169">從模擬裝置接收訊息</span><span class="sxs-lookup"><span data-stu-id="3ae5a-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="3ae5a-170">tooreceive 遙測訊息從您的裝置，您需要 toouse[事件中心][lnk-event-hubs-overview]-相容 hello IoT 中樞，讀取 hello 裝置到雲端訊息所公開的端點。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="3ae5a-171">讀取 hello[開始使用事件中心][ lnk-eventhubs-tutorial]教學課程，如需有關如何 tooprocess 訊息從事件中樞 IoT 中樞的事件中樞相容端點資訊。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="3ae5a-172">事件中心尚不支援遙測中 Python，因此您可以建立[Node.js](iot-hub-node-node-getstarted.md#D2C_node)或[.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp)事件中心主控台應用程式 tooread hello 裝置到雲端訊息從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="3ae5a-173">本教學課程示範如何使用 hello [IoT 中樞總管工具][ lnk-iot-hub-explorer] tooread 這些裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="3ae5a-174">開啟命令提示字元，並安裝 hello IoT 中樞總管。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="3ae5a-175">執行下列命令 hello 命令提示字元中的 hello，toobegin 監視 hello 裝置到雲端訊息從您的裝置。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="3ae5a-176">使用您的 IoT 中樞連接字串之後的 hello 預留位置中`--login`。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="3ae5a-177">開啟新的命令提示字元並瀏覽包含 hello toohello 目錄**SimulatedDevice.py**檔案。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="3ae5a-178">執行 hello **SimulatedDevice.py**檔案會定期傳送遙測資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="3ae5a-179">觀察 hello 裝置訊息 hello 命令提示字元處執行 hello IoT 中樞總管 hello 前一節。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Python 裝置到雲端訊息][2]

## <a name="next-steps"></a><span data-ttu-id="3ae5a-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ae5a-181">Next steps</span></span>
<span data-ttu-id="3ae5a-182">在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="3ae5a-183">您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 toosend 裝置到雲端訊息 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="3ae5a-184">您觀察接收的 hello hello IoT 中樞總管工具協助 hello IoT 中樞的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="3ae5a-185">tooexplore hello Python SDK 的 Azure IoT 中樞使用量深入探討，請瀏覽[此中樞 Git 儲存機制][lnk-python-github]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="3ae5a-186">tooreview hello 傳訊功能 hello Azure IoT 中樞服務 SDK for Python，您可以下載並執行[iothub_messaging_sample.py][lnk-messaging-sample]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="3ae5a-187">裝置端模擬使用 hello Azure IoT 中樞裝置 SDK for Python，您可以下載並執行 hello [iothub_client_sample.py][lnk-client-sample]。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="3ae5a-188">使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="3ae5a-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="3ae5a-189">[連接您的裝置][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="3ae5a-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="3ae5a-190">[開始使用裝置管理][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="3ae5a-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="3ae5a-191">[開始使用 Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="3ae5a-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="3ae5a-192">toolearn 如何 tooextend 您 IoT 方案和程序裝置到雲端訊息在小數位數，請參閱 hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="3ae5a-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
