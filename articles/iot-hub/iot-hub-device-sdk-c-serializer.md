---
title: "C-序列化程式，aaaAzure IoT 裝置 SDK |Microsoft 文件"
description: "如何 toouse hello 序列化程式庫的 C toocreate 裝置應用程式的 hello Azure IoT 裝置 SDK 進行通訊與 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>適用於 C 的 Azure IoT 裝置 SDK - 深入了解序列化程式
hello[先文章](iot-hub-device-sdk-c-intro.md)中這個數列導入 hello **C 的 Azure IoT 裝置 SDK**。 hello 下一篇文章提供更詳細的描述的 hello [ **IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md). 這篇文章提供更詳細的描述的其餘元件 hello 完成 hello SDK 的涵蓋範圍： hello**序列化程式**程式庫。

hello 簡介文章所述方式 toouse hello**序列化程式**文件庫 toosend 事件 tooand 從 IoT 中心接收訊息。 在本文中延伸，討論藉由提供方式的更完整的說明 toomodel 資料以 hello**序列化程式**巨集語言。 hello 文章也包含更多詳細 hello 程式庫將訊息的序列化，並在某些情況下如何控制 hello 序列化行為。 我們也將說明您可以修改判斷 hello 大小，您所建立的 hello 模型的某些參數。

最後，hello 發行項會重新審視某些訊息等屬性處理的上一個文件中涵蓋的主題。 因為我們會了解，這些功能的運作在 hello 相同方式使用 hello**序列化程式**文件庫以 hello 一樣**IoTHubClient**程式庫。

本文中所述的所有項目根據 hello**序列化程式**SDK 範例。 如果您想沿著 toofollow，請參閱 hello **simplesample\_amqp**和**simplesample\_http** C.hello Azure IoT 裝置 SDK 中所包含的應用程式

