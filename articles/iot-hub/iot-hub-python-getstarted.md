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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>連接使用 Python 您模擬的裝置 tooyour IoT 中樞
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

在本教學課程的 hello 結束時，您將擁有兩個的 Python 應用程式：

* **CreateDeviceIdentity.py**，這樣就可以建立裝置身分識別，以及相關聯的安全性金鑰 tooconnect 應用程式模擬的裝置。
* **SimulatedDevice.py**、 tooyour IoT 中樞連線以稍早建立的 hello 裝置身分識別，並定期傳送遙測訊息使用 hello MQTT 通訊協定。

> [!NOTE]
> hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 這兩個應用程式 toorun 裝置和您的方案後端上。
> 
> 

toocomplete 本教學課程中，您需要遵循的 hello:

* [Python 2.x 或 3.x][lnk-python-download]。 請確定 toouse hello 32 位元或 64 位元安裝所需的安裝程式。 出現提示時 hello 安裝期間，請確定 tooadd Python tooyour 平台專屬環境變數。 如果您使用 Python 2.x，您可能需要過[安裝或升級*pip*，hello Python 封裝管理系統][lnk-install-pip]。
* 如果您使用 Windows 作業系統，然後[Visual c + + 可轉散發套件][ lnk-visual-c-redist] tooallow hello 使用來自 Python 的原生 Dll。
* [Node.js 4.0 或更新版本][lnk-node-download]。 請確定 toouse hello 32 位元或 64 位元安裝所需的安裝程式。 這是所需的 tooinstall hello [IoT 中樞總管工具][lnk-iot-hub-explorer]。
* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。

> [!NOTE]
> hello *pip*封裝的`azure-iothub-service-client`和`azure-iothub-device-client`目前僅適用於 Windows 作業系統。 Linux/Mac OS，請參閱 toohello Linux 和 Mac OS 特定章節 hello[準備開發環境的 Python] [ lnk-python-devbox]文章。
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

您現在已經建立 IoT 中樞。 在本教學課程的 hello 其餘部分使用 hello IoT 中樞的主機名稱與 hello IoT 中樞連接字串。

> [!NOTE]
> 您可以輕鬆建立 IoT 中樞命令列上使用 hello Python 或 Node.js 基礎 Azure CLI。 hello 文章[建立 IoT 中心使用 hello Azure CLI 2.0] [ lnk-azure-cli-hub]您因此 hello toodo 快速步驟所示。 
> 

## <a name="create-a-device-identity"></a>建立裝置識別
此區段會列出 hello 步驟 toocreate Python 主控台應用程式，您的 IoT 中樞 hello 身分識別登錄中建立裝置身分識別。 如果其中有傳送 hello 身分識別登錄中的裝置只能連接 tooIoT 中樞。 如需詳細資訊，請參閱 hello**身分識別登錄**區段 hello [IoT 中樞開發人員指南][lnk-devguide-identity]。 當您執行此主控台應用程式時，它會產生唯一的裝置識別碼，並傳送至雲端的裝置時，您的裝置，可以使用 tooidentify 本身的索引鍵郵件 tooIoT 中樞。

1. 開啟命令提示字元，並安裝 hello **Azure IoT 中樞服務 SDK for Python**。 在您安裝 hello SDK 之後，請關閉 hello 命令提示字元。

    ```
    pip install azure-iothub-service-client
    ```

2. 建立名為 **CreateDeviceIdentity.py** 的 Python 檔案。 在中開啟它[Python 編輯器/IDE 您選擇的][lnk-python-ide-list]，比方說，hello 預設[閒置][lnk-idle]。

3. 新增 hello hello 服務 SDK 中的下列程式碼 tooimport hello 所需的模組：

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. 新增下列程式碼、 取代 hello 預留位置 hello `[IoTHub Connection String]` hello hello IoT 中樞，您在 hello 上一節中建立的連接字串。 您可以使用任何名稱為 hello `DEVICE_ID`。
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. 新增 hello 下列函式 tooprint hello 裝置資訊的某些部分。

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
3. 新增下列使用 hello 登錄管理員函式 toocreate hello 裝置識別碼 hello。 

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
4. 最後，新增 hello main 函式，如下所示，並儲存 hello 檔案。

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
5. Hello 命令提示字元處執行 hello **CreateDeviceIdentity.py** ，如下所示：

    ```python
    python CreateDeviceIdentity.py
    ```
6. 您應該會看到 hello 取得建立模擬的裝置。 記下 hello **deviceId**和 hello **primaryKey**此裝置。 您需要這些值稍後當您建立連線 tooIoT 中樞為裝置的應用程式。

    ![成功建立裝置][1]

