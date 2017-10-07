---
title: "C 的 aaaThe Azure IoT 裝置 SDK |Microsoft 文件"
description: "開始使用 hello Azure IoT 裝置 SDK for C，並了解如何 toocreate 裝置應用程式的通訊與 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a>適用於 C 的 Azure IoT 裝置 SDK

hello **Azure IoT 裝置 SDK**是一組程式庫設計 toosimplify hello 的 hello 從傳送訊息 tooand 接收訊息的處理程序**Azure IoT 中樞**服務。 有不同的變化的 hello SDK，每個目標為特定的平台，但此文章說明 hello **C 的 Azure IoT 裝置 SDK**。

C 的 hello Azure IoT 裝置 SDK 採用 ANSI C (C99) toomaximize 可攜性。 這個功能可以讓 hello 文件庫適合的 toooperate 上多個平台和裝置，特別是在最小化磁碟和記憶體耗用量是優先順序。

有各種平台的 hello SDK 已經過測試，(請參閱 hello [IoT 裝置類別目錄的 Azure 認證](https://catalog.azureiotsuite.com/)如需詳細資訊)。 雖然這篇文章包含 hello Windows 平台上執行的範例程式碼的逐步解說，本文中所述的 hello 程式碼支援的平台的 hello 範圍是一樣。

本文介紹 hello Azure IoT 裝置 SDK 的 toohello 結構 c。它會示範如何 tooinitialize hello 裝置程式庫，傳送資料 tooIoT 中樞，並從其中接收訊息。 本文章中的 hello 資訊應該使用 hello SDK，啟動足夠 tooget，但還提供指標 tooadditional 有關 hello 文件庫。

## <a name="sdk-architecture"></a>SDK 架構

您可以找到 hello [ **C 的 Azure IoT 裝置 SDK** ](https://github.com/Azure/azure-iot-sdk-c) GitHub 儲存機制和檢視詳細資料的 hello API 在 hello [C 應用程式開發介面參考](https://azure.github.io/azure-iot-sdk-c/index.html)。

hello hello 程式庫的最新版本可以在 hello**主要**hello 儲存機制分支：

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* hello hello SDK 的核心實作處於 hello **iot 中樞\_用戶端**hello 最低 API 層 hello SDK 中的 hello 實作所在的資料夾： hello **IoTHubClient**程式庫。 hello **IoTHubClient**程式庫包含應用程式開發介面實作未經處理的訊息，用於傳送訊息 tooIoT 中樞和接收訊息，或從 IoT 中樞。 使用此程式庫時，您要負責實作訊息序列化，但與 IoT 中樞通訊的其他細節則是由系統為您處理。
* hello**序列化程式**資料夾包含 helper 函式和範例，示範如何 tooserialize 資料之前使用 [tooAzure IoT 中樞傳送 hello 用戶端程式庫。 hello 使用 hello 序列化程式不是強制性，並提供為了方便起見。 toouse hello**序列化程式**程式庫，您定義指定 hello 資料 toosend tooIoT 中樞和 hello 訊息預期 tooreceive 從它的模型。 一旦定義 hello 模型之後，hello SDK 提供可讓您的 API 介面 tooeasily 工作與裝置到雲端與雲端到裝置訊息，而不需擔心 hello 序列化詳細資料。 hello 程式庫實作使用 MQTT 和 AMQP 通訊協定傳輸的其他開放原始碼程式庫而定。
* hello **IoTHubClient**取決於其他開放原始碼程式庫的程式庫：
  * hello [Azure C 共用公用程式](https://github.com/Azure/azure-c-shared-utility)程式庫，提供跨數個 Azure 相關 C Sdk 所需的基本工作，例如字串、 清單管理和 IO） 通用的功能。
  * hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c)程式庫，也就是針對資源限制裝置最佳化的 AMQP 的用戶端實作。
  * hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c)程式庫，這是一般用途的程式庫實作 hello MQTT 通訊協定，並最佳化資源限制裝置。

使用這些程式庫是更容易 toounderstand 藉由查看範例程式碼。 hello 下列各節將引導您完成數個 hello SDK 中隨附的 hello 範例應用程式。 本逐步解說應可提供更佳覺得 hello 的 hello SDK 和 Api 運作簡介 toohow hello 架構圖層的各種功能。

## <a name="before-you-run-hello-samples"></a>在執行之前 hello 範例

您可以在 hello Azure IoT 裝置 SDK 執行 hello 範例 c 之前，您必須[建立 hello IoT 中心服務的執行個體](iot-hub-create-through-portal.md)您 Azure 訂用帳戶中。 然後完成下列工作的 hello:

* 準備您的開發環境
* 取得裝置認證。

### <a name="prepare-your-development-environment"></a>準備您的開發環境

封裝可供通用平台 （例如 NuGet 適用於 Windows 或 apt_get Debian 和 Ubuntu） 和 hello 範例會使用這些封裝時使用。 在某些情況下，您需要 toocompile hello SDK，或者針對您的裝置。 如果您需要 toocompile hello SDK，請參閱[準備開發環境](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md)hello GitHub 儲存機制中。

tooobtain hello 應用程式程式碼範例的 hello SDK 從 GitHub 下載。 收到 hello hello 來源副本**主要**分支 hello [GitHub 儲存機制](https://github.com/Azure/azure-iot-sdk-c)。


### <a name="obtain-hello-device-credentials"></a>取得 hello 裝置認證

有 hello 範例原始碼之後下, 一件事 toodo hello 是 tooget 一組裝置認證。 如裝置 toobe 無法 tooaccess IoT 中樞，您必須先新增 hello 裝置 toohello IoT 中樞身分識別登錄。 當您新增裝置時，您會取得一組裝置認證所需的 hello 裝置 toobe 無法 tooconnect toohello IoT 中樞。 hello hello 下節中討論的範例應用程式預期這些認證中的 hello 表單**裝置連接字串**。

有數個開放原始碼工具 toohelp 管理您的 IoT 中樞。

* 稱為[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)的 Windows 應用程式。
* 稱為 [iothub-explorer](https://github.com/azure/iothub-explorer) 的跨平台 node.js CLI 工具。

本教學課程使用圖形化的 hello*裝置總管*工具。 您也可以使用 hello *iot 中樞總管*工具，如果您偏好 toouse CLI 工具。

hello 裝置總管] 工具會使用 hello Azure IoT 服務程式庫 tooperform 各種函式在 IoT 中樞內，包括新增裝置。 如果您使用 hello 裝置總管工具 tooadd 裝置時，您會取得連接字串為您的裝置。 您需要此連接字串 toorun hello 範例應用程式。

如果您不熟悉 hello 裝置總管工具，hello 遵循程序描述如何 toouse 它 tooadd 裝置，並取得裝置的連接字串。

tooinstall hello 裝置總管工具，請參閱[toouse 如何 IoT 中樞裝置 hello 裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)。

當您執行 hello 程式時，您會看到此介面：

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

輸入您**IoT 中樞連接字串**hello 中第一次欄位，然後按一下**更新**。 此步驟中設定 hello 工具，讓它可以與 IoT 中樞通訊。

Hello IoT 中樞連接字串設定時，按一下 hello**管理**] 索引標籤：

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

此索引標籤可讓您管理 hello 在 IoT 中樞註冊的裝置。

建立裝置即可 hello**建立**] 按鈕。 將會顯示一個已預先填入一組金鑰 (主要和次要) 的對話方塊。 輸入 [裝置識別碼]，然後按一下 [建立]。

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

建立 hello 裝置時，hello 裝置會列出所有的 hello 註冊裝置，包括您剛剛建立的 hello 與更新。 如果您在新裝置上按一下滑鼠右鍵，您會看到此功能表︰

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

如果您選擇**複製所選裝置的連線字串**，hello 裝置連接字串是複製的 toohello 剪貼簿。 Hello 裝置連接字串的副本。 您需要執行 hello hello 下列各節中所述的範例應用程式時。

當您完成上述 hello 步驟後時，您準備好 toostart 執行一些程式碼。 這兩個範例有常數的頂端 hello hello 主要原始程式檔，可讓您 tooenter 連接字串。 例如，hello hello 從對應的行**iot 中樞\_用戶端\_範例\_mqtt**應用程式會出現，如下所示。

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a>使用 hello IoTHubClient 程式庫

Hello 內**iot 中樞\_用戶端**資料夾中 hello [azure iot-sdk c](https://github.com/azure/azure-iot-sdk-c)儲存機制上，有**範例**資料夾包含應用程式呼叫**iot 中樞\_用戶端\_範例\_mqtt**。

hello Windows 版的 hello **iot 中樞\_用戶端\_範例\_mqtt**應用程式包含下列 Visual Studio 方案的 hello:

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> 如果您開啟這個專案在 Visual Studio 2017，接受 hello 提示 tooretarget hello 專案 toohello 最新版本。

此解決方案內含單一專案： 此解決方案中安裝了四個 NuGet 套件：

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.umqtt

您一律需要 hello **Microsoft.Azure.C.SharedUtility**封裝時您正在使用 hello SDK。 這個範例使用 hello MQTT 通訊協定，因此您必須包含 hello **Microsoft.Azure.umqtt**和**Microsoft.Azure.IoTHub.MqttTransport** （有相同的封裝 AMQP 和 HTTP 的封裝). 由於 hello 範例使用 hello **IoTHubClient**程式庫，您也必須包括 hello **Microsoft.Azure.IoTHub.IoTHubClient**方案中的封裝。

您可以在 hello 找到 hello 範例應用程式的 hello 實作**iot 中樞\_用戶端\_範例\_mqtt.c**原始程式檔。

hello 下列步驟會使用此範例應用程式 toowalk 您透過必要條件 toouse hello **IoTHubClient**程式庫。

### <a name="initialize-hello-library"></a>初始化 hello 程式庫

> [!NOTE]
> 您開始使用 hello 程式庫之前，您可能需要 tooperform 某些平台專屬的初始化。 例如，如果您計劃 Linux toouse AMQP 必須初始化 hello OpenSSL 程式庫。 hello 範例 hello [GitHub 儲存機制](https://github.com/Azure/azure-iot-sdk-c)呼叫 hello 公用程式函式**平台\_init**當 hello 用戶端開始，並呼叫 hello**平台\_deinit**結束之前的函式。 這些函式會宣告 hello platform.h 標頭檔中。 檢查 hello 定義這些函式的目標平台在 hello[儲存機制](https://github.com/Azure/azure-iot-sdk-c)toodetermine 是否需要 tooinclude 任何平台專屬的初始化程式碼中您的用戶端。

toostart hello 文件庫中，使用第一次配置 IoT 中樞用戶端控制代碼：

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

您傳遞您取得 hello 裝置總管工具 toothis 函式的 hello 裝置連接字串的複本。 您也指定 hello 通訊的通訊協定 toouse。 這個範例使用 MQTT，但 AMQP 與 HTTP 也是選項。

當您具有有效**iot 中樞\_用戶端\_處理**，您可以啟動呼叫 hello Api toosend 及接收訊息 tooand 從 IoT 中樞。

### <a name="send-messages"></a>傳送訊息

hello 範例應用程式會設定迴圈 toosend 訊息 tooyour IoT 中樞。 下列程式碼片段的 hello:

- 建立訊息。
- 新增屬性 toohello 訊息。
- 傳送訊息。

首先，建立一則訊息：

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

每次傳送訊息時，您會指定傳送嗨資料時，會叫用參考 tooa 回呼函式。 在此範例中，稱為 hello 回呼函式**SendConfirmationCallback**。 下列程式碼片段的 hello 顯示這個回呼函式：

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

請注意 hello 呼叫 toohello **IoTHubMessage\_終結**函式，當您完成 hello 訊息。 此函式會釋出 hello 建立 hello 訊息時配置的資源。

### <a name="receive-messages"></a>接收訊息

接收訊息是非同步作業。 首先，註冊 hello 回呼 tooinvoke hello 裝置收到訊息時：

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

您想要的 void 指標 toowhatever hello 最後一個參數。 在 hello 範例中，它會是指標 tooan 整數，但它可能是指標 tooa 更複雜的資料結構。 此參數可讓 hello 回呼函式 toooperate 共用狀態與 hello 呼叫者，此函式。

Hello 裝置收到訊息時，hello 註冊的回呼函式會叫用。 此回呼函式會擷取︰

* hello 訊息識別碼，從 hello 訊息的相互關聯識別碼。
* hello 訊息內容。
* Hello 訊息的任何自訂屬性。

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

使用 hello **IoTHubMessage\_GetByteArray**函式 tooretrieve hello 訊息，在此範例中為字串。

### <a name="uninitialize-hello-library"></a>取消初始化 hello 程式庫

當您完成時傳送事件，並接收訊息，您可以解除初始化 hello IoT 程式庫。 toodo 因此，發出下列函式呼叫的 hello:

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

此呼叫釋出先前 hello 所配置的 hello 資源**IoTHubClient\_CreateFromConnectionString**函式。

如您所見，它是簡單 toosend 和接收郵件 hello **IoTHubClient**程式庫。 hello 程式庫會處理與 IoT 中樞，包括哪些通訊協定 toouse 通訊的 hello 詳細資料 （hello hello 開發人員的觀點而言，這是簡單的組態選項）。

hello **IoTHubClient**程式庫也提供精確的控制如何 tooserialize hello 資料您的裝置傳送 tooIoT 中樞。 在某些情況下此層級的控制是一項優點，但在其他實作詳細資料，您不想 toobe 關心。 在 hello 情形下，您可以考慮使用 hello**序列化程式**程式庫 hello 下一節中所述。

## <a name="use-hello-serializer-library"></a>使用 hello 序列化程式庫

在概念上 hello**序列化程式**文件庫總結 hello **IoTHubClient** hello SDK 中的程式庫。 它會使用 hello **IoTHubClient** hello 基礎 IoT 中樞，但它與通訊的文件庫加入 hello 訊息序列化處理負擔移除 hello 開發人員的模型化功能。 此程式庫的運作方式最好是由範例示範。

內部 hello**序列化程式**資料夾中 hello [azure iot-sdk c 儲存機制](https://github.com/Azure/azure-iot-sdk-c)，是**範例**資料夾包含應用程式呼叫**simplesample\_mqtt**。 此範例的 hello Windows 版本包含下列 Visual Studio 方案的 hello:

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> 如果您開啟這個專案在 Visual Studio 2017，接受 hello 提示 tooretarget hello 專案 toohello 最新版本。

如同 hello 先前範例中，這其中一個包含數個 NuGet 封裝：

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.IoTHub.Serializer
* Microsoft.Azure.umqtt

您已看過大部分的這些套件在 hello 前一個範例中，但**Microsoft.Azure.IoTHub.Serializer**新。 此套件時，需要您使用 hello**序列化程式**程式庫。

您可以在 hello 找到 hello 範例應用程式的 hello 實作**simplesample\_mqtt.c**檔案。

hello 下列各節會逐步引導您 hello 的這個範例的關鍵部分。

### <a name="initialize-hello-library"></a>初始化 hello 程式庫

使用 hello toostart**序列化程式**程式庫，呼叫 hello 初始化應用程式開發介面：

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

hello 呼叫 toohello**序列化程式\_init**函式是一次性的呼叫，並初始化 hello 基礎程式庫。 然後，您可以呼叫 hello **IoTHubClient\_LL\_CreateFromConnectionString**函式，是 hello 相同的 API，例如 hello **IoTHubClient**範例。 此呼叫會設定您裝置的連接字串 (這個呼叫也是您在其中選擇 hello 通訊協定想 toouse)。 此範例會使用 MQTT 當做 hello 傳輸，但無法使用 AMQP 或 HTTP。

最後，呼叫 hello**建立\_模型\_執行個體**函式。 **WeatherStation**是 hello hello 模型命名空間和**ContosoAnemometer** hello hello 模型名稱。 一旦建立 hello 模型執行個體之後，您可以使用它，toostart 傳送和接收訊息。 不過，它是重要 toounderstand 是哪一種模型。

### <a name="define-hello-model"></a>定義 hello 模型

中的 hello**序列化程式**程式庫會定義您的裝置可以傳送 tooIoT 中樞和 hello 訊息，稱為 hello 訊息*動作*中模組化語言，它可以接收的 hello。 定義模型使用一組 C 巨集，例如 hello **simplesample\_mqtt**範例應用程式：

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

hello**開始\_命名空間**和**結束\_命名空間**巨集這兩個需要 hello 模型做為引數的 hello 命名空間。 預期這些巨集之間的任何項目是 hello 定義您的模型或模型，與 hello hello 模型使用的資料結構。

在此範例中，有一個名為 **ContosoAnemometer**的模型。 此模型會定義您的裝置可以傳送 tooIoT 中樞的資料之兩個部分： **DeviceId**和**WindSpeed**。 它也定義您裝置可接收的三個動作 (訊息)：**TurnFanOn**、**TurnFanOff** 及 **SetAirResistance**。 每個資料元素都有類型，而每個動作都有名稱 (以及一組選擇性的參數)。

hello 資料和 hello 模型中定義的動作定義的 API 介面，您可以使用 toosend 訊息 tooIoT 中樞，並回應傳送 toomessages toohello 裝置。 透過範例最能了解如何使用此模型。

### <a name="send-messages"></a>傳送訊息

hello 模型會定義您可以傳送 tooIoT 中樞的 hello 資料。 在此範例中，這表示一個 hello 使用 hello 定義的兩個資料項目**WITH_DATA**巨集。 有幾個步驟需要的 toosend **DeviceId**和**WindSpeed**值 tooan IoT 中樞。 hello 第一個是您想要 toosend tooset hello 資料：

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

hello 先前定義的模型可讓您 tooset hello 值所設定的成員**結構**。 接下來，序列化想 toosend hello 訊息：

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

此程式碼序列化 hello 裝置到雲端 tooa 緩衝區 (所參考**目的地**)。 hello 程式碼接著會叫用的 hello **sendMessage** toosend hello 訊息 tooIoT 中樞函式：

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


hello 第二個 toolast 參數**IoTHubClient\_LL\_SendEventAsync**是參考 tooa 回呼函式會成功地傳送 hello 資料時所呼叫。 以下是 hello 範例 hello 回呼函式：

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

hello 第二個參數是指標 toouser 內容。相同的指標傳遞太 hello**IoTHubClient\_LL\_SendEventAsync**。 在此情況下，hello 內容是簡單的計數器，但它可以是您想要的任何項目。

這就是沒有 toosending 裝置到雲端訊息。 hello 只保留 toocover 是如何 tooreceive 訊息。

### <a name="receive-messages"></a>接收訊息

接收訊息的運作方式類似 toohello 訊息在中運作的方式 hello **IoTHubClient**程式庫。 首先，您需登錄訊息回呼函式：

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

然後，您可以撰寫 hello 時收到訊息時叫用的回呼函式：

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

此程式碼是未定案--它具有 hello 相同的任何方案。 此函式收到 hello 訊息，並負責路由傳送透過 hello 呼叫 toohello 適當的函式太**EXECUTE\_命令**。 hello 函式，呼叫此時取決於您的模型中的 hello 動作 hello 定義。

當您在模型中定義的動作時，您需要 tooimplement 裝置收到 hello 對應的訊息時所呼叫的函式。 例如，如果您的模型定義這項動作：

```c
WITH_ACTION(SetAirResistance, int, Position)
```

使用此簽章定義函式：

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

請注意如何 hello hello 函式名稱比對 hello hello 模型中的 hello 動作名稱和 hello 的 hello 函式的參數符合指定的 hello 動作的 hello 參數。 hello 第一個參數永遠是必要項，並包含您的模型的指標 toohello 執行個體。

Hello 裝置接收符合此簽章的訊息，稱為 hello 對應函式。 因此，除了具有 tooinclude hello 未定案程式碼從**IoTHubMessage**，接收訊息只是定義為模型中定義的每個動作的簡單函式。

### <a name="uninitialize-hello-library"></a>取消初始化 hello 程式庫

當您完成將資料傳送和接收訊息，您可以解除初始化 hello IoT 程式庫：

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

所有這些三個函式符合先前所述 hello 三個初始設定函式。 呼叫這些 API 可確保您釋放先前配置的資源。

## <a name="next-steps"></a>後續步驟

本文涵蓋使用 hello 文件庫中 hello hello 基本概念**C 的 Azure IoT 裝置 SDK**。它提供您足夠的資訊 toounderstand hello SDK、 其結構，以及如何 tooget 入門使用 hello Windows 範例中包含的內容。 hello 下一個發行項的說明繼續 hello SDK hello 描述[更多關於 hello IoTHubClient 程式庫](iot-hub-device-sdk-c-iothubclient.md)。

toolearn 進一步了解開發的 IoT 中樞，請參閱 hello [Azure IoT Sdk][lnk-sdks]。

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