您可以找到 hello [ **C 的 Azure IoT 裝置 SDK** ](https://github.com/Azure/azure-iot-sdk-c) GitHub 儲存機制和檢視詳細資料的 hello API 在 hello [C 應用程式開發介面參考](https://azure.github.io/azure-iot-sdk-c/index.html)。

## <a name="hello-modeling-language"></a>hello 模組化語言
hello[簡介文章](iot-hub-device-sdk-c-intro.md)中這個數列導入 hello **C 的 Azure IoT 裝置 SDK**模組化語言 hello 中所提供的 hello 範例透過**simplesample\_amqp**應用程式：

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

如您所見，hello 模組化語言是以 C 巨集為基礎。 您的定義開頭一律會是 **BEGIN\_NAMESPACE**，而結尾則一律是 **END\_NAMESPACE**。 它是一般 tooname hello 命名空間為您的公司或如同此範例中，您正在使用的 hello 專案。

Hello 命名空間內的元素是一種模型定義。 在此案例中，有一個單一的風速計模型。 同樣地，hello 模型可以命名為任何項目，但通常此節點稱為 hello 裝置或類型的資料要 tooexchange 與 IoT 中樞。  

模型包含定義的 hello 事件中，您可以輸入 tooIoT 中樞 (hello*資料*) 以及您可以從 IoT 中樞接收 hello 訊息 (hello*動作*)。 您可以看到 hello 範例中，事件具有類型和欄位名稱。動作都有一個名稱和選擇性的參數 （各有型別）。

並不會在此範例中示範是 hello SDK 所支援的其他資料型別。 我們將在稍後討論。

> [!NOTE]
> IoT 中樞是指 toohello 資料的裝置傳送為 tooit*事件*，而 hello 模組化語言參考做為 tooit*資料*(使用定義**WITH_DATA**)。 同樣地，IoT 中樞是指 toohello 資料傳送為 toodevices*訊息*，而 hello 模組化語言參考做為 tooit*動作*(使用定義**WITH_ACTION**)。 請注意，在本文中可能會交替使用這些詞彙。
> 
> 

### <a name="supported-data-types"></a>支援的資料類型
建立 hello 的模型中支援下列資料類型的 hello**序列化程式**程式庫：

| 類型 | 說明 |
| --- | --- |
| double |雙精確度浮點數 |
| int |32 位元整數 |
| float |單精確度浮點數 |
| long |長整數 |
| int8\_t |8 位元整數 |
| int16\_t |16 位元整數 |
| int32\_t |32 位元整數 |
| int64\_t |64 位元整數 |
| 布林 |布林值 |
| ascii\_char\_ptr |ASCII 字串 |
| EDM\_DATE\_TIME\_OFFSET |日期時間位移 |
| EDM\_GUID |GUID |
| EDM\_BINARY |binary |
| DECLARE\_STRUCT |複雜資料類型 |

讓我們開始 hello 最後一個資料類型。 hello **DECLARE\_結構**可讓您 toodefine 複雜資料型別，也就是群組的 hello 其他基本型別。 這些群組可讓我們 toodefine 的模型，看起來像這樣：

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

我們的模型包含 **TestType**類型的單一資料事件。 **TestType**是包含數個成員，統稱為示範 hello hello 所支援的基本型別之複雜型別的**序列化程式**模組化語言。

使用像這樣的模型，我們可以撰寫程式碼 toosend 資料 tooIoT 集線器出現，如下所示：

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

基本上，我們正在指派值的 hello tooevery 成員**測試**結構，然後再呼叫**SendAsync** toosend hello**測試**資料事件 toohello 雲端。 **SendAsync**會傳送單一資料事件 tooIoT 中樞的 helper 函式：

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

此函式序列化 hello 指定之資料的事件，並將它傳送 tooIoT 集線器使用**IoTHubClient\_SendEventAsync**。 這是相同的程式碼中前一個發行項所討論的 hello (**SendAsync**封裝 hello 邏輯到方便的函式)。

一個 hello 先前的程式碼中使用其他 helper 函式是**GetDateTimeOffset**。 此函式轉換成值類型的特定時間的 hello **EDM\_日期\_時間\_位移**:

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

如果您執行此程式碼，hello 下訊息會傳送 tooIoT 中樞：

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

請注意，hello 序列化為 JSON，這是產生的 hello hello 格式**序列化程式**程式庫。 也請注意，每個成員的 hello 序列化 JSON 物件會比對的 hello hello 成員**TestType**我們在我們的模型定義。 hello 值也完全符合 hello 程式碼中使用。 不過，請注意，會以 base64 編碼 hello 二進位資料:"AQID 」 是 base64 編碼的 hello {0x01、 0x02、 0x03}。

這個範例會示範使用 hello 的 hello 優點**序列化程式**程式庫-它可讓我們 toosend JSON toohello 雲端，而不需要 tooexplicitly 處理我們的應用程式中的序列化。 這些了解 tooworry 在我們的模型，然後再呼叫這些事件 toohello 雲端簡單的應用程式開發介面 toosend 設定 hello hello 值資料事件。

利用此資訊，我們可以定義包含支援的資料類型，包括複雜型別 （我們甚至無法包含其他複雜類型內的複雜類型） 的 hello 範圍的模型。 不過，他序列化 JSON 產生的 hello 上述範例會顯示很重要的一點。 *如何*我們傳送給資料以 hello**序列化程式**程式庫可讓您判斷完全 hello JSON 形成方式。 此特點就是我們接下來要討論的內容。

## <a name="more-about-serialization"></a>深入了解序列化
hello 上一節會反白顯示 hello 所產生的輸出 hello 範例**序列化程式**程式庫。 在本節中，我們將說明 hello 程式庫將資料序列化，以及如何控制使用 hello 序列化應用程式開發介面的行為。

在進行序列化時的順序 tooadvance hello 討論，我們將會使用新的模型根據 thermostat。 首先，我們提供一些背景 hello 案例中，我們正嘗試 tooaddress。

我們想要測量的溫度和溼度 thermostat toomodel。 每個資料片段即將 toobe 以不同的方式傳送 tooIoT 中樞。 根據預設，hello thermostat ingresses 溫度事件一次每 2 分鐘。溼度事件是一次每隔 15 分鐘 ingressed。 Ingressed 任一事件時，它必須包含該 hello 對應溫度顯示 hello 時間的時間戳記或測量溼度。

提供此案例中，我們將示範兩個不同的方式 toomodel hello 資料，及我們將說明該模型已在 hello 序列化輸出的 hello 效果。

### <a name="model-1"></a>模型 1
以下是模型的 hello 第一個版本支援 hello 前一個案例：

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

請注意該 hello 模型包含兩個資料事件：**溫度**和**溼度**。 不同於上述範例中，每個事件 hello 類型是定義使用的結構**DECLARE\_結構**。 **TemperatureEvent** 包含溫度測量和時間戳記；**HumidityEvent** 包含溼度測量和時間戳記。 此模型會提供自然的方式 toomodel hello 資料 hello 上面所述的案例。 當我們傳送事件 toohello 雲端時，我們可能會傳送溫度/時間戳記或時間戳記溼度/配對。

我們可以傳送溫度事件 toohello 雲端中使用 hello 如下的程式碼：

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

我們會使用硬式編碼值氣溫和溼度 hello 範例程式碼，但假設，我們實際擷取這些值由取樣 hello hello thermostat 上的對應感應器。

hello 上述的程式碼會使用 hello **GetDateTimeOffset**引進了先前的協助程式。 原因將會清除更新版本，此程式碼明確分隔 hello 的工作序列化，以及傳送嗨事件。 hello 先前的程式碼會將 hello 溫度事件序列化至緩衝區。 然後， **sendMessage**是 helper 函式 (包含在**simplesample\_amqp**) 傳送 hello 事件 tooIoT 中樞：

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

此程式碼是子集 hello **SendAsync** helper hello 上一節中所述，因此我們將不會在這裡透過它一次。

當我們執行 hello 先前程式碼 toosend hello 溫度的事件時，這種 hello 事件序列化的形式傳送 tooIoT 中樞：

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

我們要傳送的溫度屬於 **TemperatureEvent** 類型，而該結構包含 **Temperature** 和 **Time** 成員。 這會直接反映 hello 序列化資料中。

同樣地，我們可以利用此程式碼來傳送溼度事件：

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

傳送 tooIoT 中樞 hello 序列化表單隨即出現，如下所示：

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

同樣地，全如預期一般。

您可以使用此模型來想像如何輕鬆地加入其他事件。 您定義使用多個結構**DECLARE\_結構**，並將 hello 對應事件包含在 hello 模型使用**WITH\_資料**。

現在，讓我們來修改 hello 模型，使其包含 hello 相同的資料，但不同的結構。

### <a name="model-2"></a>模型 2
上方，請考慮這個替代的模型 toohello 其中一個：

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

在此情況下，我們已去除 hello **DECLARE\_結構**巨集，只會定義從我們的案例中使用簡單型別從模組化語言 hello hello 資料項目。

只針對 hello 目前我們忽略 hello**時間**事件。 與該另行，以下是 hello 程式碼 tooingress**溫度**:

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

此程式碼會傳送 hello 下列序列化事件 tooIoT 中樞：

```
{"Temperature":75}
```

而且 hello 傳送 hello 溼度事件程式碼會出現，如下所示：

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

此程式碼會傳送此 tooIoT 中樞：

```
{"Humidity":45}
```

到目前為止，仍毫無意外。 現在我們來變更 我們如何使用 hello 序列化巨集。

hello**序列化**巨集可做為引數的多個資料事件。 這可讓我們 tooserialize hello**溫度**和**溼度**事件放在一起，並在單一呼叫中傳送 tooIoT 中樞：

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

您猜的這段程式碼的 hello 結果是兩個資料事件會傳送 tooIoT 中樞：

[

{"Temperature":75},

{"Humidity":45}

]

換句話說，您可能預期這段程式碼是 hello 相同傳送**溫度**和**溼度**分開。 它是只方便 toopass 這兩個事件太**序列化**hello 在相同呼叫。 不過，這不是 hello 案例。 相反地，hello 上述的程式碼會傳送這個單一資料事件 tooIoT 中樞：

{"Temperature":75, "Humidity":45}

這可能看似奇怪，因為我們的模型將 **Temperature** 和 **Humidity** 定義成兩個「個別」事件：

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

多個 toohello 點，我們沒有這些事件模型其中**溫度**和**溼度**hello 中相同的結構：

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

如果我們使用此模型時，將更容易 toounderstand 如何**溫度**和**溼度**就會傳送 hello 中相同序列化訊息。 不過它可能無法清除為什麼 ﹐，這樣一來當您將傳遞這兩個資料事件太**序列化**使用模型 2。

如果您知道該 hello hello 假設，此行為是更容易 toounderstand**序列化程式**正在程式庫。 toomake 意義吧後 tooour 模型：

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

請以物件導向的觀點思考此模型。 在此案例中，我們要模型化的是一個實體裝置 (控溫器)，而該裝置包含 **Temperature** 和 **Humidity** 之類的屬性。

我們可以傳送 hello 與 hello 如下的程式碼模型的完整的狀態：

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

假設 hello 值溫度、 溼度和時間設定，我們將會看到類似此傳送 tooIoT 中樞事件：

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

有時候您可能只想 toosend*某些*hello 模型 toohello 雲端 （特別是如果您的模型包含大量的資料事件） 的內容。 它是有用 toosend 子集的資料事件，如在先前的範例：

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

這會產生完全 hello 相同序列化事件，如同我們已經定義**TemperatureEvent**與**溫度**和**時間**成員，就像我們並未與模型 1。 我們在此情況下無法 toogenerate 完全 hello 相同序列化事件使用不同的模型 （模型 2），因為我們呼叫**序列化**以不同方式。

hello 很重要的一點是，如果您傳遞太多個資料事件**序列化，**然後它會假設每個事件位於單一 JSON 物件中的屬性。

hello 最好的方法取決於您和考慮您的模型。 如果您要傳送 「 事件 」 toohello 雲端，而且每個事件包含一組定義的屬性，hello 第一種方法可讓一個很實用。 在此情況下，您會使用**DECLARE\_結構**toodefine hello 結構的每個事件，然後將它們包含在您的模型，以 hello **WITH\_資料**巨集。 然後可以如同我們在 hello 上面的第一個範例中傳送的每個事件。 在這種方法中您可以只傳遞單一的資料事件太**序列化程式**。

如果您認為有關您的模型物件導向的方式，然後 hello 第二種方法可能適合您。 在此情況下，hello 定義使用的項目**WITH\_資料**是 hello 「 屬性 」 的物件。 您傳遞事件的任何子集太**序列化**，您想要根據您 「 物件 」 狀態中有多少 toosend toohello 雲端。

沒有絕對正確或錯誤的方法。 只是如何 hello**序列化程式**程式庫的運作方式，並挑選 hello 模型化方法最適合您的需求。

## <a name="message-handling"></a>訊息處理
到目前為止本文僅討論傳送事件 tooIoT 集線器，，而且尚未處理接收訊息。 hello 原因 tooknow 關於接收訊息為此，我們需要主要中涵蓋[稍早文章](iot-hub-device-sdk-c-intro.md)。 請從那篇文章回憶，您是藉由註冊訊息回呼函式來處理訊息：

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

接著，您可以撰寫在 hello 時收到訊息時叫用的回呼函式：

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
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

這項實作**IoTHubMessage**呼叫 hello 您的模型中每個動作的特定函式。 例如，如果您的模型定義這項動作：

```
WITH_ACTION(SetAirResistance, int, Position)
```

您必須使用此簽章定義函式：

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** tooyour 裝置傳送該訊息時再呼叫。

我們還沒說明尚未的訊息看起來像是 hello 序列化版本。 換句話說，如果您想 toosend **SetAirResistance**訊息 tooyour 裝置，該的外觀為何？

如果您要傳送的訊息 tooa 裝置，您會達成透過 hello Azure IoT 服務 SDK。 您需要 tooknow 字串 toosend tooinvoke 特定動作。 hello 傳送訊息的一般格式如下所示：

```
{"Name" : "", "Parameters" : "" }
```

您要傳送序列化的 JSON 物件，使用兩個屬性：**名稱**hello 名稱 hello 動作 （訊息） 和**參數**包含 hello 參數，該動作。

例如，tooinvoke **SetAirResistance**可以傳送此訊息 tooa 裝置：

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

hello 動作名稱必須完全符合您的模型中定義的動作。 必須同時符合 hello 參數名稱。 也請注意區分大小寫。 **Name** 和 **Parameters** 一律是大寫。 在模型中，請確定 toomatch hello 情況下，您的動作名稱和參數。 在此範例中，hello 動作名稱是"SetAirResistance"並不是"setairresistance"。

hello 其他兩個動作**TurnFanOn**和**TurnFanOff**可以傳送這些訊息 tooa 裝置叫用：

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

本章節所述的一切 tooknow 時將事件傳送和接收訊息與 hello**序列化程式**程式庫。 在繼續討論之前，讓我們先討論一些您可以設定以控制模型大小的參數。

## <a name="macro-configuration"></a>巨集組態
如果您使用 hello**序列化程式**hello azure-c-共用-公用程式程式庫中找到 hello SDK toobe 注意的重要部分的程式庫。
如果您已經複製 hello Azure iot-sdk c 儲存機制從 GitHub 使用 hello-遞迴 選項，您會找到這個公用程式共用程式庫：

```
.\\c-utility
```

如果您已經不複製 hello 程式庫，您可以找到[這裡](https://github.com/Azure/azure-c-shared-utility)。

Hello 共用公用程式庫中，您將找到下列資料夾的 hello:

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

此資料夾包含名為 **macro\_utils\_h\_generator.sln** 的 Visual Studio 方案：

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

在此解決方案中的 hello 程式會產生 hello**巨集\_utils.h**檔案。 沒有預設巨集\_utils.h hello SDK 所包含的檔案。 此解決方案可讓您 toomodify 某些參數，然後重新建立 hello 根據這些參數的標頭檔。

hello 兩個索引鍵參數 toobe 關心**nArithmetic**和**nMacroParameters**巨集中找到這兩行定義所在\_utils.tt:

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

這些值為 hello hello SDK 所隨附的預設參數。 每個參數具有下列意義 hello:

* nMacroParameters – 控制您在一個 DECLARE\_MODEL 巨集定義中可以擁有多少參數。
* nArithmetic – 控制項 hello 的總數在模型中允許的成員。

這些參數都是重要的 hello 原因是因為他們控制您的模型可以是多大。 例如，請考慮以此模型定義：

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

如先前所述，**DECLARE\_MODEL** 只是一個 C 巨集。 hello hello 模型與 hello 名稱**WITH\_資料**陳述式 （但其他巨集） 是參數**DECLARE\_模型**。 **nMacroParameters** 會定義 **DECLARE\_MODEL** 中可以包含多少參數。 實際上，這定義的是您所能擁有的資料事件和動作宣告數目。 因此，124 hello 預設限制這表示您可以定義具有約 60 動作和事件資料的組合的模型。 如果您嘗試 tooexceed 這項限制，您會收到看起來類似 toothis 編譯器錯誤：

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

hello **nArithmetic**參數是深入了解 hello 內部運作的 hello 巨集語言與您的應用程式。  它所控制的成員，您可以在模型中的 hello 總數包括**DECLARE_STRUCT**巨集。 如果您開始看到這類編譯器錯誤，則應該嘗試提高 **nArithmetic**的值：

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

如果您想 toochange 這些參數，修改 hello 巨集中的 hello 值\_utils.tt 檔案、 重新編譯 hello 巨集\_utils\_h\_generator.sln 解決方案，以及執行的 hello 已編譯的程式。 當您這樣做，新的巨集\_utils.h 檔案會產生並放置於 hello。\\一般\\inc 目錄。

在巨集的順序 toouse hello 新版本\_utils.h、 移除 hello**序列化程式**NuGet 封裝，從您的方案，然後在其位置包含 hello**序列化程式**Visual Studio 專案。 這可讓您的程式碼 toocompile 針對 hello 序列化程式庫的 hello 原始程式碼。 這包括更新的 hello 巨集\_utils.h。 如果您想 toodo 此作業對於**simplesample\_amqp**，開始移除 hello 方案中的 hello 序列化程式庫的 hello NuGet 封裝：

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

然後加入此專案 tooyour Visual Studio 方案：

> .\\c\\serializer\\build\\windows\\serializer.vcxproj
> 
> 

完成時，解決方案應該如下所示：

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

現在當您編譯您的方案，hello 更新巨集\_utils.h 隨附於您的二進位檔。

請注意，增加這些值到足夠高的數目可能會超出編譯器限制。 toothis 點，hello **nMacroParameters**是以 hello 擔心哪些 toobe 主要參數。 hello C99 規格指定的巨集定義中允許有 127 參數的最小值。 hello Microsoft 編譯器完全遵循 hello 規格 （並已限制為 127），因此您必須能夠 tooincrease **nMacroParameters**超出 hello 預設。 其他編譯器可讓您 toodo 因此 （例如，hello GNU 編譯器支援更高的限制）。

到目前為止我們所討論的幾乎所需的一切相關 toowrite 撰寫程式碼以 hello tooknow**序列化程式**程式庫。 在做出結論之前，讓我們先從先前的文章中回顧一些您可能想知道的主題。

## <a name="hello-lower-level-apis"></a>hello 較低層級應用程式開發介面
這篇文章焦點所在的 hello 範例應用程式是**simplesample\_amqp**。 此範例會使用 hello 較高層級 （hello 非-"LL"） 應用程式開發介面 toosend 事件，並接收訊息。 如果您使用這些 API，將會執行背景執行緒來處理事件傳送和訊息接收。 不過，您可以使用 hello 較低層級 (LL) Api tooeliminate 這個背景執行緒，並採取明確控制當您將事件傳送或接收 hello 雲端中的訊息。

中所述[前一篇文章](iot-hub-device-sdk-c-iothubclient.md)，沒有一組函式組成的 hello 較高層級的應用程式開發介面：

* IoTHubClient\_CreateFromConnectionString
* IoTHubClient\_SendEventAsync
* IoTHubClient\_SetMessageCallback
* IoTHubClient\_Destroy

**simplesample\_amqp** 中會示範這些 API。

此外，也有一組類似的較低層級 API。

* IoTHubClient\_LL\_CreateFromConnectionString
* IoTHubClient\_LL\_SendEventAsync
* IoTHubClient\_LL\_SetMessageCallback
* IoTHubClient\_LL\_Destroy

請注意，hello 較低層級 Api 工作完全 hello 相同方式與 hello 前一個發行項中所述。 如果您想背景執行緒 toohandle 事件傳送和接收訊息，您可以使用 hello 第一組 Api。 如果您想要明確控制當您傳送並接收來自 IoT 中樞的資料，您可以使用應用程式開發介面的 hello 第二個集合。 設定的應用程式開發介面的工作也與 hello**序列化程式**程式庫。

如需如何 hello 較低層級的 Api 來以 hello**序列化程式**程式庫，請參閱 hello **simplesample\_http**應用程式。

## <a name="additional-topics"></a>其他主題
幾個其他值得再次一提的主題包括屬性處理、使用替代裝置認證及組態選項。 這些都是 [先前的文章](iot-hub-device-sdk-c-iothubclient.md)中所涵蓋的主題。 hello 重點是，所有這些功能的作用中 hello 相同方式與 hello**序列化程式**文件庫以 hello 一樣**IoTHubClient**程式庫。 例如，如果您想 tooattach 屬性 tooan 事件從您的模型，您使用**IoTHubMessage\_屬性**和**對應**\_**AddorUpdate**，hello 相同方式就像先前所述：

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Hello 事件是否從 hello 產生**序列化程式**程式庫建立或手動使用 hello **IoTHubClient**程式庫並不重要。

Hello 交替使用的裝置認證**IoTHubClient\_LL\_建立**一樣能夠運作為**IoTHubClient\_CreateFromConnectionString**的配置**iot 中樞\_用戶端\_處理**。

最後，如果您使用 hello**序列化程式**程式庫，您可以設定與組態選項**IoTHubClient\_LL\_SetOption**就像您未使用 hello時**IoTHubClient**程式庫。

功能的唯一 toohello**序列化程式**文件庫中的 hello 初始化應用程式開發介面。 您可以開始使用 hello 程式庫之前，必須先呼叫**序列化程式\_init**:

```
serializer_init(NULL);
```

此動作必須正好在呼叫 **IoTHubClient\_CreateFromConnectionString** 之前執行。

同樣地，當您完成使用 hello 程式庫，您要進行的 hello 最後一次呼叫太**序列化程式\_deinit**:

```
serializer_deinit();
```

否則，所有的 hello 上面所列的其他功能工作相同的 hello hello**序列化程式**程式庫在 hello **IoTHubClient**程式庫。 如需這些主題的詳細資訊，請參閱 hello[前一篇文章](iot-hub-device-sdk-c-iothubclient.md)本系列。

## <a name="next-steps"></a>後續步驟
本文說明在詳細資料 hello 唯一的層面 hello**序列化程式**hello 中所包含的程式庫**C 的 Azure IoT 裝置 SDK**。提供的 hello 資訊應該充分了解如何 toouse 模型 toosend 事件也可以從 IoT 中心接收訊息。

這也會結束 hello 三部分的系列 toodevelop 應用程式如何 hello **C 的 Azure IoT 裝置 SDK**。這應該是您啟動足夠資訊的 toonot 只有 get，但可讓您瞭解 hello 應用程式開發介面的運作方式。 如需詳細資訊，幾個範例中有 SDK 未涵蓋的 hello。 否則，hello [SDK 文件](https://github.com/Azure/azure-iot-sdk-c)是很好的資源，如需詳細資訊。

toolearn 進一步了解開發的 IoT 中樞，請參閱 hello [Azure IoT Sdk][lnk-sdks]。

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