> [!NOTE]
> hello IoT 中樞身分識別登錄只會儲存裝置身分識別 tooenable 安全存取 toohello IoT 中樞。 它會儲存裝置識別碼和金鑰 toouse 安全性認證以及啟用/停用旗標，您可以使用 toodisable 存取個別的裝置。 如果您的應用程式需要 toostore 其他裝置專屬的中繼資料，它應該使用特定應用程式存放區。 如需詳細資訊，請參閱 hello [IoT 中樞開發人員指南][lnk-devguide-identity]。
> 
> 


## <a name="create-a-simulated-device-app"></a>建立模擬裝置應用程式
此區段會列出 hello 步驟 toocreate Python 主控台應用程式，可模擬裝置，並將傳送裝置到雲端訊息 tooyour IoT 中樞。

1. 開啟新的命令提示字元，並安裝 hello Azure IoT 中樞裝置 SDK for Python 如下。 關閉 hello hello 安裝後的命令提示字元。

    ```
    pip install azure-iothub-device-client
    ```
2. 建立名為 **SimulatedDevice.py** 的檔案。 在您所選的 Python 編輯器/IDE (例如 IDLE) 中開啟此檔案。

3. 新增 hello hello 裝置 SDK 中的下列程式碼 tooimport hello 所需的模組。

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. 新增 hello 下列程式碼，並取代 hello 預留位置`[IoTHub Device Connection String]`與您的裝置 hello 連接字串。 hello 裝置連接字串中的 hello 格式通常是`HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`。 使用 hello **deviceId**和**primaryKey** hello 裝置，您在前一個區段 tooreplace hello hello 中建立的`<deviceId>`和`<primaryKey>`分別。 使用 IoT 中樞的主機名稱 (通常為 `<IoT hub name>.azure-devices.net`) 取代 `<hostName>`。

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
5. 新增下列程式碼 toodefine 傳送確認回呼 hello。 

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
6. 新增下列程式碼 tooinitialize hello 裝置用戶端 hello。

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. 加入下列 hello 函式 tooformat，並從模擬的裝置 tooyour IoT 中樞將訊息傳送。

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
8. 最後，加入 hello main 函式。 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. 儲存並關閉 hello **SimulatedDevice.py**檔案。 您會立即準備 toorun 此應用程式。

> [!NOTE]
> 簡單 tookeep 方面，本教學課程未實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>從模擬裝置接收訊息
tooreceive 遙測訊息從您的裝置，您需要 toouse[事件中心][lnk-event-hubs-overview]-相容 hello IoT 中樞，讀取 hello 裝置到雲端訊息所公開的端點。 讀取 hello[開始使用事件中心][ lnk-eventhubs-tutorial]教學課程，如需有關如何 tooprocess 訊息從事件中樞 IoT 中樞的事件中樞相容端點資訊。 事件中心尚不支援遙測中 Python，因此您可以建立[Node.js](iot-hub-node-node-getstarted.md#D2C_node)或[.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp)事件中心主控台應用程式 tooread hello 裝置到雲端訊息從 IoT 中樞。 本教學課程示範如何使用 hello [IoT 中樞總管工具][ lnk-iot-hub-explorer] tooread 這些裝置的訊息。

1. 開啟命令提示字元，並安裝 hello IoT 中樞總管。 

    ```
    npm install -g iothub-explorer
    ```

2. 執行下列命令 hello 命令提示字元中的 hello，toobegin 監視 hello 裝置到雲端訊息從您的裝置。 使用您的 IoT 中樞連接字串之後的 hello 預留位置中`--login`。

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. 開啟新的命令提示字元並瀏覽包含 hello toohello 目錄**SimulatedDevice.py**檔案。

4. 執行 hello **SimulatedDevice.py**檔案會定期傳送遙測資料 tooyour IoT 中樞。 
   
    ```
    python SimulatedDevice.py
    ```
5. 觀察 hello 裝置訊息 hello 命令提示字元處執行 hello IoT 中樞總管 hello 前一節。 

    ![Python 裝置到雲端訊息][2]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。 您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 toosend 裝置到雲端訊息 toohello IoT 中樞。 您觀察接收的 hello hello IoT 中樞總管工具協助 hello IoT 中樞的 hello 訊息。 

tooexplore hello Python SDK 的 Azure IoT 中樞使用量深入探討，請瀏覽[此中樞 Git 儲存機制][lnk-python-github]。 tooreview hello 傳訊功能 hello Azure IoT 中樞服務 SDK for Python，您可以下載並執行[iothub_messaging_sample.py][lnk-messaging-sample]。 裝置端模擬使用 hello Azure IoT 中樞裝置 SDK for Python，您可以下載並執行 hello [iothub_client_sample.py][lnk-client-sample]。

使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：

* [連接您的裝置][lnk-connect-device]
* [開始使用裝置管理][lnk-device-management]
* [開始使用 Azure IoT Edge][lnk-iot-edge]

toolearn 如何 tooextend 您 IoT 方案和程序裝置到雲端訊息在小數位數，請參閱 hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程。
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
